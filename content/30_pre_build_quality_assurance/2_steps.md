+++
title = "Steps"
chapter = false
weight = 2
+++

#### PIPELINE OVERVIEW

Pre-Build Quality Assurance CodePipeline aims at embedding automated quality measures right at the beginning of the SDLC to help detect and fix bugs early, thereby building in a stable and resilient code. 

In this section, you will learn how to execute static code analysis, unit testing, sanity UI testing and measure code coverage with an open-source tool stack. 

`<< Need pipeline’s technical architecture / workflow image >>`

The Pre-Build Quality Assurance CodePipeline consists of the following stages and components:
1.	**Source Stage** monitors changes to below source code repository for any new commits 
    - **FrontEndreactApp** – Code for front-end application
    - **BackEndSprintBootApp** – Code for backed microservices 
When a new commit (or a new code change) is detected, a CodeBuild job will be triggered.

2.	**Pre-Build Quality Check** uses SonarQube for continuous inspection of code quality and perform automatic reviews with static code analysis to detect bugs, code smells and security vulnerabilities for both front-end and back-end code. 
Separate CodeBuild jobs i.e. **ReactAppSonarCheck** and **SprinBootSonarCheck** are created to induce static code quality measures on both the components of application under test.

3.	**Unit Test** is a series of tests configured as CodeBuild actions i.e. **ReactAppUnitTest** and **SprinBootUnitTest** that validate all parts of the application under test. In case of issues, this phase of the CodePipeline process is ended with a failure status. If no issues are detected, the pipeline proceeds to the build stage.
Enzyme and Jest libraries are used for unit testing of the front-end. Similarly, Junit and Mockito is used for the back-end micro services. 

This stage is also complimented with code coverage tools such as Jacoco for back-end and Jest for front-end code for actionable guidance and identifying critical slips. You will be able to see the status of these tests on the reporting dashboard and the code coverage on SONARQube dashboard.

4.	**Build** commences with the creation of Docker image for front-end applications. When a new Docker image is successfully built, it is pushed to Amazon ECR.

5.	**Deploy to Fargate** deploys the image carted in the build stage o AWS Fargate cluster, which spins up the following two containers -. **frontendapplication** and **virtualizedbackend** with the latest image.
At this stage, front-end application is pointing to a virtualized back-end so that tests can be executed without back-end dependencies - one of the key advantages of virtualization.

A portion of developers’ UI tests are also executed using playwright and Jest at this stage to ensure the front-end image is properly built and running along with virtualized back-end.

ECS and the Application Load Balancer will continuously monitor the health of the container and the application and will make required adjustments to keep optimal healthy container tasks running at all times.


#### PIPELINE CREATION AND EXECUTION

To deploy the pipeline, run the following commands in Cloud9’s terminal:

```bash text
aws cloudformation  create-stack --stack-name awsworkshopprebuildqa --template-url https://aws-workshop-trial.s3-eu-west-1.amazonaws.com/CFN3.json --capabilities CAPABILITY_NAMED_IAM 
```

Go to the CloudFormation console and check the status of your pipeline creation. It should state -  “CREATE_IN_PROGRESS”

**INFO:** This step takes approximately `XX` minute and if successful, you can see the status of STACK as “CREATE_COMPLETE”, as in the screenshot below

![Cloudformation](/images/Module_1-1.png)

Please click on you stack name. Under Outputs tabs, details of the key services created will reflect. Refer screenshot below:

![AWS workshop prebuildqa](/images/Module_1-2.png)

All the necessary details are also added in AWS Secrets Manager as Secrets, so that these values can be utilized throughout the various components that we will build as the part of this workshop.

At this point, you should also have an automatically triggered, fully-functioning Pre-Build-QA CodePipeline. 

If you head over to CodePipeline in the AWS console and click on the pipeline that begins with the name workshop-**codpipeline_prebuildqulaitycheck**, you should see this screen:.

![AWS workshop prebuild quality check](/images/Module_1-3.png)

You will notice that the Pipeline fails at the UnitTest stage - ReactAppUnitTest and thus the subsequent steps (Build and Deploy to Fargate) are not executed.

Let us debug and fix this issue to re-execute the pipeline and then see the impact on subsequent stages.

#### DEBUGGING AND RE-EXECUTION

To debug the issue, from the AWSCodeBuild you can go to CodeBuild section -> BuildHistory and click on the latest failed link under **Build Run**. 

You can then view the below report. Click on the failed test case to see the reason for failure.

![AWS workshop Unit Test](/images/Module_1-4.png)

Alternatively, please switch to your Reporting Dashboard and go to the section UnitTest to view the summary of this stage. Click on the component to view detailed test report to spot where the test failed. (This will link you to the above report)

`<<Snapshot of the Reporting Dashboard >>`

Let’s understand the nature of the failure.

**What is the failure?**
One of the unit tests named **‘Register - Last name should be present’** has failed because the ID of the UI object is incorrect while the unit test was written. 

Instead of **‘lastname’**, the developer has updated it to **lastname1**.

**AWS CodeBuild Logs**
![Register Test](/images/Module_1-5.png)

**How to fix it?**
Go to “AWS CodeCommit’ and navigate to below path:

**awswrkshp-aut-frontend -> test -> applicationcomponents -> testscripts -> unit_tests -> containers** and look for the file Register.test.js. This file has unit tests related to ‘registration’.

To fix this issue, go to line number 60 and change **‘lastname1’** to **‘lastname’**. (Refer screenshot):
![How to Fix](/images/Module_1-6.png)


Great, you have now debugged and fixed the issue. 

Provide required details such as **author name, email address** and **commit message** (change description) and click **‘commit changes’**.
![Edit a File](/images/Module_1-7.png)

The Commit Change to the **Register.test.js** file will trigger the pipeline automatically and this time, it will execut without errors. Refer screenshot below for ‘succeeded’ status updated against each stage.

![Register Test](/images/Module_1-8.png)

With the succesful execution of the pipeline, you should have a working instance of your application under test, deployed in ECS. 

To access the application, replace the value of key **‘ECSALB‘** which you have noted in output section of the **Pre-Build Quality** section in below URL:
- **Application Under Test URL is**  -  `http://<ECSALB Value>:3000`

![Register Test](/images/Module_1-9.png)

#### TEST REPORTS ANALYSIS

To view the CodeQuality and test coverage reports, use SONARQube dashboard for code quality metrics. 

Refer the screenshot below for more details:

![Test Report](/images/Module_1-10.png)

To view the details of unit test, use the reporting dashboard for all statistics .

Refer the screenshot below for more details:

![Statistics](/images/Module_1-11.png)







