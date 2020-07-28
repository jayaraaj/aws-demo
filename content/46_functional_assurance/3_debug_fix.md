+++
title = "Debug & Fix"
chapter = false
weight = 3
+++


#### DEBUGGING AND RE-EXECUTION
Access the reporting dashboard page, refresh to see the failure status and the error message:
![Report](/images/module3/module_3-debug.png)


{{% icontext trail %}}  icon on AWS console to be used to check the error message below:{{% /icontext %}}

`< org.openqa.selenium.NoSuchElementException: no such element: Unable to locate element: 
{"method":"css selector","selector":"#productsearch"} >`

Such errors indicate that the automation script is unable to locate the object on the screen as properties of that UI object have seemingly changed since the last build. This is a very common error and calls for script maintenance.

Navigate to the report to see the error: 
- Navigate to Dashboard **->** UI Test Report Section **->** Click “**More Info**” **->** User will be able to see the report with the error


To fix this issue, navigate to [CodeCommit](https://console.aws.amazon.com/codesuite/codecommit/home), find the repository **“awswrkshp-functional-assurance”** and edit the file ShopProductsPage.java
**awswrkshp-functional-assurance/src/test/java/pages/ShopProductsPage.java**

Refer the screenshot as shown below for details:

![AWS Functional Assurance](/images/module3/Module_3-4.png)

You will notice at line# 25 as: @FindBy(id = "productsearch1")
Change the productsearch1 to productsearch

Provide the required details like **author name**, **email address** and **commit message** (change description) and click **‘commit changes’**
. 
![Commit Changes](/images/module3/Module_3-4-1.jpg)
The Commit Change will automatically trigger the pipeline and this time it will be executed successfully. Refer the screenshot as shown below for ‘succeeded’ status updated against each stage.

![CodePipeline Functional Assurance](/images/module3/Module_3-5.png)






