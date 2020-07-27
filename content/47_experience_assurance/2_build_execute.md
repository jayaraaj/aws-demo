+++
title = "Build & Execute"
chapter = false
weight = 2
+++


#### PIPELINE CREATION AND EXECUTION

Execute the cloud formation template from Cloud9 to automatically create the Experience Assurance pipeline.

```bash text
aws cloudformation  create-stack --stack-name ExperienceAssurance --template-url https://aws-wrkshp-artifacts.s3-eu-west-1.amazonaws.com/awsworkshop_infrastructure_artefacts/awsworkshop_experience_assurance.json --capabilities CAPABILITY_NAMED_IAM
```




**INFO**: This step takes approximately ~1 minute and if successful, you can see the status of STACK -  'ExperienceAssurance' as {{% color success %}}“CREATE_COMPLETE”{{% /color %}}, as in the screenshot below:



![](/images/module4/b-1.png)


**Note**: On successful creation of the pipeline, the CFN will also auto trigger the execution. You can now view the execution progress by navigating to [CodePipeline](https://console.aws.amazon.com/codesuite/codepipeline/home) and selecting 


![](/images/module4/b-2.png)

You will notice the pipeline fails at security testing and thus the subsequent step for accessibility test is not executed. 

![](/images/module4/b-3.png)

Let us fix this issue to re-execute the pipeline and check the overall non-functional impact of the code change committed.

{{% notice tip %}}
Additionally, Practitioners can access Cognizant Thought Leadership on Performance Testing for SaaS-based Applications, please review the insightful blog by our technology expert on [“Performance Assurance for SaaS-based Applications”](https://www.linkedin.com/pulse/performance-assurance-saas-based-applications-leo-peter/?published=t). 
{{% /notice %}}
