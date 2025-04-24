Objective:
Create a serverless web application where a user submits a form on a website. That form data is processed by a Lambda function, which then stores the data in DynamoDB, all triggered via API Gateway.

Step-by-Step Breakdown:
1. Create a DynamoDB Table
Action:
Go to AWS → DynamoDB → “Create table”
Table name: Akash
Partition key: email (used to uniquely identify records)
Why: DynamoDB stores the user form data. You use email as the key to avoid duplicates.

2. Create a Lambda Function
Action:
Go to Lambda → “Create function”
Name: storeUserData (any name)
Runtime: Python 3.x
Use existing role: Select the IAM role created in step 2
Click Create function
Why: This function contains the logic to process form input and store it in DynamoDB.

3. Write Lambda Code
Action:
In your Lambda function’s code editor, replace the default code with this:
lambda_function.py
What it does:
Parses incoming JSON from API Gateway
Validates fields (like name, email)
Connects to DynamoDB and stores the data
Returns a success or error response

4. Build the HTML Frontend
Action:
Create a file index.html
index.html
What it does:
Simple HTML form that collects user data (e.g., Name, Email, Phone)
Sends data using a POST request to the API endpoint

5. Create a Success Page
Action:
Create a file success.html
success.html
Why: After successful submission, the user is redirected to this page.

6. Create the API in API Gateway
Service: Amazon API Gateway
Action:
Go to API Gateway → Create API → Choose REST API → Click Build
API Name: formAPI
Endpoint Type: Regional
Click Create API

7. Add Methods to API Gateway
Action:
Click on / (root resource) → Click “Create Method” → Choose POST
Enable Lambda Proxy Integration
Select the Lambda function created earlier
Repeat for GET if needed (to test or retrieve data)
Why: API Gateway connects your frontend to Lambda.

8. Deploy the API
Action:
Click “Actions” → “Deploy API”
Stage: Create a new one, e.g., dev
Click “Deploy”
Result: You get a public Invoke URL

9. Test the App
Action:
Open the Invoke URL in browser → It loads your index.html form
Fill in the form → Click Submit
On success, it redirects to success.html
Backend:
API Gateway sends request → Lambda processes → Stores in DynamoDB

10. Verify Data in DynamoDB
Action:
Go to DynamoDB → Tables → Click Akash → Click “Explore items”
You should see the form data stored as a new item
