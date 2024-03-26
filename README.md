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
### Step 2 : Add a policy to an IAM user to allow access to CodeCommit

1. Go to IAM user
2. Navigate to the permissions tab and click on add permissions
3. Attach the policies directly
4.You then search for codecomitpoweruser
5. Add permissions
This will give codecommit the access we need
### Step 3 : Create Git credentials to allow HTTPS connections to CodeCommit
1. Go to security credentials
2. Scroll down to the https git credentials for AWS CodeCommit
3. Click on generate credentials
The generated credentials will allow us make https calls to codecommit.( download the credentials as we wil use them later)
### Step 4 : Clone the CodeCommit repository using cloudshell
1. Go to the codecommit repository we created
2. Copy the url of the repo(go with the https version)
when you click on ‘clone https’ it copies it and then we need to open a cloud shell( a command line interface that runs in the browser) at the top of the browser
3. Open the cloud shell with is located to the right of the search bar. 
4. Type in git clone and paste the url of the repository and hit enter
5. You then type in the username you generated for codecommit as well as the password
However it takes us to an directory in cloud shell that hosts the repository so we will have to change it to our created repository by using ‘cd’
Cloning the repository created an empty folder and this is where our code files will end up

### Step 5 : Copy the code from an s3 bucket to cloudshell
1. So were going to download the files from an s3 bucket.
2. We use ls to check the files and see that they are in the folder but not in the cloudcommit repo.
3. To push them into the cloud commit repo we type ‘git add.’ And then ‘git commit’.
4. After pushing the code to the repository
You go back to the wildrydes repository and you seethe files loaded in there

### Step 6 : Create a new app for hosting in AWS Amplify
1. You open aws amplify, click on host web app
2. Go to code commit and hit continue and select the wildrydes repository from the list of options and hit next
3. Click on allow aws amplify to automatically deploy files hosted in the project root directory. This means when theres an update or change in the code file it automatically deploys. After doing that you hit next.
4. This will take you to the review page where you just save and deploy
5. You can click the link to check out the site in a new tab
6. We are going to try and see if the continuous deployment is working. We do that by going to codecommit and navigating to the index.html file, clicking edit. You make whatever change you want and then fill in in the tabs which specify your name and email and then click on commit changes.
7. It then triggers amplify which starts the build process. When its done, you go back to the site and hit refresh and see that the changes have been applied
### Creating Source and Designation s3 Buckets :

1. Navigate to the S3 Console.
2. Follow the Outlined Steps below.


![i1](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/fcf47c3c-3b40-4952-a0b5-5f53fe3d6444)


![i2](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/038c999c-e926-4613-9a23-2d5593c8fd95)


![i3](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/5cc0025f-29ac-40bd-8ee3-619271aaba58)

3. Create the destination bucket using the same steps and name it with a unique name.

![i4](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/2b98cf18-6e99-4154-81d9-c3ca5e864938)

4. As you can see above , I created two buckets one is Source bucket and another one is Destination bucket.

### Step 2 :
### Creating the SNS Notification :

1. Navigate to the SNS console.
2. Follow the Outlined Steps below.


![i5](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/50ae0833-cc4a-4cdd-9d03-2554cf981104)


![i6](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/bd101082-a68f-4f12-8131-412766a0835a)



![i7](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/12321adb-93ea-4715-9416-9ad0c3dd7ca3)


![i8](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/50d699f3-6501-418e-8303-9f4f113325ef)


![i9](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/96b45ba6-822d-4961-b5d1-e70fab104ac6)


![i10](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/9da24906-1523-4158-8c9c-0a3c23902dbc)
3. Scroll down and Click "Create subscription" <br>
4. After this , you will receive some mail for Subscription Confirmation and you have to confirm that.<br>
5. You can use any other protocols also like SQS, HTTP, SMS etc .,<br>


![i11](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/39c7c7d2-e9c0-41e7-b3e9-54802bf871d5)


![i12](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/3bb970d6-b6de-4d45-a7d7-8738987d32b7)


![i3](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/00b10697-1827-4304-b130-a4856e780570)



### Step 3 :
### Creating the Lambda :

1. Navigate to the Lambda Console.
2. Follow the Outlined steps below.

![i14](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/c90eaf3b-2a38-46dc-80f2-a097febf0e95)



![i15](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/1eeca065-8dbd-41d4-953d-59cec42c87bc)

3. Now replace the default code with the image-resizing-s3.py and deploy the changes , Don't test the code now we have to do some more actions before testing.
4. After that , We have to give some permission for our Lambda Function to do our process (resizing) , For that navigate to the IAM Console and follow the below steps.


![i16](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/c49c69dc-7e60-4fd1-835c-4b1581e3122e)

![i17](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/c983d5e0-e443-42c1-ab03-5bdea50434df)


![i18](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/2eb8707d-bb9c-40e6-a4cb-3fb9688fe4b2)


![i19](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/e7ab7943-e876-402c-b074-ad3b4873484e)


![i20](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/70bc666a-cda0-4374-b01f-1c91e5082770)


![i21](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/d0f40dad-c535-45c0-a19c-402aba93d555)


![i22](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/11be7629-4cf2-4318-adbf-d01873a4655c)

5. Now navigate to the Lambda Console and follow the steps below.


![i23](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/17797c6b-109c-455d-ae15-d412b83182fe)


![i24](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/fd489e94-5129-4bee-a682-ad24a2685233)


![i25](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/69779aa0-34d3-4502-9f9e-4ac15331db99)


6. Now we have to trigger the function.


![i26](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/166aadb1-4d3a-40d8-a70e-681ea507e1d1)


![i27](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/b8dcb311-1914-47bc-96a7-5df62a283954)


![i28](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/76164aba-a478-4590-a7e4-966d3f30078f)


7. Now we have to go to code section , and scroll down to  layers.<br>
8. We have to add layer .<br>
9. May be you can think , why ?<br>
10. It's because for resize the image we upload in our source S3 bucket , We need a python library called pillow in our code to resize the image . We can manually add Pillow library also, But it's very time consuming and you have to do lot more , Instead of manually adding pillow library we are going to use layers for Some easy action.<br>
11. Follow the outlined Steps below.


![i51](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/a4500c08-8a18-4a26-844a-5ad7712ba310)


![i52](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/d20cb878-d8a9-4757-8f42-7596f5448f0f)
12.You can copy the arn from below.

```
arn:aws:lambda:ap-south-1:770693421928:layer:Klayers-p39-pillow:1
```

13. After done all the actions above , now we can test our code.

![i49](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/fa884cf6-e858-44c4-ac03-fa4b4c0de763)


![i50](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/9f13561b-3839-495e-bf69-9ac34605f3c9)

14. It will show some results like below , It runs successfully but return some error because we still not upload the images in S3 yet.


![i50 1](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/d4d73c43-32aa-4ada-bed0-3aa30dd053e4)


### Step 4 :
### Results :

1. Navigate to the S3 Console.
2. Upload Some images in  Source Bucket.


![i29](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/43f39f6f-dc95-4df6-a7b2-7b4f7d631642)



![i30](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/4deb12e5-3597-4ebc-bf28-3b235b058969)


![i31](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/bc0585bd-0e6d-47e3-891b-e5dd3be0da2b)


![i32](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/c9eb1a36-198e-4b90-be94-0c95c9d877c6)


![i33](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/4e827762-b1f7-49d0-90ce-370ddaac014f)


![i34](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/b5933c6c-91d8-4eac-8940-389dbd64d101)


![i35](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/d7bdb74a-9d8f-4d02-b9ad-c1c5e463e75a)

### It Successfully resized the Image and sends me the Notification.

