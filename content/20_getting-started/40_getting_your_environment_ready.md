+++
title = "Getting your environment ready"
chapter = false
weight = 40
+++


#### Creating Your Environment

**For this workshop, you will need to setup and configure your environment as below:**

1.	Spin AWS Cloud9, leveraging CloudFormation to create source repositories and foundation infrastructure 
2.	Run a few custom scripts.  

This will build the required infrastructure, pipelines and setup that you need for this workshop without any configurations. You can focus on the workshop without worrying about peripherals.

#### Launch AWS Cloud9
There are a number of ways you can provision AWS Cloud9, however, for this workshop, we will use [ AWS Management Console ](https://aws.amazon.com/console/) to create our environment.

**Go to Cloud9 service from AWS Management Console and -**

- Click on Create Environment.
- Enter Name and Description and Click on Next Steps.
- In the Configure Settings section, leave the default values as it is and click on Next Steps.
- Review and click on Create environment.

**INFO:** The creation of Cloud9 environment can take 1-2 minutes depending on the region you are operating from.

You should see the below screen. 

![AWSCoud9](/images/aws-9.png)

Your Cloud9 environment is ready. 

#### Create the source repositories

Now, we need six repositories for the essential code base required for this workshop.

{{% leftcolumn half %}}
**Repository**
- awswrkshp-aut-frontend
- awswrkshp-aut-backend
- awswrkshp-functional-assurance
- awswrkshp-tests-performance
- awswrkshp-tests-security
- awswrkshp-tests-accessibility

{{% /leftcolumn %}}

{{% leftcolumn half %}}
**Contains code for**
- Frontend react application
- Backend micro services
- Test automation code for API, UI & RWD test
- Performance test
- Security test
- Accessibility test

{{% /leftcolumn %}}

{{% spacer %}}
**To create these repositories, run the following commands in Cloud9’s terminal:**
{{% /spacer %}}

```bash text 
# Cloud9’s
```
To verify the repositories, go to [CodeCommit](https://console.aws.amazon.com/codesuite/codecommit/home) in AWS Console where they should reflect as shown below 

**NOTE** – At this point, all the repositories are blank. In the next step, we are going to push the code to these repositories. Screenshot below for reference:

![Repositories](/images/repo-1.png)

#### Pushing the code to source repositories

Run the following commands in Cloud9’s terminal
Command - `to be given by KGV`

**INFO:** This step takes approximately `XX` minute and if successful, you should see the message as below:

`<< Screenshot to be given by Rahul / Saksham >>`

At this point, you should have all the necessary code repositories with the required code base for this workshop. You can refer the README.md file `<< Path to be provided by Rahul / Saksham >>` of each repository to get more information on what the repository contains.

#### Setup Foundation Infrastructure

Now, you are ready to deploy the infrastructure that will be leveraged during this workshop by:

1.	Creating and setting up services such as VPC, Subnets, Elastic IPs, Amazon EC2, Security groups, S3 Buckets, secrets in AWS Secrets Manager and Amazon ECR services.

Copy and paste the following into Cloud9’s terminal to launch a CloudFormation stack

```bash text 
    aws cloudformation  create-stack --stack-name awsworkshopstep2 --template-url https://aws-workshop-trial.s3-eu-west-1.amazonaws.com/CFN2.json --capabilities CAPABILITY_NAMED_IAM
```

Go to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home) console and check the status of your foundation stack creation. It should be “CREATE_IN_PROGRESS”

**INFO:**  This step takes approximately `XX` minute and if successful, you can see the status of STACK as “CREATE_COMPLETE”

![Repositories](/images/stacks.png)

Please click on your stack name and under **Outputs**   Tabs you can see the details of the key services created. Refer screenshot below:

![Repositories](/images/awsworkshop2.png)

Please verify other services as well e.g. S3 Bucket, Secrets in AWS Secrets Manager. 
All the necessary details are also added in AWS Secrets Manager as Secrets so that these values can be utilized throughout the various components that you will build as the part of this workshop.

As a part of this setup, you have also installed SONARQube and a customized reporting dashboard. Both these dashboards are required to check the status and progress of your testing. 

We recommend you to keep these open in your browser throughout the workshop:
- Access SONARQube dashboard : `http://<backendPublicIP>:9000`
- Access Reporting dashboard : `http://<frontendIP>:3777` Please replace the actual IPs from your Output tab in these links (*) to access the dashboards

Well done!! Your environment is now ready to go. 

Let’s kickstart the workshop and delve deeper into the what, why and how of **‘Testing in DevOps’**

