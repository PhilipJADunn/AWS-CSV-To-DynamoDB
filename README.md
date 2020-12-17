# AWS-CSV-To-DynamoDB

Bulk upload a CSV file into DynamoDB using S3 and a Lambda function via IaC.

First of all we want to zip our code and upload it into an S3 bucket, this will be referenced in our YAML file on the line under 'Code:' and then we are going to upload our YAML template file in CloudFormation:

![1  Create Stack](https://user-images.githubusercontent.com/68379635/102357104-e9d2eb80-3fa5-11eb-9c89-f93d61bd917a.PNG)

It's also a good opportunity to view what resources will be created in the Designer tab:

![3  Stack in Designer](https://user-images.githubusercontent.com/68379635/102358175-1cc9af00-3fa7-11eb-89a9-7a017e3cfc37.PNG)

Next we have to specify the parameters set out in the YAML file:

![2  Parameters](https://user-images.githubusercontent.com/68379635/102357372-243c8880-3fa6-11eb-8ef9-2defa5d12830.PNG)

After this we can create our CloudFormation stack and we can see services being created in the Events tab, note that this can fail if the S3 bucket parameter you choose is already in use by somebody else:

![4  Resources being created](https://user-images.githubusercontent.com/68379635/102358810-db85cf00-3fa7-11eb-833a-9ad47b5b568e.PNG)

After this is created, we can go to DynamoDB and see our table with the partition key of uuid, as per the AttributeName defined in our YAML file, this can be anything you want/need depending on your needs for your CSV file but it should match the first column of your CSV file:

![5  DynamoDB Table](https://user-images.githubusercontent.com/68379635/102359505-c9586080-3fa8-11eb-9f3b-d0a815aada62.PNG)

Next we'll take a look at the environment variables for our Lambda function:

![6  Environment Variables](https://user-images.githubusercontent.com/68379635/102359857-35d35f80-3fa9-11eb-8523-7ae1d36ade8f.PNG)

We now want to go to our S3 bucket and upload our testfile.csv file:

![7  Upload CSV from S3](https://user-images.githubusercontent.com/68379635/102360838-6ec00400-3faa-11eb-9355-21c062e45463.PNG)

When this is uploaded the Lambda function takes the data and inserts it into our CSVDynamoDB table:

![8  DynamoDB Table CSV](https://user-images.githubusercontent.com/68379635/102361513-38cf4f80-3fab-11eb-9a85-d2bac7250c24.PNG)

Note if you are testing this with a large CSV file I would suggest deleting the table afterwards instead of trying to batch delete data so you can avoid charges.

Finally we can take a look at our CloudWatch logs for the Lambda function to see some details regarding the execution:

![9  CloudWatch Log](https://user-images.githubusercontent.com/68379635/102362485-5a7d0680-3fac-11eb-9795-34efece49edc.PNG)
