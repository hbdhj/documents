# MySQL 与 Mongodb 常用命令对比

| 任务            | MySQL                  | mongodb              |
| --------------- |------------------------| --------------------|
| 创建数据库 | create database db_name | 同选择数据库 |
| 列出数据库       | show databases | show dbs |
| 选择数据库      | use db_name   | use db_name  |
| 当前数据库 | select database()    | db |
| 删除数据库 | drop database db_name | db.dropDatabase() |
| 创建数据表 | create table ``<table_name>`` (...) | 同插入数据 |
| 列出数据表 | show tables | show collections |
| 查询数据表 | select ``<field_id_list>`` from ``<table_name>`` | db.``<col_name>``.find(``<cond>``) |
| 条件查询   | select ``<field_id_list>`` where * | db.``<col_name>``.find(<cond>) |
| 插入数据   | insert into ``<table_name>`` ...  | db.``<col_name>``.insert({...}) |
| 更新数据   | update ``<table_name>`` set ... where ...  | db.``<col_name>``.update(``<query>``,``<update>``{...}) |
| 删除数据表 | drop table ``<table_name>`` | db.``<col_name>``.remove(...) |
| 建立索引   | create index ``<index_name>`` on ``<table_name>``(field) | db.``<col_name>``.ensureIndex({<field_name>:1}) |
| 删除索引   | drop index ``<index_name>`` on ``<table_name>`` | db.``<col_name>``.dropIndex({<field_name>:1}) |
| 排序   | select ``<field_id_list>`` from ``<table_name>`` ordered by ``<field_name>`` | db.``<col_name>``.find().sort({KEY:1}) |
| 限定   | select ``<field_id_list>`` from ``<table_name>`` limit ``<start>``,``<end>`` | db.``<col_name>``.find().limit(NUMBER) |
| 排除   | 同限定 | db.``<col_name>``.find().skip(NUMBER) |
