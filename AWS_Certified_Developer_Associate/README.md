# Section 3: AWS Certified Developer Associate

### Exercise 16: Working with AWS Cloud9

1. Setup AWS cloud 9 IDE.
2. Check various settings of the IDE.
3. Check if nodeJs is installed.
4. Clone a demo nodeJs app in the IDE.
5. Run the app.
6. Clean the environment by deleting the IDE.

### Exercise 17: NodeJs Development on EC2

1. Create a IAM role with administrative access
2. Create a Security group for HTTP, HTTPS, SSH inward traffic.
3. Launch an EC2 instance using the custom nodeJs AMI.
4. Connect to the instance using SSH.
5. Run the nodeJs app on the instance.

### Exercise 18: 

1. Create Cognito User Pool using AWS Cognito.
2. Attach a new app to the Cognito user pool.
3. Create federated identity pool related to the the user pool.
4. Upload a static website(provided in the lab) to a new amazon S3 bucket.
5. Make the bucket public and host a static website on it.
6. Make changes to app.js to enable User Sign up on the website using the AWS Javascript SDK Cognito Service.
7. Add feature to Sign In and Logout using the AWS Cognito.

#### Exercise 19: Deploying server less app with amazon Dynamo DB

1. Set up a static website on AWS S3.
2. Create a cloudFront distribution using the default SSL and files on S3.
3. Create table in DynamoDb.
4. Set up an app in amazon developers site to set up login via amazon.
5. Create an IAM role that will allow the app to work with the AWS dynamo DB.
6. Update the app code on S3 to include the role Arn information and app web client ID.
7. Upload the updated code to S3 and create an invalidation in AWS cloudFront.
8. Open the app in browser and login with amazon.
9. Click “write to dynamo db” to same user login response info to dynamo db.
10. Finally, clean the env.

#### Exercise 20: Working with DynamoDb using nodeJs aws-sdk

1. Create a table in AWS DynamoDB and create primary and secondary indexes.
2. Add a record in the table.
3. Upload to a Json file, containing records to be uploaded to the newly create table , to an AWS S3 bucket.
4. Create a AWS Cloud 9 environment.
5. Nam install aws-sdk.
6. Using the aws-sdk, find the available tables.
7. Get the uploaded file object from S3 and import it to DynamoDb table.
8. Write and execute a search query using the aws-sdk.
9. Remove the DynamoDb table and clean the rest of the created resources.