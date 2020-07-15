+++
title = "Step"
chapter = false
weight = 20
+++

#### PIPELINE OVERVIEW
This module will walk you through the assurance of your application functionalities. You will learn how to execute UI-based tests, responsive web design (RWD)-based tests and API tests with an open-source tool stack. 

`<Need pipeline’s technical architecture / workflow image>`

The Functional Assurance pipeline consists of two stages viz. source and build.

With every code change committed to the repository, the pipeline will trigger all the three tests in parallel. Various dependencies and commands required for respective tests are defined in the `buildspec.yml` file in the source code repository. Test automation for all three tests is triggered with open-source tools – Selenium & BDD Cucumber framework:

- UI Automation: `<< count >>` test cases will be executed using AWS CodeBuild and the results will be saved in the directory -  awswrkshp_functional_assurance_ui/target/extent-reports in the target s3 bucket.

- RWD  Automation: `<< count >>` test cases will be executed on mobile compatible application rendered on Chrome web browser and results will be saved in the directory - awswrkshp_functional_assurance_ui_rwd/target/extent-reports in the target s3 bucket.

- API Tests: `<< count >>` test cases will be executed on the AWS CodeBuild and the results will be saved in the directory awswrkshp_functional_assurance_api /target/extent-reports in the target s3 bucket.

#### PIPELINE CREATION AND EXECUTION
Execute the cloud formation template from Cloud9 to automatically create the Functional Assurance pipeline.

```bash text
aws cloudformation create-stack functionalassurance --template-url https://aws-workshop-trial.s3-eu-west-1.amazonaws.com/functionalassurance.js on --capabilities CAPABILITY_NAMED_IAM
```

In the “Resources” tab of Cloud Formation, verify if all resources created are shown with status as “CREATE_COMPLETE” (Refer screenshot). 

![Functional Assurance](/images/Module_3-1.png)

Note - On successful creation of the pipeline, the CFN will auto trigger the execution. You can now view the execution progress by navigating to Pipeline and selecting - codepipeline_Functional_Assurance.

![Pipelines](/images/Module_3-2.png)


You will notice the three tests are being executed in parallel. 

Soon, you will see the Pipeline fails for the UI and RWD tests. 

Navigate to the Build **->** UI_Test **->** Details

![Pipelines Functional Assurance](/images/Module_3-3.png)

Let us debug to re-execute the pipeline.

#### DEBUGGING AND RE-EXECUTION
Access the reporting dashboard page, refresh to see the failure status and the error message:
`<< Show the reporting snapshot and error messages >>`

On AWS console, you can navigate to ‘Tail Logs’   to check the error message as below:
`<< Can we not have this error message from our reporting dashboard instead of AWS console >>`
< org.openqa.selenium.NoSuchElementException: no such element: Unable to locate element: {"method":"css selector","selector":"#productsearch1"} >

This means that the automation script is unable to locate the object on the screen as properties of that UI object have seemingly changed since the last build. This is a very common error and calls for script maintenance.

To fix this issue, navigate to CodeCommit, find the repository **“awswrkshp-functional-assurance”** and edit the file ShopProductsPage.java
**awswrkshp-functional-assurance/src/test/java/pages/ShopProductsPage.java**

Refer screenshot below for more details:

![AWS Functional Assurance](/images/Module_3-4.png)

You will notice at line# 25 as: @FindBy(id = "productsearch1")
Change the productsearch1 to productsearch

Provide the required details like author name, email address and commit message (change description) and click ‘commit changes’.

The Commit Change will automatically trigger the pipeline and this time it will be executed successfully. Refer screenshot below for ‘succeeded’ status updated against each stage.

![CodePipeline Functional Assurance](/images/Module_3-5.png)

TEST REPORT ANALYSIS
You can find in the S3 buckets, the output artifacts i.e. reports and other files, as follows:
`<< Need Screenshot >>`

You can now refresh the reporting dashboard and review the test results for this pipeline. (Refer the screenshot)

![AWS Pipeline Report](/images/Module_3-6.png)

See test summary of the recently executed Functional Assurance pipeline. For detailed report, navigate to ‘More Info’ for the corresponding testing type.

![AWS Pipeline Report](/images/Module_3-7.png)

Click on the icon   on the right side of a test step for the respective image captured during test execution. This feature helps document the test evidence and supports defect reporting, reproduction and debugging.







