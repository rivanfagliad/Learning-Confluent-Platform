# 🚀 Learn Kafka – Phase 1  
**Environment:** Confluent Platform 7.9.x  di Local VM(VirtualBox)
**Mode:** 1 ZooKeeper, 1 Kafka Broker, 1 Schema Registry, 1 Kafka Connect, 1 ksqlDB, 1 Kafka REST Proxy, 1 Control Center
**Specs:** 4-Core CPU, 10GB RAM, 40GB Disk
---

## 2.1 Install Confluent Platform via Package Manager

Pada tahap ini saya melakukan persiapan environment sebelum instalasi Confluent Platform.

### 🔹 Update & Download Java
Langkah pertama adalah memastikan Java telah terinstall karena seluruh service Confluent berjalan di atas JVM.

![Update & Download Java](img/update-and-download-java.png)

---

### 🔹 Verifikasi Java
Setelah instalasi Java, saya melakukan pengecekan versi untuk memastikan Java aktif dan dikenali sistem.

![Verifikasi Java](img/verifikasi-java.png)

---

### 🔹 Menambahkan Repository Confluent
Saya menambahkan repository Confluent agar package Confluent Platform dapat di-install melalui package manager.

![Menambahkan Repo Confluent](img/menambahkan-repo-confluent.png)

---

### 🔹 Verifikasi Repository
Memastikan repository Confluent berhasil ditambahkan dan dapat diakses.

![Verifikasi Repo Confluent](img/verifikasi-repo-confluent.png)

---

### 🔹 Download Package Confluent Platform
Melakukan download seluruh komponen Confluent Platform.

![Download CP All Services](img/download-CP-all-services.png)

---

### 🔹 Install Confluent Platform
Melakukan instalasi service-service utama:

- ZooKeeper  
- Kafka Broker  
- Schema Registry  
- Kafka Connect  
- ksqlDB  
- Kafka REST Proxy  
- Control Center  

![Install CP All Services](img/install-CP-all-services.png)

---

### 🔹 Verifikasi Instalasi
Memastikan seluruh package berhasil terpasang tanpa error.

![Verifikasi Install](img/verifikasi-install-CP-all-services.png)

---

## 2.2 Deploy Kafka Cluster menggunakan systemd

Pada tahap ini saya menjalankan service Confluent Platform menggunakan `systemd`.

Hal ini memungkinkan service berjalan sebagai daemon dan otomatis start saat boot.

![Deploy Cluster](img/deploy-cluster.png)

---

## 2.3 Verifikasi Seluruh Service Confluent Platform

Saya melakukan pengecekan status setiap service untuk memastikan cluster berjalan normal.

---

### 🔹 ZooKeeper
Memastikan ZooKeeper aktif sebagai metadata coordinator Kafka cluster.

![Cek Status Zookeeper](img/cek-status-zookeeper.png)

---

### 🔹 Kafka Broker
Verifikasi Kafka broker berjalan dan listening pada port 9092.

![Cek Status Broker](img/cek-status-broker.png)

---

### 🔹 Schema Registry
Memastikan Schema Registry aktif untuk kebutuhan Avro / Protobuf / JSON Schema.

![Cek Status Schema Registry](img/cek-status-schema-registry.png)

---

### 🔹 ksqlDB
Verifikasi ksqlDB server berjalan untuk stream processing.

![Cek Status ksqlDB](img/cek-status-ksqldb.png)

---

### 🔹 Kafka Connect
Memastikan Kafka Connect berjalan untuk integrasi source/sink connector.

![Cek Status Kafka Connect](img/cek-status-kafka-connect.png)

---

### 🔹 Kafka REST Proxy
Verifikasi REST Proxy aktif untuk akses Kafka via HTTP API.

![Cek Status Kafka REST](img/cek-status-kafka-rest.png)

---

### 🔹 Confluent Control Center
Memastikan UI monitoring cluster berjalan.

![Cek Status Control Center](img/cek-status-c3.png)

---

## 2.4 Membuat Topic & Test Produce/Consume

Tahap ini bertujuan memastikan Kafka cluster benar-benar berfungsi.

---

### 🔹 Create Topic
Membuat topic baru untuk testing.

![Create Topic](img/create-topic.png)

---

### 🔹 Describe Topic
Memastikan topic berhasil dibuat dan memiliki partition & leader.

![Describe Topic](img/describe-topic.png)

---

### 🔹 Test Produce
Mengirim data ke topic menggunakan CLI producer.

![Test Produce](img/tes-produce.png)

---

### 🔹 Test Consume
Membaca data dari topic menggunakan CLI consumer.

![Test Consume](img/tes-consume.png)

---

## 2.5 Pengecekan ZooKeeper & Kafka Cluster

---

### 🔹 ZooKeeper Quorum
Memastikan ZooKeeper node aktif dan terhubung.

![Cek ZooKeeper Quorum](img/cek-zookeeper-quorum.png)

---

### 🔹 Kafka Cluster ID
Memverifikasi cluster ID dari broker metadata.

![Cek Cluster ID](img/cek-cluster-id.png)

---

## 2.6 Summary

Pada Phase 1 ini saya berhasil:

✅ Menginstall dan Konfigurasi Confluent Platform 7.9.x  
✅ Menjalankan seluruh service utama  
✅ Memverifikasi health service  
✅ Membuat topic Kafka  
✅ Melakukan test produce & consume  
✅ Memverifikasi ZooKeeper & Cluster ID  

Sebagai validasi akhir, saya memastikan Confluent Control Center dapat diakses melalui browser.

![Final Check Control Center](img/cek-c3.png)
