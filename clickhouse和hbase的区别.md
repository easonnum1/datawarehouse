<!-- TOC -->

* [1. 背景](#1-背景)
* [2. 区分点](#2-区分点)
    * [2.1. 数据库类型](#21-数据库类型)
    * [2.2. 存储方式](#22-存储方式)
    * [2.3. 数据模型](#23-数据模型)
    * [2.4. 查询语言](#24-查询语言)
    * [2.5. 数据压缩](#25-数据压缩)
    * [2.6. 查询性能](#26-查询性能)
    * [2.7. 数据一致性](#27-数据一致性)
    * [2.8. 使用场景](#28-使用场景)
    * [2.9. 集成和生态](#29-集成和生态)
    * [2.10. 事务支持](#210-事务支持)
* [3. 总结](#3-总结)

<!-- TOC -->

## 1. 背景

听同事说，ClickHouse 和 HBase 都是`列式存储`，我就好奇，这两个有什么区别。我只知道hbase是一个列式存储的数据库。

记录一下。

## 2. 区分点

ClickHouse 和 HBase 是两种不同类型的数据库系统，各自有独特的特性和适用场景。以下是它们之间的主要区别：

### 2.1. 数据库类型

* ClickHouse：列式数据库`管理系统`。专为大规模数据分析和实时数据处理设计，适用于高性能的数据仓库和分析查询。
* HBase：列式NoSQL`数据库`，是Hadoop生态系统的一部分。设计用于处理大规模结构化数据，特别适合需要快速读写和高可扩展性的场景。

### 2.2. 存储方式

* ClickHouse：使用列式存储，即数据按列而不是按行存储。这种方式优化了读取和压缩性能，`特别适合分析查询`（为什么？）。
* HBase：也使用列式存储，但其设计是为了支持灵活的行和列数据模型，提供快速的读写能力。HBase 的数据是以列族（Column
  Family）的形式存储的。

### 2.3. 数据模型

* ClickHouse：支持结构化数据，采用表格格式存储数据，表结构类似于关系型数据库。数据模型通常包括列、行和表。
* HBase：支持半结构化数据，数据以行和列的形式组织在表中，每个表可以有多个列族，每个列族下可以有多个列。适合处理灵活的数据模型。

### 2.4. 查询语言

* ClickHouse：使用 SQL 语言，支持复杂的查询、聚合、分组等操作。提供了丰富的分析功能。
* HBase：没有内置的查询语言。通常通过 Java API、Thrift、REST 等接口进行操作，查询和数据操作更多依赖于应用程序的逻辑。

### 2.5. 数据压缩

* ClickHouse：内置高效的数据压缩算法，能够显著减少存储需求，提高查询性能。
* HBase：支持多种压缩算法（如 LZO、Snappy、Gzip），可以在数据存储时选择合适的压缩方式。

### 2.6. 查询性能

* ClickHouse：优化了大规模数据的读取和查询性能，特别适合复杂的分析查询和聚合操作。
* HBase：优化了快速的读写操作，适合需要高吞吐量和低延迟的数据访问场景，查询性能与表结构和设计相关。

### 2.7. 数据一致性

* ClickHouse：设计用于数据分析，通常不涉及严格的一致性保证，适用于最终一致性场景。
* HBase：提供了强一致性保证，确保在单行操作中数据的一致性，适用于需要严格数据一致性的场景。

### 2.8. 使用场景

* ClickHouse：适合用于实时分析、大数据仓库、数据报告和商业智能（BI）应用场景。
* HBase：适合用于大数据存储、实时数据处理、日志分析、数据挖掘等场景，特别是在需要高并发读写的环境下表现优异。

### 2.9. 集成和生态

* ClickHouse：通常与数据仓库和分析工具集成良好，如数据可视化工具、ETL 工具等。
* HBase：是 Hadoop 生态系统的一部分，能够与 Hadoop 的其他组件（如 HDFS、MapReduce、Hive）紧密集成，支持大规模的数据处理。

### 2.10. 事务支持

* ClickHouse：不支持复杂的事务处理，主要关注于数据读取和分析。
* HBase：支持单行事务，提供了基本的事务功能以支持数据的原子性操作。

## 3. 总结

总的来说，ClickHouse 和 HBase 各自适合不同的工作负载和应用场景。

* ClickHouse 更加专注于高性能的数据分析和查询，
* HBase 则擅长处理大规模数据存储和快速读写操作。根据具体需求和使用场景选择适合的数据库系统。


