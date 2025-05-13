# Advanced Programming Module 9 Publisher
**Nama: Edmond Christian**<br>
**NPM: 2306208363**

### Reflection 1
a. How much data your publisher program will send to the message broker in one run?

```rust
fn main() {
    let mut p =
        CrosstownBus::new_queue_publisher("amqp://guest:guest@localhost:5672".to_owned(
        )).unwrap();
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage {
        user_id: "1".to_owned(), user_name: "2306208363-Amir".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage {
        user_id: "2".to_owned(), user_name: "2306208363-Budi".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage {
        user_id: "3".to_owned(), user_name: "2306208363-Cica".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage {
        user_id: "4".to_owned(), user_name: "2306208363-Dira".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage {
        user_id: "5".to_owned(), user_name: "2306208363-Emir".to_owned() });
}
```
- Berdasarkan kode di `main.rs` *publisher* akan mengirimkan data sebanyak 5 kali ke *message broker* setiap kali dijalankan.

b. The url of: “`amqp://guest:guest@localhost:5672`” is the same as in the subscriber program, what does it mean?
- `amqp://guest:guest@localhost:5672` adalah URL koneksi yang digunakan oleh aplikasi *publisher* dan *subscriber*. Hal ini berarti bahwa keduanya akan terhubung ke *instance message broker* RabbitMQ yang sama juga. Dengan ini, *publisher* dapat mengirim/*publish* pesan/data ke *message broker* dan *subscriber* akan menerima pesan yang dikirim tersebut dari *broker*.

### Running RabbitMQ as message broker.
![Running RabbitMQ as message broker.](RunningRabbitMQ.png)

### Sending & Processing Event
![Sending & Processing Event](SendingProcessingEvent.png)
Saat *subscriber* sudah terkoneksi ke RabbitMQ dan *publisher* dijalankan, maka publisher akan mengirim 5 pesan/data ke *broker* yang kemudian subscriber akan terima.

### Monitoring Chart on RabbitMQ Browser
![Monitoring Image](MonitoringChart.png)
Grafik kedua yang memiliki lonjakan pada browser RabbitMQ mengukur *rate* atau kecepatan pesan/data yang dikirim dalam interval tertentu. Pada gambar terdapat lonjakan garis kuning dan garis ungu. Garis ungu menandakan pesan yang mendapat *consumer acknowledgement* atau diterima, sementara garis kuning menandakan pesan yang di-*publish* atau dikirim. Lonjakan kedua garis tersebut terjadi karena *publisher* di run sehingga dari 0 pesan yang di*publish* dan diterima *subscriber* menjadi 5 atau lebih jika dijalankan beberapa kali dalam waktu yang cepat.


## Bonus
### Sending & Processing Event (Cloud)
![Bonus1](BonusSendingProcessingEvent.png)
Sama seperti di `localhost`, jika *subscriber* dan *publisher* sudah disambungkan ke *message broker* yang sama maka akan terjadi pengiriman dan penerimaan pesan. Perbedaan yang *noticeable* adalah tidak dapat meng-*spam* *run* publisher dalam waktu yang singkat, karena sekarang terdapat delay dalam menjalakannya. Hal itu disebabkan *publisher* mencoba menyambungkan dirinya dengan RabbitMQ yang berada di cloud dan tidak secepat menyabungkand dirinya dengan *localhost*.

### Monitoring Chart on RabbitMQ Browser (Cloud)
![Bonus2](BonusMonitoringChart.png)
Tidak terdapat perbedaan yang banyak pada monitoring chart di *localhost* dan *cloud*. Jika *publisher* dijalankan sekali maka akan terjadi lonjakan dalam mengirim 5 pesan yang kemudian akan diterima oleh *subscriber*.