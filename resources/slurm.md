---
layout: page
title: CI on HPC with Slurm
permalink: /resources/slurm/
parent: Resources
---
## Running GitHub Actions CI Runners with Slurm
Many institutions maintain large clusters of computers designed for high performance computing workloads.
Access to resources in these clusters is typically managed by a workload manager, like the popular (and open-source) [Slurm](https://slurm.schedmd.com).
These systems allow users to submit batch jobs --- scripts that specify an allocation of compute nodes required for a workload, along with the script to run on each of those nodes.
Successfully utilizing these resources requires an understanding of scientific computing workflows.

In order to utilize our existing, on-campus HPC infrastructure (and avoid paying for cloud resources), we built a prototype application to auto-scale GitHub Actions runners on our Slurm-managed cluster.
This allows us to [execute long-running performance evaluations of our fuzzer in CI]({% link resources/confetti.md %}) on an existing on-premises HPC cluster.

### GitHub Application for Managing CI Infrastructure

This app is trusted by GitHub (must be installed as a GitHub App), and can act on behalf of users who trigger builds on GitHub Actions. [ripley-cloud/gha-slurm-munge](https://github.com/ripley-cloud/gha-slurm-munge) are the components that need to be trusted by Slurm. 

The high level workflow to launch a build runner is:
1. Receive webhook from GitHub that a build is needed, check the labels on the requested runner
2. Generate a self-signed JWT token that encodes the build request, send this to [ripley-cloud/gha-slurm-munge](https://github.com/ripley-cloud/gha-slurm-munge) to request that an actions runner be scheduled to run in Slurm
3. Once the Slurm Job is allocated, the node sends the JWT token back to this app, which checks it, and then if valid, refreshes the GitHub runner token 
4. Actions runner starts and connects to GitHub. If there is no build started within 2 minutes (e.g. if the request was satisfied by another runner outside of our control, or canceled by the user), the job terminates and releases its resources

### CI Service for Slurm

This is a simple web app designed to live inside of your [MUNGE](https://dun.github.io/munge/) domain that will provision an ephemeral GitHub Actions Runner on behalf of a user.

The responsibilities for launching a GitHub Actions Runner for a given repo and talking to GitHub are separated to simplify auditing of the security-critical aspects of this app: the part that talks to Slurm must have permissions of the SlurmUser in order to launch jobs on behalf of other users. There are many other responsibilities that we might want to put in the GitHub App that *do not* require SlurmUser's permission (e.g. operations on each Actions run/pull request/etc, which can be performed using the GitHub Token passed by the webhook). If you are not doing much to change that app, it would be fine to run the two apps on the same machine, both under the SlurmUser's account, but it seemed like a better design choice for flexibility to keep this separate.