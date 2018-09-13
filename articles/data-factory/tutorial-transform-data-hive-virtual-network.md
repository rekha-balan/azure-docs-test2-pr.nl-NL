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
ms.date: 01/22/2018
ms.author: douglasl
ms.openlocfilehash: 94269056a7bf0a89c3d1b2f4968ad9ff90abbc82
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870244"
---
# <a name="transform-data-in-azure-virtual-network-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="1df39-103">Transform data in Azure Virtual Network using Hive activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1df39-103">Transform data in Azure Virtual Network using Hive activity in Azure Data Factory</span></span>
<span data-ttu-id="1df39-104">In this tutorial, you use Azure PowerShell to create a Data Factory pipeline that transforms data using Hive Activity on a HDInsight cluster that is in an Azure Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="1df39-104">In this tutorial, you use Azure PowerShell to create a Data Factory pipeline that transforms data using Hive Activity on a HDInsight cluster that is in an Azure Virtual Network (VNet).</span></span> <span data-ttu-id="1df39-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="1df39-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1df39-106">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="1df39-106">Create a data factory.</span></span> 
> * <span data-ttu-id="1df39-107">Author and setup self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="1df39-107">Author and setup self-hosted integration runtime</span></span>
> * <span data-ttu-id="1df39-108">Author and deploy linked services.</span><span class="sxs-lookup"><span data-stu-id="1df39-108">Author and deploy linked services.</span></span>
> * <span data-ttu-id="1df39-109">Author and deploy a pipeline that contains a Hive activity.</span><span class="sxs-lookup"><span data-stu-id="1df39-109">Author and deploy a pipeline that contains a Hive activity.</span></span>
> * <span data-ttu-id="1df39-110">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="1df39-110">Start a pipeline run.</span></span>
> * <span data-ttu-id="1df39-111">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="1df39-111">Monitor the pipeline run</span></span> 
> * <span data-ttu-id="1df39-112">verify the output.</span><span class="sxs-lookup"><span data-stu-id="1df39-112">verify the output.</span></span> 

<span data-ttu-id="1df39-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="1df39-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1df39-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1df39-114">Prerequisites</span></span>
- <span data-ttu-id="1df39-115">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="1df39-115">**Azure Storage account**.</span></span> <span data-ttu-id="1df39-116">You create a hive script, and upload it to the Azure storage.</span><span class="sxs-lookup"><span data-stu-id="1df39-116">You create a hive script, and upload it to the Azure storage.</span></span> <span data-ttu-id="1df39-117">The output from the Hive script is stored in this storage account.</span><span class="sxs-lookup"><span data-stu-id="1df39-117">The output from the Hive script is stored in this storage account.</span></span> <span data-ttu-id="1df39-118">In this sample, HDInsight cluster uses this Azure Storage account as the primary storage.</span><span class="sxs-lookup"><span data-stu-id="1df39-118">In this sample, HDInsight cluster uses this Azure Storage account as the primary storage.</span></span> 
- <span data-ttu-id="1df39-119">**Azure Virtual Network.**</span><span class="sxs-lookup"><span data-stu-id="1df39-119">**Azure Virtual Network.**</span></span> <span data-ttu-id="1df39-120">If you don't have an Azure virtual network, create it by following [these instructions](../virtual-network/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1df39-120">If you don't have an Azure virtual network, create it by following [these instructions](../virtual-network/quick-create-portal.md).</span></span> <span data-ttu-id="1df39-121">In this sample, the HDInsight is in an Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="1df39-121">In this sample, the HDInsight is in an Azure Virtual Network.</span></span> <span data-ttu-id="1df39-122">Here is a sample configuration of Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="1df39-122">Here is a sample configuration of Azure Virtual Network.</span></span> 

    ![Create virtual network](media/tutorial-transform-data-using-hive-in-vnet/create-virtual-network.png)
- <span data-ttu-id="1df39-124">**HDInsight cluster.**</span><span class="sxs-lookup"><span data-stu-id="1df39-124">**HDInsight cluster.**</span></span> <span data-ttu-id="1df39-125">Create a HDInsight cluster and join it to the virtual network you created in the previous step by following this article: [Extend Azure HDInsight using an Azure Virtual Network](../hdinsight/hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="1df39-125">Create a HDInsight cluster and join it to the virtual network you created in the previous step by following this article: [Extend Azure HDInsight using an Azure Virtual Network](../hdinsight/hdinsight-extend-hadoop-virtual-network.md).</span></span> <span data-ttu-id="1df39-126">Here is a sample configuration of HDInsight in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="1df39-126">Here is a sample configuration of HDInsight in a virtual network.</span></span> 

    ![HDInsight in a virtual network](media/tutorial-transform-data-using-hive-in-vnet/hdinsight-in-vnet-configuration.png)
- <span data-ttu-id="1df39-128">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1df39-128">**Azure PowerShell**.</span></span> <span data-ttu-id="1df39-129">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1df39-129">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

### <a name="upload-hive-script-to-your-blob-storage-account"></a><span data-ttu-id="1df39-130">Upload Hive script to your Blob Storage account</span><span class="sxs-lookup"><span data-stu-id="1df39-130">Upload Hive script to your Blob Storage account</span></span>

1. <span data-ttu-id="1df39-131">Create a Hive SQL file named **hivescript.hql** with the following content:</span><span class="sxs-lookup"><span data-stu-id="1df39-131">Create a Hive SQL file named **hivescript.hql** with the following content:</span></span>

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
2. <span data-ttu-id="1df39-132">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="1df39-132">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span></span>
3. <span data-ttu-id="1df39-133">Create a folder named **hivescripts**.</span><span class="sxs-lookup"><span data-stu-id="1df39-133">Create a folder named **hivescripts**.</span></span>
4. <span data-ttu-id="1df39-134">Upload the **hivescript.hql** file to the **hivescripts** subfolder.</span><span class="sxs-lookup"><span data-stu-id="1df39-134">Upload the **hivescript.hql** file to the **hivescripts** subfolder.</span></span>

 

## <a name="create-a-data-factory"></a><span data-ttu-id="1df39-135">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="1df39-135">Create a data factory</span></span>


1. <span data-ttu-id="1df39-136">Set the resource group name.</span><span class="sxs-lookup"><span data-stu-id="1df39-136">Set the resource group name.</span></span> <span data-ttu-id="1df39-137">You create a resource group as part of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1df39-137">You create a resource group as part of this tutorial.</span></span> <span data-ttu-id="1df39-138">However, you can use an existing resource group if you like.</span><span class="sxs-lookup"><span data-stu-id="1df39-138">However, you can use an existing resource group if you like.</span></span> 

    ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup" 
    ```
2. <span data-ttu-id="1df39-139">Specify the data factory name.</span><span class="sxs-lookup"><span data-stu-id="1df39-139">Specify the data factory name.</span></span> <span data-ttu-id="1df39-140">Must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="1df39-140">Must be globally unique.</span></span>

    ```powershell
    $dataFactoryName = "MyDataFactory09142017"
    ```
3. <span data-ttu-id="1df39-141">Specify a name for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="1df39-141">Specify a name for the pipeline.</span></span> 

    ```powershell
    $pipelineName = "MyHivePipeline" # 
    ```
4. <span data-ttu-id="1df39-142">Specify a name for the self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="1df39-142">Specify a name for the self-hosted integration runtime.</span></span> <span data-ttu-id="1df39-143">You need a self-hosted integration runtime when the Data Factory needs to access resources (such as Azure SQL Database) inside a VNet.</span><span class="sxs-lookup"><span data-stu-id="1df39-143">You need a self-hosted integration runtime when the Data Factory needs to access resources (such as Azure SQL Database) inside a VNet.</span></span> 
    ```powershell
    $selfHostedIntegrationRuntimeName = "MySelfHostedIR09142017" 
    ```
2. <span data-ttu-id="1df39-144">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1df39-144">Launch **PowerShell**.</span></span> <span data-ttu-id="1df39-145">Keep Azure PowerShell open until the end of this quickstart.</span><span class="sxs-lookup"><span data-stu-id="1df39-145">Keep Azure PowerShell open until the end of this quickstart.</span></span> <span data-ttu-id="1df39-146">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="1df39-146">If you close and reopen, you need to run the commands again.</span></span> <span data-ttu-id="1df39-147">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="1df39-147">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="1df39-148">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="1df39-148">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

    <span data-ttu-id="1df39-149">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="1df39-149">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>
        
    ```powershell
    Connect-AzureRmAccount
    ```        
    <span data-ttu-id="1df39-150">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="1df39-150">Run the following command to view all the subscriptions for this account:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```
    <span data-ttu-id="1df39-151">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="1df39-151">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="1df39-152">Replace **SubscriptionId** with the ID of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="1df39-152">Replace **SubscriptionId** with the ID of your Azure subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"    
    ```  
3. <span data-ttu-id="1df39-153">Create the resource group: ADFTutorialResourceGroup if it does not exist already in your subscription.</span><span class="sxs-lookup"><span data-stu-id="1df39-153">Create the resource group: ADFTutorialResourceGroup if it does not exist already in your subscription.</span></span> 

    ```powershell
    New-AzureRmResourceGroup -Name $resourceGroupName -Location "East Us" 
    ```
4. <span data-ttu-id="1df39-154">Create the data factory.</span><span class="sxs-lookup"><span data-stu-id="1df39-154">Create the data factory.</span></span> 

    ```powershell
     $df = Set-AzureRmDataFactoryV2 -Location EastUS -Name $dataFactoryName -ResourceGroupName $resourceGroupName
    ```

    <span data-ttu-id="1df39-155">Execute the following command to see the output:</span><span class="sxs-lookup"><span data-stu-id="1df39-155">Execute the following command to see the output:</span></span> 

    ```powershell
    $df
    ```

## <a name="create-self-hosted-ir"></a><span data-ttu-id="1df39-156">Create self-hosted IR</span><span class="sxs-lookup"><span data-stu-id="1df39-156">Create self-hosted IR</span></span>
<span data-ttu-id="1df39-157">In this section, you create a self-hosted integration runtime and associate it with an Azure VM in the same Azure Virtual Network where your HDInsight cluster is in.</span><span class="sxs-lookup"><span data-stu-id="1df39-157">In this section, you create a self-hosted integration runtime and associate it with an Azure VM in the same Azure Virtual Network where your HDInsight cluster is in.</span></span>

1. <span data-ttu-id="1df39-158">Create Self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="1df39-158">Create Self-hosted integration runtime.</span></span> <span data-ttu-id="1df39-159">Use a unique name in case if another integration runtime with the same name exists.</span><span class="sxs-lookup"><span data-stu-id="1df39-159">Use a unique name in case if another integration runtime with the same name exists.</span></span>

   ```powershell
   Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $selfHostedIntegrationRuntimeName -Type SelfHosted
   ```
    <span data-ttu-id="1df39-160">This command creates a logical registration of the self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="1df39-160">This command creates a logical registration of the self-hosted integration runtime.</span></span> 
2. <span data-ttu-id="1df39-161">Use PowerShell to retrieve authentication keys to register the self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="1df39-161">Use PowerShell to retrieve authentication keys to register the self-hosted integration runtime.</span></span> <span data-ttu-id="1df39-162">Copy one of the keys for registering the self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="1df39-162">Copy one of the keys for registering the self-hosted integration runtime.</span></span>

   ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntimeKey -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $selfHostedIntegrationRuntimeName | ConvertTo-Json
   ```

   <span data-ttu-id="1df39-163">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="1df39-163">Here is the sample output:</span></span> 

   ```powershell
   {
       "AuthKey1":  "IR@0000000000000000000000000000000000000=",
       "AuthKey2":  "IR@0000000000000000000000000000000000000="
   }
   ```
    <span data-ttu-id="1df39-164">Note down the value of **AuthKey1** without quotation mark.</span><span class="sxs-lookup"><span data-stu-id="1df39-164">Note down the value of **AuthKey1** without quotation mark.</span></span> 
3. <span data-ttu-id="1df39-165">Create an Azure VM and join it into the same virtual network that contains your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1df39-165">Create an Azure VM and join it into the same virtual network that contains your HDInsight cluster.</span></span> <span data-ttu-id="1df39-166">For details, see [How to create virtual machines](../virtual-network/quick-create-portal.md#create-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="1df39-166">For details, see [How to create virtual machines](../virtual-network/quick-create-portal.md#create-virtual-machines).</span></span> <span data-ttu-id="1df39-167">Join them into an Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="1df39-167">Join them into an Azure Virtual Network.</span></span> 
4. <span data-ttu-id="1df39-168">On the Azure VM, download [self-hosted integration runtime](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="1df39-168">On the Azure VM, download [self-hosted integration runtime](https://www.microsoft.com/download/details.aspx?id=39717).</span></span> <span data-ttu-id="1df39-169">Use the Authentication Key obtained in the previous step to manually register the self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="1df39-169">Use the Authentication Key obtained in the previous step to manually register the self-hosted integration runtime.</span></span> 

   ![Register integration runtime](media/tutorial-transform-data-using-hive-in-vnet/register-integration-runtime.png)

   <span data-ttu-id="1df39-171">You see the following message when the self-hosted integration runtime is registered successfully: ![Registered successfully](media/tutorial-transform-data-using-hive-in-vnet/registered-successfully.png)</span><span class="sxs-lookup"><span data-stu-id="1df39-171">You see the following message when the self-hosted integration runtime is registered successfully: ![Registered successfully](media/tutorial-transform-data-using-hive-in-vnet/registered-successfully.png)</span></span>

   <span data-ttu-id="1df39-172">You see the following page when the node is connected to the cloud service: ![Node is connected](media/tutorial-transform-data-using-hive-in-vnet/node-is-connected.png)</span><span class="sxs-lookup"><span data-stu-id="1df39-172">You see the following page when the node is connected to the cloud service: ![Node is connected](media/tutorial-transform-data-using-hive-in-vnet/node-is-connected.png)</span></span>

## <a name="author-linked-services"></a><span data-ttu-id="1df39-173">Author linked services</span><span class="sxs-lookup"><span data-stu-id="1df39-173">Author linked services</span></span>

<span data-ttu-id="1df39-174">You author and deploy two Linked Services in this section:</span><span class="sxs-lookup"><span data-stu-id="1df39-174">You author and deploy two Linked Services in this section:</span></span>
- <span data-ttu-id="1df39-175">An Azure Storage Linked Service that links an Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="1df39-175">An Azure Storage Linked Service that links an Azure Storage account to the data factory.</span></span> <span data-ttu-id="1df39-176">This storage is the primary storage used by your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1df39-176">This storage is the primary storage used by your HDInsight cluster.</span></span> <span data-ttu-id="1df39-177">In this case, we also use this Azure Storage account to keep the Hive script and output of the script.</span><span class="sxs-lookup"><span data-stu-id="1df39-177">In this case, we also use this Azure Storage account to keep the Hive script and output of the script.</span></span>
- <span data-ttu-id="1df39-178">An HDInsight Linked Service.</span><span class="sxs-lookup"><span data-stu-id="1df39-178">An HDInsight Linked Service.</span></span> <span data-ttu-id="1df39-179">Azure Data Factory submits the Hive script to this HDInsight cluster for execution.</span><span class="sxs-lookup"><span data-stu-id="1df39-179">Azure Data Factory submits the Hive script to this HDInsight cluster for execution.</span></span>

### <a name="azure-storage-linked-service"></a><span data-ttu-id="1df39-180">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="1df39-180">Azure Storage linked service</span></span>

<span data-ttu-id="1df39-181">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure Storage linked service, and then save the file as **MyStorageLinkedService.json**.</span><span class="sxs-lookup"><span data-stu-id="1df39-181">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure Storage linked service, and then save the file as **MyStorageLinkedService.json**.</span></span>

```json
{
    "name": "MyStorageLinkedService",
    "properties": {
      "type": "AzureStorage",
      "typeProperties": {
        "connectionString": {
          "value": "DefaultEndpointsProtocol=https;AccountName=<storageAccountName>;AccountKey=<storageAccountKey>",
          "type": "SecureString"
        }
      },
      "connectVia": {
        "referenceName": "MySelfhostedIR",
        "type": "IntegrationRuntimeReference"
      }  
    }
}
```

<span data-ttu-id="1df39-182">Replace **&lt;accountname&gt; and &lt;accountkey&gt;** with the name and key of your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="1df39-182">Replace **&lt;accountname&gt; and &lt;accountkey&gt;** with the name and key of your Azure Storage account.</span></span>

### <a name="hdinsight-linked-service"></a><span data-ttu-id="1df39-183">HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="1df39-183">HDInsight linked service</span></span>

<span data-ttu-id="1df39-184">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure HDInsight linked service, and save the file as **MyHDInsightLinkedService.json**.</span><span class="sxs-lookup"><span data-stu-id="1df39-184">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure HDInsight linked service, and save the file as **MyHDInsightLinkedService.json**.</span></span>

```
{
  "name": "MyHDInsightLinkedService",
  "properties": {     
      "type": "HDInsight",
      "typeProperties": {
          "clusterUri": "https://<clustername>.azurehdinsight.net",
          "userName": "<username>",
          "password": {
            "value": "<password>",
            "type": "SecureString"
          },
          "linkedServiceName": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
      },
      "connectVia": {
        "referenceName": "MySelfhostedIR",
        "type": "IntegrationRuntimeReference"
      }
  }
}
```

<span data-ttu-id="1df39-185">Update values for the following properties in the linked service definition:</span><span class="sxs-lookup"><span data-stu-id="1df39-185">Update values for the following properties in the linked service definition:</span></span>

- <span data-ttu-id="1df39-186">**userName**.</span><span class="sxs-lookup"><span data-stu-id="1df39-186">**userName**.</span></span> <span data-ttu-id="1df39-187">Name of the cluster login user that you specified when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="1df39-187">Name of the cluster login user that you specified when creating the cluster.</span></span> 
- <span data-ttu-id="1df39-188">**password**.</span><span class="sxs-lookup"><span data-stu-id="1df39-188">**password**.</span></span> <span data-ttu-id="1df39-189">The password for the user.</span><span class="sxs-lookup"><span data-stu-id="1df39-189">The password for the user.</span></span>
- <span data-ttu-id="1df39-190">**clusterUri**.</span><span class="sxs-lookup"><span data-stu-id="1df39-190">**clusterUri**.</span></span> <span data-ttu-id="1df39-191">Specify the URL of your HDInsight cluster in the following format: https://<clustername>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1df39-191">Specify the URL of your HDInsight cluster in the following format: https://<clustername>.azurehdinsight.net.</span></span>  <span data-ttu-id="1df39-192">This article assumes that you have access to the cluster over the internet.</span><span class="sxs-lookup"><span data-stu-id="1df39-192">This article assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="1df39-193">For example, you can connect to the cluster at `https://clustername.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="1df39-193">For example, you can connect to the cluster at `https://clustername.azurehdinsight.net`.</span></span> <span data-ttu-id="1df39-194">This address uses the public gateway, which is not available if you have used network security groups (NSGs) or user-defined routes (UDRs) to restrict access from the internet.</span><span class="sxs-lookup"><span data-stu-id="1df39-194">This address uses the public gateway, which is not available if you have used network security groups (NSGs) or user-defined routes (UDRs) to restrict access from the internet.</span></span> <span data-ttu-id="1df39-195">For Data Factory to submit jobs to HDInsight clusters in Azure Virtual Network, your Azure Virtual Network needs to be configured in such a way that the URL can be resolved to the private IP address of the gateway used by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1df39-195">For Data Factory to submit jobs to HDInsight clusters in Azure Virtual Network, your Azure Virtual Network needs to be configured in such a way that the URL can be resolved to the private IP address of the gateway used by HDInsight.</span></span>

  1. <span data-ttu-id="1df39-196">From Azure portal, open the Virtual Network the HDInsight is in.</span><span class="sxs-lookup"><span data-stu-id="1df39-196">From Azure portal, open the Virtual Network the HDInsight is in.</span></span> <span data-ttu-id="1df39-197">Open the network interface with name starting with `nic-gateway-0`.</span><span class="sxs-lookup"><span data-stu-id="1df39-197">Open the network interface with name starting with `nic-gateway-0`.</span></span> <span data-ttu-id="1df39-198">Note down its private IP address.</span><span class="sxs-lookup"><span data-stu-id="1df39-198">Note down its private IP address.</span></span> <span data-ttu-id="1df39-199">For example, 10.6.0.15.</span><span class="sxs-lookup"><span data-stu-id="1df39-199">For example, 10.6.0.15.</span></span> 
  2. <span data-ttu-id="1df39-200">If your Azure Virtual Network has DNS server, update the DNS record so the HDInsight cluster URL `https://<clustername>.azurehdinsight.net` can be resolved to `10.6.0.15`.</span><span class="sxs-lookup"><span data-stu-id="1df39-200">If your Azure Virtual Network has DNS server, update the DNS record so the HDInsight cluster URL `https://<clustername>.azurehdinsight.net` can be resolved to `10.6.0.15`.</span></span> <span data-ttu-id="1df39-201">This is the recommended approach.</span><span class="sxs-lookup"><span data-stu-id="1df39-201">This is the recommended approach.</span></span> <span data-ttu-id="1df39-202">If you don’t have a DNS server in your Azure Virtual Network, you can temporarily work around this by editing the hosts file (C:\Windows\System32\drivers\etc) of all VMs that registered as self-hosted integration runtime nodes by adding an entry like this:</span><span class="sxs-lookup"><span data-stu-id="1df39-202">If you don’t have a DNS server in your Azure Virtual Network, you can temporarily work around this by editing the hosts file (C:\Windows\System32\drivers\etc) of all VMs that registered as self-hosted integration runtime nodes by adding an entry like this:</span></span> 
  
        `10.6.0.15 myHDIClusterName.azurehdinsight.net`

## <a name="create-linked-services"></a><span data-ttu-id="1df39-203">Create linked services</span><span class="sxs-lookup"><span data-stu-id="1df39-203">Create linked services</span></span>
<span data-ttu-id="1df39-204">In the PowerShell, switch to the folder where you created JSON files, and run the following command to deploy the linked services:</span><span class="sxs-lookup"><span data-stu-id="1df39-204">In the PowerShell, switch to the folder where you created JSON files, and run the following command to deploy the linked services:</span></span> 

1. <span data-ttu-id="1df39-205">In the PowerShell, switch to the folder where you created JSON files.</span><span class="sxs-lookup"><span data-stu-id="1df39-205">In the PowerShell, switch to the folder where you created JSON files.</span></span>
2. <span data-ttu-id="1df39-206">Run the following command to create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="1df39-206">Run the following command to create an Azure Storage linked service.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyStorageLinkedService" -File "MyStorageLinkedService.json"
    ```
3. <span data-ttu-id="1df39-207">Run the following command to create an Azure HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="1df39-207">Run the following command to create an Azure HDInsight linked service.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyHDInsightLinkedService" -File "MyHDInsightLinkedService.json"
    ```

## <a name="author-a-pipeline"></a><span data-ttu-id="1df39-208">Author a pipeline</span><span class="sxs-lookup"><span data-stu-id="1df39-208">Author a pipeline</span></span>
<span data-ttu-id="1df39-209">In this step, you create a new pipeline with a Hive activity.</span><span class="sxs-lookup"><span data-stu-id="1df39-209">In this step, you create a new pipeline with a Hive activity.</span></span> <span data-ttu-id="1df39-210">The activity executes Hive script to return data from a sample table and save it to a path you defined.</span><span class="sxs-lookup"><span data-stu-id="1df39-210">The activity executes Hive script to return data from a sample table and save it to a path you defined.</span></span> <span data-ttu-id="1df39-211">Create a JSON file in your preferred editor, copy the following JSON definition of a pipeline definition, and save it as **MyHivePipeline.json**.</span><span class="sxs-lookup"><span data-stu-id="1df39-211">Create a JSON file in your preferred editor, copy the following JSON definition of a pipeline definition, and save it as **MyHivePipeline.json**.</span></span>


```json
{
  "name": "MyHivePipeline",
  "properties": {
    "activities": [
      {
        "name": "MyHiveActivity",
        "type": "HDInsightHive",
        "linkedServiceName": {
            "referenceName": "MyHDILinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "scriptPath": "adftutorial\\hivescripts\\hivescript.hql",
          "getDebugInfo": "Failure",
          "defines": {           
            "Output": "wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/"
          },
          "scriptLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
        }
      }
    ]
  }
}

```

<span data-ttu-id="1df39-212">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="1df39-212">Note the following points:</span></span>

- <span data-ttu-id="1df39-213">**scriptPath** points to path to Hive script on the Azure Storage Account you used for MyStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="1df39-213">**scriptPath** points to path to Hive script on the Azure Storage Account you used for MyStorageLinkedService.</span></span> <span data-ttu-id="1df39-214">The path is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="1df39-214">The path is case-sensitive.</span></span>
- <span data-ttu-id="1df39-215">**Output** is an argument used in the Hive script.</span><span class="sxs-lookup"><span data-stu-id="1df39-215">**Output** is an argument used in the Hive script.</span></span> <span data-ttu-id="1df39-216">Use the format of `wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/` to point it to an existing folder on your Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1df39-216">Use the format of `wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/` to point it to an existing folder on your Azure Storage.</span></span> <span data-ttu-id="1df39-217">The path is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="1df39-217">The path is case-sensitive.</span></span> 

<span data-ttu-id="1df39-218">Switch to the folder where you created JSON files, and run the following command to deploy the pipeline:</span><span class="sxs-lookup"><span data-stu-id="1df39-218">Switch to the folder where you created JSON files, and run the following command to deploy the pipeline:</span></span> 


```powershell
Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name $pipelineName -File "MyHivePipeline.json"
```

## <a name="start-the-pipeline"></a><span data-ttu-id="1df39-219">Start the pipeline</span><span class="sxs-lookup"><span data-stu-id="1df39-219">Start the pipeline</span></span> 

1. <span data-ttu-id="1df39-220">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="1df39-220">Start a pipeline run.</span></span> <span data-ttu-id="1df39-221">It also captures the pipeline run ID for future monitoring.</span><span class="sxs-lookup"><span data-stu-id="1df39-221">It also captures the pipeline run ID for future monitoring.</span></span>

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName
   ```
2. <span data-ttu-id="1df39-222">Run the following script to continuously check the pipeline run status until it finishes.</span><span class="sxs-lookup"><span data-stu-id="1df39-222">Run the following script to continuously check the pipeline run status until it finishes.</span></span>

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

        if(!$result) {
            Write-Host "Waiting for pipeline to start..." -foregroundcolor "Yellow"
        }
        elseif (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
        }
        else {
            Write-Host "Pipeline '"$pipelineName"' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
        ($result | Format-List | Out-String)
        Start-Sleep -Seconds 15
    }
    
    Write-Host "Activity `Output` section:" -foregroundcolor "Yellow"
    $result.Output -join "`r`n"

    Write-Host "Activity `Error` section:" -foregroundcolor "Yellow"
    $result.Error -join "`r`n"
    ```

   <span data-ttu-id="1df39-223">Here is the output of the sample run:</span><span class="sxs-lookup"><span data-stu-id="1df39-223">Here is the output of the sample run:</span></span>

    ```json
    Pipeline run status: In Progress
    
    ResourceGroupName : ADFV2SampleRG2
    DataFactoryName   : SampleV2DataFactory2
    ActivityName      : MyHiveActivity
    PipelineRunId     : 000000000-0000-0000-000000000000000000
    PipelineName      : MyHivePipeline
    Input             : {getDebugInfo, scriptPath, scriptLinkedService, defines}
    Output            :
    LinkedServiceName :
    ActivityRunStart  : 9/18/2017 6:58:13 AM
    ActivityRunEnd    :
    DurationInMs      :
    Status            : InProgress
    Error             :
    
    Pipeline ' MyHivePipeline' run finished. Result:
    
    ResourceGroupName : ADFV2SampleRG2
    DataFactoryName   : SampleV2DataFactory2
    ActivityName      : MyHiveActivity
    PipelineRunId     : 0000000-0000-0000-0000-000000000000
    PipelineName      : MyHivePipeline
    Input             : {getDebugInfo, scriptPath, scriptLinkedService, defines}
    Output            : {logLocation, clusterInUse, jobId, ExecutionProgress...}
    LinkedServiceName :
    ActivityRunStart  : 9/18/2017 6:58:13 AM
    ActivityRunEnd    : 9/18/2017 6:59:16 AM
    DurationInMs      : 63636
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    Activity Output section:
    "logLocation": "wasbs://adfjobs@adfv2samplestor.blob.core.windows.net/HiveQueryJobs/000000000-0000-47c3-9b28-1cdc7f3f2ba2/18_09_2017_06_58_18_023/Status"
    "clusterInUse": "https://adfv2HivePrivate.azurehdinsight.net"
    "jobId": "job_1505387997356_0024"
    "ExecutionProgress": "Succeeded"
    "effectiveIntegrationRuntime": "MySelfhostedIR"
    Activity Error section:
    "errorCode": ""
    "message": ""
    "failureType": ""
    "target": "MyHiveActivity"
    ```
4. <span data-ttu-id="1df39-224">Check the `outputfolder` folder for new file created as the Hive query result, it should look like the following sample output:</span><span class="sxs-lookup"><span data-stu-id="1df39-224">Check the `outputfolder` folder for new file created as the Hive query result, it should look like the following sample output:</span></span> 

   ```
   8 en-US SCH-i500 California
   23 en-US Incredible Pennsylvania
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   246 en-US SCH-i500 District Of Columbia
   246 en-US SCH-i500 District Of Columbia
   ```

## <a name="next-steps"></a><span data-ttu-id="1df39-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="1df39-225">Next steps</span></span>
<span data-ttu-id="1df39-226">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="1df39-226">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="1df39-227">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="1df39-227">Create a data factory.</span></span> 
> * <span data-ttu-id="1df39-228">Author and setup self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="1df39-228">Author and setup self-hosted integration runtime</span></span>
> * <span data-ttu-id="1df39-229">Author and deploy linked services.</span><span class="sxs-lookup"><span data-stu-id="1df39-229">Author and deploy linked services.</span></span>
> * <span data-ttu-id="1df39-230">Author and deploy a pipeline that contains a Hive activity.</span><span class="sxs-lookup"><span data-stu-id="1df39-230">Author and deploy a pipeline that contains a Hive activity.</span></span>
> * <span data-ttu-id="1df39-231">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="1df39-231">Start a pipeline run.</span></span>
> * <span data-ttu-id="1df39-232">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="1df39-232">Monitor the pipeline run</span></span> 
> * <span data-ttu-id="1df39-233">verify the output.</span><span class="sxs-lookup"><span data-stu-id="1df39-233">verify the output.</span></span> 

<span data-ttu-id="1df39-234">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span><span class="sxs-lookup"><span data-stu-id="1df39-234">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="1df39-235">Branching and chaining Data Factory control flow</span><span class="sxs-lookup"><span data-stu-id="1df39-235">Branching and chaining Data Factory control flow</span></span>](tutorial-control-flow.md)



