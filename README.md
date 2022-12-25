# aws.eventbridge_lambda

## Lab Overview:  Use Lambda Destinations to send a message to the Inventory EventBridge event bus, following message processing through EventBridge, SNS and Step Functions. 


![lambda_dest_arch](https://user-images.githubusercontent.com/29739578/209454289-6c9d5ba1-054b-44c0-ab74-ff90faab916d.png)


Step 1: Configure the Inventory event bus
Configure the Inventory event bus as a successful Lambda Destination on InventoryFunction Lambda function

Open the AWS Management Console for Lambda in a new tab or window, so you can keep this step-by-step guide open.

Select Functions in the left navigation.

Enter InventoryFunction in the Lambda function filter. And select the function name filter when it shows up.

Select the Lambda function from the list of functions.

![lambda-function-select](https://user-images.githubusercontent.com/29739578/209454356-161587fc-a50b-474d-b85e-936bcde090a5.png)
