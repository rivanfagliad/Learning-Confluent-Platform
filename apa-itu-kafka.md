# Apa Itu Apache Kafka?

## 📌 Pengertian
**Apache Kafka** adalah *distributed event streaming platform* yang digunakan untuk:
- Mengirim data secara real-time
- Menyimpan data dalam bentuk log
- Memproses data secara stream

Kafka banyak digunakan sebagai tulang punggung **event-driven architecture** dan **data pipeline**.

Secara sederhana:
> Kafka adalah sistem log terdistribusi yang sangat cepat dan tahan banting.

---

## 🧠 Kenapa Kafka Dibuat?
Masalah yang ingin diselesaikan Kafka:
- Sistem lama sulit scale
- Message queue tradisional tidak bisa replay data
- Banyak sistem butuh data yang sama secara real-time

Kafka menjawab itu dengan:
- High throughput
- Fault tolerant
- Horizontal scalability
- Data bisa dibaca ulang (replay)

---

## 🏗️ Konsep Dasar Kafka

### 1️⃣ Event
Event adalah data yang dikirim ke Kafka.

Contoh event:
```json
{
  "order_id": "ORD-123",
  "amount": 150000,
  "timestamp": "2026-02-09T10:00:00Z"
}
