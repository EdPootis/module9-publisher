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