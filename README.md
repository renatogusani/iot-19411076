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

1. Create an AWS account if you don't have one already by going to the AWS website and following the prompts to sign up.

2. Once you have an AWS account, go to the AWS IoT Core console by navigating to the "Services" menu and searching for "IoT Core" in the search bar. 3. Click on "IoT Core" to open the console.

4. In the IoT Core console, click on "Manage" in the left-hand menu, and then click on "Things."
Click on the "Create" button to create a new Thing.

5. Enter a name for your Thing, and optionally add any attribute key-value pairs. Click on "Create Thing" to create the Thing.

6. Once the Thing has been created, click on its name to open its details page.

7. On the Thing's details page, click on "Security" in the left-hand menu.

8. Click on the "Create a certificate" button to create a new certificate for the Thing.

9. Click on the "Download" button for each of the following to download the Thing's certificate, public key, and private key:

- Certificate: This is the certificate that your Thing will use to authenticate with AWS IoT Core.
- Public key: This is the public key that your Thing will use to encrypt messages.
- Private key: This is the private key that your Thing will use to decrypt messages.

10. Click on "Activate" to activate the certificate.

11. Attach a policy to the Thing to grant it permission to publish and subscribe to desired topics.

12. Click on "Attach a policy" and enter a name for the policy.

13. In the policy editor, enter the necessary details to grant the Thing permission to publish and subscribe to desired topics. For example, you can use the following policy to allow the Thing to publish and subscribe to a topic named "my/topic":
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

1. Install Node-RED on your computer or Raspberry Pi: You can download and install Node-RED from the official website of Node-RED.

2. Open the Node-RED editor: Once Node-RED is installed, open the Node-RED editor by typing the following command in the terminal: node-red.

3. Create a new flow: Click on the "+" icon on the right side of the editor to create a new flow.

4. Drag an "inject" node onto the workspace: Drag the "inject" node from the left-hand side of the editor onto the workspace.

5. Configure the "inject" node: Double-click on the "inject" node to configure it. Set the "Payload Type" to "String" and enter the desired interval in milliseconds.

6. Drag a "function" node onto the workspace: Drag the "function" node from the left-hand side of the editor onto the workspace.

7. Write JavaScript code for generating simulated sensor data: Double-click on the "function" node to edit it. Write some JavaScript code that generates simulated sensor data. You can use the following example code:
```
msg.payload = {
  temperature: Math.floor(Math.random() * 100),
  humidity: Math.floor(Math.random() * 100),
  pressure: Math.floor(Math.random() * 1000)
};
return msg;
```
8. Connect the nodes: Connect the output of the "inject" node to the input of the "function" node.

9. Drag an "aws-iot" node onto the workspace: Drag the "aws-iot" node from the left-hand side of the editor onto the workspace.

10. Configure the "aws-iot" node: Double-click on the "aws-iot" node to configure it. In the "AWS IoT Core" section, enter the Thing's certificate, public key, and private key that you downloaded earlier. In the "Topic" section, select the desired topic to publish to.

11. Connect the nodes: Connect the output of the "function" node to the input of the "aws-iot" node.

12. Deploy the Node-RED flow: Click on the "Deploy" button in the top right corner of the editor to deploy the Node-RED flow.

That's it! You have now set up Node-RED to generate simulated sensor data and publish it to AWS IoT Core.

### Step 3: Set Up AWS DynamoDB

Here are the step-by-step technical details to set up AWS DynamoDB:

1. Go to the AWS Management Console and log in to your account.

2. In the console search bar, type "DynamoDB" and select the "DynamoDB" service.

3. Click on the "Create table" button.

4. Enter a unique table name in the "Table name" field.

5. Choose a primary key for your table. You can either select a partition key, a combination of partition key and sort key or use no sort key.

6. Configure any additional desired settings, such as read and write capacity units, provisioned throughput, global secondary indexes or tags.

7. Click the "Create" button to create the table.

Your DynamoDB table is now set up and ready to be used.

### Step 4: Configure the AWS IoT Rule

Here are the step-by-step technical details for configuring the AWS IoT rule:

Step 1: Log in to the AWS IoT Core console using your AWS account credentials.

Step 2: Click on "Create a rule" on the left-hand side of the screen.

Step 3: Enter a name for your rule in the "Rule name" field.

Step 4: In the "Rule query statement" section, enter the topic that your Node-RED flow is publishing to. For example, if your flow is publishing to a topic called "sensors/temperature," enter that topic here.

Step 5: In the "Set one or more actions" section, select "Send a message to a DynamoDB table" from the dropdown menu.

Step 6: Choose the table that you created in step 3 from the "Choose a target DynamoDB table" dropdown menu.

Step 7: In the "Configure payload" section, you can choose to use the entire message payload or select specific fields to be included in the DynamoDB item attributes. You can also set data types and transformations as needed.

Step 8: Click on "Add action" to save the rule.

Your AWS IoT rule is now configured to send messages from your Node-RED flow to the DynamoDB table you created in step 3.

### Step 5: Verify Data in DynamoDB

Here are the step-by-step technical details for verifying data in DynamoDB:

1. Wait for the Node-RED flow to publish some simulated sensor data to AWS IoT Core.

2. Go to the AWS DynamoDB console and select the table that you created in step 3.

3. Click on the "Items" tab to see the list of items in the table.

4. Check if the simulated sensor data is being written to the table by verifying the values in the items.

5. You can also use the "Query" tab to search for specific items based on the item attributes.

6. If you see the simulated sensor data in the table, then the integration between Node-RED and AWS DynamoDB is working correctly.



Here are step-by-step technical details for:

### Step 6: Visualize the Data in Node-RED

1. Open the Node-RED editor and create a new flow.

3. Drag a "dynamodb" node from the Node-RED palette onto the workspace.

5. Double-click the "dynamodb" node and configure it to read from the table you created in step 3. Enter the desired key and any optional filtering or sorting options.

7. Drag a "function" node from the Node-RED palette onto the workspace and connect it to the "dynamodb" node.

9. Write some JavaScript code in the "function" node that extracts the sensor data from the DynamoDB item and formats it as an array. For example, you can use the following code:
```
msg.payload = msg.payload.Items.map(item => {
  return {
    timestamp: new Date(item.timestamp.S).getTime(),
    value: parseFloat(item.value.N)
  };
});
return msg;
```
This code extracts the timestamp and value from each DynamoDB item, converts the timestamp to a Unix timestamp in milliseconds, and formats the data as an array of objects.

6. Drag a "ui_chart" node from the Node-RED dashboard palette onto the workspace and connect it to the output of the "function" node.

8. Double-click the "ui_chart" node and configure it with the desired settings for the chart, such as the chart type, title, and axis labels.

9. Deploy the Node-RED flow and open the Node-RED dashboard to view the chart.
Congratulations! You have now visualized the sensor data retrieved from AWS DynamoDB in a chart using Node-RED.
