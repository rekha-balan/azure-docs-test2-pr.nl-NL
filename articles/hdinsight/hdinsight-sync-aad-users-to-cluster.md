---
title: Synchronize Azure Active Directory users to a cluster - Azure HDInsight
description: Synchronize authenticated users from Azure Active Directory to a cluster.
services: hdinsight
ms.service: hdinsight
author: ashishthaps
ms.author: ashishth
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 08/19/2018
ms.openlocfilehash: 7e002a43c774bd1a6df9cfe46207ddebd02284b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866677"
---
# <a name="synchronize-azure-active-directory-users-to-an-hdinsight-cluster"></a><span data-ttu-id="8fb03-103">Synchronize Azure Active Directory users to an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="8fb03-103">Synchronize Azure Active Directory users to an HDInsight cluster</span></span>

<span data-ttu-id="8fb03-104">[Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md) can use strong authentication with Azure Active Directory (Azure AD) users, as well as use *role-based access control* (RBAC) policies.</span><span class="sxs-lookup"><span data-stu-id="8fb03-104">[Domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md) can use strong authentication with Azure Active Directory (Azure AD) users, as well as use *role-based access control* (RBAC) policies.</span></span> <span data-ttu-id="8fb03-105">As you add  users and groups to Azure AD, you can synchronize the users who need access to your cluster.</span><span class="sxs-lookup"><span data-stu-id="8fb03-105">As you add  users and groups to Azure AD, you can synchronize the users who need access to your cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fb03-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8fb03-106">Prerequisites</span></span>

<span data-ttu-id="8fb03-107">If you have not already done so, [create a domain-joined HDInsight cluster](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8fb03-107">If you have not already done so, [create a domain-joined HDInsight cluster](hdinsight-domain-joined-configure.md).</span></span>

## <a name="add-new-azure-ad-users"></a><span data-ttu-id="8fb03-108">Add new Azure AD users</span><span class="sxs-lookup"><span data-stu-id="8fb03-108">Add new Azure AD users</span></span>

<span data-ttu-id="8fb03-109">To view your hosts, open the Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="8fb03-109">To view your hosts, open the Ambari Web UI.</span></span> <span data-ttu-id="8fb03-110">Each node will be updated with  new unattended upgrade settings.</span><span class="sxs-lookup"><span data-stu-id="8fb03-110">Each node will be updated with  new unattended upgrade settings.</span></span>

1. <span data-ttu-id="8fb03-111">In  the [Azure portal](https://portal.azure.com), navigate to the Azure AD directory associated with your domain-joined cluster.</span><span class="sxs-lookup"><span data-stu-id="8fb03-111">In  the [Azure portal](https://portal.azure.com), navigate to the Azure AD directory associated with your domain-joined cluster.</span></span>

2. <span data-ttu-id="8fb03-112">Select **All users** from the left-hand menu, then select **New user**.</span><span class="sxs-lookup"><span data-stu-id="8fb03-112">Select **All users** from the left-hand menu, then select **New user**.</span></span>

    ![All users pane](./media/hdinsight-sync-aad-users-to-cluster/aad-users.png)

3. <span data-ttu-id="8fb03-114">Complete the new user form.</span><span class="sxs-lookup"><span data-stu-id="8fb03-114">Complete the new user form.</span></span> <span data-ttu-id="8fb03-115">Select groups you created for assigning cluster-based permissions.</span><span class="sxs-lookup"><span data-stu-id="8fb03-115">Select groups you created for assigning cluster-based permissions.</span></span> <span data-ttu-id="8fb03-116">In this example, create a group named "HiveUsers", to which you can assign new users.</span><span class="sxs-lookup"><span data-stu-id="8fb03-116">In this example, create a group named "HiveUsers", to which you can assign new users.</span></span> <span data-ttu-id="8fb03-117">The [example instructions](hdinsight-domain-joined-configure.md) for creating a domain-joined cluster include adding two groups, `HiveUsers` and `AAD DC Administrators`.</span><span class="sxs-lookup"><span data-stu-id="8fb03-117">The [example instructions](hdinsight-domain-joined-configure.md) for creating a domain-joined cluster include adding two groups, `HiveUsers` and `AAD DC Administrators`.</span></span>

    ![New user pane](./media/hdinsight-sync-aad-users-to-cluster/aad-new-user.png)

4. <span data-ttu-id="8fb03-119">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="8fb03-119">Select **Create**.</span></span>

## <a name="use-the-ambari-rest-api-to-synchronize-users"></a><span data-ttu-id="8fb03-120">Use the Ambari REST API to synchronize users</span><span class="sxs-lookup"><span data-stu-id="8fb03-120">Use the Ambari REST API to synchronize users</span></span>

<span data-ttu-id="8fb03-121">User groups specified during the cluster creation process are synchronized at that time.</span><span class="sxs-lookup"><span data-stu-id="8fb03-121">User groups specified during the cluster creation process are synchronized at that time.</span></span> <span data-ttu-id="8fb03-122">User synchronization occurs automatically once every hour.</span><span class="sxs-lookup"><span data-stu-id="8fb03-122">User synchronization occurs automatically once every hour.</span></span> <span data-ttu-id="8fb03-123">To synchronize the users immediately, or to synchronize a group other than the groups specified during cluster creation, use the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="8fb03-123">To synchronize the users immediately, or to synchronize a group other than the groups specified during cluster creation, use the Ambari REST API.</span></span>

<span data-ttu-id="8fb03-124">The following method uses POST with the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="8fb03-124">The following method uses POST with the Ambari REST API.</span></span> <span data-ttu-id="8fb03-125">For more information, see [Manage HDInsight clusters by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="8fb03-125">For more information, see [Manage HDInsight clusters by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

1. <span data-ttu-id="8fb03-126">[Connect to your cluster with SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8fb03-126">[Connect to your cluster with SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="8fb03-127">From the overview pane for your cluster in the Azure portal, select the **Secure Shell (SSH)** button.</span><span class="sxs-lookup"><span data-stu-id="8fb03-127">From the overview pane for your cluster in the Azure portal, select the **Secure Shell (SSH)** button.</span></span>

    ![Secure Shell (SSH)](./media/hdinsight-sync-aad-users-to-cluster/ssh.png)

2. <span data-ttu-id="8fb03-129">Copy the displayed `ssh` command and paste it into your SSH client.</span><span class="sxs-lookup"><span data-stu-id="8fb03-129">Copy the displayed `ssh` command and paste it into your SSH client.</span></span> <span data-ttu-id="8fb03-130">Enter the ssh user password when prompted.</span><span class="sxs-lookup"><span data-stu-id="8fb03-130">Enter the ssh user password when prompted.</span></span>

3. <span data-ttu-id="8fb03-131">After authenticating, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="8fb03-131">After authenticating, enter the following command:</span></span>

    ```bash
    curl -u admin:<YOUR PASSWORD> -sS -H "X-Requested-By: ambari" \
    -X POST -d '{"Event": {"specs": [{"principal_type": "groups", "sync_type": "existing"}]}}' \
    "https://<YOUR CLUSTER NAME>.azurehdinsight.net/api/v1/ldap_sync_events"
    ```
    
    <span data-ttu-id="8fb03-132">The response should look like this:</span><span class="sxs-lookup"><span data-stu-id="8fb03-132">The response should look like this:</span></span>

    ```json
    {
      "resources" : [
        {
          "href" : "http://hn0-hadoop.<YOUR DOMAIN>.com:8080/api/v1/ldap_sync_events/1",
          "Event" : {
            "id" : 1
          }
        }
      ]
    }
    ```

4. <span data-ttu-id="8fb03-133">To see the synchronization status, execute a new `curl` command:</span><span class="sxs-lookup"><span data-stu-id="8fb03-133">To see the synchronization status, execute a new `curl` command:</span></span>

    ```bash
    curl -u admin:<YOUR PASSWORD> https://<YOUR CLUSTER NAME>.azurehdinsight.net/api/v1/ldap_sync_events/1
    ```
    
    <span data-ttu-id="8fb03-134">The response should look like this:</span><span class="sxs-lookup"><span data-stu-id="8fb03-134">The response should look like this:</span></span>
    
    ```json
    {
      "href" : "http://hn0-hadoop.YOURDOMAIN.com:8080/api/v1/ldap_sync_events/1",
      "Event" : {
        "id" : 1,
        "specs" : [
          {
            "sync_type" : "existing",
            "principal_type" : "groups"
          }
        ],
        "status" : "COMPLETE",
        "status_detail" : "Completed LDAP sync.",
        "summary" : {
          "groups" : {
            "created" : 0,
            "removed" : 0,
            "updated" : 0
          },
          "memberships" : {
            "created" : 1,
            "removed" : 0
          },
          "users" : {
            "created" : 1,
            "removed" : 0,
            "skipped" : 0,
            "updated" : 0
          }
        },
        "sync_time" : {
          "end" : 1497994072182,
          "start" : 1497994071100
        }
      }
    }
    ```

5. <span data-ttu-id="8fb03-135">This  result shows  that the status is **COMPLETE**,  one new user was created, and the user was assigned a membership.</span><span class="sxs-lookup"><span data-stu-id="8fb03-135">This  result shows  that the status is **COMPLETE**,  one new user was created, and the user was assigned a membership.</span></span> <span data-ttu-id="8fb03-136">In this example,  the user is assigned to the "HiveUsers" synchronized LDAP group, since the user was added to that same group in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fb03-136">In this example,  the user is assigned to the "HiveUsers" synchronized LDAP group, since the user was added to that same group in Azure AD.</span></span>

> [!NOTE]
> <span data-ttu-id="8fb03-137">The previous method only  synchronizes   the Azure AD groups specified in the **Access user group** property of the domain settings during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="8fb03-137">The previous method only  synchronizes   the Azure AD groups specified in the **Access user group** property of the domain settings during cluster creation.</span></span> <span data-ttu-id="8fb03-138">For more information, see  [create an HDInsight cluster](domain-joined/apache-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8fb03-138">For more information, see  [create an HDInsight cluster](domain-joined/apache-domain-joined-configure.md).</span></span>

## <a name="verify-the-newly-added-azure-ad-user"></a><span data-ttu-id="8fb03-139">Verify the newly added Azure AD user</span><span class="sxs-lookup"><span data-stu-id="8fb03-139">Verify the newly added Azure AD user</span></span>

<span data-ttu-id="8fb03-140">Open the [Ambari Web UI](hdinsight-hadoop-manage-ambari.md) to verify that the new Azure AD user was added.</span><span class="sxs-lookup"><span data-stu-id="8fb03-140">Open the [Ambari Web UI](hdinsight-hadoop-manage-ambari.md) to verify that the new Azure AD user was added.</span></span> <span data-ttu-id="8fb03-141">Access the Ambari Web UI by browsing to **`https://<YOUR CLUSTER NAME>.azurehdinsight.net`**.</span><span class="sxs-lookup"><span data-stu-id="8fb03-141">Access the Ambari Web UI by browsing to **`https://<YOUR CLUSTER NAME>.azurehdinsight.net`**.</span></span> <span data-ttu-id="8fb03-142">Enter the cluster administrator username and password.</span><span class="sxs-lookup"><span data-stu-id="8fb03-142">Enter the cluster administrator username and password.</span></span>

1. <span data-ttu-id="8fb03-143">From the Ambari dashboard, select **Manage Ambari** under the **admin** menu.</span><span class="sxs-lookup"><span data-stu-id="8fb03-143">From the Ambari dashboard, select **Manage Ambari** under the **admin** menu.</span></span>

    ![Manage Ambari](./media/hdinsight-sync-aad-users-to-cluster/manage-ambari.png)

2. <span data-ttu-id="8fb03-145">Select **Users** under the **User + Group Management** menu group on the left-hand side of the page.</span><span class="sxs-lookup"><span data-stu-id="8fb03-145">Select **Users** under the **User + Group Management** menu group on the left-hand side of the page.</span></span>

    ![Users menu item](./media/hdinsight-sync-aad-users-to-cluster/users-link.png)

3. <span data-ttu-id="8fb03-147">The new user should be listed within the Users table.</span><span class="sxs-lookup"><span data-stu-id="8fb03-147">The new user should be listed within the Users table.</span></span> <span data-ttu-id="8fb03-148">The Type is set to `LDAP` rather than  `Local`.</span><span class="sxs-lookup"><span data-stu-id="8fb03-148">The Type is set to `LDAP` rather than  `Local`.</span></span>

    ![Users page](./media/hdinsight-sync-aad-users-to-cluster/users.png)

## <a name="log-in-to-ambari-as-the-new-user"></a><span data-ttu-id="8fb03-150">Log in to Ambari as the new user</span><span class="sxs-lookup"><span data-stu-id="8fb03-150">Log in to Ambari as the new user</span></span>

<span data-ttu-id="8fb03-151">When the new user (or any other domain user) logs in to Ambari, they use their full Azure AD user name and  domain credentials.</span><span class="sxs-lookup"><span data-stu-id="8fb03-151">When the new user (or any other domain user) logs in to Ambari, they use their full Azure AD user name and  domain credentials.</span></span>  <span data-ttu-id="8fb03-152">Ambari displays a user  alias, which is the display name of the user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fb03-152">Ambari displays a user  alias, which is the display name of the user in Azure AD.</span></span> <span data-ttu-id="8fb03-153">The new example user has the user name `hiveuser3@contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8fb03-153">The new example user has the user name `hiveuser3@contoso.com`.</span></span> <span data-ttu-id="8fb03-154">In Ambari, this new user shows up as `hiveuser3` but the user logs into Ambari as `hiveuser3@contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8fb03-154">In Ambari, this new user shows up as `hiveuser3` but the user logs into Ambari as `hiveuser3@contoso.com`.</span></span>

## <a name="see-also"></a><span data-ttu-id="8fb03-155">See also</span><span class="sxs-lookup"><span data-stu-id="8fb03-155">See also</span></span>

* [<span data-ttu-id="8fb03-156">Configure Hive policies in domain-joined HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fb03-156">Configure Hive policies in domain-joined HDInsight</span></span>](hdinsight-domain-joined-run-hive.md)
* [<span data-ttu-id="8fb03-157">Manage domain-joined HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="8fb03-157">Manage domain-joined HDInsight clusters</span></span>](hdinsight-domain-joined-manage.md)
* [<span data-ttu-id="8fb03-158">Authorize users to Ambari</span><span class="sxs-lookup"><span data-stu-id="8fb03-158">Authorize users to Ambari</span></span>](hdinsight-authorize-users-to-ambari.md)
