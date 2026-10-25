<!-- 中文用途说明：开始 -->
# 电脑里的大表格分析｜DuckDB

> **一句话看懂：快速分析电脑里的大表格和数据文件。**

| 你想了解什么 | 中文说明 |
|---|---|
| 这个工具能做什么 | 快速分析电脑里的大表格和数据文件。 |
| 怎么使用 | 用查询语句分析表格文件，适合本地数据整理和汇总。 |
| 适合谁 | 需要合并多个数据文件、计算行业指标的人。 |
| 主要限制 | 多个程序同时直接写同一文件需要协调。 |
| 后续可以怎么改 | 安排统一写入，并限制内存和临时文件大小。 |

**当前状态：代码已复制到这个账号；尚未安装或实际运行验证。上面的修改建议还没有实施。**

[查看中文工具总目录](https://github.com/3416461284a-debug/akshare/tree/research-catalog-2026-10-25/%E8%A1%8C%E4%B8%9A%E7%A0%94%E7%A9%B6%E5%B7%A5%E5%85%B7%E7%AE%B1) · [查看各工具的详细评估](https://github.com/3416461284a-debug/akshare/tree/research-catalog-2026-10-25/%E8%A1%8C%E4%B8%9A%E7%A0%94%E7%A9%B6%E5%B7%A5%E5%85%B7%E7%AE%B1/03_详细报告和核验记录/%E7%83%AD%E9%97%A8%E5%B7%A5%E5%85%B7%E7%BC%BA%E9%99%B7%E4%B8%8E%E6%94%B9%E9%80%A0%E6%8A%A5%E5%91%8A.md)

中文用途整理日期：2026年10月25日。
<!-- 中文用途说明：结束 -->

---

<details>
<summary>原项目详细说明（点击展开）</summary>

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://duckdb.org/images/designmanual/DuckDB_inline-lightmode.svg">
    <source media="(prefers-color-scheme: dark)" srcset="https://duckdb.org/images/designmanual/DuckDB_inline-darkmode.svg">
    <img alt="DuckDB logo" src="https://duckdb.org/images/designmanual/DuckDB_inline-lightmode.svg" height="100">
  </picture>
</div>
<br>

<p align="center">
  <a href="https://github.com/duckdb/duckdb/actions"><img src="https://github.com/duckdb/duckdb/actions/workflows/Main.yml/badge.svg?branch=main" alt="Github Actions Badge"></a>
  <a href="https://discord.gg/tcvwpjfnZx"><img src="https://shields.io/discord/909674491309850675" alt="discord" /></a>
  <a href="https://github.com/duckdb/duckdb/releases/"><img src="https://img.shields.io/github/v/release/duckdb/duckdb?color=brightgreen&display_name=tag&logo=duckdb&logoColor=white" alt="Latest Release"></a>
</p>

## DuckDB

DuckDB is a high-performance analytical database system. It is designed to be fast, reliable, portable, and easy to use. DuckDB runs in-process inside your application, so there is no separate server to manage and no external dependencies. It can also read remote files, query other databases, and connect to other DuckDB instances when needed. It provides a rich SQL dialect with support far beyond basic SQL: arbitrary and nested correlated subqueries, window functions, collations, and complex types (arrays, structs, maps). Its [friendly SQL](https://duckdb.org/docs/current/sql/dialect/friendly_sql.html) extensions add syntax that makes queries shorter and easier to write.

DuckDB is available as a [standalone CLI application](https://duckdb.org/docs/current/clients/cli/overview) and has clients for [Python](https://duckdb.org/docs/current/clients/python/overview), [R](https://duckdb.org/docs/current/clients/r), [Java](https://duckdb.org/docs/current/clients/java), [Rust](https://duckdb.org/docs/current/clients/rust), [Go](https://duckdb.org/docs/current/clients/go), [Wasm](https://duckdb.org/docs/current/clients/wasm/overview), and [many more](https://duckdb.org/docs/current/clients/overview), with deep integrations with packages such as [pandas](https://duckdb.org/docs/current/guides/python/sql_on_pandas).

For more information on using DuckDB, please refer to the [DuckDB documentation](https://duckdb.org/docs/current/).

## Reads and writes any data

DuckDB reads and writes a wide range of file formats, including [CSV](https://duckdb.org/docs/current/data/csv/overview), [Parquet](https://duckdb.org/docs/current/data/parquet/overview), [JSON](https://duckdb.org/docs/current/data/json/overview), and [Excel](https://duckdb.org/docs/current/core_extensions/excel), directly from local disk or from remote endpoints such as S3, HTTP(S), Azure, and Google Cloud Storage. For many of these formats, including CSV, Parquet, and JSON, loading data is as simple as referencing the file in the FROM clause:

```sql
SELECT * FROM 'myfile.csv';
SELECT * FROM 'myfile.parquet';
```

DuckDB also works with open lakehouse formats. [DuckLake](https://ducklake.select/) stores table metadata in a SQL database rather than in metadata files, which removes the need for a separate catalog server while still providing ACID transactions, snapshots, and time travel. DuckDB also supports the [Apache Iceberg](https://duckdb.org/docs/current/core_extensions/iceberg/overview) and [Delta Lake](https://duckdb.org/docs/current/core_extensions/delta) formats. Refer to our [Data Import](https://duckdb.org/docs/current/data/overview) section for more information.

## Connects to other databases

DuckDB can attach to other database systems and query them in place, so you can read, join, and move data across engines without a separate ETL step. It speaks the native protocols of [PostgreSQL](https://duckdb.org/docs/current/core_extensions/postgres/overview), [MySQL](https://duckdb.org/docs/current/core_extensions/mysql), and [SQLite](https://duckdb.org/docs/current/core_extensions/sqlite).

DuckDB instances can also connect to each other over the [quack protocol](https://duckdb.org/docs/current/quack/overview), which turns a DuckDB instance into a server that other DuckDB clients attach to over HTTP.

## Extensible

DuckDB has a modular [extension mechanism](https://duckdb.org/docs/current/extensions/overview): core extensions are bundled with DuckDB, while community and third-party extensions can be installed and loaded at runtime. Extensions add file formats, database connectors, and new functions, types, and more.

## Installation

If you want to install DuckDB, please see [our installation page](https://duckdb.org/docs/installation/) for instructions.

## SQL Reference

The documentation contains a [SQL introduction and reference](https://duckdb.org/docs/current/sql/introduction).

## Development

For development, DuckDB requires [CMake](https://cmake.org), Python 3 and a `C++17` compliant compiler. In the root directory, run `make` to compile the sources. For development, use `make debug` to build a non-optimized debug version. You should run `make unit` and `make allunit` to verify that your version works properly after making changes. To test performance, you can run `BUILD_BENCHMARK=1 BUILD_TPCH=1 make` and then perform several standard benchmarks from the root directory by executing `./build/release/benchmark/benchmark_runner`. The details of benchmarks are in our [Benchmark Guide](benchmark/README.md).

Please also refer to our [Build Guide](https://duckdb.org/docs/current/dev/building/overview) and [Contribution Guide](CONTRIBUTING.md).

## Support

See the [Support Options](https://ducklabs.com/support/) page and the dedicated [`endoflife.date`](https://endoflife.date/duckdb) page.


</details>
