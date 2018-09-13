---
title: Get started with HBase on Azure HDInsight | Microsoft Docs
description: Follow this HBase tutorial to get started using Apache HBase with Hadoop in HDInsight. Create tables from the HBase shell and query them using Hive.
keywords: apache hbase,hbase,hbase shell,hbase tutorial
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/22/2017
ms.author: jgao
ms.openlocfilehash: 7aabf92898b44443bed43f0205000da4f948018a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564293"
---
# <a name="hbase-tutorial-get-started-using-apache-hbase-in-hdinsight"></a><span data-ttu-id="154e5-105">HBase tutorial: Get started using Apache HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="154e5-105">HBase tutorial: Get started using Apache HBase in HDInsight</span></span>

<span data-ttu-id="154e5-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span><span class="sxs-lookup"><span data-stu-id="154e5-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="154e5-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="154e5-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="154e5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="154e5-108">Prerequisites</span></span>
<span data-ttu-id="154e5-109">Before you begin this HBase tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="154e5-109">Before you begin this HBase tutorial, you must have the following:</span></span>

* <span data-ttu-id="154e5-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="154e5-110">**An Azure subscription**.</span></span> <span data-ttu-id="154e5-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="154e5-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="154e5-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="154e5-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="154e5-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="154e5-113">[curl](http://curl.haxx.se/download.html).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="154e5-114">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="154e5-114">Access control requirements</span></span>
[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="create-hbase-cluster"></a><span data-ttu-id="154e5-115">Create HBase cluster</span><span class="sxs-lookup"><span data-stu-id="154e5-115">Create HBase cluster</span></span>
<span data-ttu-id="154e5-116">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="154e5-116">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="154e5-117">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="154e5-117">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="154e5-118">Click the following image to open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="154e5-118">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="154e5-119">The template is located in a public blob container.</span><span class="sxs-lookup"><span data-stu-id="154e5-119">The template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-cluster-in-hdinsight.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="154e5-120">From the **Custom deployment** blade, enter the following:</span><span class="sxs-lookup"><span data-stu-id="154e5-120">From the **Custom deployment** blade, enter the following:</span></span>
   
   * <span data-ttu-id="154e5-121">**Subscription**: Select your Azure subscription that will be used to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="154e5-121">**Subscription**: Select your Azure subscription that will be used to create the cluster.</span></span>
   * <span data-ttu-id="154e5-122">**Resource group**: Create a new Azure Resource Management group or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="154e5-122">**Resource group**: Create a new Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="154e5-123">**Location**: Specify the location of the resource group.</span><span class="sxs-lookup"><span data-stu-id="154e5-123">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="154e5-124">**ClusterName**: Enter a name for the HBase cluster that you will create.</span><span class="sxs-lookup"><span data-stu-id="154e5-124">**ClusterName**: Enter a name for the HBase cluster that you will create.</span></span>
   * <span data-ttu-id="154e5-125">**Cluster login name and password**: The default login name is **admin**.</span><span class="sxs-lookup"><span data-stu-id="154e5-125">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="154e5-126">**SSH username and password**: The default username is **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="154e5-126">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="154e5-127">You can rename it.</span><span class="sxs-lookup"><span data-stu-id="154e5-127">You can rename it.</span></span>
     
     <span data-ttu-id="154e5-128">Other parameters are optional.</span><span class="sxs-lookup"><span data-stu-id="154e5-128">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="154e5-129">Each cluster has an Azure Storage account dependency.</span><span class="sxs-lookup"><span data-stu-id="154e5-129">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="154e5-130">After you delete a cluster, the data retains in the storage account.</span><span class="sxs-lookup"><span data-stu-id="154e5-130">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="154e5-131">The cluster default storage account name is the cluster name with "store" appended.</span><span class="sxs-lookup"><span data-stu-id="154e5-131">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="154e5-132">It is hardcoded in the template variables section.</span><span class="sxs-lookup"><span data-stu-id="154e5-132">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="154e5-133">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="154e5-133">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="154e5-134">It takes about 20 minutes to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="154e5-134">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="154e5-135">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span><span class="sxs-lookup"><span data-stu-id="154e5-135">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="154e5-136">The new cluster will pick up the HBase tables you created in the original cluster.</span><span class="sxs-lookup"><span data-stu-id="154e5-136">The new cluster will pick up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="154e5-137">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="154e5-137">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="154e5-138">Create tables and insert data</span><span class="sxs-lookup"><span data-stu-id="154e5-138">Create tables and insert data</span></span>
<span data-ttu-id="154e5-139">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data and query data.</span><span class="sxs-lookup"><span data-stu-id="154e5-139">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data and query data.</span></span> <span data-ttu-id="154e5-140">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="154e5-140">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="154e5-141">For most people, data appears in the tabular format:</span><span class="sxs-lookup"><span data-stu-id="154e5-141">For most people, data appears in the tabular format:</span></span>

![HDInsight HBase tabular data][img-hbase-sample-data-tabular]

<span data-ttu-id="154e5-143">In HBase which is an implementation of BigTable, the same data looks like:</span><span class="sxs-lookup"><span data-stu-id="154e5-143">In HBase which is an implementation of BigTable, the same data looks like:</span></span>

![HDInsight HBase BigTable data][img-hbase-sample-data-bigtable]

<span data-ttu-id="154e5-145">It will make more sense after you finish the next procedure.</span><span class="sxs-lookup"><span data-stu-id="154e5-145">It will make more sense after you finish the next procedure.</span></span>  

<span data-ttu-id="154e5-146">**To use the HBase shell**</span><span class="sxs-lookup"><span data-stu-id="154e5-146">**To use the HBase shell**</span></span>

1. <span data-ttu-id="154e5-147">From SSH, run the following command:</span><span class="sxs-lookup"><span data-stu-id="154e5-147">From SSH, run the following command:</span></span>
   
        hbase shell
2. <span data-ttu-id="154e5-148">Create an HBase with two-column families:</span><span class="sxs-lookup"><span data-stu-id="154e5-148">Create an HBase with two-column families:</span></span>
   
        create 'Contacts', 'Personal', 'Office'
        list
3. <span data-ttu-id="154e5-149">Insert some data:</span><span class="sxs-lookup"><span data-stu-id="154e5-149">Insert some data:</span></span>
   
        put 'Contacts', '1000', 'Personal:Name', 'John Dole'
        put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
        put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
        put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
        scan 'Contacts'
   
    ![HDInsight Hadoop HBase shell][img-hbase-shell]
4. <span data-ttu-id="154e5-151">Get a single row</span><span class="sxs-lookup"><span data-stu-id="154e5-151">Get a single row</span></span>
   
        get 'Contacts', '1000'
   
    <span data-ttu-id="154e5-152">You will see the same results as using the scan command because there is only one row.</span><span class="sxs-lookup"><span data-stu-id="154e5-152">You will see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="154e5-153">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="154e5-153">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="154e5-154">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="154e5-154">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="154e5-155">Exit the shell</span><span class="sxs-lookup"><span data-stu-id="154e5-155">Exit the shell</span></span>
   
        exit

<span data-ttu-id="154e5-156">**To bulk load data into the contacts HBase table**</span><span class="sxs-lookup"><span data-stu-id="154e5-156">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="154e5-157">HBase includes several methods of loading data into tables.</span><span class="sxs-lookup"><span data-stu-id="154e5-157">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="154e5-158">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="154e5-158">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="154e5-159">A sample data file has been uploaded to a public blob container, *wasbs://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="154e5-159">A sample data file has been uploaded to a public blob container, *wasbs://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="154e5-160">The content of the data file is:</span><span class="sxs-lookup"><span data-stu-id="154e5-160">The content of the data file is:</span></span>

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

<span data-ttu-id="154e5-161">You can create a text file and upload the file to your own storage account if you want.</span><span class="sxs-lookup"><span data-stu-id="154e5-161">You can create a text file and upload the file to your own storage account if you want.</span></span> <span data-ttu-id="154e5-162">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="154e5-162">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="154e5-163">This procedure uses the Contacts HBase table you have created in the last procedure.</span><span class="sxs-lookup"><span data-stu-id="154e5-163">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 
> 

1. <span data-ttu-id="154e5-164">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output:.</span><span class="sxs-lookup"><span data-stu-id="154e5-164">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output:.</span></span>  <span data-ttu-id="154e5-165">If you are in HBase Shell, use the exit command to exit.</span><span class="sxs-lookup"><span data-stu-id="154e5-165">If you are in HBase Shell, use the exit command to exit.</span></span>
   
        hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasbs://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
2. <span data-ttu-id="154e5-166">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span><span class="sxs-lookup"><span data-stu-id="154e5-166">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
        hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
3. <span data-ttu-id="154e5-167">You can open the HBase shell, and use the scan command to list the table content.</span><span class="sxs-lookup"><span data-stu-id="154e5-167">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="154e5-168">Use Hive to query HBase</span><span class="sxs-lookup"><span data-stu-id="154e5-168">Use Hive to query HBase</span></span>
<span data-ttu-id="154e5-169">You can query data in HBase tables by using Hive.</span><span class="sxs-lookup"><span data-stu-id="154e5-169">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="154e5-170">This section creates a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span><span class="sxs-lookup"><span data-stu-id="154e5-170">This section creates a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

> [!NOTE]
> <span data-ttu-id="154e5-171">If Hive and HBase are on different clusters in the same VNet, you need to pass zookeeper quorum while invoking the Hive shell:</span><span class="sxs-lookup"><span data-stu-id="154e5-171">If Hive and HBase are on different clusters in the same VNet, you need to pass zookeeper quorum while invoking the Hive shell:</span></span>
>
>       hive --hiveconf hbase.zookeeper.quorum=zk0-xxxx.xxxxxxxxxxxxxxxxxxxxxxx.cx.internal.cloudapp.net,zk1-xxxx.xxxxxxxxxxxxxxxxxxxxxxx.cx.internal.cloudapp.net,zk2-xxxx.xxxxxxxxxxxxxxxxxxxxxxx.cx.internal.cloudapp.net --hiveconf zookeeper.znode.parent=/hbase-unsecure  
>
>

1. <span data-ttu-id="154e5-172">Open **PuTTY**, and connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="154e5-172">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="154e5-173">See the instructions in the previous procedure.</span><span class="sxs-lookup"><span data-stu-id="154e5-173">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="154e5-174">Open the Hive shell.</span><span class="sxs-lookup"><span data-stu-id="154e5-174">Open the Hive shell.</span></span>
   
       hive
       
3. <span data-ttu-id="154e5-175">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span><span class="sxs-lookup"><span data-stu-id="154e5-175">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="154e5-176">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span><span class="sxs-lookup"><span data-stu-id="154e5-176">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>
   
        CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
        STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
        WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
        TBLPROPERTIES ('hbase.table.name' = 'Contacts');
4. <span data-ttu-id="154e5-177">Run the following HiveQL script to query the data in the HBase table:</span><span class="sxs-lookup"><span data-stu-id="154e5-177">Run the following HiveQL script to query the data in the HBase table:</span></span>
   
         SELECT count(*) FROM hbasecontacts;

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="154e5-178">Use HBase REST APIs using Curl</span><span class="sxs-lookup"><span data-stu-id="154e5-178">Use HBase REST APIs using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="154e5-179">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="154e5-179">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="154e5-180">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span><span class="sxs-lookup"><span data-stu-id="154e5-180">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="154e5-181">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="154e5-181">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="154e5-182">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="154e5-182">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="154e5-183">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="154e5-183">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="154e5-184">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="154e5-184">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="154e5-185">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="154e5-185">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u <UserName>:<Password> \
        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="154e5-186">You should receive a response similar to the following:</span><span class="sxs-lookup"><span data-stu-id="154e5-186">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="154e5-187">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="154e5-187">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="154e5-188">**-u** - The user name and password used to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="154e5-188">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="154e5-189">**-G** - Indicates that this is a GET request.</span><span class="sxs-lookup"><span data-stu-id="154e5-189">**-G** - Indicates that this is a GET request.</span></span>
2. <span data-ttu-id="154e5-190">Use the following command to list the existing HBase tables:</span><span class="sxs-lookup"><span data-stu-id="154e5-190">Use the following command to list the existing HBase tables:</span></span>
   
        curl -u <UserName>:<Password> \
        -G https://<ClusterName>.azurehdinsight.net/hbaserest/
3. <span data-ttu-id="154e5-191">Use the following command to create a new HBase table with two-column families:</span><span class="sxs-lookup"><span data-stu-id="154e5-191">Use the following command to create a new HBase table with two-column families:</span></span>
   
        curl -u <UserName>:<Password> \
        -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
        -H "Accept: application/json" \
        -H "Content-Type: application/json" \
        -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
        -v
   
    <span data-ttu-id="154e5-192">The schema is provided in the JSon format.</span><span class="sxs-lookup"><span data-stu-id="154e5-192">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="154e5-193">Use the following command to insert some data:</span><span class="sxs-lookup"><span data-stu-id="154e5-193">Use the following command to insert some data:</span></span>
   
        curl -u <UserName>:<Password> \
        -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
        -H "Accept: application/json" \
        -H "Content-Type: application/json" \
        -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
        -v
   
    <span data-ttu-id="154e5-194">You must base64 encode the values specified in the -d switch.</span><span class="sxs-lookup"><span data-stu-id="154e5-194">You must base64 encode the values specified in the -d switch.</span></span>  <span data-ttu-id="154e5-195">In the exmaple:</span><span class="sxs-lookup"><span data-stu-id="154e5-195">In the exmaple:</span></span>
   
   * <span data-ttu-id="154e5-196">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="154e5-196">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="154e5-197">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="154e5-197">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="154e5-198">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="154e5-198">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="154e5-199">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) value.</span><span class="sxs-lookup"><span data-stu-id="154e5-199">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) value.</span></span>
5. <span data-ttu-id="154e5-200">Use the following command to get a row:</span><span class="sxs-lookup"><span data-stu-id="154e5-200">Use the following command to get a row:</span></span>
   
        curl -u <UserName>:<Password> \
        -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
        -H "Accept: application/json" \
        -v

<span data-ttu-id="154e5-201">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="154e5-201">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

>
> [!NOTE]
> <span data-ttu-id="154e5-202">Thrift is not supported by HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="154e5-202">Thrift is not supported by HBase in HDInsight.</span></span>
>

## <a name="check-cluster-status"></a><span data-ttu-id="154e5-203">Check cluster status</span><span class="sxs-lookup"><span data-stu-id="154e5-203">Check cluster status</span></span>
<span data-ttu-id="154e5-204">HBase in HDInsight ships with a Web UI for monitoring clusters.</span><span class="sxs-lookup"><span data-stu-id="154e5-204">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="154e5-205">Using the Web UI, you can request statistics or information about regions.</span><span class="sxs-lookup"><span data-stu-id="154e5-205">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="154e5-206">**To access the HBase Master UI**</span><span class="sxs-lookup"><span data-stu-id="154e5-206">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="154e5-207">Open the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="154e5-207">Open the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="154e5-208">Click **HBase** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="154e5-208">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="154e5-209">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span><span class="sxs-lookup"><span data-stu-id="154e5-209">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="154e5-210">The UI is opened in another browser tab:</span><span class="sxs-lookup"><span data-stu-id="154e5-210">The UI is opened in another browser tab:</span></span>

  ![HDInsight HBase HMaster UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="154e5-212">The HBase Master UI contains the following sections:</span><span class="sxs-lookup"><span data-stu-id="154e5-212">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="154e5-213">region servers</span><span class="sxs-lookup"><span data-stu-id="154e5-213">region servers</span></span>
  - <span data-ttu-id="154e5-214">backup masters</span><span class="sxs-lookup"><span data-stu-id="154e5-214">backup masters</span></span>
  - <span data-ttu-id="154e5-215">tables</span><span class="sxs-lookup"><span data-stu-id="154e5-215">tables</span></span>
  - <span data-ttu-id="154e5-216">tasks</span><span class="sxs-lookup"><span data-stu-id="154e5-216">tasks</span></span>
  - <span data-ttu-id="154e5-217">software attributes</span><span class="sxs-lookup"><span data-stu-id="154e5-217">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="154e5-218">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="154e5-218">Delete the cluster</span></span>
<span data-ttu-id="154e5-219">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="154e5-219">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="154e5-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="154e5-220">Next steps</span></span>
<span data-ttu-id="154e5-221">In this HBase tutorial for HDInsight, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span><span class="sxs-lookup"><span data-stu-id="154e5-221">In this HBase tutorial for HDInsight, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="154e5-222">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span><span class="sxs-lookup"><span data-stu-id="154e5-222">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="154e5-223">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="154e5-223">To learn more, see:</span></span>

* <span data-ttu-id="154e5-224">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span><span class="sxs-lookup"><span data-stu-id="154e5-224">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png







