---
title: Access Hadoop YARN application logs on Linux-based HDInsight | Microsoft Docs
description: Learn how to access YARN application logs on a Linux-based HDInsight (Hadoop) cluster using both the command-line and a web browser.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: larryfr
ms.openlocfilehash: 7829602db1ff6d4aaa49fe05e01a600bd3b79dfe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551304"
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a><span data-ttu-id="7ad08-103">Access YARN application logs on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ad08-103">Access YARN application logs on Linux-based HDInsight</span></span>
<span data-ttu-id="7ad08-104">This document explains how to access the logs for YARN (Yet Another Resource Negotiator) applications that have finished on a Hadoop cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ad08-104">This document explains how to access the logs for YARN (Yet Another Resource Negotiator) applications that have finished on a Hadoop cluster in Azure HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ad08-105">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="7ad08-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7ad08-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="7ad08-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7ad08-107">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="7ad08-107">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ad08-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7ad08-108">Prerequisites</span></span>
* <span data-ttu-id="7ad08-109">A Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7ad08-109">A Linux-based HDInsight cluster.</span></span>
* <span data-ttu-id="7ad08-110">You must [create an SSH tunnel](hdinsight-linux-ambari-ssh-tunnel.md) before you can access the ResourceManager Logs web UI.</span><span class="sxs-lookup"><span data-stu-id="7ad08-110">You must [create an SSH tunnel](hdinsight-linux-ambari-ssh-tunnel.md) before you can access the ResourceManager Logs web UI.</span></span>

## <a name="YARNTimelineServer"></a><span data-ttu-id="7ad08-111">YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="7ad08-111">YARN Timeline Server</span></span>
<span data-ttu-id="7ad08-112">The [YARN Timeline Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) provides generic information on completed applications and framework-specific application information through two different interfaces.</span><span class="sxs-lookup"><span data-stu-id="7ad08-112">The [YARN Timeline Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) provides generic information on completed applications and framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="7ad08-113">Specifically:</span><span class="sxs-lookup"><span data-stu-id="7ad08-113">Specifically:</span></span>

* <span data-ttu-id="7ad08-114">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span><span class="sxs-lookup"><span data-stu-id="7ad08-114">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="7ad08-115">The framework-specific application information component of the Timeline Server is not currently available on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="7ad08-115">The framework-specific application information component of the Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="7ad08-116">Generic information on applications includes the following sorts of data:</span><span class="sxs-lookup"><span data-stu-id="7ad08-116">Generic information on applications includes the following sorts of data:</span></span>

* <span data-ttu-id="7ad08-117">The application ID, a unique identifier of an application</span><span class="sxs-lookup"><span data-stu-id="7ad08-117">The application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="7ad08-118">The user who started the application</span><span class="sxs-lookup"><span data-stu-id="7ad08-118">The user who started the application</span></span>
* <span data-ttu-id="7ad08-119">Information on attempts made to complete the application</span><span class="sxs-lookup"><span data-stu-id="7ad08-119">Information on attempts made to complete the application</span></span>
* <span data-ttu-id="7ad08-120">The containers used by any given application attempt</span><span class="sxs-lookup"><span data-stu-id="7ad08-120">The containers used by any given application attempt</span></span>

## <a name="YARNAppsAndLogs"></a><span data-ttu-id="7ad08-121">YARN applications and logs</span><span class="sxs-lookup"><span data-stu-id="7ad08-121">YARN applications and logs</span></span>

<span data-ttu-id="7ad08-122">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span><span class="sxs-lookup"><span data-stu-id="7ad08-122">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="7ad08-123">This is done through a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span><span class="sxs-lookup"><span data-stu-id="7ad08-123">This is done through a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="7ad08-124">The per-application AM negotiates resources (CPU, memory, disk, network) for running your application with the RM.</span><span class="sxs-lookup"><span data-stu-id="7ad08-124">The per-application AM negotiates resources (CPU, memory, disk, network) for running your application with the RM.</span></span> <span data-ttu-id="7ad08-125">The RM works with NMs to grant these resources, which are granted as *containers*.</span><span class="sxs-lookup"><span data-stu-id="7ad08-125">The RM works with NMs to grant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="7ad08-126">The AM is responsible for tracking the progress of the containers assigned to it by the RM.</span><span class="sxs-lookup"><span data-stu-id="7ad08-126">The AM is responsible for tracking the progress of the containers assigned to it by the RM.</span></span> <span data-ttu-id="7ad08-127">An application may require many containers depending on the nature of the application.</span><span class="sxs-lookup"><span data-stu-id="7ad08-127">An application may require many containers depending on the nature of the application.</span></span>

<span data-ttu-id="7ad08-128">Each application may consist of multiple *application attempts*.</span><span class="sxs-lookup"><span data-stu-id="7ad08-128">Each application may consist of multiple *application attempts*.</span></span> <span data-ttu-id="7ad08-129">This allows an application to retry an operation when a crash occurs or there is a loss of communication between an AM and an RM.</span><span class="sxs-lookup"><span data-stu-id="7ad08-129">This allows an application to retry an operation when a crash occurs or there is a loss of communication between an AM and an RM.</span></span> <span data-ttu-id="7ad08-130">Each attempt runs in a container.</span><span class="sxs-lookup"><span data-stu-id="7ad08-130">Each attempt runs in a container.</span></span> <span data-ttu-id="7ad08-131">In a sense, a container provides the context for basic unit of work performed by a YARN application.</span><span class="sxs-lookup"><span data-stu-id="7ad08-131">In a sense, a container provides the context for basic unit of work performed by a YARN application.</span></span> <span data-ttu-id="7ad08-132">All work that is done within the context of a container is performed on the single worker node on which the container was allocated.</span><span class="sxs-lookup"><span data-stu-id="7ad08-132">All work that is done within the context of a container is performed on the single worker node on which the container was allocated.</span></span> <span data-ttu-id="7ad08-133">See [YARN Concepts][YARN-concepts] for further reference.</span><span class="sxs-lookup"><span data-stu-id="7ad08-133">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="7ad08-134">Application logs (and the associated container logs) are critical in debugging problematic Hadoop applications.</span><span class="sxs-lookup"><span data-stu-id="7ad08-134">Application logs (and the associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="7ad08-135">YARN provides a nice framework for collecting, aggregating, and storing application logs with the [Log Aggregation][log-aggregation] feature.</span><span class="sxs-lookup"><span data-stu-id="7ad08-135">YARN provides a nice framework for collecting, aggregating, and storing application logs with the [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="7ad08-136">The Log Aggregation feature makes accessing application logs more deterministic.</span><span class="sxs-lookup"><span data-stu-id="7ad08-136">The Log Aggregation feature makes accessing application logs more deterministic.</span></span> <span data-ttu-id="7ad08-137">It aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node.</span><span class="sxs-lookup"><span data-stu-id="7ad08-137">It aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node.</span></span> <span data-ttu-id="7ad08-138">The log is stored on the default file system after an application finishes.</span><span class="sxs-lookup"><span data-stu-id="7ad08-138">The log is stored on the default file system after an application finishes.</span></span> <span data-ttu-id="7ad08-139">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node will always be aggregated to a single file.</span><span class="sxs-lookup"><span data-stu-id="7ad08-139">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node will always be aggregated to a single file.</span></span> <span data-ttu-id="7ad08-140">This results in one log file per worker node used by your application.</span><span class="sxs-lookup"><span data-stu-id="7ad08-140">This results in one log file per worker node used by your application.</span></span> <span data-ttu-id="7ad08-141">Log Aggregation is enabled by default on HDInsight clusters (version 3.0 and above), and aggregated logs can be found in the default container of your cluster at the following location:</span><span class="sxs-lookup"><span data-stu-id="7ad08-141">Log Aggregation is enabled by default on HDInsight clusters (version 3.0 and above), and aggregated logs can be found in the default container of your cluster at the following location:</span></span>

    wasbs:///app-logs/<user>/logs/<applicationId>

<span data-ttu-id="7ad08-142">In that location, *user* is the name of the user who started the application, and *applicationId* is the unique identifier of an application as assigned by the YARN RM.</span><span class="sxs-lookup"><span data-stu-id="7ad08-142">In that location, *user* is the name of the user who started the application, and *applicationId* is the unique identifier of an application as assigned by the YARN RM.</span></span>

<span data-ttu-id="7ad08-143">The aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span><span class="sxs-lookup"><span data-stu-id="7ad08-143">The aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="7ad08-144">You must use the YARN ResourceManager logs or CLI tools to view these logs as plain text for applications or containers of interest.</span><span class="sxs-lookup"><span data-stu-id="7ad08-144">You must use the YARN ResourceManager logs or CLI tools to view these logs as plain text for applications or containers of interest.</span></span>

## <a name="yarn-cli-tools"></a><span data-ttu-id="7ad08-145">YARN CLI tools</span><span class="sxs-lookup"><span data-stu-id="7ad08-145">YARN CLI tools</span></span>

<span data-ttu-id="7ad08-146">To use the YARN CLI tools, you must first connect to the HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="7ad08-146">To use the YARN CLI tools, you must first connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="7ad08-147">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7ad08-147">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="7ad08-148">You can view these logs as plain text by running one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="7ad08-148">You can view these logs as plain text by running one of the following commands:</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

<span data-ttu-id="7ad08-149">You must specify the &lt;applicationId>, &lt;user-who-started-the-application>, &lt;containerId>, and &lt;worker-node-address> information when running these commands.</span><span class="sxs-lookup"><span data-stu-id="7ad08-149">You must specify the &lt;applicationId>, &lt;user-who-started-the-application>, &lt;containerId>, and &lt;worker-node-address> information when running these commands.</span></span>

## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="7ad08-150">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="7ad08-150">YARN ResourceManager UI</span></span>
<span data-ttu-id="7ad08-151">The YARN ResourceManager UI runs on the cluster headnode, and can be accessed through the Ambari web UI; however, you must first [create an SSH tunnel](hdinsight-linux-ambari-ssh-tunnel.md) before you can access the ResourceManager UI.</span><span class="sxs-lookup"><span data-stu-id="7ad08-151">The YARN ResourceManager UI runs on the cluster headnode, and can be accessed through the Ambari web UI; however, you must first [create an SSH tunnel](hdinsight-linux-ambari-ssh-tunnel.md) before you can access the ResourceManager UI.</span></span>

<span data-ttu-id="7ad08-152">Once you have created an SSH tunnel, use the following steps to view the YARN logs:</span><span class="sxs-lookup"><span data-stu-id="7ad08-152">Once you have created an SSH tunnel, use the following steps to view the YARN logs:</span></span>

1. <span data-ttu-id="7ad08-153">In your web browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="7ad08-153">In your web browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="7ad08-154">Replace CLUSTERNAME with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7ad08-154">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="7ad08-155">From the list of services on the left, select **YARN**.</span><span class="sxs-lookup"><span data-stu-id="7ad08-155">From the list of services on the left, select **YARN**.</span></span>

    ![Yarn service selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. <span data-ttu-id="7ad08-157">From the **Quick Links** dropdown, select one of the cluster head nodes and then select **ResourceManager Log**.</span><span class="sxs-lookup"><span data-stu-id="7ad08-157">From the **Quick Links** dropdown, select one of the cluster head nodes and then select **ResourceManager Log**.</span></span>

    ![Yarn quick links](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    <span data-ttu-id="7ad08-159">You are presented with a list of links to YARN logs.</span><span class="sxs-lookup"><span data-stu-id="7ad08-159">You are presented with a list of links to YARN logs.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/


