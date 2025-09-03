# 📘 Reference Guide: Kinesis Setup using LocalStack with Docker CLI

This document outlines the standard procedure to configure and use **AWS Kinesis** with **LocalStack** in a Docker-based setup using the AWS CLI.

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

## 🔍 Step 2: List Existing Streams

Check for existing streams in LocalStack Kinesis:

```bash
aws --endpoint-url=<url> kinesis list-streams
```

**Example:**

```bash
aws --endpoint-url=http://localstack:4566 kinesis list-streams
```

**Sample Output:**

```json
{
  "StreamNames": []
}
```

> If `StreamNames` is empty, continue to Step 3 to create a new stream.

---

## ➕ Step 3: Create a Stream _(Optional)_

```bash
aws kinesis create-stream \
  --endpoint-url=<url> \
  --stream-name <streamName> \
  --shard-count 1
```

**Example:**

```bash
aws kinesis create-stream \
  --endpoint-url=http://localstack:4566 \
  --stream-name test-stream-name \
  --shard-count 1
```

**Sample Output:**

```json
<No output; successful creation returns no content>
```

---

## 📤 Step 4: Put a Record into the Stream

```bash
aws --endpoint-url=<url> kinesis put-record \
  --stream-name <streamName> \
  --partition-key 123 \
  --data <payload>
```

**Example (Order Event JSON):**

```bash
aws --endpoint-url=http://localstack:4566 kinesis put-record \
  --stream-name test-stream-name \
  --partition-key 123 \
  --data "{\"orderId\":\"ORD-1001\",\"customerId\":\"CUST-789\",\"orderDate\":\"2023-07-21T15:30:00Z\",\"items\":[{\"productId\":\"P-100\",\"quantity\":2},{\"productId\":\"P-200\",\"quantity\":1}],\"status\":\"PLACED\"}"
```

✅ **Note**: This record will be consumed and processed by your application consumer.

**Sample Output:**

```json
{
  "ShardId": "shardId-000000000000",
  "SequenceNumber": "49600867904802023483138018394835915410184799594261430274"
}
```

---

## 🔍 Step 5: (Optional) Get Shard Iterator

```bash
aws --endpoint-url=<url> kinesis get-shard-iterator \
  --shard-id <shardId> \
  --shard-iterator-type TRIM_HORIZON \
  --stream-name <streamName>
```

**Example:**

```bash
aws --endpoint-url=http://localstack:4566 kinesis get-shard-iterator \
  --shard-id shardId-000000000000 \
  --shard-iterator-type TRIM_HORIZON \
  --stream-name test-stream-name
```

**Sample Output:**

```json
{
  "ShardIterator": "AAAAAAAAAAE2KDFOQ0hNVkhZSzRHT1JYRUU2Sk4yQjM2RUxDUzVHN3BMQzRSRFRKQVRRS0FCUEdBQkFBQUFBQUFBQUE="
}
```

> Copy the `ShardIterator` value from the response for the next step.

---

## 📥 Step 6: (Optional) Get Records Using Shard Iterator

```bash
aws --endpoint-url=<url> kinesis get-records \
  --shard-iterator <iterator>
```

**Example:**

```bash
aws --endpoint-url=http://localstack:4566 kinesis get-records \
  --shard-iterator AAAAAAAAAAE2KDFOQ0hNVkhZSzRHT1JYRUU2Sk4yQjM2RUxDUzVHN3BMQzRSRFRKQVRRS0FCUEdBQkFBQUFBQUFBQUE=
```

**Sample Output:**

```json
{
  "Records": [
    {
      "SequenceNumber": "49600867904802023483138018394835915410184799594261430274",
      "ApproximateArrivalTimestamp": 1669730400.0,
      "Data": "eyJvcmRlcklkIjoiT1JELTEwMDEiLCJjdXN0b21lcklkIjoiQ1VTVC03ODkiLCJzdGF0dXMiOiJQTEFDRUQifQ==",
      "PartitionKey": "123"
    }
  ],
  "NextShardIterator": "AAAAAAAAAAE3QzU1NUNFOEtQNzJRR0dVTzJK..."
}
```

---

## 📊 Step 7: (Optional) Describe Stream _(New Command)_

You can describe a stream to check its details (status, shards, retention, etc.):

```bash
aws --endpoint-url=<url> kinesis describe-stream \
  --stream-name <streamName>
```

**Example:**

```bash
aws --endpoint-url=http://localstack:4566 kinesis describe-stream \
  --stream-name test-stream-name
```

**Sample Output:**

```json
{
  "StreamDescription": {
    "StreamName": "test-stream-name",
    "StreamARN": "arn:aws:kinesis:us-east-1:000000000000:stream/test-stream-name",
    "StreamStatus": "ACTIVE",
    "Shards": [
      {
        "ShardId": "shardId-000000000000",
        "HashKeyRange": {
          "StartingHashKey": "0",
          "EndingHashKey": "340282366920938463463374607431768211455"
        },
        "SequenceNumberRange": {
          "StartingSequenceNumber": "49600867904802023483138018394835915410184799594261430274"
        }
      }
    ]
  }
}
```

---

## ✅ Summary of Commands

| Step | Command                      | Description                      |
| ---- | ---------------------------- | -------------------------------- |
| 1    | `aws configure`              | Configure AWS CLI for LocalStack |
| 2    | `kinesis list-streams`       | List all streams                 |
| 3    | `kinesis create-stream`      | Create a new stream              |
| 4    | `kinesis put-record`         | Insert a record                  |
| 5    | `kinesis get-shard-iterator` | Fetch shard iterator             |
| 6    | `kinesis get-records`        | Read inserted records            |
| 7    | `kinesis describe-stream`    | Get stream details               |

---

## 📎 Notes

- Replace `<url>` with `http://localstack:4566` or your configured LocalStack endpoint.
- Replace `<streamName>`, `<shardId>`, and `<iterator>` with actual values as applicable.
- Payloads must be **Base64 encoded** when sent via SDKs; AWS CLI handles this internally when using `--data`.

---
