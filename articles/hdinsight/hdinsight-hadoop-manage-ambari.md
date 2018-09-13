---
title: Monitor and manage Azure HDInsight using Ambari Web UI
description: Learn how to use Ambari to monitor and manage Linux-based HDInsight clusters. In this document, you learn how to use the Ambari Web UI included with HDInsight clusters.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 03/23/2018
ms.author: jasonh
ms.openlocfilehash: 51507dde0d027723f7bcbe18b64f791ec49e1de7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784932"
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="559a7-104">Manage HDInsight clusters by using the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="559a7-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="559a7-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span><span class="sxs-lookup"><span data-stu-id="559a7-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="559a7-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span><span class="sxs-lookup"><span data-stu-id="559a7-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="559a7-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <a id="whatis"></a><span data-ttu-id="559a7-108">What is Ambari?</span><span class="sxs-lookup"><span data-stu-id="559a7-108">What is Ambari?</span></span>

<span data-ttu-id="559a7-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span><span class="sxs-lookup"><span data-stu-id="559a7-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="559a7-110">You can use Ambari to manage and monitor Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="559a7-110">You can use Ambari to manage and monitor Hadoop clusters.</span></span> <span data-ttu-id="559a7-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="559a7-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="559a7-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="559a7-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="559a7-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="559a7-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="559a7-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="559a7-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="559a7-115">Connectivity</span><span class="sxs-lookup"><span data-stu-id="559a7-115">Connectivity</span></span>

<span data-ttu-id="559a7-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="559a7-117">Connecting to Ambari on HDInsight requires HTTPS.</span><span class="sxs-lookup"><span data-stu-id="559a7-117">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="559a7-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span><span class="sxs-lookup"><span data-stu-id="559a7-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="559a7-119">SSH tunnel (proxy)</span><span class="sxs-lookup"><span data-stu-id="559a7-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="559a7-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span><span class="sxs-lookup"><span data-stu-id="559a7-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span></span> <span data-ttu-id="559a7-121">To access these services, you must create an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="559a7-121">To access these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="559a7-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="559a7-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="559a7-123">Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="559a7-123">Ambari Web UI</span></span>

> [!WARNING]
> <span data-ttu-id="559a7-124">Not all features of the Ambari Web UI are supported on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="559a7-124">Not all features of the Ambari Web UI are supported on HDInsight.</span></span> <span data-ttu-id="559a7-125">For more information, see the [Unsupported operations](#unsupported-operations) section of this document.</span><span class="sxs-lookup"><span data-stu-id="559a7-125">For more information, see the [Unsupported operations](#unsupported-operations) section of this document.</span></span>

<span data-ttu-id="559a7-126">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span><span class="sxs-lookup"><span data-stu-id="559a7-126">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="559a7-127">Use the cluster admin user (default Admin) and password you used during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="559a7-127">Use the cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="559a7-128">When the page opens, note the bar at the top.</span><span class="sxs-lookup"><span data-stu-id="559a7-128">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="559a7-129">This bar contains the following information and controls:</span><span class="sxs-lookup"><span data-stu-id="559a7-129">This bar contains the following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="559a7-131">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-131">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="559a7-132">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span><span class="sxs-lookup"><span data-stu-id="559a7-132">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="559a7-133">Selecting the cluster name or **# ops** displays a list of background operations.</span><span class="sxs-lookup"><span data-stu-id="559a7-133">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="559a7-134">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-134">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span></span>

* <span data-ttu-id="559a7-135">**Dashboard** - Displays the dashboard.</span><span class="sxs-lookup"><span data-stu-id="559a7-135">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="559a7-136">**Services** - Information and configuration settings for the services in the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-136">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="559a7-137">**Hosts** - Information and configuration settings for the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-137">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="559a7-138">**Alerts** - A log of information, warnings, and critical alerts.</span><span class="sxs-lookup"><span data-stu-id="559a7-138">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="559a7-139">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span><span class="sxs-lookup"><span data-stu-id="559a7-139">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="559a7-140">**Admin button** - Ambari management, user settings, and logout.</span><span class="sxs-lookup"><span data-stu-id="559a7-140">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="559a7-141">Monitoring</span><span class="sxs-lookup"><span data-stu-id="559a7-141">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="559a7-142">Alerts</span><span class="sxs-lookup"><span data-stu-id="559a7-142">Alerts</span></span>

<span data-ttu-id="559a7-143">The following list contains the common alert statuses used by Ambari:</span><span class="sxs-lookup"><span data-stu-id="559a7-143">The following list contains the common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="559a7-144">**OK**</span><span class="sxs-lookup"><span data-stu-id="559a7-144">**OK**</span></span>
* <span data-ttu-id="559a7-145">**Warning**</span><span class="sxs-lookup"><span data-stu-id="559a7-145">**Warning**</span></span>
* <span data-ttu-id="559a7-146">**CRITICAL**</span><span class="sxs-lookup"><span data-stu-id="559a7-146">**CRITICAL**</span></span>
* <span data-ttu-id="559a7-147">**UNKNOWN**</span><span class="sxs-lookup"><span data-stu-id="559a7-147">**UNKNOWN**</span></span>

<span data-ttu-id="559a7-148">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span><span class="sxs-lookup"><span data-stu-id="559a7-148">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="559a7-149">Selecting this entry displays the alerts and their status.</span><span class="sxs-lookup"><span data-stu-id="559a7-149">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="559a7-150">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span><span class="sxs-lookup"><span data-stu-id="559a7-150">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![alerts page](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="559a7-152">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span><span class="sxs-lookup"><span data-stu-id="559a7-152">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![manage alert groups dialog](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="559a7-154">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span><span class="sxs-lookup"><span data-stu-id="559a7-154">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="559a7-155">Any current notifications are displayed.</span><span class="sxs-lookup"><span data-stu-id="559a7-155">Any current notifications are displayed.</span></span> <span data-ttu-id="559a7-156">You can also create notifications from here.</span><span class="sxs-lookup"><span data-stu-id="559a7-156">You can also create notifications from here.</span></span> <span data-ttu-id="559a7-157">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span><span class="sxs-lookup"><span data-stu-id="559a7-157">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="559a7-158">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span><span class="sxs-lookup"><span data-stu-id="559a7-158">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![Create alert dialog](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="559a7-160">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span><span class="sxs-lookup"><span data-stu-id="559a7-160">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="559a7-161">This setting can be used to prevent notifications for transient errors.</span><span class="sxs-lookup"><span data-stu-id="559a7-161">This setting can be used to prevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="559a7-162">Cluster</span><span class="sxs-lookup"><span data-stu-id="559a7-162">Cluster</span></span>

<span data-ttu-id="559a7-163">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span><span class="sxs-lookup"><span data-stu-id="559a7-163">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="559a7-164">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span><span class="sxs-lookup"><span data-stu-id="559a7-164">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![dashboard with metrics](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="559a7-166">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span><span class="sxs-lookup"><span data-stu-id="559a7-166">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![dashboard with heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="559a7-168">For more information on the nodes within the cluster, select **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="559a7-168">For more information on the nodes within the cluster, select **Hosts**.</span></span> <span data-ttu-id="559a7-169">Then select the specific node you are interested in.</span><span class="sxs-lookup"><span data-stu-id="559a7-169">Then select the specific node you are interested in.</span></span>

![host details](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="559a7-171">Services</span><span class="sxs-lookup"><span data-stu-id="559a7-171">Services</span></span>

<span data-ttu-id="559a7-172">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-172">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="559a7-173">Various icons are used to indicate status or actions that should be taken.</span><span class="sxs-lookup"><span data-stu-id="559a7-173">Various icons are used to indicate status or actions that should be taken.</span></span> <span data-ttu-id="559a7-174">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span><span class="sxs-lookup"><span data-stu-id="559a7-174">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span></span>

![services side-bar](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="559a7-176">The services displayed differ between HDInsight cluster types and versions.</span><span class="sxs-lookup"><span data-stu-id="559a7-176">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="559a7-177">The services displayed here may be different than the services displayed for your cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-177">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="559a7-178">Selecting a service displays more detailed information on the service.</span><span class="sxs-lookup"><span data-stu-id="559a7-178">Selecting a service displays more detailed information on the service.</span></span>

![service summary information](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="559a7-180">Quick links</span><span class="sxs-lookup"><span data-stu-id="559a7-180">Quick links</span></span>

<span data-ttu-id="559a7-181">Some services display a **Quick Links** link at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="559a7-181">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="559a7-182">This can be used to access service-specific web UIs, such as:</span><span class="sxs-lookup"><span data-stu-id="559a7-182">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="559a7-183">**Job History** - MapReduce job history.</span><span class="sxs-lookup"><span data-stu-id="559a7-183">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="559a7-184">**Resource Manager** - YARN ResourceManager UI.</span><span class="sxs-lookup"><span data-stu-id="559a7-184">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="559a7-185">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span><span class="sxs-lookup"><span data-stu-id="559a7-185">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="559a7-186">**Oozie Web UI** - Oozie UI.</span><span class="sxs-lookup"><span data-stu-id="559a7-186">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="559a7-187">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span><span class="sxs-lookup"><span data-stu-id="559a7-187">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="559a7-188">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span><span class="sxs-lookup"><span data-stu-id="559a7-188">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="559a7-189">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span><span class="sxs-lookup"><span data-stu-id="559a7-189">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span></span> <span data-ttu-id="559a7-190">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="559a7-190">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="559a7-191">Management</span><span class="sxs-lookup"><span data-stu-id="559a7-191">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="559a7-192">Ambari users, groups, and permissions</span><span class="sxs-lookup"><span data-stu-id="559a7-192">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="559a7-193">Working with users, groups, and permissions are supported when using a [domain joined](./domain-joined/apache-domain-joined-introduction.md) HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-193">Working with users, groups, and permissions are supported when using a [domain joined](./domain-joined/apache-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="559a7-194">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](./domain-joined/apache-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="559a7-194">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](./domain-joined/apache-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="559a7-195">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-195">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="559a7-196">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-196">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="559a7-197">Hosts</span><span class="sxs-lookup"><span data-stu-id="559a7-197">Hosts</span></span>

<span data-ttu-id="559a7-198">The **Hosts** page lists all hosts in the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-198">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="559a7-199">To manage hosts, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="559a7-199">To manage hosts, follow these steps.</span></span>

![hosts page](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="559a7-201">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="559a7-201">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="559a7-202">Select the host that you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="559a7-202">Select the host that you wish to manage.</span></span>

2. <span data-ttu-id="559a7-203">Use the **Actions** menu to select the action that you wish to perform:</span><span class="sxs-lookup"><span data-stu-id="559a7-203">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="559a7-204">**Start all components** - Start all components on the host.</span><span class="sxs-lookup"><span data-stu-id="559a7-204">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="559a7-205">**Stop all components** - Stop all components on the host.</span><span class="sxs-lookup"><span data-stu-id="559a7-205">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="559a7-206">**Restart all components** - Stop and start all components on the host.</span><span class="sxs-lookup"><span data-stu-id="559a7-206">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="559a7-207">**Turn on maintenance mode** - Suppresses alerts for the host.</span><span class="sxs-lookup"><span data-stu-id="559a7-207">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="559a7-208">This mode should be enabled if you are performing actions that generate alerts.</span><span class="sxs-lookup"><span data-stu-id="559a7-208">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="559a7-209">For example, stopping and starting a service.</span><span class="sxs-lookup"><span data-stu-id="559a7-209">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="559a7-210">**Turn off maintenance mode** - Returns the host to normal alerting.</span><span class="sxs-lookup"><span data-stu-id="559a7-210">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="559a7-211">**Stop** - Stops DataNode or NodeManagers on the host.</span><span class="sxs-lookup"><span data-stu-id="559a7-211">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="559a7-212">**Start** - Starts DataNode or NodeManagers on the host.</span><span class="sxs-lookup"><span data-stu-id="559a7-212">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="559a7-213">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span><span class="sxs-lookup"><span data-stu-id="559a7-213">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="559a7-214">**Decommission** - Removes a host from the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-214">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="559a7-215">Do not use this action on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="559a7-215">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="559a7-216">**Recommission** - Adds a previously decommissioned host to the cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-216">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="559a7-217">Do not use this action on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="559a7-217">Do not use this action on HDInsight clusters.</span></span>

### <a id="service"></a><span data-ttu-id="559a7-218">Services</span><span class="sxs-lookup"><span data-stu-id="559a7-218">Services</span></span>

<span data-ttu-id="559a7-219">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span><span class="sxs-lookup"><span data-stu-id="559a7-219">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![service actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="559a7-221">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="559a7-221">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="559a7-222">New services should be added using a Script Action during cluster provisioning.</span><span class="sxs-lookup"><span data-stu-id="559a7-222">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="559a7-223">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="559a7-223">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="559a7-224">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span><span class="sxs-lookup"><span data-stu-id="559a7-224">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="559a7-225">Use the following steps to perform actions on an individual service:</span><span class="sxs-lookup"><span data-stu-id="559a7-225">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="559a7-226">From the **Dashboard** or **Services** page, select a service.</span><span class="sxs-lookup"><span data-stu-id="559a7-226">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="559a7-227">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span><span class="sxs-lookup"><span data-stu-id="559a7-227">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="559a7-228">This restarts the service on all nodes.</span><span class="sxs-lookup"><span data-stu-id="559a7-228">This restarts the service on all nodes.</span></span>

    ![service action](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="559a7-230">Restarting some services while the cluster is running may generate alerts.</span><span class="sxs-lookup"><span data-stu-id="559a7-230">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="559a7-231">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span><span class="sxs-lookup"><span data-stu-id="559a7-231">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="559a7-232">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span><span class="sxs-lookup"><span data-stu-id="559a7-232">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="559a7-233">If configured to display, the list of background operations is displayed.</span><span class="sxs-lookup"><span data-stu-id="559a7-233">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="559a7-234">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span><span class="sxs-lookup"><span data-stu-id="559a7-234">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="559a7-235">To configure a service, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="559a7-235">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="559a7-236">From the **Dashboard** or **Services** page, select a service.</span><span class="sxs-lookup"><span data-stu-id="559a7-236">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="559a7-237">Select the **Configs** tab. The current configuration is displayed.</span><span class="sxs-lookup"><span data-stu-id="559a7-237">Select the **Configs** tab. The current configuration is displayed.</span></span> <span data-ttu-id="559a7-238">A list of previous configurations is also displayed.</span><span class="sxs-lookup"><span data-stu-id="559a7-238">A list of previous configurations is also displayed.</span></span>

    ![configurations](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="559a7-240">Use the fields displayed to modify the configuration, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="559a7-240">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="559a7-241">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span><span class="sxs-lookup"><span data-stu-id="559a7-241">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="559a7-242">Ambari views</span><span class="sxs-lookup"><span data-stu-id="559a7-242">Ambari views</span></span>

<span data-ttu-id="559a7-243">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="559a7-243">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="559a7-244">HDInsight provides the following views with Hadoop cluster types:</span><span class="sxs-lookup"><span data-stu-id="559a7-244">HDInsight provides the following views with Hadoop cluster types:</span></span>


* <span data-ttu-id="559a7-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span><span class="sxs-lookup"><span data-stu-id="559a7-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="559a7-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span><span class="sxs-lookup"><span data-stu-id="559a7-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="559a7-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hadoop/apache-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="559a7-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hadoop/apache-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="559a7-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span><span class="sxs-lookup"><span data-stu-id="559a7-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span></span> <span data-ttu-id="559a7-249">You can view information on how Tez jobs are executed and what resources are used.</span><span class="sxs-lookup"><span data-stu-id="559a7-249">You can view information on how Tez jobs are executed and what resources are used.</span></span>

## <a name="unsupported-operations"></a><span data-ttu-id="559a7-250">Unsupported operations</span><span class="sxs-lookup"><span data-stu-id="559a7-250">Unsupported operations</span></span>

<span data-ttu-id="559a7-251">The following Ambari operations are not supported on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="559a7-251">The following Ambari operations are not supported on HDInsight:</span></span>

* <span data-ttu-id="559a7-252">__Moving the Metrics Collector service__.</span><span class="sxs-lookup"><span data-stu-id="559a7-252">__Moving the Metrics Collector service__.</span></span> <span data-ttu-id="559a7-253">When viewing information on the Metrics Collector service, one of the actions available from the Service Actions menu is __Move Metrics collector__.</span><span class="sxs-lookup"><span data-stu-id="559a7-253">When viewing information on the Metrics Collector service, one of the actions available from the Service Actions menu is __Move Metrics collector__.</span></span> <span data-ttu-id="559a7-254">This is not supported with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="559a7-254">This is not supported with HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="559a7-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="559a7-255">Next steps</span></span>

<span data-ttu-id="559a7-256">Learn how to use the [Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md) with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="559a7-256">Learn how to use the [Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md) with HDInsight.</span></span>
