---
title: Run a Hadoop job using Azure DocumentDB and HDInsight | Microsoft Docs
description: Learn how to run a simple Hive, Pig, and MapReduce job with DocumentDB and Azure HDInsight.
services: documentdb
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: ''
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 09/20/2016
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bd2104f60b655cf76384469cd93d692257187c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555066"
---
# <a name="DocumentDB-HDInsight"></a><span data-ttu-id="19f5e-103">Run an Apache Hive, Pig, or Hadoop job using DocumentDB and HDInsight</span><span class="sxs-lookup"><span data-stu-id="19f5e-103">Run an Apache Hive, Pig, or Hadoop job using DocumentDB and HDInsight</span></span>
<span data-ttu-id="19f5e-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with DocumentDB's Hadoop connector.</span><span class="sxs-lookup"><span data-stu-id="19f5e-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with DocumentDB's Hadoop connector.</span></span> <span data-ttu-id="19f5e-105">DocumentDB's Hadoop connector allows DocumentDB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span><span class="sxs-lookup"><span data-stu-id="19f5e-105">DocumentDB's Hadoop connector allows DocumentDB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="19f5e-106">This tutorial will use DocumentDB as both the data source and destination for Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="19f5e-106">This tutorial will use DocumentDB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="19f5e-107">After completing this tutorial, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="19f5e-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="19f5e-108">How do I load data from DocumentDB using a Hive, Pig, or MapReduce job?</span><span class="sxs-lookup"><span data-stu-id="19f5e-108">How do I load data from DocumentDB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="19f5e-109">How do I store data in DocumentDB using a Hive, Pig, or MapReduce job?</span><span class="sxs-lookup"><span data-stu-id="19f5e-109">How do I store data in DocumentDB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="19f5e-110">We recommend getting started by watching the following video, where we run through a Hive job using DocumentDB and HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19f5e-110">We recommend getting started by watching the following video, where we run through a Hive job using DocumentDB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="19f5e-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your DocumentDB data.</span><span class="sxs-lookup"><span data-stu-id="19f5e-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your DocumentDB data.</span></span>

> [!TIP]
> <span data-ttu-id="19f5e-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span><span class="sxs-lookup"><span data-stu-id="19f5e-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="19f5e-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="19f5e-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="19f5e-114">This tutorial also assumes that you have prior experience with DocumentDB and have a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="19f5e-114">This tutorial also assumes that you have prior experience with DocumentDB and have a DocumentDB account.</span></span> <span data-ttu-id="19f5e-115">If you are new to DocumentDB or you do not have a DocumentDB account, please check out our [Getting Started][getting-started] page.</span><span class="sxs-lookup"><span data-stu-id="19f5e-115">If you are new to DocumentDB or you do not have a DocumentDB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="19f5e-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span><span class="sxs-lookup"><span data-stu-id="19f5e-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="19f5e-117">Not a problem, get them [here][documentdb-hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="19f5e-117">Not a problem, get them [here][documentdb-hdinsight-samples].</span></span> <span data-ttu-id="19f5e-118">The download also contains the hql, pig, and java files for these samples.</span><span class="sxs-lookup"><span data-stu-id="19f5e-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <a name="NewestVersion"></a><span data-ttu-id="19f5e-119">Newest Version</span><span class="sxs-lookup"><span data-stu-id="19f5e-119">Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="19f5e-120">Hadoop Connector Version</span><span class="sxs-lookup"><span data-stu-id="19f5e-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="19f5e-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="19f5e-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="19f5e-122">Script Uri</span><span class="sxs-lookup"><span data-stu-id="19f5e-122">Script Uri</span></span></th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th><span data-ttu-id="19f5e-123">Date Modified</span><span class="sxs-lookup"><span data-stu-id="19f5e-123">Date Modified</span></span></th>
        <td><span data-ttu-id="19f5e-124">04/26/2016</span><span class="sxs-lookup"><span data-stu-id="19f5e-124">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="19f5e-125">Supported HDInsight Versions</span><span class="sxs-lookup"><span data-stu-id="19f5e-125">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="19f5e-126">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="19f5e-126">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="19f5e-127">Change Log</span><span class="sxs-lookup"><span data-stu-id="19f5e-127">Change Log</span></span></th>
        <td><span data-ttu-id="19f5e-128">Updated DocumentDB Java SDK to 1.6.0</span><span class="sxs-lookup"><span data-stu-id="19f5e-128">Updated DocumentDB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="19f5e-129">Added support for partitioned collections as both a source and sink</span><span class="sxs-lookup"><span data-stu-id="19f5e-129">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <a name="Prerequisites"></a><span data-ttu-id="19f5e-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="19f5e-130">Prerequisites</span></span>
<span data-ttu-id="19f5e-131">Before following the instructions in this tutorial, ensure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="19f5e-131">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="19f5e-132">A DocumentDB account, a database, and a collection with documents inside.</span><span class="sxs-lookup"><span data-stu-id="19f5e-132">A DocumentDB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="19f5e-133">For more information, see [Getting Started with DocumentDB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="19f5e-133">For more information, see [Getting Started with DocumentDB][getting-started].</span></span> <span data-ttu-id="19f5e-134">Import sample data into your DocumentDB account with the [DocumentDB import tool][documentdb-import-data].</span><span class="sxs-lookup"><span data-stu-id="19f5e-134">Import sample data into your DocumentDB account with the [DocumentDB import tool][documentdb-import-data].</span></span>
* <span data-ttu-id="19f5e-135">Throughput.</span><span class="sxs-lookup"><span data-stu-id="19f5e-135">Throughput.</span></span> <span data-ttu-id="19f5e-136">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span><span class="sxs-lookup"><span data-stu-id="19f5e-136">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="19f5e-137">Capacity for an additional stored procedure within each output collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-137">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="19f5e-138">The stored procedures are used for transferring resulting documents.</span><span class="sxs-lookup"><span data-stu-id="19f5e-138">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="19f5e-139">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span><span class="sxs-lookup"><span data-stu-id="19f5e-139">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="19f5e-140">[*Optional*] Capacity for an additional collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-140">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="19f5e-141">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-141">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="19f5e-142">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span><span class="sxs-lookup"><span data-stu-id="19f5e-142">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="19f5e-143">**The connector will automatically overwrite existing documents with id conflicts**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-143">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="19f5e-144">You can turn off this feature by setting the upsert option to false.</span><span class="sxs-lookup"><span data-stu-id="19f5e-144">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="19f5e-145">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span><span class="sxs-lookup"><span data-stu-id="19f5e-145">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <a name="ProvisionHDInsight"></a><span data-ttu-id="19f5e-146">Step 1: Create a new HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="19f5e-146">Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="19f5e-147">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="19f5e-147">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="19f5e-148">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="19f5e-148">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="19f5e-149">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span><span class="sxs-lookup"><span data-stu-id="19f5e-149">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="19f5e-150">Sign in to the [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="19f5e-150">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="19f5e-151">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span><span class="sxs-lookup"><span data-stu-id="19f5e-151">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="19f5e-152">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span><span class="sxs-lookup"><span data-stu-id="19f5e-152">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="19f5e-153">Click on it and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-153">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="19f5e-154">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span><span class="sxs-lookup"><span data-stu-id="19f5e-154">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="19f5e-155">Cluster name</span><span class="sxs-lookup"><span data-stu-id="19f5e-155">Cluster name</span></span></td><td><span data-ttu-id="19f5e-156">Name the cluster.</span><span class="sxs-lookup"><span data-stu-id="19f5e-156">Name the cluster.</span></span><br/>
<span data-ttu-id="19f5e-157">DNS name must start and end with an alpha numeric character, and may contain dashes.</span><span class="sxs-lookup"><span data-stu-id="19f5e-157">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="19f5e-158">The field must be a string between 3 and 63 characters.</span><span class="sxs-lookup"><span data-stu-id="19f5e-158">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="19f5e-159">Subscription Name</span><span class="sxs-lookup"><span data-stu-id="19f5e-159">Subscription Name</span></span></td>
            <td><span data-ttu-id="19f5e-160">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="19f5e-160">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="19f5e-161">
5. Click \*\*Select Cluster Type*\* and set the following properties to the specified values.</span><span class="sxs-lookup"><span data-stu-id="19f5e-161">
5. Click \*\*Select Cluster Type*\* and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="19f5e-162">Cluster type</span><span class="sxs-lookup"><span data-stu-id="19f5e-162">Cluster type</span></span></td><td><span data-ttu-id="19f5e-163"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="19f5e-163"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="19f5e-164">Cluster tier</span><span class="sxs-lookup"><span data-stu-id="19f5e-164">Cluster tier</span></span></td><td><span data-ttu-id="19f5e-165"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="19f5e-165"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="19f5e-166">Operating System</span><span class="sxs-lookup"><span data-stu-id="19f5e-166">Operating System</span></span></td><td><span data-ttu-id="19f5e-167"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="19f5e-167"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="19f5e-168">Version</span><span class="sxs-lookup"><span data-stu-id="19f5e-168">Version</span></span></td><td><span data-ttu-id="19f5e-169">latest version</span><span class="sxs-lookup"><span data-stu-id="19f5e-169">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="19f5e-170">Now, click **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-170">Now, click **SELECT**.</span></span>

    ![Provide Hadoop HDInsight initial cluster details][image-customprovision-page1]
6. <span data-ttu-id="19f5e-172">Click on **Credentials** to set your login and remote access credentials.</span><span class="sxs-lookup"><span data-stu-id="19f5e-172">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="19f5e-173">Choose your **Cluster Login Username** and **Cluster Login Password**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-173">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="19f5e-174">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span><span class="sxs-lookup"><span data-stu-id="19f5e-174">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="19f5e-175">Click on **Data Source** to set your primary location for data access.</span><span class="sxs-lookup"><span data-stu-id="19f5e-175">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="19f5e-176">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="19f5e-176">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="19f5e-177">On the same blade, specify a **Default Container** and a **Location**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-177">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="19f5e-178">And, click **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-178">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19f5e-179">Select a location close to your DocumentDB account region for better performance</span><span class="sxs-lookup"><span data-stu-id="19f5e-179">Select a location close to your DocumentDB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="19f5e-180">Click on **Pricing** to select the number and type of nodes.</span><span class="sxs-lookup"><span data-stu-id="19f5e-180">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="19f5e-181">You can keep the default configuration and scale the number of Worker nodes later on.</span><span class="sxs-lookup"><span data-stu-id="19f5e-181">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="19f5e-182">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span><span class="sxs-lookup"><span data-stu-id="19f5e-182">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="19f5e-183">In Script Actions, enter the following information to customize your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="19f5e-183">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="19f5e-184">Property</span><span class="sxs-lookup"><span data-stu-id="19f5e-184">Property</span></span></th><th><span data-ttu-id="19f5e-185">Value</span><span class="sxs-lookup"><span data-stu-id="19f5e-185">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="19f5e-186">Name</span><span class="sxs-lookup"><span data-stu-id="19f5e-186">Name</span></span></td>
             <td><span data-ttu-id="19f5e-187">Specify a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="19f5e-187">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="19f5e-188">Script URI</span><span class="sxs-lookup"><span data-stu-id="19f5e-188">Script URI</span></span></td>
             <td><span data-ttu-id="19f5e-189">Specify the URI to the script that is invoked to customize the cluster.</span><span class="sxs-lookup"><span data-stu-id="19f5e-189">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="19f5e-190">Please enter:</span><span class="sxs-lookup"><span data-stu-id="19f5e-190">Please enter:</span></span> </br> <span data-ttu-id="19f5e-191"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-191"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="19f5e-192">Head</span><span class="sxs-lookup"><span data-stu-id="19f5e-192">Head</span></span></td>
             <td><span data-ttu-id="19f5e-193">Click the checkbox to run the PowerShell script onto the Head node.</span><span class="sxs-lookup"><span data-stu-id="19f5e-193">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="19f5e-194">
             <strong>Check this checkbox</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-194">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="19f5e-195">Worker</span><span class="sxs-lookup"><span data-stu-id="19f5e-195">Worker</span></span></td>
             <td><span data-ttu-id="19f5e-196">Click the checkbox to run the PowerShell script onto the Worker node.</span><span class="sxs-lookup"><span data-stu-id="19f5e-196">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="19f5e-197">
             <strong>Check this checkbox</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-197">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="19f5e-198">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="19f5e-198">Zookeeper</span></span></td>
             <td><span data-ttu-id="19f5e-199">Click the checkbox to run the PowerShell script onto the Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="19f5e-199">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="19f5e-200">
             <strong>Not needed</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-200">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="19f5e-201">Parameters</span><span class="sxs-lookup"><span data-stu-id="19f5e-201">Parameters</span></span></td>
             <td><span data-ttu-id="19f5e-202">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="19f5e-202">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="19f5e-203">
             <strong>No Parameters needed</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-203">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="19f5e-204">
11. Create either a new \*\*Resource Group*\* or use an existing Resource Group under your Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="19f5e-204">
11. Create either a new \*\*Resource Group*\* or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="19f5e-205">12.</span><span class="sxs-lookup"><span data-stu-id="19f5e-205">12.</span></span> <span data-ttu-id="19f5e-206">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span><span class="sxs-lookup"><span data-stu-id="19f5e-206">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <a name="InstallCmdlets"></a><span data-ttu-id="19f5e-207">Step 2: Install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="19f5e-207">Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="19f5e-208">Install Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19f5e-208">Install Azure PowerShell.</span></span> <span data-ttu-id="19f5e-209">Instructions can be found [here][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="19f5e-209">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="19f5e-210">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span><span class="sxs-lookup"><span data-stu-id="19f5e-210">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="19f5e-211">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="19f5e-211">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="19f5e-212">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-212">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="19f5e-213">Open the Azure PowerShell Integrated Scripting Environment:</span><span class="sxs-lookup"><span data-stu-id="19f5e-213">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="19f5e-214">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span><span class="sxs-lookup"><span data-stu-id="19f5e-214">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="19f5e-215">From the Start screen, type **powershell ise** and click **Enter**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-215">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="19f5e-216">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span><span class="sxs-lookup"><span data-stu-id="19f5e-216">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="19f5e-217">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-217">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="19f5e-218">In the Command Prompt, type **powershell_ise** and click **Enter**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-218">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="19f5e-219">Add your Azure Account.</span><span class="sxs-lookup"><span data-stu-id="19f5e-219">Add your Azure Account.</span></span>

   1. <span data-ttu-id="19f5e-220">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-220">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="19f5e-221">Type in the email address associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-221">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="19f5e-222">Type in the password for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="19f5e-222">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="19f5e-223">Click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="19f5e-223">Click **Sign in**.</span></span>
4. <span data-ttu-id="19f5e-224">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span><span class="sxs-lookup"><span data-stu-id="19f5e-224">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagram for Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a><span data-ttu-id="19f5e-226">Step 3: Run a Hive job using DocumentDB and HDInsight</span><span class="sxs-lookup"><span data-stu-id="19f5e-226">Step 3: Run a Hive job using DocumentDB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="19f5e-227">All variables indicated by < > must be filled in using your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="19f5e-227">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="19f5e-228">Set the following variables in your PowerShell Script pane.</span><span class="sxs-lookup"><span data-stu-id="19f5e-228">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="19f5e-229">Let's begin constructing your query string.</span><span class="sxs-lookup"><span data-stu-id="19f5e-229">Let's begin constructing your query string.</span></span> <span data-ttu-id="19f5e-230">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from a DocumentDB collection, tallies all documents by the minute, and then stores the results back into a new DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-230">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from a DocumentDB collection, tallies all documents by the minute, and then stores the results back into a new DocumentDB collection.</span></span></p>

    <p><span data-ttu-id="19f5e-231">First, let's create a Hive table from our DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-231">First, let's create a Hive table from our DocumentDB collection.</span></span> <span data-ttu-id="19f5e-232">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span><span class="sxs-lookup"><span data-stu-id="19f5e-232">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="19f5e-233">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span><span class="sxs-lookup"><span data-stu-id="19f5e-233">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="19f5e-234">**Naming DocumentDB.inputCollections was not a mistake.**</span><span class="sxs-lookup"><span data-stu-id="19f5e-234">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="19f5e-235">Yes, we allow adding multiple collections as an input:</span><span class="sxs-lookup"><span data-stu-id="19f5e-235">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="19f5e-236">Next, let's create a Hive table for the output collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-236">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="19f5e-237">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span><span class="sxs-lookup"><span data-stu-id="19f5e-237">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19f5e-238">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span><span class="sxs-lookup"><span data-stu-id="19f5e-238">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="19f5e-239">Yes, we allow adding multiple collections as an output:</span><span class="sxs-lookup"><span data-stu-id="19f5e-239">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="19f5e-240">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="19f5e-240">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="19f5e-241">The collection names are separated without spaces, using only a single comma.</span><span class="sxs-lookup"><span data-stu-id="19f5e-241">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="19f5e-242">Documents will be distributed round-robin across multiple collections.</span><span class="sxs-lookup"><span data-stu-id="19f5e-242">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="19f5e-243">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span><span class="sxs-lookup"><span data-stu-id="19f5e-243">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="19f5e-244">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span><span class="sxs-lookup"><span data-stu-id="19f5e-244">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="19f5e-245">Add the following script snippet to create a Hive job definition from the previous query.</span><span class="sxs-lookup"><span data-stu-id="19f5e-245">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="19f5e-246">You can also use the -File switch to specify a HiveQL script file on HDFS.</span><span class="sxs-lookup"><span data-stu-id="19f5e-246">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="19f5e-247">Add the following snippet to save the start time and submit the Hive job.</span><span class="sxs-lookup"><span data-stu-id="19f5e-247">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="19f5e-248">Add the following to wait for the Hive job to complete.</span><span class="sxs-lookup"><span data-stu-id="19f5e-248">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="19f5e-249">Add the following to print the standard output and the start and end times.</span><span class="sxs-lookup"><span data-stu-id="19f5e-249">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="19f5e-250">**Run** your new script!</span><span class="sxs-lookup"><span data-stu-id="19f5e-250">**Run** your new script!</span></span> <span data-ttu-id="19f5e-251">**Click** the green execute button.</span><span class="sxs-lookup"><span data-stu-id="19f5e-251">**Click** the green execute button.</span></span>
8. <span data-ttu-id="19f5e-252">Check the results.</span><span class="sxs-lookup"><span data-stu-id="19f5e-252">Check the results.</span></span> <span data-ttu-id="19f5e-253">Sign into the [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="19f5e-253">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="19f5e-254">Click <strong>Browse</strong> on the left-side panel.</span><span class="sxs-lookup"><span data-stu-id="19f5e-254">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="19f5e-255">Click <strong>everything</strong> at the top-right of the browse panel.</span><span class="sxs-lookup"><span data-stu-id="19f5e-255">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="19f5e-256">Find and click <strong>DocumentDB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-256">Find and click <strong>DocumentDB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="19f5e-257">Next, find your <strong>DocumentDB Account</strong>, then <strong>DocumentDB Database</strong> and your <strong>DocumentDB Collection</strong> associated with the output collection specified in your Hive query.</span><span class="sxs-lookup"><span data-stu-id="19f5e-257">Next, find your <strong>DocumentDB Account</strong>, then <strong>DocumentDB Database</strong> and your <strong>DocumentDB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="19f5e-258">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-258">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="19f5e-259">You will see the results of your Hive query.</span><span class="sxs-lookup"><span data-stu-id="19f5e-259">You will see the results of your Hive query.</span></span>

   ![Hive query results][image-hive-query-results]

## <a name="RunPig"></a><span data-ttu-id="19f5e-261">Step 4: Run a Pig job using DocumentDB and HDInsight</span><span class="sxs-lookup"><span data-stu-id="19f5e-261">Step 4: Run a Pig job using DocumentDB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="19f5e-262">All variables indicated by < > must be filled in using your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="19f5e-262">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="19f5e-263">Set the following variables in your PowerShell Script pane.</span><span class="sxs-lookup"><span data-stu-id="19f5e-263">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="19f5e-264">Let's begin constructing your query string.</span><span class="sxs-lookup"><span data-stu-id="19f5e-264">Let's begin constructing your query string.</span></span> <span data-ttu-id="19f5e-265">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from a DocumentDB collection, tallies all documents by the minute, and then stores the results back into a new DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-265">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from a DocumentDB collection, tallies all documents by the minute, and then stores the results back into a new DocumentDB collection.</span></span></p>
    <p><span data-ttu-id="19f5e-266">First, load documents from DocumentDB into HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19f5e-266">First, load documents from DocumentDB into HDInsight.</span></span> <span data-ttu-id="19f5e-267">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span><span class="sxs-lookup"><span data-stu-id="19f5e-267">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="19f5e-268">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span><span class="sxs-lookup"><span data-stu-id="19f5e-268">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="19f5e-269">Yes, we allow adding multiple collections as an input:</span><span class="sxs-lookup"><span data-stu-id="19f5e-269">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="19f5e-270">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="19f5e-270">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="19f5e-271">The collection names are separated without spaces, using only a single comma.</span><span class="sxs-lookup"><span data-stu-id="19f5e-271">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="19f5e-272">Documents will be distributed round-robin across multiple collections.</span><span class="sxs-lookup"><span data-stu-id="19f5e-272">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="19f5e-273">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span><span class="sxs-lookup"><span data-stu-id="19f5e-273">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from DocumentDB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="19f5e-274">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span><span class="sxs-lookup"><span data-stu-id="19f5e-274">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="19f5e-275">Finally, let's store the results into our new output collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-275">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19f5e-276">Yes, we allow adding multiple collections as an output:</span><span class="sxs-lookup"><span data-stu-id="19f5e-276">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="19f5e-277">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span><span class="sxs-lookup"><span data-stu-id="19f5e-277">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="19f5e-278">The collection names are separated without spaces, using only a single comma.</span><span class="sxs-lookup"><span data-stu-id="19f5e-278">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="19f5e-279">Documents will be distributed round-robin across the multiple collections.</span><span class="sxs-lookup"><span data-stu-id="19f5e-279">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="19f5e-280">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span><span class="sxs-lookup"><span data-stu-id="19f5e-280">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to DocumentDB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="19f5e-281">Add the following script snippet to create a Pig job definition from the previous query.</span><span class="sxs-lookup"><span data-stu-id="19f5e-281">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="19f5e-282">You can also use the -File switch to specify a Pig script file on HDFS.</span><span class="sxs-lookup"><span data-stu-id="19f5e-282">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="19f5e-283">Add the following snippet to save the start time and submit the Pig job.</span><span class="sxs-lookup"><span data-stu-id="19f5e-283">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="19f5e-284">Add the following to wait for the Pig job to complete.</span><span class="sxs-lookup"><span data-stu-id="19f5e-284">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="19f5e-285">Add the following to print the standard output and the start and end times.</span><span class="sxs-lookup"><span data-stu-id="19f5e-285">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="19f5e-286">**Run** your new script!</span><span class="sxs-lookup"><span data-stu-id="19f5e-286">**Run** your new script!</span></span> <span data-ttu-id="19f5e-287">**Click** the green execute button.</span><span class="sxs-lookup"><span data-stu-id="19f5e-287">**Click** the green execute button.</span></span>
10. <span data-ttu-id="19f5e-288">Check the results.</span><span class="sxs-lookup"><span data-stu-id="19f5e-288">Check the results.</span></span> <span data-ttu-id="19f5e-289">Sign into the [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="19f5e-289">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="19f5e-290">Click <strong>Browse</strong> on the left-side panel.</span><span class="sxs-lookup"><span data-stu-id="19f5e-290">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="19f5e-291">Click <strong>everything</strong> at the top-right of the browse panel.</span><span class="sxs-lookup"><span data-stu-id="19f5e-291">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="19f5e-292">Find and click <strong>DocumentDB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-292">Find and click <strong>DocumentDB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="19f5e-293">Next, find your <strong>DocumentDB Account</strong>, then <strong>DocumentDB Database</strong> and your <strong>DocumentDB Collection</strong> associated with the output collection specified in your Pig query.</span><span class="sxs-lookup"><span data-stu-id="19f5e-293">Next, find your <strong>DocumentDB Account</strong>, then <strong>DocumentDB Database</strong> and your <strong>DocumentDB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="19f5e-294">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-294">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="19f5e-295">You will see the results of your Pig query.</span><span class="sxs-lookup"><span data-stu-id="19f5e-295">You will see the results of your Pig query.</span></span>

    ![Pig query results][image-pig-query-results]

## <a name="RunMapReduce"></a><span data-ttu-id="19f5e-297">Step 5: Run a MapReduce job using DocumentDB and HDInsight</span><span class="sxs-lookup"><span data-stu-id="19f5e-297">Step 5: Run a MapReduce job using DocumentDB and HDInsight</span></span>
1. <span data-ttu-id="19f5e-298">Set the following variables in your PowerShell Script pane.</span><span class="sxs-lookup"><span data-stu-id="19f5e-298">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="19f5e-299">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="19f5e-299">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your DocumentDB collection.</span></span> <span data-ttu-id="19f5e-300">Add this script snippet **after** the snippet above.</span><span class="sxs-lookup"><span data-stu-id="19f5e-300">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="19f5e-301">TallyProperties-v01.jar comes with the custom installation of the DocumentDB Hadoop Connector.</span><span class="sxs-lookup"><span data-stu-id="19f5e-301">TallyProperties-v01.jar comes with the custom installation of the DocumentDB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="19f5e-302">Add the following command to submit the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="19f5e-302">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="19f5e-303">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span><span class="sxs-lookup"><span data-stu-id="19f5e-303">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="19f5e-304">The Start-AzureHDInsightJob is an asynchronized call.</span><span class="sxs-lookup"><span data-stu-id="19f5e-304">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="19f5e-305">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="19f5e-305">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="19f5e-306">Add the following command to check any errors with running the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="19f5e-306">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="19f5e-307">**Run** your new script!</span><span class="sxs-lookup"><span data-stu-id="19f5e-307">**Run** your new script!</span></span> <span data-ttu-id="19f5e-308">**Click** the green execute button.</span><span class="sxs-lookup"><span data-stu-id="19f5e-308">**Click** the green execute button.</span></span>
6. <span data-ttu-id="19f5e-309">Check the results.</span><span class="sxs-lookup"><span data-stu-id="19f5e-309">Check the results.</span></span> <span data-ttu-id="19f5e-310">Sign into the [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="19f5e-310">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="19f5e-311">Click <strong>Browse</strong> on the left-side panel.</span><span class="sxs-lookup"><span data-stu-id="19f5e-311">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="19f5e-312">Click <strong>everything</strong> at the top-right of the browse panel.</span><span class="sxs-lookup"><span data-stu-id="19f5e-312">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="19f5e-313">Find and click <strong>DocumentDB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-313">Find and click <strong>DocumentDB Accounts</strong>.</span></span>
   4. <span data-ttu-id="19f5e-314">Next, find your <strong>DocumentDB Account</strong>, then <strong>DocumentDB Database</strong> and your <strong>DocumentDB Collection</strong> associated with the output collection specified in your MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="19f5e-314">Next, find your <strong>DocumentDB Account</strong>, then <strong>DocumentDB Database</strong> and your <strong>DocumentDB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="19f5e-315">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="19f5e-315">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="19f5e-316">You will see the results of your MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="19f5e-316">You will see the results of your MapReduce job.</span></span>

      ![MapReduce query results][image-mapreduce-query-results]

## <a name="NextSteps"></a><span data-ttu-id="19f5e-318">Next Steps</span><span class="sxs-lookup"><span data-stu-id="19f5e-318">Next Steps</span></span>
<span data-ttu-id="19f5e-319">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="19f5e-319">Congratulations!</span></span> <span data-ttu-id="19f5e-320">You just ran your first Hive, Pig, and MapReduce jobs using Azure DocumentDB and HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19f5e-320">You just ran your first Hive, Pig, and MapReduce jobs using Azure DocumentDB and HDInsight.</span></span>

<span data-ttu-id="19f5e-321">We have open sourced our Hadoop Connector.</span><span class="sxs-lookup"><span data-stu-id="19f5e-321">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="19f5e-322">If you're interested, you can contribute on [GitHub][documentdb-github].</span><span class="sxs-lookup"><span data-stu-id="19f5e-322">If you're interested, you can contribute on [GitHub][documentdb-github].</span></span>

<span data-ttu-id="19f5e-323">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="19f5e-323">To learn more, see the following articles:</span></span>

* <span data-ttu-id="19f5e-324">[Develop a Java application with Documentdb][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="19f5e-324">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="19f5e-325">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="19f5e-325">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="19f5e-326">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="19f5e-326">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="19f5e-327">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="19f5e-327">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="19f5e-328">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="19f5e-328">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="19f5e-329">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="19f5e-329">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="19f5e-330">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="19f5e-330">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[documentdb-hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[documentdb-github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[documentdb-import-data]: documentdb-import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: /powershell/azureps-cmdlets-docs





