# Lambda_API_interact
Build a Basic Web Application


Deploy a web application and add interactivity with an API and a database
To create the sample web application we require
•	Create a web app
•	Connect the web app to a serverless back-end
•	Add interactivity to your web app with an API and a database
SERVICES:
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

Create An App using AWS Amplify.

Amplify Hosting is a fully managed hosting service for web apps. Connect your repository to build, deploy, and host your web app.
 

Give App name and select the method of uploading the Source Code.
 
Once completed lets move on to Create Serverless Function for our App.
AWS Lambda : 
 It is a computing service that runs code in response to events and automatically manages the computing resources required by that code.
 
Link a Serverless Function to a Web App:
We use HTTPS triggers(POST,PUT,GET),CORS, REST API.
Create API Gateway .
 

Create Method and add POST to add the Lambda Function.
Enable CORS.
 

We added API Gateway and connected it to our existing Lambda function. Now, we can trigger our function with an API call.
DYNAMODB:
create a DynamoDB table and enable your Lambda function to store data in it.
Add Primary Key ID and copy the ARN number, Create IAM policy to  adding permissions to our function so it can use the DynamoDB service, inline policy method .

CODE: Python
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

Add Interactivity:
AWS Amplify upload the CODE in index.html . When the file is uploaded, a Deployment process will automatically begin. Once you see a green bar, your deployment will be complete.


