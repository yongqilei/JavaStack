# Elastic Compute Cloud (EC2)

- Transferring data from an EC2 instance to Amazon S3, Amazon Glacier, Amazon DynamoDB, Amazon SES, Amazon SQS, or Amazon SimpleDB in the **same** AWS Region has **not cost** at all.
- In case that one of the EC2 instances **failed a health check,** the Applocation Load Balancer **stops sending traffic** to that instance.
- 
- 
- 

# AWS RDS

## IAM Database Authentication

You can authenticate to your DB instance using AWS Identity and Access Management (IAM) database authentication. IAM database authentication works with MySQL and PostgreSQL. With this authentication method, you don't need to use a password when you connect to a DB instance. Instead, you use an authentication token.

An *authentication token* is a unique string of characters that Amazon RDS generates on request. Authentication tokens are generated using AWS Signature Version 4. Each token has a lifetime of 15 minutes.

- Network traffic to and from the database is encrypted using Secure Sockets Layer (SSL).
- You can use IAM to centrally manage access to your database resources, instead of managing access individually on each DB instance.
- For applications running on Amazon EC2, you can use profile credentials specific to your EC2 instance to access your database instead of a password, for greater security.

## AWS Aurora

Amazon Aurora typically involves a cluster of DB instances instead of a single instance. Each connection is handled by a specific DB instance. When you connect to an Aurora cluster, the host name and port that you specify point to an intermediate handler called an *endpoint*.

- Using endpoints, you can map each connection to the appropriate instance or group of instances based on your use case.

### Types of Aurora Endpoints

1. Cluster endpoint(writer endpoint)

   A *cluster endpoint* (or *writer endpoint*) for an Aurora Db cluster connects to the current primary DB instance for that DB cluster. This endpoint is the only one that can perform write operations such as DDL statements. Because of this, the cluster endpoint is the one that you connect to when you first set up a cluster or when your cluster only contains a single DB instance.
   **Each cluster has one cluster endpoint and one primary DB instance.**

   `mydbcluster.cluster-123456789012.us-east-1.rds.amazonaws.com:3306`

2. Reader endpoint

   A *reader endpoint* for an Aurora DB cluster provides load-balancing support for read-only connections to the DB cluster.

   `mydbcluster.cluster-ro-123456789012.us-east-1.rds.amazonaws.com:3306`

3. Custom endpoint

   The custom endpoint provides load-balanced database connections based on criteria other than the read-only or read-write capability of the DB instances. For example, you might define a custom endpoint to connect to instances that use a particular AWS instance class or a particular DB parameter group. Then you might tell particular groups of users about this custom endpoint. 

   > For example, you might direct internal users to low-capacity instances for report generation or ad hoc (one-time) querying, and direct production traffic to high-capacity instances.

4. Instance endpoint

## High Availability (Multi-AZ) for Amazon RDS

Amazon RDS provides **high availability** and f**ailover support** for DB instances using **Multi-AZ deployments**.

> Extra: Oracle RMAN and RAC are not supported in RDS



# Amazon MQ

AWS offering for a **managed message broker service for Apache ActiveMQ**.

## Features

- Amazon MQ uses **industry-standard APIs and protocols for messaging** , including Java Message Service (JMS), .NET Message Service (NMS), AMQP, STOMP, MQTT, OpenWire, and WebSocket.
- Amazon MQ supports both **single-instance brokers**, suitable for evaluation and testing, and **active/standby brokers** for high availability in production.

## ActiveMQ messaging features

- ActiveMQ provides all the standard JMS features including:
  - point-to-point (message queues)
  - publish-subscribe (topics)
  - request/ reply
  - persistent and non-persistent modes
  - JMS transactions
  - distributed transactions
- ActiveMQ supports more complex patterns:
  - composite destinations (producers can send the same message to multiple destinations)
  - virtual destinations (publishers broadcast messages via a topic to a pool of receicers subscribing through queues)
- **Preserves the order of message** sent by a **single producer** to al consumers on a topic
- Supports message groups, which enable multiple consumers on a queue to process messages within a group in **first-in, first-out (FIFO) order**
- Supports **massage redelivery** and **dead letter queues** when a message cannot be delivered to its destination

## Brokers

## Security and Monitoring

- Connections to the broker use SSL, and access can be restricted to a private endpoint within your Amazon VPC
- **Username and password-based authentication**

## Limits

- You can have 20 brokers per broker instance type per AWS account, per region.

## Pricing

- Pay for the time your message broker instance runs, the storage you use monthly and standard data transfer fees.

# Amazon API Gateway

**Amazon API Gateway** provides throttling at multiple levels including global and by a service call. Throttling limits can be set for standard rates and bursts. For example, API owners can set a rate limit of 1,000 requests per second for a specific method in their REST APIs, and also configure Amazon API Gateway to handle a burst of 2,000 requests per second for a few seconds.

- Enables developers to create, publish, maintain, monitor, and secure APIs at any scale

# Amazon Lambda

## Exam tips

- When you create or update Lambda functions that use environment variables, AWS Lambda encrypts them using the AWS Key Management Service (KMS). When your Lambda function is invoked, those values are decrypted and made available to the Lambda code.
- The first time you create or update Lambda functions that use environment variables in a region, a **default service key** is created for you automatically within AWS KMS. **But if you wish to use encryption helpers and use KMS to encrypt environment variables after your Lambda function is created, you must create your own AWS KMS key and choose it instead of the default key**.

# AWS Cloud Front

## Exam tips

- Cloud Front signed URLs and signed cookies provide the same basic functionality: they allow you to control who can access your content.
- Use **signed URLs** for the following cases:
  - **RTMP distribution**. Signed cookies aren't supported for RTMP distributions.
  - Restrict access to **individual files**, for example, an installation download for your application.
  - Your users are using clients doesn't support cookies.
- Use **signed cookies** for following cases:
  - Provide access to multiple restricted files.
  - You don't want to change your current URLs.



