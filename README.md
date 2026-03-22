<div align="center">

# 📨 AWS SNS & SQS — Messaging Services

### 🔔 Cloud me Messages Bhejo — Complete Guide

<br>

![AWS](https://img.shields.io/badge/Amazon_AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![SNS](https://img.shields.io/badge/SNS-Notifications-FF4F8B?style=for-the-badge&logo=amazonaws&logoColor=white)
![SQS](https://img.shields.io/badge/SQS-Queue-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Lambda](https://img.shields.io/badge/Lambda-Trigger-FF9900?style=for-the-badge&logo=aws-lambda&logoColor=white)
![Email](https://img.shields.io/badge/Email-Notifications-0078D4?style=for-the-badge&logo=gmail&logoColor=white)

> 💡 **SNS = Ek message → Sabko bhejo (Broadcast) | SQS = Message Queue me rakho → Baad me process karo!**

</div>

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 01 | [🤔 SNS & SQS Kya Hain?](#-sns--sqs-kya-hain) |
| 02 | [🔔 SNS — Simple Notification Service](#-sns--simple-notification-service) |
| 03 | [📬 SQS — Simple Queue Service](#-sqs--simple-queue-service) |
| 04 | [⚖️ SNS vs SQS — Kab Kya Use Karein?](#️-sns-vs-sqs--kab-kya-use-karein) |
| 05 | [🏗️ SNS Architecture](#️-sns-architecture) |
| 06 | [🏗️ SQS Architecture](#️-sqs-architecture) |
| 07 | [🔧 SNS Hands-On](#-sns-hands-on) |
| 08 | [🔧 SQS Hands-On](#-sqs-hands-on) |
| 09 | [🔗 SNS + SQS Fan-Out Pattern](#-sns--sqs-fan-out-pattern) |
| 10 | [⚡ Lambda Integration](#-lambda-integration) |
| 11 | [💰 Pricing](#-pricing) |
| 12 | [❌ Common Errors & Fixes](#-common-errors--fixes) |
| 13 | [📋 Cheat Sheet](#-cheat-sheet) |

---

## 🤔 SNS & SQS Kya Hain?

```
╔══════════════════════════════════════════════════════════════╗
║           SNS & SQS SIMPLE SAMAJHO                          ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║   📢 SNS — Simple Notification Service                       ║
║   ┌──────────────────────────────────────────────────────┐  ║
║   │  EXAMPLE: School ka PA System                        │  ║
║   │  Principal (Publisher) mic me bolta hai              │  ║
║   │  → Saare students (Subscribers) sunते hain           │  ║
║   │  → Ek message → Sabko ek saath milta hai! 📢         │  ║
║   └──────────────────────────────────────────────────────┘  ║
║                                                              ║
║   📬 SQS — Simple Queue Service                              ║
║   ┌──────────────────────────────────────────────────────┐  ║
║   │  EXAMPLE: Restaurant ki Order Queue                  │  ║
║   │  Customer order deta hai → Queue me jaata hai        │  ║
║   │  Chef jab free hota hai → Queue se uthata hai        │  ║
║   │  Ek ek karke process hota hai! 🍽️                   │  ║
║   └──────────────────────────────────────────────────────┘  ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

---

## 🔔 SNS — Simple Notification Service

```
╔══════════════════════════════════════════════════════════════════╗
║                   SNS CONCEPT                                   ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   PUBLISHER                 TOPIC              SUBSCRIBERS      ║
║                                                                  ║
║   ┌──────────┐    Publish  ┌─────────┐         📧 Email         ║
║   │   App    │ ──────────► │   SNS   │ ──────► 📱 SMS           ║
║   │  Server  │    Message  │  TOPIC  │ ──────► ⚡ Lambda        ║
║   │  S3      │             │         │ ──────► 📬 SQS Queue     ║
║   │  CloudW. │             └─────────┘ ──────► 🌐 HTTP/HTTPS   ║
║   └──────────┘                                                   ║
║                                                                  ║
║   ✅ Ek message → Multiple subscribers ko ek saath              ║
║   ✅ Push based (subscriber ka wait nahi)                        ║
║   ✅ Real-time delivery                                          ║
║   ✅ 1 Crore+ subscriptions ek topic me                         ║
╚══════════════════════════════════════════════════════════════════╝
```

**SNS Use Cases:**

| 🎯 Use Case | 💬 Example |
|------------|-----------|
| 🚨 **Alerts** | Server down → Team ko email/SMS |
| 📱 **Push Notifications** | Mobile app notifications |
| 🔄 **Fanout** | Ek event → Multiple systems notify |
| 💳 **Payment Alert** | Transaction hone pe SMS |
| 🖥️ **System Events** | EC2 start/stop notification |

---

## 📬 SQS — Simple Queue Service

```
╔══════════════════════════════════════════════════════════════════╗
║                   SQS CONCEPT                                   ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   PRODUCER              QUEUE               CONSUMER            ║
║                                                                  ║
║   ┌──────────┐  Send   ┌───────────────┐  Poll  ┌───────────┐  ║
║   │  Order   │ ──────► │  📬 📬 📬 📬  │ ─────► │  Worker   │  ║
║   │  Service │  Msgs   │  SQS QUEUE    │        │  (EC2/    │  ║
║   │          │         │               │        │  Lambda)  │  ║
║   └──────────┘         │  Messages wait│        └───────────┘  ║
║                        │  karte hain   │                        ║
║                        └───────────────┘                        ║
║                                                                  ║
║   ✅ Decoupling (Services alag alag kaam kar sakti hain)        ║
║   ✅ Buffer (Traffic spike handle karta hai)                    ║
║   ✅ Retry (Fail hone pe message wapas aata hai)                ║
║   ✅ 14 days tak message store hota hai                         ║
╚══════════════════════════════════════════════════════════════════╝
```

### 🔵 SQS Queue Types

```
╔══════════════════════════════════════════════════════════════════╗
║                  SQS QUEUE TYPES                                ║
╠══════════════════════════════╦═══════════════════════════════════╣
║   🔵 STANDARD QUEUE          ║   🟡 FIFO QUEUE                   ║
╠══════════════════════════════╬═══════════════════════════════════╣
║  Order guarantee NAHI        ║  Order guarantee HAI ✅           ║
║  At-least-once delivery      ║  Exactly-once delivery            ║
║  Unlimited throughput        ║  300 msgs/sec (3000 with batch)   ║
║  Duplicate ho sakta hai      ║  No duplicates ✅                 ║
║  Use: Logs, notifications    ║  Use: Bank, Order processing      ║
║  💰 Sasta                    ║  💰 Thoda mehnga                  ║
╚══════════════════════════════╩═══════════════════════════════════╝
```

---

## ⚖️ SNS vs SQS — Kab Kya Use Karein?

```
╔══════════════════════════════════════════════════════════════════╗
║                  SNS vs SQS COMPARISON                          ║
╠══════════════════════╦═══════════════════════════════════════════╣
║   📢 SNS              ║   📬 SQS                                 ║
╠══════════════════════╬═══════════════════════════════════════════╣
║  PUSH model           ║  PULL model                              ║
║  (Subscriber ko bhejo)║  (Consumer khud uthata hai)              ║
╠══════════════════════╬═══════════════════════════════════════════╣
║  Multiple receivers   ║  Single receiver (usually)               ║
║  Ek saath sabko       ║  Ek ek karke process                     ║
╠══════════════════════╬═══════════════════════════════════════════╣
║  No message storage   ║  14 days storage                         ║
║  (Deliver ya lose)    ║  (Message safe rehta hai)                ║
╠══════════════════════╬═══════════════════════════════════════════╣
║  Real-time            ║  Async processing                        ║
╠══════════════════════╬═══════════════════════════════════════════╣
║  USE WHEN:            ║  USE WHEN:                               ║
║  ✅ Alerts & emails   ║  ✅ Task queue chahiye                    ║
║  ✅ Mobile push       ║  ✅ Rate limit karna hai                  ║
║  ✅ Multiple systems  ║  ✅ Retry logic chahiye                   ║
║     notify karo       ║  ✅ Services decouple karo               ║
╚══════════════════════╩═══════════════════════════════════════════╝
```

---

## 🏗️ SNS Architecture

```
╔═════════════════════════════════════════════════════════════════╗
║               SNS FULL ARCHITECTURE                            ║
╠═════════════════════════════════════════════════════════════════╣
║                                                                 ║
║   🌐 EVENT SOURCES                                              ║
║   ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐     ║
║   │  AWS EC2 │  │CloudWatch│  │   S3     │  │  Lambda  │     ║
║   │  (alarm) │  │ (metric) │  │ (upload) │  │  (code)  │     ║
║   └─────┬────┘  └─────┬────┘  └─────┬────┘  └─────┬────┘     ║
║         └─────────────┴─────────────┴──────────────┘          ║
║                                    │                           ║
║                                    ▼                           ║
║                          ┌──────────────────┐                 ║
║                          │   📢 SNS TOPIC   │                 ║
║                          │  "MyAlertTopic"  │                 ║
║                          └────────┬─────────┘                 ║
║                                   │                           ║
║          ┌────────────────────────┼───────────────────────┐   ║
║          │                        │                       │   ║
║     ┌────▼────┐            ┌──────▼─────┐         ┌──────▼──┐ ║
║     │  📧     │            │    📱      │         │  ⚡     │ ║
║     │ Email   │            │    SMS     │         │ Lambda  │ ║
║     │Subscriber│           │ Subscriber │         │Function │ ║
║     └─────────┘            └────────────┘         └─────────┘ ║
║                                                                 ║
║          ┌────────────────┐              ┌─────────────────┐   ║
║          │   📬 SQS Queue │              │  🌐 HTTP/HTTPS  │   ║
║          │  (for async)   │              │  Webhook        │   ║
║          └────────────────┘              └─────────────────┘   ║
╚═════════════════════════════════════════════════════════════════╝
```

---

## 🏗️ SQS Architecture

```
╔═════════════════════════════════════════════════════════════════╗
║                SQS FULL ARCHITECTURE                           ║
╠═════════════════════════════════════════════════════════════════╣
║                                                                 ║
║   PRODUCERS                QUEUE                CONSUMERS      ║
║                                                                 ║
║   ┌──────────┐             ┌───────────────┐                   ║
║   │  Order   │──── Send ──►│               │──► 🖥️ EC2 Worker  ║
║   │  Service │             │  📬 📬 📬 📬  │                   ║
║   └──────────┘             │               │──► ⚡ Lambda      ║
║                            │  SQS STANDARD │                   ║
║   ┌──────────┐             │     QUEUE     │──► 🖥️ ECS Task   ║
║   │  Web App │──── Send ──►│               │                   ║
║   └──────────┘             └───────┬───────┘                   ║
║                                    │                           ║
║                            ┌───────▼───────┐                   ║
║                            │  💀 DEAD LETTER│                  ║
║                            │    QUEUE (DLQ) │                  ║
║                            │ Failed messages│                  ║
║                            │ yahan jaate    │                  ║
║                            └───────────────┘                   ║
║                                                                 ║
║   KEY CONCEPTS:                                                 ║
║   ⏱️  Visibility Timeout  = Message process hone ka time       ║
║   🔄  Retry               = Fail hone pe wapas queue me        ║
║   💀  DLQ                 = Zyada fail hone pe yahan jaaye     ║
╚═════════════════════════════════════════════════════════════════╝
```

---

## 🔧 SNS Hands-On

### Step 1 — SNS Topic Banao

```bash
# 📢 Standard SNS Topic banao
aws sns create-topic \
    --name "MyAlertTopic" \
    --region ap-south-1

# Output:
# {
#   "TopicArn": "arn:aws:sns:ap-south-1:123456789:MyAlertTopic"
# }

# 📢 FIFO Topic banao (ordered)
aws sns create-topic \
    --name "MyOrderTopic.fifo" \
    --attributes FifoTopic=true,ContentBasedDeduplication=true

# 📋 Topics list karo
aws sns list-topics --output table

# 📋 Topic info dekho
aws sns get-topic-attributes \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic"
```

### Step 2 — Subscribers Add Karo

```bash
# 📧 Email subscribe karo
aws sns subscribe \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --protocol email \
    --notification-endpoint "rahul@example.com"

# ✅ Email me confirmation link aayega — click karo!

# 📱 SMS subscribe karo
aws sns subscribe \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --protocol sms \
    --notification-endpoint "+919876543210"

# ⚡ Lambda subscribe karo
aws sns subscribe \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --protocol lambda \
    --notification-endpoint "arn:aws:lambda:ap-south-1:123456789:function:MyFunc"

# 📬 SQS subscribe karo
aws sns subscribe \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --protocol sqs \
    --notification-endpoint "arn:aws:sqs:ap-south-1:123456789:MyQueue"

# 📋 Subscriptions list karo
aws sns list-subscriptions-by-topic \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --output table
```

### Step 3 — Message Publish Karo

```bash
# 📢 Simple message bhejo
aws sns publish \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --message "🚨 Server CPU 90% ho gayi! Dekho jaldi!" \
    --subject "AWS Alert — High CPU"

# 📢 JSON message bhejo
aws sns publish \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --message '{
        "alert": "HIGH_CPU",
        "server": "WebServer-01",
        "cpu": "92%",
        "time": "2025-01-15 14:30:00"
    }' \
    --subject "Server Alert"

# 📢 Message Attributes ke saath
aws sns publish \
    --topic-arn "arn:aws:sns:ap-south-1:123456789:MyAlertTopic" \
    --message "Payment successful!" \
    --message-attributes '{
        "type": {
            "DataType": "String",
            "StringValue": "payment"
        },
        "amount": {
            "DataType": "Number",
            "StringValue": "500"
        }
    }'

# 📢 Direct phone pe SMS bhejo (topic nahi chahiye)
aws sns publish \
    --phone-number "+919876543210" \
    --message "Tumhara OTP hai: 123456"
```

---

## 🔧 SQS Hands-On

### Step 1 — Queue Banao

```bash
# 📬 Standard Queue banao
aws sqs create-queue \
    --queue-name "MyOrderQueue" \
    --region ap-south-1

# Output:
# {
#   "QueueUrl": "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue"
# }

# 📬 FIFO Queue banao (ordered + no duplicate)
aws sqs create-queue \
    --queue-name "MyOrderQueue.fifo" \
    --attributes '{
        "FifoQueue": "true",
        "ContentBasedDeduplication": "true"
    }'

# 📬 Queue with all settings banao
aws sqs create-queue \
    --queue-name "MyFullQueue" \
    --attributes '{
        "VisibilityTimeout": "30",
        "MessageRetentionPeriod": "86400",
        "ReceiveMessageWaitTimeSeconds": "20",
        "MaximumMessageSize": "262144"
    }'

# 📋 Queues list karo
aws sqs list-queues --output table

# 📋 Queue info dekho
aws sqs get-queue-attributes \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --attribute-names All
```

### Step 2 — Messages Bhejo

```bash
# 📤 Simple message bhejo
aws sqs send-message \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --message-body "Order #1001 - 2x Pizza, 1x Burger"

# 📤 JSON message bhejo
aws sqs send-message \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --message-body '{
        "order_id": "1001",
        "customer": "Rahul",
        "items": ["Pizza", "Burger"],
        "total": 450
    }'

# 📤 Delay ke saath message bhejo (60 second baad visible hoga)
aws sqs send-message \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --message-body "Delayed Order Processing" \
    --delay-seconds 60

# 📤 Batch me messages bhejo (10 ek saath)
aws sqs send-message-batch \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --entries '[
        {"Id": "1", "MessageBody": "Order #1001"},
        {"Id": "2", "MessageBody": "Order #1002"},
        {"Id": "3", "MessageBody": "Order #1003"}
    ]'
```

### Step 3 — Messages Receive & Delete Karo

```bash
# 📥 Message receive karo
aws sqs receive-message \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --max-number-of-messages 5 \
    --wait-time-seconds 10

# 📥 Receipt Handle se message delete karo
aws sqs delete-message \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --receipt-handle "AQEB...receipt-handle-value..."

# 📥 Saare messages delete karo (queue purge)
aws sqs purge-queue \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue"

# 📊 Queue me kitne messages hain dekho
aws sqs get-queue-attributes \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --attribute-names ApproximateNumberOfMessages \
    --query 'Attributes.ApproximateNumberOfMessages'
```

### Step 4 — Dead Letter Queue (DLQ)

```bash
# 💀 DLQ banao (failed messages yahan jaate hain)
aws sqs create-queue \
    --queue-name "MyOrderQueue-DLQ"

# DLQ ka ARN lo
DLQ_ARN=$(aws sqs get-queue-attributes \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue-DLQ" \
    --attribute-names QueueArn \
    --query 'Attributes.QueueArn' \
    --output text)

# Main queue me DLQ attach karo
# (3 baar fail hone pe DLQ me chala jaayega)
aws sqs set-queue-attributes \
    --queue-url "https://sqs.ap-south-1.amazonaws.com/123456789/MyOrderQueue" \
    --attributes "{
        \"RedrivePolicy\": \"{
            \\\"deadLetterTargetArn\\\": \\\"$DLQ_ARN\\\",
            \\\"maxReceiveCount\\\": 3
        }\"
    }"
```

---

## 🔗 SNS + SQS Fan-Out Pattern

```
╔══════════════════════════════════════════════════════════════════╗
║                  FAN-OUT PATTERN                                ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   PROBLEM:                                                       ║
║   Order aaya → Email bhejo + DB update karo + Invoice banao     ║
║   Agar koi fail ho → Sab fail! ❌                               ║
║                                                                  ║
║   SOLUTION — FAN-OUT:                                            ║
║                                                                  ║
║   ┌──────────┐    ┌────────────────┐                            ║
║   │  Order   │───►│   📢 SNS TOPIC │                            ║
║   │  Service │    └───────┬────────┘                            ║
║   └──────────┘            │                                      ║
║              ┌────────────┼─────────────┐                       ║
║              │            │             │                        ║
║         ┌────▼───┐  ┌─────▼───┐  ┌─────▼───┐                   ║
║         │ 📬 SQS │  │ 📬 SQS  │  │ 📬 SQS  │                   ║
║         │ Email  │  │   DB    │  │Invoice  │                   ║
║         │ Queue  │  │  Queue  │  │  Queue  │                   ║
║         └────┬───┘  └─────┬───┘  └─────┬───┘                   ║
║              │             │             │                       ║
║         ⚡Lambda      ⚡Lambda      ⚡Lambda                    ║
║         Email bhejo   DB update    Invoice PDF                  ║
║                                                                  ║
║   ✅ Sab parallel chalte hain!                                   ║
║   ✅ Ek fail → Baaki theek rehte hain!                           ║
║   ✅ Scale independently                                         ║
╚══════════════════════════════════════════════════════════════════╝
```

```bash
# 🔗 Fan-Out Setup

# Step 1: SNS Topic banao
aws sns create-topic --name "OrderTopic"

# Step 2: 3 SQS Queues banao
aws sqs create-queue --queue-name "EmailQueue"
aws sqs create-queue --queue-name "DBQueue"
aws sqs create-queue --queue-name "InvoiceQueue"

# Step 3: Har Queue ko SNS me subscribe karo
for QUEUE in EmailQueue DBQueue InvoiceQueue; do
    QUEUE_ARN=$(aws sqs get-queue-attributes \
        --queue-url "https://sqs.ap-south-1.amazonaws.com/ACCOUNT/$QUEUE" \
        --attribute-names QueueArn \
        --query 'Attributes.QueueArn' --output text)

    aws sns subscribe \
        --topic-arn "arn:aws:sns:ap-south-1:ACCOUNT:OrderTopic" \
        --protocol sqs \
        --notification-endpoint "$QUEUE_ARN"

    echo "✅ $QUEUE subscribed to SNS!"
done

# Step 4: SNS ko SQS me message bhejne ki permission do
for QUEUE in EmailQueue DBQueue InvoiceQueue; do
    aws sqs set-queue-attributes \
        --queue-url "https://sqs.ap-south-1.amazonaws.com/ACCOUNT/$QUEUE" \
        --attributes '{
            "Policy": "{
                \"Statement\": [{
                    \"Effect\": \"Allow\",
                    \"Principal\": {\"Service\": \"sns.amazonaws.com\"},
                    \"Action\": \"sqs:SendMessage\",
                    \"Resource\": \"*\"
                }]
            }"
        }'
done

# Step 5: Test karo — SNS me publish karo
aws sns publish \
    --topic-arn "arn:aws:sns:ap-south-1:ACCOUNT:OrderTopic" \
    --message '{"order_id": "5001", "customer": "Rahul", "total": 999}'

# ✅ Teeno queues me message aayega!
```

---

## ⚡ Lambda Integration

```bash
# ⚡ SNS → Lambda Trigger

# Lambda function banao
cat > sns_handler.py << 'EOF'
import json

def lambda_handler(event, context):
    for record in event['Records']:
        # SNS message nikalo
        sns_message = record['Sns']
        subject = sns_message.get('Subject', 'No Subject')
        message = sns_message['Message']

        print(f"📢 SNS Alert Aaya!")
        print(f"   Subject : {subject}")
        print(f"   Message : {message}")

        # Yahan apna logic likho
        # Email bhejo, DB update karo, etc.

    return {"statusCode": 200, "body": "Processed!"}
EOF

zip sns_function.zip sns_handler.py

aws lambda create-function \
    --function-name "SNS-Handler" \
    --runtime python3.11 \
    --role arn:aws:iam::ACCOUNT:role/lambda-role \
    --handler sns_handler.lambda_handler \
    --zip-file fileb://sns_function.zip


# ⚡ SQS → Lambda Trigger

cat > sqs_handler.py << 'EOF'
import json

def lambda_handler(event, context):
    for record in event['Records']:
        # SQS message nikalo
        body = json.loads(record['body'])

        print(f"📬 SQS Message Mili!")
        print(f"   Order ID : {body.get('order_id')}")
        print(f"   Customer : {body.get('customer')}")

        # Order process karo
        process_order(body)

    return {"statusCode": 200}

def process_order(order):
    print(f"✅ Processing order: {order['order_id']}")
EOF

zip sqs_function.zip sqs_handler.py

aws lambda create-function \
    --function-name "SQS-Handler" \
    --runtime python3.11 \
    --role arn:aws:iam::ACCOUNT:role/lambda-role \
    --handler sqs_handler.lambda_handler \
    --zip-file fileb://sqs_function.zip

# SQS ko Lambda se connect karo (Event Source Mapping)
aws lambda create-event-source-mapping \
    --function-name "SQS-Handler" \
    --event-source-arn "arn:aws:sqs:ap-south-1:ACCOUNT:MyOrderQueue" \
    --batch-size 10 \
    --enabled
```

---

## 💰 Pricing

```
╔══════════════════════════════════════════════════════════════════╗
║                SNS & SQS PRICING                                ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   📢 SNS PRICING:                                                ║
║   ┌──────────────────────────────────────────────────────────┐  ║
║   │  📧 Email/Email-JSON : $2 per 1 lakh notifications       │  ║
║   │  📱 SMS (India)      : ~$0.02 per message                │  ║
║   │  ⚡ Lambda/SQS/HTTP  : $0.50 per 10 lakh requests        │  ║
║   │  🆓 FREE TIER        : 10 lakh requests/month FREE!      │  ║
║   └──────────────────────────────────────────────────────────┘  ║
║                                                                  ║
║   📬 SQS PRICING:                                                ║
║   ┌──────────────────────────────────────────────────────────┐  ║
║   │  Standard Queue : $0.40 per 10 lakh requests             │  ║
║   │  FIFO Queue     : $0.50 per 10 lakh requests             │  ║
║   │  🆓 FREE TIER   : 10 lakh requests/month FREE!           │  ║
║   └──────────────────────────────────────────────────────────┘  ║
║                                                                  ║
║   💡 Chhoti applications ke liye practically FREE!              ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## ❌ Common Errors & Fixes

```
╔══════════════════════════════════════════════════════════════════╗
║             COMMON ERRORS & SOLUTIONS                           ║
╠══════════════════════════════════════════╦═══════════════════════╣
║  ❌ Error                                ║  ✅ Fix               ║
╠══════════════════════════════════════════╬═══════════════════════╣
║  Email confirm nahi hua                  ║  Inbox check karo,   ║
║                                          ║  spam bhi dekho      ║
╠══════════════════════════════════════════╬═══════════════════════╣
║  SQS → SNS message nahi aa raha          ║  SQS policy me SNS   ║
║                                          ║  permission do       ║
╠══════════════════════════════════════════╬═══════════════════════╣
║  Lambda trigger nahi ho raha             ║  Event source mapping║
║                                          ║  check karo          ║
╠══════════════════════════════════════════╬═══════════════════════╣
║  Message lost ho raha                    ║  DLQ setup karo      ║
╠══════════════════════════════════════════╬═══════════════════════╣
║  Duplicate messages aa rahe hain         ║  FIFO queue use karo ║
╠══════════════════════════════════════════╬═══════════════════════╣
║  Message visibility issue                ║  VisibilityTimeout   ║
║                                          ║  badhao              ║
╠══════════════════════════════════════════╬═══════════════════════╣
║  FIFO queue slow hai                     ║  Batch size badhao   ║
║                                          ║  ya Standard use karo║
╚══════════════════════════════════════════╩═══════════════════════╝
```

---

## 📋 Cheat Sheet

```
╔════════════════════════════════════════════════════════════════════╗
║                 SNS & SQS QUICK CHEAT SHEET                      ║
╠═══════════════════════════╦════════════════════════════════════════╣
║  📢 SNS COMMANDS           ║                                       ║
║  Topic banao               ║  aws sns create-topic --name          ║
║  Topics list               ║  aws sns list-topics                  ║
║  Subscribe karo            ║  aws sns subscribe                    ║
║  Subscriptions list        ║  aws sns list-subscriptions           ║
║  Message publish           ║  aws sns publish                      ║
║  Topic delete              ║  aws sns delete-topic                 ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  📬 SQS COMMANDS           ║                                       ║
║  Queue banao               ║  aws sqs create-queue --queue-name    ║
║  Queues list               ║  aws sqs list-queues                  ║
║  Message bhejo             ║  aws sqs send-message                 ║
║  Message receive           ║  aws sqs receive-message              ║
║  Message delete            ║  aws sqs delete-message               ║
║  Queue purge               ║  aws sqs purge-queue                  ║
║  Queue delete              ║  aws sqs delete-queue                 ║
║  Queue attributes          ║  aws sqs get-queue-attributes         ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  💡 KEY CONCEPTS           ║                                       ║
║  SNS                       ║  Push → Multiple subscribers          ║
║  SQS                       ║  Pull → Single consumer               ║
║  FIFO Queue                ║  Ordered + No duplicate               ║
║  Standard Queue            ║  Unordered + High throughput          ║
║  DLQ                       ║  Failed messages ka graveyard         ║
║  Fan-Out Pattern           ║  SNS → Multiple SQS queues            ║
║  Visibility Timeout        ║  Processing ke liye lock time         ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  🆓 FREE TIER              ║                                       ║
║  SNS                       ║  10 lakh requests/month               ║
║  SQS                       ║  10 lakh requests/month               ║
╚═══════════════════════════╩════════════════════════════════════════╝
```

---

