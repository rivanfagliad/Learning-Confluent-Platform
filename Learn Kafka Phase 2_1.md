# 🚀 Learn Kafka – Rivan Phase 2.1

## 🎯 Objective
Pada phase ini saya melakukan eksplorasi fitur lanjutan di Confluent Platform:

- Menggunakan **Avro Producer & Consumer**
- Membuat **Source & Sink Connector (Kafka Connect)**
- Melakukan **Stream Processing dengan ksqlDB**
- Mendokumentasikan hasil pengujian

---

# 🧩 2.1 Avro Producer & Consumer

## ✅ Producer (Avro)

Pada tahap ini saya mengirim data ke Kafka menggunakan **kafka-avro-console-producer**.

Langkah yang terjadi:

1️⃣ JSON dibaca oleh producer  
2️⃣ KafkaAvroSerializer aktif  
3️⃣ JSON dikonversi menjadi **Avro binary**  
4️⃣ Schema otomatis diregister ke **Schema Registry**  
5️⃣ Message dikirim ke topic **avro-test**

![Avro Producer](./img/phase2/avro_producer.png)
![Avro Producer](./img/phase2/avro_producer2.png)
![Avro Producer](./img/phase2/avro_producer3.png)
---

## ✅ Consumer (Avro)

Kemudian saya membaca data menggunakan **kafka-avro-console-consumer**.

![Avro Consumer](./img/phase2/avro_consumer.png)

Proses yang terjadi:

1️⃣ Consumer mengambil Avro binary dari broker  
2️⃣ KafkaAvroDeserializer aktif  
3️⃣ Consumer mengambil schema dari Schema Registry  
4️⃣ Avro dikonversi kembali menjadi JSON  
5️⃣ Data ditampilkan ke console

![Avro Consumer](./img/phase2/avro_consumer2.png)

---

# 🔌 2.1 Kafka Connect – Source & Sink Connector

## ✅ Membuat Topic untuk Datagen

Saya membuat topic baru sebagai target data generator.

![Create Topic Datagen](./img/phase2/create_topic_datagen.png)

---

## ✅ Verifikasi Topic

Memastikan topic berhasil dibuat.

![Check Topic Datagen](./img/phase2/check_topic_datagen.png)

---

## ✅ Membuat Source Connector (Datagen)

Menggunakan **DatagenConnector** untuk menghasilkan data dummy secara realtime.

![Create Datagen Connector](./img/phase2/create_datagen_connector.png)

---

## ✅ Cek Status Connector

Memastikan connector berjalan normal.

![Connector Status](./img/phase2/datagen_status.png)

---

## ✅ Verifikasi Data di Topic

Mengecek apakah data berhasil masuk ke Kafka topic.

![Consume Datagen Topic](./img/phase2/consume_datagen_topic.png)
![Consume Datagen Topic](./img/phase2/consume_datagen_topic2.png)

---

# 🛢️ Sink Connector – JDBC ke PostgreSQL

## ✅ Install JDBC Connector

Menginstall plugin JDBC Sink Connector.

![Install JDBC Connector](./img/phase2/install_jdbc.png)

---

## ✅ Verifikasi Plugin JDBC

Memastikan JDBC connector terdeteksi.

![Check JDBC Plugin](./img/phase2/check_jdbc_plugin.png)

---

## ✅ Membuat JDBC Sink Connector

Mengirim data dari topic Kafka ke PostgreSQL.

![Create JDBC Sink](./img/phase2/create_jdbc_sink.png)

---

## ✅ Cek Status Sink Connector

Memastikan sink connector berjalan.

![Sink Status](./img/phase2/jdbc_status.png)

---

## ✅ Verifikasi Data di PostgreSQL

Memastikan data berhasil landing ke database.

![PostgreSQL Data](./img/phase2/postgres_result.png)

---

# 🌊 2.1 Stream Processing – ksqlDB

## ✅ Masuk ke ksqlDB CLI

Mengakses CLI ksqlDB.

![Enter ksqlDB](./img/phase2/enter_ksqldb.png)

---

## ✅ Cek Topic yang Ada

Melihat daftar topic Kafka.

![Show Topics](./img/phase2/show_topics.png)

---

## ✅ Menampilkan Isi Topic

Memastikan data terbaca di ksqlDB.

![Print Topic](./img/phase2/print_topic.png)

---

## ✅ Membuat Stream users_stream

Mapping struktur payload JSON ke kolom stream.

![Create users_stream](./img/phase2/create_users_stream.png)
![Create users_stream](./img/phase2/create_users_stream2.png)

---

## ✅ Transformasi Data (Uppercase Gender)

Mengubah nilai gender menjadi uppercase.

![Uppercase Stream](./img/phase2/users_upper.png)

---

## ✅ Transformasi Data (Lowercase Gender)

Mengubah nilai gender menjadi lower.

![Uppercase Stream](./img/phase2/users_lower.png)

---

## ✅ Filter Stream (Female Only)

Menyaring data gender FEMALE.

![Female Stream](./img/phase2/female_stream.png)

---

## ✅ Aggregation (Users per Region)

Menghitung jumlah user per region.

![Aggregation Table](./img/phase2/users_per_region.png)
![Aggregation Table](./img/phase2/users_per_region2.png)

---

## ✅ Verifikasi Topic Baru

Melihat topic hasil stream processing.

![Check Derived Topics](./img/phase2/check_derived_topics.png)

---

# 📝 Summary Phase 2.1

Pada phase ini saya berhasil:

✅ Menggunakan Avro serialization & Schema Registry  
✅ Memahami alur JSON → Avro → JSON  
✅ Menggunakan Kafka Connect (Datagen Source)  
✅ Mengirim data Kafka → PostgreSQL (JDBC Sink)  
✅ Menggunakan ksqlDB untuk:
- Stream creation
- Transformasi data
- Filtering data
- Aggregation realtime

Phase ini memperkuat pemahaman saya terhadap:

- Event Streaming  
- Schema Management  
- Data Integration  
- Stream Processing  

---

🔥 **Next Phase:** Kafka Security & Advanced Processing
