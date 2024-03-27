# Aurora Serverless V2 Automation

This AWS CloudFormation stack automates the pre-warming and cooling down of Amazon Aurora Serverless V2 databases. It leverages AWS Lambda functions triggered by Amazon CloudWatch Events based on defined schedules to adjust the Aurora Serverless V2 minimum and maximum ACUs (Aurora Capacity Units), optimizing performance and cost.

## Description

The stack manages the following resources:
- **Lambda Functions**: Two Lambda functions are created, one for pre-warming the Aurora Serverless V2 cluster in the morning and another for cooling it down in the evening.
- **IAM Role**: An execution role for the Lambda functions with necessary permissions.
- **CloudWatch Event Rules**: Two rules that trigger the Lambda functions according to the defined cron expressions for pre-warming and cooling down.

## Parameters

- `PreWarmScheduleExpression`: Cron expression for the pre-warm schedule (Default: `cron(0 5 * * ? *)` for 5:00 AM UTC).
- `CoolDownScheduleExpression`: Cron expression for the cool down schedule (Default: `cron(0 23 * * ? *)` for 11:00 PM UTC).
- `PreWarmMinACU`: Minimum ACU to set for pre-warming (Default: 8).
- `PreWarmMaxACU`: Maximum ACU to set for pre-warming (Default: 64).
- `CoolDownMinACU`: Minimum ACU to set for cooling down (Default: 2).
- `CoolDownMaxACU`: Maximum ACU to set for cooling down (Default: 32).

## Deployment

To deploy this stack:
1. Navigate to the AWS CloudFormation Console.
2. Click on "Create Stack" > With new resources (standard).
3. Upload the provided CloudFormation template file or paste the template content into the template editor.
4. Provide the necessary parameters adjustment according to your Aurora Serverless V2 cluster requirements.
5. Review and create the stack.

## Operation

Once deployed, the Lambda functions will automatically adjust the ACUs of your Aurora Serverless V2 clusters based on the tags:
- For pre-warming: Looks for clusters with the tag `prewarm=yes`.
- For cooling down: Looks for clusters with the tag `cooldown=yes`.

Ensure your Aurora Serverless V2 clusters are tagged accordingly for the automation to apply.

## Customization

You can customize the schedule and ACU settings by updating the CloudFormation stack and modifying the parameters as needed. This allows for flexibility in managing your Aurora Serverless V2 clusters' performance and cost optimization strategies.
