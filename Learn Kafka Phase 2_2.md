# Hands On Basic Kafka: Security

Pada phase ini saya melakukan implementasi **Kafka Security menggunakan
TLS/SSL dan ACL**.\
Tujuannya adalah untuk memastikan komunikasi antar komponen Kafka
berjalan secara **terenkripsi (encrypted) dan terautentikasi**.

Pada percobaan ini saya mencoba mengamankan beberapa komponen utama
Kafka, yaitu:

-   ZooKeeper
-   Kafka Broker
-   Kafka Client
-   Inter Broker Communication
-   Authorization menggunakan ACL

Secara sederhana alur security yang saya bangun adalah:

    Kafka Client (SSL)
            │
            ▼
    Kafka Broker :9093 (SSL)
            │
            ▼
    ZooKeeper :2281 (SSL)

------------------------------------------------------------------------

# Generate Keystore dan Certificate

Sebelum mengaktifkan TLS di Kafka dan ZooKeeper, saya perlu membuat
**certificate, keystore, dan truststore** terlebih dahulu.

Secara sederhana konsepnya adalah:

**Keystore**\
Berisi identitas service itu sendiri (private key + certificate).

**Truststore**\
Berisi daftar certificate yang dipercaya oleh service tersebut.

Dalam percobaan ini saya membuat certificate untuk:

-   Kafka Broker
-   Kafka Client
-   ZooKeeper

------------------------------------------------------------------------

## Generate Keystore untuk Kafka Broker

    keytool -genkey -alias kafka-broker -keystore kafka.server.keystore.jks -keyalg RSA -validity 365

![generate broker keystore](img/phase22/generate_broker_keystore.png)

------------------------------------------------------------------------

## Export Certificate Kafka Broker

    keytool -export -alias kafka-broker -file kafka.server.cert -keystore kafka.server.keystore.jks

![export broker cert](img/phase22/export_broker_cert.png)

------------------------------------------------------------------------

## Import Certificate ke Truststore

    keytool -import -alias kafka-broker -file kafka.server.cert -keystore kafka.server.truststore.jks

![import broker truststore](img/phase22/import_broker_truststore.png)

------------------------------------------------------------------------

## Generate Keystore untuk Kafka Client

    keytool -genkey -alias kafka-client -keystore kafka.client.keystore.jks -keyalg RSA -validity 365

![generate client keystore](img/phase22/generate_client_keystore.png)

![export client cert](img/phase22/export_client_cert.png)

![import client truststore](img/phase22/import_client_truststore.png)

------------------------------------------------------------------------

## Generate Keystore untuk ZooKeeper

    keytool -genkey -alias zookeeper -keystore zookeeper.keystore.jks -keyalg RSA -validity 365

![generate zookeeper keystore](img/phase22/generate_zookeeper_keystore.png)

![export zookeeper cert](img/phase22/export_zookeeper_cert.png)

![import zookeeper truststore](img/phase22/import_zookeeper_truststore.png)


------------------------------------------------------------------------

# 4.1 Apply security for zookeeper quorum (Encryption and authentication)

Pada environment yang saya gunakan saat percobaan ini, saya hanya
menggunakan **1 Kafka broker dan 1 ZooKeeper**, sehingga sebenarnya
belum membentuk **ZooKeeper quorum cluster**.

Saya mencoba mengaktifkan TLS pada ZooKeeper.

    secureClientPort=2281

ZooKeeper default port:

    2181

ZooKeeper TLS port:

    2281

![zookeeper ssl](img/phase22/zookeeper_ssl_config0.png)

![zookeeper ssl](img/phase22/zookeeper_ssl_config.png)

![zookeeper ssl](img/phase22/zookeeper_ssl_config2.png)

------------------------------------------------------------------------

# 4.2 Apply security for zookeeper client and connect kafka to zookeeper using security

Konfigurasi Kafka agar terhubung ke ZooKeeper menggunakan TLS.

    zookeeper.connect=localhost:2281
    zookeeper.ssl.client.enable=true

![kafka zookeeper ssl](img/phase22/kafka_zookeeper_ssl.png)

![kafka zookeeper ssl](img/phase22/kafka_zookeeper_ssl2.png)

------------------------------------------------------------------------

# 4.3 Apply security for kafka inter broker

Pada percobaan ini saya hanya menggunakan **1 broker**, jadi inter
broker communication belum benar‑benar terjadi.

Namun saya tetap mengaktifkan SSL pada broker.

    listeners=SSL://:9093
    security.inter.broker.protocol=SSL

![broker ssl](img/phase22/kafka_broker_ssl_config.png)

![broker ssl](img/phase22/kafka_broker_ssl_config2.png)

------------------------------------------------------------------------

# 4.4 Apply security for kafka client

Saya membuat file konfigurasi client:

    client-ssl.properties

    security.protocol=SSL
    ssl.truststore.location=/etc/kafka/secrets/kafka.client.truststore.jks
    ssl.keystore.location=/etc/kafka/secrets/kafka.client.keystore.jks

![client ssl](img/phase22/client_ssl_config.png)

Test koneksi:

    kafka-topics.sh --bootstrap-server localhost:9093 --command-config client-ssl.properties --list

------------------------------------------------------------------------

# 4.5 Enable ACL

Mengaktifkan ACL pada Kafka.

    authorizer.class.name=kafka.security.authorizer.AclAuthorizer
    super.users=User:CN=192.168.1.11

![enable acl](img/phase22/kafka_acl_enable.png)

![enable acl](img/phase22/kafka_acl_enable2.png)

![enable acl](img/phase22/kafka_acl_enable3.png)

Coba menambahkan ACL Write dan Read

![enable acl](img/phase22/kafka_acl_enable4.png)

------------------------------------------------------------------------

# 4.6 Test produce and consume using security

Test producer:

    kafka-console-producer.sh --broker-list localhost:9093 --topic test-topic --producer.config client-ssl.properties

![producer ssl](img/phase22/ssl_producer_test.png)

Test consumer:

    kafka-console-consumer.sh --bootstrap-server localhost:9093 --topic test-topic --from-beginning --consumer.config client-ssl.properties

![consumer ssl](img/phase22/ssl_consumer_test.png)

------------------------------------------------------------------------

# 4.7 Summary

Dari percobaan ini saya belajar:

-   generate certificate Kafka
-   membuat keystore dan truststore
-   mengaktifkan TLS pada ZooKeeper
-   mengaktifkan TLS pada Kafka Broker
-   menghubungkan client menggunakan SSL
-   mengatur akses menggunakan ACL

Dengan konfigurasi ini komunikasi **Client → Kafka → ZooKeeper** sudah
berjalan menggunakan **TLS encryption**.
