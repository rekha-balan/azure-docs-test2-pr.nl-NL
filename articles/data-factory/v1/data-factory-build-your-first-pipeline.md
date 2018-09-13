---
title: 'Data Factory tutorial: First data pipeline | Microsoft Docs'
description: This Azure Data Factory tutorial shows you how to create and schedule a data factory that processes data using Hive script on a Hadoop cluster.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
editor: ''
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 8f86bcf5ecf38f0f1054fce82b66e63f0509f1c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864597"
---
# <a name="tutorial-build-your-first-pipeline-to-transform-data-using-hadoop-cluster"></a><span data-ttu-id="192da-103">Tutorial: Build your first pipeline to transform data using Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="192da-103">Tutorial: Build your first pipeline to transform data using Hadoop cluster</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Quickstart: Create a data factory using Azure Data Factory](../quickstart-create-data-factory-dot-net.md).

<span data-ttu-id="192da-112">In this tutorial, you build your first Azure data factory with a data pipeline.</span><span class="sxs-lookup"><span data-stu-id="192da-112">In this tutorial, you build your first Azure data factory with a data pipeline.</span></span> <span data-ttu-id="192da-113">The pipeline transforms input data by running Hive script on an Azure HDInsight (Hadoop) cluster to produce output data.</span><span class="sxs-lookup"><span data-stu-id="192da-113">The pipeline transforms input data by running Hive script on an Azure HDInsight (Hadoop) cluster to produce output data.</span></span>  

<span data-ttu-id="192da-114">This article provides overview and prerequisites for the tutorial.</span><span class="sxs-lookup"><span data-stu-id="192da-114">This article provides overview and prerequisites for the tutorial.</span></span> <span data-ttu-id="192da-115">After you complete the prerequisites, you can do the tutorial using one of the following tools/SDKs: Azure portal, Visual Studio, PowerShell, Resource Manager template, REST API.</span><span class="sxs-lookup"><span data-stu-id="192da-115">After you complete the prerequisites, you can do the tutorial using one of the following tools/SDKs: Azure portal, Visual Studio, PowerShell, Resource Manager template, REST API.</span></span> <span data-ttu-id="192da-116">Select one of the options in the drop-down list at the beginning (or) links at the end of this article to do the tutorial using one of these options.</span><span class="sxs-lookup"><span data-stu-id="192da-116">Select one of the options in the drop-down list at the beginning (or) links at the end of this article to do the tutorial using one of these options.</span></span>    

## <a name="tutorial-overview"></a><span data-ttu-id="192da-117">Tutorial overview</span><span class="sxs-lookup"><span data-stu-id="192da-117">Tutorial overview</span></span>
<span data-ttu-id="192da-118">In this tutorial, you perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="192da-118">In this tutorial, you perform the following steps:</span></span>

1. <span data-ttu-id="192da-119">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="192da-119">Create a **data factory**.</span></span> <span data-ttu-id="192da-120">A data factory can contain one or more data pipelines that move and transform data.</span><span class="sxs-lookup"><span data-stu-id="192da-120">A data factory can contain one or more data pipelines that move and transform data.</span></span> 

    <span data-ttu-id="192da-121">In this tutorial, you create one pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="192da-121">In this tutorial, you create one pipeline in the data factory.</span></span> 
2. <span data-ttu-id="192da-122">Create a **pipeline**.</span><span class="sxs-lookup"><span data-stu-id="192da-122">Create a **pipeline**.</span></span> <span data-ttu-id="192da-123">A pipeline can have one or more activities (Examples: Copy Activity, HDInsight Hive Activity).</span><span class="sxs-lookup"><span data-stu-id="192da-123">A pipeline can have one or more activities (Examples: Copy Activity, HDInsight Hive Activity).</span></span> <span data-ttu-id="192da-124">This sample uses the HDInsight Hive activity that runs a Hive script on a HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="192da-124">This sample uses the HDInsight Hive activity that runs a Hive script on a HDInsight Hadoop cluster.</span></span> <span data-ttu-id="192da-125">The script first creates a table that references the raw web log data stored in Azure blob storage and then partitions the raw data by year and month.</span><span class="sxs-lookup"><span data-stu-id="192da-125">The script first creates a table that references the raw web log data stored in Azure blob storage and then partitions the raw data by year and month.</span></span>

    <span data-ttu-id="192da-126">In this tutorial, the pipeline uses the Hive Activity to transform data by running a Hive query on an Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="192da-126">In this tutorial, the pipeline uses the Hive Activity to transform data by running a Hive query on an Azure HDInsight Hadoop cluster.</span></span> 
3. <span data-ttu-id="192da-127">Create **linked services**.</span><span class="sxs-lookup"><span data-stu-id="192da-127">Create **linked services**.</span></span> <span data-ttu-id="192da-128">You create a linked service to link a data store or a compute service to the data factory.</span><span class="sxs-lookup"><span data-stu-id="192da-128">You create a linked service to link a data store or a compute service to the data factory.</span></span> <span data-ttu-id="192da-129">A data store such as Azure Storage holds input/output data of activities in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="192da-129">A data store such as Azure Storage holds input/output data of activities in the pipeline.</span></span> <span data-ttu-id="192da-130">A compute service such as HDInsight Hadoop cluster processes/transforms data.</span><span class="sxs-lookup"><span data-stu-id="192da-130">A compute service such as HDInsight Hadoop cluster processes/transforms data.</span></span>

    <span data-ttu-id="192da-131">In this tutorial, you create two linked services: **Azure Storage** and **Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="192da-131">In this tutorial, you create two linked services: **Azure Storage** and **Azure HDInsight**.</span></span> <span data-ttu-id="192da-132">The Azure Storage linked service links an Azure Storage Account that holds the input/output data to the data factory.</span><span class="sxs-lookup"><span data-stu-id="192da-132">The Azure Storage linked service links an Azure Storage Account that holds the input/output data to the data factory.</span></span> <span data-ttu-id="192da-133">Azure HDInsight linked service links an Azure HDInsight cluster that is used to transform data to the data factory.</span><span class="sxs-lookup"><span data-stu-id="192da-133">Azure HDInsight linked service links an Azure HDInsight cluster that is used to transform data to the data factory.</span></span> 
3. <span data-ttu-id="192da-134">Create input and output **datasets**.</span><span class="sxs-lookup"><span data-stu-id="192da-134">Create input and output **datasets**.</span></span> <span data-ttu-id="192da-135">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span><span class="sxs-lookup"><span data-stu-id="192da-135">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span></span>

    <span data-ttu-id="192da-136">In this tutorial, the input and output datasets specify locations of input and output data in the Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="192da-136">In this tutorial, the input and output datasets specify locations of input and output data in the Azure Blob Storage.</span></span> <span data-ttu-id="192da-137">The Azure Storage linked service specifies what Azure Storage Account is used.</span><span class="sxs-lookup"><span data-stu-id="192da-137">The Azure Storage linked service specifies what Azure Storage Account is used.</span></span> <span data-ttu-id="192da-138">An input dataset specifies where the input files are located and an output dataset specifies where the output files are placed.</span><span class="sxs-lookup"><span data-stu-id="192da-138">An input dataset specifies where the input files are located and an output dataset specifies where the output files are placed.</span></span> 


<span data-ttu-id="192da-139">See [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="192da-139">See [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of Azure Data Factory.</span></span>
  
<span data-ttu-id="192da-140">Here is the **diagram view** of the sample data factory you build in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="192da-140">Here is the **diagram view** of the sample data factory you build in this tutorial.</span></span> <span data-ttu-id="192da-141">**MyFirstPipeline** has one activity of type Hive that consumes **AzureBlobInput** dataset as an input and produces **AzureBlobOutput** dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="192da-141">**MyFirstPipeline** has one activity of type Hive that consumes **AzureBlobInput** dataset as an input and produces **AzureBlobOutput** dataset as an output.</span></span> 

![Diagram view in Data Factory tutorial](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


<span data-ttu-id="192da-143">In this tutorial, **inputdata** folder of the **adfgetstarted** Azure blob container contains one file named input.log.</span><span class="sxs-lookup"><span data-stu-id="192da-143">In this tutorial, **inputdata** folder of the **adfgetstarted** Azure blob container contains one file named input.log.</span></span> <span data-ttu-id="192da-144">This log file has entries from three months: January, February, and March of 2016.</span><span class="sxs-lookup"><span data-stu-id="192da-144">This log file has entries from three months: January, February, and March of 2016.</span></span> <span data-ttu-id="192da-145">Here are the sample rows for each month in the input file.</span><span class="sxs-lookup"><span data-stu-id="192da-145">Here are the sample rows for each month in the input file.</span></span> 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="192da-146">When the file is processed by the pipeline with HDInsight Hive Activity, the activity runs a Hive script on the HDInsight cluster that partitions input data by year and month.</span><span class="sxs-lookup"><span data-stu-id="192da-146">When the file is processed by the pipeline with HDInsight Hive Activity, the activity runs a Hive script on the HDInsight cluster that partitions input data by year and month.</span></span> <span data-ttu-id="192da-147">The script creates three output folders that contain a file with entries from each month.</span><span class="sxs-lookup"><span data-stu-id="192da-147">The script creates three output folders that contain a file with entries from each month.</span></span>  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

<span data-ttu-id="192da-148">From the sample lines shown above, the first one (with 2016-01-01) is written to the 000000_0 file in the month=1 folder.</span><span class="sxs-lookup"><span data-stu-id="192da-148">From the sample lines shown above, the first one (with 2016-01-01) is written to the 000000_0 file in the month=1 folder.</span></span> <span data-ttu-id="192da-149">Similarly, the second one is written to the file in the month=2 folder and the third one is written to the file in the month=3 folder.</span><span class="sxs-lookup"><span data-stu-id="192da-149">Similarly, the second one is written to the file in the month=2 folder and the third one is written to the file in the month=3 folder.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="192da-150">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="192da-150">Prerequisites</span></span>
<span data-ttu-id="192da-151">Before you begin this tutorial, you must have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="192da-151">Before you begin this tutorial, you must have the following prerequisites:</span></span>

1. <span data-ttu-id="192da-152">**Azure subscription** - If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="192da-152">**Azure subscription** - If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="192da-153">See the [Free Trial](https://azure.microsoft.com/pricing/free-trial/) article on how you can obtain a free trial account.</span><span class="sxs-lookup"><span data-stu-id="192da-153">See the [Free Trial](https://azure.microsoft.com/pricing/free-trial/) article on how you can obtain a free trial account.</span></span>
2. <span data-ttu-id="192da-154">**Azure Storage** – You use an Azure storage account for storing the data in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="192da-154">**Azure Storage** – You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="192da-155">If you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article.</span><span class="sxs-lookup"><span data-stu-id="192da-155">If you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article.</span></span> <span data-ttu-id="192da-156">After you have created the storage account, note down the **account name** and **access key**.</span><span class="sxs-lookup"><span data-stu-id="192da-156">After you have created the storage account, note down the **account name** and **access key**.</span></span> <span data-ttu-id="192da-157">See [View, copy and regenerate storage access keys](../../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="192da-157">See [View, copy and regenerate storage access keys](../../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>
3. <span data-ttu-id="192da-158">Download and review the Hive query file (**HQL**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql).</span><span class="sxs-lookup"><span data-stu-id="192da-158">Download and review the Hive query file (**HQL**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql).</span></span> <span data-ttu-id="192da-159">This query transforms input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="192da-159">This query transforms input data to produce output data.</span></span> 
4. <span data-ttu-id="192da-160">Download and review the sample input file (**input.log**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span><span class="sxs-lookup"><span data-stu-id="192da-160">Download and review the sample input file (**input.log**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span></span>
5. <span data-ttu-id="192da-161">Create a blob container named **adfgetstarted** in your Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="192da-161">Create a blob container named **adfgetstarted** in your Azure Blob Storage.</span></span> 
6. <span data-ttu-id="192da-162">Upload **partitionweblogs.hql** file to the **script** folder in the **adfgetstarted** container.</span><span class="sxs-lookup"><span data-stu-id="192da-162">Upload **partitionweblogs.hql** file to the **script** folder in the **adfgetstarted** container.</span></span> <span data-ttu-id="192da-163">Use tools such as [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="192da-163">Use tools such as [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 
7. <span data-ttu-id="192da-164">Upload **input.log** file to the **inputdata** folder in the **adfgetstarted** container.</span><span class="sxs-lookup"><span data-stu-id="192da-164">Upload **input.log** file to the **inputdata** folder in the **adfgetstarted** container.</span></span> 

<span data-ttu-id="192da-165">After you complete the prerequisites, select one of the following tools/SDKs to do the tutorial:</span><span class="sxs-lookup"><span data-stu-id="192da-165">After you complete the prerequisites, select one of the following tools/SDKs to do the tutorial:</span></span> 

- [<span data-ttu-id="192da-166">Azure portal</span><span class="sxs-lookup"><span data-stu-id="192da-166">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
- [<span data-ttu-id="192da-167">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="192da-167">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
- [<span data-ttu-id="192da-168">PowerShell</span><span class="sxs-lookup"><span data-stu-id="192da-168">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
- [<span data-ttu-id="192da-169">Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="192da-169">Resource Manager template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
- [<span data-ttu-id="192da-170">REST API</span><span class="sxs-lookup"><span data-stu-id="192da-170">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="192da-171">Azure portal and Visual Studio provide GUI way of building your data factories.</span><span class="sxs-lookup"><span data-stu-id="192da-171">Azure portal and Visual Studio provide GUI way of building your data factories.</span></span> <span data-ttu-id="192da-172">Whereas, PowerShell, Resource Manager Template, and REST API options provides scripting/programming way of building your data factories.</span><span class="sxs-lookup"><span data-stu-id="192da-172">Whereas, PowerShell, Resource Manager Template, and REST API options provides scripting/programming way of building your data factories.</span></span>

> [!NOTE]
> The data pipeline in this tutorial transforms input data to produce output data. It does not copy data from a source data store to a destination data store. For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 





  
