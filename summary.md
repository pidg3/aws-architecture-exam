# Summary

This page gives a summary of all AWS services. I was writing this list when studying for the AWS Architect Associate exam and thought other people might find it helpful.

All the below is linked to Regions (geographic region) and Availability Zones (data centres within a specific region; at least 2 per region).

## Compute *

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| EC2 (Elastic Compute Cloud) | Virtual Linux or Windows machine. Can be used flexibly. Other services often use this under the hood e.g. Elastic Beanstalk. | Web application server capable of running server side code
| EC2 Container Service | Container management service supporting docker. Allows running applications on managed cluster of EC2 instances - very scalable. |
| Lightsail | 'Server in a box', essentially a simplified version of EC2 (similar to Linode, Digital Ocean) | Set up a web server without AWS expertise
| Elastic Beanstalk | Provision services necessary to run code. Similar to Heroku | I want to deploy a simple Node API backend |
| Lambda | Function as a Service (FaaS) - run a block of code on demand without having to provision any underlying infrastructure, and with flexible trigger(s). Used for all Alexa skills! | I want to process images on demand without provisioning infrastructure |
| Batch | Allows batch computing jobs to be run, automatically provisions infrastructure and optimises for best resources e.g. CPU/memory focussed (similar to Lambda but for larger workloads) | Overnight analysis of post trading data for a finance company |

## Storage *

Good comparison of S3/EFS/EBS: https://cloud.netapp.com/blog/ebs-efs-amazons3-best-cloud-storage-system

Note EBS (Elastic Block Store) is very similar to EFS, but slightly less 'managed' and can only be accessed from a single EC2 instance. Not included in the table below as strictly speaking it isn't a service in its own right, but is tightly coupled to EC2.

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| S3 (Simple Storage Service) | Blob storage for flat files, accessible from anywhere with an internet connection (as opposed to an EC2 instance only for EBS/EFS) | I need to store a large number of image and video files that are used in my mobile app |
| EFS (Elastic File System) | File based storage - can be shared, and can install databases/applications | I need a single file system that can be shared between different EC2 instances, thus providing greater scalability |
| Glacier | Long term storage - cheap but takes a few hours to retrieve data | I need to store audit logs for 7 years to meet regulatory requirements |
| Storage Gateway | Connect physical on-site storage to S3 | Store rarely used files on S3

## Database *

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| RDS (Relational Database Service) | Managed relational DB service. Can use Postgres, My SQL, MariaDB, SQL Service, Oracle, Amazon Aurora | I need a relational database service to support my application
| DynamoDB | Non-relational DB (noSQL). Scalable and performant | I need an AWS alternative to MongoDB
| Elasticache | Allows data to be cached in the cloud, reduces DB load | Cache data for 'top selling products' for a retailer (provided data does not change often) - avoids a DB query each time
| Amazon Redshift | Data warehouse system, can run reports against data stored here | I want analtics data but don't want to slow down prod by running queries against it

## Networking & Content Delivery *

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| VPC (Virtual Private Cloud) ** | Virtual data centre where assets can be deployed in a secure cloud. Can be connected to one another.
| CloudFront | Content Delivery Network (CDN) - uses 'edge locations' to cache content for users in a given geographical area, thus speeding up their connection (especially if far away from hosting region) | I want to speed up access to my web application
| Direct Connect | Way of connecting data centres to AWS using dedicated lines (very reliable) | AWS as DR solution. Gradual migration to AWS |
| Route 53 | DNS service (DNS uses port 53). Also allows domain registrations | I want to register a domain and publish it to DNS servers |

## Migration

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| AWS Migration Hub |
| Application Discovery Service |
| Database Migration Service (DMS) | Facilitates DB migrations - automatically converts to different formats | I want to move away from an expensive Oracle DB ecosystem to an open source cloud DB e.g. Postgres |
| Server Migration Service (SMS) | Facilitates virtual machine migrations, specifically VMWare virtual machines |
| Snowball | Allows bulk (TB) import/export of data. (Also Snowball Edge for bundled compute capacity and Snowmobile for PB scale) | I want to migrate an established data centre to S3 and only have a 100Mb internet connection

## Developer Tools

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| CodeStar | Templates for development environment | I want to build a simple node application but don't how to provision the infrastructure |
| CodeCommit | Github copycat |
| CodeBuild | Compile code in different environments |
| CodeDeploy | Deploy code to EC2 instances in automated/regulated fashion |
| CodePipeline | Keep track of of different verions of code | I need to manage different environments e.g. UAT / Dev / Prod |
| X-Ray | Analyse requests to distributed application | I want to see where in my microservices appplications errors are originating |

## Management Tools *

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| CloudWatch | Monitor performance of AWS environment, especially EC2 | I need to see which EC2 instances are being utilised the most so I can deploy extra servers |
| CloudFormation | Infrastructure as code - document that describes your AWS environment (CloudFormation template) | Can provision production environment for new product |
| CloudTrail | Audit logs | I want to see who created a new user |
| Config | Automatically monitors environment and warns when required | Generate alerts when a deployment breaks company policy |
| Opsworks | Automated deployments using Chef
| Service Catalog | For larger enterprises - set up what should be authorised or not | I want to only allow Ubuntu EC2 instances, no Windows |
| Trusted Advisor | Automated advice - scans environment and gives tips
| Managed Services | Infrastructure operations management for AWS | I want to outsource my entire IT function to AWS |

## Security, Identity & Compliance *

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| IAM (Identity and Access Management) ** | Primary tool to change user permissions | I need to create a new user type for 3rd party contractors |
| Inspector | Inspects virtual machines and reports on security |
| Certificate Manager | Generates free SSL certificate for domains |
| Directory Service | Connect Microsoft AD to AWS | I want to avoid managing users in two different locations |
| Directory Shield |
| WAF (Web Application Firewall) & Shield | Give application level protection (as opposed to network level protection) to an application | I want to guard against application level threats e.g. SQL injection |
| Artifact | Get security certifications for your AWS environment | I need to demonstrate PCI DSS compliance for my auditors |
| Amazon Macie | Uses ML to discover, classify and protect sensitive data (currently S3 only) | I want to see where my security risks for PI information are |
| CloudHSM | Managed hardware security model, manage encrption keys for secure environment | Protect private keys for an issuing Certification Authority |

## Analytics

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| Athena | Run SQL queries over S3 buckets | Test a new data source to make sure structured correctly / run queries over web logs to analyse a performance issue
| EMR (Elastic MapReduce) | Managed big data framework (Hadoop/Apache Spark etc) | Any big data applications - financial analysis, scientific analysis etc
| CloudSearch | An out of the box search engine that can be added to a website/applicaton | Need to search products |
| ElasticSearch Service | Same as CloudSearch but not fully managed | I know a bit more about search engines so won't use CloudSearch |
| Kinesis | Stream and analyse real time data at scale | Analyse financial markets in real time / real time sentiment analysis for election |
| Data Pipeline | Moves data from one place to another | Need to move data from S3 to a more structured DB |
| QuickSight | Business analytics tool | I want to create rich visualisations and dashboard for my users |
| AWS Glue | Fully managed extract, transform and load (ETL) service | Transform semi-structured log data and load into data warehouse |

## Artificial Intelligence

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| Lex | Voice recognition (used by Alexa)
| Amazon Polly | Text to speech conversion | An e-learning application / Alexa voice rendering |
| Rekognition | Identity what pictures are of | Facial recognition for an app |
| Machine Learning | Analyse datasets for given outcomes - can then predict future outcomes | Want to see how likely visitors to a website are to make a purchase based on historic demographic data |

## Internet of Tings

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| AWS IoT | Managed cloud platform for IoT devices | I want to connect my IoT devices up to other AWS services e.g. Lambda functions |
| AWS Greengrass | Software for running locally on IoT devices | Want to run Lambda function on device even without an internet connection |

## Contact Center

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| Amazon Connect | Contact centre | I want to outsource customer contact with a simple workflow (e.g. taking payments) and combine with Lex voice recognition |

## Game Development

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| Amazon GameLift |

## Mobile Services

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| Mobile Hub | Separate AWS console specifically for mobile apps |
| Cognito | Out of the box user authentication, including OpenID | I don't want to roll my own user login module |
| Device Farm | Literally a farm of device for testing purposes | I want to check my app works on multiple Android devices |
| Pinpoint | Collect and analyse app usage data, including mixpanel style funnels, engagement etc (now includes Mobile Analytics, previously a separate service) | I want to understand conversion % once a user adds an item to their basket |

## Application Services

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| Step Functions | Way of visualising what is happening inside an application |
| SWF (Simple Workflow Service) | Way of defining a workflow, can mix manual and automated steps (what is used within Amazon warehouses)
| API Gateway | Create publish maintain and secure APIs | I want to provide a single API with multiple backends / I want to mock API endpoints for development purposes
| Elastic Transcoder | Video formatting to suit all different devices | I want to record one video and ensure it formats correctly |
| Amazon Appstream 2.0 | Stream applications directly to users

## Messaging *

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| Simple Queue Service (SQS) ** | Decouple applications via a queue system | Manage load to an EC2 server - if it fails, route to another server |
| Simple Notification Service (SNS) ** | Notifification by email or SMS |
| Simple Email Service | Send and receive emails |

## Business Productivity

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| WorkDocs | Securely store documents using S3 (with additional security)
| WorkMail | Exchange for AWS |
| Amazon Chime | Conference calling |


## Desktop & App Streaming *

| Name  | Description | Example use case |
| ------------- | ------------- | ------------- |
| WorkSpaces | VDI on AWS - desktop in cloud so can use thin client machines without a local OS |
| AppStream 2.0 | Stream desktop applications to users |
