---
layout: page
title: Home
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

---

## Continuous Large Scale Software Engineering Experimentation 
Evaluating software engineering tools is a challenging task.
With the growth of large-scale open-source datasets like [Defects4J](https://github.com/rjust/defects4j), [BugSwarm](http://www.bugswarm.org), [Bears](https://github.com/bears-bugs/bears-benchmark), [Bugs.Jar](https://github.com/bugs-dot-jar/bugs-dot-jar) and [GrowingBugsRepository](https://github.com/liuhuigmail/GrowingBugRepository), it is increasingly common to evaluate software engineering tools (e.g. program repair, fault localization, regression testing, fuzzers, test generation, etc) on huge datasets.
In total, there might be thousands of different workloads that a researcher would like to evaluate their tool on, and if the tool takes several minutes to run, this evaluation can quickly become a multi-week effort to run.
Parallelizing large experiments to use cloud or on-premises compute clusters requires specialized knowledge of distributed systems, and often results in scripts that are tightly coupled to a particular infrastructure. 
Scripting these evaluations so that they can be repeated is also a tremendous challenge: an experiment might depend on third-party dependencies that could disspear or change over time, and creating sufficient documentation to allow newcomers to understand how to run the tool is a tall order.

CLASSEE.cloud is a project that aims to enable Continuous LAarge Scale Software Engineering Experimentation using cloud resources.
"Devops" and Continuous Integration have become common practices in software engineering.
Whereas traditional software development viewed "testing" as a process that was performed only at the very end of a project, continuous integration workflows have enabled developers to get fast feedback on the quality of each set of changes that they make. 
CLASSEE.cloud will bring continuous integration to researchers building large-scale systems, providing open-source infrastructure and training to automate the most common kinds of large-scale evaluations in Software Engineering research, allowing evaluations of different scales to be easily executed throughout the development process.
Key to the design of this infrastructure is a focus on repeatability - it will be possible for any execution of any experiment to be replicated at any time, by any researcher who has access to that data.

This project is motivated by our past experience (and pain-points) building and evaluating software engineering tools, submitting artifacts, and serving as an artifact evaluation chair.
At ICSE 2022, we organized a birds of a feather session that generated [a great list of challenges and opportunities]({% link resources/icse22bof.md %})
We are currently gathering community feedback to help inform the design of CLASSEE.cloud.
If you are interested in discussing this project further, please reach out to us at [team@classee.cloud](mailto:team@classee.cloud).