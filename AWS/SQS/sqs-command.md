# 📘 Reference Guide: SQS Setup using LocalStack with Docker CLI

This document outlines the standard procedure to configure and use **AWS SQS** with **LocalStack** in a Docker-based setup using the AWS CLI.

---

## 🛠️ Prerequisites

- Docker and Docker Compose installed
- LocalStack running (e.g., via Docker or Docker Compose)
- AWS CLI installed and available in your container or local CLI

---

## ⚙️ Step 1: Configure AWS CLI

Run the following in the Docker CLI (or inside the container where AWS CLI is available):

```bash
aws configure
```

Use placeholder values (they're not used with LocalStack):

- Access Key ID: `test`
- Secret Access Key: `test`
- Region: `us-east-1`

---

## 🔍 Step 2: List Queues

Check for existing queues in LocalStack SQS:

```bash
aws --endpoint-url=<url> sqs list-queues
```

**Example:**

```bash
aws --endpoint-url=http://localstack:4566 sqs list-queues
```

**Sample Output:**

```json
{
  "QueueUrls": []
}
```

> If `QueueUrls` is empty, continue to Step 3 to create a new queue.

---

## ➕ Step 3: Create a Queue

```bash
aws sqs create-queue \
  --endpoint-url=<url> \
  --queue-name <queueName>
```

**Example:**

```bash
aws sqs create-queue \
  --endpoint-url=http://localstack:4566 \
  --queue-name test-queue
```

**Sample Output:**

```json
{
  "QueueUrl": "http://localstack:4566/000000000000/test-queue"
}
```

---

## 📤 Step 4: Send a Message to the Queue

```bash
aws sqs send-message \
  --endpoint-url=<url> \
  --queue-url <queueUrl> \
  --message-body <message>
```

**Example (Order Message JSON):**

```bash
aws sqs send-message \
  --endpoint-url=http://localstack:4566 \
  --queue-url http://localstack:4566/000000000000/test-queue \
  --message-body "{\"orderId\":\"ORD-2002\",\"customerId\":\"CUST-456\",\"total\":199.99,\"currency\":\"USD\",\"status\":\"CONFIRMED\"}"
```

**Sample Output:**

```json
{
  "MD5OfMessageBody": "9c8af5f3a8b0e65a6a2c8d6a4bb2d47f",
  "MessageId": "6d5f0dfd-4f13-46a5-9b55-06a3e9bda4ff"
}
```

---

## 📥 Step 5: Receive Messages from the Queue

```bash
aws sqs receive-message \
  --endpoint-url=<url> \
  --queue-url <queueUrl>
```

**Example:**

```bash
aws sqs receive-message \
  --endpoint-url=http://localstack:4566 \
  --queue-url http://localstack:4566/000000000000/test-queue
```

**Sample Output:**

```json
{
  "Messages": [
    {
      "MessageId": "6d5f0dfd-4f13-46a5-9b55-06a3e9bda4ff",
      "ReceiptHandle": "AQEBz5qjW...==",
      "MD5OfBody": "9c8af5f3a8b0e65a6a2c8d6a4bb2d47f",
      "Body": "{\"orderId\":\"ORD-2002\",\"customerId\":\"CUST-456\",\"total\":199.99,\"currency\":\"USD\",\"status\":\"CONFIRMED\"}"
    }
  ]
}
```

---

## 🗑️ Step 6: Delete a Message _(Optional)_

After processing a message, delete it from the queue:

```bash
aws sqs delete-message \
  --endpoint-url=<url> \
  --queue-url <queueUrl> \
  --receipt-handle <receiptHandle>
```

**Example:**

```bash
aws sqs delete-message \
  --endpoint-url=http://localstack:4566 \
  --queue-url http://localstack:4566/000000000000/test-queue \
  --receipt-handle AQEBz5qjW...==
```

**Sample Output:**

```json
<No output; successful deletion returns no content>
```

---

## 📊 Step 7: Get Queue Attributes _(Optional)_

You can inspect queue properties such as visibility timeout, message retention, etc.:

```bash
aws sqs get-queue-attributes \
  --endpoint-url=<url> \
  --queue-url <queueUrl> \
  --attribute-names All
```

**Example:**

```bash
aws sqs get-queue-attributes \
  --endpoint-url=http://localstack:4566 \
  --queue-url http://localstack:4566/000000000000/test-queue \
  --attribute-names All
```

**Sample Output:**

```json
{
  "Attributes": {
    "ApproximateNumberOfMessages": "0",
    "ApproximateNumberOfMessagesNotVisible": "0",
    "VisibilityTimeout": "30",
    "CreatedTimestamp": "1691107200",
    "LastModifiedTimestamp": "1691107200",
    "QueueArn": "arn:aws:sqs:us-east-1:000000000000:test-queue"
  }
}
```

---

## ✅ Summary of Commands

| Step | Command                    | Description                      |
| ---- | -------------------------- | -------------------------------- |
| 1    | `aws configure`            | Configure AWS CLI for LocalStack |
| 2    | `sqs list-queues`          | List all queues                  |
| 3    | `sqs create-queue`         | Create a new queue               |
| 4    | `sqs send-message`         | Send a message                   |
| 5    | `sqs receive-message`      | Receive messages                 |
| 6    | `sqs delete-message`       | Delete a processed message       |
| 7    | `sqs get-queue-attributes` | Inspect queue attributes         |

---

## 📎 Notes

- Replace `<url>` with `http://localstack:4566` or your configured LocalStack endpoint.
- Replace `<queueUrl>` and `<receiptHandle>` with actual values from your environment.
- Messages can be JSON, XML, or plain text.

---
