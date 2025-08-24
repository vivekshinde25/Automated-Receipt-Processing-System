
# Automated Receipt Processing System

An AWS Serverless Project that automates the process of uploading, extracting, organizing, and emailing receipt data.
This project uses Amazon S3, Textract, DynamoDB, SES, and Lambda to create a fully automated pipeline for receipt management.


## 📌 Features

* 📤 Upload receipts (images/PDFs) into an S3 bucket.

* 🤖 Extract receipt details using Amazon Textract.

* 📂 Store structured data in DynamoDB.

* 📧 Send receipt summaries automatically via Amazon SES.

* ⚡ Serverless & cost-efficient (fits in AWS Free Tier).
## 🏗️ Architecture

**1.** S3 → Stores uploaded receipts (incoming/ folder).

**2.** Lambda → Triggered by S3 events, orchestrates processing.

**3.** Textract → Extracts structured receipt details.

**4.** DynamoDB → Stores extracted data (Receipts table).

**5.** SES → Sends email summaries.

    User → S3 (incoming folder) → Lambda → Textract → DynamoDB → SES (Email Summary) 

## 🛠️ Tech Stack

* AWS S3 – Receipt storage

* AWS Textract – OCR & data extraction

* AWS DynamoDB – NoSQL database for receipts

* AWS SES – Email notifications

* AWS Lambda (Python 3.9) – Event-driven glue logic

* IAM Roles & Policies – Secure service communication
## ⚙️ Setup Instructions

1️⃣ Create S3 Bucket

* Go to Amazon S3 → Create Bucket.

* Name it automated-receipts-<username>.

* Create folder incoming/ for receipt uploads.

2️⃣ Create DynamoDB Table

* Name: Receipts

* Partition Key: ReceiptID (String)

* Sort Key: Date (String)

3️⃣ Configure SES

* Verify your email under SES → Identities.

* Use this email as sender & recipient for receipt summaries.

4️⃣ IAM Role for Lambda

* Attach these policies:

* AmazonS3ReadOnlyAccess

* AmazonTextractFullAccess

* AmazonDynamoDBFullAccess

* AmazonSESFullAccess

* AWSLambdaBasicExecutionRole

* Name it: ReceiptProcessingLambdaRole.

5️⃣ Lambda Function

* Runtime: Python 3.9

* Name: receipt-processor

* Attach role: ReceiptProcessingLambdaRole

* Increase timeout to 3 minutes.

* Add environment variables:

* DYNAMO_DB_TABLE=Receipts

* SES_SENDER_EMAIL=<your_verified_email>

* SES_RECIPIENT_EMAIL=<your_verified_email>

* Paste and deploy provided Python code.

6️⃣ Connect S3 Event → Lambda

* Go to S3 → Properties → Event Notifications.

* Create notification:

* Name: upload-event

* Prefix: incoming/

* Event type: All object create events

* Destination: receipt-processor (Lambda)
## 🚀 Usage

**1.** Upload a receipt file (JPG, PNG, PDF) into the incoming/ folder of your S3 bucket.

**2.** Wait 10–15 seconds for processing.

**3.** Verify:

    DynamoDB → Extracted data stored in Receipts table.

    SES Email → Summary of the receipt in your inbox.
## 📚 Learning Outcomes

* Hands-on with AWS serverless services.

* Event-driven architecture with Lambda + S3.

* Working with Textract OCR for automation.

* Integrating DynamoDB & SES into real workflows.
