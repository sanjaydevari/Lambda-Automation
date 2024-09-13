
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




