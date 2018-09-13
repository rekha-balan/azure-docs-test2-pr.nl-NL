---
title: Apache Phoenix in HDInsight - Azure HDInsight
description: ''
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/19/2018
ms.author: ashishth
ms.openlocfilehash: d86600dd000d3e9c71a38b632aa75e82239401dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868765"
---
# <a name="apache-phoenix-in-hdinsight"></a><span data-ttu-id="fb817-102">Apache Phoenix in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb817-102">Apache Phoenix in HDInsight</span></span>

<span data-ttu-id="fb817-103">[Apache Phoenix](http://phoenix.apache.org/) is an open source, massively parallel relational database layer built on [HBase](hbase/apache-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb817-103">[Apache Phoenix](http://phoenix.apache.org/) is an open source, massively parallel relational database layer built on [HBase](hbase/apache-hbase-overview.md).</span></span> <span data-ttu-id="fb817-104">Phoenix allows you to use SQL-like queries over HBase.</span><span class="sxs-lookup"><span data-stu-id="fb817-104">Phoenix allows you to use SQL-like queries over HBase.</span></span> <span data-ttu-id="fb817-105">Phoenix uses JDBC drivers underneath to enable users to create, delete, alter SQL tables, indexes, views and sequences, and upsert rows individually and in bulk.</span><span class="sxs-lookup"><span data-stu-id="fb817-105">Phoenix uses JDBC drivers underneath to enable users to create, delete, alter SQL tables, indexes, views and sequences, and upsert rows individually and in bulk.</span></span> <span data-ttu-id="fb817-106">Phoenix uses noSQL native compilation rather than using MapReduce to compile queries, enabling the creation of low-latency applications on top of HBase.</span><span class="sxs-lookup"><span data-stu-id="fb817-106">Phoenix uses noSQL native compilation rather than using MapReduce to compile queries, enabling the creation of low-latency applications on top of HBase.</span></span> <span data-ttu-id="fb817-107">Phoenix adds coprocessors to support running client-supplied code in the address space of the server, executing the code colocated with the data.</span><span class="sxs-lookup"><span data-stu-id="fb817-107">Phoenix adds coprocessors to support running client-supplied code in the address space of the server, executing the code colocated with the data.</span></span> <span data-ttu-id="fb817-108">This approach minimizes client/server data transfer.</span><span class="sxs-lookup"><span data-stu-id="fb817-108">This approach minimizes client/server data transfer.</span></span>

<span data-ttu-id="fb817-109">Apache Phoenix opens up big data queries to non-developers who can use  an SQL-like syntax rather than programming.</span><span class="sxs-lookup"><span data-stu-id="fb817-109">Apache Phoenix opens up big data queries to non-developers who can use  an SQL-like syntax rather than programming.</span></span> <span data-ttu-id="fb817-110">Phoenix is highly optimized for HBase, unlike other tools such as [Hive](hadoop/hdinsight-use-hive.md) and Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="fb817-110">Phoenix is highly optimized for HBase, unlike other tools such as [Hive](hadoop/hdinsight-use-hive.md) and Spark SQL.</span></span> <span data-ttu-id="fb817-111">The benefit to developers is writing highly performant queries with much less code.</span><span class="sxs-lookup"><span data-stu-id="fb817-111">The benefit to developers is writing highly performant queries with much less code.</span></span>
<!-- [Spark SQL](spark/apache-spark-sql-with-hdinsight.md)  -->

<span data-ttu-id="fb817-112">When you submit a SQL query, Phoenix compiles the query to HBase native calls and runs the scan (or plan) in parallel for optimization.</span><span class="sxs-lookup"><span data-stu-id="fb817-112">When you submit a SQL query, Phoenix compiles the query to HBase native calls and runs the scan (or plan) in parallel for optimization.</span></span> <span data-ttu-id="fb817-113">This layer of abstraction frees the developer from writing MapReduce jobs,  to focus instead on the business logic and the workflow of their application around Phoenix's big data storage.</span><span class="sxs-lookup"><span data-stu-id="fb817-113">This layer of abstraction frees the developer from writing MapReduce jobs,  to focus instead on the business logic and the workflow of their application around Phoenix's big data storage.</span></span>

## <a name="query-performance-optimization-and-other-features"></a><span data-ttu-id="fb817-114">Query performance optimization and other features</span><span class="sxs-lookup"><span data-stu-id="fb817-114">Query performance optimization and other features</span></span>

<span data-ttu-id="fb817-115">Apache Phoenix adds several performance enhancements and  features to  HBase queries.</span><span class="sxs-lookup"><span data-stu-id="fb817-115">Apache Phoenix adds several performance enhancements and  features to  HBase queries.</span></span>

### <a name="secondary-indexes"></a><span data-ttu-id="fb817-116">Secondary indexes</span><span class="sxs-lookup"><span data-stu-id="fb817-116">Secondary indexes</span></span>

<span data-ttu-id="fb817-117">HBase has a single index that is lexicographically sorted on the primary row key.</span><span class="sxs-lookup"><span data-stu-id="fb817-117">HBase has a single index that is lexicographically sorted on the primary row key.</span></span> <span data-ttu-id="fb817-118">These records can only be accessed through the row key.</span><span class="sxs-lookup"><span data-stu-id="fb817-118">These records can only be accessed through the row key.</span></span> <span data-ttu-id="fb817-119">Accessing records through any column other than the row key requires scanning all of the data while applying the required filter.</span><span class="sxs-lookup"><span data-stu-id="fb817-119">Accessing records through any column other than the row key requires scanning all of the data while applying the required filter.</span></span> <span data-ttu-id="fb817-120">In a secondary index, the columns or expressions that are indexed form an alternate row key, allowing lookups and range scans on that index.</span><span class="sxs-lookup"><span data-stu-id="fb817-120">In a secondary index, the columns or expressions that are indexed form an alternate row key, allowing lookups and range scans on that index.</span></span>

<span data-ttu-id="fb817-121">Create a secondary index with the `CREATE INDEX` command:</span><span class="sxs-lookup"><span data-stu-id="fb817-121">Create a secondary index with the `CREATE INDEX` command:</span></span>

```sql
CREATE INDEX ix_purchasetype on SALTEDWEBLOGS (purchasetype, transactiondate) INCLUDE (bookname, quantity);
```

<span data-ttu-id="fb817-122">This approach can yield a significant performance increase over executing single-indexed queries.</span><span class="sxs-lookup"><span data-stu-id="fb817-122">This approach can yield a significant performance increase over executing single-indexed queries.</span></span> <span data-ttu-id="fb817-123">This type of secondary index is a **covering index**,  containing all of the columns included in the query.</span><span class="sxs-lookup"><span data-stu-id="fb817-123">This type of secondary index is a **covering index**,  containing all of the columns included in the query.</span></span> <span data-ttu-id="fb817-124">Therefore, the table lookup is not required and the index satisfies the entire query.</span><span class="sxs-lookup"><span data-stu-id="fb817-124">Therefore, the table lookup is not required and the index satisfies the entire query.</span></span>

### <a name="views"></a><span data-ttu-id="fb817-125">Views</span><span class="sxs-lookup"><span data-stu-id="fb817-125">Views</span></span>

<span data-ttu-id="fb817-126">Phoenix views provide a  way to overcome an  HBase limitation, where performance begins to degrade when you create more than about 100 physical tables.</span><span class="sxs-lookup"><span data-stu-id="fb817-126">Phoenix views provide a  way to overcome an  HBase limitation, where performance begins to degrade when you create more than about 100 physical tables.</span></span> <span data-ttu-id="fb817-127">Phoenix views enable multiple *virtual tables* to share one underlying physical HBase table.</span><span class="sxs-lookup"><span data-stu-id="fb817-127">Phoenix views enable multiple *virtual tables* to share one underlying physical HBase table.</span></span>

<span data-ttu-id="fb817-128">Creating a Phoenix view is  similar to using standard SQL view syntax.</span><span class="sxs-lookup"><span data-stu-id="fb817-128">Creating a Phoenix view is  similar to using standard SQL view syntax.</span></span> <span data-ttu-id="fb817-129">One difference is that you can define columns for your view, in addition to the columns inherited from its base table.</span><span class="sxs-lookup"><span data-stu-id="fb817-129">One difference is that you can define columns for your view, in addition to the columns inherited from its base table.</span></span> <span data-ttu-id="fb817-130">You can also  add new `KeyValue` columns.</span><span class="sxs-lookup"><span data-stu-id="fb817-130">You can also  add new `KeyValue` columns.</span></span>

<span data-ttu-id="fb817-131">For example, here is a physical table named `product_metrics` with the following definition:</span><span class="sxs-lookup"><span data-stu-id="fb817-131">For example, here is a physical table named `product_metrics` with the following definition:</span></span>

```sql
CREATE  TABLE product_metrics (
    metric_type CHAR(1),
    created_by VARCHAR, 
    created_date DATE, 
    metric_id INTEGER
    CONSTRAINT pk PRIMARY KEY (metric_type, created_by, created_date, metric_id));
```

<span data-ttu-id="fb817-132">Define a view over this table, with additional columns:</span><span class="sxs-lookup"><span data-stu-id="fb817-132">Define a view over this table, with additional columns:</span></span>

```sql
CREATE VIEW mobile_product_metrics (carrier VARCHAR, dropped_calls BIGINT) AS
SELECT * FROM product_metrics
WHERE metric_type = 'm';
```

<span data-ttu-id="fb817-133">To add more columns later,  use the `ALTER VIEW` statement.</span><span class="sxs-lookup"><span data-stu-id="fb817-133">To add more columns later,  use the `ALTER VIEW` statement.</span></span>

### <a name="skip-scan"></a><span data-ttu-id="fb817-134">Skip scan</span><span class="sxs-lookup"><span data-stu-id="fb817-134">Skip scan</span></span>

<span data-ttu-id="fb817-135">Skip scan uses one or more columns of a composite index to find distinct values.</span><span class="sxs-lookup"><span data-stu-id="fb817-135">Skip scan uses one or more columns of a composite index to find distinct values.</span></span> <span data-ttu-id="fb817-136">Unlike a range scan, skip scan implements intra-row scanning, yielding [improved performance](http://phoenix.apache.org/performance.html#Skip-Scan).</span><span class="sxs-lookup"><span data-stu-id="fb817-136">Unlike a range scan, skip scan implements intra-row scanning, yielding [improved performance](http://phoenix.apache.org/performance.html#Skip-Scan).</span></span> <span data-ttu-id="fb817-137">While scanning, the first matched value is skipped along with the index until the next value is found.</span><span class="sxs-lookup"><span data-stu-id="fb817-137">While scanning, the first matched value is skipped along with the index until the next value is found.</span></span>

<span data-ttu-id="fb817-138">A skip scan uses the `SEEK_NEXT_USING_HINT` enumeration of the HBase filter.</span><span class="sxs-lookup"><span data-stu-id="fb817-138">A skip scan uses the `SEEK_NEXT_USING_HINT` enumeration of the HBase filter.</span></span> <span data-ttu-id="fb817-139">Using `SEEK_NEXT_USING_HINT`, the skip scan keeps track of which set of keys, or ranges of keys, are being searched for in each column.</span><span class="sxs-lookup"><span data-stu-id="fb817-139">Using `SEEK_NEXT_USING_HINT`, the skip scan keeps track of which set of keys, or ranges of keys, are being searched for in each column.</span></span> <span data-ttu-id="fb817-140">The skip scan then takes a key that was passed to it during filter evaluation, and determines whether it is one of the combinations.</span><span class="sxs-lookup"><span data-stu-id="fb817-140">The skip scan then takes a key that was passed to it during filter evaluation, and determines whether it is one of the combinations.</span></span> <span data-ttu-id="fb817-141">If not, the skip scan evaluates the next highest key to jump to.</span><span class="sxs-lookup"><span data-stu-id="fb817-141">If not, the skip scan evaluates the next highest key to jump to.</span></span>

### <a name="transactions"></a><span data-ttu-id="fb817-142">Transactions</span><span class="sxs-lookup"><span data-stu-id="fb817-142">Transactions</span></span>

<span data-ttu-id="fb817-143">While HBase provides row-level transactions, Phoenix integrates with [Tephra](http://tephra.io/) to add cross-row and cross-table transaction support with full [ACID](https://en.wikipedia.org/wiki/ACID) semantics.</span><span class="sxs-lookup"><span data-stu-id="fb817-143">While HBase provides row-level transactions, Phoenix integrates with [Tephra](http://tephra.io/) to add cross-row and cross-table transaction support with full [ACID](https://en.wikipedia.org/wiki/ACID) semantics.</span></span>

<span data-ttu-id="fb817-144">As with traditional SQL transactions, transactions provided through the Phoenix transaction manager allow you to ensure an atomic unit of data is successfully upserted, rolling back the transaction if the upsert operation fails on any transaction-enabled table.</span><span class="sxs-lookup"><span data-stu-id="fb817-144">As with traditional SQL transactions, transactions provided through the Phoenix transaction manager allow you to ensure an atomic unit of data is successfully upserted, rolling back the transaction if the upsert operation fails on any transaction-enabled table.</span></span>

<span data-ttu-id="fb817-145">To enable Phoenix transactions, see the [Apache Phoenix transaction documentation](http://phoenix.apache.org/transactions.html).</span><span class="sxs-lookup"><span data-stu-id="fb817-145">To enable Phoenix transactions, see the [Apache Phoenix transaction documentation](http://phoenix.apache.org/transactions.html).</span></span>

<span data-ttu-id="fb817-146">To create a new table with transactions enabled, set the `TRANSACTIONAL` property to `true` in a `CREATE` statement:</span><span class="sxs-lookup"><span data-stu-id="fb817-146">To create a new table with transactions enabled, set the `TRANSACTIONAL` property to `true` in a `CREATE` statement:</span></span>

```sql
CREATE TABLE my_table (k BIGINT PRIMARY KEY, v VARCHAR) TRANSACTIONAL=true;
```

<span data-ttu-id="fb817-147">To alter an existing table to be transactional, use the same property in an `ALTER` statement:</span><span class="sxs-lookup"><span data-stu-id="fb817-147">To alter an existing table to be transactional, use the same property in an `ALTER` statement:</span></span>

```sql
ALTER TABLE my_other_table SET TRANSACTIONAL=true;
```

> [!NOTE]
> <span data-ttu-id="fb817-148">You cannot switch a transactional table back to being non-transactional.</span><span class="sxs-lookup"><span data-stu-id="fb817-148">You cannot switch a transactional table back to being non-transactional.</span></span>

### <a name="salted-tables"></a><span data-ttu-id="fb817-149">Salted Tables</span><span class="sxs-lookup"><span data-stu-id="fb817-149">Salted Tables</span></span>

<span data-ttu-id="fb817-150">*Region server hotspotting* can occur  when writing records with sequential keys to HBase.</span><span class="sxs-lookup"><span data-stu-id="fb817-150">*Region server hotspotting* can occur  when writing records with sequential keys to HBase.</span></span> <span data-ttu-id="fb817-151">Though you may have multiple region servers in your cluster, your writes are all occurring on just one.</span><span class="sxs-lookup"><span data-stu-id="fb817-151">Though you may have multiple region servers in your cluster, your writes are all occurring on just one.</span></span> <span data-ttu-id="fb817-152">This concentration creates the hotspotting issue where, instead of your write workload being distributed across all of the available region servers, just one is handling the load.</span><span class="sxs-lookup"><span data-stu-id="fb817-152">This concentration creates the hotspotting issue where, instead of your write workload being distributed across all of the available region servers, just one is handling the load.</span></span> <span data-ttu-id="fb817-153">Since each region has a predefined maximum size, when a region reaches that size limit, it is split into two small regions.</span><span class="sxs-lookup"><span data-stu-id="fb817-153">Since each region has a predefined maximum size, when a region reaches that size limit, it is split into two small regions.</span></span> <span data-ttu-id="fb817-154">When that happens, one of these new regions takes all new records, becoming the new hotspot.</span><span class="sxs-lookup"><span data-stu-id="fb817-154">When that happens, one of these new regions takes all new records, becoming the new hotspot.</span></span>

<span data-ttu-id="fb817-155">To mitigate this problem and achieve better performance,  pre-split tables so  that all of the region servers are equally used.</span><span class="sxs-lookup"><span data-stu-id="fb817-155">To mitigate this problem and achieve better performance,  pre-split tables so  that all of the region servers are equally used.</span></span> <span data-ttu-id="fb817-156">Phoenix provides *salted tables*,  transparently adding the salting byte to the row key for a particular table.</span><span class="sxs-lookup"><span data-stu-id="fb817-156">Phoenix provides *salted tables*,  transparently adding the salting byte to the row key for a particular table.</span></span> <span data-ttu-id="fb817-157">The table is pre-split on the salt byte boundaries to ensure equal load distribution among region servers during the initial phase of the table.</span><span class="sxs-lookup"><span data-stu-id="fb817-157">The table is pre-split on the salt byte boundaries to ensure equal load distribution among region servers during the initial phase of the table.</span></span> <span data-ttu-id="fb817-158">This approach distributes the write workload across all of the available region servers, improving the write and read performance.</span><span class="sxs-lookup"><span data-stu-id="fb817-158">This approach distributes the write workload across all of the available region servers, improving the write and read performance.</span></span> <span data-ttu-id="fb817-159">To salt a table,  specify the `SALT_BUCKETS` table property when the table is created:</span><span class="sxs-lookup"><span data-stu-id="fb817-159">To salt a table,  specify the `SALT_BUCKETS` table property when the table is created:</span></span>

```sql
CREATE TABLE Saltedweblogs (
    transactionid varchar(500) Primary Key,
    transactiondate Date NULL,
    customerid varchar(50) NULL,
    bookid varchar(50) NULL,
    purchasetype varchar(50) NULL,
    orderid varchar(50) NULL,
    bookname varchar(50) NULL,
    categoryname varchar(50) NULL,
    invoicenumber varchar(50) NULL,
    invoicestatus varchar(50) NULL,
    city varchar(50) NULL,
    state varchar(50) NULL,
    paymentamount DOUBLE NULL,
    quantity INTEGER NULL,
    shippingamount DOUBLE NULL) SALT_BUCKETS=4;
```

## <a name="enable-and-tune-phoenix-with-ambari"></a><span data-ttu-id="fb817-160">Enable and tune Phoenix with Ambari</span><span class="sxs-lookup"><span data-stu-id="fb817-160">Enable and tune Phoenix with Ambari</span></span>

<span data-ttu-id="fb817-161">An HDInsight HBase cluster includes the [Ambari UI](hdinsight-hadoop-manage-ambari.md) for making configuration changes.</span><span class="sxs-lookup"><span data-stu-id="fb817-161">An HDInsight HBase cluster includes the [Ambari UI](hdinsight-hadoop-manage-ambari.md) for making configuration changes.</span></span>

1. <span data-ttu-id="fb817-162">To enable or disable Phoenix, and to control Phoenix's query timeout settings, log in to the Ambari Web UI (`https://YOUR_CLUSTER_NAME.azurehdinsight.net`) using your Hadoop user credentials.</span><span class="sxs-lookup"><span data-stu-id="fb817-162">To enable or disable Phoenix, and to control Phoenix's query timeout settings, log in to the Ambari Web UI (`https://YOUR_CLUSTER_NAME.azurehdinsight.net`) using your Hadoop user credentials.</span></span>

2. <span data-ttu-id="fb817-163">Select **HBase** from the list of services in the left-hand menu, then select the **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="fb817-163">Select **HBase** from the list of services in the left-hand menu, then select the **Configs** tab.</span></span>

    ![Ambari HBase config](./media/hdinsight-phoenix-in-hdinsight/ambari-hbase-config.png)

3. <span data-ttu-id="fb817-165">Find the **Phoenix SQL** configuration section to enable or disable phoenix, and set the query timeout.</span><span class="sxs-lookup"><span data-stu-id="fb817-165">Find the **Phoenix SQL** configuration section to enable or disable phoenix, and set the query timeout.</span></span>

    ![Ambari Phoenix SQL configuration section](./media/hdinsight-phoenix-in-hdinsight/ambari-phoenix.png)

## <a name="see-also"></a><span data-ttu-id="fb817-167">See also</span><span class="sxs-lookup"><span data-stu-id="fb817-167">See also</span></span>

* [<span data-ttu-id="fb817-168">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb817-168">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>](hbase/apache-hbase-phoenix-squirrel-linux.md)
