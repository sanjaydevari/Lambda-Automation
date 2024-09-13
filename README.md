
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

# `Adding the s3-trigger`
Click on add trigger

![Screenshot 2024-09-10 144740 01](https://github.com/user-attachments/assets/e0ad8d01-6909-457d-8433-0913c390cbe3)

Select the trigger as : S3

Select the bucket : s3-data-storage20

Select the event types as : all object create events

![Screenshot 2024-09-10 145731 02](https://github.com/user-attachments/assets/7afaa3e0-8daf-4647-9d24-eaabf62dac16)

Click on add to add the trigger:

![Screenshot 2024-09-10 145834 03](https://github.com/user-attachments/assets/3a3d12bb-b495-4bb3-904a-877d3eecc390)

The s3 trigger is added to the lambda function

![Screenshot 2024-09-10 145908 04](https://github.com/user-attachments/assets/fd992065-8846-459d-9482-729d292de7f9)

# `Adding the SNS-trigger`

Click on add trigger

Select the trigger as : SNS

Select the sns topic that has created earlier

Than click on add

![Screenshot 2024-09-10 145946 15](https://github.com/user-attachments/assets/625950ad-a31d-41a6-88a1-ba34ce09a3c6)

The SNS trigger is added to the lambda-function

![Screenshot 2024-09-10 150758 16](https://github.com/user-attachments/assets/84c85061-554f-4840-971d-1e05f984a80c)

# `Adding the destination`

Adding this destination can get notification for every

 successfull or failure events based on your notification

 ![Screenshot 2024-09-10 150902 18](https://github.com/user-attachments/assets/fdedbba8-f232-4c70-9582-6eb5ad3c9dae)

 The destination is added successfully

 ![Screenshot 2024-09-10 151022 19](https://github.com/user-attachments/assets/fa3e0279-2c2a-49e9-a0d8-029d0d1f1be4)

 # `Lambda Function : CODE`
import json import boto3

def lambda_handler(event, context): s3 = boto3.client('s3') # Initialize the S3 client sns = boto3.client('sns') # Initialize the SNS client

  Get the S3 bucket and object key from the event
bucket = event['Records'][0]['s3']['bucket']['name']
key = event['Records'][0]['s3']['object']['key']

  Download the CSV file from S3
response = s3.get_object(Bucket=bucket, Key=key)
csv_content = response['Body'].read().decode('utf-8').splitlines()

  Count the number of rows in the CSV file
row_count = len(csv_content)

  Print the result (you can modify this to store the count or send it elsewhere)
print(f"Number of rows in {key}: {row_count}")

  Publish a message to SNS
sns_topic_arn = 'arn:aws:sns:ap-south-1:136543311415:email-notification'
sns_message = f"Number of rows in {key}: {row_count}"

sns.publish(
    TopicArn=sns_topic_arn,
    Message=sns_message,
    Subject=f"CSV File Upload: {key}"
)

return {
    'statusCode': 200,
    'body': json.dumps(f"Number of rows in {key}: {row_count}")
}

# `Uploading the CSV file to the s3-bucket`

Click on add files and upload the file

![Screenshot 2024-09-10 152222 21](https://github.com/user-attachments/assets/cfd39c4c-d64b-4f04-adec-4ed91e2a68db)

The lambda function has ran successfully

# `CLOUDWATCH LOGS:`

![Screenshot 2024-09-10 153823 22](https://github.com/user-attachments/assets/bcdf5ee1-23c7-4570-8ef2-f3e067758e55)

# `NOTIFICATION`

I got notification to the email when the file is uploaded to the s3-bucket

Hence the lambda is successfully triggered for event and automated the process


# `The Project Is Completed`
























