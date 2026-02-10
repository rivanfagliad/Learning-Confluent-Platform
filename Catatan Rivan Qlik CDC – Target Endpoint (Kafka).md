# Kafka Fundamentals Notes  
_Context: Qlik CDC – Target Endpoint (BRI Project)_

Dokumen ini berisi rangkuman catatan pembelajaran **Apache Kafka fundamentals** yang dikumpulkan untuk mendukung implementasi dan troubleshooting **Qlik CDC (Change Data Capture)** dengan Kafka sebagai **Target Endpoint**.

---

## 1. Kafka Producer Basics

### 1.1 Acknowledgment (ACK)
Kafka Producer dapat dikonfigurasi untuk menggunakan **ACK** atau **No ACK**, yang memengaruhi **durability, latency, dan throughput**.

Nilai konfigurasi `acks`:
- `acks=0`  
  Tidak menunggu acknowledgment.  
  ➜ **Paling cepat**, tetapi **berisiko kehilangan data**.

- `acks=1`  
  Acknowledgment diterima setelah **leader replica** menerima pesan.  
  ➜ **Balance** antara performa dan reliability.

- `acks=all`  
  Acknowledgment diterima setelah **semua ISR (In-Sync Replicas)** menerima pesan.  
  ➜ **Paling aman**, latency paling tinggi.

---

## 2. Producer Throughput & Latency Control

Producer Kafka menyediakan beberapa parameter utama untuk mengontrol:
- **Throughput** (berapa banyak data dikirim)
- **Latency** (seberapa cepat data dikirim)

Parameter penting:
- `batch.size`  
  Ukuran batch data sebelum dikirim ke broker.

- `linger.ms`  
  Waktu tunggu tambahan sebelum batch dikirim untuk mengumpulkan lebih banyak data.

- `acks`  
  Level acknowledgment dari broker.

Optimalisasi parameter ini sangat penting untuk use case **CDC dengan volume data tinggi**.

---

## 3. Exactly Once Semantics (EOS)

**Exactly Once Semantics (EOS)** memastikan bahwa:
- Setiap message **diproduksi tepat satu kali**
- Tidak ada **duplikasi**
- Tidak ada **data yang hilang**

### 3.1 Cara Kerja EOS
EOS dicapai melalui kombinasi:
1. **Producer Idempotence**
   - Producer memberikan **sequence number unik** pada setiap message.
   - Jika terjadi retry, Kafka akan **mengabaikan duplikasi**.

2. **Consumer Offset Management**
   - Offset hanya di-commit setelah message berhasil diproses.
   - Mencegah reprocessing data.

### 3.2 Kenapa EOS Penting?
EOS sangat krusial untuk:
- Financial transaction
- Banking system
- Audit log
- CDC pipeline (seperti Qlik CDC)

> Kombinasi idempotent producer + offset management memberikan **strong delivery guarantee**.

---

## 4. Synchronous vs Asynchronous Producer

### 4.1 Asynchronous Send (Default)
- Producer tidak menunggu acknowledgment secara blocking.
- **Throughput tinggi**
- Latency sedikit lebih tinggi
- Cocok untuk high-volume streaming

### 4.2 Synchronous Send
- Producer menunggu response broker.
- **Latency lebih rendah per message**
- Throughput menurun
- Cocok untuk use case yang sangat sensitif terhadap error handling

---

## 5. What Should a Kafka Developer Know?

Seorang Kafka Developer idealnya memahami:

### 5.1 Kafka Ecosystem
- Kafka Streams
- Kafka Connect
- KSQL / ksqlDB

### 5.2 Infrastructure Knowledge
- Containerization (Docker)
- Orchestration (Kubernetes)
- Integrasi dengan Big Data tools

Knowledge ini sangat membantu untuk:
- Deployment Kafka cluster
- Scaling
- Observability
- Integration dengan Qlik & enterprise systems

---

## 6. Kafka Operations – L1 / Administrator Perspective

### 6.1 Throughput & Performance Monitoring
- Producer throughput (messages/sec, bytes/sec)
- Consumer throughput
- Latency end-to-end

### 6.2 Broker Resource Utilization
- CPU usage
- Memory
- Disk I/O
- Network bandwidth

### 6.3 Replication & Data Safety
- Replication lag
- ISR (In-Sync Replicas) count
- Under-replicated partitions

---

## 7. Consumer & Topic Monitoring

### 7.1 Consumer Lag
- Monitor consumer lag secara konsisten
- Lag tinggi dapat mengindikasikan:
  - Consumer lambat
  - Issue pada downstream system

### 7.2 Topic & Partition Health
- Jumlah partition
- Leader election changes
- ISR stability

---

## 8. Producer & Error Monitoring

### 8.1 Producer Metrics
- Acknowledgment latency
- Retry count
- Failed send rate

### 8.2 Logging & Alerting
- Message delivery failure
- Authentication / authorization error
- Configuration mismatch

Alerting penting untuk **early detection** pada pipeline CDC.

---

## 9. Relevance to Qlik CDC (Target Endpoint)

Kafka sebagai Target Endpoint pada Qlik CDC membutuhkan:
- Reliability (ACK & EOS)
- Monitoring consumer lag
- Proper tuning producer parameter
- Observability end-to-end

Konfigurasi yang tepat akan memastikan:
- Tidak ada data duplikat
- Tidak ada data yang terlewat
- Pipeline CDC stabil dan scalable

---

## References
- [:contentReference[oaicite:0]{index=0} Documentation](https://partner-training.confluent.io/learn/courses/1073/confluent-apache-kafka-fundamentals-course-accreditation)
- Confluent Kafka Documentation
