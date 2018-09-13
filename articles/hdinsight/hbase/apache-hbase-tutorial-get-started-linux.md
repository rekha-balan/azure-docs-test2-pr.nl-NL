---
title: Get started with an HBase example on HDInsight - Azure
description: Follow this Apache HBase example to start using hadoop on HDInsight. Create tables from the HBase shell and query them using Hive.
keywords: hbasecommand,hbase example
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 02/22/2018
ms.author: jasonh
ms.openlocfilehash: 0ace6585dc11b49fdbb0654d0c45ca6bc446a42b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871533"
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="eefb9-105">Get started with an Apache HBase example in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eefb9-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="eefb9-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span><span class="sxs-lookup"><span data-stu-id="eefb9-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="eefb9-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="eefb9-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="eefb9-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eefb9-108">Prerequisites</span></span>
<span data-ttu-id="eefb9-109">Before you begin trying this HBase example, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="eefb9-109">Before you begin trying this HBase example, you must have the following items:</span></span>

* <span data-ttu-id="eefb9-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="eefb9-110">**An Azure subscription**.</span></span> <span data-ttu-id="eefb9-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="eefb9-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="eefb9-112">[Secure Shell(SSH)](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="eefb9-112">[Secure Shell(SSH)](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="eefb9-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="eefb9-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="eefb9-114">Create HBase cluster</span><span class="sxs-lookup"><span data-stu-id="eefb9-114">Create HBase cluster</span></span>
<span data-ttu-id="eefb9-115">The following procedure uses an Azure Resource Manager template to create a HBase cluster and the dependent default Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="eefb9-115">The following procedure uses an Azure Resource Manager template to create a HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="eefb9-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="eefb9-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="eefb9-117">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="eefb9-117">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>

1. <span data-ttu-id="eefb9-118">Click the following image to open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eefb9-118">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="eefb9-119">The template is located in [Azure QuickStart templates](https://azure.microsoft.com/resources/templates/).</span><span class="sxs-lookup"><span data-stu-id="eefb9-119">The template is located in [Azure QuickStart templates](https://azure.microsoft.com/resources/templates/).</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/apache-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="eefb9-120">From the **Custom deployment** blade, enter the following values:</span><span class="sxs-lookup"><span data-stu-id="eefb9-120">From the **Custom deployment** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="eefb9-121">**Subscription**: Select your Azure subscription that is used to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="eefb9-121">**Subscription**: Select your Azure subscription that is used to create the cluster.</span></span>
   * <span data-ttu-id="eefb9-122">**Resource group**: Create an Azure Resource management group or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="eefb9-122">**Resource group**: Create an Azure Resource management group or use an existing one.</span></span>
   * <span data-ttu-id="eefb9-123">**Location**: Specify the location of the resource group.</span><span class="sxs-lookup"><span data-stu-id="eefb9-123">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="eefb9-124">**ClusterName**: Enter a name for the HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="eefb9-124">**ClusterName**: Enter a name for the HBase cluster.</span></span>
   * <span data-ttu-id="eefb9-125">**Cluster login name and password**: The default login name is **admin**.</span><span class="sxs-lookup"><span data-stu-id="eefb9-125">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="eefb9-126">**SSH username and password**: The default username is **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="eefb9-126">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="eefb9-127">You can rename it.</span><span class="sxs-lookup"><span data-stu-id="eefb9-127">You can rename it.</span></span>
     
     <span data-ttu-id="eefb9-128">Other parameters are optional.</span><span class="sxs-lookup"><span data-stu-id="eefb9-128">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="eefb9-129">Each cluster has an Azure Storage account dependency.</span><span class="sxs-lookup"><span data-stu-id="eefb9-129">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="eefb9-130">After you delete a cluster, the data retains in the storage account.</span><span class="sxs-lookup"><span data-stu-id="eefb9-130">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="eefb9-131">The cluster default storage account name is the cluster name with "store" appended.</span><span class="sxs-lookup"><span data-stu-id="eefb9-131">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="eefb9-132">It is hardcoded in the template variables section.</span><span class="sxs-lookup"><span data-stu-id="eefb9-132">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="eefb9-133">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="eefb9-133">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="eefb9-134">It takes about 20 minutes to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="eefb9-134">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="eefb9-135">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span><span class="sxs-lookup"><span data-stu-id="eefb9-135">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="eefb9-136">The new cluster picks up the HBase tables you created in the original cluster.</span><span class="sxs-lookup"><span data-stu-id="eefb9-136">The new cluster picks up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="eefb9-137">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="eefb9-137">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="eefb9-138">Create tables and insert data</span><span class="sxs-lookup"><span data-stu-id="eefb9-138">Create tables and insert data</span></span>
<span data-ttu-id="eefb9-139">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span><span class="sxs-lookup"><span data-stu-id="eefb9-139">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span></span> <span data-ttu-id="eefb9-140">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="eefb9-140">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="eefb9-141">For most people, data appears in the tabular format:</span><span class="sxs-lookup"><span data-stu-id="eefb9-141">For most people, data appears in the tabular format:</span></span>

![HDInsight HBase tabular data][img-hbase-sample-data-tabular]

<span data-ttu-id="eefb9-143">In HBase (an implementation of BigTable), the same data looks like:</span><span class="sxs-lookup"><span data-stu-id="eefb9-143">In HBase (an implementation of BigTable), the same data looks like:</span></span>

![HDInsight HBase BigTable data][img-hbase-sample-data-bigtable]


<span data-ttu-id="eefb9-145">**To use the HBase shell**</span><span class="sxs-lookup"><span data-stu-id="eefb9-145">**To use the HBase shell**</span></span>

1. <span data-ttu-id="eefb9-146">From SSH, run the following HBase command:</span><span class="sxs-lookup"><span data-stu-id="eefb9-146">From SSH, run the following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="eefb9-147">Create an HBase with two-column families:</span><span class="sxs-lookup"><span data-stu-id="eefb9-147">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="eefb9-148">Insert some data:</span><span class="sxs-lookup"><span data-stu-id="eefb9-148">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase shell][img-hbase-shell]
4. <span data-ttu-id="eefb9-150">Get a single row</span><span class="sxs-lookup"><span data-stu-id="eefb9-150">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="eefb9-151">You shall see the same results as using the scan command because there is only one row.</span><span class="sxs-lookup"><span data-stu-id="eefb9-151">You shall see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="eefb9-152">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="eefb9-152">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="eefb9-153">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="eefb9-153">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="eefb9-154">Exit the shell</span><span class="sxs-lookup"><span data-stu-id="eefb9-154">Exit the shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="eefb9-155">**To bulk load data into the contacts HBase table**</span><span class="sxs-lookup"><span data-stu-id="eefb9-155">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="eefb9-156">HBase includes several methods of loading data into tables.</span><span class="sxs-lookup"><span data-stu-id="eefb9-156">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="eefb9-157">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="eefb9-157">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="eefb9-158">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="eefb9-158">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="eefb9-159">The content of the data file is:</span><span class="sxs-lookup"><span data-stu-id="eefb9-159">The content of the data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="eefb9-160">You can optionally create a text file and upload the file to your own storage account.</span><span class="sxs-lookup"><span data-stu-id="eefb9-160">You can optionally create a text file and upload the file to your own storage account.</span></span> <span data-ttu-id="eefb9-161">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="eefb9-161">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="eefb9-162">This procedure uses the Contacts HBase table you have created in the last procedure.</span><span class="sxs-lookup"><span data-stu-id="eefb9-162">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 

1. <span data-ttu-id="eefb9-163">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="eefb9-163">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="eefb9-164">If you are in HBase Shell, use the exit command to exit.</span><span class="sxs-lookup"><span data-stu-id="eefb9-164">If you are in HBase Shell, use the exit command to exit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="eefb9-165">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span><span class="sxs-lookup"><span data-stu-id="eefb9-165">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="eefb9-166">You can open the HBase shell, and use the scan command to list the table content.</span><span class="sxs-lookup"><span data-stu-id="eefb9-166">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="eefb9-167">Use Hive to query HBase</span><span class="sxs-lookup"><span data-stu-id="eefb9-167">Use Hive to query HBase</span></span>

<span data-ttu-id="eefb9-168">You can query data in HBase tables by using Hive.</span><span class="sxs-lookup"><span data-stu-id="eefb9-168">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="eefb9-169">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span><span class="sxs-lookup"><span data-stu-id="eefb9-169">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

1. <span data-ttu-id="eefb9-170">Open **PuTTY**, and connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="eefb9-170">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="eefb9-171">See the instructions in the previous procedure.</span><span class="sxs-lookup"><span data-stu-id="eefb9-171">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="eefb9-172">From the SSH session, use the following command to start Beeline:</span><span class="sxs-lookup"><span data-stu-id="eefb9-172">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="eefb9-173">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](../hadoop/apache-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="eefb9-173">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](../hadoop/apache-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="eefb9-174">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span><span class="sxs-lookup"><span data-stu-id="eefb9-174">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="eefb9-175">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span><span class="sxs-lookup"><span data-stu-id="eefb9-175">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="eefb9-176">Run the following HiveQL script to query the data in the HBase table:</span><span class="sxs-lookup"><span data-stu-id="eefb9-176">Run the following HiveQL script to query the data in the HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="eefb9-177">Use HBase REST APIs using Curl</span><span class="sxs-lookup"><span data-stu-id="eefb9-177">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="eefb9-178">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="eefb9-178">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="eefb9-179">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="eefb9-179">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

2. <span data-ttu-id="eefb9-180">Use the following command to list the existing HBase tables:</span><span class="sxs-lookup"><span data-stu-id="eefb9-180">Use the following command to list the existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="eefb9-181">Use the following command to create a new HBase table with two-column families:</span><span class="sxs-lookup"><span data-stu-id="eefb9-181">Use the following command to create a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="eefb9-182">The schema is provided in the JSon format.</span><span class="sxs-lookup"><span data-stu-id="eefb9-182">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="eefb9-183">Use the following command to insert some data:</span><span class="sxs-lookup"><span data-stu-id="eefb9-183">Use the following command to insert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="eefb9-184">You must base64 encode the values specified in the -d switch.</span><span class="sxs-lookup"><span data-stu-id="eefb9-184">You must base64 encode the values specified in the -d switch.</span></span> <span data-ttu-id="eefb9-185">In the example:</span><span class="sxs-lookup"><span data-stu-id="eefb9-185">In the example:</span></span>
   
   * <span data-ttu-id="eefb9-186">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="eefb9-186">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="eefb9-187">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="eefb9-187">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="eefb9-188">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="eefb9-188">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="eefb9-189">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span><span class="sxs-lookup"><span data-stu-id="eefb9-189">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span></span>
5. <span data-ttu-id="eefb9-190">Use the following command to get a row:</span><span class="sxs-lookup"><span data-stu-id="eefb9-190">Use the following command to get a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="eefb9-191">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="eefb9-191">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="eefb9-192">Thrift is not supported by HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eefb9-192">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="eefb9-193">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="eefb9-193">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="eefb9-194">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span><span class="sxs-lookup"><span data-stu-id="eefb9-194">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="eefb9-195">You should receive a response similar to the following response:</span><span class="sxs-lookup"><span data-stu-id="eefb9-195">You should receive a response similar to the following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="eefb9-196">Check cluster status</span><span class="sxs-lookup"><span data-stu-id="eefb9-196">Check cluster status</span></span>
<span data-ttu-id="eefb9-197">HBase in HDInsight ships with a Web UI for monitoring clusters.</span><span class="sxs-lookup"><span data-stu-id="eefb9-197">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="eefb9-198">Using the Web UI, you can request statistics or information about regions.</span><span class="sxs-lookup"><span data-stu-id="eefb9-198">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="eefb9-199">**To access the HBase Master UI**</span><span class="sxs-lookup"><span data-stu-id="eefb9-199">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="eefb9-200">Sign into the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="eefb9-200">Sign into the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="eefb9-201">Click **HBase** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="eefb9-201">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="eefb9-202">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span><span class="sxs-lookup"><span data-stu-id="eefb9-202">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="eefb9-203">The UI is opened in another browser tab:</span><span class="sxs-lookup"><span data-stu-id="eefb9-203">The UI is opened in another browser tab:</span></span>

  ![HDInsight HBase HMaster UI](./media/apache-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="eefb9-205">The HBase Master UI contains the following sections:</span><span class="sxs-lookup"><span data-stu-id="eefb9-205">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="eefb9-206">region servers</span><span class="sxs-lookup"><span data-stu-id="eefb9-206">region servers</span></span>
  - <span data-ttu-id="eefb9-207">backup masters</span><span class="sxs-lookup"><span data-stu-id="eefb9-207">backup masters</span></span>
  - <span data-ttu-id="eefb9-208">tables</span><span class="sxs-lookup"><span data-stu-id="eefb9-208">tables</span></span>
  - <span data-ttu-id="eefb9-209">tasks</span><span class="sxs-lookup"><span data-stu-id="eefb9-209">tasks</span></span>
  - <span data-ttu-id="eefb9-210">software attributes</span><span class="sxs-lookup"><span data-stu-id="eefb9-210">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="eefb9-211">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="eefb9-211">Delete the cluster</span></span>
<span data-ttu-id="eefb9-212">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="eefb9-212">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="eefb9-213">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="eefb9-213">Troubleshoot</span></span>

<span data-ttu-id="eefb9-214">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="eefb9-214">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eefb9-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="eefb9-215">Next steps</span></span>
<span data-ttu-id="eefb9-216">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span><span class="sxs-lookup"><span data-stu-id="eefb9-216">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="eefb9-217">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span><span class="sxs-lookup"><span data-stu-id="eefb9-217">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="eefb9-218">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="eefb9-218">To learn more, see:</span></span>

* <span data-ttu-id="eefb9-219">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span><span class="sxs-lookup"><span data-stu-id="eefb9-219">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: ../hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]:apache-hbase-overview.md
[hdinsight-hbase-provision-vnet]:apache-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hbase-shell]: ./media/apache-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/apache-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/apache-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
