# **aws.eventbridge_lambda**

## **Lab Overview:  Use Lambda Destinations to send a message to the Inventory EventBridge event bus, following message processing through EventBridge, SNS and Step Functions.** 


![lambda_dest_arch](https://user-images.githubusercontent.com/29739578/209454289-6c9d5ba1-054b-44c0-ab74-ff90faab916d.png)


**Step 1: Configure the Inventory event bus**


Configure the Inventory event bus as a successful Lambda Destination on InventoryFunction Lambda function

Open the AWS Management Console for Lambda in a new tab or window, so you can keep this step-by-step guide open.

Select Functions in the left navigation.

Enter InventoryFunction in the Lambda function filter. And select the function name filter when it shows up.

Select the Lambda function from the list of functions.

![lambda-function-select](https://user-images.githubusercontent.com/29739578/209454356-161587fc-a50b-474d-b85e-936bcde090a5.png)

In the Lambda function Designer, choose Add destination.

![lambda-function-designer](https://user-images.githubusercontent.com/29739578/209454397-d38c8130-a101-4770-b8be-8840622ca27f.png)

In the Add destination dialogue box:

For Condition, select On success.
For Destination type, select EventBridge event bus.
For Destination, select Inventory.
![lambda-add-destination](https://user-images.githubusercontent.com/29739578/209454406-64d37215-e8a0-4d53-8439-55b11c852eb1.png)

Choose Save. 
[The Lambda function must have permissions through its IAM Execution Policy to access the success and failure Destinations. For simplicity, the function's IAM Execution Policy has been configured with access to EventBridge and SQS (see below).]

![vnfunction](https://user-images.githubusercontent.com/29739578/209454428-f6407d3f-3864-46b4-b701-1b1a743b5f46.PNG)

The On success Destination is displayed.

![lambda-success-destination](https://user-images.githubusercontent.com/29739578/209454434-a2b3fea3-1a7a-4296-94ed-0cc5490485df.png)

**Step 2: Create the "Order Processed" rule for the Inventory function**

The Inventory function subscribes to events that signal the processing of the order has been completed successfully. The OrderProcessed event is published by the Step Function you created in the AWS Step Functions challenge.

Create a rule on the Orders event bus called OrderProcessingRule

Add a description: Handles orders successfully processed by the Order Processing state machine

Define a rule pattern

![rulepattern](https://user-images.githubusercontent.com/29739578/209454469-18c148fa-ccd0-4f0d-a5a8-bf48762148be.PNG)

Configure the rule target to point to the Inventory function.

**Step 3: Testing the end-to-end functionality**

To test the end-to-end functionality, you will publish a message to the Orders EventBridge event bus with an EU location. This will trigger the following sequence of event-driven actions:

The message containing an EU location triggers the rule on the Orders event bus, which you created in the previous module, to route the message to the OrderProcessing StepFunctions workflow.

The OrderProcessing StepFunctions workflow processes the order and publishes an event to the Orders event bus.

The OrderProcessingRule that you just created on the Orders event bus routes the event to the Inventory function.

On successful execution, the InventoryFunction function sends an event to the Inventory event bus through the On success Lambda destination.

The InventoryDevRule rule on the Inventory event bus logs the event to the /aws/events/inventory CloudWatch Logs log group.

Let's test it!
Select the EventBridge tab in the Event Generator .

Make sure that the Event Generator is populated with the following (if you clicked the link above then you should see this pre-populated)

Event Bus selected to Orders
Source should be com.aws.orders
In the Detail Type add Order Notification
JSON payload for the Detail Template should be:

![vgener](https://user-images.githubusercontent.com/29739578/209454494-49b06f72-147d-49d8-a084-031ddc14827c.PNG)

Click Publish.

Open the AWS Management Console for CloudWatch  in a new tab or window, so you can keep this step-by-step guide open.

Choose Log groups in the left navigation.

Enter /aws/events/inventory in the Log Group Filter and choose /aws/events/inventory log group.

![cloudwatch-logs-select-log-group](https://user-images.githubusercontent.com/29739578/209454505-e046577f-6732-4ce6-9072-3cfffe5dcb4e.png)

In the list of Log Streams, choose the Log Stream.

![cloudwatch-logs-select-log-stream](https://user-images.githubusercontent.com/29739578/209454512-3c788422-f554-4306-9732-6ac4021d54f9.png)

Expand the Log Stream record to verify success and explore the event schema.

![cloudwatch-logs-view-log-stream](https://user-images.githubusercontent.com/29739578/209454519-504b99d4-aaa7-4369-aa32-faf68ff700f5.png)

## **Congratulations! You have successfully used Lambda Destinations to send a message to the Inventory EventBridge event bus, following message processing through EventBridge, Step Functions, and SNS**.##


