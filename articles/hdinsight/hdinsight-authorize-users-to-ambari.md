---
title: Authorize users for Ambari Views - Azure HDInsight
description: How to manage Ambari user and group permissions for domain-joined HDInsight clusters.
services: hdinsight
author: maxluk
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 09/26/2017
ms.author: maxluk
ms.openlocfilehash: 5c7e436854b93bc2cd0619c3d7942a0cca451a57
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966649"
---
# <a name="authorize-users-for-ambari-views"></a><span data-ttu-id="98bec-103">Authorize users for Ambari Views</span><span class="sxs-lookup"><span data-stu-id="98bec-103">Authorize users for Ambari Views</span></span>

<span data-ttu-id="98bec-104">[Domain-joined HDInsight clusters](./domain-joined/apache-domain-joined-introduction.md) provide enterprise-grade capabilities, including Azure Active Directory-based authentication.</span><span class="sxs-lookup"><span data-stu-id="98bec-104">[Domain-joined HDInsight clusters](./domain-joined/apache-domain-joined-introduction.md) provide enterprise-grade capabilities, including Azure Active Directory-based authentication.</span></span> <span data-ttu-id="98bec-105">You can [synchronize new users](hdinsight-sync-aad-users-to-cluster.md) added to Azure AD groups that have been provided access to the cluster, allowing those specific users to perform certain actions.</span><span class="sxs-lookup"><span data-stu-id="98bec-105">You can [synchronize new users](hdinsight-sync-aad-users-to-cluster.md) added to Azure AD groups that have been provided access to the cluster, allowing those specific users to perform certain actions.</span></span> <span data-ttu-id="98bec-106">Working with users, groups, and permissions in Ambari is supported for both domain-joined HDInsight cluster and standard HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="98bec-106">Working with users, groups, and permissions in Ambari is supported for both domain-joined HDInsight cluster and standard HDInsight cluster.</span></span>

<span data-ttu-id="98bec-107">Active Directory users can log on to the cluster nodes using their domain credentials.</span><span class="sxs-lookup"><span data-stu-id="98bec-107">Active Directory users can log on to the cluster nodes using their domain credentials.</span></span> <span data-ttu-id="98bec-108">They can also use their domain credentials to authenticate cluster interactions with other approved endpoints like Hue, Ambari Views, ODBC, JDBC, PowerShell, and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="98bec-108">They can also use their domain credentials to authenticate cluster interactions with other approved endpoints like Hue, Ambari Views, ODBC, JDBC, PowerShell, and REST APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="98bec-109">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="98bec-109">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="98bec-110">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span><span class="sxs-lookup"><span data-stu-id="98bec-110">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

<span data-ttu-id="98bec-111">If you have not already done so, follow [these instructions](./domain-joined/apache-domain-joined-configure.md) to provision a new domain-joined cluster.</span><span class="sxs-lookup"><span data-stu-id="98bec-111">If you have not already done so, follow [these instructions](./domain-joined/apache-domain-joined-configure.md) to provision a new domain-joined cluster.</span></span>

## <a name="access-the-ambari-management-page"></a><span data-ttu-id="98bec-112">Access the Ambari management page</span><span class="sxs-lookup"><span data-stu-id="98bec-112">Access the Ambari management page</span></span>

<span data-ttu-id="98bec-113">To get to the **Ambari management page** on the [Ambari Web UI](hdinsight-hadoop-manage-ambari.md), browse to **`https://<YOUR CLUSTER NAME>.azurehdinsight.net`**.</span><span class="sxs-lookup"><span data-stu-id="98bec-113">To get to the **Ambari management page** on the [Ambari Web UI](hdinsight-hadoop-manage-ambari.md), browse to **`https://<YOUR CLUSTER NAME>.azurehdinsight.net`**.</span></span> <span data-ttu-id="98bec-114">Enter the cluster administrator username and password that you defined when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="98bec-114">Enter the cluster administrator username and password that you defined when creating the cluster.</span></span> <span data-ttu-id="98bec-115">Next, from the Ambari dashboard, select **Manage Ambari** underneath the **admin** menu:</span><span class="sxs-lookup"><span data-stu-id="98bec-115">Next, from the Ambari dashboard, select **Manage Ambari** underneath the **admin** menu:</span></span>

![Manage Ambari](./media/hdinsight-authorize-users-to-ambari/manage-ambari.png)

## <a name="grant-permissions-to-hive-views"></a><span data-ttu-id="98bec-117">Grant permissions to Hive views</span><span class="sxs-lookup"><span data-stu-id="98bec-117">Grant permissions to Hive views</span></span>

<span data-ttu-id="98bec-118">Ambari comes with view instances for Hive and Tez, among others.</span><span class="sxs-lookup"><span data-stu-id="98bec-118">Ambari comes with view instances for Hive and Tez, among others.</span></span> <span data-ttu-id="98bec-119">To grant access to one or more Hive view instances, go to the **Ambari management page**.</span><span class="sxs-lookup"><span data-stu-id="98bec-119">To grant access to one or more Hive view instances, go to the **Ambari management page**.</span></span>

1. <span data-ttu-id="98bec-120">From the management page, select the **Views** link under the **Views** menu heading on the left.</span><span class="sxs-lookup"><span data-stu-id="98bec-120">From the management page, select the **Views** link under the **Views** menu heading on the left.</span></span>

    ![Views link](./media/hdinsight-authorize-users-to-ambari/views-link.png)

2. <span data-ttu-id="98bec-122">On the Views page, expand the **HIVE** row.</span><span class="sxs-lookup"><span data-stu-id="98bec-122">On the Views page, expand the **HIVE** row.</span></span> <span data-ttu-id="98bec-123">There is one default Hive view that is created when the Hive service is added to the cluster.</span><span class="sxs-lookup"><span data-stu-id="98bec-123">There is one default Hive view that is created when the Hive service is added to the cluster.</span></span> <span data-ttu-id="98bec-124">You can also create more Hive view instances as needed.</span><span class="sxs-lookup"><span data-stu-id="98bec-124">You can also create more Hive view instances as needed.</span></span> <span data-ttu-id="98bec-125">Select a Hive view:</span><span class="sxs-lookup"><span data-stu-id="98bec-125">Select a Hive view:</span></span>

    ![Views - Hive view](./media/hdinsight-authorize-users-to-ambari/views-hive-view.png)

3. <span data-ttu-id="98bec-127">Scroll toward the bottom of the View page.</span><span class="sxs-lookup"><span data-stu-id="98bec-127">Scroll toward the bottom of the View page.</span></span> <span data-ttu-id="98bec-128">Under the *Permissions* section, you have two options for granting domain users their permissions to the view:</span><span class="sxs-lookup"><span data-stu-id="98bec-128">Under the *Permissions* section, you have two options for granting domain users their permissions to the view:</span></span>

<span data-ttu-id="98bec-129">**Grant permission to these users** ![Grant permission to these users](./media/hdinsight-authorize-users-to-ambari/add-user-to-view.png)</span><span class="sxs-lookup"><span data-stu-id="98bec-129">**Grant permission to these users** ![Grant permission to these users](./media/hdinsight-authorize-users-to-ambari/add-user-to-view.png)</span></span>

<span data-ttu-id="98bec-130">**Grant permission to these groups** ![Grant permission to these groups](./media/hdinsight-authorize-users-to-ambari/add-group-to-view.png)</span><span class="sxs-lookup"><span data-stu-id="98bec-130">**Grant permission to these groups** ![Grant permission to these groups](./media/hdinsight-authorize-users-to-ambari/add-group-to-view.png)</span></span>

4. <span data-ttu-id="98bec-131">To add a user, select the **Add User** button.</span><span class="sxs-lookup"><span data-stu-id="98bec-131">To add a user, select the **Add User** button.</span></span>

    * <span data-ttu-id="98bec-132">Start typing the user name and you will see a dropdown list of previously defined names.</span><span class="sxs-lookup"><span data-stu-id="98bec-132">Start typing the user name and you will see a dropdown list of previously defined names.</span></span>

    ![User autocompletes](./media/hdinsight-authorize-users-to-ambari/user-autocomplete.png)

    * <span data-ttu-id="98bec-134">Select, or finish typing, the user name.</span><span class="sxs-lookup"><span data-stu-id="98bec-134">Select, or finish typing, the user name.</span></span> <span data-ttu-id="98bec-135">To add this user name as a new user, select the **New** button.</span><span class="sxs-lookup"><span data-stu-id="98bec-135">To add this user name as a new user, select the **New** button.</span></span>

    * <span data-ttu-id="98bec-136">To save your changes, select the **blue checkbox**.</span><span class="sxs-lookup"><span data-stu-id="98bec-136">To save your changes, select the **blue checkbox**.</span></span>

    ![User entered](./media/hdinsight-authorize-users-to-ambari/user-entered.png)

5. <span data-ttu-id="98bec-138">To add a group, select the **Add Group** button.</span><span class="sxs-lookup"><span data-stu-id="98bec-138">To add a group, select the **Add Group** button.</span></span>

    * <span data-ttu-id="98bec-139">Start typing the group name.</span><span class="sxs-lookup"><span data-stu-id="98bec-139">Start typing the group name.</span></span> <span data-ttu-id="98bec-140">The process of selecting an existing group name, or adding a new group, is the same as for adding users.</span><span class="sxs-lookup"><span data-stu-id="98bec-140">The process of selecting an existing group name, or adding a new group, is the same as for adding users.</span></span>
    * <span data-ttu-id="98bec-141">To save your changes, select the **blue checkbox**.</span><span class="sxs-lookup"><span data-stu-id="98bec-141">To save your changes, select the **blue checkbox**.</span></span>

    ![Group entered](./media/hdinsight-authorize-users-to-ambari/group-entered.png)

<span data-ttu-id="98bec-143">Adding users directly to a view is useful when you want to assign permissions to a user to use that view, but do not want them to be a member of a group that has additional permissions.</span><span class="sxs-lookup"><span data-stu-id="98bec-143">Adding users directly to a view is useful when you want to assign permissions to a user to use that view, but do not want them to be a member of a group that has additional permissions.</span></span> <span data-ttu-id="98bec-144">To reduce the amount of administrative overhead, it may be simpler to assign permissions to groups.</span><span class="sxs-lookup"><span data-stu-id="98bec-144">To reduce the amount of administrative overhead, it may be simpler to assign permissions to groups.</span></span>

## <a name="grant-permissions-to-tez-views"></a><span data-ttu-id="98bec-145">Grant permissions to Tez views</span><span class="sxs-lookup"><span data-stu-id="98bec-145">Grant permissions to Tez views</span></span>

<span data-ttu-id="98bec-146">The Tez view instances allow the users to monitor and debug all Tez jobs, submitted by Hive queries and Pig scripts.</span><span class="sxs-lookup"><span data-stu-id="98bec-146">The Tez view instances allow the users to monitor and debug all Tez jobs, submitted by Hive queries and Pig scripts.</span></span> <span data-ttu-id="98bec-147">There is one default Tez view instance that is created when the cluster is provisioned.</span><span class="sxs-lookup"><span data-stu-id="98bec-147">There is one default Tez view instance that is created when the cluster is provisioned.</span></span>

<span data-ttu-id="98bec-148">To assign users and groups to a Tez view instance, expand the **TEZ** row on the Views page, as described previously.</span><span class="sxs-lookup"><span data-stu-id="98bec-148">To assign users and groups to a Tez view instance, expand the **TEZ** row on the Views page, as described previously.</span></span>

![Views - Tez view](./media/hdinsight-authorize-users-to-ambari/views-tez-view.png)

<span data-ttu-id="98bec-150">To add users or groups, repeat steps 3 - 5 in the previous section.</span><span class="sxs-lookup"><span data-stu-id="98bec-150">To add users or groups, repeat steps 3 - 5 in the previous section.</span></span>

## <a name="assign-users-to-roles"></a><span data-ttu-id="98bec-151">Assign users to roles</span><span class="sxs-lookup"><span data-stu-id="98bec-151">Assign users to roles</span></span>

<span data-ttu-id="98bec-152">There are five security roles for users and groups, listed in order of decreasing access permissions:</span><span class="sxs-lookup"><span data-stu-id="98bec-152">There are five security roles for users and groups, listed in order of decreasing access permissions:</span></span>

* <span data-ttu-id="98bec-153">Cluster Administrator</span><span class="sxs-lookup"><span data-stu-id="98bec-153">Cluster Administrator</span></span>
* <span data-ttu-id="98bec-154">Cluster Operator</span><span class="sxs-lookup"><span data-stu-id="98bec-154">Cluster Operator</span></span>
* <span data-ttu-id="98bec-155">Service Administrator</span><span class="sxs-lookup"><span data-stu-id="98bec-155">Service Administrator</span></span>
* <span data-ttu-id="98bec-156">Service Operator</span><span class="sxs-lookup"><span data-stu-id="98bec-156">Service Operator</span></span>
* <span data-ttu-id="98bec-157">Cluster User</span><span class="sxs-lookup"><span data-stu-id="98bec-157">Cluster User</span></span>

<span data-ttu-id="98bec-158">To manage roles, go to the **Ambari management page**, then select the **Roles** link within the *Clusters* menu group on the left.</span><span class="sxs-lookup"><span data-stu-id="98bec-158">To manage roles, go to the **Ambari management page**, then select the **Roles** link within the *Clusters* menu group on the left.</span></span>

![Roles menu link](./media/hdinsight-authorize-users-to-ambari/roles-link.png)

<span data-ttu-id="98bec-160">To see the list of permissions given to each role, click on the blue question mark next to the **Roles** table header on the Roles page.</span><span class="sxs-lookup"><span data-stu-id="98bec-160">To see the list of permissions given to each role, click on the blue question mark next to the **Roles** table header on the Roles page.</span></span>

![Roles menu link](./media/hdinsight-authorize-users-to-ambari/roles-permissions.png)

<span data-ttu-id="98bec-162">On this page, there are two different views you can use to manage roles for users and groups: Block and List.</span><span class="sxs-lookup"><span data-stu-id="98bec-162">On this page, there are two different views you can use to manage roles for users and groups: Block and List.</span></span>

### <a name="block-view"></a><span data-ttu-id="98bec-163">Block view</span><span class="sxs-lookup"><span data-stu-id="98bec-163">Block view</span></span>

<span data-ttu-id="98bec-164">The Block view displays each role in its own row, and provides the **Assign roles to these users** and **Assign roles to these groups** options as described previously.</span><span class="sxs-lookup"><span data-stu-id="98bec-164">The Block view displays each role in its own row, and provides the **Assign roles to these users** and **Assign roles to these groups** options as described previously.</span></span>

![Roles block view](./media/hdinsight-authorize-users-to-ambari/roles-block-view.png)

### <a name="list-view"></a><span data-ttu-id="98bec-166">List view</span><span class="sxs-lookup"><span data-stu-id="98bec-166">List view</span></span>

<span data-ttu-id="98bec-167">The List view provides quick editing capabilities in two categories: Users and Groups.</span><span class="sxs-lookup"><span data-stu-id="98bec-167">The List view provides quick editing capabilities in two categories: Users and Groups.</span></span>

* <span data-ttu-id="98bec-168">The Users category of the List view displays a list of all users, allowing you to select a role for each user in the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="98bec-168">The Users category of the List view displays a list of all users, allowing you to select a role for each user in the dropdown list.</span></span>

    ![Roles list view - users](./media/hdinsight-authorize-users-to-ambari/roles-list-view-users.png)

* <span data-ttu-id="98bec-170">The Groups category of the List view displays all groups, and the role assigned to each group.</span><span class="sxs-lookup"><span data-stu-id="98bec-170">The Groups category of the List view displays all groups, and the role assigned to each group.</span></span> <span data-ttu-id="98bec-171">In our example, the list of groups is synchronized from the Azure AD groups specified in the **Access user group** property of the cluster's Domain settings.</span><span class="sxs-lookup"><span data-stu-id="98bec-171">In our example, the list of groups is synchronized from the Azure AD groups specified in the **Access user group** property of the cluster's Domain settings.</span></span> <span data-ttu-id="98bec-172">See [Create a Domain-joined HDInsight cluster](./domain-joined/apache-domain-joined-configure-using-azure-adds.md#create-a-domain-joined-hdinsight-cluster).</span><span class="sxs-lookup"><span data-stu-id="98bec-172">See [Create a Domain-joined HDInsight cluster](./domain-joined/apache-domain-joined-configure-using-azure-adds.md#create-a-domain-joined-hdinsight-cluster).</span></span>

    ![Roles list view - groups](./media/hdinsight-authorize-users-to-ambari/roles-list-view-groups.png)

    <span data-ttu-id="98bec-174">In the image above, the "hiveusers" group is assigned the *Cluster User* role.</span><span class="sxs-lookup"><span data-stu-id="98bec-174">In the image above, the "hiveusers" group is assigned the *Cluster User* role.</span></span> <span data-ttu-id="98bec-175">This is a read-only role that allows the users of that group to view but not change service configurations and cluster metrics.</span><span class="sxs-lookup"><span data-stu-id="98bec-175">This is a read-only role that allows the users of that group to view but not change service configurations and cluster metrics.</span></span>

## <a name="log-in-to-ambari-as-a-view-only-user"></a><span data-ttu-id="98bec-176">Log in to Ambari as a view-only user</span><span class="sxs-lookup"><span data-stu-id="98bec-176">Log in to Ambari as a view-only user</span></span>

<span data-ttu-id="98bec-177">We have assigned our Azure AD domain user "hiveuser1" permissions to Hive and Tez views.</span><span class="sxs-lookup"><span data-stu-id="98bec-177">We have assigned our Azure AD domain user "hiveuser1" permissions to Hive and Tez views.</span></span> <span data-ttu-id="98bec-178">When we launch the Ambari Web UI and enter this user's domain credentials (Azure AD user name in e-mail format, and password), the user is redirected to the Ambari Views page.</span><span class="sxs-lookup"><span data-stu-id="98bec-178">When we launch the Ambari Web UI and enter this user's domain credentials (Azure AD user name in e-mail format, and password), the user is redirected to the Ambari Views page.</span></span> <span data-ttu-id="98bec-179">From here, the user can select any accessible view.</span><span class="sxs-lookup"><span data-stu-id="98bec-179">From here, the user can select any accessible view.</span></span> <span data-ttu-id="98bec-180">The user cannot visit any other part of the site, including the dashboard, services, hosts, alerts, or admin pages.</span><span class="sxs-lookup"><span data-stu-id="98bec-180">The user cannot visit any other part of the site, including the dashboard, services, hosts, alerts, or admin pages.</span></span>

![User with views only](./media/hdinsight-authorize-users-to-ambari/user-views-only.png)

## <a name="log-in-to-ambari-as-a-cluster-user"></a><span data-ttu-id="98bec-182">Log in to Ambari as a cluster user</span><span class="sxs-lookup"><span data-stu-id="98bec-182">Log in to Ambari as a cluster user</span></span>

<span data-ttu-id="98bec-183">We have assigned our Azure AD domain user "hiveuser2" to the *Cluster User* role.</span><span class="sxs-lookup"><span data-stu-id="98bec-183">We have assigned our Azure AD domain user "hiveuser2" to the *Cluster User* role.</span></span> <span data-ttu-id="98bec-184">This role is able to access the dashboard and all of the menu items.</span><span class="sxs-lookup"><span data-stu-id="98bec-184">This role is able to access the dashboard and all of the menu items.</span></span> <span data-ttu-id="98bec-185">A cluster user has fewer permitted options than an administrator.</span><span class="sxs-lookup"><span data-stu-id="98bec-185">A cluster user has fewer permitted options than an administrator.</span></span> <span data-ttu-id="98bec-186">For example, hiveuser2 can view configurations for each of the services, but cannot edit them.</span><span class="sxs-lookup"><span data-stu-id="98bec-186">For example, hiveuser2 can view configurations for each of the services, but cannot edit them.</span></span>

![User with Cluster User role](./media/hdinsight-authorize-users-to-ambari/user-cluster-user-role.png)

## <a name="next-steps"></a><span data-ttu-id="98bec-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="98bec-188">Next steps</span></span>

* [<span data-ttu-id="98bec-189">Configure Hive policies in Domain-joined HDInsight</span><span class="sxs-lookup"><span data-stu-id="98bec-189">Configure Hive policies in Domain-joined HDInsight</span></span>](./domain-joined/apache-domain-joined-run-hive.md)
* [<span data-ttu-id="98bec-190">Manage Domain-joined HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="98bec-190">Manage Domain-joined HDInsight clusters</span></span>](./domain-joined/apache-domain-joined-manage.md)
* [<span data-ttu-id="98bec-191">Use the Hive View with Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="98bec-191">Use the Hive View with Hadoop in HDInsight</span></span>](hadoop/apache-hadoop-use-hive-ambari-view.md)
* [<span data-ttu-id="98bec-192">Synchronize Azure AD users to the cluster</span><span class="sxs-lookup"><span data-stu-id="98bec-192">Synchronize Azure AD users to the cluster</span></span>](hdinsight-sync-aad-users-to-cluster.md)
