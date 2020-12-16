# CSV-To-DynamoDB

Bulk upload a CSV file into DynamoDB using S3 and a Lambda function via IaC.

First of all we want to zip our code and upload it into an S3 bucket and then we are going to upload our YAML template file:

![1  Create Stack](https://user-images.githubusercontent.com/68379635/102357104-e9d2eb80-3fa5-11eb-9c89-f93d61bd917a.PNG)

Next we have to specifies the parameters set out in the YAML file:

