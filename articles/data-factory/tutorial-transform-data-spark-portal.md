---
title: Transform data by using Spark in Azure Data Factory | Microsoft Docs
description: This tutorial provides step-by-step instructions for transforming data by using a Spark activity in Azure Data Factory.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/10/2018
ms.author: douglasl
ms.openlocfilehash: c6817fa20d4177efd3e38f1454f3142f6d40a07d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865805"
---
# <a name="transform-data-in-the-cloud-by-using-a-spark-activity-in-azure-data-factory"></a><span data-ttu-id="08941-103">Transform data in the cloud by using a Spark activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="08941-103">Transform data in the cloud by using a Spark activity in Azure Data Factory</span></span>
<span data-ttu-id="08941-104">In this tutorial, you use the Azure portal to create an Azure Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="08941-104">In this tutorial, you use the Azure portal to create an Azure Data Factory pipeline.</span></span> <span data-ttu-id="08941-105">This pipeline transforms data by using a Spark activity and an on-demand Azure HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="08941-105">This pipeline transforms data by using a Spark activity and an on-demand Azure HDInsight linked service.</span></span> 

<span data-ttu-id="08941-106">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="08941-106">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="08941-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="08941-107">Create a data factory.</span></span> 
> * <span data-ttu-id="08941-108">Create a pipeline that uses a Spark activity.</span><span class="sxs-lookup"><span data-stu-id="08941-108">Create a pipeline that uses a Spark activity.</span></span>
> * <span data-ttu-id="08941-109">Trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="08941-109">Trigger a pipeline run.</span></span>
> * <span data-ttu-id="08941-110">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="08941-110">Monitor the pipeline run.</span></span>

<span data-ttu-id="08941-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="08941-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08941-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="08941-112">Prerequisites</span></span>
* <span data-ttu-id="08941-113">**Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="08941-113">**Azure storage account**.</span></span> <span data-ttu-id="08941-114">You create a Python script and an input file, and you upload them to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="08941-114">You create a Python script and an input file, and you upload them to Azure Storage.</span></span> <span data-ttu-id="08941-115">The output from the Spark program is stored in this storage account.</span><span class="sxs-lookup"><span data-stu-id="08941-115">The output from the Spark program is stored in this storage account.</span></span> <span data-ttu-id="08941-116">The on-demand Spark cluster uses the same storage account as its primary storage.</span><span class="sxs-lookup"><span data-stu-id="08941-116">The on-demand Spark cluster uses the same storage account as its primary storage.</span></span>  
* <span data-ttu-id="08941-117">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="08941-117">**Azure PowerShell**.</span></span> <span data-ttu-id="08941-118">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="08941-118">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>


### <a name="upload-the-python-script-to-your-blob-storage-account"></a><span data-ttu-id="08941-119">Upload the Python script to your Blob storage account</span><span class="sxs-lookup"><span data-stu-id="08941-119">Upload the Python script to your Blob storage account</span></span>
1. <span data-ttu-id="08941-120">Create a Python file named **WordCount_Spark.py** with the following content:</span><span class="sxs-lookup"><span data-stu-id="08941-120">Create a Python file named **WordCount_Spark.py** with the following content:</span></span> 

    ```python
    import sys
    from operator import add
    
    from pyspark.sql import SparkSession
    
    def main():
        spark = SparkSession\
            .builder\
            .appName("PythonWordCount")\
            .getOrCreate()
            
        lines = spark.read.text("wasbs://adftutorial@<storageaccountname>.blob.core.windows.net/spark/inputfiles/minecraftstory.txt").rdd.map(lambda r: r[0])
        counts = lines.flatMap(lambda x: x.split(' ')) \
            .map(lambda x: (x, 1)) \
            .reduceByKey(add)
        counts.saveAsTextFile("wasbs://adftutorial@<storageaccountname>.blob.core.windows.net/spark/outputfiles/wordcount")
        
        spark.stop()
    
    if __name__ == "__main__":
        main()
    ```
1. <span data-ttu-id="08941-121">Replace *&lt;storageAccountName&gt;* with the name of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="08941-121">Replace *&lt;storageAccountName&gt;* with the name of your Azure storage account.</span></span> <span data-ttu-id="08941-122">Then, save the file.</span><span class="sxs-lookup"><span data-stu-id="08941-122">Then, save the file.</span></span> 
1. <span data-ttu-id="08941-123">In Azure Blob storage, create a container named **adftutorial** if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="08941-123">In Azure Blob storage, create a container named **adftutorial** if it does not exist.</span></span> 
1. <span data-ttu-id="08941-124">Create a folder named **spark**.</span><span class="sxs-lookup"><span data-stu-id="08941-124">Create a folder named **spark**.</span></span>
1. <span data-ttu-id="08941-125">Create a subfolder named **script** under the **spark** folder.</span><span class="sxs-lookup"><span data-stu-id="08941-125">Create a subfolder named **script** under the **spark** folder.</span></span> 
1. <span data-ttu-id="08941-126">Upload the **WordCount_Spark.py** file to the **script** subfolder.</span><span class="sxs-lookup"><span data-stu-id="08941-126">Upload the **WordCount_Spark.py** file to the **script** subfolder.</span></span> 


### <a name="upload-the-input-file"></a><span data-ttu-id="08941-127">Upload the input file</span><span class="sxs-lookup"><span data-stu-id="08941-127">Upload the input file</span></span>
1. <span data-ttu-id="08941-128">Create a file named **minecraftstory.txt** with some text.</span><span class="sxs-lookup"><span data-stu-id="08941-128">Create a file named **minecraftstory.txt** with some text.</span></span> <span data-ttu-id="08941-129">The Spark program counts the number of words in this text.</span><span class="sxs-lookup"><span data-stu-id="08941-129">The Spark program counts the number of words in this text.</span></span> 
1. <span data-ttu-id="08941-130">Create a subfolder named **inputfiles** in the **spark** folder.</span><span class="sxs-lookup"><span data-stu-id="08941-130">Create a subfolder named **inputfiles** in the **spark** folder.</span></span> 
1. <span data-ttu-id="08941-131">Upload the **minecraftstory.txt** file to the **inputfiles** subfolder.</span><span class="sxs-lookup"><span data-stu-id="08941-131">Upload the **minecraftstory.txt** file to the **inputfiles** subfolder.</span></span> 

## <a name="create-a-data-factory"></a><span data-ttu-id="08941-132">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="08941-132">Create a data factory</span></span>

1. <span data-ttu-id="08941-133">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="08941-133">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="08941-134">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="08941-134">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="08941-135">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="08941-135">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span></span> 
   
   ![Data Factory selection in the "New" pane](./media/tutorial-transform-data-spark-portal/new-azure-data-factory-menu.png)
1. <span data-ttu-id="08941-137">In the **New data factory** pane, enter **ADFTutorialDataFactory** under **Name**.</span><span class="sxs-lookup"><span data-stu-id="08941-137">In the **New data factory** pane, enter **ADFTutorialDataFactory** under **Name**.</span></span> 
      
   !["New data factory" pane](./media/tutorial-transform-data-spark-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="08941-139">The name of the Azure data factory must be *globally unique*.</span><span class="sxs-lookup"><span data-stu-id="08941-139">The name of the Azure data factory must be *globally unique*.</span></span> <span data-ttu-id="08941-140">If you see the following error, change the name of the data factory.</span><span class="sxs-lookup"><span data-stu-id="08941-140">If you see the following error, change the name of the data factory.</span></span> <span data-ttu-id="08941-141">(For example, use **&lt;yourname&gt;ADFTutorialDataFactory**).</span><span class="sxs-lookup"><span data-stu-id="08941-141">(For example, use **&lt;yourname&gt;ADFTutorialDataFactory**).</span></span> <span data-ttu-id="08941-142">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](naming-rules.md) article.</span><span class="sxs-lookup"><span data-stu-id="08941-142">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](naming-rules.md) article.</span></span>
  
   ![Error when a name is not available](./media/tutorial-transform-data-spark-portal/name-not-available-error.png)
1. <span data-ttu-id="08941-144">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="08941-144">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="08941-145">For **Resource Group**, take one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="08941-145">For **Resource Group**, take one of the following steps:</span></span>
     
   - <span data-ttu-id="08941-146">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="08941-146">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
   - <span data-ttu-id="08941-147">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="08941-147">Select **Create new**, and enter the name of a resource group.</span></span>   
         
   <span data-ttu-id="08941-148">Some of the steps in this quickstart assume that you use the name **ADFTutorialResourceGroup** for the resource group.</span><span class="sxs-lookup"><span data-stu-id="08941-148">Some of the steps in this quickstart assume that you use the name **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="08941-149">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08941-149">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
1. <span data-ttu-id="08941-150">For **Version**, select **V2**.</span><span class="sxs-lookup"><span data-stu-id="08941-150">For **Version**, select **V2**.</span></span>
1. <span data-ttu-id="08941-151">For **Location**, select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="08941-151">For **Location**, select the location for the data factory.</span></span> 

   <span data-ttu-id="08941-152">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="08941-152">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="08941-153">The data stores (like Azure Storage and Azure SQL Database) and computes (like HDInsight) that Data Factory uses can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="08941-153">The data stores (like Azure Storage and Azure SQL Database) and computes (like HDInsight) that Data Factory uses can be in other regions.</span></span>
1. <span data-ttu-id="08941-154">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="08941-154">Select **Pin to dashboard**.</span></span>     
1. <span data-ttu-id="08941-155">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="08941-155">Select **Create**.</span></span>
1. <span data-ttu-id="08941-156">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="08941-156">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span> 

   !["Deploying Data Factory" tile](media//tutorial-transform-data-spark-portal/deploying-data-factory.png)
1. <span data-ttu-id="08941-158">After the creation is complete, you see the **Data factory** page.</span><span class="sxs-lookup"><span data-stu-id="08941-158">After the creation is complete, you see the **Data factory** page.</span></span> <span data-ttu-id="08941-159">Select the **Author & Monitor** tile to start the Data Factory UI application on a separate tab.</span><span class="sxs-lookup"><span data-stu-id="08941-159">Select the **Author & Monitor** tile to start the Data Factory UI application on a separate tab.</span></span>

    ![Home page for the data factory, with the "Author & Monitor" tile](./media/tutorial-transform-data-spark-portal/data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="08941-161">Create linked services</span><span class="sxs-lookup"><span data-stu-id="08941-161">Create linked services</span></span>
<span data-ttu-id="08941-162">You author two linked services in this section:</span><span class="sxs-lookup"><span data-stu-id="08941-162">You author two linked services in this section:</span></span> 
    
- <span data-ttu-id="08941-163">An **Azure Storage linked service** that links an Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="08941-163">An **Azure Storage linked service** that links an Azure storage account to the data factory.</span></span> <span data-ttu-id="08941-164">This storage is used by the on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="08941-164">This storage is used by the on-demand HDInsight cluster.</span></span> <span data-ttu-id="08941-165">It also contains the Spark script to be run.</span><span class="sxs-lookup"><span data-stu-id="08941-165">It also contains the Spark script to be run.</span></span> 
- <span data-ttu-id="08941-166">An **on-demand HDInsight linked service**.</span><span class="sxs-lookup"><span data-stu-id="08941-166">An **on-demand HDInsight linked service**.</span></span> <span data-ttu-id="08941-167">Azure Data Factory automatically creates an HDInsight cluster and runs the Spark program.</span><span class="sxs-lookup"><span data-stu-id="08941-167">Azure Data Factory automatically creates an HDInsight cluster and runs the Spark program.</span></span> <span data-ttu-id="08941-168">It then deletes the HDInsight cluster after the cluster is idle for a preconfigured time.</span><span class="sxs-lookup"><span data-stu-id="08941-168">It then deletes the HDInsight cluster after the cluster is idle for a preconfigured time.</span></span> 

### <a name="create-an-azure-storage-linked-service"></a><span data-ttu-id="08941-169">Create an Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="08941-169">Create an Azure Storage linked service</span></span>

1. <span data-ttu-id="08941-170">On the **Let's get started** page, switch to the **Edit** tab in the left panel.</span><span class="sxs-lookup"><span data-stu-id="08941-170">On the **Let's get started** page, switch to the **Edit** tab in the left panel.</span></span> 

   !["Let's get started" page](./media/tutorial-transform-data-spark-portal/get-started-page.png)

1. <span data-ttu-id="08941-172">Select **Connections** at the bottom of the window, and then select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="08941-172">Select **Connections** at the bottom of the window, and then select **+ New**.</span></span> 

   ![Buttons for creating a new connection](./media/tutorial-transform-data-spark-portal/new-connection.png)
1. <span data-ttu-id="08941-174">In the **New Linked Service** window, select **Data Store** > **Azure Blob Storage**, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="08941-174">In the **New Linked Service** window, select **Data Store** > **Azure Blob Storage**, and then select **Continue**.</span></span> 

   ![Selecting the "Azure Blob Storage" tile](./media/tutorial-transform-data-spark-portal/select-azure-storage.png)
1. <span data-ttu-id="08941-176">For **Storage account name**, select the name from the list, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="08941-176">For **Storage account name**, select the name from the list, and then select **Save**.</span></span> 

   ![Box for specifying the storage account name](./media/tutorial-transform-data-spark-portal/new-azure-storage-linked-service.png)


### <a name="create-an-on-demand-hdinsight-linked-service"></a><span data-ttu-id="08941-178">Create an on-demand HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="08941-178">Create an on-demand HDInsight linked service</span></span>

1. <span data-ttu-id="08941-179">Select the **+ New** button again to create another linked service.</span><span class="sxs-lookup"><span data-stu-id="08941-179">Select the **+ New** button again to create another linked service.</span></span> 
1. <span data-ttu-id="08941-180">In the **New Linked Service** window, select **Compute** > **Azure HDInsight**, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="08941-180">In the **New Linked Service** window, select **Compute** > **Azure HDInsight**, and then select **Continue**.</span></span> 

   ![Selecting the "Azure HDInsight" tile](./media/tutorial-transform-data-spark-portal/select-azure-hdinsight.png)
1. <span data-ttu-id="08941-182">In the **New Linked Service** window, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="08941-182">In the **New Linked Service** window, complete the following steps:</span></span> 

   <span data-ttu-id="08941-183">a.</span><span class="sxs-lookup"><span data-stu-id="08941-183">a.</span></span> <span data-ttu-id="08941-184">For **Name**, enter **AzureHDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="08941-184">For **Name**, enter **AzureHDInsightLinkedService**.</span></span>
   
   <span data-ttu-id="08941-185">b.</span><span class="sxs-lookup"><span data-stu-id="08941-185">b.</span></span> <span data-ttu-id="08941-186">For **Type**, confirm that **On-demand HDInsight** is selected.</span><span class="sxs-lookup"><span data-stu-id="08941-186">For **Type**, confirm that **On-demand HDInsight** is selected.</span></span>
   
   <span data-ttu-id="08941-187">c.</span><span class="sxs-lookup"><span data-stu-id="08941-187">c.</span></span> <span data-ttu-id="08941-188">For **Azure Storage Linked Service**, select **AzureStorage1**.</span><span class="sxs-lookup"><span data-stu-id="08941-188">For **Azure Storage Linked Service**, select **AzureStorage1**.</span></span> <span data-ttu-id="08941-189">You created this linked service earlier.</span><span class="sxs-lookup"><span data-stu-id="08941-189">You created this linked service earlier.</span></span> <span data-ttu-id="08941-190">If you used a different name, specify the right name here.</span><span class="sxs-lookup"><span data-stu-id="08941-190">If you used a different name, specify the right name here.</span></span> 
   
   <span data-ttu-id="08941-191">d.</span><span class="sxs-lookup"><span data-stu-id="08941-191">d.</span></span> <span data-ttu-id="08941-192">For **Cluster type**, select **spark**.</span><span class="sxs-lookup"><span data-stu-id="08941-192">For **Cluster type**, select **spark**.</span></span>
   
   <span data-ttu-id="08941-193">e.</span><span class="sxs-lookup"><span data-stu-id="08941-193">e.</span></span> <span data-ttu-id="08941-194">For **Service principal id**, enter the ID of the service principal that has permission to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="08941-194">For **Service principal id**, enter the ID of the service principal that has permission to create an HDInsight cluster.</span></span> 
   
      <span data-ttu-id="08941-195">This service principal needs to be a member of the Contributor role of the subscription or the resource group in which the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="08941-195">This service principal needs to be a member of the Contributor role of the subscription or the resource group in which the cluster is created.</span></span> <span data-ttu-id="08941-196">For more information, see [Create an Azure Active Directory application and service principal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08941-196">For more information, see [Create an Azure Active Directory application and service principal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>
   
   <span data-ttu-id="08941-197">f.</span><span class="sxs-lookup"><span data-stu-id="08941-197">f.</span></span> <span data-ttu-id="08941-198">For **Service principal key**, enter the key.</span><span class="sxs-lookup"><span data-stu-id="08941-198">For **Service principal key**, enter the key.</span></span> 
   
   <span data-ttu-id="08941-199">g.</span><span class="sxs-lookup"><span data-stu-id="08941-199">g.</span></span> <span data-ttu-id="08941-200">For **Resource group**, select the same resource group that you used when you created the data factory.</span><span class="sxs-lookup"><span data-stu-id="08941-200">For **Resource group**, select the same resource group that you used when you created the data factory.</span></span> <span data-ttu-id="08941-201">The Spark cluster is created in this resource group.</span><span class="sxs-lookup"><span data-stu-id="08941-201">The Spark cluster is created in this resource group.</span></span> 
   
   <span data-ttu-id="08941-202">h.</span><span class="sxs-lookup"><span data-stu-id="08941-202">h.</span></span> <span data-ttu-id="08941-203">Expand **OS type**.</span><span class="sxs-lookup"><span data-stu-id="08941-203">Expand **OS type**.</span></span>
   
   <span data-ttu-id="08941-204">i.</span><span class="sxs-lookup"><span data-stu-id="08941-204">i.</span></span> <span data-ttu-id="08941-205">Enter a name for the cluster user.</span><span class="sxs-lookup"><span data-stu-id="08941-205">Enter a name for the cluster user.</span></span> 
   
   <span data-ttu-id="08941-206">j.</span><span class="sxs-lookup"><span data-stu-id="08941-206">j.</span></span> <span data-ttu-id="08941-207">Enter the password for the user.</span><span class="sxs-lookup"><span data-stu-id="08941-207">Enter the password for the user.</span></span> 
   
   <span data-ttu-id="08941-208">k.</span><span class="sxs-lookup"><span data-stu-id="08941-208">k.</span></span> <span data-ttu-id="08941-209">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="08941-209">Select **Save**.</span></span> 

   ![HDInsight linked service settings](./media/tutorial-transform-data-spark-portal/azure-hdinsight-linked-service-settings.png)

> [!NOTE]
> <span data-ttu-id="08941-211">Azure HDInsight limits the total number of cores that you can use in each Azure region that it supports.</span><span class="sxs-lookup"><span data-stu-id="08941-211">Azure HDInsight limits the total number of cores that you can use in each Azure region that it supports.</span></span> <span data-ttu-id="08941-212">For the on-demand HDInsight linked service, the HDInsight cluster is created in the same Azure Storage location that's used as its primary storage.</span><span class="sxs-lookup"><span data-stu-id="08941-212">For the on-demand HDInsight linked service, the HDInsight cluster is created in the same Azure Storage location that's used as its primary storage.</span></span> <span data-ttu-id="08941-213">Ensure that you have enough core quotas for the cluster to be created successfully.</span><span class="sxs-lookup"><span data-stu-id="08941-213">Ensure that you have enough core quotas for the cluster to be created successfully.</span></span> <span data-ttu-id="08941-214">For more information, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="08941-214">For more information, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span> 

## <a name="create-a-pipeline"></a><span data-ttu-id="08941-215">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="08941-215">Create a pipeline</span></span>

1. <span data-ttu-id="08941-216">Select the **+** (plus) button, and then select **Pipeline** on the menu.</span><span class="sxs-lookup"><span data-stu-id="08941-216">Select the **+** (plus) button, and then select **Pipeline** on the menu.</span></span>

   ![Buttons for creating a new pipeline](./media/tutorial-transform-data-spark-portal/new-pipeline-menu.png)
1. <span data-ttu-id="08941-218">In the **Activities** toolbox, expand **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="08941-218">In the **Activities** toolbox, expand **HDInsight**.</span></span> <span data-ttu-id="08941-219">Drag the **Spark** activity from the **Activities** toolbox to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="08941-219">Drag the **Spark** activity from the **Activities** toolbox to the pipeline designer surface.</span></span> 

   ![Dragging the Spark activity](./media/tutorial-transform-data-spark-portal/drag-drop-spark-activity.png)
1. <span data-ttu-id="08941-221">In the properties for the **Spark** activity window at the bottom, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="08941-221">In the properties for the **Spark** activity window at the bottom, complete the following steps:</span></span> 

   <span data-ttu-id="08941-222">a.</span><span class="sxs-lookup"><span data-stu-id="08941-222">a.</span></span> <span data-ttu-id="08941-223">Switch to the **HDI Cluster** tab.</span><span class="sxs-lookup"><span data-stu-id="08941-223">Switch to the **HDI Cluster** tab.</span></span>
   
   <span data-ttu-id="08941-224">b.</span><span class="sxs-lookup"><span data-stu-id="08941-224">b.</span></span> <span data-ttu-id="08941-225">Select **AzureHDInsightLinkedService** (which you created in the previous procedure).</span><span class="sxs-lookup"><span data-stu-id="08941-225">Select **AzureHDInsightLinkedService** (which you created in the previous procedure).</span></span> 
        
   ![Specifying the HDInsight linked service](./media/tutorial-transform-data-spark-portal/select-hdinsight-linked-service.png)
1. <span data-ttu-id="08941-227">Switch to the **Script/Jar** tab, and complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="08941-227">Switch to the **Script/Jar** tab, and complete the following steps:</span></span> 

   <span data-ttu-id="08941-228">a.</span><span class="sxs-lookup"><span data-stu-id="08941-228">a.</span></span> <span data-ttu-id="08941-229">For **Job Linked Service**, select **AzureStorage1**.</span><span class="sxs-lookup"><span data-stu-id="08941-229">For **Job Linked Service**, select **AzureStorage1**.</span></span>
   
   <span data-ttu-id="08941-230">b.</span><span class="sxs-lookup"><span data-stu-id="08941-230">b.</span></span> <span data-ttu-id="08941-231">Select **Browse Storage**.</span><span class="sxs-lookup"><span data-stu-id="08941-231">Select **Browse Storage**.</span></span>

   ![Specifying the Spark script on the "Script/Jar" tab](./media/tutorial-transform-data-spark-portal/specify-spark-script.png)
   
   <span data-ttu-id="08941-233">c.</span><span class="sxs-lookup"><span data-stu-id="08941-233">c.</span></span> <span data-ttu-id="08941-234">Browse to the **adftutorial/spark/script** folder, select **WordCount_Spark.py**, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="08941-234">Browse to the **adftutorial/spark/script** folder, select **WordCount_Spark.py**, and then select **Finish**.</span></span>      

1. <span data-ttu-id="08941-235">To validate the pipeline, select the **Validate** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="08941-235">To validate the pipeline, select the **Validate** button on the toolbar.</span></span> <span data-ttu-id="08941-236">Select the **>>** (right arrow) button to close the validation window.</span><span class="sxs-lookup"><span data-stu-id="08941-236">Select the **>>** (right arrow) button to close the validation window.</span></span> 
    
   !["Validate" button](./media/tutorial-transform-data-spark-portal/validate-button.png)
1. <span data-ttu-id="08941-238">Select **Publish All**.</span><span class="sxs-lookup"><span data-stu-id="08941-238">Select **Publish All**.</span></span> <span data-ttu-id="08941-239">The Data Factory UI publishes entities (linked services and pipeline) to the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="08941-239">The Data Factory UI publishes entities (linked services and pipeline) to the Azure Data Factory service.</span></span> 
    
   !["Publish All" button](./media/tutorial-transform-data-spark-portal/publish-button.png)


## <a name="trigger-a-pipeline-run"></a><span data-ttu-id="08941-241">Trigger a pipeline run</span><span class="sxs-lookup"><span data-stu-id="08941-241">Trigger a pipeline run</span></span>
<span data-ttu-id="08941-242">Select **Trigger** on the toolbar, and then select **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="08941-242">Select **Trigger** on the toolbar, and then select **Trigger Now**.</span></span> 

!["Trigger" and "Trigger Now" buttons](./media/tutorial-transform-data-spark-portal/trigger-now-menu.png)

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="08941-244">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="08941-244">Monitor the pipeline run</span></span>

1. <span data-ttu-id="08941-245">Switch to the **Monitor** tab. Confirm that you see a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="08941-245">Switch to the **Monitor** tab. Confirm that you see a pipeline run.</span></span> <span data-ttu-id="08941-246">It takes approximately 20 minutes to create a Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="08941-246">It takes approximately 20 minutes to create a Spark cluster.</span></span> 
   
1. <span data-ttu-id="08941-247">Select **Refresh** periodically to check the status of the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="08941-247">Select **Refresh** periodically to check the status of the pipeline run.</span></span> 

   ![Tab for monitoring pipeline runs, with "Refresh" button](./media/tutorial-transform-data-spark-portal/monitor-tab.png)

1. <span data-ttu-id="08941-249">To see activity runs associated with the pipeline run, select **View Activity Runs** in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="08941-249">To see activity runs associated with the pipeline run, select **View Activity Runs** in the **Actions** column.</span></span>

   ![Pipeline run status](./media/tutorial-transform-data-spark-portal/pipeline-run-succeeded.png) 

   <span data-ttu-id="08941-251">You can switch back to the pipeline runs view by selecting the **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="08941-251">You can switch back to the pipeline runs view by selecting the **Pipelines** link at the top.</span></span>

   !["Activity Runs" view](./media/tutorial-transform-data-spark-portal/activity-runs.png)

## <a name="verify-the-output"></a><span data-ttu-id="08941-253">Verify the output</span><span class="sxs-lookup"><span data-stu-id="08941-253">Verify the output</span></span>
<span data-ttu-id="08941-254">Verify that the output file is created in the spark/otuputfiles/wordcount folder of the adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="08941-254">Verify that the output file is created in the spark/otuputfiles/wordcount folder of the adftutorial container.</span></span> 

![Location of the output file](./media/tutorial-transform-data-spark-portal/verity-output.png)

<span data-ttu-id="08941-256">The file should have each word from the input text file and the number of times the word appeared in the file.</span><span class="sxs-lookup"><span data-stu-id="08941-256">The file should have each word from the input text file and the number of times the word appeared in the file.</span></span> <span data-ttu-id="08941-257">For example:</span><span class="sxs-lookup"><span data-stu-id="08941-257">For example:</span></span> 

```
(u'This', 1)
(u'a', 1)
(u'is', 1)
(u'test', 1)
(u'file', 1)
```

## <a name="next-steps"></a><span data-ttu-id="08941-258">Next steps</span><span class="sxs-lookup"><span data-stu-id="08941-258">Next steps</span></span>
<span data-ttu-id="08941-259">The pipeline in this sample transforms data by using a Spark activity and an on-demand HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="08941-259">The pipeline in this sample transforms data by using a Spark activity and an on-demand HDInsight linked service.</span></span> <span data-ttu-id="08941-260">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="08941-260">You learned how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="08941-261">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="08941-261">Create a data factory.</span></span> 
> * <span data-ttu-id="08941-262">Create a pipeline that uses a Spark activity.</span><span class="sxs-lookup"><span data-stu-id="08941-262">Create a pipeline that uses a Spark activity.</span></span>
> * <span data-ttu-id="08941-263">Trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="08941-263">Trigger a pipeline run.</span></span>
> * <span data-ttu-id="08941-264">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="08941-264">Monitor the pipeline run.</span></span>

<span data-ttu-id="08941-265">To learn how to transform data by running a Hive script on an Azure HDInsight cluster that's in a virtual network, advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="08941-265">To learn how to transform data by running a Hive script on an Azure HDInsight cluster that's in a virtual network, advance to the next tutorial:</span></span> 

> [!div class="nextstepaction"]
> <span data-ttu-id="08941-266">[Tutorial: Transform data using Hive in Azure Virtual Network](tutorial-transform-data-hive-virtual-network-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08941-266">[Tutorial: Transform data using Hive in Azure Virtual Network](tutorial-transform-data-hive-virtual-network-portal.md).</span></span>





