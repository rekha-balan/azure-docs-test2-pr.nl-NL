---
title: Manage Hadoop clusters in HDInsight using Azure portal | Microsoft Docs
description: Learn how to create and manage HDInsight clusters using the Azure portal.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: jgao
ms.openlocfilehash: 31d048d3055f969a84d0c7349412430fb98089de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556592"
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="b5224-103">Manage Hadoop clusters in HDInsight by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b5224-103">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="b5224-104">Using the [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b5224-104">Using the [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="b5224-105">Use the tab selector for information on managing Hadoop clusters in HDInsight using other tools.</span><span class="sxs-lookup"><span data-stu-id="b5224-105">Use the tab selector for information on managing Hadoop clusters in HDInsight using other tools.</span></span>

<span data-ttu-id="b5224-106">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="b5224-106">**Prerequisites**</span></span>

<span data-ttu-id="b5224-107">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="b5224-107">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="b5224-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="b5224-108">**An Azure subscription**.</span></span> <span data-ttu-id="b5224-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b5224-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="open-the-portal"></a><span data-ttu-id="b5224-110">Open the Portal</span><span class="sxs-lookup"><span data-stu-id="b5224-110">Open the Portal</span></span>
1. <span data-ttu-id="b5224-111">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5224-111">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5224-112">After you open the portal, you can:</span><span class="sxs-lookup"><span data-stu-id="b5224-112">After you open the portal, you can:</span></span>

   * <span data-ttu-id="b5224-113">Click **New** from the left menu to create a new cluster:</span><span class="sxs-lookup"><span data-stu-id="b5224-113">Click **New** from the left menu to create a new cluster:</span></span>

       ![new HDInsight cluster button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * <span data-ttu-id="b5224-115">Click **HDInsight Clusters** from the left menu to list the existing clusters</span><span class="sxs-lookup"><span data-stu-id="b5224-115">Click **HDInsight Clusters** from the left menu to list the existing clusters</span></span>

       ![Azure portal HDInsight cluster button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       <span data-ttu-id="b5224-117">If you don't see HDInsight cluster, click **More services** on the bottom of the list, and then click **HDInsight clusters** under the **Intelligence + Analytics** section.</span><span class="sxs-lookup"><span data-stu-id="b5224-117">If you don't see HDInsight cluster, click **More services** on the bottom of the list, and then click **HDInsight clusters** under the **Intelligence + Analytics** section.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="b5224-118">Create clusters</span><span class="sxs-lookup"><span data-stu-id="b5224-118">Create clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="b5224-119">HDInsight works with a wide range of Hadoop components.</span><span class="sxs-lookup"><span data-stu-id="b5224-119">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="b5224-120">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-120">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="b5224-121">For the general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-121">For the general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="b5224-122">List and show clusters</span><span class="sxs-lookup"><span data-stu-id="b5224-122">List and show clusters</span></span>
1. <span data-ttu-id="b5224-123">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5224-123">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5224-124">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span><span class="sxs-lookup"><span data-stu-id="b5224-124">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="b5224-125">Click the cluster name.</span><span class="sxs-lookup"><span data-stu-id="b5224-125">Click the cluster name.</span></span> <span data-ttu-id="b5224-126">If the cluster list is long, you can use filter on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="b5224-126">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="b5224-127">Click a cluster from the list to see the overview page:</span><span class="sxs-lookup"><span data-stu-id="b5224-127">Click a cluster from the list to see the overview page:</span></span>

    ![Azure portal HDInsight cluster essentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    <span data-ttu-id="b5224-129">**Overview menu:**</span><span class="sxs-lookup"><span data-stu-id="b5224-129">**Overview menu:**</span></span>

   * <span data-ttu-id="b5224-130">**Dashboard**: Opens the cluster dashboard, which is Ambari Web for Linux-based clusters.</span><span class="sxs-lookup"><span data-stu-id="b5224-130">**Dashboard**: Opens the cluster dashboard, which is Ambari Web for Linux-based clusters.</span></span>
   * <span data-ttu-id="b5224-131">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span><span class="sxs-lookup"><span data-stu-id="b5224-131">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
   * <span data-ttu-id="b5224-132">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-132">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
   * <span data-ttu-id="b5224-133">**Delete**: Deletes the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-133">**Delete**: Deletes the cluster.</span></span>

    <span data-ttu-id="b5224-134">**Left menu:**</span><span class="sxs-lookup"><span data-stu-id="b5224-134">**Left menu:**</span></span>

   * <span data-ttu-id="b5224-135">**Activity logs**: Show and query activity logs.</span><span class="sxs-lookup"><span data-stu-id="b5224-135">**Activity logs**: Show and query activity logs.</span></span>
   * <span data-ttu-id="b5224-136">**Access control (IAM)**: Use role assignments.</span><span class="sxs-lookup"><span data-stu-id="b5224-136">**Access control (IAM)**: Use role assignments.</span></span>  <span data-ttu-id="b5224-137">See [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-137">See [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
   * <span data-ttu-id="b5224-138">**Tags**: Allows you to set key/value pairs to define a custom taxonomy of your cloud services.</span><span class="sxs-lookup"><span data-stu-id="b5224-138">**Tags**: Allows you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="b5224-139">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span><span class="sxs-lookup"><span data-stu-id="b5224-139">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
   * <span data-ttu-id="b5224-140">**Diagnose and solve problems**: Display troubleshooting information.</span><span class="sxs-lookup"><span data-stu-id="b5224-140">**Diagnose and solve problems**: Display troubleshooting information.</span></span>
   * <span data-ttu-id="b5224-141">**Locks**: Add lock to prevent the cluster being modified or deleted.</span><span class="sxs-lookup"><span data-stu-id="b5224-141">**Locks**: Add lock to prevent the cluster being modified or deleted.</span></span>
   * <span data-ttu-id="b5224-142">**Automation script**: Display and export the Azure Resource Manager template for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-142">**Automation script**: Display and export the Azure Resource Manager template for the cluster.</span></span> <span data-ttu-id="b5224-143">Currently, you can only export the dependent Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="b5224-143">Currently, you can only export the dependent Azure storage account.</span></span> <span data-ttu-id="b5224-144">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-144">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>
   * <span data-ttu-id="b5224-145">**Quick Start**:  Displays information that will help you get started using HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b5224-145">**Quick Start**:  Displays information that will help you get started using HDInsight.</span></span>
   * <span data-ttu-id="b5224-146">**Tools for HDInsight**: Help information for HDInsight related tools.</span><span class="sxs-lookup"><span data-stu-id="b5224-146">**Tools for HDInsight**: Help information for HDInsight related tools.</span></span>
   * <span data-ttu-id="b5224-147">**Cluster Login**: Display the cluster login information.</span><span class="sxs-lookup"><span data-stu-id="b5224-147">**Cluster Login**: Display the cluster login information.</span></span>
   * <span data-ttu-id="b5224-148">**Subscription Core Usage**: Display the used and available cores for your subscription.</span><span class="sxs-lookup"><span data-stu-id="b5224-148">**Subscription Core Usage**: Display the used and available cores for your subscription.</span></span>
   * <span data-ttu-id="b5224-149">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span><span class="sxs-lookup"><span data-stu-id="b5224-149">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span> <span data-ttu-id="b5224-150">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5224-150">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span></span>
   * <span data-ttu-id="b5224-151">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span><span class="sxs-lookup"><span data-stu-id="b5224-151">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span> <span data-ttu-id="b5224-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
   * <span data-ttu-id="b5224-153">**HDInsight Partner**: Add/remove the current HDInsight Partner.</span><span class="sxs-lookup"><span data-stu-id="b5224-153">**HDInsight Partner**: Add/remove the current HDInsight Partner.</span></span>
   * <span data-ttu-id="b5224-154">**External Metastores**: View the Hive and Oozie metastores.</span><span class="sxs-lookup"><span data-stu-id="b5224-154">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="b5224-155">The metastores can only be configured during the cluster creation process.</span><span class="sxs-lookup"><span data-stu-id="b5224-155">The metastores can only be configured during the cluster creation process.</span></span> <span data-ttu-id="b5224-156">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span><span class="sxs-lookup"><span data-stu-id="b5224-156">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span></span>
   * <span data-ttu-id="b5224-157">**Script Actions**: Run Bash scripts on the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-157">**Script Actions**: Run Bash scripts on the cluster.</span></span> <span data-ttu-id="b5224-158">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-158">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
   * <span data-ttu-id="b5224-159">**Applications**: Add/remove HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="b5224-159">**Applications**: Add/remove HDInsight applications.</span></span>  <span data-ttu-id="b5224-160">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-160">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
   * <span data-ttu-id="b5224-161">**Properties**: View the cluster properties.</span><span class="sxs-lookup"><span data-stu-id="b5224-161">**Properties**: View the cluster properties.</span></span>
   * <span data-ttu-id="b5224-162">**Storage accounts**: View the storage accounts and the keys.</span><span class="sxs-lookup"><span data-stu-id="b5224-162">**Storage accounts**: View the storage accounts and the keys.</span></span> <span data-ttu-id="b5224-163">The storage accounts are configured during the cluster creation process.</span><span class="sxs-lookup"><span data-stu-id="b5224-163">The storage accounts are configured during the cluster creation process.</span></span>
   * <span data-ttu-id="b5224-164">**Cluster AAD Identity**:</span><span class="sxs-lookup"><span data-stu-id="b5224-164">**Cluster AAD Identity**:</span></span>
   * <span data-ttu-id="b5224-165">**New support request**: Allows you to create a support ticket with Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="b5224-165">**New support request**: Allows you to create a support ticket with Microsoft support.</span></span>

6. <span data-ttu-id="b5224-166">Click **Properties**:</span><span class="sxs-lookup"><span data-stu-id="b5224-166">Click **Properties**:</span></span>

    <span data-ttu-id="b5224-167">The properties are:</span><span class="sxs-lookup"><span data-stu-id="b5224-167">The properties are:</span></span>

   * <span data-ttu-id="b5224-168">**Hostname**: Cluster name.</span><span class="sxs-lookup"><span data-stu-id="b5224-168">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="b5224-169">**Cluster URL**.</span><span class="sxs-lookup"><span data-stu-id="b5224-169">**Cluster URL**.</span></span> <span data-ttu-id="b5224-170">The URL for the Ambari web interface.</span><span class="sxs-lookup"><span data-stu-id="b5224-170">The URL for the Ambari web interface.</span></span>
   * <span data-ttu-id="b5224-171">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="b5224-171">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="b5224-172">**Region**: Azure location.</span><span class="sxs-lookup"><span data-stu-id="b5224-172">**Region**: Azure location.</span></span> <span data-ttu-id="b5224-173">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b5224-173">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="b5224-174">**Date created**.</span><span class="sxs-lookup"><span data-stu-id="b5224-174">**Date created**.</span></span>
   * <span data-ttu-id="b5224-175">**Operating system**: Either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="b5224-175">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="b5224-176">**Type**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="b5224-176">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="b5224-177">**Version**.</span><span class="sxs-lookup"><span data-stu-id="b5224-177">**Version**.</span></span> <span data-ttu-id="b5224-178">See [HDInsight versions](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="b5224-178">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="b5224-179">**Subscription**: Subscription name.</span><span class="sxs-lookup"><span data-stu-id="b5224-179">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="b5224-180">**Default data source**: The default cluster file system.</span><span class="sxs-lookup"><span data-stu-id="b5224-180">**Default data source**: The default cluster file system.</span></span>
   * <span data-ttu-id="b5224-181">**Worker nodes size**.</span><span class="sxs-lookup"><span data-stu-id="b5224-181">**Worker nodes size**.</span></span>
   * <span data-ttu-id="b5224-182">**Head node size**.</span><span class="sxs-lookup"><span data-stu-id="b5224-182">**Head node size**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="b5224-183">Delete clusters</span><span class="sxs-lookup"><span data-stu-id="b5224-183">Delete clusters</span></span>
<span data-ttu-id="b5224-184">Delete a cluster will not delete the default storage account or any linked storage accounts.</span><span class="sxs-lookup"><span data-stu-id="b5224-184">Delete a cluster will not delete the default storage account or any linked storage accounts.</span></span> <span data-ttu-id="b5224-185">You can re-create the cluster by using the same storage accounts and the same metastores.</span><span class="sxs-lookup"><span data-stu-id="b5224-185">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span> <span data-ttu-id="b5224-186">It is recommended to use a new default Blob container when you re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-186">It is recommended to use a new default Blob container when you re-create the cluster.</span></span>

1. <span data-ttu-id="b5224-187">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b5224-187">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b5224-188">Click **HDInsight Clusters** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="b5224-188">Click **HDInsight Clusters** from the left menu.</span></span> <span data-ttu-id="b5224-189">If you don't see **HDInsight Clusters**, click **More services** first.</span><span class="sxs-lookup"><span data-stu-id="b5224-189">If you don't see **HDInsight Clusters**, click **More services** first.</span></span>
3. <span data-ttu-id="b5224-190">Click the cluster that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="b5224-190">Click the cluster that you want to delete.</span></span>
4. <span data-ttu-id="b5224-191">Click **Delete** from the top menu, and then follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="b5224-191">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="b5224-192">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5224-192">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="b5224-193">Scale clusters</span><span class="sxs-lookup"><span data-stu-id="b5224-193">Scale clusters</span></span>
<span data-ttu-id="b5224-194">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-194">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b5224-195">Only clusters with HDInsight version 3.1.3 or higher are supported.</span><span class="sxs-lookup"><span data-stu-id="b5224-195">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="b5224-196">If you are unsure of the version of your cluster, you can check the Properties page.</span><span class="sxs-lookup"><span data-stu-id="b5224-196">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="b5224-197">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5224-197">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="b5224-198">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b5224-198">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="b5224-199">Hadoop</span><span class="sxs-lookup"><span data-stu-id="b5224-199">Hadoop</span></span>

    <span data-ttu-id="b5224-200">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span><span class="sxs-lookup"><span data-stu-id="b5224-200">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="b5224-201">New jobs can also be submitted while the operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="b5224-201">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="b5224-202">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span><span class="sxs-lookup"><span data-stu-id="b5224-202">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="b5224-203">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span><span class="sxs-lookup"><span data-stu-id="b5224-203">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="b5224-204">This causes all running and pending jobs to fail at the completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="b5224-204">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="b5224-205">You can, however, resubmit the jobs once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="b5224-205">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="b5224-206">HBase</span><span class="sxs-lookup"><span data-stu-id="b5224-206">HBase</span></span>

    <span data-ttu-id="b5224-207">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="b5224-207">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="b5224-208">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="b5224-208">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="b5224-209">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span><span class="sxs-lookup"><span data-stu-id="b5224-209">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="b5224-210">For more information on using the HBase shell, see []</span><span class="sxs-lookup"><span data-stu-id="b5224-210">For more information on using the HBase shell, see []</span></span>
* <span data-ttu-id="b5224-211">Storm</span><span class="sxs-lookup"><span data-stu-id="b5224-211">Storm</span></span>

    <span data-ttu-id="b5224-212">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="b5224-212">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="b5224-213">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span><span class="sxs-lookup"><span data-stu-id="b5224-213">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="b5224-214">Rebalancing can be accomplished in two ways:</span><span class="sxs-lookup"><span data-stu-id="b5224-214">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="b5224-215">Storm web UI</span><span class="sxs-lookup"><span data-stu-id="b5224-215">Storm web UI</span></span>
  * <span data-ttu-id="b5224-216">Command-line interface (CLI) tool</span><span class="sxs-lookup"><span data-stu-id="b5224-216">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="b5224-217">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span><span class="sxs-lookup"><span data-stu-id="b5224-217">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="b5224-218">The Storm web UI is available on the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="b5224-218">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight Storm scale rebalance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/hdinsight.portal.scale.cluster.storm.rebalance.png)

    <span data-ttu-id="b5224-220">Here is an example how to use the CLI command to rebalance the Storm topology:</span><span class="sxs-lookup"><span data-stu-id="b5224-220">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="b5224-221">**To scale clusters**</span><span class="sxs-lookup"><span data-stu-id="b5224-221">**To scale clusters**</span></span>

1. <span data-ttu-id="b5224-222">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b5224-222">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b5224-223">Click **HDInsight Clusters** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="b5224-223">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="b5224-224">Click the cluster you want to scale.</span><span class="sxs-lookup"><span data-stu-id="b5224-224">Click the cluster you want to scale.</span></span>
3. <span data-ttu-id="b5224-225">Click **Scale Cluster**.</span><span class="sxs-lookup"><span data-stu-id="b5224-225">Click **Scale Cluster**.</span></span>
4. <span data-ttu-id="b5224-226">Enter **Number of Worker nodes**.</span><span class="sxs-lookup"><span data-stu-id="b5224-226">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="b5224-227">The limit on the number of cluster node varies among Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b5224-227">The limit on the number of cluster node varies among Azure subscriptions.</span></span> <span data-ttu-id="b5224-228">You can contact billing support to increase the limit.</span><span class="sxs-lookup"><span data-stu-id="b5224-228">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="b5224-229">The cost information will reflect the changes you have made to the number of nodes.</span><span class="sxs-lookup"><span data-stu-id="b5224-229">The cost information will reflect the changes you have made to the number of nodes.</span></span>

    ![HDInsight hadoop hbase storm spark scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="b5224-231">Pause/shut down clusters</span><span class="sxs-lookup"><span data-stu-id="b5224-231">Pause/shut down clusters</span></span>

<span data-ttu-id="b5224-232">Most of Hadoop jobs are batch jobs that are only run occasionally.</span><span class="sxs-lookup"><span data-stu-id="b5224-232">Most of Hadoop jobs are batch jobs that are only run occasionally.</span></span> <span data-ttu-id="b5224-233">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span><span class="sxs-lookup"><span data-stu-id="b5224-233">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="b5224-234">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="b5224-234">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="b5224-235">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="b5224-235">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="b5224-236">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="b5224-236">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="b5224-237">There are many ways you can program the process:</span><span class="sxs-lookup"><span data-stu-id="b5224-237">There are many ways you can program the process:</span></span>

* <span data-ttu-id="b5224-238">User Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5224-238">User Azure Data Factory.</span></span> <span data-ttu-id="b5224-239">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span><span class="sxs-lookup"><span data-stu-id="b5224-239">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span></span>
* <span data-ttu-id="b5224-240">Use Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5224-240">Use Azure PowerShell.</span></span>  <span data-ttu-id="b5224-241">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-241">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="b5224-242">Use Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b5224-242">Use Azure CLI.</span></span> <span data-ttu-id="b5224-243">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-243">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="b5224-244">Use HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b5224-244">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="b5224-245">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-245">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="b5224-246">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b5224-246">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="b5224-247">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="b5224-247">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="change-passwords"></a><span data-ttu-id="b5224-248">Change passwords</span><span class="sxs-lookup"><span data-stu-id="b5224-248">Change passwords</span></span>
<span data-ttu-id="b5224-249">An HDInsight cluster can have two user accounts.</span><span class="sxs-lookup"><span data-stu-id="b5224-249">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="b5224-250">The HDInsight cluster user account (A.K.A.</span><span class="sxs-lookup"><span data-stu-id="b5224-250">The HDInsight cluster user account (A.K.A.</span></span> <span data-ttu-id="b5224-251">HTTP user account) and the SSH user account are created during the creation process.</span><span class="sxs-lookup"><span data-stu-id="b5224-251">HTTP user account) and the SSH user account are created during the creation process.</span></span> <span data-ttu-id="b5224-252">You can the Ambari web UI to change the cluster user account username and password, and script actions to change the SSH user account</span><span class="sxs-lookup"><span data-stu-id="b5224-252">You can the Ambari web UI to change the cluster user account username and password, and script actions to change the SSH user account</span></span>

### <a name="change-the-cluster-user-password"></a><span data-ttu-id="b5224-253">Change the cluster user password</span><span class="sxs-lookup"><span data-stu-id="b5224-253">Change the cluster user password</span></span>
<span data-ttu-id="b5224-254">You can use the Ambari Web UI to change the Cluster user password.</span><span class="sxs-lookup"><span data-stu-id="b5224-254">You can use the Ambari Web UI to change the Cluster user password.</span></span> <span data-ttu-id="b5224-255">To log into Ambari, you must use the existing cluster username and password.</span><span class="sxs-lookup"><span data-stu-id="b5224-255">To log into Ambari, you must use the existing cluster username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="b5224-256">If you change the cluster user (admin) password, this may cause script actions ran against this cluster to fail.</span><span class="sxs-lookup"><span data-stu-id="b5224-256">If you change the cluster user (admin) password, this may cause script actions ran against this cluster to fail.</span></span> <span data-ttu-id="b5224-257">If you have any persisted script actions that target worker nodes, these may fail when you add nodes to the cluster through resize operations.</span><span class="sxs-lookup"><span data-stu-id="b5224-257">If you have any persisted script actions that target worker nodes, these may fail when you add nodes to the cluster through resize operations.</span></span> <span data-ttu-id="b5224-258">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b5224-258">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="b5224-259">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span><span class="sxs-lookup"><span data-stu-id="b5224-259">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="b5224-260">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="b5224-260">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="b5224-261">Click **Admin** from the top menu, and then click "Manage Ambari".</span><span class="sxs-lookup"><span data-stu-id="b5224-261">Click **Admin** from the top menu, and then click "Manage Ambari".</span></span>
3. <span data-ttu-id="b5224-262">From the left menu, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b5224-262">From the left menu, click **Users**.</span></span>
4. <span data-ttu-id="b5224-263">Click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b5224-263">Click **Admin**.</span></span>
5. <span data-ttu-id="b5224-264">Click **Change Password**.</span><span class="sxs-lookup"><span data-stu-id="b5224-264">Click **Change Password**.</span></span>

<span data-ttu-id="b5224-265">Ambari then changes the password on all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-265">Ambari then changes the password on all nodes in the cluster.</span></span>

### <a name="change-the-ssh-user-password"></a><span data-ttu-id="b5224-266">Change the SSH user password</span><span class="sxs-lookup"><span data-stu-id="b5224-266">Change the SSH user password</span></span>
1. <span data-ttu-id="b5224-267">Using a text editor, save the following text as a file named **changepassword.sh**.</span><span class="sxs-lookup"><span data-stu-id="b5224-267">Using a text editor, save the following text as a file named **changepassword.sh**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b5224-268">You must use an editor that uses LF as the line ending.</span><span class="sxs-lookup"><span data-stu-id="b5224-268">You must use an editor that uses LF as the line ending.</span></span> <span data-ttu-id="b5224-269">If the editor uses CRLF, then the script will not work.</span><span class="sxs-lookup"><span data-stu-id="b5224-269">If the editor uses CRLF, then the script will not work.</span></span>
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. <span data-ttu-id="b5224-270">Upload the file to a storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span><span class="sxs-lookup"><span data-stu-id="b5224-270">Upload the file to a storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span></span> <span data-ttu-id="b5224-271">For example, a public file store such as OneDrive or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b5224-271">For example, a public file store such as OneDrive or Azure Blob storage.</span></span> <span data-ttu-id="b5224-272">Save the URI (HTTP or HTTPS address,) to the file, as this is needed in the next step.</span><span class="sxs-lookup"><span data-stu-id="b5224-272">Save the URI (HTTP or HTTPS address,) to the file, as this is needed in the next step.</span></span>
3. <span data-ttu-id="b5224-273">From the Azure portal, click **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="b5224-273">From the Azure portal, click **HDInsight Clusters**.</span></span>
4. <span data-ttu-id="b5224-274">Click your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-274">Click your HDInsight cluster.</span></span>
4. <span data-ttu-id="b5224-275">Click **Script Actions**.</span><span class="sxs-lookup"><span data-stu-id="b5224-275">Click **Script Actions**.</span></span>
4. <span data-ttu-id="b5224-276">From the **Script Actions** blade, select **Submit New**.</span><span class="sxs-lookup"><span data-stu-id="b5224-276">From the **Script Actions** blade, select **Submit New**.</span></span> <span data-ttu-id="b5224-277">When the **Submit script action** blade appears, enter the following information.</span><span class="sxs-lookup"><span data-stu-id="b5224-277">When the **Submit script action** blade appears, enter the following information.</span></span>

   | <span data-ttu-id="b5224-278">Field</span><span class="sxs-lookup"><span data-stu-id="b5224-278">Field</span></span> | <span data-ttu-id="b5224-279">Value</span><span class="sxs-lookup"><span data-stu-id="b5224-279">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="b5224-280">Name</span><span class="sxs-lookup"><span data-stu-id="b5224-280">Name</span></span> |<span data-ttu-id="b5224-281">Change ssh password</span><span class="sxs-lookup"><span data-stu-id="b5224-281">Change ssh password</span></span> |
   | <span data-ttu-id="b5224-282">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="b5224-282">Bash script URI</span></span> |<span data-ttu-id="b5224-283">The URI to the changepassword.sh file</span><span class="sxs-lookup"><span data-stu-id="b5224-283">The URI to the changepassword.sh file</span></span> |
   | <span data-ttu-id="b5224-284">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span><span class="sxs-lookup"><span data-stu-id="b5224-284">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span></span> |<span data-ttu-id="b5224-285">✓ for all node types listed</span><span class="sxs-lookup"><span data-stu-id="b5224-285">✓ for all node types listed</span></span> |
   | <span data-ttu-id="b5224-286">Parameters</span><span class="sxs-lookup"><span data-stu-id="b5224-286">Parameters</span></span> |<span data-ttu-id="b5224-287">Enter the SSH user name and then the new password.</span><span class="sxs-lookup"><span data-stu-id="b5224-287">Enter the SSH user name and then the new password.</span></span> <span data-ttu-id="b5224-288">There should be one space between the user name and the password.</span><span class="sxs-lookup"><span data-stu-id="b5224-288">There should be one space between the user name and the password.</span></span> |
   | <span data-ttu-id="b5224-289">Persist this script action ...</span><span class="sxs-lookup"><span data-stu-id="b5224-289">Persist this script action ...</span></span> |<span data-ttu-id="b5224-290">Leave this field unchecked.</span><span class="sxs-lookup"><span data-stu-id="b5224-290">Leave this field unchecked.</span></span> |
5. <span data-ttu-id="b5224-291">Select **Create** to apply the script.</span><span class="sxs-lookup"><span data-stu-id="b5224-291">Select **Create** to apply the script.</span></span> <span data-ttu-id="b5224-292">Once the script finishes, you will be able to connect to the cluster using SSH with the new password.</span><span class="sxs-lookup"><span data-stu-id="b5224-292">Once the script finishes, you will be able to connect to the cluster using SSH with the new password.</span></span>

## <a name="grantrevoke-access"></a><span data-ttu-id="b5224-293">Grant/revoke access</span><span class="sxs-lookup"><span data-stu-id="b5224-293">Grant/revoke access</span></span>
<span data-ttu-id="b5224-294">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span><span class="sxs-lookup"><span data-stu-id="b5224-294">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="b5224-295">ODBC</span><span class="sxs-lookup"><span data-stu-id="b5224-295">ODBC</span></span>
* <span data-ttu-id="b5224-296">JDBC</span><span class="sxs-lookup"><span data-stu-id="b5224-296">JDBC</span></span>
* <span data-ttu-id="b5224-297">Ambari</span><span class="sxs-lookup"><span data-stu-id="b5224-297">Ambari</span></span>
* <span data-ttu-id="b5224-298">Oozie</span><span class="sxs-lookup"><span data-stu-id="b5224-298">Oozie</span></span>
* <span data-ttu-id="b5224-299">Templeton</span><span class="sxs-lookup"><span data-stu-id="b5224-299">Templeton</span></span>

<span data-ttu-id="b5224-300">By default, these services are granted for access.</span><span class="sxs-lookup"><span data-stu-id="b5224-300">By default, these services are granted for access.</span></span> <span data-ttu-id="b5224-301">You can revoke/grant the access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span><span class="sxs-lookup"><span data-stu-id="b5224-301">You can revoke/grant the access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span></span>

## <a name="find-the-subscription-id"></a><span data-ttu-id="b5224-302">Find the subscription ID</span><span class="sxs-lookup"><span data-stu-id="b5224-302">Find the subscription ID</span></span>

<span data-ttu-id="b5224-303">**To find your Azure subscription IDs**</span><span class="sxs-lookup"><span data-stu-id="b5224-303">**To find your Azure subscription IDs**</span></span>

1. <span data-ttu-id="b5224-304">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b5224-304">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b5224-305">Click **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="b5224-305">Click **Subscriptions**.</span></span> <span data-ttu-id="b5224-306">Each subscription has a name and an ID.</span><span class="sxs-lookup"><span data-stu-id="b5224-306">Each subscription has a name and an ID.</span></span>

<span data-ttu-id="b5224-307">Each cluster is tied to an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b5224-307">Each cluster is tied to an Azure subscription.</span></span> <span data-ttu-id="b5224-308">The subscription ID is shown on the cluster **Essential** tile.</span><span class="sxs-lookup"><span data-stu-id="b5224-308">The subscription ID is shown on the cluster **Essential** tile.</span></span> <span data-ttu-id="b5224-309">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5224-309">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="b5224-310">Find the resource group</span><span class="sxs-lookup"><span data-stu-id="b5224-310">Find the resource group</span></span>
<span data-ttu-id="b5224-311">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span><span class="sxs-lookup"><span data-stu-id="b5224-311">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span></span> <span data-ttu-id="b5224-312">The Resource Manager group that a cluster belongs to appears in:</span><span class="sxs-lookup"><span data-stu-id="b5224-312">The Resource Manager group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="b5224-313">The cluster list has a **Resource Group** column.</span><span class="sxs-lookup"><span data-stu-id="b5224-313">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="b5224-314">Cluster **Essential** tile.</span><span class="sxs-lookup"><span data-stu-id="b5224-314">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="b5224-315">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5224-315">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="b5224-316">Find the default storage account</span><span class="sxs-lookup"><span data-stu-id="b5224-316">Find the default storage account</span></span>
<span data-ttu-id="b5224-317">Each HDInsight cluster has a default storage account.</span><span class="sxs-lookup"><span data-stu-id="b5224-317">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="b5224-318">The default storage account and its keys for a cluster appears under **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="b5224-318">The default storage account and its keys for a cluster appears under **Storage Accounts**.</span></span> <span data-ttu-id="b5224-319">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5224-319">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="run-hive-queries"></a><span data-ttu-id="b5224-320">Run Hive queries</span><span class="sxs-lookup"><span data-stu-id="b5224-320">Run Hive queries</span></span>
<span data-ttu-id="b5224-321">You cannot run Hive job directly from the Azure portal, but you can use the Hive View on Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="b5224-321">You cannot run Hive job directly from the Azure portal, but you can use the Hive View on Ambari Web UI.</span></span>

<span data-ttu-id="b5224-322">**To run Hive queries using Ambari Hive View**</span><span class="sxs-lookup"><span data-stu-id="b5224-322">**To run Hive queries using Ambari Hive View**</span></span>

1. <span data-ttu-id="b5224-323">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span><span class="sxs-lookup"><span data-stu-id="b5224-323">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="b5224-324">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="b5224-324">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="b5224-325">Open Hive View as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="b5224-325">Open Hive View as shown in the following screenshot:</span></span>  

    ![HDInsight hive view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. <span data-ttu-id="b5224-327">Click **Query** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="b5224-327">Click **Query** from the top menu.</span></span>
4. <span data-ttu-id="b5224-328">Enter a Hive query in **Query Editor**, and then click **Execute**.</span><span class="sxs-lookup"><span data-stu-id="b5224-328">Enter a Hive query in **Query Editor**, and then click **Execute**.</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="b5224-329">Monitor jobs</span><span class="sxs-lookup"><span data-stu-id="b5224-329">Monitor jobs</span></span>
<span data-ttu-id="b5224-330">See [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span><span class="sxs-lookup"><span data-stu-id="b5224-330">See [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span></span>

## <a name="browse-files"></a><span data-ttu-id="b5224-331">Browse files</span><span class="sxs-lookup"><span data-stu-id="b5224-331">Browse files</span></span>
<span data-ttu-id="b5224-332">Using the Azure portal, you can browse the content of the default container.</span><span class="sxs-lookup"><span data-stu-id="b5224-332">Using the Azure portal, you can browse the content of the default container.</span></span>

1. <span data-ttu-id="b5224-333">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5224-333">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5224-334">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span><span class="sxs-lookup"><span data-stu-id="b5224-334">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="b5224-335">Click the cluster name.</span><span class="sxs-lookup"><span data-stu-id="b5224-335">Click the cluster name.</span></span> <span data-ttu-id="b5224-336">If the cluster list is long, you can use filter on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="b5224-336">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="b5224-337">Click **Storage Accounts** from the cluster left menu.</span><span class="sxs-lookup"><span data-stu-id="b5224-337">Click **Storage Accounts** from the cluster left menu.</span></span>
5. <span data-ttu-id="b5224-338">click a storage account.</span><span class="sxs-lookup"><span data-stu-id="b5224-338">click a storage account.</span></span>
7. <span data-ttu-id="b5224-339">Click the **Blobs** tile.</span><span class="sxs-lookup"><span data-stu-id="b5224-339">Click the **Blobs** tile.</span></span>
8. <span data-ttu-id="b5224-340">Click the default container name.</span><span class="sxs-lookup"><span data-stu-id="b5224-340">Click the default container name.</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="b5224-341">Monitor cluster usage</span><span class="sxs-lookup"><span data-stu-id="b5224-341">Monitor cluster usage</span></span>
<span data-ttu-id="b5224-342">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span><span class="sxs-lookup"><span data-stu-id="b5224-342">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="b5224-343">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5224-343">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5224-344">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="b5224-344">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="b5224-345">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="b5224-345">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="connect-to-a-cluster"></a><span data-ttu-id="b5224-346">Connect to a cluster</span><span class="sxs-lookup"><span data-stu-id="b5224-346">Connect to a cluster</span></span>
<span data-ttu-id="b5224-347">See [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-beeline.md#a-idsshaconnect-with-ssh).</span><span class="sxs-lookup"><span data-stu-id="b5224-347">See [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-beeline.md#a-idsshaconnect-with-ssh).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5224-348">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5224-348">Next steps</span></span>
<span data-ttu-id="b5224-349">In this article, you have learned how to create an HDInsight cluster by using the Portal, and how to open the Hadoop command-line tool.</span><span class="sxs-lookup"><span data-stu-id="b5224-349">In this article, you have learned how to create an HDInsight cluster by using the Portal, and how to open the Hadoop command-line tool.</span></span> <span data-ttu-id="b5224-350">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="b5224-350">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="b5224-351">Administer HDInsight Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5224-351">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="b5224-352">Administer HDInsight Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b5224-352">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="b5224-353">Create HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="b5224-353">Create HDInsight clusters</span></span>](hdinsight-provision-clusters.md)
* [<span data-ttu-id="b5224-354">Use Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5224-354">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b5224-355">Use Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5224-355">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b5224-356">Use Sqoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5224-356">Use Sqoop in HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="b5224-357">Get Started with Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5224-357">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="b5224-358">What version of Hadoop is in Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="b5224-358">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop command line"






