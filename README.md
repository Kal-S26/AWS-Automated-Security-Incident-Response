# AWS Automated Security Incident Response (EventBridge → Lambda → SNS + DynamoDB)

## Overview
Event-driven security automation that responds to security finding events by triggering a Lambda function, sending an email alert, and logging the incident to DynamoDB for audit purposes.

## Architecture
EventBridge Rule → Lambda (Incident Handler) → SNS (Email Alerts) + DynamoDB (Incident Audit Log) <img width="681" height="510" alt="Event-Driven Security Automation Pipeline" src="https://github.com/user-attachments/assets/c382ad10-6a72-4a6e-a566-e5d1d46ec90a" />


## AWS Services Used
- Amazon EventBridge
- AWS Lambda (Python)
- Amazon SNS
- Amazon DynamoDB
- Amazon CloudWatch

## Workflow
1. Event matches the EventBridge rule pattern.
2. EventBridge invokes Lambda.
3. Lambda logs the incident to DynamoDB.
4. Lambda publishes an alert to SNS (email).

## Testing
For demo/testing, a custom event source is used:
- `source`: `custom.guardduty`
- `detail-type`: `GuardDuty Finding`

Sample event: `events/sample_guardduty_finding.json`

## Proof
**- EventBridge monitoring + rules** <img width="1362" height="697" alt="EventBridge - Monitoring" src="https://github.com/user-attachments/assets/0df2f0d0-77b3-4cd2-bd77-45405b0bf7cc" /> <img width="1362" height="697" alt="EventBridge - Rules" src="https://github.com/user-attachments/assets/3d766219-5bd7-4fb3-aa71-3c66ae304e2f" />


**- Lambda CloudWatch logs** <img width="1362" height="697" alt="CloudWatch - Logs" src="https://github.com/user-attachments/assets/3cc586aa-b6b9-4ca6-aa76-487980d079b7" />

**- DynamoDB inserted items** <img width="1362" height="697" alt="DynamoDB - Items" src="https://github.com/user-attachments/assets/312351c2-e7f9-4649-882c-9d87afd9264c" />

**- SNS email alert** <img width="1362" height="697" alt="Amazon SNS - Topics" src="https://github.com/user-attachments/assets/ad8f88c8-f800-4f62-9e5b-51858a7275e9" />


## Cleanup (avoid cost)
- Delete EventBridge rule
- Delete Lambda function
- Delete DynamoDB table
- Delete SNS topic/subscription
