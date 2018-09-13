---
title: Manage Domain-joined HDInsight clusters| Microsoft Docs
description: Learn how to manage Domain-joined HDInsight clusters
services: hdinsight
documentationcenter: ''
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: ''
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 6e765a95d136176d3ac62133d40ffc58c7d7a544
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549980"
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="e3f62-103">Manage Domain-joined HDInsight clusters (Preview)</span><span class="sxs-lookup"><span data-stu-id="e3f62-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="e3f62-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="e3f62-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="e3f62-105">Users of Domain-joined HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="e3f62-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="e3f62-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span><span class="sxs-lookup"><span data-stu-id="e3f62-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="e3f62-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span><span class="sxs-lookup"><span data-stu-id="e3f62-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="e3f62-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e3f62-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="e3f62-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span><span class="sxs-lookup"><span data-stu-id="e3f62-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="e3f62-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span><span class="sxs-lookup"><span data-stu-id="e3f62-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="e3f62-111">It has root privileges to the Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="e3f62-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="e3f62-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span><span class="sxs-lookup"><span data-stu-id="e3f62-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="e3f62-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span><span class="sxs-lookup"><span data-stu-id="e3f62-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="e3f62-114">It is not an active directory domain user.</span><span class="sxs-lookup"><span data-stu-id="e3f62-114">It is not an active directory domain user.</span></span> <span data-ttu-id="e3f62-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span><span class="sxs-lookup"><span data-stu-id="e3f62-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="e3f62-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span><span class="sxs-lookup"><span data-stu-id="e3f62-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="e3f62-117">The password can be updated from the Settings page in Ranger.</span><span class="sxs-lookup"><span data-stu-id="e3f62-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="e3f62-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span><span class="sxs-lookup"><span data-stu-id="e3f62-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="e3f62-119">You must provide this user’s credentials during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="e3f62-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="e3f62-120">This user has the following privileges:</span><span class="sxs-lookup"><span data-stu-id="e3f62-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="e3f62-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="e3f62-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="e3f62-122">Create service principals within the OU that you specify during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="e3f62-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="e3f62-123">Create reverse DNS entries.</span><span class="sxs-lookup"><span data-stu-id="e3f62-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="e3f62-124">Note the other AD users also have these privileges.</span><span class="sxs-lookup"><span data-stu-id="e3f62-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="e3f62-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span><span class="sxs-lookup"><span data-stu-id="e3f62-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="e3f62-126">These end points are locked down for all users except the cluster admin domain user.</span><span class="sxs-lookup"><span data-stu-id="e3f62-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="e3f62-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span><span class="sxs-lookup"><span data-stu-id="e3f62-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="e3f62-128">The users in these groups will be synced to Ranger and Ambari.</span><span class="sxs-lookup"><span data-stu-id="e3f62-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="e3f62-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="e3f62-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="e3f62-130">All the RBAC policies and auditing will be applicable to these users.</span><span class="sxs-lookup"><span data-stu-id="e3f62-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="e3f62-131">Roles of Domain-joined HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="e3f62-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="e3f62-132">Domain-joined HDInsight have the following roles:</span><span class="sxs-lookup"><span data-stu-id="e3f62-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="e3f62-133">Cluster Administrator</span><span class="sxs-lookup"><span data-stu-id="e3f62-133">Cluster Administrator</span></span>
* <span data-ttu-id="e3f62-134">Cluster Operator</span><span class="sxs-lookup"><span data-stu-id="e3f62-134">Cluster Operator</span></span>
* <span data-ttu-id="e3f62-135">Service Administrator</span><span class="sxs-lookup"><span data-stu-id="e3f62-135">Service Administrator</span></span>
* <span data-ttu-id="e3f62-136">Service Operator</span><span class="sxs-lookup"><span data-stu-id="e3f62-136">Service Operator</span></span>
* <span data-ttu-id="e3f62-137">Cluster User</span><span class="sxs-lookup"><span data-stu-id="e3f62-137">Cluster User</span></span>

<span data-ttu-id="e3f62-138">**To see the permissions of these roles**</span><span class="sxs-lookup"><span data-stu-id="e3f62-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="e3f62-139">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="e3f62-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="e3f62-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="e3f62-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="e3f62-141">From the left menu, click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="e3f62-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="e3f62-142">Click the blue question mark to see the permissions:</span><span class="sxs-lookup"><span data-stu-id="e3f62-142">Click the blue question mark to see the permissions:</span></span>

    ![Domain-joined HDInsight roles permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="e3f62-144">Open the Ambari Management UI</span><span class="sxs-lookup"><span data-stu-id="e3f62-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="e3f62-145">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3f62-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e3f62-146">Open your HDInsight cluster in a blade.</span><span class="sxs-lookup"><span data-stu-id="e3f62-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="e3f62-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="e3f62-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="e3f62-148">Click **Dashboard** from the top menu to open Ambari.</span><span class="sxs-lookup"><span data-stu-id="e3f62-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="e3f62-149">Log on to Ambari using the cluster administrator domain user name and password.</span><span class="sxs-lookup"><span data-stu-id="e3f62-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="e3f62-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span><span class="sxs-lookup"><span data-stu-id="e3f62-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![Domain-joined HDInsight manage Ambari](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="e3f62-152">The UI looks like:</span><span class="sxs-lookup"><span data-stu-id="e3f62-152">The UI looks like:</span></span>

    ![Domain-joined HDInsight Ambari management UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="e3f62-154">List the domain users synchronized from your Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3f62-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="e3f62-155">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="e3f62-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="e3f62-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="e3f62-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="e3f62-157">From the left menu, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e3f62-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="e3f62-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e3f62-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Domain-joined HDInsight Ambari management UI list users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="e3f62-160">List the domain groups synchronized from your Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3f62-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="e3f62-161">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="e3f62-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="e3f62-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="e3f62-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="e3f62-163">From the left menu, click **Groups**.</span><span class="sxs-lookup"><span data-stu-id="e3f62-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="e3f62-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e3f62-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Domain-joined HDInsight Ambari management UI list groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="e3f62-166">Configure Hive Views permissions</span><span class="sxs-lookup"><span data-stu-id="e3f62-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="e3f62-167">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="e3f62-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="e3f62-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="e3f62-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="e3f62-169">From the left menu, click **Views**.</span><span class="sxs-lookup"><span data-stu-id="e3f62-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="e3f62-170">Click **HIVE** to show the details.</span><span class="sxs-lookup"><span data-stu-id="e3f62-170">Click **HIVE** to show the details.</span></span>

    ![Domain-joined HDInsight Ambari management UI Hive Views](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="e3f62-172">Click the **Hive View** link to configure Hive Views.</span><span class="sxs-lookup"><span data-stu-id="e3f62-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="e3f62-173">Scroll down to the **Permissions** section.</span><span class="sxs-lookup"><span data-stu-id="e3f62-173">Scroll down to the **Permissions** section.</span></span>

    ![Domain-joined HDInsight Ambari management UI Hive Views configure permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="e3f62-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span><span class="sxs-lookup"><span data-stu-id="e3f62-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="e3f62-176">Configure users for the roles</span><span class="sxs-lookup"><span data-stu-id="e3f62-176">Configure users for the roles</span></span>
 <span data-ttu-id="e3f62-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="e3f62-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="e3f62-178">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="e3f62-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="e3f62-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="e3f62-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="e3f62-180">From the left menu, click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="e3f62-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="e3f62-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span><span class="sxs-lookup"><span data-stu-id="e3f62-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3f62-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3f62-182">Next steps</span></span>
* <span data-ttu-id="e3f62-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e3f62-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="e3f62-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e3f62-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="e3f62-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="e3f62-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>







