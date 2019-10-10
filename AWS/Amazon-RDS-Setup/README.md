# AWS account setup to consume Amazon RDS PostgreSQL

## Description

In order to consume Amazon RDS PostgreSQL from SAP Cloud Platform, it is essential that the instances are created within a [Public Subnet in a AWS Virtual Private Cloud (VPC)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html). 

The network setup required on the AWS account and the steps to achieve this are already detailed in [SAP Help documentation](https://help.sap.com/viewer/b392039670364098a722cad3071c7af9/Cloud/en-US/3a2c613c220d4320af584435a79dbffb.html).

As the above manual procedure tends to be error-prone, we provide a [AWS CloudFormation template](https://aws.amazon.com/cloudformation/aws-cloudformation-templates/), for quick and reliable provisioning of the VPC setup in your AWS account. 

## Requirements

* An Amazon Web Services (AWS) account, procured from Amazon - **BYOA**
* Administrator access to the AWS account.
* An [AWS IAM](https://aws.amazon.com/iam/) User with the following IAM [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) assigned (as a minimum)
	* *AWSCloudFormationFullAccess*
	* *AmazonVPCFullAccess*
	* *AmazonS3FullAccess*

<img src="/AWS/Amazon-RDS-Setup/img/AWSIAMPolicy.png">

## Download and Use

* Clone or Download the CloudFormation template file **backserv-vpc-cloudformation-template.yml** from this repository.
* Sign-in to the AWS Console of your account with the IAM user created above.
* In the AWS Console, in the ***Services*** dropdown and search for the service '**CloudFormation**'.
<img src="/AWS/Amazon-RDS-Setup/img/CloudFormation.png">

* Select ***Stacks*** in the navigation pane and click **Create Stack**. 
<img src="/AWS/Amazon-RDS-Setup/img/Stack.png">

* Under ***Prerequisite - Prepare Template*** section, select **Template is ready**
* Under the ***Specify template***, pick **Upload a template file**.
* Click **Choose file** to select and upload the CloudFormation template from your local system to Amazon S3.
<img src="/AWS/Amazon-RDS-Setup/img/CreateStack.png">

* Choose **Next**.
* Enter a **Stack name** and fill in the **Parameters** as you feel necessary. Choose ***any 2 Availability Zones (AZ) or choose 2 AZs of your choice***. Note that you choose the CIDR ranges so that they do not overlap with any other VPC in your account. 
<img src="/AWS/Amazon-RDS-Setup/img/StackDetails.png">

* Choose **Next**.
* Choose **Next** on ***Configure stack options*** screen.
* Run the template by choosing **Create stack** on ***Review Test*** screen.
* Wait until the run completes with status **CREATE_COMPLETE**. You can monitor the run from the ***Events*** tab.
<img src="/AWS/Amazon-RDS-Setup/img/StackComplete.png">

* Note the VPC id from the export of the run in the ***Outputs*** tab. This will be used in the creation of a Resource Provider on SAP Cloud Platform.
<img src="/AWS/Amazon-RDS-Setup/img/StackOutput.png">


## Known Issues

There are no known issues with using this project.

## Support

The project is delivered on an "AS IS" BASIS, WITHOUT WARRANTIES, SUPPORT OR CONDITIONS OF ANY KIND, either express or implied.