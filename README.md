
# 🛡️ DDoS Detection & proection Saas

A distributed system that detects **DDoS attacks using Machine Learning** and automatically blocks malicious IPs using a **custom Go-based proxy gateway**.

Network traffic is collected, pushed into **Kafka**, analyzed by a Python ML service, and the detected malicious IPs are stored in Redis and enforced by the proxy.

Designed for **low latency, reliability, and real-time protection**.

---

## Demo

Project is not hosted

---

## 🧰 Tech Stack

### 🧠 Machine Learning (Python)

* Python
* TShark (traffic capture)
* Kafka Producer (Aggregator)
* Scikit-learn, Pandas, NumPy

### 🚀 Services (Go)

* Custom Proxy Gateway (with Bloom Filter + cache)
* Backend API (webhooks, IP control, management)
* Kafka Consumer
* Redis integration

### 🗄️ Storage

* Redis (IPs, URLs, cache, blacklist)

---

## ✨ Features

### 📡 Traffic Aggregator (Python)

* Uses **TShark** to extract packet data
* Converts traffic into structured features
* Publishes batches to **Kafka topic** for ML processing

### 🤖 ML Detection Service (Python)

* Consumes traffic data from Kafka
* Classifies traffic (Normal / DDoS)
* Pushes malicious IPs to Redis blacklist

### 🚦 Go-Based Proxy Gateway

* Redirects HTTP requests to target server
* Checks IPs using:

  * **Bloom filter (in-memory)**
  * Redis fallback
* Blocks blacklisted IPs instantly
* Fast in-memory caching of URLs
* If URL missing in memory → fetch from Redis → cache → forward

### 🧩 Backend (Go)

* Manage webhooks per user (create / update / delete)
* Exposes APIs for monitoring + administration

---

## ⚙️ Workflow

1️⃣ Aggregator captures traffic using TShark
2️⃣ Sends structured logs into **Kafka**
3️⃣ ML service consumes logs and detects DDoS patterns
4️⃣ Detected IPs are saved to Redis blacklist
5️⃣ Proxy gateway checks every incoming request against:

* In-memory Bloom Filter
* Redis (if not found)
  6️⃣ Suspicious traffic is blocked instantly

---

## 🏗️ High-Level Architecture



