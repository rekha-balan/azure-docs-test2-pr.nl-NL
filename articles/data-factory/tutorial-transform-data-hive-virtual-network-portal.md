---
title: Transform data using Hive in Azure Virtual Network | Microsoft Docs
description: This tutorial provides step-by-step instructions for transforming data by using Hive activity in Azure Data Factory.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/04/2018
ms.author: douglasl
ms.openlocfilehash: 60dc0e88998580732b50cb202fb5d00a7cfcae21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868262"
---
# <a name="transform-data-in-azure-virtual-network-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="a06a5-103">Transform data in Azure Virtual Network using Hive activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a06a5-103">Transform data in Azure Virtual Network using Hive activity in Azure Data Factory</span></span>
<span data-ttu-id="a06a5-104">In this tutorial, you use Azure portal to create a Data Factory pipeline that transforms data using Hive Activity on a HDInsight cluster that is in an Azure Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="a06a5-104">In this tutorial, you use Azure portal to create a Data Factory pipeline that transforms data using Hive Activity on a HDInsight cluster that is in an Azure Virtual Network (VNet).</span></span> <span data-ttu-id="a06a5-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="a06a5-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a06a5-106">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="a06a5-106">Create a data factory.</span></span> 
> * <span data-ttu-id="a06a5-107">Create a self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="a06a5-107">Create a self-hosted integration runtime</span></span>
> * <span data-ttu-id="a06a5-108">Create Azure Storage and Azure HDInsight linked services</span><span class="sxs-lookup"><span data-stu-id="a06a5-108">Create Azure Storage and Azure HDInsight linked services</span></span>
> * <span data-ttu-id="a06a5-109">Create a pipeline with Hive activity.</span><span class="sxs-lookup"><span data-stu-id="a06a5-109">Create a pipeline with Hive activity.</span></span>
> * <span data-ttu-id="a06a5-110">Trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="a06a5-110">Trigger a pipeline run.</span></span>
> * <span data-ttu-id="a06a5-111">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="a06a5-111">Monitor the pipeline run</span></span> 
> * <span data-ttu-id="a06a5-112">Verify the output</span><span class="sxs-lookup"><span data-stu-id="a06a5-112">Verify the output</span></span>

<span data-ttu-id="a06a5-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="a06a5-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a06a5-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a06a5-114">Prerequisites</span></span>
- <span data-ttu-id="a06a5-115">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-115">**Azure Storage account**.</span></span> <span data-ttu-id="a06a5-116">You create a hive script, and upload it to the Azure storage.</span><span class="sxs-lookup"><span data-stu-id="a06a5-116">You create a hive script, and upload it to the Azure storage.</span></span> <span data-ttu-id="a06a5-117">The output from the Hive script is stored in this storage account.</span><span class="sxs-lookup"><span data-stu-id="a06a5-117">The output from the Hive script is stored in this storage account.</span></span> <span data-ttu-id="a06a5-118">In this sample, HDInsight cluster uses this Azure Storage account as the primary storage.</span><span class="sxs-lookup"><span data-stu-id="a06a5-118">In this sample, HDInsight cluster uses this Azure Storage account as the primary storage.</span></span> 
- <span data-ttu-id="a06a5-119">**Azure Virtual Network.**</span><span class="sxs-lookup"><span data-stu-id="a06a5-119">**Azure Virtual Network.**</span></span> <span data-ttu-id="a06a5-120">If you don't have an Azure virtual network, create it by following [these instructions](../virtual-network/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a06a5-120">If you don't have an Azure virtual network, create it by following [these instructions](../virtual-network/quick-create-portal.md).</span></span> <span data-ttu-id="a06a5-121">In this sample, the HDInsight is in an Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a06a5-121">In this sample, the HDInsight is in an Azure Virtual Network.</span></span> <span data-ttu-id="a06a5-122">Here is a sample configuration of Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a06a5-122">Here is a sample configuration of Azure Virtual Network.</span></span> 

    ![Create virtual network](media/tutorial-transform-data-using-hive-in-vnet-portal/create-virtual-network.png)
- <span data-ttu-id="a06a5-124">**HDInsight cluster.**</span><span class="sxs-lookup"><span data-stu-id="a06a5-124">**HDInsight cluster.**</span></span> <span data-ttu-id="a06a5-125">Create a HDInsight cluster and join it to the virtual network you created in the previous step by following this article: [Extend Azure HDInsight using an Azure Virtual Network](../hdinsight/hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="a06a5-125">Create a HDInsight cluster and join it to the virtual network you created in the previous step by following this article: [Extend Azure HDInsight using an Azure Virtual Network](../hdinsight/hdinsight-extend-hadoop-virtual-network.md).</span></span> <span data-ttu-id="a06a5-126">Here is a sample configuration of HDInsight in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a06a5-126">Here is a sample configuration of HDInsight in a virtual network.</span></span> 

    ![HDInsight in a virtual network](media/tutorial-transform-data-using-hive-in-vnet-portal/hdinsight-virtual-network-settings.png)
- <span data-ttu-id="a06a5-128">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-128">**Azure PowerShell**.</span></span> <span data-ttu-id="a06a5-129">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a06a5-129">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
- <span data-ttu-id="a06a5-130">**A virtual machine**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-130">**A virtual machine**.</span></span> <span data-ttu-id="a06a5-131">Create an Azure virtual machine VM and join it into the same virtual network that contains your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="a06a5-131">Create an Azure virtual machine VM and join it into the same virtual network that contains your HDInsight cluster.</span></span> <span data-ttu-id="a06a5-132">For details, see [How to create virtual machines](../virtual-network/quick-create-portal.md#create-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="a06a5-132">For details, see [How to create virtual machines](../virtual-network/quick-create-portal.md#create-virtual-machines).</span></span> 

### <a name="upload-hive-script-to-your-blob-storage-account"></a><span data-ttu-id="a06a5-133">Upload Hive script to your Blob Storage account</span><span class="sxs-lookup"><span data-stu-id="a06a5-133">Upload Hive script to your Blob Storage account</span></span>

1. <span data-ttu-id="a06a5-134">Create a Hive SQL file named **hivescript.hql** with the following content:</span><span class="sxs-lookup"><span data-stu-id="a06a5-134">Create a Hive SQL file named **hivescript.hql** with the following content:</span></span>

   ```sql
   DROP TABLE IF EXISTS HiveSampleOut; 
   CREATE EXTERNAL TABLE HiveSampleOut (clientid string, market string, devicemodel string, state string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' 
   STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

   INSERT OVERWRITE TABLE HiveSampleOut
   Select 
       clientid,
       market,
       devicemodel,
       state
   FROM hivesampletable
   ```
2. <span data-ttu-id="a06a5-135">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="a06a5-135">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span></span>
3. <span data-ttu-id="a06a5-136">Create a folder named **hivescripts**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-136">Create a folder named **hivescripts**.</span></span>
4. <span data-ttu-id="a06a5-137">Upload the **hivescript.hql** file to the **hivescripts** subfolder.</span><span class="sxs-lookup"><span data-stu-id="a06a5-137">Upload the **hivescript.hql** file to the **hivescripts** subfolder.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="a06a5-138">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="a06a5-138">Create a data factory</span></span>

1. <span data-ttu-id="a06a5-139">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="a06a5-139">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="a06a5-140">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="a06a5-140">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="a06a5-141">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a06a5-141">Log in to the [Azure portal](https://portal.azure.com/).</span></span>    
2. <span data-ttu-id="a06a5-142">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-142">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-data-factory-menu.png)
3. <span data-ttu-id="a06a5-144">In the **New data factory** page, enter **ADFTutorialHiveFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-144">In the **New data factory** page, enter **ADFTutorialHiveFactory** for the **name**.</span></span> 
      
     ![New data factory page](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="a06a5-146">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-146">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="a06a5-147">If you receive the following error, change the name of the data factory (for example, yournameMyAzureSsisDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="a06a5-147">If you receive the following error, change the name of the data factory (for example, yournameMyAzureSsisDataFactory) and try creating again.</span></span> <span data-ttu-id="a06a5-148">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="a06a5-148">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
       `Data factory name “MyAzureSsisDataFactory” is not available`
3. <span data-ttu-id="a06a5-149">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="a06a5-149">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="a06a5-150">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="a06a5-150">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="a06a5-151">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="a06a5-151">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="a06a5-152">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="a06a5-152">Select **Create new**, and enter the name of a resource group.</span></span>   
         
      <span data-ttu-id="a06a5-153">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a06a5-153">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="a06a5-154">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-154">Select **V2** for the **version**.</span></span>
5. <span data-ttu-id="a06a5-155">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="a06a5-155">Select the **location** for the data factory.</span></span> <span data-ttu-id="a06a5-156">Only locations that are supported for creation of data factories are shown in the list.</span><span class="sxs-lookup"><span data-stu-id="a06a5-156">Only locations that are supported for creation of data factories are shown in the list.</span></span>
6. <span data-ttu-id="a06a5-157">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-157">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="a06a5-158">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-158">Click **Create**.</span></span>
8. <span data-ttu-id="a06a5-159">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-159">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/tutorial-transform-data-using-hive-in-vnet-portal/deploying-data-factory.png)
9. <span data-ttu-id="a06a5-161">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="a06a5-161">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
   ![Data factory home page](./media/tutorial-transform-data-using-hive-in-vnet-portal/data-factory-home-page.png)
10. <span data-ttu-id="a06a5-163">Click **Author & Monitor** to launch the Data Factory User Interface (UI) in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="a06a5-163">Click **Author & Monitor** to launch the Data Factory User Interface (UI) in a separate tab.</span></span>
11. <span data-ttu-id="a06a5-164">In the **get started** page, switch to the **Edit** tab in the left panel as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="a06a5-164">In the **get started** page, switch to the **Edit** tab in the left panel as shown in the following image:</span></span> 

   ![Edit tab](./media/tutorial-transform-data-using-hive-in-vnet-portal/get-started-page.png)

## <a name="create-a-self-hosted-integration-runtime"></a><span data-ttu-id="a06a5-166">Create a self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="a06a5-166">Create a self-hosted integration runtime</span></span>
<span data-ttu-id="a06a5-167">As the Hadoop cluster is inside a virtual network, you need to install a self-hosted integration runtime (IR) in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="a06a5-167">As the Hadoop cluster is inside a virtual network, you need to install a self-hosted integration runtime (IR) in the same virtual network.</span></span> <span data-ttu-id="a06a5-168">In this section, you create a new VM, join it to the same virtual network, and install self-hosted IR on it.</span><span class="sxs-lookup"><span data-stu-id="a06a5-168">In this section, you create a new VM, join it to the same virtual network, and install self-hosted IR on it.</span></span> <span data-ttu-id="a06a5-169">The self-hosted IR allows Data Factory service to dispatch processing requests to a compute service such as HDInsight inside a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a06a5-169">The self-hosted IR allows Data Factory service to dispatch processing requests to a compute service such as HDInsight inside a virtual network.</span></span> <span data-ttu-id="a06a5-170">It also allows you to move data to/from data stores inside a virtual network to Azure.</span><span class="sxs-lookup"><span data-stu-id="a06a5-170">It also allows you to move data to/from data stores inside a virtual network to Azure.</span></span> <span data-ttu-id="a06a5-171">You use a self-hosted IR when the data store or compute is in an on-premises environment as well.</span><span class="sxs-lookup"><span data-stu-id="a06a5-171">You use a self-hosted IR when the data store or compute is in an on-premises environment as well.</span></span> 

1. <span data-ttu-id="a06a5-172">In the Azure Data Factory UI, click **Connections** at the bottom of the window, switch to the **Integration Runtimes** tab, and click **+ New** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="a06a5-172">In the Azure Data Factory UI, click **Connections** at the bottom of the window, switch to the **Integration Runtimes** tab, and click **+ New** button on the toolbar.</span></span> 

   ![New integration runtime menu](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-integration-runtime-menu.png)
2. <span data-ttu-id="a06a5-174">In the **Integration Runtime Setup** window, Select **Perform data movement and dispatch activities to external computes** option, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-174">In the **Integration Runtime Setup** window, Select **Perform data movement and dispatch activities to external computes** option, and click **Next**.</span></span> 

   ![Select perform data movement and dispatch activities option](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-perform-data-movement-compute-option.png)
3. <span data-ttu-id="a06a5-176">Select **Private Network**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-176">Select **Private Network**, and click **Next**.</span></span>
    
   ![Select private network](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-private-network.png)
4. <span data-ttu-id="a06a5-178">Enter **MySelfHostedIR** for **Name**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-178">Enter **MySelfHostedIR** for **Name**, and click **Next**.</span></span> 

   ![Specify integration runtime name](./media/tutorial-transform-data-using-hive-in-vnet-portal/integration-runtime-name.png) 
5. <span data-ttu-id="a06a5-180">Copy the **authentication key** for the integration runtime by clicking the copy button, and save it.</span><span class="sxs-lookup"><span data-stu-id="a06a5-180">Copy the **authentication key** for the integration runtime by clicking the copy button, and save it.</span></span> <span data-ttu-id="a06a5-181">Keep the window open.</span><span class="sxs-lookup"><span data-stu-id="a06a5-181">Keep the window open.</span></span> <span data-ttu-id="a06a5-182">You use this key to register the IR installed in a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a06a5-182">You use this key to register the IR installed in a virtual machine.</span></span> 

   ![Copy authentication key](./media/tutorial-transform-data-using-hive-in-vnet-portal/copy-key.png)

### <a name="install-ir-on-a-virtual-machine"></a><span data-ttu-id="a06a5-184">Install IR on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="a06a5-184">Install IR on a virtual machine</span></span>

1. <span data-ttu-id="a06a5-185">On the Azure VM, download [self-hosted integration runtime](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="a06a5-185">On the Azure VM, download [self-hosted integration runtime](https://www.microsoft.com/download/details.aspx?id=39717).</span></span> <span data-ttu-id="a06a5-186">Use the **authentication key** obtained in the previous step to manually register the self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="a06a5-186">Use the **authentication key** obtained in the previous step to manually register the self-hosted integration runtime.</span></span> 

    ![Register integration runtime](media/tutorial-transform-data-using-hive-in-vnet-portal/register-integration-runtime.png)

2. <span data-ttu-id="a06a5-188">You see the following message when the self-hosted integration runtime is registered successfully.</span><span class="sxs-lookup"><span data-stu-id="a06a5-188">You see the following message when the self-hosted integration runtime is registered successfully.</span></span> 
   
    ![Registered successfully](media/tutorial-transform-data-using-hive-in-vnet-portal/registered-successfully.png)
3. <span data-ttu-id="a06a5-190">Click **Launch Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-190">Click **Launch Configuration Manager**.</span></span> <span data-ttu-id="a06a5-191">You see the following page when the node is connected to the cloud service:</span><span class="sxs-lookup"><span data-stu-id="a06a5-191">You see the following page when the node is connected to the cloud service:</span></span> 
   
    ![Node is connected](media/tutorial-transform-data-using-hive-in-vnet-portal/node-is-connected.png)

### <a name="self-hosted-ir-in-the-azure-data-factory-ui"></a><span data-ttu-id="a06a5-193">Self-hosted IR in the Azure Data Factory UI</span><span class="sxs-lookup"><span data-stu-id="a06a5-193">Self-hosted IR in the Azure Data Factory UI</span></span>

1. <span data-ttu-id="a06a5-194">In the **Azure Data Factory UI**, you should see the name of the self-hosted VM name and its status.</span><span class="sxs-lookup"><span data-stu-id="a06a5-194">In the **Azure Data Factory UI**, you should see the name of the self-hosted VM name and its status.</span></span>

   ![Existing self-hosted nodes](./media/tutorial-transform-data-using-hive-in-vnet-portal/existing-self-hosted-nodes.png)
2. <span data-ttu-id="a06a5-196">Click **Finish** to close the **Integration Runtime Setup** window.</span><span class="sxs-lookup"><span data-stu-id="a06a5-196">Click **Finish** to close the **Integration Runtime Setup** window.</span></span> <span data-ttu-id="a06a5-197">You see the self-hosted IR in the list of integration runtimes.</span><span class="sxs-lookup"><span data-stu-id="a06a5-197">You see the self-hosted IR in the list of integration runtimes.</span></span>

   ![Self-hosted IR in the list](./media/tutorial-transform-data-using-hive-in-vnet-portal/self-hosted-ir-in-list.png)


## <a name="create-linked-services"></a><span data-ttu-id="a06a5-199">Create linked services</span><span class="sxs-lookup"><span data-stu-id="a06a5-199">Create linked services</span></span>

<span data-ttu-id="a06a5-200">You author and deploy two Linked Services in this section:</span><span class="sxs-lookup"><span data-stu-id="a06a5-200">You author and deploy two Linked Services in this section:</span></span>
- <span data-ttu-id="a06a5-201">An **Azure Storage Linked Service** that links an Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="a06a5-201">An **Azure Storage Linked Service** that links an Azure Storage account to the data factory.</span></span> <span data-ttu-id="a06a5-202">This storage is the primary storage used by your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="a06a5-202">This storage is the primary storage used by your HDInsight cluster.</span></span> <span data-ttu-id="a06a5-203">In this case, you use this Azure Storage account to store the Hive script and output of the script.</span><span class="sxs-lookup"><span data-stu-id="a06a5-203">In this case, you use this Azure Storage account to store the Hive script and output of the script.</span></span>
- <span data-ttu-id="a06a5-204">An **HDInsight Linked Service**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-204">An **HDInsight Linked Service**.</span></span> <span data-ttu-id="a06a5-205">Azure Data Factory submits the Hive script to this HDInsight cluster for execution.</span><span class="sxs-lookup"><span data-stu-id="a06a5-205">Azure Data Factory submits the Hive script to this HDInsight cluster for execution.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="a06a5-206">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="a06a5-206">Create Azure Storage linked service</span></span>

1. <span data-ttu-id="a06a5-207">Switch to the **Linked Services** tab, and click **New**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-207">Switch to the **Linked Services** tab, and click **New**.</span></span>

   ![New linked service button](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-linked-service.png)    
2. <span data-ttu-id="a06a5-209">In the **New Linked Service** window, select **Azure Blob Storage**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-209">In the **New Linked Service** window, select **Azure Blob Storage**, and click **Continue**.</span></span> 

   ![Select Azure Blob Storage](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-azure-storage.png)
3. <span data-ttu-id="a06a5-211">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="a06a5-211">In the **New Linked Service** window, do the following steps:</span></span>

    1. <span data-ttu-id="a06a5-212">Enter **AzureStorageLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-212">Enter **AzureStorageLinkedService** for **Name**.</span></span>
    2. <span data-ttu-id="a06a5-213">Select **MySelfHostedIR** for **Connect via integration runtime**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-213">Select **MySelfHostedIR** for **Connect via integration runtime**.</span></span>
    3. <span data-ttu-id="a06a5-214">Select your Azure storage account for **Storage account name**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-214">Select your Azure storage account for **Storage account name**.</span></span> 
    4. <span data-ttu-id="a06a5-215">To test the connection to storage account, click **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-215">To test the connection to storage account, click **Test connection**.</span></span>
    5. <span data-ttu-id="a06a5-216">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-216">Click **Save**.</span></span>
   
        ![Specify Azure Blob Storage account](./media/tutorial-transform-data-using-hive-in-vnet-portal/specify-azure-storage-account.png)

### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="a06a5-218">Create HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="a06a5-218">Create HDInsight linked service</span></span>

1. <span data-ttu-id="a06a5-219">Click **New** again to create another linked service.</span><span class="sxs-lookup"><span data-stu-id="a06a5-219">Click **New** again to create another linked service.</span></span> 
    
   ![New linked service button](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-linked-service.png)    
2. <span data-ttu-id="a06a5-221">Switch to the **Compute** tab, select **Azure HDInsight**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-221">Switch to the **Compute** tab, select **Azure HDInsight**, and click **Continue**.</span></span>

    ![Select Azure HDInsight](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-hdinsight.png)
3. <span data-ttu-id="a06a5-223">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="a06a5-223">In the **New Linked Service** window, do the following steps:</span></span>

    1. <span data-ttu-id="a06a5-224">Enter **AzureHDInsightLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-224">Enter **AzureHDInsightLinkedService** for **Name**.</span></span>
    2. <span data-ttu-id="a06a5-225">Select **Bring your own HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-225">Select **Bring your own HDInsight**.</span></span> 
    3. <span data-ttu-id="a06a5-226">Select your HDInsight cluster for **Hdi cluster**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-226">Select your HDInsight cluster for **Hdi cluster**.</span></span> 
    4. <span data-ttu-id="a06a5-227">Enter the **user name** for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="a06a5-227">Enter the **user name** for the HDInsight cluster.</span></span>
    5. <span data-ttu-id="a06a5-228">Enter the **password** for the user.</span><span class="sxs-lookup"><span data-stu-id="a06a5-228">Enter the **password** for the user.</span></span> 
    
        ![Azure HDInsight settings](./media/tutorial-transform-data-using-hive-in-vnet-portal/specify-azure-hdinsight.png)

<span data-ttu-id="a06a5-230">This article assumes that you have access to the cluster over the internet.</span><span class="sxs-lookup"><span data-stu-id="a06a5-230">This article assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="a06a5-231">For example, that you can connect to the cluster at `https://clustername.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="a06a5-231">For example, that you can connect to the cluster at `https://clustername.azurehdinsight.net`.</span></span> <span data-ttu-id="a06a5-232">This address uses the public gateway, which is not available if you have used network security groups (NSGs) or user-defined routes (UDRs) to restrict access from the internet.</span><span class="sxs-lookup"><span data-stu-id="a06a5-232">This address uses the public gateway, which is not available if you have used network security groups (NSGs) or user-defined routes (UDRs) to restrict access from the internet.</span></span> <span data-ttu-id="a06a5-233">For Data Factory to be able to submit jobs to HDInsight cluster in Azure Virtual Network, you need to configure your Azure Virtual Network such a way that the URL can be resolved to the private IP address of gateway used by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a06a5-233">For Data Factory to be able to submit jobs to HDInsight cluster in Azure Virtual Network, you need to configure your Azure Virtual Network such a way that the URL can be resolved to the private IP address of gateway used by HDInsight.</span></span>

1. <span data-ttu-id="a06a5-234">From Azure portal, open the Virtual Network the HDInsight is in.</span><span class="sxs-lookup"><span data-stu-id="a06a5-234">From Azure portal, open the Virtual Network the HDInsight is in.</span></span> <span data-ttu-id="a06a5-235">Open the network interface with name starting with `nic-gateway-0`.</span><span class="sxs-lookup"><span data-stu-id="a06a5-235">Open the network interface with name starting with `nic-gateway-0`.</span></span> <span data-ttu-id="a06a5-236">Note down its private IP address.</span><span class="sxs-lookup"><span data-stu-id="a06a5-236">Note down its private IP address.</span></span> <span data-ttu-id="a06a5-237">For example, 10.6.0.15.</span><span class="sxs-lookup"><span data-stu-id="a06a5-237">For example, 10.6.0.15.</span></span> 
2. <span data-ttu-id="a06a5-238">If your Azure Virtual Network has DNS server, update the DNS record so the HDInsight cluster URL `https://<clustername>.azurehdinsight.net` can be resolved to `10.6.0.15`.</span><span class="sxs-lookup"><span data-stu-id="a06a5-238">If your Azure Virtual Network has DNS server, update the DNS record so the HDInsight cluster URL `https://<clustername>.azurehdinsight.net` can be resolved to `10.6.0.15`.</span></span> <span data-ttu-id="a06a5-239">If you don’t have a DNS server in your Azure Virtual Network, you can temporarily work around by editing the hosts file (C:\Windows\System32\drivers\etc) of all VMs that registered as self-hosted integration runtime nodes by adding an entry similar to the following one:</span><span class="sxs-lookup"><span data-stu-id="a06a5-239">If you don’t have a DNS server in your Azure Virtual Network, you can temporarily work around by editing the hosts file (C:\Windows\System32\drivers\etc) of all VMs that registered as self-hosted integration runtime nodes by adding an entry similar to the following one:</span></span> 

    `10.6.0.15 myHDIClusterName.azurehdinsight.net`

## <a name="create-a-pipeline"></a><span data-ttu-id="a06a5-240">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="a06a5-240">Create a pipeline</span></span> 
<span data-ttu-id="a06a5-241">In this step, you create a new pipeline with a Hive activity.</span><span class="sxs-lookup"><span data-stu-id="a06a5-241">In this step, you create a new pipeline with a Hive activity.</span></span> <span data-ttu-id="a06a5-242">The activity executes Hive script to return data from a sample table and save it to a path you defined.</span><span class="sxs-lookup"><span data-stu-id="a06a5-242">The activity executes Hive script to return data from a sample table and save it to a path you defined.</span></span>

<span data-ttu-id="a06a5-243">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="a06a5-243">Note the following points:</span></span>

- <span data-ttu-id="a06a5-244">**scriptPath** points to path to Hive script on the Azure Storage Account you used for MyStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="a06a5-244">**scriptPath** points to path to Hive script on the Azure Storage Account you used for MyStorageLinkedService.</span></span> <span data-ttu-id="a06a5-245">The path is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="a06a5-245">The path is case-sensitive.</span></span>
- <span data-ttu-id="a06a5-246">**Output** is an argument used in the Hive script.</span><span class="sxs-lookup"><span data-stu-id="a06a5-246">**Output** is an argument used in the Hive script.</span></span> <span data-ttu-id="a06a5-247">Use the format of `wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/` to point it to an existing folder on your Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a06a5-247">Use the format of `wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/` to point it to an existing folder on your Azure Storage.</span></span> <span data-ttu-id="a06a5-248">The path is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="a06a5-248">The path is case-sensitive.</span></span> 

1. <span data-ttu-id="a06a5-249">In the Data Factory UI, click **+ (plus)** in the left pane, and click **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-249">In the Data Factory UI, click **+ (plus)** in the left pane, and click **Pipeline**.</span></span> 

    ![New pipeline menu](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-pipeline-menu.png)
2. <span data-ttu-id="a06a5-251">In the **Activities** toolbox, expand **HDInsight**, and drag-drop **Hive** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="a06a5-251">In the **Activities** toolbox, expand **HDInsight**, and drag-drop **Hive** activity to the pipeline designer surface.</span></span> 

    ![drag-drop Hive activity](./media/tutorial-transform-data-using-hive-in-vnet-portal/drag-drop-hive-activity.png)
3. <span data-ttu-id="a06a5-253">In the properties window, switch to the **HDI Cluster** tab, and select **AzureHDInsightLinkedService** for **HDInsight Linked Service**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-253">In the properties window, switch to the **HDI Cluster** tab, and select **AzureHDInsightLinkedService** for **HDInsight Linked Service**.</span></span>

    ![Select HDInsight linked service](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-hdinsight-linked-service.png)
4. <span data-ttu-id="a06a5-255">Switch to the **Scripts** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="a06a5-255">Switch to the **Scripts** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="a06a5-256">Select **AzureStorageLinkedService** for **Script Linked Service**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-256">Select **AzureStorageLinkedService** for **Script Linked Service**.</span></span> 
    2. <span data-ttu-id="a06a5-257">For **File Path**, click **Browse Storage**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-257">For **File Path**, click **Browse Storage**.</span></span> 
 
        ![Browse storage](./media/tutorial-transform-data-using-hive-in-vnet-portal/browse-storage-hive-script.png)
    3. <span data-ttu-id="a06a5-259">In the **Choose a file or folder** window, navigate to **hivescripts** folder of the **adftutorial** container, select **hivescript.hql**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-259">In the **Choose a file or folder** window, navigate to **hivescripts** folder of the **adftutorial** container, select **hivescript.hql**, and click **Finish**.</span></span>  
        
        ![Choose a file or folder](./media/tutorial-transform-data-using-hive-in-vnet-portal/choose-file-folder.png) 
    4. <span data-ttu-id="a06a5-261">Confirm that you see **adftutorial/hivescripts/hivescript.hql** for **File Path**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-261">Confirm that you see **adftutorial/hivescripts/hivescript.hql** for **File Path**.</span></span>

        ![Script settings](./media/tutorial-transform-data-using-hive-in-vnet-portal/confirm-hive-script-settings.png)
    5. <span data-ttu-id="a06a5-263">In the **Script tab**, expand **Advanced** section.</span><span class="sxs-lookup"><span data-stu-id="a06a5-263">In the **Script tab**, expand **Advanced** section.</span></span> 
    6. <span data-ttu-id="a06a5-264">Click **Auto-fill from script** for **Parameters**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-264">Click **Auto-fill from script** for **Parameters**.</span></span> 
    7. <span data-ttu-id="a06a5-265">Enter the value for the **Output** parameter in the following format: `wasb://<Blob Container>@<StorageAccount>.blob.core.windows.net/outputfolder/`.</span><span class="sxs-lookup"><span data-stu-id="a06a5-265">Enter the value for the **Output** parameter in the following format: `wasb://<Blob Container>@<StorageAccount>.blob.core.windows.net/outputfolder/`.</span></span> <span data-ttu-id="a06a5-266">For example: `wasb://adftutorial@mystorageaccount.blob.core.windows.net/outputfolder/`.</span><span class="sxs-lookup"><span data-stu-id="a06a5-266">For example: `wasb://adftutorial@mystorageaccount.blob.core.windows.net/outputfolder/`.</span></span>
 
        ![Script arguments](./media/tutorial-transform-data-using-hive-in-vnet-portal/script-arguments.png)
1. <span data-ttu-id="a06a5-268">To publish artifacts to Data Factory, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-268">To publish artifacts to Data Factory, click **Publish**.</span></span>

    ![Publish](./media/tutorial-transform-data-using-hive-in-vnet-portal/publish.png)

## <a name="trigger-a-pipeline-run"></a><span data-ttu-id="a06a5-270">Trigger a pipeline run</span><span class="sxs-lookup"><span data-stu-id="a06a5-270">Trigger a pipeline run</span></span>

1. <span data-ttu-id="a06a5-271">First, validate the pipeline by clicking the **Validate** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="a06a5-271">First, validate the pipeline by clicking the **Validate** button on the toolbar.</span></span> <span data-ttu-id="a06a5-272">Close the **Pipeline Validation Output** window by clicking **right-arrow (>>)**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-272">Close the **Pipeline Validation Output** window by clicking **right-arrow (>>)**.</span></span> 

    ![Validate pipeline](./media/tutorial-transform-data-using-hive-in-vnet-portal/validate-pipeline.png) 
2. <span data-ttu-id="a06a5-274">To trigger a pipeline run, click Trigger on the toolbar, and click Trigger Now.</span><span class="sxs-lookup"><span data-stu-id="a06a5-274">To trigger a pipeline run, click Trigger on the toolbar, and click Trigger Now.</span></span> 

    ![Trigger now](./media/tutorial-transform-data-using-hive-in-vnet-portal/trigger-now-menu.png)

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="a06a5-276">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="a06a5-276">Monitor the pipeline run</span></span>

1. <span data-ttu-id="a06a5-277">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="a06a5-277">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="a06a5-278">You see a pipeline run in the **Pipeline Runs** list.</span><span class="sxs-lookup"><span data-stu-id="a06a5-278">You see a pipeline run in the **Pipeline Runs** list.</span></span> 

    ![Monitor pipeline runs](./media/tutorial-transform-data-using-hive-in-vnet-portal/monitor-pipeline-runs.png)
2. <span data-ttu-id="a06a5-280">To refresh the list, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-280">To refresh the list, click **Refresh**.</span></span>
4. <span data-ttu-id="a06a5-281">To view activity runs associated with the pipeline runs, click **View activity runs** in the **Action** column.</span><span class="sxs-lookup"><span data-stu-id="a06a5-281">To view activity runs associated with the pipeline runs, click **View activity runs** in the **Action** column.</span></span> <span data-ttu-id="a06a5-282">Other action links are for stopping/rerunning the pipeline.</span><span class="sxs-lookup"><span data-stu-id="a06a5-282">Other action links are for stopping/rerunning the pipeline.</span></span> 

    ![View activity runs](./media/tutorial-transform-data-using-hive-in-vnet-portal/view-activity-runs-link.png)
5. <span data-ttu-id="a06a5-284">You see only one activity run since there is only one activity in the pipeline of type **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="a06a5-284">You see only one activity run since there is only one activity in the pipeline of type **HDInsightHive**.</span></span> <span data-ttu-id="a06a5-285">To switch back to the previous view, click **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="a06a5-285">To switch back to the previous view, click **Pipelines** link at the top.</span></span>

    ![Activity runs](./media/tutorial-transform-data-using-hive-in-vnet-portal/view-activity-runs.png)
6. <span data-ttu-id="a06a5-287">Confirm that you see an output file in the **outputfolder** of the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="a06a5-287">Confirm that you see an output file in the **outputfolder** of the **adftutorial** container.</span></span> 

    ![Output file](./media/tutorial-transform-data-using-hive-in-vnet-portal/output-file.png)

## <a name="next-steps"></a><span data-ttu-id="a06a5-289">Next steps</span><span class="sxs-lookup"><span data-stu-id="a06a5-289">Next steps</span></span>
<span data-ttu-id="a06a5-290">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="a06a5-290">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="a06a5-291">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="a06a5-291">Create a data factory.</span></span> 
> * <span data-ttu-id="a06a5-292">Create a self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="a06a5-292">Create a self-hosted integration runtime</span></span>
> * <span data-ttu-id="a06a5-293">Create Azure Storage and Azure HDInsight linked services</span><span class="sxs-lookup"><span data-stu-id="a06a5-293">Create Azure Storage and Azure HDInsight linked services</span></span>
> * <span data-ttu-id="a06a5-294">Create a pipeline with Hive activity.</span><span class="sxs-lookup"><span data-stu-id="a06a5-294">Create a pipeline with Hive activity.</span></span>
> * <span data-ttu-id="a06a5-295">Trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="a06a5-295">Trigger a pipeline run.</span></span>
> * <span data-ttu-id="a06a5-296">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="a06a5-296">Monitor the pipeline run</span></span> 
> * <span data-ttu-id="a06a5-297">Verify the output</span><span class="sxs-lookup"><span data-stu-id="a06a5-297">Verify the output</span></span>

<span data-ttu-id="a06a5-298">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span><span class="sxs-lookup"><span data-stu-id="a06a5-298">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="a06a5-299">Branching and chaining Data Factory control flow</span><span class="sxs-lookup"><span data-stu-id="a06a5-299">Branching and chaining Data Factory control flow</span></span>](tutorial-control-flow-portal.md)



