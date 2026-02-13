# Apa Itu Apache Kafka?

## 📌 Pengertian

**Apache Kafka** adalah **distributed event streaming platform** yang digunakan untuk mengalirkan, menyimpan, dan memproses data **real-time**.

Kafka memungkinkan sistem untuk:

- 🚀 Mengirim data secara real-time
- 💾 Menyimpan event sebagai log terdistribusi
- 🔄 Memproses data dalam bentuk stream
- 🔁 Melakukan replay data (membaca ulang event lama)

> **Kafka = Commit Log Terdistribusi + Streaming Engine**

---

## 🧠 Kenapa Kafka Dibuat?

Kafka dibuat (oleh LinkedIn) untuk mengatasi:

❌ Sistem sulit scale  
❌ Message queue tradisional tidak replayable  
❌ Banyak sistem butuh data yang sama  
❌ Bottleneck pada data integration  

Kafka menjawab dengan:

✔ High throughput  
✔ Fault tolerant  
✔ Horizontal scalability  
✔ Replayable events  

---

## 🏗️ Konsep Dasar Kafka

### 1️⃣ Event (Record / Message)

Event = data yang dikirim ke Kafka.

Contoh:

```json
{
  "order_id": "ORD-001",
  "amount": 150000,
  "timestamp": "2026-02-13T10:00:00Z"
}
```

Event terdiri dari:

- **Key** (opsional)
- **Value** (payload)
- **Timestamp**
- **Headers** (opsional)

---

### 2️⃣ Producer

Aplikasi yang **mengirim event** ke Kafka.

Contoh:

- Service Order
- IoT device
- Log collector

---

### 3️⃣ Consumer

Aplikasi yang **membaca event** dari Kafka.

Contoh:

- Payment Service
- Analytics Engine
- Monitoring Tool

---

### 4️⃣ Topic

Topic = kategori / channel event.

Contoh:

- `orders`
- `payments`
- `metrics`

Kafka menyimpan event secara **append-only**.

---

### 5️⃣ Partition

Topic dibagi menjadi beberapa partition untuk:

✔ Scalability  
✔ Parallelism  
✔ Load distribution  

---

### 6️⃣ Offset

Offset = nomor unik event dalam partition.

Consumer membaca berdasarkan offset.

➡ Bisa resume  
➡ Bisa replay  

---

### 7️⃣ Broker

Broker = server Kafka.

Cluster Kafka = kumpulan broker.

---

## 🔁 Cara Kerja Kafka (Simplified)

```
Producer → Topic → Consumer
```

Kafka tidak push → consumer pull.

---

# 🏢 Ekosistem Confluent Platform

Dalam **Confluent Platform**, Kafka berjalan bersama beberapa komponen penting:

```
ZooKeeper → Kafka Broker → Schema Registry → (ksqlDB / Connect / REST) → Control Center
```

---

## 🐘 ZooKeeper

**ZooKeeper** adalah service koordinasi terdistribusi yang digunakan Kafka (ZooKeeper mode).

Fungsi:

- 🧭 Menyimpan metadata cluster
- 👑 Leader election
- ⚖ Sinkronisasi broker
- 🧱 Menyimpan informasi controller

---

## 🧱 Kafka Broker

**Kafka Broker** adalah server Kafka yang:

- 💾 Menyimpan data
- 🚀 Menerima event dari producer
- 📤 Mengirim event ke consumer
- 🔁 Menangani replication

Cluster = kumpulan broker untuk HA & scalability.

---

## 🧬 Schema Registry

**Schema Registry** menyimpan & mengelola schema data Kafka.

Digunakan untuk:

- Avro
- JSON Schema
- Protobuf

Manfaat:

✔ Data contract jelas  
✔ Compatibility check  
✔ Versioning schema  

---

## 🔄 ksqlDB

**ksqlDB** adalah SQL engine untuk Kafka Stream.

Memungkinkan:

- Query stream dengan SQL
- Real-time transformation
- Stream processing tanpa coding Java

Contoh:

```sql
SELECT * FROM orders EMIT CHANGES;
```

---

## 🔌 Kafka Connect

Kafka Connect = framework integrasi Kafka ↔ sistem lain.

✔ Source connector  
✔ Sink connector  

Contoh: Database, Elasticsearch, S3.

---

## 🌐 Kafka REST Proxy

Kafka REST Proxy memungkinkan Kafka diakses via HTTP API.

Contoh:

```
POST /topics/orders
```

---

## 🎛 Confluent Control Center (C3)

**Control Center** adalah UI monitoring & management Kafka.

Fitur:

- 📊 Monitoring broker
- 📈 Throughput metrics
- 🔍 Topic inspection
- 🔌 Connector management

---

# ⭐ Keunggulan Apache Kafka

- ⚡ High Throughput
- 📈 Horizontal Scalability
- 🛡 Fault Tolerance
- 🔁 Replayable Data
- 💾 Durable Storage

---

# 🧩 Use Case Kafka

✔ Event-driven architecture  
✔ Data streaming  
✔ Log aggregation  
✔ CDC  
✔ Real-time analytics  

---

# 🏁 Kesimpulan

> **Apache Kafka adalah platform streaming data real-time yang scalable, fault tolerant, dan sangat cepat.**

Kafka menjadi tulang punggung sistem modern 🚀

---

# 📚 Referensi

- https://kafka.apache.org/
- https://docs.confluent.io/
- Kafka: The Definitive Guide
