---
title: Use the Azure portal to create Azure HDInsight clusters with Data Lake Store | Microsoft Docs
description: Use the Azure portal to create and use HDInsight clusters with Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: nitinme
ms.openlocfilehash: 1e7e7db4567da2462f012d86ad44a0fc0eed53eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564094"
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-the-azure-portal"></a><span data-ttu-id="250d2-103">Create HDInsight clusters with Data Lake Store by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="250d2-103">Create HDInsight clusters with Data Lake Store by using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Use the Azure portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Use PowerShell (for default storage)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Use PowerShell (for additional storage)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Use Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="250d2-108">This article discusses how to use the Azure portal to create HDInsight clusters with access to Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="250d2-108">This article discusses how to use the Azure portal to create HDInsight clusters with access to Azure Data Lake Store.</span></span> <span data-ttu-id="250d2-109">For supported cluster types, you can use Data Lake Store as default storage or as an additional storage account.</span><span class="sxs-lookup"><span data-stu-id="250d2-109">For supported cluster types, you can use Data Lake Store as default storage or as an additional storage account.</span></span>

<span data-ttu-id="250d2-110">When you use Data Lake Store as additional storage, the default storage account for the clusters remains Azure Blob storage, and the cluster-related files (such as logs) are still written to the default storage.</span><span class="sxs-lookup"><span data-stu-id="250d2-110">When you use Data Lake Store as additional storage, the default storage account for the clusters remains Azure Blob storage, and the cluster-related files (such as logs) are still written to the default storage.</span></span> <span data-ttu-id="250d2-111">However, the data that you want to process can be stored in a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="250d2-111">However, the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="250d2-112">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to storage from the cluster.</span><span class="sxs-lookup"><span data-stu-id="250d2-112">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to storage from the cluster.</span></span>

<span data-ttu-id="250d2-113">Here are some important considerations for using HDInsight with Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="250d2-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="250d2-114">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5.</span><span class="sxs-lookup"><span data-stu-id="250d2-114">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5.</span></span>

* <span data-ttu-id="250d2-115">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span><span class="sxs-lookup"><span data-stu-id="250d2-115">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

* <span data-ttu-id="250d2-116">The option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, and 3.5.</span><span class="sxs-lookup"><span data-stu-id="250d2-116">The option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, and 3.5.</span></span>

* <span data-ttu-id="250d2-117">For HBase clusters (Windows and Linux), Data Lake Store is *not supported* as a storage option for either default or additional storage.</span><span class="sxs-lookup"><span data-stu-id="250d2-117">For HBase clusters (Windows and Linux), Data Lake Store is *not supported* as a storage option for either default or additional storage.</span></span>

* <span data-ttu-id="250d2-118">For Storm clusters (Windows and Linux), you can use Data Lake Store to write data from a Storm topology.</span><span class="sxs-lookup"><span data-stu-id="250d2-118">For Storm clusters (Windows and Linux), you can use Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="250d2-119">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span><span class="sxs-lookup"><span data-stu-id="250d2-119">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span> <span data-ttu-id="250d2-120">For more information, see [Use Data Lake Store in a Storm topology](#use-data-lake-store-in-a-storm-topology).</span><span class="sxs-lookup"><span data-stu-id="250d2-120">For more information, see [Use Data Lake Store in a Storm topology](#use-data-lake-store-in-a-storm-topology).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="250d2-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="250d2-121">Prerequisites</span></span>
<span data-ttu-id="250d2-122">Before you begin this tutorial, ensure that you've met the following requirements:</span><span class="sxs-lookup"><span data-stu-id="250d2-122">Before you begin this tutorial, ensure that you've met the following requirements:</span></span>

* <span data-ttu-id="250d2-123">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="250d2-123">**An Azure subscription**.</span></span> <span data-ttu-id="250d2-124">Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="250d2-124">Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="250d2-125">**An Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="250d2-125">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="250d2-126">Follow the instructions at [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="250d2-126">Follow the instructions at [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="250d2-127">**An Azure Active Directory service principal**.</span><span class="sxs-lookup"><span data-stu-id="250d2-127">**An Azure Active Directory service principal**.</span></span> <span data-ttu-id="250d2-128">This tutorial provides instructions on how to create a service principal in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="250d2-128">This tutorial provides instructions on how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="250d2-129">However, to create a service principal, you must be an Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="250d2-129">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="250d2-130">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span><span class="sxs-lookup"><span data-stu-id="250d2-130">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    >You can create a service principal only if you are an Azure AD administrator. Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store. Also, the service principal must be created with a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-an-hdinsight-cluster-with-access-to-a-data-lake-store"></a><span data-ttu-id="250d2-134">Create an HDInsight cluster with access to a Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="250d2-134">Create an HDInsight cluster with access to a Data Lake Store</span></span>
<span data-ttu-id="250d2-135">In this section, you create an HDInsight Hadoop cluster that uses the Data Lake Store as default storage or additional storage.</span><span class="sxs-lookup"><span data-stu-id="250d2-135">In this section, you create an HDInsight Hadoop cluster that uses the Data Lake Store as default storage or additional storage.</span></span>

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a><span data-ttu-id="250d2-136">Create a cluster with Data Lake Store as default storage</span><span class="sxs-lookup"><span data-stu-id="250d2-136">Create a cluster with Data Lake Store as default storage</span></span>

>[!NOTE]
>You can use this option only with HDInsight 3.5 clusters (Standard edition). Within HDInsight 3.5 clusters, this option is not available for the HBase cluster type.

1. <span data-ttu-id="250d2-139">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="250d2-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="250d2-140">To start provisioning an HDInsight cluster, follow the instructions in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="250d2-140">To start provisioning an HDInsight cluster, follow the instructions in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

3. <span data-ttu-id="250d2-141">On the **Storage** blade, under **Primary storage type**, click **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="250d2-141">On the **Storage** blade, under **Primary storage type**, click **Data Lake Store**.</span></span>

4. <span data-ttu-id="250d2-142">Select an existing Data Lake Store account and enter a root folder path where the cluster-specific files are to be stored.</span><span class="sxs-lookup"><span data-stu-id="250d2-142">Select an existing Data Lake Store account and enter a root folder path where the cluster-specific files are to be stored.</span></span>

    <span data-ttu-id="250d2-143">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-143">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Add service principal to HDInsight cluster")</span></span>


    <span data-ttu-id="250d2-144">In the screenshot above, the root folder path is /clusters/myhdiadlcluster, where *myhdiadlcluster* is the name of the cluster being created.</span><span class="sxs-lookup"><span data-stu-id="250d2-144">In the screenshot above, the root folder path is /clusters/myhdiadlcluster, where *myhdiadlcluster* is the name of the cluster being created.</span></span> <span data-ttu-id="250d2-145">In such a case, make sure that the */clusters* folder exists in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="250d2-145">In such a case, make sure that the */clusters* folder exists in the Data Lake Store account.</span></span> <span data-ttu-id="250d2-146">The *myhdiadlcluster* folder is created during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="250d2-146">The *myhdiadlcluster* folder is created during cluster creation.</span></span> <span data-ttu-id="250d2-147">Similarly, if the root path was set to */hdinsight/clusters/data/myhdiadlcluster*, ensure that */hdinsight/clusters/data/* exists in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="250d2-147">Similarly, if the root path was set to */hdinsight/clusters/data/myhdiadlcluster*, ensure that */hdinsight/clusters/data/* exists in the Data Lake Store account.</span></span>

5. <span data-ttu-id="250d2-148">Click **Data Lake Store access** to configure access between the Data Lake Store account and HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="250d2-148">Click **Data Lake Store access** to configure access between the Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="250d2-149">For instructions see [Configure access between HDInsight cluster and Data Lake Store](#configure-access-between-hdinsight-cluster-and-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="250d2-149">For instructions see [Configure access between HDInsight cluster and Data Lake Store](#configure-access-between-hdinsight-cluster-and-data-lake-store).</span></span>


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="250d2-150">Create a cluster with Data Lake Store as additional storage</span><span class="sxs-lookup"><span data-stu-id="250d2-150">Create a cluster with Data Lake Store as additional storage</span></span>

1. <span data-ttu-id="250d2-151">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="250d2-151">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="250d2-152">To start provisioning an HDInsight cluster, follow the instructions in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="250d2-152">To start provisioning an HDInsight cluster, follow the instructions in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

3. <span data-ttu-id="250d2-153">On the **Storage** blade, under **Primary storage type**, select **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="250d2-153">On the **Storage** blade, under **Primary storage type**, select **Azure Storage**.</span></span>

4. <span data-ttu-id="250d2-154">Under **Selection method**, do either of the following:</span><span class="sxs-lookup"><span data-stu-id="250d2-154">Under **Selection method**, do either of the following:</span></span>

    * <span data-ttu-id="250d2-155">To specify a storage account that is part of your Azure subscription, select **My subscriptions**, and then select the storage account.</span><span class="sxs-lookup"><span data-stu-id="250d2-155">To specify a storage account that is part of your Azure subscription, select **My subscriptions**, and then select the storage account.</span></span>

    * <span data-ttu-id="250d2-156">To specify a storage account that is outside your Azure subscription, select **Access key**, and then provide the information for the outside storage account.</span><span class="sxs-lookup"><span data-stu-id="250d2-156">To specify a storage account that is outside your Azure subscription, select **Access key**, and then provide the information for the outside storage account.</span></span>

5. <span data-ttu-id="250d2-157">Under **Default container**, retain the default container name that's suggested by the portal or specify your own.</span><span class="sxs-lookup"><span data-stu-id="250d2-157">Under **Default container**, retain the default container name that's suggested by the portal or specify your own.</span></span>

    <span data-ttu-id="250d2-158">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-158">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Add service principal to HDInsight cluster")</span></span>

6. <span data-ttu-id="250d2-159">When you use Blob storage as default storage, you can still use Data Lake Store as additional storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="250d2-159">When you use Blob storage as default storage, you can still use Data Lake Store as additional storage for the cluster.</span></span> <span data-ttu-id="250d2-160">To do so, click **Data Lake Store access** to configure access between the Data Lake Store account and HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="250d2-160">To do so, click **Data Lake Store access** to configure access between the Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="250d2-161">For instructions see [Configure access between HDInsight cluster and Data Lake Store](#configure-access-between-hdinsight-cluster-and-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="250d2-161">For instructions see [Configure access between HDInsight cluster and Data Lake Store](#configure-access-between-hdinsight-cluster-and-data-lake-store).</span></span>

## <a name="configure-access-between-hdinsight-cluster-and-data-lake-store"></a><span data-ttu-id="250d2-162">Configure access between HDInsight cluster and Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="250d2-162">Configure access between HDInsight cluster and Data Lake Store</span></span>

<span data-ttu-id="250d2-163">In this section, you configure access between HDInsight clusters and Data Lake Store using an Azure Active Directory service principal</span><span class="sxs-lookup"><span data-stu-id="250d2-163">In this section, you configure access between HDInsight clusters and Data Lake Store using an Azure Active Directory service principal</span></span>

1. <span data-ttu-id="250d2-164">On the **Data Lake Store access** blade, specify whether you want to use a new service principal or an existing service principal.</span><span class="sxs-lookup"><span data-stu-id="250d2-164">On the **Data Lake Store access** blade, specify whether you want to use a new service principal or an existing service principal.</span></span> <span data-ttu-id="250d2-165">This step creates a new service principal.</span><span class="sxs-lookup"><span data-stu-id="250d2-165">This step creates a new service principal.</span></span> <span data-ttu-id="250d2-166">To use an existing service principal, skip to the next step.</span><span class="sxs-lookup"><span data-stu-id="250d2-166">To use an existing service principal, skip to the next step.</span></span>

    <span data-ttu-id="250d2-167">a.</span><span class="sxs-lookup"><span data-stu-id="250d2-167">a.</span></span> <span data-ttu-id="250d2-168">On the **Data Lake Store access** blade, click **Create new**, and then click **Service Principal**.</span><span class="sxs-lookup"><span data-stu-id="250d2-168">On the **Data Lake Store access** blade, click **Create new**, and then click **Service Principal**.</span></span>

    <span data-ttu-id="250d2-169">b.</span><span class="sxs-lookup"><span data-stu-id="250d2-169">b.</span></span> <span data-ttu-id="250d2-170">On the **Create a Service Principal** blade, enter the required values.</span><span class="sxs-lookup"><span data-stu-id="250d2-170">On the **Create a Service Principal** blade, enter the required values.</span></span>  

    <span data-ttu-id="250d2-171">c.</span><span class="sxs-lookup"><span data-stu-id="250d2-171">c.</span></span> <span data-ttu-id="250d2-172">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="250d2-172">Click **Create**.</span></span> <span data-ttu-id="250d2-173">A certificate and an Azure AD application are created automatically.</span><span class="sxs-lookup"><span data-stu-id="250d2-173">A certificate and an Azure AD application are created automatically.</span></span>

    <span data-ttu-id="250d2-174">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-174">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Add service principal to HDInsight cluster")</span></span>

    <span data-ttu-id="250d2-175">You can also click **Download Certificate** to download the certificate associated with the service principal you created.</span><span class="sxs-lookup"><span data-stu-id="250d2-175">You can also click **Download Certificate** to download the certificate associated with the service principal you created.</span></span> <span data-ttu-id="250d2-176">Downloading the certificate is useful if you want to use the same service principal when you create additional HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="250d2-176">Downloading the certificate is useful if you want to use the same service principal when you create additional HDInsight clusters.</span></span> <span data-ttu-id="250d2-177">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="250d2-177">Click **Select**.</span></span>

2. <span data-ttu-id="250d2-178">To use an existing service principal, perform the steps provided below.</span><span class="sxs-lookup"><span data-stu-id="250d2-178">To use an existing service principal, perform the steps provided below.</span></span>

    <span data-ttu-id="250d2-179">a.</span><span class="sxs-lookup"><span data-stu-id="250d2-179">a.</span></span> <span data-ttu-id="250d2-180">On the **Data Lake Store access** blade, click **Use existing**, and then click **Service Principal**.</span><span class="sxs-lookup"><span data-stu-id="250d2-180">On the **Data Lake Store access** blade, click **Use existing**, and then click **Service Principal**.</span></span>

    <span data-ttu-id="250d2-181">b.</span><span class="sxs-lookup"><span data-stu-id="250d2-181">b.</span></span> <span data-ttu-id="250d2-182">On the **Select a Service Principal** blade, search for an existing service principal.</span><span class="sxs-lookup"><span data-stu-id="250d2-182">On the **Select a Service Principal** blade, search for an existing service principal.</span></span> <span data-ttu-id="250d2-183">Click the service principal that you want to use, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="250d2-183">Click the service principal that you want to use, and then click **Select**.</span></span>

    <span data-ttu-id="250d2-184">c.</span><span class="sxs-lookup"><span data-stu-id="250d2-184">c.</span></span> <span data-ttu-id="250d2-185">On the **Data Lake Store access** blade, upload the certificate (.pfx file) that's associated with your selected service principal, and then enter the certificate password.</span><span class="sxs-lookup"><span data-stu-id="250d2-185">On the **Data Lake Store access** blade, upload the certificate (.pfx file) that's associated with your selected service principal, and then enter the certificate password.</span></span>

    <span data-ttu-id="250d2-186">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-186">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Add service principal to HDInsight cluster")</span></span>

7. <span data-ttu-id="250d2-187">On the **Data Lake Store access** blade, click **Access**.</span><span class="sxs-lookup"><span data-stu-id="250d2-187">On the **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="250d2-188">The **Select file permissions** blade is open by default.</span><span class="sxs-lookup"><span data-stu-id="250d2-188">The **Select file permissions** blade is open by default.</span></span> <span data-ttu-id="250d2-189">It lists all the Data Lake Store accounts in your subscription.</span><span class="sxs-lookup"><span data-stu-id="250d2-189">It lists all the Data Lake Store accounts in your subscription.</span></span>

8. <span data-ttu-id="250d2-190">Select the Data Lake Store account that you want to associate with the cluster.</span><span class="sxs-lookup"><span data-stu-id="250d2-190">Select the Data Lake Store account that you want to associate with the cluster.</span></span>

    <span data-ttu-id="250d2-191">**If you are using Data Lake Store as the default storage**, you should assign permissions at two levels.</span><span class="sxs-lookup"><span data-stu-id="250d2-191">**If you are using Data Lake Store as the default storage**, you should assign permissions at two levels.</span></span>

    <span data-ttu-id="250d2-192">a.</span><span class="sxs-lookup"><span data-stu-id="250d2-192">a.</span></span> <span data-ttu-id="250d2-193">First, you should assign permission at the root level of the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="250d2-193">First, you should assign permission at the root level of the Data Lake Store account.</span></span> <span data-ttu-id="250d2-194">To do so, hover (do not click) the mouse over the name of the Data Lake Store account to make the check box visible.</span><span class="sxs-lookup"><span data-stu-id="250d2-194">To do so, hover (do not click) the mouse over the name of the Data Lake Store account to make the check box visible.</span></span> <span data-ttu-id="250d2-195">Select the check box.</span><span class="sxs-lookup"><span data-stu-id="250d2-195">Select the check box.</span></span>

    <span data-ttu-id="250d2-196">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-196">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Add service principal to HDInsight cluster")</span></span>

    <span data-ttu-id="250d2-197">b.</span><span class="sxs-lookup"><span data-stu-id="250d2-197">b.</span></span> <span data-ttu-id="250d2-198">Then, you should assign permission to the HDInsight cluster storage root.</span><span class="sxs-lookup"><span data-stu-id="250d2-198">Then, you should assign permission to the HDInsight cluster storage root.</span></span> <span data-ttu-id="250d2-199">According to the screenshot earlier, the cluster storage root is **/clusters** folder that you specificed while selecting the Data Lake Store as default storage.</span><span class="sxs-lookup"><span data-stu-id="250d2-199">According to the screenshot earlier, the cluster storage root is **/clusters** folder that you specificed while selecting the Data Lake Store as default storage.</span></span>

    <span data-ttu-id="250d2-200">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.add.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-200">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.add.png "Add service principal to HDInsight cluster")</span></span>

    <span data-ttu-id="250d2-201">**If you are using Data Lake Store as additional storage**, you must assign permission only for the folder that you want to access from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="250d2-201">**If you are using Data Lake Store as additional storage**, you must assign permission only for the folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="250d2-202">For example, in the screenshot below, you provide access only to **hdiaddonstorage** folder in a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="250d2-202">For example, in the screenshot below, you provide access only to **hdiaddonstorage** folder in a Data Lake Store account.</span></span>

    <span data-ttu-id="250d2-203">![Assign service principal permissions to the HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "Assign service principal permissions to the HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-203">![Assign service principal permissions to the HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "Assign service principal permissions to the HDInsight cluster")</span></span>

9. <span data-ttu-id="250d2-204">For all the accounts and paths you selected, select the permissions (Read, Write, or Execute) and specify whether the permissions apply recursively to the child items as well, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="250d2-204">For all the accounts and paths you selected, select the permissions (Read, Write, or Execute) and specify whether the permissions apply recursively to the child items as well, and then click **Select**.</span></span>

11. <span data-ttu-id="250d2-205">In the **Assign selected permissions** window, to assign the permissions for the Azure Active Directory service principal on the account, files, or folders you selected, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="250d2-205">In the **Assign selected permissions** window, to assign the permissions for the Azure Active Directory service principal on the account, files, or folders you selected, click **Run**.</span></span>

    <span data-ttu-id="250d2-206">![Assign service principal permissions to the HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-2.png "Assign service principal permissions to the HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-206">![Assign service principal permissions to the HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-2.png "Assign service principal permissions to the HDInsight cluster")</span></span>

12. <span data-ttu-id="250d2-207">After the permissions are successfully assigned, click **Done** on each open blade to return to the **Data Lake Store access** blade.</span><span class="sxs-lookup"><span data-stu-id="250d2-207">After the permissions are successfully assigned, click **Done** on each open blade to return to the **Data Lake Store access** blade.</span></span>

13. <span data-ttu-id="250d2-208">On the **Data Lake Store access**, click **Select**, and then continue with cluster creation as described in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="250d2-208">On the **Data Lake Store access**, click **Select**, and then continue with cluster creation as described in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <a name="verify-cluster-set-up"></a><span data-ttu-id="250d2-209">Verify cluster set up</span><span class="sxs-lookup"><span data-stu-id="250d2-209">Verify cluster set up</span></span>

<span data-ttu-id="250d2-210">After the cluster setup is complete, on the cluster blade, verify your results by doing either or both of the following:</span><span class="sxs-lookup"><span data-stu-id="250d2-210">After the cluster setup is complete, on the cluster blade, verify your results by doing either or both of the following:</span></span>

* <span data-ttu-id="250d2-211">To verify that the associated storage for the cluster is the Data Lake Store account that you specified, click **Storage accounts** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="250d2-211">To verify that the associated storage for the cluster is the Data Lake Store account that you specified, click **Storage accounts** in the left pane.</span></span>

    <span data-ttu-id="250d2-212">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-212">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Add service principal to HDInsight cluster")</span></span>

* <span data-ttu-id="250d2-213">To verify that the service principal is correctly associated with the HDInsight cluster, click **Data Lake Store access** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="250d2-213">To verify that the service principal is correctly associated with the HDInsight cluster, click **Data Lake Store access** in the left pane.</span></span>

    <span data-ttu-id="250d2-214">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Add service principal to HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="250d2-214">![Add service principal to HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Add service principal to HDInsight cluster")</span></span>


## <a name="examples"></a><span data-ttu-id="250d2-215">Examples</span><span class="sxs-lookup"><span data-stu-id="250d2-215">Examples</span></span>

<span data-ttu-id="250d2-216">After you have set up the cluster with Data Lake Store as your storage, refer to these examples of how to use HDInsight cluster to analyze the data that's stored in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="250d2-216">After you have set up the cluster with Data Lake Store as your storage, refer to these examples of how to use HDInsight cluster to analyze the data that's stored in Data Lake Store.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a><span data-ttu-id="250d2-217">Run a Hive query against data in a Data Lake Store (as primary storage)</span><span class="sxs-lookup"><span data-stu-id="250d2-217">Run a Hive query against data in a Data Lake Store (as primary storage)</span></span>

<span data-ttu-id="250d2-218">To run a Hive query, use the Hive views interface in the Ambari portal.</span><span class="sxs-lookup"><span data-stu-id="250d2-218">To run a Hive query, use the Hive views interface in the Ambari portal.</span></span> <span data-ttu-id="250d2-219">For instructions on how to use Ambari Hive views, see [Use the Hive View with Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="250d2-219">For instructions on how to use Ambari Hive views, see [Use the Hive View with Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

<span data-ttu-id="250d2-220">When you work with data in a Data Lake Store, there are a few strings to change.</span><span class="sxs-lookup"><span data-stu-id="250d2-220">When you work with data in a Data Lake Store, there are a few strings to change.</span></span>

<span data-ttu-id="250d2-221">If you use, for example, the cluster that you created with Data Lake Store as primary storage, the path to the data is: *adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file*.</span><span class="sxs-lookup"><span data-stu-id="250d2-221">If you use, for example, the cluster that you created with Data Lake Store as primary storage, the path to the data is: *adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file*.</span></span> <span data-ttu-id="250d2-222">A Hive query to create a table from sample data that's stored in the Data Lake Store account looks like this:</span><span class="sxs-lookup"><span data-stu-id="250d2-222">A Hive query to create a table from sample data that's stored in the Data Lake Store account looks like this:</span></span>

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

<span data-ttu-id="250d2-223">Descriptions:</span><span class="sxs-lookup"><span data-stu-id="250d2-223">Descriptions:</span></span>
* <span data-ttu-id="250d2-224">`adl://hdiadlstorage.azuredatalakestore.net/` is the root of the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="250d2-224">`adl://hdiadlstorage.azuredatalakestore.net/` is the root of the Data Lake Store account.</span></span>
* <span data-ttu-id="250d2-225">`/clusters/myhdiadlcluster` is the root of the cluster data that you specified while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="250d2-225">`/clusters/myhdiadlcluster` is the root of the cluster data that you specified while creating the cluster.</span></span>
* <span data-ttu-id="250d2-226">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/` is the location of the sample file that you used in the query.</span><span class="sxs-lookup"><span data-stu-id="250d2-226">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/` is the location of the sample file that you used in the query.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a><span data-ttu-id="250d2-227">Run a Hive query against data in a Data Lake Store (as additional storage)</span><span class="sxs-lookup"><span data-stu-id="250d2-227">Run a Hive query against data in a Data Lake Store (as additional storage)</span></span>

<span data-ttu-id="250d2-228">If the cluster that you created uses Blob storage as default storage, the sample data is not contained in the Azure Data Lake Store account that's used as additional storage.</span><span class="sxs-lookup"><span data-stu-id="250d2-228">If the cluster that you created uses Blob storage as default storage, the sample data is not contained in the Azure Data Lake Store account that's used as additional storage.</span></span> <span data-ttu-id="250d2-229">In such a case, first transfer the data from Blob storage to the Data Lake Store, and then run the queries as shown in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="250d2-229">In such a case, first transfer the data from Blob storage to the Data Lake Store, and then run the queries as shown in the preceding example.</span></span>

<span data-ttu-id="250d2-230">For information on how to copy data from Blob storage to a Data Lake Store, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="250d2-230">For information on how to copy data from Blob storage to a Data Lake Store, see the following articles:</span></span>

* [<span data-ttu-id="250d2-231">Use Distcp to copy data between Azure Storage blobs and Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="250d2-231">Use Distcp to copy data between Azure Storage blobs and Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
* [<span data-ttu-id="250d2-232">Use AdlCopy to copy data from Azure Storage blobs to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="250d2-232">Use AdlCopy to copy data from Azure Storage blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a><span data-ttu-id="250d2-233">Use Data Lake Store with a Spark cluster</span><span class="sxs-lookup"><span data-stu-id="250d2-233">Use Data Lake Store with a Spark cluster</span></span>
<span data-ttu-id="250d2-234">You can use a Spark cluster to run Spark jobs on data that is stored in a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="250d2-234">You can use a Spark cluster to run Spark jobs on data that is stored in a Data Lake Store.</span></span> <span data-ttu-id="250d2-235">For more information, see [Use HDInsight Spark cluster to analyze data in Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="250d2-235">For more information, see [Use HDInsight Spark cluster to analyze data in Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).</span></span>


### <a name="use-data-lake-store-in-a-storm-topology"></a><span data-ttu-id="250d2-236">Use Data Lake Store in a Storm topology</span><span class="sxs-lookup"><span data-stu-id="250d2-236">Use Data Lake Store in a Storm topology</span></span>
<span data-ttu-id="250d2-237">You can use the Data Lake Store to write data from a Storm topology.</span><span class="sxs-lookup"><span data-stu-id="250d2-237">You can use the Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="250d2-238">For instructions on how to achieve this scenario, see [Use Azure Data Lake Store with Apache Storm with HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="250d2-238">For instructions on how to achieve this scenario, see [Use Azure Data Lake Store with Apache Storm with HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="250d2-239">See also</span><span class="sxs-lookup"><span data-stu-id="250d2-239">See also</span></span>
* [<span data-ttu-id="250d2-240">PowerShell: Create an HDInsight cluster to use Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="250d2-240">PowerShell: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx










