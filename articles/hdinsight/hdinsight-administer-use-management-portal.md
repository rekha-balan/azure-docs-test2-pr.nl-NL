---
title: Manage Windows-based Hadoop clusters in HDInsight using the Azure portal | Microsoft Docs
description: Learn how to administer HDInsight Service. Create an HDInsight cluster, open the interactive JavaScript console, and open the Hadoop command console.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 04300805279de1fd1f5d0f83d687bc49b988a018
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550332"
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="3d815-104">Manage Windows-based Hadoop clusters in HDInsight by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3d815-104">Manage Windows-based Hadoop clusters in HDInsight by using the Azure portal</span></span>

<span data-ttu-id="3d815-105">Using the [Azure portal][azure-portal], you can create Windows-based Hadoop clusters in Azure HDInsight, change Hadoop user password, and enable Remote Desktop Protocol (RDP) so you can access the Hadoop command console on the cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-105">Using the [Azure portal][azure-portal], you can create Windows-based Hadoop clusters in Azure HDInsight, change Hadoop user password, and enable Remote Desktop Protocol (RDP) so you can access the Hadoop command console on the cluster.</span></span>

<span data-ttu-id="3d815-106">The information in this article only applies to Window-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="3d815-106">The information in this article only applies to Window-based HDInsight clusters.</span></span> <span data-ttu-id="3d815-107">For information on managing Linux-based clusters, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-107">For information on managing Linux-based clusters, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-portal-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d815-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="3d815-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3d815-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="3d815-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3d815-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3d815-110">Prerequisites</span></span>

<span data-ttu-id="3d815-111">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="3d815-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="3d815-112">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="3d815-112">**An Azure subscription**.</span></span> <span data-ttu-id="3d815-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3d815-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="3d815-114">**Azure Storage account** - An HDInsight cluster uses an Azure Blob storage container as the default file system.</span><span class="sxs-lookup"><span data-stu-id="3d815-114">**Azure Storage account** - An HDInsight cluster uses an Azure Blob storage container as the default file system.</span></span> <span data-ttu-id="3d815-115">For more information about how Azure Blob storage provides a seamless experience with HDInsight clusters, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-115">For more information about how Azure Blob storage provides a seamless experience with HDInsight clusters, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="3d815-116">For details on creating an Azure Storage account, see [How to Create a Storage Account](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-116">For details on creating an Azure Storage account, see [How to Create a Storage Account](../storage/storage-create-storage-account.md).</span></span>

## <a name="open-the-portal"></a><span data-ttu-id="3d815-117">Open the Portal</span><span class="sxs-lookup"><span data-stu-id="3d815-117">Open the Portal</span></span>
1. <span data-ttu-id="3d815-118">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d815-118">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3d815-119">After you open the portal, you can:</span><span class="sxs-lookup"><span data-stu-id="3d815-119">After you open the portal, you can:</span></span>

   * <span data-ttu-id="3d815-120">Click **New** from the left menu to create a new cluster:</span><span class="sxs-lookup"><span data-stu-id="3d815-120">Click **New** from the left menu to create a new cluster:</span></span>

       ![new HDInsight cluster button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * <span data-ttu-id="3d815-122">Click **HDInsight Clusters** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="3d815-122">Click **HDInsight Clusters** from the left menu.</span></span>

       ![Azure portal HDInsight cluster button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     <span data-ttu-id="3d815-124">If **HDInsight** doesn't appear in the left menu, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="3d815-124">If **HDInsight** doesn't appear in the left menu, click **Browse**.</span></span>

     ![Azure portal Browse cluster button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a><span data-ttu-id="3d815-126">Create clusters</span><span class="sxs-lookup"><span data-stu-id="3d815-126">Create clusters</span></span>
<span data-ttu-id="3d815-127">For the creation instructions using the Portal, see [Create HDInsight clusters](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-127">For the creation instructions using the Portal, see [Create HDInsight clusters](hdinsight-provision-clusters.md).</span></span>

<span data-ttu-id="3d815-128">HDInsight works with a wide range of Hadoop components.</span><span class="sxs-lookup"><span data-stu-id="3d815-128">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="3d815-129">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-129">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="3d815-130">You can customize HDInsight by using one of the following options:</span><span class="sxs-lookup"><span data-stu-id="3d815-130">You can customize HDInsight by using one of the following options:</span></span>

* <span data-ttu-id="3d815-131">Use Script Action to run custom scripts that can customize a cluster to either change cluster configuration or install custom components such as Giraph or Solr.</span><span class="sxs-lookup"><span data-stu-id="3d815-131">Use Script Action to run custom scripts that can customize a cluster to either change cluster configuration or install custom components such as Giraph or Solr.</span></span> <span data-ttu-id="3d815-132">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-132">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span>
* <span data-ttu-id="3d815-133">Use the cluster customization parameters in the HDInsight .NET SDK or Azure PowerShell during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="3d815-133">Use the cluster customization parameters in the HDInsight .NET SDK or Azure PowerShell during cluster creation.</span></span> <span data-ttu-id="3d815-134">These configuration changes are then preserved through the lifetime of the cluster and are not affected by cluster node reimages that Azure platform periodically performs for maintenance.</span><span class="sxs-lookup"><span data-stu-id="3d815-134">These configuration changes are then preserved through the lifetime of the cluster and are not affected by cluster node reimages that Azure platform periodically performs for maintenance.</span></span> <span data-ttu-id="3d815-135">For more information on using the cluster customization parameters, see [Create HDInsight clusters](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-135">For more information on using the cluster customization parameters, see [Create HDInsight clusters](hdinsight-provision-clusters.md).</span></span>
* <span data-ttu-id="3d815-136">Some native Java components, like Mahout and Cascading, can be run on the cluster as JAR files.</span><span class="sxs-lookup"><span data-stu-id="3d815-136">Some native Java components, like Mahout and Cascading, can be run on the cluster as JAR files.</span></span> <span data-ttu-id="3d815-137">These JAR files can be distributed to Azure Blob storage, and submitted to HDInsight clusters through Hadoop job submission mechanisms.</span><span class="sxs-lookup"><span data-stu-id="3d815-137">These JAR files can be distributed to Azure Blob storage, and submitted to HDInsight clusters through Hadoop job submission mechanisms.</span></span> <span data-ttu-id="3d815-138">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-138">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

  > [!NOTE]
  > <span data-ttu-id="3d815-139">If you have issues deploying JAR files to HDInsight clusters or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="3d815-139">If you have issues deploying JAR files to HDInsight clusters or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
  >
  > <span data-ttu-id="3d815-140">Cascading is not supported by HDInsight, and is not eligible for Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="3d815-140">Cascading is not supported by HDInsight, and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="3d815-141">For lists of supported components, see [What's new in the cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-141">For lists of supported components, see [What's new in the cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
  >
  >

<span data-ttu-id="3d815-142">Installation of custom software on the cluster by using Remote Desktop Connection is not supported.</span><span class="sxs-lookup"><span data-stu-id="3d815-142">Installation of custom software on the cluster by using Remote Desktop Connection is not supported.</span></span> <span data-ttu-id="3d815-143">You should avoid storing any files on the drives of the head node, as they will be lost if you need to re-create the clusters.</span><span class="sxs-lookup"><span data-stu-id="3d815-143">You should avoid storing any files on the drives of the head node, as they will be lost if you need to re-create the clusters.</span></span> <span data-ttu-id="3d815-144">We recommend storing files on Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3d815-144">We recommend storing files on Azure Blob storage.</span></span> <span data-ttu-id="3d815-145">Blob storage is persistent.</span><span class="sxs-lookup"><span data-stu-id="3d815-145">Blob storage is persistent.</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="3d815-146">List and show clusters</span><span class="sxs-lookup"><span data-stu-id="3d815-146">List and show clusters</span></span>
1. <span data-ttu-id="3d815-147">Sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d815-147">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3d815-148">Click **HDInsight Clusters** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="3d815-148">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="3d815-149">Click the cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-149">Click the cluster name.</span></span> <span data-ttu-id="3d815-150">If the cluster list is long, you can use filter on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="3d815-150">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="3d815-151">Double-click a cluster from the list to show the details.</span><span class="sxs-lookup"><span data-stu-id="3d815-151">Double-click a cluster from the list to show the details.</span></span>

    <span data-ttu-id="3d815-152">**Menu and essentials**:</span><span class="sxs-lookup"><span data-stu-id="3d815-152">**Menu and essentials**:</span></span>

    ![Azure portal HDInsight cluster essentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * <span data-ttu-id="3d815-154">To customize the menu, right-click anywhere on the menu, and then click **Customize**.</span><span class="sxs-lookup"><span data-stu-id="3d815-154">To customize the menu, right-click anywhere on the menu, and then click **Customize**.</span></span>
   * <span data-ttu-id="3d815-155">**Settings** and **All Settings**: Displays the **Settings** blade for the cluster, which allows you to access detailed configuration information for the cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-155">**Settings** and **All Settings**: Displays the **Settings** blade for the cluster, which allows you to access detailed configuration information for the cluster.</span></span>
   * <span data-ttu-id="3d815-156">**Dashboard**, **Cluster Dashboard** and **URL: These are all ways to access the cluster dashboard, which is Ambari Web for Linux-based clusters. -** Secure Shell\*\*: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span><span class="sxs-lookup"><span data-stu-id="3d815-156">**Dashboard**, **Cluster Dashboard** and **URL: These are all ways to access the cluster dashboard, which is Ambari Web for Linux-based clusters. -** Secure Shell\*\*: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
   * <span data-ttu-id="3d815-157">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-157">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
   * <span data-ttu-id="3d815-158">**Delete**: Deletes the cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-158">**Delete**: Deletes the cluster.</span></span>
   * <span data-ttu-id="3d815-159">**Quickstart (![cloud and thunderbolt icon = quickstart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/quickstart.png))**: Displays information that will help you get started using HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3d815-159">**Quickstart (![cloud and thunderbolt icon = quickstart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/quickstart.png))**: Displays information that will help you get started using HDInsight.</span></span>
   * <span data-ttu-id="3d815-160">**Users (![users icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/users.png))**: Allows you to set permissions for *portal management* of this cluster for other users on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3d815-160">**Users (![users icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/users.png))**: Allows you to set permissions for *portal management* of this cluster for other users on your Azure subscription.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="3d815-161">This *only* affects access and permissions to this cluster in the Azure portal, and has no effect on who can connect to or submit jobs to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-161">This *only* affects access and permissions to this cluster in the Azure portal, and has no effect on who can connect to or submit jobs to the HDInsight cluster.</span></span>
     >
     >
   * <span data-ttu-id="3d815-162">**Tags (![tag icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/tags.png))**: Tags allow you to set key/value pairs to define a custom taxonomy of your cloud services.</span><span class="sxs-lookup"><span data-stu-id="3d815-162">**Tags (![tag icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-portal-linux/tags.png))**: Tags allow you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="3d815-163">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span><span class="sxs-lookup"><span data-stu-id="3d815-163">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
   * <span data-ttu-id="3d815-164">**Ambari Views**: Links to Ambari Web.</span><span class="sxs-lookup"><span data-stu-id="3d815-164">**Ambari Views**: Links to Ambari Web.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="3d815-165">To manage the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="3d815-165">To manage the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="3d815-166">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-166">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
     >
     >

     <span data-ttu-id="3d815-167">**Usage**:</span><span class="sxs-lookup"><span data-stu-id="3d815-167">**Usage**:</span></span>

     ![Azure portal HDInsight cluster usage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. <span data-ttu-id="3d815-169">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="3d815-169">Click **Settings**.</span></span>

    ![Azure portal HDInsight cluster usage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * <span data-ttu-id="3d815-171">**Properties**: View the cluster properties.</span><span class="sxs-lookup"><span data-stu-id="3d815-171">**Properties**: View the cluster properties.</span></span>
   * <span data-ttu-id="3d815-172">**Cluster AAD Identity**:</span><span class="sxs-lookup"><span data-stu-id="3d815-172">**Cluster AAD Identity**:</span></span>
   * <span data-ttu-id="3d815-173">**Azure Storage Keys**: View the default storage account and its key.</span><span class="sxs-lookup"><span data-stu-id="3d815-173">**Azure Storage Keys**: View the default storage account and its key.</span></span> <span data-ttu-id="3d815-174">The storage account is configuration during the cluster creation process.</span><span class="sxs-lookup"><span data-stu-id="3d815-174">The storage account is configuration during the cluster creation process.</span></span>
   * <span data-ttu-id="3d815-175">**Cluster Login**: Change the cluster HTTP user name and password.</span><span class="sxs-lookup"><span data-stu-id="3d815-175">**Cluster Login**: Change the cluster HTTP user name and password.</span></span>
   * <span data-ttu-id="3d815-176">**External Metastores**: View the Hive and Oozie metastores.</span><span class="sxs-lookup"><span data-stu-id="3d815-176">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="3d815-177">The metastores can only be configured during the cluster creation process.</span><span class="sxs-lookup"><span data-stu-id="3d815-177">The metastores can only be configured during the cluster creation process.</span></span>
   * <span data-ttu-id="3d815-178">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span><span class="sxs-lookup"><span data-stu-id="3d815-178">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span>
   * <span data-ttu-id="3d815-179">**Remote Desktop**: Enable and disable remote desktop (RDP) access, and configure the RDP username.</span><span class="sxs-lookup"><span data-stu-id="3d815-179">**Remote Desktop**: Enable and disable remote desktop (RDP) access, and configure the RDP username.</span></span>  <span data-ttu-id="3d815-180">The RDP user name must be different from the HTTP user name.</span><span class="sxs-lookup"><span data-stu-id="3d815-180">The RDP user name must be different from the HTTP user name.</span></span>
   * <span data-ttu-id="3d815-181">**Partner of Record**:</span><span class="sxs-lookup"><span data-stu-id="3d815-181">**Partner of Record**:</span></span>

     > [!NOTE]
     > <span data-ttu-id="3d815-182">This is a generic list of available settings; not all of them will be present for all cluster types.</span><span class="sxs-lookup"><span data-stu-id="3d815-182">This is a generic list of available settings; not all of them will be present for all cluster types.</span></span>
     >
     >
6. <span data-ttu-id="3d815-183">Click **Properties**:</span><span class="sxs-lookup"><span data-stu-id="3d815-183">Click **Properties**:</span></span>

    <span data-ttu-id="3d815-184">The properties section lists the following:</span><span class="sxs-lookup"><span data-stu-id="3d815-184">The properties section lists the following:</span></span>

   * <span data-ttu-id="3d815-185">**Hostname**: Cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="3d815-186">**Cluster URL**.</span><span class="sxs-lookup"><span data-stu-id="3d815-186">**Cluster URL**.</span></span>
   * <span data-ttu-id="3d815-187">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="3d815-187">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="3d815-188">**Region**: Azure location.</span><span class="sxs-lookup"><span data-stu-id="3d815-188">**Region**: Azure location.</span></span> <span data-ttu-id="3d815-189">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3d815-189">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="3d815-190">**Data created**.</span><span class="sxs-lookup"><span data-stu-id="3d815-190">**Data created**.</span></span>
   * <span data-ttu-id="3d815-191">**Operating system**: Either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="3d815-191">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="3d815-192">**Type**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="3d815-192">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="3d815-193">**Version**.</span><span class="sxs-lookup"><span data-stu-id="3d815-193">**Version**.</span></span> <span data-ttu-id="3d815-194">See [HDInsight versions](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="3d815-194">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="3d815-195">**Subscription**: Subscription name.</span><span class="sxs-lookup"><span data-stu-id="3d815-195">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="3d815-196">**Subscription ID**.</span><span class="sxs-lookup"><span data-stu-id="3d815-196">**Subscription ID**.</span></span>
   * <span data-ttu-id="3d815-197">**Primary data source**.</span><span class="sxs-lookup"><span data-stu-id="3d815-197">**Primary data source**.</span></span> <span data-ttu-id="3d815-198">The Azure Blob storage account used as the default Hadoop file system.</span><span class="sxs-lookup"><span data-stu-id="3d815-198">The Azure Blob storage account used as the default Hadoop file system.</span></span>
   * <span data-ttu-id="3d815-199">**Worker nodes pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="3d815-199">**Worker nodes pricing tier**.</span></span>
   * <span data-ttu-id="3d815-200">**Head node pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="3d815-200">**Head node pricing tier**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="3d815-201">Delete clusters</span><span class="sxs-lookup"><span data-stu-id="3d815-201">Delete clusters</span></span>
<span data-ttu-id="3d815-202">Delete a cluster will not delete the default storage account or any linked storage accounts.</span><span class="sxs-lookup"><span data-stu-id="3d815-202">Delete a cluster will not delete the default storage account or any linked storage accounts.</span></span> <span data-ttu-id="3d815-203">You can re-create the cluster by using the same storage accounts and the same metastores.</span><span class="sxs-lookup"><span data-stu-id="3d815-203">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span>

1. <span data-ttu-id="3d815-204">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3d815-204">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="3d815-205">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-205">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="3d815-206">Click **Delete** from the top menu, and then follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="3d815-206">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="3d815-207">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span><span class="sxs-lookup"><span data-stu-id="3d815-207">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="3d815-208">Scale clusters</span><span class="sxs-lookup"><span data-stu-id="3d815-208">Scale clusters</span></span>
<span data-ttu-id="3d815-209">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-209">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3d815-210">Only clusters with HDInsight version 3.1.3 or higher are supported.</span><span class="sxs-lookup"><span data-stu-id="3d815-210">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="3d815-211">If you are unsure of the version of your cluster, you can check the Properties page.</span><span class="sxs-lookup"><span data-stu-id="3d815-211">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="3d815-212">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="3d815-212">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="3d815-213">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3d815-213">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="3d815-214">Hadoop</span><span class="sxs-lookup"><span data-stu-id="3d815-214">Hadoop</span></span>

    <span data-ttu-id="3d815-215">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span><span class="sxs-lookup"><span data-stu-id="3d815-215">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="3d815-216">New jobs can also be submitted while the operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="3d815-216">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="3d815-217">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span><span class="sxs-lookup"><span data-stu-id="3d815-217">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="3d815-218">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span><span class="sxs-lookup"><span data-stu-id="3d815-218">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="3d815-219">This causes all running and pending jobs to fail at the completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="3d815-219">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="3d815-220">You can, however, resubmit the jobs once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="3d815-220">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="3d815-221">HBase</span><span class="sxs-lookup"><span data-stu-id="3d815-221">HBase</span></span>

    <span data-ttu-id="3d815-222">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="3d815-222">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="3d815-223">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="3d815-223">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="3d815-224">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span><span class="sxs-lookup"><span data-stu-id="3d815-224">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="3d815-225">For more information on using the HBase shell, see []</span><span class="sxs-lookup"><span data-stu-id="3d815-225">For more information on using the HBase shell, see []</span></span>
* <span data-ttu-id="3d815-226">Storm</span><span class="sxs-lookup"><span data-stu-id="3d815-226">Storm</span></span>

    <span data-ttu-id="3d815-227">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="3d815-227">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="3d815-228">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span><span class="sxs-lookup"><span data-stu-id="3d815-228">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="3d815-229">Rebalancing can be accomplished in two ways:</span><span class="sxs-lookup"><span data-stu-id="3d815-229">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="3d815-230">Storm web UI</span><span class="sxs-lookup"><span data-stu-id="3d815-230">Storm web UI</span></span>
  * <span data-ttu-id="3d815-231">Command-line interface (CLI) tool</span><span class="sxs-lookup"><span data-stu-id="3d815-231">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="3d815-232">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span><span class="sxs-lookup"><span data-stu-id="3d815-232">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="3d815-233">The Storm web UI is available on the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="3d815-233">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight storm scale rebalance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.storm.rebalance.png)

    <span data-ttu-id="3d815-235">Here is an example how to use the CLI command to rebalance the Storm topology:</span><span class="sxs-lookup"><span data-stu-id="3d815-235">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="3d815-236">**To scale clusters**</span><span class="sxs-lookup"><span data-stu-id="3d815-236">**To scale clusters**</span></span>

1. <span data-ttu-id="3d815-237">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3d815-237">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="3d815-238">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-238">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="3d815-239">Click **Settings** from the top menu, and then click **Scale Cluster**.</span><span class="sxs-lookup"><span data-stu-id="3d815-239">Click **Settings** from the top menu, and then click **Scale Cluster**.</span></span>
4. <span data-ttu-id="3d815-240">Enter **Number of Worker nodes**.</span><span class="sxs-lookup"><span data-stu-id="3d815-240">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="3d815-241">The limit on the number of cluster node varies among Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3d815-241">The limit on the number of cluster node varies among Azure subscriptions.</span></span> <span data-ttu-id="3d815-242">You can contact billing support to increase the limit.</span><span class="sxs-lookup"><span data-stu-id="3d815-242">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="3d815-243">The cost information will reflect the changes you have made to the number of nodes.</span><span class="sxs-lookup"><span data-stu-id="3d815-243">The cost information will reflect the changes you have made to the number of nodes.</span></span>

    ![HDInsight Hadoop HBase Storm Spark scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="3d815-245">Pause/shut down clusters</span><span class="sxs-lookup"><span data-stu-id="3d815-245">Pause/shut down clusters</span></span>
<span data-ttu-id="3d815-246">Most of Hadoop jobs are batch jobs that are only ran occasionally.</span><span class="sxs-lookup"><span data-stu-id="3d815-246">Most of Hadoop jobs are batch jobs that are only ran occasionally.</span></span> <span data-ttu-id="3d815-247">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span><span class="sxs-lookup"><span data-stu-id="3d815-247">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="3d815-248">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="3d815-248">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="3d815-249">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="3d815-249">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="3d815-250">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="3d815-250">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="3d815-251">There are many ways you can program the process:</span><span class="sxs-lookup"><span data-stu-id="3d815-251">There are many ways you can program the process:</span></span>

* <span data-ttu-id="3d815-252">User Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3d815-252">User Azure Data Factory.</span></span> <span data-ttu-id="3d815-253">See [Azure HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md) and [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) for on-demand and self-defined HDInsight linked services.</span><span class="sxs-lookup"><span data-stu-id="3d815-253">See [Azure HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md) and [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) for on-demand and self-defined HDInsight linked services.</span></span>
* <span data-ttu-id="3d815-254">Use Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d815-254">Use Azure PowerShell.</span></span>  <span data-ttu-id="3d815-255">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-255">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="3d815-256">Use Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3d815-256">Use Azure CLI.</span></span> <span data-ttu-id="3d815-257">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-257">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="3d815-258">Use HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="3d815-258">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="3d815-259">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-259">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="3d815-260">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3d815-260">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="3d815-261">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="3d815-261">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="change-cluster-username"></a><span data-ttu-id="3d815-262">Change cluster username</span><span class="sxs-lookup"><span data-stu-id="3d815-262">Change cluster username</span></span>
<span data-ttu-id="3d815-263">An HDInsight cluster can have two user accounts.</span><span class="sxs-lookup"><span data-stu-id="3d815-263">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="3d815-264">The HDInsight cluster user account is created during the creation process.</span><span class="sxs-lookup"><span data-stu-id="3d815-264">The HDInsight cluster user account is created during the creation process.</span></span> <span data-ttu-id="3d815-265">You can also create an RDP user account for accessing the cluster via RDP.</span><span class="sxs-lookup"><span data-stu-id="3d815-265">You can also create an RDP user account for accessing the cluster via RDP.</span></span> <span data-ttu-id="3d815-266">See [Enable remote desktop](#connect-to-hdinsight-clusters-by-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="3d815-266">See [Enable remote desktop](#connect-to-hdinsight-clusters-by-using-rdp).</span></span>

<span data-ttu-id="3d815-267">**To change the HDInsight cluster user name and password**</span><span class="sxs-lookup"><span data-stu-id="3d815-267">**To change the HDInsight cluster user name and password**</span></span>

1. <span data-ttu-id="3d815-268">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3d815-268">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="3d815-269">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-269">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="3d815-270">Click **Settings** from the top menu, and then click **Cluster Login**.</span><span class="sxs-lookup"><span data-stu-id="3d815-270">Click **Settings** from the top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="3d815-271">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span><span class="sxs-lookup"><span data-stu-id="3d815-271">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span></span>
5. <span data-ttu-id="3d815-272">Change the **Cluster Login Name** and/or the **Cluster Login Password**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3d815-272">Change the **Cluster Login Name** and/or the **Cluster Login Password**, and then click **Save**.</span></span>

    ![HDInsight change cluster user username password http user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a><span data-ttu-id="3d815-274">Grant/revoke access</span><span class="sxs-lookup"><span data-stu-id="3d815-274">Grant/revoke access</span></span>
<span data-ttu-id="3d815-275">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span><span class="sxs-lookup"><span data-stu-id="3d815-275">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="3d815-276">ODBC</span><span class="sxs-lookup"><span data-stu-id="3d815-276">ODBC</span></span>
* <span data-ttu-id="3d815-277">JDBC</span><span class="sxs-lookup"><span data-stu-id="3d815-277">JDBC</span></span>
* <span data-ttu-id="3d815-278">Ambari</span><span class="sxs-lookup"><span data-stu-id="3d815-278">Ambari</span></span>
* <span data-ttu-id="3d815-279">Oozie</span><span class="sxs-lookup"><span data-stu-id="3d815-279">Oozie</span></span>
* <span data-ttu-id="3d815-280">Templeton</span><span class="sxs-lookup"><span data-stu-id="3d815-280">Templeton</span></span>

<span data-ttu-id="3d815-281">By default, these services are granted for access.</span><span class="sxs-lookup"><span data-stu-id="3d815-281">By default, these services are granted for access.</span></span> <span data-ttu-id="3d815-282">You can revoke/grant the access from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3d815-282">You can revoke/grant the access from the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3d815-283">By granting/revoking the access, you will reset the cluster user name and password.</span><span class="sxs-lookup"><span data-stu-id="3d815-283">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="3d815-284">**To grant/revoke HTTP web services access**</span><span class="sxs-lookup"><span data-stu-id="3d815-284">**To grant/revoke HTTP web services access**</span></span>

1. <span data-ttu-id="3d815-285">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3d815-285">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="3d815-286">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-286">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="3d815-287">Click **Settings** from the top menu, and then click **Cluster Login**.</span><span class="sxs-lookup"><span data-stu-id="3d815-287">Click **Settings** from the top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="3d815-288">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span><span class="sxs-lookup"><span data-stu-id="3d815-288">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span></span>
5. <span data-ttu-id="3d815-289">For **Cluster Login Username** and **Cluster Login Password**, enter the new user name and password (respectively) for the cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-289">For **Cluster Login Username** and **Cluster Login Password**, enter the new user name and password (respectively) for the cluster.</span></span>
6. <span data-ttu-id="3d815-290">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="3d815-290">Click **SAVE**.</span></span>

    ![HDInsight grand remove http web service access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-the-default-storage-account"></a><span data-ttu-id="3d815-292">Find the default storage account</span><span class="sxs-lookup"><span data-stu-id="3d815-292">Find the default storage account</span></span>
<span data-ttu-id="3d815-293">Each HDInsight cluster has a default storage account.</span><span class="sxs-lookup"><span data-stu-id="3d815-293">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="3d815-294">The default storage account and its keys for a cluster appears under **Settings**/**Properties**/**Azure Storage Keys**.</span><span class="sxs-lookup"><span data-stu-id="3d815-294">The default storage account and its keys for a cluster appears under **Settings**/**Properties**/**Azure Storage Keys**.</span></span> <span data-ttu-id="3d815-295">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="3d815-295">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="3d815-296">Find the resource group</span><span class="sxs-lookup"><span data-stu-id="3d815-296">Find the resource group</span></span>
<span data-ttu-id="3d815-297">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="3d815-297">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure resource group.</span></span> <span data-ttu-id="3d815-298">The Azure resource group that a cluster belongs to appears in:</span><span class="sxs-lookup"><span data-stu-id="3d815-298">The Azure resource group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="3d815-299">The cluster list has a **Resource Group** column.</span><span class="sxs-lookup"><span data-stu-id="3d815-299">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="3d815-300">Cluster **Essential** tile.</span><span class="sxs-lookup"><span data-stu-id="3d815-300">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="3d815-301">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="3d815-301">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="open-hdinsight-query-console"></a><span data-ttu-id="3d815-302">Open HDInsight Query console</span><span class="sxs-lookup"><span data-stu-id="3d815-302">Open HDInsight Query console</span></span>
<span data-ttu-id="3d815-303">The HDInsight Query console includes the following features:</span><span class="sxs-lookup"><span data-stu-id="3d815-303">The HDInsight Query console includes the following features:</span></span>

* <span data-ttu-id="3d815-304">**Hive Editor**: A GUI web interface for submitting Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="3d815-304">**Hive Editor**: A GUI web interface for submitting Hive jobs.</span></span>  <span data-ttu-id="3d815-305">See [Run Hive queries using the Query Console](hdinsight-hadoop-use-hive-query-console.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-305">See [Run Hive queries using the Query Console](hdinsight-hadoop-use-hive-query-console.md).</span></span>

    ![HDInsight portal hive editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* <span data-ttu-id="3d815-307">**Job history**: Monitor Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="3d815-307">**Job history**: Monitor Hadoop jobs.</span></span>  

    ![HDInsight portal job history](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    <span data-ttu-id="3d815-309">Click **Query Name** to show the details including Job properties, **Job Query**, and \*\*Job Output.</span><span class="sxs-lookup"><span data-stu-id="3d815-309">Click **Query Name** to show the details including Job properties, **Job Query**, and \*\*Job Output.</span></span> <span data-ttu-id="3d815-310">You can also download both the query and the output to your workstation.</span><span class="sxs-lookup"><span data-stu-id="3d815-310">You can also download both the query and the output to your workstation.</span></span>
* <span data-ttu-id="3d815-311">**File Browser**: Browse the default storage account and the linked storage accounts.</span><span class="sxs-lookup"><span data-stu-id="3d815-311">**File Browser**: Browse the default storage account and the linked storage accounts.</span></span>

    ![HDInsight portal file browser browse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    <span data-ttu-id="3d815-313">On the screenshot, the **<Account>** type indicates the item is an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="3d815-313">On the screenshot, the **<Account>** type indicates the item is an Azure storage account.</span></span>  <span data-ttu-id="3d815-314">Click the account name to browse the files.</span><span class="sxs-lookup"><span data-stu-id="3d815-314">Click the account name to browse the files.</span></span>
* <span data-ttu-id="3d815-315">**Hadoop UI**.</span><span class="sxs-lookup"><span data-stu-id="3d815-315">**Hadoop UI**.</span></span>

    ![HDInsight portal Hadoop UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    <span data-ttu-id="3d815-317">From \**Hadoop UI*, you can browse files, and check logs.</span><span class="sxs-lookup"><span data-stu-id="3d815-317">From \**Hadoop UI*, you can browse files, and check logs.</span></span>
* <span data-ttu-id="3d815-318">**Yarn UI**.</span><span class="sxs-lookup"><span data-stu-id="3d815-318">**Yarn UI**.</span></span>

    ![HDInsight portal YARN UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a><span data-ttu-id="3d815-320">Run Hive queries</span><span class="sxs-lookup"><span data-stu-id="3d815-320">Run Hive queries</span></span>
<span data-ttu-id="3d815-321">To ran Hive jobs from the Portal, click **Hive Editor** in the HDInsight Query console.</span><span class="sxs-lookup"><span data-stu-id="3d815-321">To ran Hive jobs from the Portal, click **Hive Editor** in the HDInsight Query console.</span></span> <span data-ttu-id="3d815-322">See [Open HDInsight Query console](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="3d815-322">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="3d815-323">Monitor jobs</span><span class="sxs-lookup"><span data-stu-id="3d815-323">Monitor jobs</span></span>
<span data-ttu-id="3d815-324">To monitor jobs from the Portal, click **Job History** in the HDInsight Query console.</span><span class="sxs-lookup"><span data-stu-id="3d815-324">To monitor jobs from the Portal, click **Job History** in the HDInsight Query console.</span></span> <span data-ttu-id="3d815-325">See [Open HDInsight Query console](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="3d815-325">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="browse-files"></a><span data-ttu-id="3d815-326">Browse files</span><span class="sxs-lookup"><span data-stu-id="3d815-326">Browse files</span></span>
<span data-ttu-id="3d815-327">To browse files stored in the default storage account and the linked storage accounts, click **File Browser** in the HDInsight Query console.</span><span class="sxs-lookup"><span data-stu-id="3d815-327">To browse files stored in the default storage account and the linked storage accounts, click **File Browser** in the HDInsight Query console.</span></span> <span data-ttu-id="3d815-328">See [Open HDInsight Query console](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="3d815-328">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

<span data-ttu-id="3d815-329">You can also use the **Browse the file system** utility from the **Hadoop UI** in the HDInsight console.</span><span class="sxs-lookup"><span data-stu-id="3d815-329">You can also use the **Browse the file system** utility from the **Hadoop UI** in the HDInsight console.</span></span>  <span data-ttu-id="3d815-330">See [Open HDInsight Query console](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="3d815-330">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="3d815-331">Monitor cluster usage</span><span class="sxs-lookup"><span data-stu-id="3d815-331">Monitor cluster usage</span></span>
<span data-ttu-id="3d815-332">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-332">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="3d815-333">See [List and show clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="3d815-333">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d815-334">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="3d815-334">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="3d815-335">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="3d815-335">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="open-hadoop-ui"></a><span data-ttu-id="3d815-336">Open Hadoop UI</span><span class="sxs-lookup"><span data-stu-id="3d815-336">Open Hadoop UI</span></span>
<span data-ttu-id="3d815-337">To monitor the cluster, browse the file system, and check logs, click **Hadoop UI** in the HDInsight Query console.</span><span class="sxs-lookup"><span data-stu-id="3d815-337">To monitor the cluster, browse the file system, and check logs, click **Hadoop UI** in the HDInsight Query console.</span></span> <span data-ttu-id="3d815-338">See [Open HDInsight Query console](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="3d815-338">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="open-yarn-ui"></a><span data-ttu-id="3d815-339">Open Yarn UI</span><span class="sxs-lookup"><span data-stu-id="3d815-339">Open Yarn UI</span></span>
<span data-ttu-id="3d815-340">To use Yarn user interface, click **Yarn UI** in the HDInsight Query console.</span><span class="sxs-lookup"><span data-stu-id="3d815-340">To use Yarn user interface, click **Yarn UI** in the HDInsight Query console.</span></span> <span data-ttu-id="3d815-341">See [Open HDInsight Query console](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="3d815-341">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="connect-to-clusters-using-rdp"></a><span data-ttu-id="3d815-342">Connect to clusters using RDP</span><span class="sxs-lookup"><span data-stu-id="3d815-342">Connect to clusters using RDP</span></span>
<span data-ttu-id="3d815-343">The credentials for the cluster that you provided at its creation give access to the services on the cluster, but not to the cluster itself through Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="3d815-343">The credentials for the cluster that you provided at its creation give access to the services on the cluster, but not to the cluster itself through Remote Desktop.</span></span> <span data-ttu-id="3d815-344">You can turn on Remote Desktop access when you provision a cluster or after a cluster is provisioned.</span><span class="sxs-lookup"><span data-stu-id="3d815-344">You can turn on Remote Desktop access when you provision a cluster or after a cluster is provisioned.</span></span> <span data-ttu-id="3d815-345">For the instructions about enabling Remote Desktop at creation, see [Create HDInsight cluster](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3d815-345">For the instructions about enabling Remote Desktop at creation, see [Create HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

<span data-ttu-id="3d815-346">**To enable Remote Desktop**</span><span class="sxs-lookup"><span data-stu-id="3d815-346">**To enable Remote Desktop**</span></span>

1. <span data-ttu-id="3d815-347">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3d815-347">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="3d815-348">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-348">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="3d815-349">Click **Settings** from the top menu, and then click **Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="3d815-349">Click **Settings** from the top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="3d815-350">Enter **Expires On**, **Remote Desktop Username** and **Remote Desktop Password**, and then click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="3d815-350">Enter **Expires On**, **Remote Desktop Username** and **Remote Desktop Password**, and then click **Enable**.</span></span>

    ![HDInsight enable disable configure remote desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    <span data-ttu-id="3d815-352">The default values for Expires On is a week.</span><span class="sxs-lookup"><span data-stu-id="3d815-352">The default values for Expires On is a week.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3d815-353">You can also use the HDInsight .NET SDK to enable Remote Desktop on a cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-353">You can also use the HDInsight .NET SDK to enable Remote Desktop on a cluster.</span></span> <span data-ttu-id="3d815-354">Use the **EnableRdp** method on the HDInsight client object in the following manner: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span><span class="sxs-lookup"><span data-stu-id="3d815-354">Use the **EnableRdp** method on the HDInsight client object in the following manner: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span></span> <span data-ttu-id="3d815-355">Similarly, to disable Remote Desktop on the cluster, you can use **client.DisableRdp(clustername, location)**.</span><span class="sxs-lookup"><span data-stu-id="3d815-355">Similarly, to disable Remote Desktop on the cluster, you can use **client.DisableRdp(clustername, location)**.</span></span> <span data-ttu-id="3d815-356">For more information on these methods, see [HDInsight .NET SDK Reference](http://go.microsoft.com/fwlink/?LinkId=529017).</span><span class="sxs-lookup"><span data-stu-id="3d815-356">For more information on these methods, see [HDInsight .NET SDK Reference](http://go.microsoft.com/fwlink/?LinkId=529017).</span></span> <span data-ttu-id="3d815-357">This is applicable only for HDInsight clusters running on Windows.</span><span class="sxs-lookup"><span data-stu-id="3d815-357">This is applicable only for HDInsight clusters running on Windows.</span></span>
   >
   >

<span data-ttu-id="3d815-358">**To connect to a cluster by using RDP**</span><span class="sxs-lookup"><span data-stu-id="3d815-358">**To connect to a cluster by using RDP**</span></span>

1. <span data-ttu-id="3d815-359">Sign in to the [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3d815-359">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="3d815-360">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span><span class="sxs-lookup"><span data-stu-id="3d815-360">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="3d815-361">Click **Settings** from the top menu, and then click **Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="3d815-361">Click **Settings** from the top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="3d815-362">Click **Connect** and follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="3d815-362">Click **Connect** and follow the instructions.</span></span> <span data-ttu-id="3d815-363">If Connect is disable, you must enable it first.</span><span class="sxs-lookup"><span data-stu-id="3d815-363">If Connect is disable, you must enable it first.</span></span> <span data-ttu-id="3d815-364">Make sure using the Remote Desktop user username and password.</span><span class="sxs-lookup"><span data-stu-id="3d815-364">Make sure using the Remote Desktop user username and password.</span></span>  <span data-ttu-id="3d815-365">You can't use the Cluster user credentials.</span><span class="sxs-lookup"><span data-stu-id="3d815-365">You can't use the Cluster user credentials.</span></span>

## <a name="open-hadoop-command-line"></a><span data-ttu-id="3d815-366">Open Hadoop command line</span><span class="sxs-lookup"><span data-stu-id="3d815-366">Open Hadoop command line</span></span>
<span data-ttu-id="3d815-367">To connect to the cluster by using Remote Desktop and use the Hadoop command line, you must first have enabled Remote Desktop access to the cluster as described in the previous section.</span><span class="sxs-lookup"><span data-stu-id="3d815-367">To connect to the cluster by using Remote Desktop and use the Hadoop command line, you must first have enabled Remote Desktop access to the cluster as described in the previous section.</span></span>

<span data-ttu-id="3d815-368">**To open a Hadoop command line**</span><span class="sxs-lookup"><span data-stu-id="3d815-368">**To open a Hadoop command line**</span></span>

1. <span data-ttu-id="3d815-369">Connect to the cluster using Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="3d815-369">Connect to the cluster using Remote Desktop.</span></span>
2. <span data-ttu-id="3d815-370">From the desktop, double-click **Hadoop Command Line**.</span><span class="sxs-lookup"><span data-stu-id="3d815-370">From the desktop, double-click **Hadoop Command Line**.</span></span>

    <span data-ttu-id="3d815-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span><span class="sxs-lookup"><span data-stu-id="3d815-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span></span>

    <span data-ttu-id="3d815-372">For more information on Hadoop commands, see [Hadoop commands reference](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span><span class="sxs-lookup"><span data-stu-id="3d815-372">For more information on Hadoop commands, see [Hadoop commands reference](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span></span>

<span data-ttu-id="3d815-373">In the previous screenshot, the folder name has the Hadoop version number embedded.</span><span class="sxs-lookup"><span data-stu-id="3d815-373">In the previous screenshot, the folder name has the Hadoop version number embedded.</span></span> <span data-ttu-id="3d815-374">The version number can changed based on the version of the Hadoop components installed on the cluster.</span><span class="sxs-lookup"><span data-stu-id="3d815-374">The version number can changed based on the version of the Hadoop components installed on the cluster.</span></span> <span data-ttu-id="3d815-375">You can use Hadoop environment variables to refer to those folders.</span><span class="sxs-lookup"><span data-stu-id="3d815-375">You can use Hadoop environment variables to refer to those folders.</span></span> <span data-ttu-id="3d815-376">For example:</span><span class="sxs-lookup"><span data-stu-id="3d815-376">For example:</span></span>

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a><span data-ttu-id="3d815-377">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d815-377">Next steps</span></span>
<span data-ttu-id="3d815-378">In this article, you have learned how to create an HDInsight cluster by using the Portal, and how to open the Hadoop command-line tool.</span><span class="sxs-lookup"><span data-stu-id="3d815-378">In this article, you have learned how to create an HDInsight cluster by using the Portal, and how to open the Hadoop command-line tool.</span></span> <span data-ttu-id="3d815-379">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="3d815-379">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="3d815-380">Administer HDInsight Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d815-380">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="3d815-381">Administer HDInsight Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3d815-381">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="3d815-382">Create HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="3d815-382">Create HDInsight clusters</span></span>](hdinsight-provision-clusters.md)
* [<span data-ttu-id="3d815-383">Submit Hadoop jobs programmatically</span><span class="sxs-lookup"><span data-stu-id="3d815-383">Submit Hadoop jobs programmatically</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* [<span data-ttu-id="3d815-384">Get Started with Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3d815-384">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="3d815-385">What version of Hadoop is in Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="3d815-385">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop command line"




















