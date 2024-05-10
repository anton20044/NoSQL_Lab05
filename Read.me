Лабораторная работа №5 по курсу NoSQL.

Задание:
	- развернуть БД;
	- выполнить импорт тестовой БД;
	- выполнить несколько запросов и оценить скорость выполнения.
	- развернуть дополнительно одну из тестовых БД https://clickhouse.com/docs/en/getting-started/example-datasets , протестировать скорость запросов
	- развернуть Кликхаус в кластерном исполнении, создать распределенную таблицу, заполнить данными и протестировать скорость по сравнению с 1 инстансом

Решение:

1) Развернута виртуальная машина, на которую установлен ClickHouse.
2) В качестве тестового датасета выбран covid19(https://clickhouse.com/docs/en/getting-started/example-datasets/covid19)
3) Создана таблица covid19, в нее импортирован датасет 
3) Выполнены запросы к датасету (см рисунок 1), средняя скорость выборки 0, 178 секунд при выборке 12,5 млн строк
4) Развернул еще 4 виртуальных машины. На трех установил ZooKeeper и собрал из них кластер. 
5) На четвертой виртуальной машине установил ClickHouse.
6) На обоих ВМ с ClickHouse добавил конфиги в каталог /etc/clickhouse-server/config.d/:
 - конфиг для работы с ZooKeeper
 <clickhouse>
        <zookeeper>
            <node index="1">
                <host>192.168.50.100</host>
                <port>2181</port>
            </node>
            <node index="2">
                <host>192.168.50.101</host>
                <port>2181</port>
            </node>
            <node index="3">
                <host>192.168.50.150</host>
                <port>2181</port>
            </node>
        </zookeeper>
</clickhouse>
 - конфиг для работы в кластерном режиме (для теста использовалась конфигурация из двух шардов, в каждом шарде по одной реплике)
 <clickhouse>
        <remote_servers>
                <cluster>
                        <shard>
                            <replica>
                                <host>192.168.50.142</host>
                                <port>9000</port>
                                <user>default</user>
                                <password>123</password>
                            </replica>
                        </shard>
                        <shard>
                            <replica>
                                <host>192.168.50.143</host>
                                <port>9000</port>
                                <user>default</user>
                                <password>123</password>
                            </replica>
                        </shard>
                    </cluster>
        </remote_servers>
</clickhouse>
 - конфиг для работы по сети
 <clickhouse>
    <listen_host>::</listen_host>
</clickhouse>
7) В качестве распределенного датасета выбран nyc-taxi (https://clickhouse.com/docs/en/getting-started/example-datasets/nyc-taxi)
8) Была создана локальная таблица trips_local с директивой ON CLUSTER cluster (для создание таблицы на всех шардах и репликах)

CREATE TABLE trips_local ON CLUSTER cluster
(
    `trip_id` UInt32,
    `pickup_datetime` DateTime,
    `dropoff_datetime` DateTime,
    `pickup_longitude` Nullable(Float64),
    `pickup_latitude` Nullable(Float64),
    `dropoff_longitude` Nullable(Float64),
    `dropoff_latitude` Nullable(Float64),
    `passenger_count` UInt8,
    `trip_distance` Float32,
    `fare_amount` Float32,
    `extra` Float32,
    `tip_amount` Float32,
    `tolls_amount` Float32,
    `total_amount` Float32,
    `payment_type` Enum('CSH' = 1, 'CRE' = 2, 'NOC' = 3, 'DIS' = 4, 'UNK' = 5),
    `pickup_ntaname` LowCardinality(String),
    `dropoff_ntaname` LowCardinality(String)
)
ENGINE = MergeTree
PRIMARY KEY (pickup_datetime, dropoff_datetime)

9) Была создана таблица с движком Distributed, в качетсве ключа шардирования указана функция rand()

CREATE TABLE trips ON CLUSTER cluster AS trips_local
ENGINE = Distributed(cluster, default, trips_local,  rand()) 

10) В распределенную таблицу trips вставлен датасет. Датасет был распределен между двумя нодами (см рисунок 2, 3)
