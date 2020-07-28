+++
title = "Build & Execute"
chapter = false
weight = 2
+++


#### PIPELINE CREATION AND EXECUTION
Execute the cloud formation template from Cloud9 to automatically create the Functional Assurance pipeline.

```bash text
aws cloudformation  create-stack --stack-name FunctionalAssurance --template-url https://aws-wrkshp-artifacts.s3-eu-west-1.amazonaws.com/awsworkshop_infrastructure_artefacts/awsworkshop_functional_assurance.json --capabilities CAPABILITY_NAMED_IAM
```

Go to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home) console and check the status of your pipeline stack creation named 'FunctionalAssurance'. It should state - {{% color info %}}“CREATE_IN_PROGRESS”{{% /color %}}


**INFO**: This step takes approximately 1 minute and if successful, you can see the status of STACK as {{% color success %}}“CREATE_COMPLETE”{{% /color %}}, as shown in the screenshot below: 



![Functional Assurance](/images/module3/Module_3-1.png)

**Note** - On successful creation of the pipeline, the CFN will auto trigger the execution. You can now view the execution progress by navigating to Pipeline and selecting - codepipeline_Functional_Assurance. 


![Pipelines](/images/module3/Module_3-2.png)


You will notice the three tests are being executed in parallel. 

Soon, you will see the Pipeline fails for the UI and RWD tests. 

Navigate to the Build **->** UI_Test **->** Details

![Pipelines Functional Assurance](/images/module3/Module_3-3.png)

Let us debug to re-execute the pipeline.

{{% notice recommonded %}} 
Additionally, Practitioners can access Cognizant Thought Leadership on CI/CD for Web Services Testing, by referring the insightful whitepaper by our technology experts titled - **“Continuous Integration and Continuous Delivery to Facilitate Web Service Testing”**.  You will find the link to the whitepaper in the Register with Cognizant page -[https://www.cognizant.com/application-modernization](https://www.cognizant.com/application-modernization). 
{{% /notice %}}

