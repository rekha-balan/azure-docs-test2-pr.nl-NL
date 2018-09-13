---
title: Manage Hadoop clusters in HDInsight using Azure portal
description: Learn how to create and manage HDInsight clusters using the Azure portal.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/18/2018
ms.author: jasonh
ms.openlocfilehash: 4eb93932c2bf95c71d4407304cb04a94a2eec8c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774065"
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="64725-103">Manage Hadoop clusters in HDInsight by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="64725-103">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>

[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="64725-104">Using the [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64725-104">Using the [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="64725-105">Use the tab selector above for information on managing Hadoop clusters in HDInsight using other tools.</span><span class="sxs-lookup"><span data-stu-id="64725-105">Use the tab selector above for information on managing Hadoop clusters in HDInsight using other tools.</span></span>

<span data-ttu-id="64725-106">**Prerequisite**</span><span class="sxs-lookup"><span data-stu-id="64725-106">**Prerequisite**</span></span>

<span data-ttu-id="64725-107">To follow the steps in this article, you will need an **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="64725-107">To follow the steps in this article, you will need an **Azure subscription**.</span></span> <span data-ttu-id="64725-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="64725-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="open-the-azure-portal"></a><span data-ttu-id="64725-109">Open the Azure portal</span><span class="sxs-lookup"><span data-stu-id="64725-109">Open the Azure portal</span></span>
1. <span data-ttu-id="64725-110">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64725-110">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64725-111">After you open the portal, you can:</span><span class="sxs-lookup"><span data-stu-id="64725-111">After you open the portal, you can:</span></span>

   * <span data-ttu-id="64725-112">Click **Create a resource** from the left menu to create a new cluster:</span><span class="sxs-lookup"><span data-stu-id="64725-112">Click **Create a resource** from the left menu to create a new cluster:</span></span>

       ![new HDInsight cluster button](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)

       <span data-ttu-id="64725-114">Enter **HDInsight** in **Search the Marketplace**, click **HDInsight**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="64725-114">Enter **HDInsight** in **Search the Marketplace**, click **HDInsight**, and then click **Create**.</span></span>

   * <span data-ttu-id="64725-115">Click **HDInsight Clusters** from the left menu to list the existing clusters:</span><span class="sxs-lookup"><span data-stu-id="64725-115">Click **HDInsight Clusters** from the left menu to list the existing clusters:</span></span>

       ![Azure portal HDInsight cluster button](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       <span data-ttu-id="64725-117">If you don't see the **HDInsight clusters** button, and then click **HDInsight clusters** under the **Intelligence + Analytics** section.</span><span class="sxs-lookup"><span data-stu-id="64725-117">If you don't see the **HDInsight clusters** button, and then click **HDInsight clusters** under the **Intelligence + Analytics** section.</span></span>


## <a name="create-clusters"></a><span data-ttu-id="64725-118">Create clusters</span><span class="sxs-lookup"><span data-stu-id="64725-118">Create clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="64725-119">HDInsight works with a wide range of Hadoop components.</span><span class="sxs-lookup"><span data-stu-id="64725-119">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="64725-120">For the list of the components that are verified and supported, see [What version of Hadoop is in Azure HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="64725-120">For the list of the components that are verified and supported, see [What version of Hadoop is in Azure HDInsight?](hdinsight-component-versioning.md)</span></span> <span data-ttu-id="64725-121">For general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="64725-121">For general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="64725-122">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="64725-122">Access control requirements</span></span>

<span data-ttu-id="64725-123">You must specify an Azure subscription when you create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-123">You must specify an Azure subscription when you create an HDInsight cluster.</span></span> <span data-ttu-id="64725-124">The cluster can be created either in a new Azure Resource group or in an existing Resource group.</span><span class="sxs-lookup"><span data-stu-id="64725-124">The cluster can be created either in a new Azure Resource group or in an existing Resource group.</span></span> <span data-ttu-id="64725-125">You can use the following steps to verify your permissions for creating HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="64725-125">You can use the following steps to verify your permissions for creating HDInsight clusters:</span></span>

- <span data-ttu-id="64725-126">To create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="64725-126">To create a new resource group:</span></span>

    1. <span data-ttu-id="64725-127">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64725-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="64725-128">Click **Subscription** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="64725-128">Click **Subscription** from the left menu.</span></span> <span data-ttu-id="64725-129">It has a yellow key icon.</span><span class="sxs-lookup"><span data-stu-id="64725-129">It has a yellow key icon.</span></span> <span data-ttu-id="64725-130">You shall see a list of subscriptions.</span><span class="sxs-lookup"><span data-stu-id="64725-130">You shall see a list of subscriptions.</span></span>
    3. <span data-ttu-id="64725-131">Click the subscription that you use to create clusters.</span><span class="sxs-lookup"><span data-stu-id="64725-131">Click the subscription that you use to create clusters.</span></span> 
    4. <span data-ttu-id="64725-132">Click **My permissions**.</span><span class="sxs-lookup"><span data-stu-id="64725-132">Click **My permissions**.</span></span>  <span data-ttu-id="64725-133">It shows your [role](../role-based-access-control/built-in-roles.md) on the subscription.</span><span class="sxs-lookup"><span data-stu-id="64725-133">It shows your [role](../role-based-access-control/built-in-roles.md) on the subscription.</span></span> <span data-ttu-id="64725-134">You need at least Contributor access to create HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-134">You need at least Contributor access to create HDInsight cluster.</span></span>

- <span data-ttu-id="64725-135">To use an existing resource group:</span><span class="sxs-lookup"><span data-stu-id="64725-135">To use an existing resource group:</span></span>

    1. <span data-ttu-id="64725-136">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64725-136">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="64725-137">Click **Resource groups** from the left menu to list the resource groups.</span><span class="sxs-lookup"><span data-stu-id="64725-137">Click **Resource groups** from the left menu to list the resource groups.</span></span>
    3. <span data-ttu-id="64725-138">Click the resource group you want to use for creating your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-138">Click the resource group you want to use for creating your HDInsight cluster.</span></span>
    4. <span data-ttu-id="64725-139">Click **Access control (IAM)**, and verify that you (or a group you belong to) have at least the Contributor access to the resource group.</span><span class="sxs-lookup"><span data-stu-id="64725-139">Click **Access control (IAM)**, and verify that you (or a group you belong to) have at least the Contributor access to the resource group.</span></span>

<span data-ttu-id="64725-140">If you receive the NoRegisteredProviderFound error or the MissingSubscriptionRegistration error, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="64725-140">If you receive the NoRegisteredProviderFound error or the MissingSubscriptionRegistration error, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="64725-141">List and show clusters</span><span class="sxs-lookup"><span data-stu-id="64725-141">List and show clusters</span></span>
1. <span data-ttu-id="64725-142">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64725-142">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64725-143">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span><span class="sxs-lookup"><span data-stu-id="64725-143">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span> <span data-ttu-id="64725-144">If you don't see **HDInsight Clusters**, click **All services** first.</span><span class="sxs-lookup"><span data-stu-id="64725-144">If you don't see **HDInsight Clusters**, click **All services** first.</span></span>
3. <span data-ttu-id="64725-145">Click the cluster name.</span><span class="sxs-lookup"><span data-stu-id="64725-145">Click the cluster name.</span></span> <span data-ttu-id="64725-146">If the cluster list is long, you can use filter on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="64725-146">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="64725-147">Click a cluster from the list to see the overview page:</span><span class="sxs-lookup"><span data-stu-id="64725-147">Click a cluster from the list to see the overview page:</span></span>

    <span data-ttu-id="64725-148">![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png) **Overview menu:**</span><span class="sxs-lookup"><span data-stu-id="64725-148">![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png) **Overview menu:**</span></span>
    * <span data-ttu-id="64725-149">**Dashboard**: Opens the Ambari web UI for the cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-149">**Dashboard**: Opens the Ambari web UI for the cluster.</span></span>
    * <span data-ttu-id="64725-150">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span><span class="sxs-lookup"><span data-stu-id="64725-150">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
    * <span data-ttu-id="64725-151">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-151">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
    * <span data-ttu-id="64725-152">**Move**: Moves the cluster to another resource group or to another subscription.</span><span class="sxs-lookup"><span data-stu-id="64725-152">**Move**: Moves the cluster to another resource group or to another subscription.</span></span>
    * <span data-ttu-id="64725-153">**Delete**: Deletes the cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-153">**Delete**: Deletes the cluster.</span></span>

    <span data-ttu-id="64725-154">**Left menu:**</span><span class="sxs-lookup"><span data-stu-id="64725-154">**Left menu:**</span></span>
    * <span data-ttu-id="64725-155">**Activity logs**: Show and query activity logs.</span><span class="sxs-lookup"><span data-stu-id="64725-155">**Activity logs**: Show and query activity logs.</span></span>
    * <span data-ttu-id="64725-156">**Access control (IAM)**: Use role assignments.</span><span class="sxs-lookup"><span data-stu-id="64725-156">**Access control (IAM)**: Use role assignments.</span></span>  <span data-ttu-id="64725-157">See [Use role assignments to manage access to your Azure subscription resources](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64725-157">See [Use role assignments to manage access to your Azure subscription resources](../role-based-access-control/role-assignments-portal.md).</span></span>
    * <span data-ttu-id="64725-158">**Tags**: Allows you to set key/value pairs to define a custom taxonomy of your cloud services.</span><span class="sxs-lookup"><span data-stu-id="64725-158">**Tags**: Allows you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="64725-159">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span><span class="sxs-lookup"><span data-stu-id="64725-159">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
    * <span data-ttu-id="64725-160">**Diagnose and solve problems**: Display troubleshooting information.</span><span class="sxs-lookup"><span data-stu-id="64725-160">**Diagnose and solve problems**: Display troubleshooting information.</span></span>
    * <span data-ttu-id="64725-161">**Locks**: Add a lock to prevent the cluster being modified or deleted.</span><span class="sxs-lookup"><span data-stu-id="64725-161">**Locks**: Add a lock to prevent the cluster being modified or deleted.</span></span>
    * <span data-ttu-id="64725-162">**Automation script**: Display and export the Azure Resource Manager template for the cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-162">**Automation script**: Display and export the Azure Resource Manager template for the cluster.</span></span> <span data-ttu-id="64725-163">Currently, you can only export the dependent Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="64725-163">Currently, you can only export the dependent Azure storage account.</span></span> <span data-ttu-id="64725-164">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span><span class="sxs-lookup"><span data-stu-id="64725-164">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>
    * <span data-ttu-id="64725-165">**Quick Start**:  Displays information that helps you get started using HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64725-165">**Quick Start**:  Displays information that helps you get started using HDInsight.</span></span>
    * <span data-ttu-id="64725-166">**Tools for HDInsight**: Help information for HDInsight related tools.</span><span class="sxs-lookup"><span data-stu-id="64725-166">**Tools for HDInsight**: Help information for HDInsight related tools.</span></span>
    * <span data-ttu-id="64725-167">**Subscription Core Usage**: Display the used and available cores for your subscription.</span><span class="sxs-lookup"><span data-stu-id="64725-167">**Subscription Core Usage**: Display the used and available cores for your subscription.</span></span>
    * <span data-ttu-id="64725-168">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span><span class="sxs-lookup"><span data-stu-id="64725-168">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span> <span data-ttu-id="64725-169">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-169">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span></span>
    * <span data-ttu-id="64725-170">**SSH + Cluster login**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span><span class="sxs-lookup"><span data-stu-id="64725-170">**SSH + Cluster login**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span> <span data-ttu-id="64725-171">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="64725-171">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
    * <span data-ttu-id="64725-172">**HDInsight Partner**: Add/remove the current HDInsight Partner.</span><span class="sxs-lookup"><span data-stu-id="64725-172">**HDInsight Partner**: Add/remove the current HDInsight Partner.</span></span>
    * <span data-ttu-id="64725-173">**External Metastores**: View the Hive and Oozie metastores.</span><span class="sxs-lookup"><span data-stu-id="64725-173">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="64725-174">The metastores can only be configured during the cluster creation process.</span><span class="sxs-lookup"><span data-stu-id="64725-174">The metastores can only be configured during the cluster creation process.</span></span> <span data-ttu-id="64725-175">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span><span class="sxs-lookup"><span data-stu-id="64725-175">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span></span>
    * <span data-ttu-id="64725-176">**Script Actions**: Run Bash scripts on the cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-176">**Script Actions**: Run Bash scripts on the cluster.</span></span> <span data-ttu-id="64725-177">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="64725-177">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    * <span data-ttu-id="64725-178">**Applications**: Add/remove HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="64725-178">**Applications**: Add/remove HDInsight applications.</span></span>  <span data-ttu-id="64725-179">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="64725-179">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
    * <span data-ttu-id="64725-180">**Monitoring**: Monitor the cluster in Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="64725-180">**Monitoring**: Monitor the cluster in Azure Log Analytics.</span></span>
    * <span data-ttu-id="64725-181">**Properties**: View the cluster properties.</span><span class="sxs-lookup"><span data-stu-id="64725-181">**Properties**: View the cluster properties.</span></span>
    * <span data-ttu-id="64725-182">**Storage accounts**: View the storage accounts and the keys.</span><span class="sxs-lookup"><span data-stu-id="64725-182">**Storage accounts**: View the storage accounts and the keys.</span></span> <span data-ttu-id="64725-183">The storage accounts are configured during the cluster creation process.</span><span class="sxs-lookup"><span data-stu-id="64725-183">The storage accounts are configured during the cluster creation process.</span></span>
    * <span data-ttu-id="64725-184">**Data Lake Store access**: Configure access Data Lake Stores.</span><span class="sxs-lookup"><span data-stu-id="64725-184">**Data Lake Store access**: Configure access Data Lake Stores.</span></span>  <span data-ttu-id="64725-185">See [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="64725-185">See [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>
    * <span data-ttu-id="64725-186">**Resource health**: See [Azure resource health overview](../service-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64725-186">**Resource health**: See [Azure resource health overview](../service-health/resource-health-overview.md).</span></span>
    * <span data-ttu-id="64725-187">**New support request**: Allows you to create a support ticket with Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="64725-187">**New support request**: Allows you to create a support ticket with Microsoft support.</span></span>
    
6. <span data-ttu-id="64725-188">Click **Properties**:</span><span class="sxs-lookup"><span data-stu-id="64725-188">Click **Properties**:</span></span>

    <span data-ttu-id="64725-189">The properties are:</span><span class="sxs-lookup"><span data-stu-id="64725-189">The properties are:</span></span>

   * <span data-ttu-id="64725-190">**Hostname**: Cluster name.</span><span class="sxs-lookup"><span data-stu-id="64725-190">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="64725-191">**Cluster URL**: The URL for the Ambari web interface.</span><span class="sxs-lookup"><span data-stu-id="64725-191">**Cluster URL**: The URL for the Ambari web interface.</span></span>
   * <span data-ttu-id="64725-192">**Secure shell (SSH)**: The username and host name to use in accessing the cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="64725-192">**Secure shell (SSH)**: The username and host name to use in accessing the cluster via SSH.</span></span>
   * <span data-ttu-id="64725-193">**Status**: One of: Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, or ClusterCustomization.</span><span class="sxs-lookup"><span data-stu-id="64725-193">**Status**: One of: Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, or ClusterCustomization.</span></span>
   * <span data-ttu-id="64725-194">**Region**: Azure location.</span><span class="sxs-lookup"><span data-stu-id="64725-194">**Region**: Azure location.</span></span> <span data-ttu-id="64725-195">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="64725-195">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="64725-196">**Date created**: The date the cluster was deployed.</span><span class="sxs-lookup"><span data-stu-id="64725-196">**Date created**: The date the cluster was deployed.</span></span>
   * <span data-ttu-id="64725-197">**Operating system**: Either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="64725-197">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="64725-198">**Type**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="64725-198">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="64725-199">**Version**.</span><span class="sxs-lookup"><span data-stu-id="64725-199">**Version**.</span></span> <span data-ttu-id="64725-200">See [HDInsight versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="64725-200">See [HDInsight versions](hdinsight-component-versioning.md).</span></span>
   * <span data-ttu-id="64725-201">**Subscription**: Subscription name.</span><span class="sxs-lookup"><span data-stu-id="64725-201">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="64725-202">**Default data source**: The default cluster file system.</span><span class="sxs-lookup"><span data-stu-id="64725-202">**Default data source**: The default cluster file system.</span></span>
   * <span data-ttu-id="64725-203">**Worker nodes size**: The selected VM size of the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="64725-203">**Worker nodes size**: The selected VM size of the worker nodes.</span></span>
   * <span data-ttu-id="64725-204">**Head node size**: The selected VM size of the head nodes.</span><span class="sxs-lookup"><span data-stu-id="64725-204">**Head node size**: The selected VM size of the head nodes.</span></span>
   * <span data-ttu-id="64725-205">**Virtual network**: The name of the Virtual Network which the cluster is deployed, if one was selected at deployment time.</span><span class="sxs-lookup"><span data-stu-id="64725-205">**Virtual network**: The name of the Virtual Network which the cluster is deployed, if one was selected at deployment time.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="64725-206">Delete clusters</span><span class="sxs-lookup"><span data-stu-id="64725-206">Delete clusters</span></span>
<span data-ttu-id="64725-207">Deleting a cluster does not delete the default storage account nor any linked storage accounts.</span><span class="sxs-lookup"><span data-stu-id="64725-207">Deleting a cluster does not delete the default storage account nor any linked storage accounts.</span></span> <span data-ttu-id="64725-208">You can re-create the cluster by using the same storage accounts and the same metastores.</span><span class="sxs-lookup"><span data-stu-id="64725-208">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span> <span data-ttu-id="64725-209">We recommend using a new default Blob container when you re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-209">We recommend using a new default Blob container when you re-create the cluster.</span></span>

1. <span data-ttu-id="64725-210">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="64725-210">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="64725-211">Click **HDInsight Clusters** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="64725-211">Click **HDInsight Clusters** from the left menu.</span></span> <span data-ttu-id="64725-212">If you don't see **HDInsight Clusters**, click **All services** first.</span><span class="sxs-lookup"><span data-stu-id="64725-212">If you don't see **HDInsight Clusters**, click **All services** first.</span></span>
3. <span data-ttu-id="64725-213">Click the cluster that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="64725-213">Click the cluster that you want to delete.</span></span>
4. <span data-ttu-id="64725-214">Click **Delete** from the top menu, and then follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="64725-214">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="64725-215">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-215">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="64725-216">Add additional storage accounts</span><span class="sxs-lookup"><span data-stu-id="64725-216">Add additional storage accounts</span></span>

<span data-ttu-id="64725-217">You can add additional Azure Storage accounts and Azure Data Lake Store accounts after a cluster is created.</span><span class="sxs-lookup"><span data-stu-id="64725-217">You can add additional Azure Storage accounts and Azure Data Lake Store accounts after a cluster is created.</span></span> <span data-ttu-id="64725-218">For more information, see [Add additional storage accounts to HDInsight](./hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="64725-218">For more information, see [Add additional storage accounts to HDInsight](./hdinsight-hadoop-add-storage.md).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="64725-219">Scale clusters</span><span class="sxs-lookup"><span data-stu-id="64725-219">Scale clusters</span></span>
<span data-ttu-id="64725-220">The cluster scaling feature allows you to change the number of worker nodes used by an Azure HDInsight cluster, without having to re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-220">The cluster scaling feature allows you to change the number of worker nodes used by an Azure HDInsight cluster, without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="64725-221">Only clusters with HDInsight version 3.1.3 or higher are supported.</span><span class="sxs-lookup"><span data-stu-id="64725-221">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="64725-222">If you are unsure of the version of your cluster, you can check the Properties page.</span><span class="sxs-lookup"><span data-stu-id="64725-222">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="64725-223">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-223">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="64725-224">The impact of changing the number of data nodes varies for each type of cluster supported by HDInsight:</span><span class="sxs-lookup"><span data-stu-id="64725-224">The impact of changing the number of data nodes varies for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="64725-225">Hadoop</span><span class="sxs-lookup"><span data-stu-id="64725-225">Hadoop</span></span>

    <span data-ttu-id="64725-226">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span><span class="sxs-lookup"><span data-stu-id="64725-226">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="64725-227">New jobs can also be submitted while the operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="64725-227">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="64725-228">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span><span class="sxs-lookup"><span data-stu-id="64725-228">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="64725-229">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span><span class="sxs-lookup"><span data-stu-id="64725-229">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="64725-230">This behavior causes all running and pending jobs to fail at the completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="64725-230">This behavior causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="64725-231">You can, however, resubmit the jobs once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="64725-231">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="64725-232">HBase</span><span class="sxs-lookup"><span data-stu-id="64725-232">HBase</span></span>

    <span data-ttu-id="64725-233">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="64725-233">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="64725-234">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="64725-234">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="64725-235">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span><span class="sxs-lookup"><span data-stu-id="64725-235">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

    ```bash
    >pushd %HBASE_HOME%\bin
    >hbase shell
    >balancer
    ```

    <span data-ttu-id="64725-236">For more information on using the HBase shell, see [Get started with an Apache HBase example in HDInsight](hbase/apache-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="64725-236">For more information on using the HBase shell, see [Get started with an Apache HBase example in HDInsight](hbase/apache-hbase-tutorial-get-started-linux.md).</span></span>

* <span data-ttu-id="64725-237">Storm</span><span class="sxs-lookup"><span data-stu-id="64725-237">Storm</span></span>

    <span data-ttu-id="64725-238">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="64725-238">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="64725-239">However, after a successful completion of the scaling operation, you will need to rebalance the topology.</span><span class="sxs-lookup"><span data-stu-id="64725-239">However, after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="64725-240">Rebalancing can be accomplished in two ways:</span><span class="sxs-lookup"><span data-stu-id="64725-240">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="64725-241">Storm web UI</span><span class="sxs-lookup"><span data-stu-id="64725-241">Storm web UI</span></span>
  * <span data-ttu-id="64725-242">Command-line interface (CLI) tool</span><span class="sxs-lookup"><span data-stu-id="64725-242">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="64725-243">Refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span><span class="sxs-lookup"><span data-stu-id="64725-243">Refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="64725-244">The Storm web UI is available on the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="64725-244">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight Storm scale rebalance](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="64725-246">Here is an example CLI command to rebalance the Storm topology:</span><span class="sxs-lookup"><span data-stu-id="64725-246">Here is an example CLI command to rebalance the Storm topology:</span></span>

    ```cli
    ## Reconfigure the topology "mytopology" to use 5 worker processes,
    ## the spout "blue-spout" to use 3 executors, and
    ## the bolt "yellow-bolt" to use 10 executors
    $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10
    ```

<span data-ttu-id="64725-247">**To scale clusters**</span><span class="sxs-lookup"><span data-stu-id="64725-247">**To scale clusters**</span></span>

1. <span data-ttu-id="64725-248">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="64725-248">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="64725-249">Click **HDInsight Clusters** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="64725-249">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="64725-250">Click the cluster you want to scale.</span><span class="sxs-lookup"><span data-stu-id="64725-250">Click the cluster you want to scale.</span></span>
3. <span data-ttu-id="64725-251">Click **Scale Cluster**.</span><span class="sxs-lookup"><span data-stu-id="64725-251">Click **Scale Cluster**.</span></span>
4. <span data-ttu-id="64725-252">Enter **Number of Worker nodes**.</span><span class="sxs-lookup"><span data-stu-id="64725-252">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="64725-253">The limit on the number of cluster nodes varies between Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="64725-253">The limit on the number of cluster nodes varies between Azure subscriptions.</span></span> <span data-ttu-id="64725-254">You can contact billing support to increase the limit.</span><span class="sxs-lookup"><span data-stu-id="64725-254">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="64725-255">The cost information reflects the changes you have made to the number of nodes.</span><span class="sxs-lookup"><span data-stu-id="64725-255">The cost information reflects the changes you have made to the number of nodes.</span></span>

    ![HDInsight hadoop hbase storm spark scale](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="64725-257">Pause/shut down clusters</span><span class="sxs-lookup"><span data-stu-id="64725-257">Pause/shut down clusters</span></span>

<span data-ttu-id="64725-258">Most of Hadoop jobs are batch jobs that are only run occasionally.</span><span class="sxs-lookup"><span data-stu-id="64725-258">Most of Hadoop jobs are batch jobs that are only run occasionally.</span></span> <span data-ttu-id="64725-259">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span><span class="sxs-lookup"><span data-stu-id="64725-259">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="64725-260">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="64725-260">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="64725-261">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="64725-261">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="64725-262">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="64725-262">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="64725-263">There are many ways you can program the process:</span><span class="sxs-lookup"><span data-stu-id="64725-263">There are many ways you can program the process:</span></span>

* <span data-ttu-id="64725-264">User Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="64725-264">User Azure Data Factory.</span></span> <span data-ttu-id="64725-265">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span><span class="sxs-lookup"><span data-stu-id="64725-265">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span></span>
* <span data-ttu-id="64725-266">Use Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64725-266">Use Azure PowerShell.</span></span>  <span data-ttu-id="64725-267">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span><span class="sxs-lookup"><span data-stu-id="64725-267">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="64725-268">Use Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="64725-268">Use Azure CLI.</span></span> <span data-ttu-id="64725-269">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span><span class="sxs-lookup"><span data-stu-id="64725-269">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="64725-270">Use HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="64725-270">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="64725-271">See [Submit Hadoop jobs](hadoop/submit-apache-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="64725-271">See [Submit Hadoop jobs](hadoop/submit-apache-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="64725-272">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="64725-272">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="64725-273">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="64725-273">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="move-cluster"></a><span data-ttu-id="64725-274">Move cluster</span><span class="sxs-lookup"><span data-stu-id="64725-274">Move cluster</span></span>

<span data-ttu-id="64725-275">You can move an HDInsight cluster to another Azure resource group or another subscription.</span><span class="sxs-lookup"><span data-stu-id="64725-275">You can move an HDInsight cluster to another Azure resource group or another subscription.</span></span>  <span data-ttu-id="64725-276">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-276">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="upgrade-clusters"></a><span data-ttu-id="64725-277">Upgrade clusters</span><span class="sxs-lookup"><span data-stu-id="64725-277">Upgrade clusters</span></span>

<span data-ttu-id="64725-278">See [Upgrade HDInsight cluster to a newer version](./hdinsight-upgrade-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="64725-278">See [Upgrade HDInsight cluster to a newer version](./hdinsight-upgrade-cluster.md).</span></span>

## <a name="open-the-ambari-web-ui"></a><span data-ttu-id="64725-279">Open the Ambari web UI</span><span class="sxs-lookup"><span data-stu-id="64725-279">Open the Ambari web UI</span></span>

<span data-ttu-id="64725-280">Ambari provides an intuitive, easy-to-use Hadoop management web UI backed by its RESTful APIs.</span><span class="sxs-lookup"><span data-stu-id="64725-280">Ambari provides an intuitive, easy-to-use Hadoop management web UI backed by its RESTful APIs.</span></span> <span data-ttu-id="64725-281">Ambari enables system administrators to manage and monitor Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="64725-281">Ambari enables system administrators to manage and monitor Hadoop clusters.</span></span>

1. <span data-ttu-id="64725-282">Open an HDInsight cluster from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="64725-282">Open an HDInsight cluster from the Azure portal.</span></span>  <span data-ttu-id="64725-283">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-283">See [List and show clusters](#list-and-show-clusters).</span></span>
2. <span data-ttu-id="64725-284">Click **Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="64725-284">Click **Cluster Dashboard**.</span></span>

    ![HDInsight Hadoop cluster menu](./media/hdinsight-administer-use-portal-linux/hdinsight-azure-portal-cluster-menu.png)

1. <span data-ttu-id="64725-286">Enter the cluster username and password.</span><span class="sxs-lookup"><span data-stu-id="64725-286">Enter the cluster username and password.</span></span>  <span data-ttu-id="64725-287">The default cluster username is _admin_. The Ambari web UI looks like:</span><span class="sxs-lookup"><span data-stu-id="64725-287">The default cluster username is _admin_. The Ambari web UI looks like:</span></span>

    ![HDInsight Hadoop Ambari Web UI](./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-ambari-web-ui.png)

<span data-ttu-id="64725-289">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="64725-289">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="change-passwords"></a><span data-ttu-id="64725-290">Change passwords</span><span class="sxs-lookup"><span data-stu-id="64725-290">Change passwords</span></span>
<span data-ttu-id="64725-291">An HDInsight cluster can have two user accounts.</span><span class="sxs-lookup"><span data-stu-id="64725-291">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="64725-292">The HDInsight cluster user account (A.K.A.</span><span class="sxs-lookup"><span data-stu-id="64725-292">The HDInsight cluster user account (A.K.A.</span></span> <span data-ttu-id="64725-293">HTTP user account) and the SSH user account are created during the creation process.</span><span class="sxs-lookup"><span data-stu-id="64725-293">HTTP user account) and the SSH user account are created during the creation process.</span></span> <span data-ttu-id="64725-294">You can use the Ambari web UI to change the cluster user account username and password, and script actions to change the SSH user account</span><span class="sxs-lookup"><span data-stu-id="64725-294">You can use the Ambari web UI to change the cluster user account username and password, and script actions to change the SSH user account</span></span>

### <a name="change-the-cluster-user-password"></a><span data-ttu-id="64725-295">Change the cluster user password</span><span class="sxs-lookup"><span data-stu-id="64725-295">Change the cluster user password</span></span>
<span data-ttu-id="64725-296">You can use the Ambari Web UI to change the Cluster user password.</span><span class="sxs-lookup"><span data-stu-id="64725-296">You can use the Ambari Web UI to change the Cluster user password.</span></span> <span data-ttu-id="64725-297">To log in to Ambari, you must use the existing cluster username and password.</span><span class="sxs-lookup"><span data-stu-id="64725-297">To log in to Ambari, you must use the existing cluster username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="64725-298">Changing the cluster user (admin) password may cause script actions run against this cluster to fail.</span><span class="sxs-lookup"><span data-stu-id="64725-298">Changing the cluster user (admin) password may cause script actions run against this cluster to fail.</span></span> <span data-ttu-id="64725-299">If you have any persisted script actions that target worker nodes, these scripts may fail when you add nodes to the cluster through resize operations.</span><span class="sxs-lookup"><span data-stu-id="64725-299">If you have any persisted script actions that target worker nodes, these scripts may fail when you add nodes to the cluster through resize operations.</span></span> <span data-ttu-id="64725-300">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="64725-300">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="64725-301">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span><span class="sxs-lookup"><span data-stu-id="64725-301">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="64725-302">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="64725-302">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="64725-303">Click **Admin** from the top menu, and then click "Manage Ambari".</span><span class="sxs-lookup"><span data-stu-id="64725-303">Click **Admin** from the top menu, and then click "Manage Ambari".</span></span>
3. <span data-ttu-id="64725-304">From the left menu, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="64725-304">From the left menu, click **Users**.</span></span>
4. <span data-ttu-id="64725-305">Click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="64725-305">Click **Admin**.</span></span>
5. <span data-ttu-id="64725-306">Click **Change Password**.</span><span class="sxs-lookup"><span data-stu-id="64725-306">Click **Change Password**.</span></span>

<span data-ttu-id="64725-307">Ambari then changes the password on all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-307">Ambari then changes the password on all nodes in the cluster.</span></span>

### <a name="change-the-ssh-user-password"></a><span data-ttu-id="64725-308">Change the SSH user password</span><span class="sxs-lookup"><span data-stu-id="64725-308">Change the SSH user password</span></span>
1. <span data-ttu-id="64725-309">Using a text editor, save the following text as a file named **changepassword.sh**.</span><span class="sxs-lookup"><span data-stu-id="64725-309">Using a text editor, save the following text as a file named **changepassword.sh**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="64725-310">You must use an editor that uses LF as the line ending.</span><span class="sxs-lookup"><span data-stu-id="64725-310">You must use an editor that uses LF as the line ending.</span></span> <span data-ttu-id="64725-311">If the editor uses CRLF, then the script does not work.</span><span class="sxs-lookup"><span data-stu-id="64725-311">If the editor uses CRLF, then the script does not work.</span></span>

    ```bash
    #! /bin/bash
    USER=$1
    PASS=$2
    usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
    ```

2. <span data-ttu-id="64725-312">Upload the file to a storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span><span class="sxs-lookup"><span data-stu-id="64725-312">Upload the file to a storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span></span> <span data-ttu-id="64725-313">For example, a public file store such as OneDrive or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="64725-313">For example, a public file store such as OneDrive or Azure Blob storage.</span></span> <span data-ttu-id="64725-314">Save the URI (HTTP or HTTPS address) to the file, as this URI is needed in the next step.</span><span class="sxs-lookup"><span data-stu-id="64725-314">Save the URI (HTTP or HTTPS address) to the file, as this URI is needed in the next step.</span></span>
3. <span data-ttu-id="64725-315">From the Azure portal, click **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="64725-315">From the Azure portal, click **HDInsight Clusters**.</span></span>
4. <span data-ttu-id="64725-316">Click your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-316">Click your HDInsight cluster.</span></span>
4. <span data-ttu-id="64725-317">Click **Script Actions**.</span><span class="sxs-lookup"><span data-stu-id="64725-317">Click **Script Actions**.</span></span>
4. <span data-ttu-id="64725-318">From the **Script Actions** blade, select **Submit New**.</span><span class="sxs-lookup"><span data-stu-id="64725-318">From the **Script Actions** blade, select **Submit New**.</span></span> <span data-ttu-id="64725-319">When the **Submit script action** blade appears, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="64725-319">When the **Submit script action** blade appears, enter the following information:</span></span>

   | <span data-ttu-id="64725-320">Field</span><span class="sxs-lookup"><span data-stu-id="64725-320">Field</span></span> | <span data-ttu-id="64725-321">Value</span><span class="sxs-lookup"><span data-stu-id="64725-321">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="64725-322">Name</span><span class="sxs-lookup"><span data-stu-id="64725-322">Name</span></span> |<span data-ttu-id="64725-323">Change ssh password</span><span class="sxs-lookup"><span data-stu-id="64725-323">Change ssh password</span></span> |
   | <span data-ttu-id="64725-324">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="64725-324">Bash script URI</span></span> |<span data-ttu-id="64725-325">The URI to the changepassword.sh file</span><span class="sxs-lookup"><span data-stu-id="64725-325">The URI to the changepassword.sh file</span></span> |
   | <span data-ttu-id="64725-326">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span><span class="sxs-lookup"><span data-stu-id="64725-326">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span></span> |<span data-ttu-id="64725-327">✓ for all node types listed</span><span class="sxs-lookup"><span data-stu-id="64725-327">✓ for all node types listed</span></span> |
   | <span data-ttu-id="64725-328">Parameters</span><span class="sxs-lookup"><span data-stu-id="64725-328">Parameters</span></span> |<span data-ttu-id="64725-329">Enter the SSH user name and then the new password.</span><span class="sxs-lookup"><span data-stu-id="64725-329">Enter the SSH user name and then the new password.</span></span> <span data-ttu-id="64725-330">There should be one space between the user name and the password.</span><span class="sxs-lookup"><span data-stu-id="64725-330">There should be one space between the user name and the password.</span></span> |
   | <span data-ttu-id="64725-331">Persist this script action ...</span><span class="sxs-lookup"><span data-stu-id="64725-331">Persist this script action ...</span></span> |<span data-ttu-id="64725-332">Leave this field unchecked.</span><span class="sxs-lookup"><span data-stu-id="64725-332">Leave this field unchecked.</span></span> |
5. <span data-ttu-id="64725-333">Select **Create** to apply the script.</span><span class="sxs-lookup"><span data-stu-id="64725-333">Select **Create** to apply the script.</span></span> <span data-ttu-id="64725-334">Once the script finishes, you are able to connect to the cluster using SSH with the new password.</span><span class="sxs-lookup"><span data-stu-id="64725-334">Once the script finishes, you are able to connect to the cluster using SSH with the new password.</span></span>

## <a name="grantrevoke-access"></a><span data-ttu-id="64725-335">Grant/revoke access</span><span class="sxs-lookup"><span data-stu-id="64725-335">Grant/revoke access</span></span>
<span data-ttu-id="64725-336">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span><span class="sxs-lookup"><span data-stu-id="64725-336">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="64725-337">ODBC</span><span class="sxs-lookup"><span data-stu-id="64725-337">ODBC</span></span>
* <span data-ttu-id="64725-338">JDBC</span><span class="sxs-lookup"><span data-stu-id="64725-338">JDBC</span></span>
* <span data-ttu-id="64725-339">Ambari</span><span class="sxs-lookup"><span data-stu-id="64725-339">Ambari</span></span>
* <span data-ttu-id="64725-340">Oozie</span><span class="sxs-lookup"><span data-stu-id="64725-340">Oozie</span></span>
* <span data-ttu-id="64725-341">Templeton</span><span class="sxs-lookup"><span data-stu-id="64725-341">Templeton</span></span>

<span data-ttu-id="64725-342">By default, these services are granted for access.</span><span class="sxs-lookup"><span data-stu-id="64725-342">By default, these services are granted for access.</span></span> <span data-ttu-id="64725-343">You can revoke/grant the access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span><span class="sxs-lookup"><span data-stu-id="64725-343">You can revoke/grant the access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span></span>

## <a name="find-the-subscription-id"></a><span data-ttu-id="64725-344">Find the subscription ID</span><span class="sxs-lookup"><span data-stu-id="64725-344">Find the subscription ID</span></span>

<span data-ttu-id="64725-345">**To find your Azure subscription IDs**</span><span class="sxs-lookup"><span data-stu-id="64725-345">**To find your Azure subscription IDs**</span></span>

1. <span data-ttu-id="64725-346">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="64725-346">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="64725-347">Click **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="64725-347">Click **Subscriptions**.</span></span> <span data-ttu-id="64725-348">Each subscription has a name and an ID.</span><span class="sxs-lookup"><span data-stu-id="64725-348">Each subscription has a name and an ID.</span></span>

<span data-ttu-id="64725-349">Each cluster is tied to an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="64725-349">Each cluster is tied to an Azure subscription.</span></span> <span data-ttu-id="64725-350">The subscription ID is shown on the cluster **Essential** tile.</span><span class="sxs-lookup"><span data-stu-id="64725-350">The subscription ID is shown on the cluster **Essential** tile.</span></span> <span data-ttu-id="64725-351">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-351">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="64725-352">Find the resource group</span><span class="sxs-lookup"><span data-stu-id="64725-352">Find the resource group</span></span>
<span data-ttu-id="64725-353">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span><span class="sxs-lookup"><span data-stu-id="64725-353">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span></span> <span data-ttu-id="64725-354">The Resource Manager group that a cluster belongs to appears in:</span><span class="sxs-lookup"><span data-stu-id="64725-354">The Resource Manager group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="64725-355">The cluster list has a **Resource Group** column.</span><span class="sxs-lookup"><span data-stu-id="64725-355">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="64725-356">Cluster **Essential** tile.</span><span class="sxs-lookup"><span data-stu-id="64725-356">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="64725-357">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-357">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-storage-accounts"></a><span data-ttu-id="64725-358">Find the storage accounts</span><span class="sxs-lookup"><span data-stu-id="64725-358">Find the storage accounts</span></span>

<span data-ttu-id="64725-359">HDInsight clusters use either an Azure Storage account or an Azure Data Lake Store to store data.</span><span class="sxs-lookup"><span data-stu-id="64725-359">HDInsight clusters use either an Azure Storage account or an Azure Data Lake Store to store data.</span></span> <span data-ttu-id="64725-360">Each HDInsight cluster can have one default storage account and a number of linked storage accounts.</span><span class="sxs-lookup"><span data-stu-id="64725-360">Each HDInsight cluster can have one default storage account and a number of linked storage accounts.</span></span> <span data-ttu-id="64725-361">To list the storage accounts, you first open the cluster from the portal, and then click **Storage accounts**:</span><span class="sxs-lookup"><span data-stu-id="64725-361">To list the storage accounts, you first open the cluster from the portal, and then click **Storage accounts**:</span></span>

![HDInsight cluster storage accounts](./media/hdinsight-administer-use-portal-linux/hdinsight-storage-accounts.png)

<span data-ttu-id="64725-363">On the previous screenshot, there is a __Default__ column indicating whether the account is the default storage account.</span><span class="sxs-lookup"><span data-stu-id="64725-363">On the previous screenshot, there is a __Default__ column indicating whether the account is the default storage account.</span></span>

<span data-ttu-id="64725-364">To list the Data Lake Store accounts, click **Data Lake Store access** in the previous screenshot.</span><span class="sxs-lookup"><span data-stu-id="64725-364">To list the Data Lake Store accounts, click **Data Lake Store access** in the previous screenshot.</span></span>

## <a name="run-hive-queries"></a><span data-ttu-id="64725-365">Run Hive queries</span><span class="sxs-lookup"><span data-stu-id="64725-365">Run Hive queries</span></span>
<span data-ttu-id="64725-366">You cannot run Hive job directly from the Azure portal, but you can use the Hive View on Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="64725-366">You cannot run Hive job directly from the Azure portal, but you can use the Hive View on Ambari Web UI.</span></span>

<span data-ttu-id="64725-367">**To run Hive queries using Ambari Hive View**</span><span class="sxs-lookup"><span data-stu-id="64725-367">**To run Hive queries using Ambari Hive View**</span></span>

1. <span data-ttu-id="64725-368">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span><span class="sxs-lookup"><span data-stu-id="64725-368">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="64725-369">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="64725-369">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="64725-370">Open Hive View as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="64725-370">Open Hive View as shown in the following screenshot:</span></span>  

    ![HDInsight hive view](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)

3. <span data-ttu-id="64725-372">Click **Query** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="64725-372">Click **Query** from the top menu.</span></span>
4. <span data-ttu-id="64725-373">Enter a Hive query in **Query Editor**, and then click **Execute**.</span><span class="sxs-lookup"><span data-stu-id="64725-373">Enter a Hive query in **Query Editor**, and then click **Execute**.</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="64725-374">Monitor jobs</span><span class="sxs-lookup"><span data-stu-id="64725-374">Monitor jobs</span></span>
<span data-ttu-id="64725-375">See [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span><span class="sxs-lookup"><span data-stu-id="64725-375">See [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span></span>

## <a name="browse-files"></a><span data-ttu-id="64725-376">Browse files</span><span class="sxs-lookup"><span data-stu-id="64725-376">Browse files</span></span>
<span data-ttu-id="64725-377">Using the Azure portal, you can browse the content of the default container.</span><span class="sxs-lookup"><span data-stu-id="64725-377">Using the Azure portal, you can browse the content of the default container.</span></span>

1. <span data-ttu-id="64725-378">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64725-378">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64725-379">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span><span class="sxs-lookup"><span data-stu-id="64725-379">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="64725-380">Click the cluster name.</span><span class="sxs-lookup"><span data-stu-id="64725-380">Click the cluster name.</span></span> <span data-ttu-id="64725-381">If the cluster list is long, you can use filter on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="64725-381">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="64725-382">Click **Storage Accounts** from the cluster left menu.</span><span class="sxs-lookup"><span data-stu-id="64725-382">Click **Storage Accounts** from the cluster left menu.</span></span>
5. <span data-ttu-id="64725-383">Click a Storage account.</span><span class="sxs-lookup"><span data-stu-id="64725-383">Click a Storage account.</span></span>
7. <span data-ttu-id="64725-384">Click the **Blobs** tile.</span><span class="sxs-lookup"><span data-stu-id="64725-384">Click the **Blobs** tile.</span></span>
8. <span data-ttu-id="64725-385">Click the default container name.</span><span class="sxs-lookup"><span data-stu-id="64725-385">Click the default container name.</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="64725-386">Monitor cluster usage</span><span class="sxs-lookup"><span data-stu-id="64725-386">Monitor cluster usage</span></span>
<span data-ttu-id="64725-387">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span><span class="sxs-lookup"><span data-stu-id="64725-387">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="64725-388">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="64725-388">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64725-389">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="64725-389">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="64725-390">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="64725-390">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

## <a name="connect-to-a-cluster"></a><span data-ttu-id="64725-391">Connect to a cluster</span><span class="sxs-lookup"><span data-stu-id="64725-391">Connect to a cluster</span></span>

* [<span data-ttu-id="64725-392">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="64725-392">Use Hive with HDInsight</span></span>](hadoop/apache-hadoop-use-hive-ambari-view.md)
* [<span data-ttu-id="64725-393">Use SSH with HDInsight</span><span class="sxs-lookup"><span data-stu-id="64725-393">Use SSH with HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a><span data-ttu-id="64725-394">Next steps</span><span class="sxs-lookup"><span data-stu-id="64725-394">Next steps</span></span>

<span data-ttu-id="64725-395">In this article, you have learned some basic administrative functions.</span><span class="sxs-lookup"><span data-stu-id="64725-395">In this article, you have learned some basic administrative functions.</span></span> <span data-ttu-id="64725-396">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="64725-396">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="64725-397">Administer HDInsight Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="64725-397">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="64725-398">Administer HDInsight Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64725-398">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="64725-399">Create HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="64725-399">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="64725-400">Read more about using the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="64725-400">Read more about using the Ambari Web UI</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="64725-401">Details on using the Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="64725-401">Details on using the Ambari REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)
* [<span data-ttu-id="64725-402">Use Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="64725-402">Use Hive in HDInsight</span></span>](hadoop/hdinsight-use-hive.md)
* [<span data-ttu-id="64725-403">Use Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="64725-403">Use Pig in HDInsight</span></span>](hadoop/hdinsight-use-pig.md)
* [<span data-ttu-id="64725-404">Use Sqoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="64725-404">Use Sqoop in HDInsight</span></span>](hadoop/hdinsight-use-sqoop.md)
* [<span data-ttu-id="64725-405">Get Started with Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="64725-405">Get Started with Azure HDInsight</span></span>](hadoop/apache-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="64725-406">What version of Hadoop is in Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="64725-406">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop command line"
