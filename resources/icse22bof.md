---
layout: page
title: ICSE 2022 Birds of a Feather
permalink: /resources/icse22bof/
parent: Resources
---
## Report from ICSE 2022 Birds of a Feather meeting

On May 26, 2022, we organized a "Birds of a Feather" [community meeting at ICSE 2022](https://conf.researchr.org/track/icse-2022/icse-2022-birds-of-a-feather?#program) on the topic of "Automating Large-Scale SE Experiment Execution and Artifact Reproduction." We provided a 5 minute overview of the challenges and potential solutions that we have been considering, and for the remainder of the 1 hour session, the 52 attendees of the session discussed their observations and experiences.

Major discussions of challenges included:
* Making it easier to evaluate software engineering tools large open-source software benchmarks doesn't solve the problem of building good benchmarks
* It is hard to motivate researchers to build good, repeatable evaluation experiment scripting and build artifacts. This makes it hard to train new researchers, because there are no good examples to use as lessons.
* Artifacts are vital for bridging the gap from research prototypes to industrial practice
* Shoot for artifacts that allow for easy adaptability in the short-term (e.g. post on GitHub, create a culture that encourages pull-requests), and archivability for the long-term (e.g. create a container with all of the dependencies of the original system, archive it to avoid decay)

The majority of the time was spent discussing the challenges, but the attendees also discussed the applicability of CI to software tool artifacts:
* CI is good because it forces a developer to make the build process explicit and automated
* A service that mapped from CI artifacts to compute resources could allow authors to provide artifact review committee with access to their build cluster to run a replication, and could allow sponsors to provide researchers with compute resources

### Notes
The notes below capture the (unedited) discussion points raised by the attendees.

####  Challenges
* Big challenge for users of different artifact datasets - lack of common interface for running artifacts
* Mismatched incentives for designing reusable/repeatable artifacts - some researchers might build tools to throw them away after a paper + not build on them, resulting in not maintainable
* Benchmark dataset problems - creators of different benchmarks need to be brought together to standardize usage + curation - each of the benchmarks have (differing) embedded assumptions about their intended use. What is the API we should use as benchmark designers?
* Do the evaluations that we design for papers match the actual workflows and challenges of the intended user of the tool? For example, in Fuzzing there are commonly cited suggestions like "Fuzzers should be evaluated for 24h using multiple targets and multiple trials" - but how do we match our evaluation designs to the methodologies that developers follow to use these tools? Maybe they don't do 24h runs and multiple trials.
* Some domains have specific infrastructures for running large software evaluations already, e.g. genomics + scientific workflow management platforms, but we need community buy-in for SE; what is the business case for standardizing these large-scale evaluations?
* How do we train new students who might have the domain expertise to write the software but not the systems expertise to implement the evaluation? Best right now seems to be apprenticeship model (sit with students and let them observe/ask questions as senior person does the scripting)
* Current open science standards have pushed community to publish tool + data, but not necessarily the experimental scripts; examples of effective experimental scripts could be helpful for training - a repository of experiment scripts could be useful for education
* Participating in artifact evaluation provides students an opportunity to observe the good and bad parts of evaluation design. 
* What to do if an experiment involves closed-source and/or proprietary code or data?
* Artifact evaluation is largely grad students - does that indicate that the senior members of the community are invested - do we need the senior members to participate to provide actual training in this role?
	* Some artifact committees mitigate this by pairing junior and senior members to co-review
	* Open calls can help attract broader spectrum of reviewers
	* What are the actual guidelines that we should set to evaluate an artifact? What is maximum effort to expend to find a reviewer, and for reviewer to expend?
* There is a barrier to entry to submitting artifacts, prior studies have shown that many researchers may be entirely turned off from the process.
* Depending on how the experiments are designed, the tool's API/interface might be designed JUST for running on a benchmark, making them hard to execute on new workloads
* How to quantify and replicate experiments that are inherently non-deterministic? What is an appropriate bound?
	* How to ensure that you can get the same kind of results in the end, for example, when totally changing the environment in which the experiment runs?
* What is the goal of the replication? To build trust in the research article and its results, or to create a community resource that someone else can come along and extend?
* Even self-replication is troublesome: something that works today might not work in 3 years even in the same machine. External libraries become problematic, and *licensing* for those third-party libraries can become problematic (e.g. JVM)
* What does "replication" mean in a world where technology adapts so quickly that long-term guarantees will not be possible, particularly when an artifact has particular dependencies
* What is the appropriate standard of effort for a researcher today who is building a new tool that "should" be compared to a prior tool, but that prior tool is not available? Re-implement? Blow it off?
	* Depends on the sensitivity of the approach to implementation-level details - if it's very sensitive to implementation details it's very hard to make a fair re-implementation; also depends on the contribution - if it is necessary to demonstrate the contribution, then perhaps it is necessary to find a way to reimplement
* Should the reproducibility of a result be considered in the paper review standards?
* When reproducing an approach and finding differing results, do you compare to the original results published in the original paper, or of the reproduced results?
	* A re-implementation can be a significant threat to validity, but if you acknowledge it and do best-effort to be fair, that might be best
* Reproduction packages are not always entirely complete - beyond dependencies, ML systems might be missing various parameter settings
* Should there be a trusted external entity that is relied on to run the reproduction/evaluation, no human-in-the-loop? Expensive, but could help solve many challenges
* Artifact evolution is hard- push something on Docker and it's OK, but hard to keep using into the future. Versions of Java, ant, etc can change over time, the students move on, tools are static. Some dependencies become entirely defunct and unmaintained (e.g. cobertura, bcel). Ongoing maintenance of these tools is a hard problem, and each tool needs its maintenance.
* Where is the line between the effort researchers should do to make their work adoptable, versus what industrial practitioners should do to adopt something?
	* Industry is busy; goal is not to do research but to deliver fast ROI and products. Example: Randoop vs SBST in 2007, just before EvoSuite's release; SBST was in research but no well-supported tool for practitioners to apply out-of-the-box. This is not surviving for 25 years, but remaining available for the "now"
* Is it worth the time to build an artifact? Especially if your artifact gets rejected for a silly reason.
  * Artifact evaluation can be used as a training exercise: open communication between reviewers authors and chairs can help elevate artifact quality and train everyone; but potentially a huge effort
  * Artifacts benefit the creator by making something that is available to hand off to new students, to new collaborators, etc who are eager to get involved in a project, and come up to ask those questions *after* the project is completed, and are eager to participate in follow-on work. Particularly good for a student who reads a paper and is interested in the work - good first-step to get involved.
  * Current artifact evaluation process is very focused on replication, but not on helping researchers to craft those tools that are reusable
  * Where is the incentive for building replication packages, if they are not necessary for publication? Why bother, if there is no guarantee that nobody will come and use it?
	* It is an essential part of the scientific attitude - we must do it, but figure out what it means; it's important to be able to replicate things in the short-term at least (to confirm that results are sound/correct). What is the expected lifespan of an artifact?
	* Lifespan varies based on your goal: Trust + transparency in publication vs to create new artifacts derived from this one in the future?
* What are the requirements for getting involved to make a pull request on someone's GitHub artifact?
	* Example of how to do it: 1. Send an email describing what was done and asking if this is something that is interested to be made and outlining a few options of why and tradeoffs in the design, have a conversation 2. Open PR
    * Create a welcoming environment for open science, avoid the toxic comments about "wasted time" on artifacts
* Depending on the intended use of the artifact, it should be packaged differently:
	* Long term archiving (tarball on Zenodo)
	* Short-term extension and reuse (GitHub)
		* This is where a lot of the benefit comes from - this is where you can get that third-party pull request that improves your work!
		* At some point it might "sunset", but that is OK
        * There are many examples of external factors shifting that entirely deprecate a tool (e.g. HW architecture change, JVM version change, TLS deprecation)
    	* Even if picked up by industry, this is still a problem (perhaps even more so if they really want it to work!)

#### What about continuous integration as a framework for artifacts?
* Good: forces you to make build process explicit, mechanical and automated. 
* Note: To ensure robustness make sure that it can be compiled without internet access
* Could be useful as a standard mechanism for provisioning resources, making it easier for artifact evaluation committees to run the artifact (PLUS it could simplify the process of allowing reviewers to re-execute the artifact using author-provided resources, or enable a sponsor to provide those resources)
* Broader impact for artifacts - helps to enable adoption (not just replication) - practitioners want something that they can play with _now_, not something that has a huge readme and complex requirements to run. Easy replication is the first step to easy reuse.
* Unresolved challenge - We still have problem of: what is the ground truth for "does this tool actually work in the real world?" We still have to figure out benchmarks and evaluation methodologies. But, making that experiment repeatable is a big step to understanding and characterizing the tool's performance 
* Positive example for tool adoption: Pitest is a mutation testing tool ("research" tool, developed in industry) that is in fact used in many organization; quoted as due-to the presence of the maven plugin making easy to integrate in CI