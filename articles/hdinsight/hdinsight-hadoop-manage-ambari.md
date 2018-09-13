---
title: Monitor and manage Azure HDInsight using Ambari Web UI | Microsoft Docs
description: Learn how to use Ambari to monitor and manage Linux-based HDInsight clusters. In this document, you learn how to use the Ambari Web UI included with HDInsight clusters.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/08/2017
ms.author: larryfr
ms.openlocfilehash: 6c0bee83da0164777e9152c54009e4c8d6baacbb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553998"
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="b1836-104">Manage HDInsight clusters by using the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="b1836-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="b1836-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span><span class="sxs-lookup"><span data-stu-id="b1836-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="b1836-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span><span class="sxs-lookup"><span data-stu-id="b1836-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="b1836-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <a id="whatis"></a><span data-ttu-id="b1836-108">What is Ambari?</span><span class="sxs-lookup"><span data-stu-id="b1836-108">What is Ambari?</span></span>

<span data-ttu-id="b1836-109">[Apache Ambari](http://ambari.apache.org) makes Hadoop management simpler by providing an easy-to-use web UI that can be used to provision, manage, and monitor Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="b1836-109">[Apache Ambari](http://ambari.apache.org) makes Hadoop management simpler by providing an easy-to-use web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="b1836-110">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="b1836-110">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="b1836-111">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="b1836-111">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1836-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="b1836-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b1836-113">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="b1836-113">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="b1836-114">Connectivity</span><span class="sxs-lookup"><span data-stu-id="b1836-114">Connectivity</span></span>

<span data-ttu-id="b1836-115">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-115">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1836-116">Connecting to Ambari on HDInsight requires HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b1836-116">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="b1836-117">You must also authenticate to Ambari using the admin account name (the default is **admin**,) and password you provided when the cluster was created.</span><span class="sxs-lookup"><span data-stu-id="b1836-117">You must also authenticate to Ambari using the admin account name (the default is **admin**,) and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="b1836-118">SSH tunnel (proxy)</span><span class="sxs-lookup"><span data-stu-id="b1836-118">SSH tunnel (proxy)</span></span>

> [!NOTE]
> <span data-ttu-id="b1836-119">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker,) are not exposed on the internet.</span><span class="sxs-lookup"><span data-stu-id="b1836-119">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker,) are not exposed on the internet.</span></span> <span data-ttu-id="b1836-120">So you receive "server not found" errors when trying to access these features unless you use a Secure Shell (SSH) tunnel to proxy web traffic to the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="b1836-120">So you receive "server not found" errors when trying to access these features unless you use a Secure Shell (SSH) tunnel to proxy web traffic to the cluster head node.</span></span>

<span data-ttu-id="b1836-121">For information on creating an SSH tunnel to work with Ambari, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="b1836-121">For information on creating an SSH tunnel to work with Ambari, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="b1836-122">Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="b1836-122">Ambari Web UI</span></span>

<span data-ttu-id="b1836-123">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span><span class="sxs-lookup"><span data-stu-id="b1836-123">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="b1836-124">Use the cluster admin user (default Admin,) and password you used during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="b1836-124">Use the cluster admin user (default Admin,) and password you used during cluster creation.</span></span>

<span data-ttu-id="b1836-125">When the page opens, note the bar at the top.</span><span class="sxs-lookup"><span data-stu-id="b1836-125">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="b1836-126">This contains the following information and controls:</span><span class="sxs-lookup"><span data-stu-id="b1836-126">This contains the following information and controls:</span></span>

![ambari-nav](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="b1836-128">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-128">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="b1836-129">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span><span class="sxs-lookup"><span data-stu-id="b1836-129">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="b1836-130">Selecting the cluster name or **# ops** displays a list of background operations.</span><span class="sxs-lookup"><span data-stu-id="b1836-130">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="b1836-131">**# alerts** - Warnings or critical alerts, if any, for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-131">**# alerts** - Warnings or critical alerts, if any, for the cluster.</span></span> <span data-ttu-id="b1836-132">Selecting this displays a list of alerts.</span><span class="sxs-lookup"><span data-stu-id="b1836-132">Selecting this displays a list of alerts.</span></span>

* <span data-ttu-id="b1836-133">**Dashboard** - Displays the dashboard.</span><span class="sxs-lookup"><span data-stu-id="b1836-133">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="b1836-134">**Services** - Information and configuration settings for the services in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-134">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="b1836-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="b1836-136">**Alerts** - A log of information, warnings, and critical alerts.</span><span class="sxs-lookup"><span data-stu-id="b1836-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="b1836-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span><span class="sxs-lookup"><span data-stu-id="b1836-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="b1836-138">**Admin button** - Ambari management, user settings, and logout.</span><span class="sxs-lookup"><span data-stu-id="b1836-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="b1836-139">Monitoring</span><span class="sxs-lookup"><span data-stu-id="b1836-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="b1836-140">Alerts</span><span class="sxs-lookup"><span data-stu-id="b1836-140">Alerts</span></span>

<span data-ttu-id="b1836-141">Ambari provides many alerts, which have one of the following as the status:</span><span class="sxs-lookup"><span data-stu-id="b1836-141">Ambari provides many alerts, which have one of the following as the status:</span></span>

* <span data-ttu-id="b1836-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="b1836-142">**OK**</span></span>
* <span data-ttu-id="b1836-143">**Warning**</span><span class="sxs-lookup"><span data-stu-id="b1836-143">**Warning**</span></span>
* <span data-ttu-id="b1836-144">**CRITICAL**</span><span class="sxs-lookup"><span data-stu-id="b1836-144">**CRITICAL**</span></span>
* <span data-ttu-id="b1836-145">**UNKNOWN**</span><span class="sxs-lookup"><span data-stu-id="b1836-145">**UNKNOWN**</span></span>

<span data-ttu-id="b1836-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span><span class="sxs-lookup"><span data-stu-id="b1836-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="b1836-147">Selecting this entry displays the alerts and their status.</span><span class="sxs-lookup"><span data-stu-id="b1836-147">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="b1836-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span><span class="sxs-lookup"><span data-stu-id="b1836-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![alerts page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="b1836-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span><span class="sxs-lookup"><span data-stu-id="b1836-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span> <span data-ttu-id="b1836-151">This allows you to modify existing groups, or create new groups.</span><span class="sxs-lookup"><span data-stu-id="b1836-151">This allows you to modify existing groups, or create new groups.</span></span>

![manage alert groups dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="b1836-153">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span><span class="sxs-lookup"><span data-stu-id="b1836-153">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="b1836-154">This displays any current notifications, and allows you to create new notifications.</span><span class="sxs-lookup"><span data-stu-id="b1836-154">This displays any current notifications, and allows you to create new notifications.</span></span> <span data-ttu-id="b1836-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span><span class="sxs-lookup"><span data-stu-id="b1836-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="b1836-156">For example, you can send an alert when any of the alerts in the **YARN Default** group is set to **Critical**.</span><span class="sxs-lookup"><span data-stu-id="b1836-156">For example, you can send an alert when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![Create alert dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="b1836-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you tos et the number of times an alert must occur before a notification is sent.</span><span class="sxs-lookup"><span data-stu-id="b1836-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you tos et the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="b1836-159">This can be used to prevent notifications for transient errors, such as when a service fails on one head node and restarts on the other head node.</span><span class="sxs-lookup"><span data-stu-id="b1836-159">This can be used to prevent notifications for transient errors, such as when a service fails on one head node and restarts on the other head node.</span></span>

### <a name="cluster"></a><span data-ttu-id="b1836-160">Cluster</span><span class="sxs-lookup"><span data-stu-id="b1836-160">Cluster</span></span>

<span data-ttu-id="b1836-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span><span class="sxs-lookup"><span data-stu-id="b1836-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="b1836-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span><span class="sxs-lookup"><span data-stu-id="b1836-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![dashboard with metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="b1836-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span><span class="sxs-lookup"><span data-stu-id="b1836-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![dashboard with heatmaps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="b1836-166">For more detailed information on the nodes within the cluster, select **Hosts**, and then select the specific node you are interested in.</span><span class="sxs-lookup"><span data-stu-id="b1836-166">For more detailed information on the nodes within the cluster, select **Hosts**, and then select the specific node you are interested in.</span></span>

![host details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="b1836-168">Services</span><span class="sxs-lookup"><span data-stu-id="b1836-168">Services</span></span>

<span data-ttu-id="b1836-169">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-169">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="b1836-170">Various icons are used to indicate status or actions that should be taken, such as a yellow recycle symbol if a service needs to be recycled.</span><span class="sxs-lookup"><span data-stu-id="b1836-170">Various icons are used to indicate status or actions that should be taken, such as a yellow recycle symbol if a service needs to be recycled.</span></span>

![services side-bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="b1836-172">The services displayed differ between HDInsight cluster types and versions.</span><span class="sxs-lookup"><span data-stu-id="b1836-172">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="b1836-173">The services displayed here may be different than the services displayed for your cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-173">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="b1836-174">Selecting a service displays more detailed information on the service.</span><span class="sxs-lookup"><span data-stu-id="b1836-174">Selecting a service displays more detailed information on the service.</span></span>

![service summary information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="b1836-176">Quick links</span><span class="sxs-lookup"><span data-stu-id="b1836-176">Quick links</span></span>

<span data-ttu-id="b1836-177">Some services display a **Quick Links** link at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="b1836-177">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="b1836-178">This can be used to access service-specific web UIs, such as:</span><span class="sxs-lookup"><span data-stu-id="b1836-178">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="b1836-179">**Job History** - MapReduce job history.</span><span class="sxs-lookup"><span data-stu-id="b1836-179">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="b1836-180">**Resource Manager** - YARN ResourceManager UI.</span><span class="sxs-lookup"><span data-stu-id="b1836-180">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="b1836-181">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span><span class="sxs-lookup"><span data-stu-id="b1836-181">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="b1836-182">**Oozie Web UI** - Oozie UI.</span><span class="sxs-lookup"><span data-stu-id="b1836-182">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="b1836-183">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span><span class="sxs-lookup"><span data-stu-id="b1836-183">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="b1836-184">Selecting a **Quick Links** link for any service results in a "server not found" error unless you are using a Secure Sockets Layer (SSL) tunnel to proxy web traffic to the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-184">Selecting a **Quick Links** link for any service results in a "server not found" error unless you are using a Secure Sockets Layer (SSL) tunnel to proxy web traffic to the cluster.</span></span> <span data-ttu-id="b1836-185">This is because the web applications used to display this information are not exposed on the internet.</span><span class="sxs-lookup"><span data-stu-id="b1836-185">This is because the web applications used to display this information are not exposed on the internet.</span></span>
>
> <span data-ttu-id="b1836-186">For information on using an SSL tunnel with HDInsight, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="b1836-186">For information on using an SSL tunnel with HDInsight, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="b1836-187">Management</span><span class="sxs-lookup"><span data-stu-id="b1836-187">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="b1836-188">Ambari users, groups, and permissions</span><span class="sxs-lookup"><span data-stu-id="b1836-188">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="b1836-189">Working with users, groups, and permissions is supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-189">Working with users, groups, and permissions is supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="b1836-190">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1836-190">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="b1836-191">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-191">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b1836-192">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-192">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="b1836-193">Hosts</span><span class="sxs-lookup"><span data-stu-id="b1836-193">Hosts</span></span>

<span data-ttu-id="b1836-194">The **Hosts** page lists all hosts in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-194">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="b1836-195">To manage hosts, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="b1836-195">To manage hosts, follow these steps.</span></span>

![hosts page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="b1836-197">Adding, decommissioning or recommissioning a host should not be used with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="b1836-197">Adding, decommissioning or recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="b1836-198">Select the host(s) that you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="b1836-198">Select the host(s) that you wish to manage.</span></span>

2. <span data-ttu-id="b1836-199">Use the **Actions** menu to select the action that you wish to perform:</span><span class="sxs-lookup"><span data-stu-id="b1836-199">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="b1836-200">**Start all components** - Start all components on the host.</span><span class="sxs-lookup"><span data-stu-id="b1836-200">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="b1836-201">**Stop all components** - Stop all components on the host.</span><span class="sxs-lookup"><span data-stu-id="b1836-201">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="b1836-202">**Restart all components** - Stop and start all components on the host.</span><span class="sxs-lookup"><span data-stu-id="b1836-202">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="b1836-203">**Turn on maintenance mode** - Suppresses alerts for the host.</span><span class="sxs-lookup"><span data-stu-id="b1836-203">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="b1836-204">This should be enabled if you are performing actions that generate alerts, such as restarting a service that running services rely on.</span><span class="sxs-lookup"><span data-stu-id="b1836-204">This should be enabled if you are performing actions that generate alerts, such as restarting a service that running services rely on.</span></span>

   * <span data-ttu-id="b1836-205">**Turn off maintenance mode** - Returns the host to normal alerting.</span><span class="sxs-lookup"><span data-stu-id="b1836-205">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="b1836-206">**Stop** - Stops DataNode or NodeManagers on the host.</span><span class="sxs-lookup"><span data-stu-id="b1836-206">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="b1836-207">**Start** - Starts DataNode or NodeManagers on the host.</span><span class="sxs-lookup"><span data-stu-id="b1836-207">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="b1836-208">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span><span class="sxs-lookup"><span data-stu-id="b1836-208">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="b1836-209">**Decommission** - Removes a host from the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-209">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b1836-210">Do not use this action on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="b1836-210">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="b1836-211">**Recommission** - Adds a previously decommissioned host to the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-211">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b1836-212">Do not use this action on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="b1836-212">Do not use this action on HDInsight clusters.</span></span>

### <a id="service"></a><span data-ttu-id="b1836-213">Services</span><span class="sxs-lookup"><span data-stu-id="b1836-213">Services</span></span>

<span data-ttu-id="b1836-214">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span><span class="sxs-lookup"><span data-stu-id="b1836-214">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![service actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="b1836-216">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b1836-216">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="b1836-217">New services should be added using a Script Action during cluster provisioning.</span><span class="sxs-lookup"><span data-stu-id="b1836-217">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="b1836-218">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b1836-218">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="b1836-219">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span><span class="sxs-lookup"><span data-stu-id="b1836-219">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="b1836-220">Use the following steps to perform actions on an individual service:</span><span class="sxs-lookup"><span data-stu-id="b1836-220">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="b1836-221">From the **Dashboard** or **Services** page, select a service.</span><span class="sxs-lookup"><span data-stu-id="b1836-221">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="b1836-222">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span><span class="sxs-lookup"><span data-stu-id="b1836-222">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="b1836-223">This restarts the service on all nodes.</span><span class="sxs-lookup"><span data-stu-id="b1836-223">This restarts the service on all nodes.</span></span>

    ![service action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="b1836-225">Restarting some services while the cluster is running may generate alerts.</span><span class="sxs-lookup"><span data-stu-id="b1836-225">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="b1836-226">To avoid this, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span><span class="sxs-lookup"><span data-stu-id="b1836-226">To avoid this, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="b1836-227">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span><span class="sxs-lookup"><span data-stu-id="b1836-227">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="b1836-228">If configured to display, the list of background operations is displayed.</span><span class="sxs-lookup"><span data-stu-id="b1836-228">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b1836-229">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span><span class="sxs-lookup"><span data-stu-id="b1836-229">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="b1836-230">To configure a service, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="b1836-230">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="b1836-231">From the **Dashboard** or **Services** page, select a service.</span><span class="sxs-lookup"><span data-stu-id="b1836-231">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="b1836-232">Select the **Configs** tab. The current configuration is displayed.</span><span class="sxs-lookup"><span data-stu-id="b1836-232">Select the **Configs** tab. The current configuration is displayed.</span></span> <span data-ttu-id="b1836-233">A list of previous configurations is also displayed.</span><span class="sxs-lookup"><span data-stu-id="b1836-233">A list of previous configurations is also displayed.</span></span>

    ![configurations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="b1836-235">Use the fields displayed to modify the configuration, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="b1836-235">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="b1836-236">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span><span class="sxs-lookup"><span data-stu-id="b1836-236">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="b1836-237">Ambari views</span><span class="sxs-lookup"><span data-stu-id="b1836-237">Ambari views</span></span>

<span data-ttu-id="b1836-238">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="b1836-238">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="b1836-239">HDInsight provides the following views with Hadoop cluster types:</span><span class="sxs-lookup"><span data-stu-id="b1836-239">HDInsight provides the following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="b1836-240">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span><span class="sxs-lookup"><span data-stu-id="b1836-240">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="b1836-241">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span><span class="sxs-lookup"><span data-stu-id="b1836-241">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="b1836-242">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span><span class="sxs-lookup"><span data-stu-id="b1836-242">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="b1836-243">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="b1836-243">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="b1836-244">Tez View: The Tez View allows you to better understand and optimize jobs by viewing information on how Tez jobs are executed and what resources are used by the job.</span><span class="sxs-lookup"><span data-stu-id="b1836-244">Tez View: The Tez View allows you to better understand and optimize jobs by viewing information on how Tez jobs are executed and what resources are used by the job.</span></span>













