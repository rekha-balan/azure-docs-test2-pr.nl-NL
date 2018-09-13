---
title: Use custom activities in an Azure Data Factory pipeline
description: Learn how to create custom activities and use them in an Azure Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: spelluru
ms.openlocfilehash: 1175d19375d699f6a8ef6d3aae9be82483fffb46
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540803"
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="9c69c-103">Use custom activities in an Azure Data Factory pipeline</span><span class="sxs-lookup"><span data-stu-id="9c69c-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive Activity](data-factory-hive-activity.md) 
> * [Pig Activity](data-factory-pig-activity.md)
> * [MapReduce Activity](data-factory-map-reduce.md)
> * [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md)
> * [Spark Activity](data-factory-spark.md)
> * [Machine Learning Batch Execution Activity](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Update Resource Activity](data-factory-azure-ml-update-resource-activity.md)
> * [Stored Procedure Activity](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md)
> * [.NET Custom Activity](data-factory-use-custom-activities.md)


<span data-ttu-id="9c69c-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="9c69c-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="9c69c-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9c69c-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="9c69c-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9c69c-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="9c69c-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="9c69c-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span></span> <span data-ttu-id="9c69c-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="9c69c-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span></span> 

<span data-ttu-id="9c69c-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or an **Azure HDInsight** cluster.</span><span class="sxs-lookup"><span data-stu-id="9c69c-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or an **Azure HDInsight** cluster.</span></span> <span data-ttu-id="9c69c-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="9c69c-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span><span class="sxs-lookup"><span data-stu-id="9c69c-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="9c69c-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="9c69c-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span></span> <span data-ttu-id="9c69c-123">The walkthrough uses an **Azure Batch** linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-123">The walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="9c69c-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span><span class="sxs-lookup"><span data-stu-id="9c69c-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="9c69c-125">Then, configure custom activity to use the HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-125">Then, configure custom activity to use the HDInsight linked service.</span></span> <span data-ttu-id="9c69c-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span></span>

> [!NOTE]
> It is not possible to use a Data Management Gateway from a custom activity to access on-premises data sources. Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only the copy activity and stored procedure activity in Data Factory.   

## <a name="walkthrough"></a><span data-ttu-id="9c69c-129">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="9c69c-129">Walkthrough</span></span>
### <a name="prerequisites"></a><span data-ttu-id="9c69c-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c69c-130">Prerequisites</span></span>
* <span data-ttu-id="9c69c-131">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="9c69c-131">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="9c69c-132">Download and install [Azure .NET SDK][azure-developer-center]</span><span class="sxs-lookup"><span data-stu-id="9c69c-132">Download and install [Azure .NET SDK][azure-developer-center]</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="9c69c-133">Azure Batch prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c69c-133">Azure Batch prerequisites</span></span>
<span data-ttu-id="9c69c-134">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span><span class="sxs-lookup"><span data-stu-id="9c69c-134">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="9c69c-135">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span><span class="sxs-lookup"><span data-stu-id="9c69c-135">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="9c69c-136">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-136">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span></span> <span data-ttu-id="9c69c-137">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-137">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span></span>

<span data-ttu-id="9c69c-138">For the tutorial, create an Azure Batch account with a pool of VMs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-138">For the tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="9c69c-139">Here are the steps:</span><span class="sxs-lookup"><span data-stu-id="9c69c-139">Here are the steps:</span></span>

1. <span data-ttu-id="9c69c-140">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c69c-140">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="9c69c-141">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span><span class="sxs-lookup"><span data-stu-id="9c69c-141">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="9c69c-142">Note down the Azure Batch account name, account key, URI, and pool name.</span><span class="sxs-lookup"><span data-stu-id="9c69c-142">Note down the Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="9c69c-143">You need them to create an Azure Batch linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-143">You need them to create an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="9c69c-144">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="9c69c-144">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="9c69c-145">In this example, **myaccount** is the name of the Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="9c69c-145">In this example, **myaccount** is the name of the Azure Batch account.</span></span> <span data-ttu-id="9c69c-146">URI you use in the linked service definition is the URL without the name of the account.</span><span class="sxs-lookup"><span data-stu-id="9c69c-146">URI you use in the linked service definition is the URL without the name of the account.</span></span> <span data-ttu-id="9c69c-147">For example: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="9c69c-147">For example: `https://westus.batch.azure.com`.</span></span>
    2. <span data-ttu-id="9c69c-148">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-148">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="9c69c-149">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-149">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span></span> <span data-ttu-id="9c69c-150">If you don't have an existing pool, move to the next step.</span><span class="sxs-lookup"><span data-stu-id="9c69c-150">If you don't have an existing pool, move to the next step.</span></span>     
2. <span data-ttu-id="9c69c-151">Create an **Azure Batch pool**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-151">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="9c69c-152">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-152">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="9c69c-153">Select your Azure Batch account to open the **Batch Account** blade.</span><span class="sxs-lookup"><span data-stu-id="9c69c-153">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
   3. <span data-ttu-id="9c69c-154">Click **Pools** tile.</span><span class="sxs-lookup"><span data-stu-id="9c69c-154">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="9c69c-155">In the **Pools** blade, click Add button on the toolbar to add a pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-155">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
      1. <span data-ttu-id="9c69c-156">Enter an ID for the pool (Pool ID).</span><span class="sxs-lookup"><span data-stu-id="9c69c-156">Enter an ID for the pool (Pool ID).</span></span> <span data-ttu-id="9c69c-157">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span><span class="sxs-lookup"><span data-stu-id="9c69c-157">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
      2. <span data-ttu-id="9c69c-158">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span><span class="sxs-lookup"><span data-stu-id="9c69c-158">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
      3. <span data-ttu-id="9c69c-159">Select a **node pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-159">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="9c69c-160">Enter **2** as value for the **Target Dedicated** setting.</span><span class="sxs-lookup"><span data-stu-id="9c69c-160">Enter **2** as value for the **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="9c69c-161">Enter **2** as value for the **Max tasks per node** setting.</span><span class="sxs-lookup"><span data-stu-id="9c69c-161">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="9c69c-162">Click **OK** to create the pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-162">Click **OK** to create the pool.</span></span>
   6. <span data-ttu-id="9c69c-163">Note down the **ID** of the pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-163">Note down the **ID** of the pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="9c69c-164">High-level steps</span><span class="sxs-lookup"><span data-stu-id="9c69c-164">High-level steps</span></span>
<span data-ttu-id="9c69c-165">Here are the two high-level steps you perform as part of this walkthrough:</span><span class="sxs-lookup"><span data-stu-id="9c69c-165">Here are the two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="9c69c-166">Create a custom activity that contains simple data transformation/processing logic.</span><span class="sxs-lookup"><span data-stu-id="9c69c-166">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="9c69c-167">Create an Azure data factory with a pipeline that uses the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-167">Create an Azure data factory with a pipeline that uses the custom activity.</span></span>

## <a name="create-a-custom-activity"></a><span data-ttu-id="9c69c-168">Create a custom activity</span><span class="sxs-lookup"><span data-stu-id="9c69c-168">Create a custom activity</span></span>
<span data-ttu-id="9c69c-169">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="9c69c-169">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="9c69c-170">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span><span class="sxs-lookup"><span data-stu-id="9c69c-170">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="9c69c-171">The method takes four parameters:</span><span class="sxs-lookup"><span data-stu-id="9c69c-171">The method takes four parameters:</span></span>

- <span data-ttu-id="9c69c-172">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-172">**linkedServices**.</span></span> <span data-ttu-id="9c69c-173">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-173">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span></span>   
- <span data-ttu-id="9c69c-174">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-174">**datasets**.</span></span> <span data-ttu-id="9c69c-175">This property is an enumerable list of input/output datasets for the activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-175">This property is an enumerable list of input/output datasets for the activity.</span></span> <span data-ttu-id="9c69c-176">You can use this parameter to get the locations and schemas defined by input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="9c69c-176">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="9c69c-177">**activity**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-177">**activity**.</span></span> <span data-ttu-id="9c69c-178">This property represents the current activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-178">This property represents the current activity.</span></span> <span data-ttu-id="9c69c-179">It can be used to access extended properties associated with the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-179">It can be used to access extended properties associated with the custom activity.</span></span> <span data-ttu-id="9c69c-180">See [Access extended properties](#access-extended-properties) for details.</span><span class="sxs-lookup"><span data-stu-id="9c69c-180">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="9c69c-181">**logger**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-181">**logger**.</span></span> <span data-ttu-id="9c69c-182">This object lets you write debug comments that surface in the user log for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="9c69c-182">This object lets you write debug comments that surface in the user log for the pipeline.</span></span>

<span data-ttu-id="9c69c-183">The method returns a dictionary that can be used to chain custom activities together in the future.</span><span class="sxs-lookup"><span data-stu-id="9c69c-183">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="9c69c-184">This feature is not implemented yet, so return an empty dictionary from the method.</span><span class="sxs-lookup"><span data-stu-id="9c69c-184">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="9c69c-185">Procedure</span><span class="sxs-lookup"><span data-stu-id="9c69c-185">Procedure</span></span>
1. <span data-ttu-id="9c69c-186">Create a **.NET Class Library** project.</span><span class="sxs-lookup"><span data-stu-id="9c69c-186">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="9c69c-187">Launch <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="9c69c-187">Launch <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="9c69c-188">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span><span class="sxs-lookup"><span data-stu-id="9c69c-188">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="9c69c-189">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="9c69c-189">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="9c69c-190">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-190">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span></span></li>
     <li><span data-ttu-id="9c69c-191">Select <b>Class Library</b> from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="9c69c-191">Select <b>Class Library</b> from the list of project types on the right.</span></span></li>
     <li><span data-ttu-id="9c69c-192">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span><span class="sxs-lookup"><span data-stu-id="9c69c-192">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="9c69c-193">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span><span class="sxs-lookup"><span data-stu-id="9c69c-193">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="9c69c-194">Click <b>OK</b> to create the project.</span><span class="sxs-lookup"><span data-stu-id="9c69c-194">Click <b>OK</b> to create the project.</span></span></li>
   </ol><span data-ttu-id="9c69c-195">
2. Click \*\*Tools\*\*, point to \*\*NuGet Package Manager\*\*, and click \*\*Package Manager Console\**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-195">
2. Click \*\*Tools\*\*, point to \*\*NuGet Package Manager\*\*, and click \*\*Package Manager Console\**.</span></span>
<span data-ttu-id="9c69c-196">3.</span><span class="sxs-lookup"><span data-stu-id="9c69c-196">3.</span></span> <span data-ttu-id="9c69c-197">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-197">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="9c69c-198">Import the **Azure Storage** NuGet package in to the project.</span><span class="sxs-lookup"><span data-stu-id="9c69c-198">Import the **Azure Storage** NuGet package in to the project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage. If you add a reference to a later version of Azure Storage assembly in your custom activity project, you see an error when the activity executes. To resolve the error, see [Appdomain isolation](#appdomain-isolation) section. 
5. <span data-ttu-id="9c69c-202">Add the following **using** statements to the source file in the project.</span><span class="sxs-lookup"><span data-stu-id="9c69c-202">Add the following **using** statements to the source file in the project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="9c69c-203">Change the name of the **namespace** to **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-203">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="9c69c-204">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="9c69c-204">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="9c69c-205">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span><span class="sxs-lookup"><span data-stu-id="9c69c-205">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span>

    <span data-ttu-id="9c69c-206">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-206">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // to log information, use the logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass the connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize the continuation token before using it in the do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get the list of input blobs from the input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns the number of occurrences of
            // the search term (“Microsoft”) in each blob associated
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload the output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} to the output blob", output);
        outputBlob.UploadText(output);
    
        // The dictionary can be used to chain custom activities together in the future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="9c69c-207">Add the following helper methods:</span><span class="sxs-lookup"><span data-stu-id="9c69c-207">Add the following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="9c69c-208">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span><span class="sxs-lookup"><span data-stu-id="9c69c-208">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span> <span data-ttu-id="9c69c-209">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span><span class="sxs-lookup"><span data-stu-id="9c69c-209">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="9c69c-210">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span><span class="sxs-lookup"><span data-stu-id="9c69c-210">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="9c69c-211">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span><span class="sxs-lookup"><span data-stu-id="9c69c-211">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span></span> <span data-ttu-id="9c69c-212">The search term (“Microsoft”) is hard-coded in the code.</span><span class="sxs-lookup"><span data-stu-id="9c69c-212">The search term (“Microsoft”) is hard-coded in the code.</span></span>
10. <span data-ttu-id="9c69c-213">Compile the project.</span><span class="sxs-lookup"><span data-stu-id="9c69c-213">Compile the project.</span></span> <span data-ttu-id="9c69c-214">Click **Build** from the menu and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-214">Click **Build** from the menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > Set 4.5.2 version of .NET Framework as the target framework for your project: right-click the project, and click **Properties** to set the target framework. Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.

11. <span data-ttu-id="9c69c-217">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span><span class="sxs-lookup"><span data-stu-id="9c69c-217">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span></span>
12. <span data-ttu-id="9c69c-218">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span><span class="sxs-lookup"><span data-stu-id="9c69c-218">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="9c69c-219">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span><span class="sxs-lookup"><span data-stu-id="9c69c-219">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > All the files in the zip file for the custom activity must be at the **top level** with no sub folders.

    ![Binary output files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="9c69c-222">Create a blob container named **customactivitycontainer** if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="9c69c-222">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span>
15. <span data-ttu-id="9c69c-223">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hold/cool Blob storage) that is referred by AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="9c69c-223">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hold/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!NOTE]
> If you add this .NET activity project to a solution in Visual Studio that contains a Data Factory project, and add a reference to .NET activity project from the Data Factory application project, you do not need to perform the last two steps of manually creating the zip file and uploading it to the general-purpose Azure blob storage. When you publish Data Factory entities using Visual Studio, these steps are automatically done by the publishing process. See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob to Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles to learn about creating and publishing Data Factory entities using Visual Studio.  


## <a name="create-a-data-factory"></a><span data-ttu-id="9c69c-227">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="9c69c-227">Create a data factory</span></span> 
<span data-ttu-id="9c69c-228">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="9c69c-228">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="9c69c-229">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-229">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="9c69c-230">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="9c69c-230">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span></span> <span data-ttu-id="9c69c-231">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="9c69c-231">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span></span>

<span data-ttu-id="9c69c-232">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="9c69c-232">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span></span> <span data-ttu-id="9c69c-233">Create the adftutorial container if it does not exist already.</span><span class="sxs-lookup"><span data-stu-id="9c69c-233">Create the adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="9c69c-234">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span><span class="sxs-lookup"><span data-stu-id="9c69c-234">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span></span> <span data-ttu-id="9c69c-235">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-235">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="9c69c-236">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span><span class="sxs-lookup"><span data-stu-id="9c69c-236">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="9c69c-237">Here are the steps you perform in this section:</span><span class="sxs-lookup"><span data-stu-id="9c69c-237">Here are the steps you perform in this section:</span></span>

1. <span data-ttu-id="9c69c-238">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-238">Create a **data factory**.</span></span>
2. <span data-ttu-id="9c69c-239">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-239">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span></span>
3. <span data-ttu-id="9c69c-240">Create input and output **datasets** that represent input and output of the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-240">Create input and output **datasets** that represent input and output of the custom activity.</span></span>
4. <span data-ttu-id="9c69c-241">Create a **pipeline** that uses the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-241">Create a **pipeline** that uses the custom activity.</span></span>

> [!NOTE]
> Create the **file.txt** and upload it to a blob container if you haven't already done so. See instructions in the preceding section.   

### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="9c69c-244">Step 1: Create the data factory</span><span class="sxs-lookup"><span data-stu-id="9c69c-244">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="9c69c-245">After logging in to the Azure portal, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="9c69c-245">After logging in to the Azure portal, do the following steps:</span></span>
   1. <span data-ttu-id="9c69c-246">Click **NEW** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="9c69c-246">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="9c69c-247">Click **Data + Analytics** in the **New** blade.</span><span class="sxs-lookup"><span data-stu-id="9c69c-247">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="9c69c-248">Click **Data Factory** on the **Data analytics** blade.</span><span class="sxs-lookup"><span data-stu-id="9c69c-248">Click **Data Factory** on the **Data analytics** blade.</span></span>
   
    ![New Azure Data Factory menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="9c69c-250">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span><span class="sxs-lookup"><span data-stu-id="9c69c-250">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="9c69c-251">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="9c69c-251">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="9c69c-252">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="9c69c-252">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![New Azure Data Factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="9c69c-254">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="9c69c-254">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="9c69c-255">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="9c69c-255">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="9c69c-256">Click **Create** on the **New data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="9c69c-256">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="9c69c-257">You see the data factory being created in the **Dashboard** of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9c69c-257">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="9c69c-258">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="9c69c-258">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span></span>
    
    ![Data Factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="9c69c-260">Step 2: Create linked services</span><span class="sxs-lookup"><span data-stu-id="9c69c-260">Step 2: Create linked services</span></span>
<span data-ttu-id="9c69c-261">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="9c69c-261">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="9c69c-262">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="9c69c-262">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="9c69c-263">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="9c69c-263">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="9c69c-264">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-264">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="9c69c-265">You see the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="9c69c-265">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="9c69c-266">Click **New data store** on the command bar and choose **Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-266">Click **New data store** on the command bar and choose **Azure storage**.</span></span> <span data-ttu-id="9c69c-267">You should see the JSON script for creating an Azure Storage linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="9c69c-267">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>
    
    ![New data store - Azure Storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="9c69c-269">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="9c69c-269">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span></span> <span data-ttu-id="9c69c-270">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9c69c-270">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Azure Storage liked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="9c69c-272">Click **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-272">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="9c69c-273">Create Azure Batch linked service</span><span class="sxs-lookup"><span data-stu-id="9c69c-273">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="9c69c-274">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span><span class="sxs-lookup"><span data-stu-id="9c69c-274">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span></span>

    ![New compute - Azure Batch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="9c69c-276">Make the following changes to the JSON script:</span><span class="sxs-lookup"><span data-stu-id="9c69c-276">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="9c69c-277">Specify Azure Batch account name for the **accountName** property.</span><span class="sxs-lookup"><span data-stu-id="9c69c-277">Specify Azure Batch account name for the **accountName** property.</span></span> <span data-ttu-id="9c69c-278">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="9c69c-278">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="9c69c-279">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span><span class="sxs-lookup"><span data-stu-id="9c69c-279">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span></span>
   2. <span data-ttu-id="9c69c-280">Specify the Azure Batch account key for the **accessKey** property.</span><span class="sxs-lookup"><span data-stu-id="9c69c-280">Specify the Azure Batch account key for the **accessKey** property.</span></span>
   3. <span data-ttu-id="9c69c-281">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span><span class="sxs-lookup"><span data-stu-id="9c69c-281">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span></span> <span data-ttu-id="9c69c-282">You can also specify the ID of the pool instead of the name of the pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-282">You can also specify the ID of the pool instead of the name of the pool.</span></span>
   4. <span data-ttu-id="9c69c-283">Specify Azure Batch URI for the **batchUri** property.</span><span class="sxs-lookup"><span data-stu-id="9c69c-283">Specify Azure Batch URI for the **batchUri** property.</span></span> <span data-ttu-id="9c69c-284">Example: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="9c69c-284">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="9c69c-285">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="9c69c-285">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="9c69c-286">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-286">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!IMPORTANT]
      > The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight. You can only use your own Azure Batch pool in an Azure data factory.   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="9c69c-289">Step 3: Create datasets</span><span class="sxs-lookup"><span data-stu-id="9c69c-289">Step 3: Create datasets</span></span>
<span data-ttu-id="9c69c-290">In this step, you create datasets to represent input and output data.</span><span class="sxs-lookup"><span data-stu-id="9c69c-290">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="9c69c-291">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="9c69c-291">Create input dataset</span></span>
1. <span data-ttu-id="9c69c-292">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="9c69c-292">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="9c69c-293">Replace the JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="9c69c-293">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="9c69c-294">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="9c69c-294">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="9c69c-295">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span><span class="sxs-lookup"><span data-stu-id="9c69c-295">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="9c69c-296">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span><span class="sxs-lookup"><span data-stu-id="9c69c-296">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span> <span data-ttu-id="9c69c-297">In this sample, it is the same file (file.txt) in the intputfolder.</span><span class="sxs-lookup"><span data-stu-id="9c69c-297">In this sample, it is the same file (file.txt) in the intputfolder.</span></span>

   <span data-ttu-id="9c69c-298">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="9c69c-298">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span></span>
3. <span data-ttu-id="9c69c-299">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-299">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span></span> <span data-ttu-id="9c69c-300">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span><span class="sxs-lookup"><span data-stu-id="9c69c-300">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="9c69c-301">Create an output dataset</span><span class="sxs-lookup"><span data-stu-id="9c69c-301">Create an output dataset</span></span>
1. <span data-ttu-id="9c69c-302">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-302">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="9c69c-303">Replace the JSON script in the right pane with the following JSON script:</span><span class="sxs-lookup"><span data-stu-id="9c69c-303">Replace the JSON script in the right pane with the following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="9c69c-304">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span><span class="sxs-lookup"><span data-stu-id="9c69c-304">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span></span> <span data-ttu-id="9c69c-305">See [Developer Reference][adf-developer-reference] for details.</span><span class="sxs-lookup"><span data-stu-id="9c69c-305">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="9c69c-306">An output blob/file is generated for each input slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-306">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="9c69c-307">Here is how an output file is named for each slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-307">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="9c69c-308">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-308">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="9c69c-309">Slice</span><span class="sxs-lookup"><span data-stu-id="9c69c-309">Slice</span></span> | <span data-ttu-id="9c69c-310">Start time</span><span class="sxs-lookup"><span data-stu-id="9c69c-310">Start time</span></span> | <span data-ttu-id="9c69c-311">Output file</span><span class="sxs-lookup"><span data-stu-id="9c69c-311">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="9c69c-312">1</span><span class="sxs-lookup"><span data-stu-id="9c69c-312">1</span></span> |<span data-ttu-id="9c69c-313">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="9c69c-313">2016-11-16T00:00:00</span></span> |<span data-ttu-id="9c69c-314">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="9c69c-314">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="9c69c-315">2</span><span class="sxs-lookup"><span data-stu-id="9c69c-315">2</span></span> |<span data-ttu-id="9c69c-316">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="9c69c-316">2016-11-16T01:00:00</span></span> |<span data-ttu-id="9c69c-317">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="9c69c-317">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="9c69c-318">3</span><span class="sxs-lookup"><span data-stu-id="9c69c-318">3</span></span> |<span data-ttu-id="9c69c-319">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="9c69c-319">2016-11-16T02:00:00</span></span> |<span data-ttu-id="9c69c-320">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="9c69c-320">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="9c69c-321">4</span><span class="sxs-lookup"><span data-stu-id="9c69c-321">4</span></span> |<span data-ttu-id="9c69c-322">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="9c69c-322">2016-11-16T03:00:00</span></span> |<span data-ttu-id="9c69c-323">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="9c69c-323">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="9c69c-324">5</span><span class="sxs-lookup"><span data-stu-id="9c69c-324">5</span></span> |<span data-ttu-id="9c69c-325">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="9c69c-325">2016-11-16T04:00:00</span></span> |<span data-ttu-id="9c69c-326">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="9c69c-326">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="9c69c-327">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span><span class="sxs-lookup"><span data-stu-id="9c69c-327">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span></span> <span data-ttu-id="9c69c-328">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span><span class="sxs-lookup"><span data-stu-id="9c69c-328">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="9c69c-329">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span><span class="sxs-lookup"><span data-stu-id="9c69c-329">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="9c69c-330">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="9c69c-330">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a><span data-ttu-id="9c69c-331">Create and run a pipeline that uses the custom activity</span><span class="sxs-lookup"><span data-stu-id="9c69c-331">Create and run a pipeline that uses the custom activity</span></span>
1. <span data-ttu-id="9c69c-332">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="9c69c-332">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span></span> 
2. <span data-ttu-id="9c69c-333">Replace the JSON in the right pane with the following JSON script:</span><span class="sxs-lookup"><span data-stu-id="9c69c-333">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="9c69c-334">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="9c69c-334">Note the following points:</span></span>

   * <span data-ttu-id="9c69c-335">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-335">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span></span>
   * <span data-ttu-id="9c69c-336">There is one activity in the activities section and it is of type: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-336">There is one activity in the activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="9c69c-337">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-337">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="9c69c-338">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-338">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="9c69c-339">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span><span class="sxs-lookup"><span data-stu-id="9c69c-339">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="9c69c-340">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-340">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="9c69c-341">This article assumes that you are using the same Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="9c69c-341">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="9c69c-342">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-342">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="9c69c-343">It is in the format: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="9c69c-343">It is in the format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="9c69c-344">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span><span class="sxs-lookup"><span data-stu-id="9c69c-344">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="9c69c-345">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-345">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span></span>
   * <span data-ttu-id="9c69c-346">**isPaused** property is set to **false** by default.</span><span class="sxs-lookup"><span data-stu-id="9c69c-346">**isPaused** property is set to **false** by default.</span></span> <span data-ttu-id="9c69c-347">The pipeline runs immediately in this example because the slices start in the past.</span><span class="sxs-lookup"><span data-stu-id="9c69c-347">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="9c69c-348">You can set this property to true to pause the pipeline and set it back to false to restart.</span><span class="sxs-lookup"><span data-stu-id="9c69c-348">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>
   * <span data-ttu-id="9c69c-349">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="9c69c-349">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>
3. <span data-ttu-id="9c69c-350">To deploy the pipeline, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="9c69c-350">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-the-pipeline"></a><span data-ttu-id="9c69c-351">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="9c69c-351">Monitor the pipeline</span></span>
1. <span data-ttu-id="9c69c-352">In the Data Factory blade in the Azure portal, click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-352">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

    ![Diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="9c69c-354">In the Diagram View, now click the OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="9c69c-354">In the Diagram View, now click the OutputDataset.</span></span>

    ![Diagram view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="9c69c-356">You should see that the five output slices are in the Ready state.</span><span class="sxs-lookup"><span data-stu-id="9c69c-356">You should see that the five output slices are in the Ready state.</span></span> <span data-ttu-id="9c69c-357">If they are not in the Ready state, they haven't been produced yet.</span><span class="sxs-lookup"><span data-stu-id="9c69c-357">If they are not in the Ready state, they haven't been produced yet.</span></span> 

   ![Output slices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="9c69c-359">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="9c69c-359">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span></span>

   ![output from custom activity][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="9c69c-361">If you open the output file, you should see the output similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="9c69c-361">If you open the output file, you should see the output similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="9c69c-362">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span><span class="sxs-lookup"><span data-stu-id="9c69c-362">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="9c69c-363">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9c69c-363">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span></span>

   ![download logs from custom activity][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="9c69c-365">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span><span class="sxs-lookup"><span data-stu-id="9c69c-365">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="9c69c-366">Data Factory and Batch integration</span><span class="sxs-lookup"><span data-stu-id="9c69c-366">Data Factory and Batch integration</span></span>
<span data-ttu-id="9c69c-367">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-367">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="9c69c-368">Click **Jobs** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="9c69c-368">Click **Jobs** from the left menu.</span></span> 

![Azure Data Factory - Batch jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="9c69c-370">A task is created for each activity run of a slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-370">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="9c69c-371">If there are five slices ready to be processed, five tasks are created in this job.</span><span class="sxs-lookup"><span data-stu-id="9c69c-371">If there are five slices ready to be processed, five tasks are created in this job.</span></span> <span data-ttu-id="9c69c-372">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span><span class="sxs-lookup"><span data-stu-id="9c69c-372">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="9c69c-373">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span><span class="sxs-lookup"><span data-stu-id="9c69c-373">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span></span>

![Azure Data Factory - Batch job tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="9c69c-375">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span><span class="sxs-lookup"><span data-stu-id="9c69c-375">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory & Batch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="9c69c-377">Troubleshoot failures</span><span class="sxs-lookup"><span data-stu-id="9c69c-377">Troubleshoot failures</span></span>
<span data-ttu-id="9c69c-378">Troubleshooting consists of a few basic techniques:</span><span class="sxs-lookup"><span data-stu-id="9c69c-378">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="9c69c-379">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="9c69c-379">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="9c69c-380">Upload the zip file to a **general-purpose Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-380">Upload the zip file to a **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="9c69c-381">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="9c69c-381">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span></span> <span data-ttu-id="9c69c-382">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-382">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="9c69c-383">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span><span class="sxs-lookup"><span data-stu-id="9c69c-383">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span></span> <span data-ttu-id="9c69c-384">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span><span class="sxs-lookup"><span data-stu-id="9c69c-384">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="9c69c-385">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span><span class="sxs-lookup"><span data-stu-id="9c69c-385">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span></span>
3. <span data-ttu-id="9c69c-386">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span><span class="sxs-lookup"><span data-stu-id="9c69c-386">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="9c69c-387">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span><span class="sxs-lookup"><span data-stu-id="9c69c-387">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="9c69c-388">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-388">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="9c69c-389">You see **activity runs** for that slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-389">You see **activity runs** for that slice.</span></span> <span data-ttu-id="9c69c-390">You should see one activity run for the slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-390">You should see one activity run for the slice.</span></span> <span data-ttu-id="9c69c-391">If you click Run in the command bar, you can start another activity run for the same slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-391">If you click Run in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="9c69c-392">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span><span class="sxs-lookup"><span data-stu-id="9c69c-392">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="9c69c-393">You see logged messages in the user_0.log file.</span><span class="sxs-lookup"><span data-stu-id="9c69c-393">You see logged messages in the user_0.log file.</span></span> <span data-ttu-id="9c69c-394">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span><span class="sxs-lookup"><span data-stu-id="9c69c-394">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="9c69c-395">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span><span class="sxs-lookup"><span data-stu-id="9c69c-395">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   <span data-ttu-id="9c69c-396">In the list of log files, click the **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-396">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="9c69c-397">In the right panel are the results of using the **IActivityLogger.Write** method.</span><span class="sxs-lookup"><span data-stu-id="9c69c-397">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span> <span data-ttu-id="9c69c-398">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span><span class="sxs-lookup"><span data-stu-id="9c69c-398">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span></span>

   <span data-ttu-id="9c69c-399">In addition, check **system-0.log** for any system error messages and exceptions.</span><span class="sxs-lookup"><span data-stu-id="9c69c-399">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="9c69c-400">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-400">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="9c69c-401">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span><span class="sxs-lookup"><span data-stu-id="9c69c-401">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>
6. <span data-ttu-id="9c69c-402">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span><span class="sxs-lookup"><span data-stu-id="9c69c-402">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span></span>
7. <span data-ttu-id="9c69c-403">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-403">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="9c69c-404">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="9c69c-404">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="9c69c-405">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="9c69c-405">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="9c69c-406">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span><span class="sxs-lookup"><span data-stu-id="9c69c-406">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="9c69c-407">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="9c69c-407">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="9c69c-408">Then, run the following command from NuGet Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="9c69c-408">Then, run the following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="9c69c-409">Build the project.</span><span class="sxs-lookup"><span data-stu-id="9c69c-409">Build the project.</span></span> <span data-ttu-id="9c69c-410">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span><span class="sxs-lookup"><span data-stu-id="9c69c-410">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span></span> <span data-ttu-id="9c69c-411">Create a zip file with binaries and the PDB file.</span><span class="sxs-lookup"><span data-stu-id="9c69c-411">Create a zip file with binaries and the PDB file.</span></span> <span data-ttu-id="9c69c-412">Replace the old zip file with this one in the blob container (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="9c69c-412">Replace the old zip file with this one in the blob container (customactivitycontainer).</span></span> <span data-ttu-id="9c69c-413">Rerun the slices that failed (right-click slice, and click Run).</span><span class="sxs-lookup"><span data-stu-id="9c69c-413">Rerun the slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="9c69c-414">The custom activity does not use the **app.config** file from your package.</span><span class="sxs-lookup"><span data-stu-id="9c69c-414">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="9c69c-415">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span><span class="sxs-lookup"><span data-stu-id="9c69c-415">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="9c69c-416">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="9c69c-416">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="9c69c-417">The .NET custom activity then can access secrets from the KeyVault at runtime.</span><span class="sxs-lookup"><span data-stu-id="9c69c-417">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="9c69c-418">This solution is a generic solution and can scale to any type of secret, not just connection string.</span><span class="sxs-lookup"><span data-stu-id="9c69c-418">This solution is a generic solution and can scale to any type of secret, not just connection string.</span></span>

   <span data-ttu-id="9c69c-419">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-419">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="9c69c-420">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span><span class="sxs-lookup"><span data-stu-id="9c69c-420">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="9c69c-421">Update custom activity</span><span class="sxs-lookup"><span data-stu-id="9c69c-421">Update custom activity</span></span>
<span data-ttu-id="9c69c-422">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span><span class="sxs-lookup"><span data-stu-id="9c69c-422">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="9c69c-423">Appdomain isolation</span><span class="sxs-lookup"><span data-stu-id="9c69c-423">Appdomain isolation</span></span>
<span data-ttu-id="9c69c-424">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span><span class="sxs-lookup"><span data-stu-id="9c69c-424">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="9c69c-425">Access extended properties</span><span class="sxs-lookup"><span data-stu-id="9c69c-425">Access extended properties</span></span>
<span data-ttu-id="9c69c-426">You can declare extended properties in the activity JSON as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="9c69c-426">You can declare extended properties in the activity JSON as shown in the following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="9c69c-427">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-427">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="9c69c-428">The value for SliceStart is based on the SliceStart system variable.</span><span class="sxs-lookup"><span data-stu-id="9c69c-428">The value for SliceStart is based on the SliceStart system variable.</span></span> <span data-ttu-id="9c69c-429">See [System Variables](data-factory-scheduling-and-execution.md#data-factory-functions-and-system-variables) for a list of supported system variables.</span><span class="sxs-lookup"><span data-stu-id="9c69c-429">See [System Variables](data-factory-scheduling-and-execution.md#data-factory-functions-and-system-variables) for a list of supported system variables.</span></span> <span data-ttu-id="9c69c-430">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="9c69c-430">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span></span>

<span data-ttu-id="9c69c-431">To access these extended properties in the **Execute** method, use code similar to the following code:</span><span class="sxs-lookup"><span data-stu-id="9c69c-431">To access these extended properties in the **Execute** method, use code similar to the following code:</span></span>

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="9c69c-432">Auto-scaling of Azure Batch</span><span class="sxs-lookup"><span data-stu-id="9c69c-432">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="9c69c-433">You can also create an Azure Batch pool with **autoscale** feature.</span><span class="sxs-lookup"><span data-stu-id="9c69c-433">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="9c69c-434">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span><span class="sxs-lookup"><span data-stu-id="9c69c-434">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="9c69c-435">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span><span class="sxs-lookup"><span data-stu-id="9c69c-435">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="9c69c-436">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span><span class="sxs-lookup"><span data-stu-id="9c69c-436">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="9c69c-437">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span><span class="sxs-lookup"><span data-stu-id="9c69c-437">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="9c69c-438">It ensures that TargetDedicated never goes beyond 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-438">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="9c69c-439">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-439">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="9c69c-440">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span><span class="sxs-lookup"><span data-stu-id="9c69c-440">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="9c69c-441">Autoscale formula:</span><span class="sxs-lookup"><span data-stu-id="9c69c-441">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="9c69c-442">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span><span class="sxs-lookup"><span data-stu-id="9c69c-442">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="9c69c-443">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-443">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="9c69c-444">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="9c69c-444">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="9c69c-445">Use HDInsight compute service</span><span class="sxs-lookup"><span data-stu-id="9c69c-445">Use HDInsight compute service</span></span>
<span data-ttu-id="9c69c-446">In the walkthrough, you used Azure Batch compute to run the custom activity.</span><span class="sxs-lookup"><span data-stu-id="9c69c-446">In the walkthrough, you used Azure Batch compute to run the custom activity.</span></span> <span data-ttu-id="9c69c-447">You can also use your own HDInsight cluster or have Data Factory create an on-demand HDInsight cluster and have the custom activity run on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="9c69c-447">You can also use your own HDInsight cluster or have Data Factory create an on-demand HDInsight cluster and have the custom activity run on the HDInsight cluster.</span></span> <span data-ttu-id="9c69c-448">Here are the high-level steps for using an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="9c69c-448">Here are the high-level steps for using an HDInsight cluster.</span></span>  

1. <span data-ttu-id="9c69c-449">Create an Azure HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-449">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="9c69c-450">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="9c69c-450">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span></span>

<span data-ttu-id="9c69c-451">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-451">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="9c69c-452">Create Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="9c69c-452">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="9c69c-453">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span><span class="sxs-lookup"><span data-stu-id="9c69c-453">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span></span> <span data-ttu-id="9c69c-454">You can also use your own cluster to perform the same.</span><span class="sxs-lookup"><span data-stu-id="9c69c-454">You can also use your own cluster to perform the same.</span></span> <span data-ttu-id="9c69c-455">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span><span class="sxs-lookup"><span data-stu-id="9c69c-455">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="9c69c-456">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span><span class="sxs-lookup"><span data-stu-id="9c69c-456">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span></span> <span data-ttu-id="9c69c-457">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span><span class="sxs-lookup"><span data-stu-id="9c69c-457">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> At runtime, an instance of a .NET activity runs only on one worker node in the HDInsight cluster; it cannot be scaled to run on multiple nodes. Multiple instances of .NET activity can run in parallel on different nodes of the HDInsight cluster.
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="9c69c-460">To use an on-demand HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="9c69c-460">To use an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="9c69c-461">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span><span class="sxs-lookup"><span data-stu-id="9c69c-461">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="9c69c-462">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span><span class="sxs-lookup"><span data-stu-id="9c69c-462">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="9c69c-463">Make the following changes to the JSON script:</span><span class="sxs-lookup"><span data-stu-id="9c69c-463">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="9c69c-464">For the **clusterSize** property, specify the size of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="9c69c-464">For the **clusterSize** property, specify the size of the HDInsight cluster.</span></span>
   2. <span data-ttu-id="9c69c-465">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span><span class="sxs-lookup"><span data-stu-id="9c69c-465">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="9c69c-466">For the **version** property, specify the HDInsight version you want to use.</span><span class="sxs-lookup"><span data-stu-id="9c69c-466">For the **version** property, specify the HDInsight version you want to use.</span></span> <span data-ttu-id="9c69c-467">If you exclude this property, the latest version is used.</span><span class="sxs-lookup"><span data-stu-id="9c69c-467">If you exclude this property, the latest version is used.</span></span>  
   4. <span data-ttu-id="9c69c-468">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-468">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```
4. <span data-ttu-id="9c69c-469">Click **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-469">Click **Deploy** on the command bar to deploy the linked service.</span></span>

##### <a name="to-use-your-own-hdinsight-cluster"></a><span data-ttu-id="9c69c-470">To use your own HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="9c69c-470">To use your own HDInsight cluster:</span></span>
1. <span data-ttu-id="9c69c-471">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span><span class="sxs-lookup"><span data-stu-id="9c69c-471">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="9c69c-472">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span><span class="sxs-lookup"><span data-stu-id="9c69c-472">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="9c69c-473">Make the following changes to the JSON script:</span><span class="sxs-lookup"><span data-stu-id="9c69c-473">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="9c69c-474">For the **clusterUri** property, enter the URL for your HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c69c-474">For the **clusterUri** property, enter the URL for your HDInsight.</span></span> <span data-ttu-id="9c69c-475">For example: https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="9c69c-475">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="9c69c-476">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="9c69c-476">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span></span>
   3. <span data-ttu-id="9c69c-477">For the **Password** property, enter the password for the user.</span><span class="sxs-lookup"><span data-stu-id="9c69c-477">For the **Password** property, enter the password for the user.</span></span>
   4. <span data-ttu-id="9c69c-478">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="9c69c-478">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="9c69c-479">Click **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="9c69c-479">Click **Deploy** on the command bar to deploy the linked service.</span></span>

<span data-ttu-id="9c69c-480">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span><span class="sxs-lookup"><span data-stu-id="9c69c-480">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="9c69c-481">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span><span class="sxs-lookup"><span data-stu-id="9c69c-481">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="examples"></a><span data-ttu-id="9c69c-482">Examples</span><span class="sxs-lookup"><span data-stu-id="9c69c-482">Examples</span></span>
| <span data-ttu-id="9c69c-483">Sample</span><span class="sxs-lookup"><span data-stu-id="9c69c-483">Sample</span></span> | <span data-ttu-id="9c69c-484">What custom activity does</span><span class="sxs-lookup"><span data-stu-id="9c69c-484">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="9c69c-485">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="9c69c-485">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="9c69c-486">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9c69c-486">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="9c69c-487">Twitter Sentiment Analysis sample</span><span class="sxs-lookup"><span data-stu-id="9c69c-487">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="9c69c-488">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span><span class="sxs-lookup"><span data-stu-id="9c69c-488">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="9c69c-489">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="9c69c-489">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="9c69c-490">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span><span class="sxs-lookup"><span data-stu-id="9c69c-490">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="9c69c-491">Cross AppDomain .NET Activity</span><span class="sxs-lookup"><span data-stu-id="9c69c-491">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="9c69c-492">Uses different assembly versions from ones used by the Data Factory launcher</span><span class="sxs-lookup"><span data-stu-id="9c69c-492">Uses different assembly versions from ones used by the Data Factory launcher</span></span> |
| [<span data-ttu-id="9c69c-493">Reprocess a model in Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="9c69c-493">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="9c69c-494">Reprocesses a model in Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="9c69c-494">Reprocesses a model in Azure Analysis Services.</span></span> |


[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[azure-developer-center]: http://azure.microsoft.com/develop/net/
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png















