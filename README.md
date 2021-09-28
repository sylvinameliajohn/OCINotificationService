# OCINotificationService

## Overview
The Oracle Cloud Infrastructure Notifications service broadcasts messages to distributed components through a publish-subscribe pattern, delivering secure, highly reliable, low latency and durable messages for applications hosted on Oracle Cloud Infrastructure and externally. Use Notifications to get messages whenever alarms, service connectors, and event rules are triggered. You can also directly publish messages. The Notifications service enables you to set up communication channels for publishing messages using topics and subscriptions. When a message is published to a topic, the Notifications service sends the message to all of the topic's subscriptions.
Supported subscription protocols:
- Email
- Function
- HTTPS
- PagerDuty
- Slack
- SMS

In this lab, we will create a basic Pub-Sub model with a topic and set of subscribers with different protocols like Email and Functions.

## Task 1 - Sign in to OCI Console and Configure Notification Service using Email Subscription and SMS Subscription
1. Sign in using your tenant name, user name and password. Use the login option under **Oracle Cloud Infrastructure**.
  <img src="https://user-images.githubusercontent.com/77334410/134939102-96e76d6c-febd-4d8d-8f02-1279244af722.png" height="50%" width="50%"/>

2. First we will create a Notification topic and subscribe to this topic. Click the Navigation Menu in the upper left, navigate to **Developer Services**, and select **Notifications**.
  <img src="https://user-images.githubusercontent.com/77334410/134951340-4293c336-2cc0-4eba-96cb-e5ea70882fed.png" height="50%" width="50%"/>

3. Click **Create Topic** and fill out the dialog box:
    - Name: Provide a name
    - Description: Provide a description.<br/>
   Click **Create**.
   <img src="https://user-images.githubusercontent.com/77334410/134952200-826b27bb-9438-4273-9ac3-794187cb9684.png" height="50%" width="50%"/>

4. **Creating an Email Subscription**<br/>
Once the topic state changes to **Active**, Click the topic Name. Click **Create Subscription** and fill out the dialog box:
    - PROTOCOL: Email
    - EMAIL: Provide your email id.<br/>
  Click **Create**.<br/>
 <img src="https://user-images.githubusercontent.com/77334410/135036605-164e0b2d-ab29-4a7c-8c3c-5f9720ac89ce.png" height="30%" width="30%"/><br/>
5. Subscription details screen will be displayed with subscription status showing Pending.<br/>
 Check the email account you specified and click the verification link for this subscription. Switch back to OCI console window and verify the subscription status changed to   **Active**. You may need to refresh your browser.<br/>
<img src="https://user-images.githubusercontent.com/77334410/135037481-24576ec2-e103-4923-bec9-9ff6fe6fbefb.png"  height="50%" width="50%"/>

6. **Creating an SMS Subscription**<br/>
 Click the topic Name. Click **Create Subscription** and fill out the dialog box:
    - PROTOCOL: SMS
    - Country: Select the country from the list<br/>
    - Phone Number: Provide your phone number
  Click **Create**.<br/>
<img src="https://user-images.githubusercontent.com/77334410/135043654-f97366ee-544b-4ebb-b67b-80f8a198b2a6.png" height="50%" width="50%"/>

7. Subscription details screen will be displayed with subscription status showing Pending.<br/>
 Check the SMS received on the number you specified and reply back with 'CONFIRM CODE_NO' for this subscription. Switch back to OCI console window and verify the subscription status changed to **Active**. You may need to refresh your browser.<br/>
 NOTE : International SMS capabilities are required if SMS messages come from a phone number in another country. 
 
8. **Creating a Slack Subscription**<br/>
Click the topic Name. Click **Create Subscription** and fill out the dialog box:
    - PROTOCOL: Slack
    - URL: Incoming webhook URL<br/>
    NOTE : the webhook URL can be obtained by following the steps mentioned <a href="https://api.slack.com/messaging/webhooks#getting_started">Here</a><br/>
  Click **Create**.<br/>
  <img src="https://user-images.githubusercontent.com/77334410/135049247-5128d280-848d-4a46-a17f-969eeafb0c00.png" height="50%" width="50%"/><br/>
  
7. Subscription details screen will be displayed with subscription status showing Pending.<br/>
 Check the Slack app for the Confirmation URL and click the link.<br/>
 <img src="https://user-images.githubusercontent.com/77334410/135050254-d07a0ec4-8552-417d-888a-a8a4cb6a3396.png" height="50%" width="50%"/><br/>
 <img src="https://user-images.githubusercontent.com/77334410/135050460-0a8d659b-a199-4d25-88cc-ade0af4198e6.png" height="50%" width="50%"/><br/>
 Switch back to OCI console window and verify the subscription status changed to **Active**. You may need to refresh your browser.<br/>
 
8. You are now subscribed to a Notification topic with Email, SMS and Slack subscriptions. Next we will configure Events that will publish messages to this Notification topic.<br/>
From OCI Services menu, under **Observability and Management**, click **Events Service**.<br/>
Click **Create Rule**, Fill out the dialog box:
    - **DISPLAY NAME** : Provide a name
    - **DESCRIPTION** : Provide a description<br/>
Under Rule Conditions
Ensure **Event Type** is selected
    - **SERVICE NAME**: Object Storage
    - **EVENT TYPE** : Choose these 4 Types from the drop down menu. Bucket - Create, Bucket - Delete, Bucket - Update
    - **ACTION TYPE**: Notifications
    - **NOTIFICATIONS COMPARTMENT**: Choose your compartment
    - **TOPIC**: Choose the topic created earlier<br/>
Click **Create Rule**.<br/>
<img src="https://user-images.githubusercontent.com/77334410/135039083-de543718-dc08-407e-9fec-282a01f7371f.png"/>

9. We have now configured Notification service and tied events to it with a specific compartment. When a new bucket is created, deleted or updated in Object Storage, an email notification will be sent to the email address specified.
10. To verify the subscription, create a bucket in Object storage. <br/>
  From the OCI Services menu, under **Storage**, click **Object Storage and Archive Storage**. Select the compartment assigned to you from drop down menu on left part of the screen under Buckets and click **Create Bucket**.<br/>
NOTE: Ensure the correct Compartment is selected under COMPARTMENT list.
11. Provide a name for the bucket, leave the default options and click **Create**
  <img src="https://user-images.githubusercontent.com/77334410/135040115-374c34cb-d14e-4d18-9081-ba9a60e0009a.png" height="30%" width="30%"/>
  
12. Switch to your email account and verify an event indicating Object Storage Bucket create was successful.
<img src="https://user-images.githubusercontent.com/77334410/135041132-79388b02-43d2-4168-9064-46e1a4fc2d56.png" height="30%" width="30%"/>
13. Repeat the same steps by updating the bucket and deleting the bucket and verify the Notification received in Slack and SMS.
<img src="https://user-images.githubusercontent.com/77334410/135050917-feebe9b1-733e-4887-833b-bcaab4d37465.png" height="30%" width="30%"/>







  
 


