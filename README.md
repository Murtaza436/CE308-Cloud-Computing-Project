# UniNotify

### A Serverless Student Announcement & Notification System on AWS

UniNotify is a fully serverless, cloud-native announcement platform built on AWS that allows faculty and administrators to send targeted announcements to students through a modern web interface.

The system stores announcements permanently in DynamoDB, delivers instant email notifications using SNS, and operates entirely without managing servers.

---

## Features

* Serverless architecture using AWS services
* Targeted audience-based announcements
* Instant email notifications via Amazon SNS
* Persistent storage with DynamoDB
* Secure REST API using API Gateway
* CloudFront CDN + private S3 frontend hosting
* Monitoring and logging with CloudWatch
* API protection using AWS WAF
* Fully scalable and AWS Free Tier friendly

---

## Architecture Overview

UniNotify uses a fully managed event-driven architecture:

```text
[User Browser]
       ↓
[CloudFront CDN]
       ↓
[Private S3 Bucket]
       ↓
[API Gateway]
       ↓
[AWS WAF]
       ↓
[Lambda Function]
      ↙        ↘
[DynamoDB]   [SNS Topics]
                  ↓
             [Email Notifications]
```

---

## AWS Services Used

| Service     | Purpose                                 |
| ----------- | --------------------------------------- |
| Amazon S3   | Hosts React frontend                    |
| CloudFront  | Global CDN and secure frontend delivery |
| API Gateway | REST API endpoint                       |
| AWS Lambda  | Serverless backend logic                |
| DynamoDB    | NoSQL announcement storage              |
| Amazon SNS  | Email notification delivery             |
| IAM         | Least-privilege access control          |
| CloudWatch  | Logging, dashboards, and alarms         |
| AWS WAF     | API protection and rate limiting        |

---

## How It Works

1. Faculty opens the frontend hosted on CloudFront.
2. React frontend sends a POST request to API Gateway.
3. WAF inspects incoming requests for threats.
4. API Gateway triggers the Lambda function.
5. Lambda:

   * Validates input
   * Stores announcement in DynamoDB
   * Publishes message to appropriate SNS topic
6. SNS sends emails to subscribed users.
7. CloudWatch logs all activity and metrics.

---

# Tech Stack

## Frontend

* React 18
* Axios
* HTML/CSS

## Backend

* AWS Lambda (Python 3.12)

## Cloud Services

* AWS API Gateway
* DynamoDB
* SNS
* S3
* CloudFront
* IAM
* CloudWatch
* AWS WAF

---

## DynamoDB Schema

### Table: `Announcements`

| Attribute  | Type                          |
| ---------- | ----------------------------- |
| id         | UUID (Partition Key)          |
| created_at | ISO 8601 Timestamp (Sort Key) |
| title      | String                        |
| message    | String                        |
| audience   | String                        |

---

## SNS Audience Topics

The system supports targeted notifications using dedicated SNS topics:

* All Students
* CE Department
* CS Department
* Final Year
* Faculty

---

## Security Features

* Private S3 bucket with Origin Access Control (OAC)
* Least-privilege IAM policies
* AWS Managed WAF Core Rule Set
* Rate limiting protection
* CORS handling for secure frontend communication

---

## Monitoring & Observability

CloudWatch is used for:

* Lambda execution logs
* Invocation monitoring
* Error tracking
* Custom dashboards
* Alarm notifications

---

## Testing Performed

| Test                        | Status |
| --------------------------- | ------ |
| Lambda Unit Testing         | ✅ Pass |
| API Gateway Integration     | ✅ Pass |
| CORS Validation             | ✅ Pass |
| DynamoDB Write Verification | ✅ Pass |
| SNS Email Delivery          | ✅ Pass |
| Audience Routing            | ✅ Pass |
| CloudWatch Logging          | ✅ Pass |
| WAF Verification            | ✅ Pass |

---

## Challenges Faced

### CORS Errors

Resolved by enabling CORS in API Gateway and Lambda responses.

### SNS Emails Not Arriving

Resolved by confirming SNS email subscriptions.

### Lambda Access Denied to DynamoDB

Resolved by attaching correct IAM permissions.

### CloudFront 403 Errors

Resolved by updating the S3 bucket policy after OAC creation.

### React App Blank Screen

Resolved by uploading the `build/` folder instead of `public/`.

---

## Cost Analysis

Most services remain within AWS Free Tier limits.

| Service     | Estimated Cost |
| ----------- | -------------- |
| Lambda      | $0.00          |
| DynamoDB    | $0.00          |
| SNS         | $0.00          |
| API Gateway | $0.00          |
| S3          | $0.00          |
| CloudFront  | $0.00          |
| CloudWatch  | $0.00          |
| WAF         | ~$6/month      |

> Note: WAF was used temporarily for demonstration purposes.

---

## Learning Outcomes

This project demonstrates practical understanding of:

* Serverless Computing
* REST API Design
* NoSQL Databases
* Event-Driven Architecture
* AWS Security Best Practices
* Monitoring & Observability
* Cloud-Native Application Deployment

---

## Team Members

| Name                | Registration Number |
| ------------------- | ------------------- |
| Abdul Wadood Khan   | 2023029             |
| Ashir Siddiqui      | 2023385             |
| Rayyan Mehmood      | 2023602             |
| Syed Murtaza Salman | 2023694             |

---

## Conclusion

UniNotify successfully demonstrates a production-grade serverless application architecture using AWS. The project integrates multiple AWS services into a cohesive, scalable, secure, and low-cost cloud solution for university announcement management.

The system provides:

* Reliable announcement delivery
* Persistent cloud storage
* Scalable backend infrastructure
* Real-world cloud security implementation
* Fully managed serverless deployment

---

## License

This project was developed for academic purposes as part of:

**CE308 — Cloud Computing**
**Ghulam Ishaq Khan Institute of Engineering Sciences and Technology (GIKI)**
**Spring 2026**
