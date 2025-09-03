# 📘 Reference Guide: Apache Kafka Setup on Windows (Local Development)

This guide provides step-by-step instructions for setting up, running, and using **Apache Kafka** on **Windows** for local development. It covers **installation, configuration, topic management, producing/consuming messages, and troubleshooting**.

---

## 🛠️ Prerequisites

Before starting, make sure you have the following installed:

- **Windows 10/11**
- **Java JDK 11+**
  Download & install [Eclipse Adoptium (Temurin)](https://adoptium.net/).
  Add `JAVA_HOME` to your environment variables (e.g., `C:\Program Files\Eclipse Adoptium\jdk-11`).
- **Apache Kafka (latest stable)**
  Download [Kafka binaries](https://kafka.apache.org/downloads), extract to `C:\kafka`.
- **PowerShell or Command Prompt**

---

## ⚙️ Step 1: Start Zookeeper

Kafka (pre-3.5 versions) requires **Zookeeper** for coordination. Open a new PowerShell/Command Prompt:

```powershell
cd C:\kafka
.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
```

✅ Zookeeper runs on **port 2181** by default.
Leave this terminal open.

---

## ⚙️ Step 2: Start Kafka Broker

Open another PowerShell/Command Prompt window:

```powershell
cd C:\kafka
.\bin\windows\kafka-server-start.bat .\config\server.properties
```

✅ Kafka Broker runs on **port 9092** by default.
Leave this terminal open as well.

---

## ➕ Step 3: Create a Topic

Topics are the **streams of records** in Kafka. To create one:

```powershell
cd C:\kafka
.\bin\windows\kafka-topics.bat --create ^
  --zookeeper localhost:2181 ^
  --replication-factor 1 ^
  --partitions 1 ^
  --topic test-topic
```

**Sample Output:**

```bash
Created topic test-topic.
```

---

## 🔍 Step 4: List Topics

Check available topics:

```powershell
cd C:\kafka
.\bin\windows\kafka-topics.bat --list --zookeeper localhost:2181
```

**Sample Output:**

```bash
test-topic
```

---

## 📤 Step 5: Produce Messages

Start a producer (to publish messages):

```powershell
cd C:\kafka
.\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic test-topic
```

Now type messages in the terminal, e.g.:

```
Hello Kafka!
Temperature:25C
```

✅ Each line is a new Kafka message.

---

## 📥 Step 6: Consume Messages

Start a consumer (to read messages):

```powershell
cd C:\kafka
.\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning
```

**Sample Output:**

```bash
Hello Kafka!
Temperature:25C
```

---

## 🗑️ Step 7: Delete a Topic _(Optional)_

```powershell
cd C:\kafka
.\bin\windows\kafka-topics.bat --delete --zookeeper localhost:2181 --topic test-topic
```

---

## 📊 Step 8: Describe a Topic _(Optional)_

```powershell
cd C:\kafka
.\bin\windows\kafka-topics.bat --describe --zookeeper localhost:2181 --topic test-topic
```

**Sample Output:**

```bash
Topic: test-topic  PartitionCount: 1  ReplicationFactor: 1  Configs:
    Topic: test-topic  Partition: 0  Leader: 0  Replicas: 0  Isr: 0
```

---

## 🧩 Advanced Setup (Optional)

### 1️⃣ Running Kafka Without Zookeeper (KRaft Mode)

Newer Kafka versions (≥ 2.8) support **KRaft mode**, eliminating Zookeeper.

- Configure `server.properties` with:

  ```
  process.roles=broker,controller
  node.id=1
  controller.quorum.voters=1@localhost:9093
  listeners=PLAINTEXT://:9092,CONTROLLER://:9093
  ```

- Start with:

  ```powershell
  .\bin\windows\kafka-server-start.bat .\config\server.properties
  ```

### 2️⃣ Running Multiple Brokers (Cluster)

- Duplicate `server.properties` → `server-1.properties`, `server-2.properties`.
- Change:

  - `broker.id=1`, `broker.id=2`
  - Ports: `listeners=PLAINTEXT://:9093`, `PLAINTEXT://:9094`
  - Log dirs: `log.dirs=/tmp/kafka-logs-1`, `/tmp/kafka-logs-2`

---

## 🛠️ Troubleshooting

- **Port Already in Use**

  - Stop existing services:
    `netstat -ano | findstr 9092`
    `taskkill /PID <pid> /F`

- **Broker Fails to Start**

  - Delete old log files:
    `C:\kafka\logs` and topic log dirs inside `\tmp\kafka-logs`

- **Consumer Not Receiving Messages**

  - Use `--from-beginning` to read all existing messages.

- **Java Errors**

  - Ensure `JAVA_HOME` is correctly set to your JDK.

---

## ✅ Summary of Commands

| Step | Command                       | Description        |
| ---- | ----------------------------- | ------------------ |
| 1    | `zookeeper-server-start.bat`  | Start Zookeeper    |
| 2    | `kafka-server-start.bat`      | Start Kafka broker |
| 3    | `kafka-topics.bat --create`   | Create a topic     |
| 4    | `kafka-topics.bat --list`     | List topics        |
| 5    | `kafka-console-producer.bat`  | Produce messages   |
| 6    | `kafka-console-consumer.bat`  | Consume messages   |
| 7    | `kafka-topics.bat --delete`   | Delete a topic     |
| 8    | `kafka-topics.bat --describe` | Describe a topic   |

---

## 📎 Notes

- Default ports: **2181 (Zookeeper)**, **9092 (Kafka Broker)**.
- Kafka CLI tools are inside `.\bin\windows\`.
- Use `Ctrl + C` to stop Zookeeper/Kafka.
- For production setups, use **Docker/Kubernetes** or managed Kafka services (e.g., **AWS MSK**).

---
