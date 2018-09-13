---
title: Phoenix performance in Azure HDInsight
description: Best practices to optimize Phoenix performance.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: ashishth
ms.openlocfilehash: ff194ef7f5ae609eba5334eb5c66db02d660ab08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866019"
---
# <a name="phoenix-performance-best-practices"></a>Phoenix performance best practices

The most important aspect of Phoenix performance is to optimize the underlying HBase. Phoenix creates a relational data model atop HBase that converts SQL queries into HBase operations, such as scans. The design of your table schema, the selection and ordering of the fields in your primary key, and your use of indexes all affect Phoenix performance.

## <a name="table-schema-design"></a>Table schema design

When you create a table in Phoenix, that table is stored in an HBase table. The HBase table contains groups of columns (column families) that are accessed together. A row in the Phoenix table is a row in the HBase table, where each row consists of versioned cells associated with one or more columns. Logically, a single HBase row is a collection of key-value pairs, each having the same rowkey value. That is, each key-value pair has a rowkey attribute, and the value of that rowkey attribute is the same for a particular row.

The schema design of a Phoenix table includes the primary key design, column family design, individual column design, and how the data is partitioned.

### <a name="primary-key-design"></a>Primary key design

The primary key defined on a table in Phoenix determines how data is stored within the rowkey of the underlying HBase table. In HBase, the only way to access a particular row is with the rowkey. In addition, data stored in an HBase table is sorted by the rowkey. Phoenix builds the rowkey value by concatenating the values of each of the columns in the row, in the order they are defined in the primary key.

For example, a table for contacts has the first name, last name, phone number, and address, all in the same column family. You could define a primary key based on an increasing sequence number:

|rowkey|       address|   phone| firstName| lastName|
|------|--------------------|--------------|-------------|--------------|
|  1000|1111 San Gabriel Dr.|1-425-000-0002|    John|Dole|
|  8396|5415 San Gabriel Dr.|1-230-555-0191|  Calvin|Raji|

However, if you frequently query by lastName this primary key may not perform well, because each query requires a full table scan to read the value of every lastName. Instead, you can define a primary key on the lastName, firstName, and social security number columns. This last column is to disambiguate two residents at the same address with the same name, such as a father and son.

|rowkey|       address|   phone| firstName| lastName| socialSecurityNum |
|------|--------------------|--------------|-------------|--------------| ---|
|  1000|1111 San Gabriel Dr.|1-425-000-0002|    John|Dole| 111 |
|  8396|5415 San Gabriel Dr.|1-230-555-0191|  Calvin|Raji| 222 |

With this new primary key the row keys generated by Phoenix would be:

|rowkey|       address|   phone| firstName| lastName| socialSecurityNum |
|------|--------------------|--------------|-------------|--------------| ---|
|  Dole-John-111|1111 San Gabriel Dr.|1-425-000-0002|    John|Dole| 111 |
|  Raji-Calvin-222|5415 San Gabriel Dr.|1-230-555-0191|  Calvin|Raji| 222 |

In the first row above, the data for the rowkey is represented as shown:

|rowkey|       key|   value| 
|------|--------------------|---|
|  Dole-John-111|address |1111 San Gabriel Dr.|  
|  Dole-John-111|phone |1-425-000-0002|  
|  Dole-John-111|firstName |John|  
|  Dole-John-111|lastName |Dole|  
|  Dole-John-111|socialSecurityNum |111| 

This rowkey now stores a duplicate copy of the data. Consider the size and number of columns you include in your primary key, because this value is included with every cell in the underlying HBase table.

Also, if the primary key has values that are monotonically increasing, you should create the table with *salt buckets* to help avoid creating write hotspots - see [Partition data](#partition-data).

### <a name="column-family-design"></a>Column family design

If some columns are accessed more frequently than others, you should create multiple column families to separate the frequently accessed columns from rarely accessed columns.

Also, if certain columns tend to be accessed together, put those columns in the same column family.

### <a name="column-design"></a>Column design

* Keep VARCHAR columns under about 1 MB due to the I/O costs of large columns. When processing queries, HBase materializes cells in full before sending them over to the client, and the client receives them in full before handing them off to the application code.
* Store column values using a compact format such as protobuf, Avro, msgpack, or BSON. JSON is not recommended, as it is larger.
* Consider compressing data before storage to cut latency and I/O costs.

### <a name="partition-data"></a>Partition data

Phoenix enables you to control the number of regions where your data is distributed, which can significantly increase read/write performance. When creating a Phoenix table, you can either salt or pre-split your data.

To salt a table during creation, specify the number of salt buckets:

    CREATE TABLE CONTACTS (...) SALT_BUCKETS = 16

This salting splits the table along the values of primary keys, choosing the values automatically. 

To control where the table splits occur, you can pre-split the table by providing the range values along which the splitting occurs. For example, to create a table split along three regions:

    CREATE TABLE CONTACTS (...) SPLIT ON ('CS','EU','NA')

## <a name="index-design"></a>Index design

A Phoenix index is an HBase table that stores a copy of some or all of the data from the indexed table. An index improves performance for specific types of queries.

When you have multiple indexes defined and then query a table, Phoenix automatically selects the best index for the query. The primary index is created automatically based on the primary keys you select.

For anticipated queries, you can also create secondary indexes by specifying their columns.

When designing your indexes:

* Only create the indexes you need.
* Limit the number of indexes on frequently updated tables. Updates to a table translate into writes to both the main table and the index tables.

## <a name="create-secondary-indexes"></a>Create secondary indexes

Secondary indexes can improve read performance by turning what would be a full table scan into a point lookup, at the cost of storage space and write speed. Secondary indexes can be added or removed after table creation and don’t require changes to existing queries – queries just run faster. Depending on your needs, consider creating covered indexes, functional indexes, or both.

### <a name="use-covered-indexes"></a>Use covered indexes

Covered indexes are indexes that include data from the row in addition to the values that are indexed. After finding the desired index entry, there is no need to access the primary table.

For example, in the example contact table you could create a secondary index on just the socialSecurityNum column. This secondary index would speed up queries that filter by socialSecurityNum values, but retrieving other field values will require another read against the main table.

|rowkey|       address|   phone| firstName| lastName| socialSecurityNum |
|------|--------------------|--------------|-------------|--------------| ---|
|  Dole-John-111|1111 San Gabriel Dr.|1-425-000-0002|    John|Dole| 111 |
|  Raji-Calvin-222|5415 San Gabriel Dr.|1-230-555-0191|  Calvin|Raji| 222 |

However, if you typically want to look up the firstName and lastName given the socialSecurityNum, you could create a covered index that includes the firstName and lastName as actual data in the index table:

    CREATE INDEX ssn_idx ON CONTACTS (socialSecurityNum) INCLUDE(firstName, lastName);

This covered index enables the following query to acquire all data just by reading from the table containing the secondary index:

    SELECT socialSecurityNum, firstName, lastName FROM CONTACTS WHERE socialSecurityNum > 100;

### <a name="use-functional-indexes"></a>Use functional indexes

Functional indexes allow you to create an index on an arbitrary expression that you expect to be used in queries. Once you have a functional index in place and a query uses that expression, the index may be used to retrieve the results rather than the data table.

For example, you could create an index to allow you to do case-insensitive searches on the combined first name and last name of a person:

     CREATE INDEX FULLNAME_UPPER_IDX ON "Contacts" (UPPER("firstName"||' '||"lastName"));

## <a name="query-design"></a>Query design

The main considerations in query design are:

* Understand the query plan and verify its expected behavior.
* Join efficiently.

### <a name="understand-the-query-plan"></a>Understand the query plan

In [SQLLine](http://sqlline.sourceforge.net/), use EXPLAIN followed by your SQL query to view the plan of operations that Phoenix will perform. Check that the plan:

* Uses your primary key when appropriate.
* Uses appropriate secondary indexes, rather than the data table.
* Uses RANGE SCAN or SKIP SCAN whenever possible, rather than TABLE SCAN.

#### <a name="plan-examples"></a>Plan examples

As an example, say you have a table called FLIGHTS that stores flight delay information.

To select all the flights with an airlineid of `19805`, where airlineid is a field that is not in the primary key or in any index:

    select * from "FLIGHTS" where airlineid = '19805';

Run the explain command as follows:

    explain select * from "FLIGHTS" where airlineid = '19805';

The query plan looks like this:

    CLIENT 1-CHUNK PARALLEL 1-WAY ROUND ROBIN FULL SCAN OVER FLIGHTS
        SERVER FILTER BY AIRLINEID = '19805'

In this plan, note the phrase FULL SCAN OVER FLIGHTS. This phrase indicates the execution does a TABLE SCAN over all rows in the table, rather than using the more efficient RANGE SCAN or SKIP SCAN option.

Now, say you want to query for flights on January 2, 2014 for the carrier `AA` where its flightnum was greater than 1. Let's assume that the columns year, month, dayofmonth, carrier, and flightnum exist in the example table, and are all part of the composite primary key. The query would look as follows:

    select * from "FLIGHTS" where year = 2014 and month = 1 and dayofmonth = 2 and carrier = 'AA' and flightnum > 1;

Let's examine the plan for this query with:

    explain select * from "FLIGHTS" where year = 2014 and month = 1 and dayofmonth = 2 and carrier = 'AA' and flightnum > 1;

The resulting plan is:

    CLIENT 1-CHUNK PARALLEL 1-WAY ROUND ROBIN RANGE SCAN OVER FLIGHTS [2014,1,2,'AA',2] - [2014,1,2,'AA',*]

The values in square brackets are the range of values for the primary keys. In this case, the range values are fixed with year 2014, month 1, and dayofmonth 2, but allow values for flightnum starting with 2 and on up (`*`). This query plan confirms that the primary key is being used as expected.

Next, create an index on the FLIGHTS table named `carrier2_idx` that is on the carrier field only. This index also includes flightdate, tailnum, origin, and flightnum as covered columns whose data is also stored in the index.

    CREATE INDEX carrier2_idx ON FLIGHTS (carrier) INCLUDE(FLIGHTDATE,TAILNUM,ORIGIN,FLIGHTNUM);

Say you want to get the carrier along with the flightdate and tailnum, as in the following query:

    explain select carrier,flightdate,tailnum from "FLIGHTS" where carrier = 'AA';

You should see this index being used:

    CLIENT 1-CHUNK PARALLEL 1-WAY ROUND ROBIN RANGE SCAN OVER CARRIER2_IDX ['AA']

For a complete listing of the items that can appear in explain plan results, see the Explain Plans section in the [Apache Phoenix Tuning Guide](https://phoenix.apache.org/tuning_guide.html).

### <a name="join-efficiently"></a>Join efficiently

Generally, you want to avoid joins unless one side is small, especially on frequent queries.

If necessary, you can do large joins with the `/*+ USE_SORT_MERGE_JOIN */` hint, but a large join is an expensive operation over huge numbers of rows. If the overall size of all right-hand-side tables would exceed the available memory, use the `/*+ NO_STAR_JOIN */` hint.

## <a name="scenarios"></a>Scenarios

The following guidelines describe some common patterns.

### <a name="read-heavy-workloads"></a>Read-heavy workloads

For read-heavy use cases, make sure you are using indexes. Additionally, to save read-time overhead, consider creating covered indexes.

### <a name="write-heavy-workloads"></a>Write-heavy workloads

For write-heavy workloads where the primary key is monotonically increasing, create salt buckets to help avoid write hotspots, at the expense of overall read throughput due to the additional scans needed. Also, when using UPSERT to write a large number of records, turn off autoCommit and batch up the records.

### <a name="bulk-deletes"></a>Bulk deletes

When deleting a large data set, turn on autoCommit before issuing the DELETE query, so that the client does not need to remember the row keys for all deleted rows. AutoCommit prevents the client from buffering the rows affected by the DELETE, so that Phoenix can delete them directly on the region servers without the expense of returning them to the client.

### <a name="immutable-and-append-only"></a>Immutable and Append-only

If your scenario favors write speed over data integrity, consider disabling the write-ahead log when creating your tables:

    CREATE TABLE CONTACTS (...) DISABLE_WAL=true;

For details on this and other options, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html#options).

## <a name="next-steps"></a>Next steps

* [Phoenix Tuning Guide](https://phoenix.apache.org/tuning_guide.html)
* [Secondary Indexes](http://phoenix.apache.org/secondary_indexing.html)