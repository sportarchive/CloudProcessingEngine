[![Join the chat at https://gitter.im/sportarchive/CloudProcessingEngine](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/sportarchive/CloudProcessingEngine?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/sportarchive/CloudProcessingEngine/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/sportarchive/CloudProcessingEngine/?branch=master)

# What is the Cloud Processing Engine (CPE) ?

CPE allows you to run workflows and distribute processing accross many machines located anywhere (any cloud provider or local). If you have processes that need to scale, then CPE is for you. 

# Technology

CPE use the following AWS services to run your tasks at scale:
- [SWF](http://aws.amazon.com/swf/): Workflow mangement. SWF allows you to create processing workflows so you can chain activities. Each activity is handled by a worker who will process a certain task using input data.
- [SQS](http://aws.amazon.com/sqs/): Messaging and communication. Clients using the CPE stack can send commands to the stack using SQS to initiate a new workflow for example. They receive job updates, progress, and output results from SQS as well.

Before getting started, you need a good understanding of those two services. Read the AWS documentation.

# How to use it?

To use CPE, you need to deploy the CPE stack which is composed of three components:
   - **Decider:** Listens to Amazon SWF and make decision on "what's next" in your workflow. The decider is not in this repository. It can be accessed here: https://github.com/sportarchive/CloudProcessingEngine-Decider
   - **InputPoller:** Listens to Amazon SQS for commands from your client applications. Your client apps can start new workflows by sending a `start_job` command along with some JSON payload.
   - **ActivityPoller:** Listens to SWF for incoming tasks. An ActivityPoller is a worker processing a certain type of ActivityTask (Read SWF doc). You can have many running. They all listen on a particular queue (TaskList) and only process tasks assign to them by SWF.

Each ActivityPoller executes Activities that you develop. You must create an Activity for each type of task your workflow will handle. So you can have several types of workers handling different type of activities in your workflow. Each worker is a daemon that run on a box or in a Docker container, locally or in the Cloud.

Workflows are arbitrary and are defined using a YAML plan that you must write yourself. A plan defines your workflow steps and which ActivityPoller type will execute each step. Input and Output data can be passed on from one activity to another.

## Example

Transcoding media files (videos, audio, documents, etc) requires processing power on demand and must be elastic if a lot of transcoding is required. This business requirement gave birth to CPE.

The Cloud Transcode (CT) project implements activities (workers) in charge of transcoding media files. The ActivityPoller loads those activities and use them to process incoming transcoding tasks. CT activities download the media files from AWS S3, transcode them at scale and upload them back to S3.

See the Cloud Transcode documentation for a working example of CPE activities and more information: https://github.com/sportarchive/CloudTranscode

# Documentation

Read the detailed CPE documentation for more information about CPE and how to:
- Create your workflow and define your YAML plan
- Create and use your own activities
- Run the stack natively or using Docker
- Run the stack at scale in the Cloud

See: http://sportarchive.github.io/CloudProcessingEngine/

# High Level Architecture
![Alt text](/../images/high_level_arch.png?raw=true "High Level Architecture")

# Task tracking
Check the project status and tasks on Pivotal Tracker:
- https://www.pivotaltracker.com/n/projects/1044000


