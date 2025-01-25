#  Process & Analyze the Sales Data of Tech Gadgets in Near Real-Time

##  Table of Contents

1. [Overview](#-overview)  
   - [Tech Stack](#-tech-stack)  
2. [File Structure](#-file-structure)  
3. [Features](#-features)  
4. [Architecture Workflow](#-architecture-workflow)  
   - [Explanation of Workflow](#-explanation-of-workflow)  
5. [Setup & Usage](#-setup--usage)  
   - [Prerequisites](#-prerequisites)  
   - [Clone the Repository](#-clone-the-repository)  
   - [Run the Mock Data Generator](#-run-the-mock-data-generator)  
   - [Deploy AWS Lambda](#-deploy-aws-lambda)  
   - [Query Data with Athena](#-query-data-with-athena)  
6. [Best Practices](#-best-practices)  
7. [Contributions](#-contributions)  


##  Overview

This project demonstrates an end-to-end data pipeline for processing and analyzing sales data of tech gadgets in near real-time. The solution leverages **AWS services** for ingestion, transformation, and storage, enabling efficient and scalable data processing.

###  Tech Stack:
1. **Python** - For generating mock data and transformation logic.
2. **DynamoDB** - A NoSQL database for real-time data ingestion.
3. **DynamoDB Streams** - Captures real-time changes in DynamoDB.
4. **Kinesis Streams** - Processes DynamoDB stream data in near real-time.
5. **EventBridge Pipe** - A low-latency connector between DynamoDB Streams and Kinesis Streams.
6. **Kinesis Firehose** - Delivers processed data into S3 for analytics.
7. **S3** - Scalable storage for processed data.
8. **Lambda** - Executes data transformation logic.
9. **Athena** - SQL-based analytics on processed data in S3.



##  File Structure
1. `mock_data_generator_for_dynamodb.py`  
   - Generates random sales data for tech gadgets.
   - Inserts generated data into **DynamoDB** in real-time.

2. `transformation_layer_with_lambda.py`  
   - Transforms and enriches raw data captured from **DynamoDB Streams**.
   - Outputs processed data to **Kinesis Firehose**.

3. `readme.md`  
   - Comprehensive documentation of the project.


## Features
- Near real-time data ingestion using **DynamoDB**.
- Automated transformation of raw data using **AWS Lambda**.
- Scalable data storage in **S3** for analytical queries.
- Analytics-ready data structure optimized for querying with **Athena**.
- Low-latency data processing pipeline leveraging **EventBridge Pipes** and **Kinesis**.



##  Architecture Workflow

```plaintext
[Mock Data Generator] 
        |
        v
[DynamoDB OrderTable]
        |
        v
[DynamoDB Streams] ---> [EventBridge Pipe] ---> [Kinesis Data Stream] ---> [AWS Lambda Transformation]
                                                                              |
                                                                              v
                                                                           [Kinesis Firehose]
                                                                              |
                                                                              v
                                                                            [S3 Bucket]
                                                                              |
                                                                              v
                                                                       [Athena Analytics]
```

###  Explanation of Workflow:
1. **Mock Data Generation**  
   A Python script (`mock_data_generator_for_dynamodb.py`) generates random order data for tech gadgets (e.g., laptops, phones) and inserts it into a **DynamoDB** table.

2. **Real-Time Data Capture**  
   Changes in the **DynamoDB** table are captured via **DynamoDB Streams** and routed to **Kinesis Data Streams** using **EventBridge Pipe**.

3. **Data Transformation**  
   An **AWS Lambda function** (`transformation_layer_with_lambda.py`) processes and transforms the data (e.g., decoding, enriching) before forwarding it to **Kinesis Firehose**.

4. **Data Storage**  
   **Kinesis Firehose** delivers the transformed data into an **S3** bucket in an analytics-ready format.

5. **Analytics**  
   Data stored in **S3** can be queried using **Athena**, enabling insights and reporting.



##  Setup & Usage

### Prerequisites
- **AWS CLI** configured with appropriate IAM permissions.
- Python installed with `boto3` and other required libraries.

### Clone the Repository
```bash
git clone https://github.com/your-username/repo-name.git
cd repo-name
```

### Run the Mock Data Generator
```bash
python mock_data_generator_for_dynamodb.py
```

### Deploy AWS Lambda
1. Create a Lambda function in the AWS Management Console.
2. Copy the code from `transformation_layer_with_lambda.py` and paste it into the Lambda editor.
3. Connect the Lambda function to your **Kinesis Data Stream** as an event source.

### Query Data with Athena
1. Configure Athena to query your **S3** bucket.
2. Use SQL to analyze sales trends, popular products, and more.



## Best Practices
- Use **IAM roles** with least privilege for AWS resources.
- Monitor data pipeline health with **AWS CloudWatch**.
- Optimize Lambda functions for performance and cost-efficiency.
- Leverage **partitioning** in S3 for efficient Athena queries.


## Contributions
Contributions, issues, and feature requests are welcome!  
Feel free to open a pull request or file an issue.

