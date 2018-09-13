---
title: Enable heap dumps for Hadoop services on HDInsight - Azure
description: Enable heap dumps for Hadoop services from Linux-based HDInsight clusters for debugging and analysis.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/27/2018
ms.author: jasonh
ms.openlocfilehash: 7fa0ebb1946a856d02296b4ec752113ff8fecbd5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814605"
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="7cb0a-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="7cb0a-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="7cb0a-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="7cb0a-105">So they are useful for diagnosing problems that occur at run-time.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7cb0a-106">The steps in this document only work with HDInsight clusters that use Linux.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="7cb0a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7cb0a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7cb0a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="whichServices"></a><span data-ttu-id="7cb0a-109">Services</span><span class="sxs-lookup"><span data-stu-id="7cb0a-109">Services</span></span>

<span data-ttu-id="7cb0a-110">You can enable heap dumps for the following services:</span><span class="sxs-lookup"><span data-stu-id="7cb0a-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="7cb0a-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="7cb0a-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="7cb0a-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="7cb0a-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="7cb0a-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="7cb0a-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="7cb0a-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="7cb0a-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="7cb0a-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="7cb0a-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="7cb0a-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <a name="configuration"></a><span data-ttu-id="7cb0a-117">Understanding heap dump configuration</span><span class="sxs-lookup"><span data-stu-id="7cb0a-117">Understanding heap dump configuration</span></span>

<span data-ttu-id="7cb0a-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="7cb0a-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="7cb0a-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="7cb0a-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="7cb0a-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="7cb0a-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="7cb0a-124">Both contained in **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="7cb0a-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="7cb0a-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="7cb0a-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="7cb0a-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="7cb0a-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="7cb0a-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="7cb0a-128">See the [Using Ambari](#using-ambari) section for specific steps.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="7cb0a-129">Enable heap dumps</span><span class="sxs-lookup"><span data-stu-id="7cb0a-129">Enable heap dumps</span></span>

<span data-ttu-id="7cb0a-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span><span class="sxs-lookup"><span data-stu-id="7cb0a-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="7cb0a-131">The **+** indicates that this option is enabled.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="7cb0a-132">The default is disabled.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="7cb0a-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="7cb0a-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="7cb0a-135">Dump location</span><span class="sxs-lookup"><span data-stu-id="7cb0a-135">Dump location</span></span>

<span data-ttu-id="7cb0a-136">The default location for the dump file is the current working directory.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="7cb0a-137">You can control where the file is stored using the following option:</span><span class="sxs-lookup"><span data-stu-id="7cb0a-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="7cb0a-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="7cb0a-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="7cb0a-139">Scripts</span></span>

<span data-ttu-id="7cb0a-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="7cb0a-141">For example, triggering a notification so you know that the error has occurred.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="7cb0a-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="7cb0a-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="7cb0a-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="7cb0a-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="7cb0a-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="7cb0a-146">Using Ambari</span><span class="sxs-lookup"><span data-stu-id="7cb0a-146">Using Ambari</span></span>

<span data-ttu-id="7cb0a-147">To modify the configuration for a service, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="7cb0a-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="7cb0a-148">Open the Ambari web UI for your cluster.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="7cb0a-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="7cb0a-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7cb0a-151">You may be prompted a second time by Ambari for the user name and password.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="7cb0a-152">If so, enter the same account name and password</span><span class="sxs-lookup"><span data-stu-id="7cb0a-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="7cb0a-153">Using the list of on the left, select the service area you want to modify.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="7cb0a-154">For example, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-154">For example, **HDFS**.</span></span> <span data-ttu-id="7cb0a-155">In the center area, select the **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-155">In the center area, select the **Configs** tab.</span></span>

    ![Image of Ambari web with HDFS Configs tab selected](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="7cb0a-157">Using the **Filter...** entry, enter **opts**.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="7cb0a-158">Only items containing this text are displayed.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-158">Only items containing this text are displayed.</span></span>

    ![Filtered list](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="7cb0a-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="7cb0a-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span><span class="sxs-lookup"><span data-stu-id="7cb0a-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS with -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="7cb0a-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="7cb0a-164">Use the **Save** button to save the changes.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="7cb0a-165">You can enter a short note describing the changes.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="7cb0a-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![restart required icon and restart button](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="7cb0a-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="7cb0a-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![Turn on maintenance mode menu](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="7cb0a-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span><span class="sxs-lookup"><span data-stu-id="7cb0a-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![Restart All Affected entry](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="7cb0a-173">the entries for the **Restart** button may be different for other services.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="7cb0a-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="7cb0a-175">This Ambari to resume monitoring for alerts for the service.</span><span class="sxs-lookup"><span data-stu-id="7cb0a-175">This Ambari to resume monitoring for alerts for the service.</span></span>

