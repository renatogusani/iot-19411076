# IoT Real Time Analytics Assessment

# Building a Cloud-Based IoT System with Node-RED and AWS DynamoDB

This guide will walk you through the steps to build a cloud-based IoT system using Node-RED and AWS DynamoDB. By following these steps, you will be able to access sensor values, publish them to the cloud, and retrieve and graph the findings in a web application.

## Steps

### Step 1: Set Up AWS IoT Core

Create an AWS account if you don't have one already. Go to the AWS IoT Core console and create a new Thing. Download the Thing's certificate, public key, and private key. Create an IoT policy that grants the Thing permission to publish and subscribe to the desired topics. Attach the policy to the Thing.

### Step 2: Set Up Node-RED

Install Node-RED on your computer or a Raspberry Pi. Open the Node-RED editor and create a new flow. Drag an "inject" node onto the workspace and configure it to send a message at a desired interval. Drag a "function" node onto the workspace and write some JavaScript code that generates simulated sensor data. Connect the output of the "inject" node to the input of the "function" node. Drag an "aws-iot" node onto the workspace and double-click it to configure the AWS IoT Core settings. Enter the Thing's certificate, public key, and private key, and select the desired topic to publish to. Connect the output of the "function" node to the input of the "aws-iot" node. Deploy the Node-RED flow.

### Step 3: Set Up AWS DynamoDB

Go to the AWS DynamoDB console and create a new table. Choose a unique table name and a primary key. Configure any desired settings, such as read and write capacity units. Save the table.

### Step 4: Configure the AWS IoT Rule

Go to the AWS IoT Core console and create a new rule. Configure the rule to match the desired topic that the Node-RED flow is publishing to. Choose an action to take when a message matches the rule. Select "Send a message to a DynamoDB table" and choose the table that you created in step 3. Configure the mapping between the message payload and the DynamoDB item attributes. Save the rule.

### Step 5: Verify Data in DynamoDB

Wait for the Node-RED flow to publish some simulated sensor data to AWS IoT Core. Go to the AWS DynamoDB console and verify that the data is being written to the table.

### Step 6: Visualize the Data in Node-RED

Create a new flow in Node-RED that retrieves the sensor data from the DynamoDB table and visualizes it in a graph. Drag a "dynamodb" node onto the workspace and configure it to read from the table you created in step 3. Choose the desired key and any optional filtering or sorting options. Connect the output of the "dynamodb" node to a function node that extracts the sensor data from the DynamoDB item and formats it as an array. Connect the output of the function node to a "ui_chart" node, which can be used to display the sensor data as a line chart. Configure the chart with the desired settings. Deploy the Node-RED flow and open the Node-RED dashboard to view the chart.

That's it! You have now built a cloud-based IoT system that accesses sensor values, publishes them to the cloud, and retrieves and graphs the findings in a web application using Node-RED and AWS DynamoDB.


## Technical Steps

### Step 1: Set Up AWS IoT Core
Here are the step-by-step technical details for creating an AWS IoT Thing, downloading the Thing's certificate, public key, and private key, creating an IoT policy, and attaching the policy to the Thing:

Create an AWS account if you don't have one already by going to the AWS website and following the prompts to sign up.

Once you have an AWS account, go to the AWS IoT Core console by navigating to the "Services" menu and searching for "IoT Core" in the search bar. Click on "IoT Core" to open the console.
In the IoT Core console, click on "Manage" in the left-hand menu, and then click on "Things."
Click on the "Create" button to create a new Thing.

Enter a name for your Thing, and optionally add any attribute key-value pairs. Click on "Create Thing" to create the Thing.

Once the Thing has been created, click on its name to open its details page.
On the Thing's details page, click on "Security" in the left-hand menu.

Click on the "Create a certificate" button to create a new certificate for the Thing.
Click on the "Download" button for each of the following to download the Thing's certificate, public key, and private key:

Certificate: This is the certificate that your Thing will use to authenticate with AWS IoT Core.
Public key: This is the public key that your Thing will use to encrypt messages.
Private key: This is the private key that your Thing will use to decrypt messages.
Click on "Activate" to activate the certificate.

Attach a policy to the Thing to grant it permission to publish and subscribe to desired topics.

Click on "Attach a policy" and enter a name for the policy.

In the policy editor, enter the necessary details to grant the Thing permission to publish and subscribe to desired topics. For example, you can use the following policy to allow the Thing to publish and subscribe to a topic named "my/topic":
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iot:Publish",
                "iot:Subscribe",
                "iot:Connect",
                "iot:Receive"
            ],
            "Resource": [
                "arn:aws:iot:us-east-1:<account_id>:topic/my/topic"
            ]
        }
    ]
}
```
Note: Replace "<account_id>" with your AWS account ID.

Click on "Create" to create the policy and attach it to the Thing.
That's it! You have now created an AWS IoT Thing, downloaded its certificate, public key, and private key, created an IoT policy, and attached the policy to the Thing.

### Step 2: Set Up Node-RED
Here are the step-by-step technical details for setting up Node-RED:

Install Node-RED on your computer or Raspberry Pi: You can download and install Node-RED from the official website of Node-RED.

Open the Node-RED editor: Once Node-RED is installed, open the Node-RED editor by typing the following command in the terminal: node-red.

Create a new flow: Click on the "+" icon on the right side of the editor to create a new flow.

Drag an "inject" node onto the workspace: Drag the "inject" node from the left-hand side of the editor onto the workspace.

Configure the "inject" node: Double-click on the "inject" node to configure it. Set the "Payload Type" to "String" and enter the desired interval in milliseconds.

Drag a "function" node onto the workspace: Drag the "function" node from the left-hand side of the editor onto the workspace.

Write JavaScript code for generating simulated sensor data: Double-click on the "function" node to edit it. Write some JavaScript code that generates simulated sensor data. You can use the following example code:


