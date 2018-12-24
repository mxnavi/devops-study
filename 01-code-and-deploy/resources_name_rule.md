## 资源命名规则

***[该文档未包含的中间件，请与运维定义命名规则]***

通常中间件会有简单的隔离机制，而各类 **服务** 必须支持使用中间件的隔离功能，例如：数据库中的 database、Hbase中的namespace等；在服务的生命周期中，这些隔离机制的命名与服务ID一一对应，以便我们再服务生命周期结束时，通过命名规则进行回收；

**首先我们遵守以下命名规则：**

* 能够直接采用 服务ID 命名的，直接使用

* 服务ID 与中间件命名规则冲突的，可以适当进行转换，例如：Mysql 不支持中间横杠“-”，可以使用下横杠“_”

* 中间件不支持英文命名，例如：Redis 仅支持 database index，代码需同时支持： database index 、 所有key前缀，例如：服务支持运维配置，在 index为：0 的Redis 库中存储 {服务ID}_key : {value}

* 多服务共享中间件，可以数据生产方命名，例如：pnavi-data-collect 与 pnavi-data-storage 都使用 kafka，其中 pnavi-data-collect 负责kafka的数据生产，那么他们使用kakfa topic 名称为 pnavi-data-collect

* 🚫除极特殊情况，禁止多类型服务共同对同一个中间件进行数据生产、更改操作，如果避免不了，应使用 **资源主要使用方** 进行命名

----

### Mysql、TiDB database 命名规则：

服务ID中的 “-”【英文中横杠】 变更为 “_”【英文下横杠】，例如： 

* 服务ID: pnavi-data-collect , 数据库名称： pnavi_data_collect
* 如果一个服务对应多个数据库，数据库名称可以使用增加双下横线+用途：pnavi_data_collect__log_collect 、pnavi_data_collect__user_info_collect

----

### Postgresql Database 命名规则[TODO，需要注意，Postgresql 有 namespace 维度]：
需支持：服务 对应 多个数据库

----

### Redis 命名规则

由于Redis仅支持 0 - x 的数据库命名：
* 服务需支持配置 使用 0 - x 的任意数据库
* 服务需支持： 服务ID前缀_自定义 = value ，例如：pnavi_data_collect 存储用户 daigong 信息，Redis 中存储的结构：{ key : pnavi_data_collect_daigong ，value： some_info }

----

### Kafka topic 命名规则 [TODO]
需举例，一个服务同时拥有生产数据、消费数据 多个topic

----

### Mongodb 命名规则 [TODO]

### Zookeeper 命名规则 [TODO]

### HDFS 命名规则 [TODO]
### Hive 命名规则 [TODO]
### Kylin 命名规则 [TODO]