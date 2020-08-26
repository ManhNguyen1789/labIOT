# labIOT
Thiết lập Kafka
Mac
các cửa sổ
Đảm bảo rằng bạn đang ở trong thư mục bin / windows .
Bắt đầu Zookeeper và Kafka Broker
Khởi động Zookeeper.
zookeeper-server-start.bat ..\..\config\zookeeper.properties
Khởi động Kafka Broker.
kafka-server-start.bat ..\..\config\server.properties
Làm thế nào để tạo một chủ đề?
kafka-topics.bat --create --topic test-topic -zookeeper localhost:2181 --replication-factor 1 --partitions 4
Làm cách nào để khởi tạo Console Producer?
Không có chìa khóa
kafka-console-producer.bat --broker-list localhost:9092 --topic test-topic
Cùng với chìa khóa
kafka-console-producer.bat --broker-list localhost:9092 --topic test-topic --property "key.separator=-" --property "parse.key=true"
Làm thế nào để khởi tạo Người tiêu dùng bảng điều khiển?
Không có chìa khóa
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning
Cùng với chìa khóa
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning -property "key.separator= - " --property "print.key=true"
Với nhóm người tiêu dùng
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --group <group-name>
Thiết lập nhiều nhà môi giới Kafka
Bước đầu tiên là thêm một server.properties mới .

Chúng tôi cần sửa đổi ba thuộc tính để bắt đầu thiết lập nhiều nhà môi giới.

broker.id=<unique-broker-d>
listeners=PLAINTEXT://localhost:<unique-port>
log.dirs=/tmp/<unique-kafka-folder>
auto.create.topics.enable=false
Cấu hình ví dụ sẽ như dưới đây.
broker.id=1
listeners=PLAINTEXT://localhost:9093
log.dirs=/tmp/kafka-logs-1
auto.create.topics.enable=false
Khởi động Nhà môi giới mới
Cung cấp server.properties mới đã được thêm vào.
./kafka-server-start.sh ../config/server-1.properties
./kafka-server-start.sh ../config/server-2.properties
Hoạt động Kafka CLI nâng cao:
Mac
các cửa sổ
Đảm bảo rằng bạn đang ở trong thư mục bin / windows .
Liệt kê các chủ đề trong một cụm
kafka-topics.bat --zookeeper localhost:2181 --list
Mô tả chủ đề
Lệnh dưới đây có thể được sử dụng để mô tả tất cả các chủ đề.
kafka-topics.bat --zookeeper localhost:2181 --describe
Lệnh dưới đây có thể được sử dụng để mô tả một chủ đề cụ thể.
kafka-topics.bat --zookeeper localhost:2181 --describe --topic <topic-name>
Thay đổi bản sao thiếu đồng bộ
kafka-topics.bat --alter --zookeeper localhost:2181 --topic library-events --config min.insync.replicas=2
Xóa chủ đề
kafka-topics.bat --zookeeper localhost:2181 --delete --topic <topic-name>
Cách xem các nhóm người tiêu dùng
kafka-consumer-groups.bat --bootstrap-server localhost:9092 --list
Nhóm người tiêu dùng và sự bù đắp của họ
kafka-consumer-groups.bat --bootstrap-server localhost:9092 --describe --group console-consumer-27773
Xem Nhật ký cam kết
kafka-run-class.bat kafka.tools.DumpLogSegments --deep-iteration --files /tmp/kafka-logs/test-topic-0/00000000000000000000.log
