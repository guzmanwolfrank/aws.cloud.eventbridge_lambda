# aws.eventbridge_lambda

## Lab Overview:  Use Lambda Destinations to send a message to the Inventory EventBridge event bus, following message processing through EventBridge, SNS and Step Functions. 


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

** Step 2: Create the "Order Processed" rule for the Inventory function **

The Inventory function subscribes to events that signal the processing of the order has been completed successfully. The OrderProcessed event is published by the Step Function you created in the AWS Step Functions challenge.

Create a rule on the Orders event bus called OrderProcessingRule

Add a description: Handles orders successfully processed by the Order Processing state machine

Define a rule pattern









