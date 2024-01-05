# Links

* Courses:
  * https://digitalu.udemy.com/course/aws-certified-sysops-administrator-associate-training/
    * The main course and the one the code came from 
* Practice Tests:
  1. https://digitalu.udemy.com/course/aws-certified-sysops-administrator-associate-aws-practice-exams
  2. https://digitalu.udemy.com/course/practice-exams-aws-certified-sysops-administrator-associate
  3. Main course has a practice test
  4. Maybe (it's getting expired soon): https://digitalu.udemy.com/course/aws-sysops-admin-associate-3-full-practice-tests/

# Notes
Hoping to note out some main study points that I realize I don't know from the practice tests that are much harder than the course content.
Goal is a study guide for things I didn't learn enough of to go back and read more on later. 

Noted: 2.1-2
Score: 
* 2.1: 41
* 2.2: 60


* ASG
  * Scale-in (protection) - making it smaller (but doesn't delete any)
  * may terminate instances that are stopped, pause if you are updating an instance
  * launch process can get suspended 

* Athena 
	* Analyze data where it's at
	* serverless
* Beanstalk
  * Default scaling is based on network traffic (high or low)

* CloudFormation
  * Stack policy - defines what can be done on some resources to prevent unintentional updates, have to specify them explicitly
  * Change set - show changes from last deployed set, deleted after successful deployment
  * Stack set - act across multiple accounts and regions
  * Resource Import - bring in things you already have
* CloudFront
	* Configure log files to contain every request info
	  * Remove quickly - invalidate the file then serve a new file
	  * caches for 24 hrs
	  * Use custom origin or origin access identity to require it's use for s3
	  * Errors if you move buckets from one region to another, have to update the CF distribution
* CloudWatch
  * Can have two config files - different file names
  * Events - do things on a schedule
  * Synthetics - Creates canaries - scripts that run on a schedule to monitor endpoints and APIs
  * ServiceLens - enhances observaibility by integrating traces, metrics, logs, alarms
  * Metrics:
    * Bandwidth: NetworkIn, NetworkOut
    * Disk Use: DiskReadBytes, DiskWriteBytes
    * Status: StatusCheckFailed is combination of StatusCheckFailed_Instance and StatusCheckFailed_System
    * CPUUtilization
    * Custom: StatsD for L/W, CollectD for L
    * Custom metrics via CLI or API
	* Agent
	    * CloudWatchAgentServerRole - IAM role for EC2 instances
	    * Custom metrics via CLI or API
	    * Agent
		    * Preinstalled on some AMIs, can be installed
		* Events - do things on a schedule
			* e.x.: snapshot EBS
		* Synthetics - Creates canaries - scripts that run on a schedule to monitor endpoints and APIs
		* ServiceLens - enhances observaibility by integrating traces, metrics, logs, alarms
* Config - 
	* keeps track of configuration and relationships to other resources and evaluates for compliance
	* Auto Remediation to fix things that aren't right

* EC2
  * DisableApiTermination: stops termination from API, CLI, UI
  * Detailed monitoring for 1 minute logs to CW
  * Health checks cover the instance, not any applications 
  * Status checks can not be disabled
  * T2 unlimited - CPU better for longer
  * Enhanced Networking - many packets per second
  * Cluster placement group - fast inter-ec2 networking
* ELB
  * 503 if no registered targets
  * routes to unhealthy if there are no healthy
* EventBridge - Something happends, send trigger to something else (Lanbda, SNS, etc)
  * Sending to Kinesis - requires IAM role
  * Sending to anything else - configure resource-based policy 

* Gateways
	* Volume - iSCSI
	* Egress Only Internet Gateway - IPv6
* IAM
  * Resources must be globally unique named
  * Policies
	  * identity based apply to user, group role
	  * resource based apply to things, buckets, keys, etc.
	  * to access things cross-account: need identify based on user, and resource based on object
* Inspector
	* check security state 

* Lambda
  * Not self-invoking

* Site to site
	* direct connect - physical
	* The rest - can be software VPNs
* Systems Manager
	* Collect metadata about instances 
* RDS
	* parameter groups to enforce SSL
	* Multi-az is HA
* Accidental deleting
  * AMI - can't be recovered, only remade
* X-Ray
	* helps trace app workflows, integrated with S3, ELB, Lambda, APIs. Not ALB. 
* Trusted Advisor
  * monitor against service limints
  * monitor for best practices




