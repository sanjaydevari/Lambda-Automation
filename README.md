
# `Lambda-Automation`
# `S3 to SNS Notification Lambda Function`
# `Overview:`
This AWS Lambda function is designed to be triggered by S3 events, specifically when a new file is uploaded to a specified S3 bucket. Upon trigger, the function counts the number of rows in the uploaded CSV file and sends an email notification via Amazon SNS (Simple Notification Service) with the count of rows.
# `Setup Instructions`
1.Create an S3 Bucket: If you haven't already, create an S3 bucket
  where you want to monitor file uploads.

2.Create an SNS Topic: Create an SNS topic that will be used to send email notifications. Make sure to note down the ARN (Amazon Resource Name) of the SNS topic.

3.Subscribe to the SNS Topic: Subscribe the email addresses you want to receive notifications to the SNS topic.

4.Create the Lambda Function: Navigate to the AWS Lambda console. Click on "Create function" and choose "Author from scratch". Provide a name for your function, select the runtime as Python, and choose an existing execution role that has permissions to interact with S3 and SNS. If you don't have an appropriate role, create one with necessary permissions. Click on "Create function".

5.Configure Trigger: Once the function is created, click on "Add trigger". Select "S3" as the trigger type. Choose the S3 bucket where you want to monitor file uploads. Select the event type (e.g., 'All object create events'). Click on "Add".

6.Deploy the Lambda Function Code: Copy the provided Python code and paste it into the Lambda function code editor. Modify the sns_topic_arn variable to include the ARN of the SNS topic you created earlier.

7.Save and Test: Save the Lambda function. You can test the function by manually uploading a CSV file to the configured S3 bucket. Check the SNS topic for the email notification.

# `Creation of s3-topic:`

Go to the Simple Notification Service (SNS)

Click on create topic
![Screenshot 2024-09-10 141624 1](https://github.com/user-attachments/assets/de6844e4-cb75-4557-bc1b-a27e9b431d47)
Select the type as : standard

Enter the name of the notification : email-notification

Click on create
![Screenshot 2024-09-10 141719 2](https://github.com/user-attachments/assets/0e51d8b5-b242-4b7f-8c08-49f13f047873)

The topic is created

![Screenshot 2024-09-10 141735 3](https://github.com/user-attachments/assets/06a7aa7c-49a6-459a-8582-d8baf5f2ff66)

Click on create subscription

![Screenshot 2024-09-10 142124 4](https://github.com/user-attachments/assets/37123892-48b4-4048-9295-eba844bb6fcf)

Select the arn of the topic

Select the protocol has : email

Enter the endpoint : sanjaydevari0023@gmail.com

click on create

![Screenshot 2024-09-10 142251 4](https://github.com/user-attachments/assets/3f3ad470-b110-4f4c-b0a5-afbe65293120)

The subscription for the email-notification is created succesfully

![Screenshot 2024-09-10 142313 6](https://github.com/user-attachments/assets/46cdca8e-ace9-4d9f-be24-da5d44842ef7)

Click on the confirm-subscription

![Screenshot 2024-09-10 142436 7](https://github.com/user-attachments/assets/933b909e-8108-4417-a02c-feacd8f92f0b)

The Subscription is confirmed successfully

![Screenshot 2024-09-10 142453 8](https://github.com/user-attachments/assets/ae14ba0f-e6b6-4570-beec-e8549934987b)

![Screenshot 2024-09-10 142615 9](https://github.com/user-attachments/assets/9ee1a687-2720-4920-86bb-2d263aea1922)

# `Creation of lambda-function:`

Click on the create function button

![Screenshot 2024-09-10 143347 13](https://github.com/user-attachments/assets/2afa6267-5983-4594-a07c-421762fbd10e)

Select the Author from Scratch option

Enter the name of the function : Lambda-project

Select the Runtime : Python 3.12

Architecture as : x86_64

Click on create function

![Screenshot 2024-09-10 143300 12](https://github.com/user-attachments/assets/ef9d1349-8340-4dc8-9b00-65b0afe75908)

The Lambda-project function is created:

![Screenshot 2024-09-10 143347 13](https://github.com/user-attachments/assets/fa273aa7-0073-439a-8f4f-4577427eaa1a)










