# What is the Cloud Processing Engine (CPE) ?

CPE allows you to distribute and scale processing accross many machines located anywhere (any cloud provider or local). If you have processes that need to scale, then CPE is for you. 

# What can I do with CPE?

You can process things at scale. Any tasks that takes an input and do some processing is eligible for CPE.

Do use CPE, you first need to deploy the CPE stack. Then you can create your Activities (workers) that will handle the processing for your workflow. You can have several types of workers handling different activities in your workflow.

## Example

Transcoding media files (videos, audio, documents, etc) requires processing power on demand and must scale if a lot of transcoding is required. This need gave birth to CPE.

The Cloud Transcode (CT) project implements the transcoding activities (workers) that used by CPE to transcode files to different formats. CT workers download files from AWS S3, transcode them and push them back to S3.

See the Cloud Transcode documentation for more information: https://github.com/sportarchive/CloudTranscode

# Documentation

Read the CPE documentation for more information about CPE and how to:
- Create your workflow
- Create and use your own activities
- Run the stack locally using Vagrant and Docker
- Run the stack at scale in the Cloud

See: http://sportarchive.github.io/CloudProcessingEngine/

# Technology

CPE use the following AWS services:
- [SWF](http://aws.amazon.com/swf/): Workflow mangement. SWF allows you to create processing workflows so you can chain activities. Each activity is handled by a worker who will process a certain task using input data.
- [SQS](http://aws.amazon.com/swf/): Messaging and communication. Clients using the CPE stack can send commands to the stack using SQS to initiate a new workflow for example. They receive job updates, progress, and output results from SQS as well.

Before getting started, you need a good understanding of those two services. Read the AWS documentation.

# High Level Architecture
![Alt text](/../images/high_level_arch.png?raw=true "High Level Architecture")

# Task tracking
Check the project status and tasks on Pivotal Tracker:
- https://www.pivotaltracker.com/n/projects/1044000


