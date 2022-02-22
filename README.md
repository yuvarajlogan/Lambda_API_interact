# Lambda_API_interact
**Build a Basic Web Application**


Deploy a web application and add interactivity with an API and a database
To create the sample web application we require
•	Create a web app
•	Connect the web app to a serverless back-end
•	Add interactivity to your web app with an API and a database
**SERVICES:**
AWS Amplify, Amazon API Gateway, AWS Lambda, and Amazon DynamoDB.

Step 1: Create Web App.
 Deploy static resources for your web application using the AWS Amplify Console.
 Step 2: Build Serverless Function.
	AWS Lambda .
Step 3: Connecting the Function and Web App.
	Deploy Serverless function with API gateway to initiate interaction
Step 4: Create Data Table.
	Collect the data in Amazon DynamoDB table.
Step 5: Add Interactivity to Web app.

**Create An App using AWS Amplify.**

Amplify Hosting is a fully managed hosting service for web apps. Connect your repository to build, deploy, and host your web app.
 ![image](https://user-images.githubusercontent.com/52998388/155178125-59b2649e-7720-4d14-922d-28ac8e19d903.png)

 

Give App name and select the method of uploading the Source Code.
 
 ![image](https://user-images.githubusercontent.com/52998388/155178154-7c4d9df5-bf39-46a2-84fd-974ce4cd6c52.png)


Once completed lets move on to Create Serverless Function for our App.

**AWS Lambda : **

 It is a computing service that runs code in response to events and automatically manages the computing resources required by that code.
 ![image](https://user-images.githubusercontent.com/52998388/155178045-f8021559-a7a1-49c7-ac7f-800d7ce07d46.png)


 
Link a Serverless Function to a Web App:
We use HTTPS triggers(POST,PUT,GET),CORS, REST API.
**Create API Gateway .**
 
![image](https://user-images.githubusercontent.com/52998388/155177993-df2df256-5f00-4df8-8307-c3970fb88365.png)

Create Method and add POST to add the Lambda Function.


**Enable CORS.**
 ![image](https://user-images.githubusercontent.com/52998388/155177908-15e53976-ca0b-41b5-a7b0-a6f11223c064.png)

We added API Gateway and connected it to our existing Lambda function. Now, we can trigger our function with an API call.
**DYNAMODB:**
create a DynamoDB table and enable your Lambda function to store data in it.
Add Primary Key ID and copy the ARN number, Create IAM policy to  adding permissions to our function so it can use the DynamoDB service, inline policy method .

**CODE: Python**
import json
import boto3
from time import gmtime, strftime
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('HelloWorldDatabase')     # Table name
now = strftime("%a, %d %b %Y %H:%M:%S +0000", gmtime())
def lambda_handler(event, context):

    name = event['firstName'] +' '+ event['lastName']

    response = table.put_item(
        Item={
            'ID': name,                         #ID is primary Key
            'LatestGreetingTime':now
            })

    return {
        'statusCode': 200,
        'body': json.dumps('Hello, ' + name)
    }

**Add Interactivity:**
AWS Amplify upload the CODE in index.html . When the file is uploaded, a Deployment process will automatically begin. Once you see a green bar, your deployment will be complete.


