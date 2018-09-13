---
title: Use Spark to read and write HBase data - Azure HDInsight
description: Use the Spark HBase Connector to read and write data from a Spark cluster to an HBase cluster.
services: hdinsight
author: maxluk
ms.author: maxluk
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 07/18/2018
ms.openlocfilehash: 6f957e5841bbc75756fc42d9496bbc1057cd478e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966949"
---
# <a name="use-spark-to-read-and-write-hbase-data"></a><span data-ttu-id="d9cab-103">Use Spark to read and write HBase data</span><span class="sxs-lookup"><span data-stu-id="d9cab-103">Use Spark to read and write HBase data</span></span>

<span data-ttu-id="d9cab-104">Apache HBase is typically queried either with its low-level API (scans, gets, and puts) or with a SQL syntax using Phoenix.</span><span class="sxs-lookup"><span data-stu-id="d9cab-104">Apache HBase is typically queried either with its low-level API (scans, gets, and puts) or with a SQL syntax using Phoenix.</span></span> <span data-ttu-id="d9cab-105">Apache also provides the Spark HBase Connector, which is a convenient and performant alternative to query and modify data stored by HBase.</span><span class="sxs-lookup"><span data-stu-id="d9cab-105">Apache also provides the Spark HBase Connector, which is a convenient and performant alternative to query and modify data stored by HBase.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9cab-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d9cab-106">Prerequisites</span></span>

* <span data-ttu-id="d9cab-107">Two separate HDInsight clusters, one HBase, and one Spark with Spark 2.1 (HDInsight 3.6) installed.</span><span class="sxs-lookup"><span data-stu-id="d9cab-107">Two separate HDInsight clusters, one HBase, and one Spark with Spark 2.1 (HDInsight 3.6) installed.</span></span>
* <span data-ttu-id="d9cab-108">The Spark cluster needs to communicate directly with the HBase cluster with minimal latency, so the recommended configuration is deploying both clusters in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="d9cab-108">The Spark cluster needs to communicate directly with the HBase cluster with minimal latency, so the recommended configuration is deploying both clusters in the same virtual network.</span></span> <span data-ttu-id="d9cab-109">For more information, see [Create Linux-based clusters in HDInsight using the Azure portal](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d9cab-109">For more information, see [Create Linux-based clusters in HDInsight using the Azure portal](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>
* <span data-ttu-id="d9cab-110">SSH access to each cluster.</span><span class="sxs-lookup"><span data-stu-id="d9cab-110">SSH access to each cluster.</span></span>
* <span data-ttu-id="d9cab-111">Access to each cluster's default storage.</span><span class="sxs-lookup"><span data-stu-id="d9cab-111">Access to each cluster's default storage.</span></span>

## <a name="overall-process"></a><span data-ttu-id="d9cab-112">Overall process</span><span class="sxs-lookup"><span data-stu-id="d9cab-112">Overall process</span></span>

<span data-ttu-id="d9cab-113">The high-level process for enabling your Spark cluster to query your HDInsight cluster is as follows:</span><span class="sxs-lookup"><span data-stu-id="d9cab-113">The high-level process for enabling your Spark cluster to query your HDInsight cluster is as follows:</span></span>

1. <span data-ttu-id="d9cab-114">Prepare some sample data in HBase.</span><span class="sxs-lookup"><span data-stu-id="d9cab-114">Prepare some sample data in HBase.</span></span>
2. <span data-ttu-id="d9cab-115">Acquire the hbase-site.xml file from your HBase cluster configuration folder (/etc/hbase/conf).</span><span class="sxs-lookup"><span data-stu-id="d9cab-115">Acquire the hbase-site.xml file from your HBase cluster configuration folder (/etc/hbase/conf).</span></span>
3. <span data-ttu-id="d9cab-116">Place a copy of hbase-site.xml in your Spark 2 configuration folder (/etc/spark2/conf).</span><span class="sxs-lookup"><span data-stu-id="d9cab-116">Place a copy of hbase-site.xml in your Spark 2 configuration folder (/etc/spark2/conf).</span></span>
4. <span data-ttu-id="d9cab-117">Run `spark-shell` referencing the Spark HBase Connector by its Maven coordinates in the `packages` option.</span><span class="sxs-lookup"><span data-stu-id="d9cab-117">Run `spark-shell` referencing the Spark HBase Connector by its Maven coordinates in the `packages` option.</span></span>
5. <span data-ttu-id="d9cab-118">Define a catalog that maps the schema from Spark to HBase.</span><span class="sxs-lookup"><span data-stu-id="d9cab-118">Define a catalog that maps the schema from Spark to HBase.</span></span>
6. <span data-ttu-id="d9cab-119">Interact with the HBase data using either the RDD or DataFrame APIs.</span><span class="sxs-lookup"><span data-stu-id="d9cab-119">Interact with the HBase data using either the RDD or DataFrame APIs.</span></span>

## <a name="prepare-sample-data-in-hbase"></a><span data-ttu-id="d9cab-120">Prepare sample data in HBase</span><span class="sxs-lookup"><span data-stu-id="d9cab-120">Prepare sample data in HBase</span></span>

<span data-ttu-id="d9cab-121">In this step, you create and populate a simple table in HBase that you can then query using Spark.</span><span class="sxs-lookup"><span data-stu-id="d9cab-121">In this step, you create and populate a simple table in HBase that you can then query using Spark.</span></span>

1. <span data-ttu-id="d9cab-122">Connect to the head node of your HBase cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="d9cab-122">Connect to the head node of your HBase cluster using SSH.</span></span> <span data-ttu-id="d9cab-123">For more information, see [Connect to HDInsight using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9cab-123">For more information, see [Connect to HDInsight using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="d9cab-124">Run the HBase shell:</span><span class="sxs-lookup"><span data-stu-id="d9cab-124">Run the HBase shell:</span></span>

        hbase shell

3. <span data-ttu-id="d9cab-125">Create a `Contacts` table with the column families `Personal` and `Office`:</span><span class="sxs-lookup"><span data-stu-id="d9cab-125">Create a `Contacts` table with the column families `Personal` and `Office`:</span></span>

        create 'Contacts', 'Personal', 'Office'

4. <span data-ttu-id="d9cab-126">Load a few sample rows of data:</span><span class="sxs-lookup"><span data-stu-id="d9cab-126">Load a few sample rows of data:</span></span>

        put 'Contacts', '1000', 'Personal:Name', 'John Dole'
        put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
        put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
        put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
        put 'Contacts', '8396', 'Personal:Name', 'Calvin Raji'
        put 'Contacts', '8396', 'Personal:Phone', '230-555-0191'
        put 'Contacts', '8396', 'Office:Phone', '230-555-0191'
        put 'Contacts', '8396', 'Office:Address', '5415 San Gabriel Dr.'

## <a name="acquire-hbase-sitexml-from-your-hbase-cluster"></a><span data-ttu-id="d9cab-127">Acquire hbase-site.xml from your HBase cluster</span><span class="sxs-lookup"><span data-stu-id="d9cab-127">Acquire hbase-site.xml from your HBase cluster</span></span>

1. <span data-ttu-id="d9cab-128">Connect to the head node of your HBase cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="d9cab-128">Connect to the head node of your HBase cluster using SSH.</span></span>
2. <span data-ttu-id="d9cab-129">Copy the hbase-site.xml from local storage to the root of your HBase cluster's default storage:</span><span class="sxs-lookup"><span data-stu-id="d9cab-129">Copy the hbase-site.xml from local storage to the root of your HBase cluster's default storage:</span></span>

        hdfs dfs -copyFromLocal /etc/hbase/conf/hbase-site.xml /

3. <span data-ttu-id="d9cab-130">Navigate to your HBase cluster using the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9cab-130">Navigate to your HBase cluster using the [Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="d9cab-131">Select Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="d9cab-131">Select Storage accounts.</span></span> 

    ![Storage accounts](./media/hdinsight-using-spark-query-hbase/storage-accounts.png)

5. <span data-ttu-id="d9cab-133">Select the Storage account in the list that has a checkmark under the Default column.</span><span class="sxs-lookup"><span data-stu-id="d9cab-133">Select the Storage account in the list that has a checkmark under the Default column.</span></span>

    ![Default storage account](./media/hdinsight-using-spark-query-hbase/default-storage.png)

6. <span data-ttu-id="d9cab-135">On the Storage account pane, select the Blobs tile.</span><span class="sxs-lookup"><span data-stu-id="d9cab-135">On the Storage account pane, select the Blobs tile.</span></span>

    ![Blobs tile](./media/hdinsight-using-spark-query-hbase/blobs-tile.png)

7. <span data-ttu-id="d9cab-137">In the list of containers, select the container that is used by your HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="d9cab-137">In the list of containers, select the container that is used by your HBase cluster.</span></span>
8. <span data-ttu-id="d9cab-138">In the file list, select `hbase-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="d9cab-138">In the file list, select `hbase-site.xml`.</span></span>

    ![HBase-site.xml](./media/hdinsight-using-spark-query-hbase/hbase-site-xml.png)

9. <span data-ttu-id="d9cab-140">On the Blob properties panel, select Download and save `hbase-site.xml` to a location on your local machine.</span><span class="sxs-lookup"><span data-stu-id="d9cab-140">On the Blob properties panel, select Download and save `hbase-site.xml` to a location on your local machine.</span></span>

    ![Download](./media/hdinsight-using-spark-query-hbase/download.png)

## <a name="put-hbase-sitexml-on-your-spark-cluster"></a><span data-ttu-id="d9cab-142">Put hbase-site.xml on your Spark cluster</span><span class="sxs-lookup"><span data-stu-id="d9cab-142">Put hbase-site.xml on your Spark cluster</span></span>

1. <span data-ttu-id="d9cab-143">Navigate to your Spark cluster using the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9cab-143">Navigate to your Spark cluster using the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d9cab-144">Select Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="d9cab-144">Select Storage accounts.</span></span>

    ![Storage accounts](./media/hdinsight-using-spark-query-hbase/storage-accounts.png)

3. <span data-ttu-id="d9cab-146">Select the Storage account in the list that has a checkmark under the Default column.</span><span class="sxs-lookup"><span data-stu-id="d9cab-146">Select the Storage account in the list that has a checkmark under the Default column.</span></span>

    ![Default storage account](./media/hdinsight-using-spark-query-hbase/default-storage.png)

4. <span data-ttu-id="d9cab-148">On the Storage account pane, select the Blobs tile.</span><span class="sxs-lookup"><span data-stu-id="d9cab-148">On the Storage account pane, select the Blobs tile.</span></span>

    ![Blobs tile](./media/hdinsight-using-spark-query-hbase/blobs-tile.png)

5. <span data-ttu-id="d9cab-150">In the list of containers, select the container that is used by your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="d9cab-150">In the list of containers, select the container that is used by your Spark cluster.</span></span>
6. <span data-ttu-id="d9cab-151">Select upload.</span><span class="sxs-lookup"><span data-stu-id="d9cab-151">Select upload.</span></span>

    ![Upload](./media/hdinsight-using-spark-query-hbase/upload.png)

7. <span data-ttu-id="d9cab-153">Select the `hbase-site.xml` file you previously downloaded to your local machine.</span><span class="sxs-lookup"><span data-stu-id="d9cab-153">Select the `hbase-site.xml` file you previously downloaded to your local machine.</span></span>

    ![Upload hbase-site.xml](./media/hdinsight-using-spark-query-hbase/upload-selection.png)

8. <span data-ttu-id="d9cab-155">Select Upload.</span><span class="sxs-lookup"><span data-stu-id="d9cab-155">Select Upload.</span></span>
9. <span data-ttu-id="d9cab-156">Connect to the head node of your Spark cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="d9cab-156">Connect to the head node of your Spark cluster using SSH.</span></span>
10. <span data-ttu-id="d9cab-157">Copy `hbase-site.xml` from your Spark cluster's default storage to the Spark 2 configuration folder on the cluster's local storage:</span><span class="sxs-lookup"><span data-stu-id="d9cab-157">Copy `hbase-site.xml` from your Spark cluster's default storage to the Spark 2 configuration folder on the cluster's local storage:</span></span>

        sudo hdfs dfs -copyToLocal /hbase-site.xml /etc/spark2/conf

## <a name="run-spark-shell-referencing-the-spark-hbase-connector"></a><span data-ttu-id="d9cab-158">Run Spark Shell referencing the Spark HBase Connector</span><span class="sxs-lookup"><span data-stu-id="d9cab-158">Run Spark Shell referencing the Spark HBase Connector</span></span>

1. <span data-ttu-id="d9cab-159">Connect to the head node of your Spark cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="d9cab-159">Connect to the head node of your Spark cluster using SSH.</span></span>
2. <span data-ttu-id="d9cab-160">Start the spark shell, specifying the Spark HBase Connector package:</span><span class="sxs-lookup"><span data-stu-id="d9cab-160">Start the spark shell, specifying the Spark HBase Connector package:</span></span>

        spark-shell --packages com.hortonworks:shc-core:1.1.0-2.1-s_2.11 --repositories http://repo.hortonworks.com/content/groups/public/

3. <span data-ttu-id="d9cab-161">Keep this Spark Shell instance open and continue to the next step.</span><span class="sxs-lookup"><span data-stu-id="d9cab-161">Keep this Spark Shell instance open and continue to the next step.</span></span>

## <a name="define-a-catalog-and-query"></a><span data-ttu-id="d9cab-162">Define a Catalog and Query</span><span class="sxs-lookup"><span data-stu-id="d9cab-162">Define a Catalog and Query</span></span>

<span data-ttu-id="d9cab-163">In this step, you define a catalog object that maps the schema from Spark to HBase.</span><span class="sxs-lookup"><span data-stu-id="d9cab-163">In this step, you define a catalog object that maps the schema from Spark to HBase.</span></span> 

1. <span data-ttu-id="d9cab-164">In your open Spark Shell, run the following `import` statements:</span><span class="sxs-lookup"><span data-stu-id="d9cab-164">In your open Spark Shell, run the following `import` statements:</span></span>

        import org.apache.spark.sql.{SQLContext, _}
        import org.apache.spark.sql.execution.datasources.hbase._
        import org.apache.spark.{SparkConf, SparkContext}
        import spark.sqlContext.implicits._

2. <span data-ttu-id="d9cab-165">Define a catalog for the Contacts table you created in HBase:</span><span class="sxs-lookup"><span data-stu-id="d9cab-165">Define a catalog for the Contacts table you created in HBase:</span></span>
    1. <span data-ttu-id="d9cab-166">Define a catalog schema for the HBase table named `Contacts`.</span><span class="sxs-lookup"><span data-stu-id="d9cab-166">Define a catalog schema for the HBase table named `Contacts`.</span></span>
    2. <span data-ttu-id="d9cab-167">Identify the rowkey as `key`, and map the column names used in Spark to the column family, column name, and column type as used in HBase.</span><span class="sxs-lookup"><span data-stu-id="d9cab-167">Identify the rowkey as `key`, and map the column names used in Spark to the column family, column name, and column type as used in HBase.</span></span>
    3. <span data-ttu-id="d9cab-168">The rowkey also has to be defined in detail as a named column (`rowkey`), which has a specific column family `cf` of `rowkey`.</span><span class="sxs-lookup"><span data-stu-id="d9cab-168">The rowkey also has to be defined in detail as a named column (`rowkey`), which has a specific column family `cf` of `rowkey`.</span></span>

            def catalog = s"""{
                |"table":{"namespace":"default", "name":"Contacts"},
                |"rowkey":"key",
                |"columns":{
                |"rowkey":{"cf":"rowkey", "col":"key", "type":"string"},
                |"officeAddress":{"cf":"Office", "col":"Address", "type":"string"},
                |"officePhone":{"cf":"Office", "col":"Phone", "type":"string"},
                |"personalName":{"cf":"Personal", "col":"Name", "type":"string"},
                |"personalPhone":{"cf":"Personal", "col":"Phone", "type":"string"}
                |}
            |}""".stripMargin

3. <span data-ttu-id="d9cab-169">Define a method that provides a DataFrame around your `Contacts` table in HBase:</span><span class="sxs-lookup"><span data-stu-id="d9cab-169">Define a method that provides a DataFrame around your `Contacts` table in HBase:</span></span>

            def withCatalog(cat: String): DataFrame = {
                spark.sqlContext
                .read
                .options(Map(HBaseTableCatalog.tableCatalog->cat))
                .format("org.apache.spark.sql.execution.datasources.hbase")
                .load()
            }

4. <span data-ttu-id="d9cab-170">Create an instance of the DataFrame:</span><span class="sxs-lookup"><span data-stu-id="d9cab-170">Create an instance of the DataFrame:</span></span>

        val df = withCatalog(catalog)

5. <span data-ttu-id="d9cab-171">Query the DataFrame:</span><span class="sxs-lookup"><span data-stu-id="d9cab-171">Query the DataFrame:</span></span>

        df.show()

6. <span data-ttu-id="d9cab-172">You should see two rows of data:</span><span class="sxs-lookup"><span data-stu-id="d9cab-172">You should see two rows of data:</span></span>

        +------+--------------------+--------------+-------------+--------------+
        |rowkey|       officeAddress|   officePhone| personalName| personalPhone|
        +------+--------------------+--------------+-------------+--------------+
        |  1000|1111 San Gabriel Dr.|1-425-000-0002|    John Dole|1-425-000-0001|
        |  8396|5415 San Gabriel Dr.|  230-555-0191|  Calvin Raji|  230-555-0191|
        +------+--------------------+--------------+-------------+--------------+

7. <span data-ttu-id="d9cab-173">Register a temporary table so you can query the HBase table using Spark SQL:</span><span class="sxs-lookup"><span data-stu-id="d9cab-173">Register a temporary table so you can query the HBase table using Spark SQL:</span></span>

        df.registerTempTable("contacts")

8. <span data-ttu-id="d9cab-174">Issue a SQL query against the `contacts` table:</span><span class="sxs-lookup"><span data-stu-id="d9cab-174">Issue a SQL query against the `contacts` table:</span></span>

        val query = spark.sqlContext.sql("select personalName, officeAddress from contacts")
        query.show()

9. <span data-ttu-id="d9cab-175">You should see results like these:</span><span class="sxs-lookup"><span data-stu-id="d9cab-175">You should see results like these:</span></span>

        +-------------+--------------------+
        | personalName|       officeAddress|
        +-------------+--------------------+
        |    John Dole|1111 San Gabriel Dr.|
        |  Calvin Raji|5415 San Gabriel Dr.|
        +-------------+--------------------+

## <a name="insert-new-data"></a><span data-ttu-id="d9cab-176">Insert new data</span><span class="sxs-lookup"><span data-stu-id="d9cab-176">Insert new data</span></span>

1. <span data-ttu-id="d9cab-177">To insert a new Contact record, define a `ContactRecord` class:</span><span class="sxs-lookup"><span data-stu-id="d9cab-177">To insert a new Contact record, define a `ContactRecord` class:</span></span>

        case class ContactRecord(
            rowkey: String,
            officeAddress: String,
            officePhone: String,
            personalName: String,
            personalPhone: String
            )

2. <span data-ttu-id="d9cab-178">Create an instance of `ContactRecord` and put it in an array:</span><span class="sxs-lookup"><span data-stu-id="d9cab-178">Create an instance of `ContactRecord` and put it in an array:</span></span>

        val newContact = ContactRecord("16891", "40 Ellis St.", "674-555-0110", "John Jackson","230-555-0194")

        var newData = new Array[ContactRecord](1)
        newData(0) = newContact

3. <span data-ttu-id="d9cab-179">Save the array of new data to HBase:</span><span class="sxs-lookup"><span data-stu-id="d9cab-179">Save the array of new data to HBase:</span></span>

        sc.parallelize(newData).toDF.write
        .options(Map(HBaseTableCatalog.tableCatalog -> catalog))
        .format("org.apache.spark.sql.execution.datasources.hbase").save()

4. <span data-ttu-id="d9cab-180">Examine the results:</span><span class="sxs-lookup"><span data-stu-id="d9cab-180">Examine the results:</span></span>
    
        df.show()

5. <span data-ttu-id="d9cab-181">You should see output like this:</span><span class="sxs-lookup"><span data-stu-id="d9cab-181">You should see output like this:</span></span>

        +------+--------------------+--------------+------------+--------------+
        |rowkey|       officeAddress|   officePhone|personalName| personalPhone|
        +------+--------------------+--------------+------------+--------------+
        |  1000|1111 San Gabriel Dr.|1-425-000-0002|   John Dole|1-425-000-0001|
        | 16891|        40 Ellis St.|  674-555-0110|John Jackson|  230-555-0194|
        |  8396|5415 San Gabriel Dr.|  230-555-0191| Calvin Raji|  230-555-0191|
        +------+--------------------+--------------+------------+--------------+

## <a name="next-steps"></a><span data-ttu-id="d9cab-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="d9cab-182">Next steps</span></span>

* [<span data-ttu-id="d9cab-183">Spark HBase Connector</span><span class="sxs-lookup"><span data-stu-id="d9cab-183">Spark HBase Connector</span></span>](https://github.com/hortonworks-spark/shc)
