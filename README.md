# Ride Sharing App Using AWS Services

## Project Description:
This project focuses on building a ride sharing app within the AWS ecosystem. The goal is to streamline the handling of images by automatically resizing them and transferring them to a designated storage location while keeping stakeholders informed through notifications. Key AWS services, such as Lambda, S3, and SNS, are used to orchestrate this workflow.

## AWS Services to be used:
1.	Codecommit
2.	Amplify
3.	Cognito
4.	Lambda
5.	IAM
6.	API Gateway
7.	DynamoDB


## Key Features:
1. All the code is provided by AWS and we need a way to get it into a source control system
2. We need to be able to handle permissions for the code
3. A place to host the website and also make updates
4. A way for users to register and login
5. We need some ride sharing functionality
6. Somewhere to store and return the ride results
7. We need a way to invoke the ride sharing functionality from the browser


## Steps :
### Step 1 : Create a new repository in AWS CodeCommit
For getting the html,css, and javascript, we will not be typing anything from scratch as aws has provided the codes for us. So we will be taking that code and creating a codecommit repo and copy the code into our repo where we can work with it
![create repository](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/966b406f-3b8f-4b7a-b574-d53e2e6a0e24)
### Step 2 : Add a policy to an IAM user to allow access to CodeCommit

1. Go to IAM user
![iam user](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/669e13fc-e4af-43bf-90f3-ca3255345494)
2. Navigate to the permissions tab and click on add permissions
![add permissions](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/57593f3d-ecf9-4690-acc2-72ec9784598d)
3. Attach the policies directly
![attach policies directly](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/58bf670d-610e-42f1-8b62-00fb3caa036c)
4.You then search for codecomitpoweruser
![codecommitpoweruser](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/8fc94313-a10a-4b9f-816d-8733bc5f2b40)
5. Add permissions
This will give codecommit the access we need
### Step 3 : Create Git credentials to allow HTTPS connections to CodeCommit
1. Go to security credentials
![security creds](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/4ae74a1d-8c00-48af-a511-16192bff682d)
2. Scroll down to the https git credentials for AWS CodeCommit
![https git creds](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/519e8bbe-d6b4-4720-a39e-4fbfe4fa2f04)
3. Click on generate credentials
The generated credentials will allow us make https calls to codecommit.( download the credentials as we wil use them later)
### Step 4 : Clone the CodeCommit repository using cloudshell
1. Go to the codecommit repository we created
![created repo](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/46b214ea-7432-476e-88a9-d8cac8da2a05)

2. Copy the url of the repo(go with the https version)
![url](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/5ca26321-5a8f-4300-a698-98a50ee88411)
when you click on ‘clone https’ it copies it and then we need to open a cloud shell( a command line interface that runs in the browser) at the top of the browser
3. Open the cloud shell with is located to the right of the search bar. 
4. Type in git clone and paste the url of the repository and hit enter
5. You then type in the username you generated for codecommit as well as the password
![cli](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/bb40aa79-7009-4830-a842-e539c91057a5
However it takes us to an directory in cloud shell that hosts the repository so we will have to change it to our created repository by using ‘cd’
Cloning the repository created an empty folder and this is where our code files will end up
![cd](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/d06004f4-1ef2-4334-be39-83a61f791979)

### Step 5 : Copy the code from an s3 bucket to cloudshell
use this command to get the files:
aws s3 cp s3://ttt-wildrydes/wildrydes-site ./ --recursive
1. So were going to download the files from an s3 bucket.
![files from s3](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/3b11a0f5-9554-4955-9e23-9c6796c27c56)
2. We use ls to check the files and see that they are in the folder but not in the cloudcommit repo.
3. To push them into the cloud commit repo we type ‘git add.’ And then ‘git commit’.
![git push](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/c7499305-11ad-4576-86b1-c9b4ada2fd2d)
4. After pushing the code to the repository
You go back to the wildrydes repository and you seethe files loaded in there
![repo](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/a2aa645f-47cb-467d-a12e-8bf35ad32139)

### Step 6 : Create a new app for hosting in AWS Amplify
1. You open aws amplify, click on host web app
![amplify](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/a249a08f-5091-4950-8f1a-a008148cf9fe)
2. Go to code commit and hit continue and select the wildrydes repository from the list of options and hit next
![go to codecommit](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/a0a15d14-4972-42ec-9635-d0182c3873d7)
3. Click on allow aws amplify to automatically deploy files hosted in the project root directory. This means when theres an update or change in the code file it automatically deploys. After doing that you hit next.
![click on allow aws amplify to automatically blah blah](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/b3a7287a-8ec3-474c-89d4-46fcd17ef162)
4. This will take you to the review page where you just save and deploy
![save and deploy](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/5960ff2f-4090-40be-bea2-2f0db35cacf2)
5. You can click the link to check out the site in a new tab
![checking out the site](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/57f5ee14-3ab9-4681-ba59-fe6209d61e5e)
6. We are going to try and see if the continuous deployment is working. We do that by going to codecommit and navigating to the index.html file, clicking edit. You make whatever change you want and then fill in in the tabs which specify your name and email and then click on commit changes.
7. It then triggers amplify which starts the build process. When its done, you go back to the site and hit refresh and see that the changes have been applied
![amplify build deployment](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/29d29ca1-e7e7-4c24-b653-cfabe75d71c4)

### Step 7 : Setting up AWS Cognito for user authentification
1. Now we need to work on a way to login and register as those fuctionalities haven’t been worked on. We will be using AWS Cognito(used to do authentication)
2. We go over to aws cognito and then click on create user pool
![create user pool](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/917a2b96-14f3-4267-b66f-116e4d222985)

3. At the security requirements select cognito defaults for the passwork policy and no mfa to keep things simple and then go to next
![cognito password policy](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/e9838f1b-a1b4-49d4-b615-9520c6906fe9)
![no mfa](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/e4d472d3-d3a1-42a9-96e4-5d51089b53ae)
4. leave all the defaults on the next page and click on next
5. On the next page which is the message delivery page we will click on send email with cognito,leave all the defaults and then hit next
6. On the next page which is the integrate your app page we will give a name to our user pool and then give an app client name as wildrydeswebapp. We will leave the other defaults. Then hit next
7. Review and create the user pool.
![review and create user pool](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/a973a313-1e68-4b1a-807e-c7af5c122f5f)
8. Now we will click into the user pool.(Copythe user pool id)
9. We then click on app integration and copy the client ID
![client ID COPIED](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/92706f99-8373-4f97-9682-5ef44698f890)

### Step 8 : Updating the app configuration file to use the Amazon Cognito user pool
1. Now we need to hook up cognito with our code by updating the config file in our application code to point to the dedicated user pool
2. we go back to codecommit and open our repo and then navigate to the js file and then the config.js file
3. Click on edit . you paste the user pool ID,user pool client ID, and the region and then commit the changes which will trigger amplify again
![config js file updated](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/e5fae7b4-c703-418d-9386-a0cddd93fbbc)

### Step 9 : Testing Cognito integration by doing user registration and login
1. Now you go over to the wild rydes site and click on giddyup to register
2. Fill in the details and cognito will send an email with the verification code.
3. Once you put in the details you will be routed to the login page where you wil need to login again

### Step 10 :  Implementing ride sharing functionality with Lambda and DynamoDB
We will use a lambda function and a dynamodb database. The user will request a ride that will invoke the lambda fuction and the request will be stored In the dynamo table

1. Go to dynamodb and navigate to tables where you create a new table
2. You name the table Rides and give the partition key as RideId and leave everything as default and hit create table
3. Click into the created table, go to general information and additional info and copy the aws arn

### Step 11 :  Creating an IAM role to be used for a Lambda execution role, allowing PutItem on DynamoDB table
We will need to create a role for our lambda function to be able to write into our table so we would go to IAM

1. Click on create new role 
2. The trusted entity type will be aws service and the service will be lambda
3. Now we look for a policy to attach to the role
4. We select the aws basic lambda execution role and hit next
5. We give the name of the role as wildrydeslambda and leave the defaults of everything else and create role
6. Now we will open up the role and add some additional permissions. Go to add permissions and hit create inline policy
7. You chose the service as dynamodb and then you select putitem and then add the arn
8. You give the policy a name-dynamodbwriteaccess and create policy

### Step 11 :  Creating a new Lambda function to choose a unicorn and write the ride sharing info to DynamoDB
1. go to aws lambda and create a new lambda function by clicking create function
2. We will author from scratch. The name of the function will be requestunicorn
3. For the runtime we use Node.js 16x
4. For the execution role we will select ‘use an existing role’ which is the role we created in IAM and then hit create function
5. We then scroll down to the code source and replace the original lambda code with the code provided by aws( this can be found in the lambda.py file)
6. deploy the changes

### Step 12 :  Deploying Lambda code and executing a test event
1. Now we have to configure a test event
2. Copy our test function and paste it in the json file and hit save
3. Now we need to run the test and see that the test succeeded

### Step 13 :  Testing that items are saved to the DynamoDB table
1. We then check the dynamodb table to see if everything was recorded properly
2. In the rides table you click on explore table items
3. When we scroll down we see the one item for the test

### Step 14 :  Setting up API Gateway to invoke the ride sharing functionality
1. We go to api gateway and then hit create new api
2. Select rest api
3. Give the api a name ‘wildrydes’
4. Select edge optimized and then create api
5. Now we need to create an authorizer to authenticate calls api gateway uses that are returned by cognito
6. After creating the authorizer, click into it to test if things are working
7. Paste in the authorization token from the wildrydes page and hit test
8. We get a feedback of 200 meaning everything is working fine

### Step 15 :  Creating a resource and POST method in API Gateway for Lambda integration
Now we go into our api and then create resource which is how we will hook it up to the lambda function

1. Now we go into our api and then create resource which is how we will hook it up to the lambda function. 
![create resource in api](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/2f144882-a61a-4938-b4f0-52681d59319e)
2. We make sure to select cors when creating the resource and then hit create resource
![select cors when creating the resource](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/1c6fd1c9-f49d-42be-b725-702679f09249)
3. After creating the resource , we need to create a method. We click create method from inside the ride resource
![create method from inside the resource](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/f0f5df38-365f-4a2d-87c1-ce217d833037)
4. The method type will be a post type to integrate with the lambda function, select lambda as the integration type and then select the unicorns lambda function and then create method
![create method in resource](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/fccc61d0-214a-4a8c-bdf4-10f39d135569)
5. After creating the post method, select the method request card and then click on edit
![select the method request card](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/557801e6-c681-482f-9153-c5127dc9cedb)
6. We will authorize using the cognito user pool authorization
![edit method request using the cognito user pool authorization](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/5d5f7db7-bcfe-4135-8148-736e5c7cb3ba)
7. After its all said and done, we depLoy the API
![NOW WE DEPLOY THE api](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/31a2793d-49ed-4a68-bf88-0f43d93e87c2)
8. A pop up tab will show where you select stage s new stage and name it ‘dev’ and deploy
![select stage as dev and then deploy](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/98db7696-f242-4e07-9a50-850698bf234e)
9. Copy the invoke url 
![copy invoke url](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/8517a6cf-1059-4865-972a-1f0124553a80)
10. Now we go back to codecommit inside the config.js file and update the involve url with the one we copied from our api and commit the change
![config js file updated](https://github.com/GeorgeEliWilliams/Building-A-Ride-Sharing-App-With-7-AWS-Services/assets/103576454/eef6479a-08c4-49bd-8c1c-7251696940f9)
now to check if everything is working properly we go to our rides site and refresh
after requesting your unicorn you can go check the dynamodb table to see if it was recorded.everything is working as it should

