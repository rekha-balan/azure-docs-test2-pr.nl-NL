---
title: Copy data to/from a file system using Azure Data Factory | Microsoft Docs
description: Learn how to copy data to and from an on-premises file system by using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/13/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 7ab38c689cb6445bc85a942fc350c2a1f5de7912
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856119"
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="85614-103">Copy data to and from an on-premises file system by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="85614-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-onprem-file-system-connector.md)
> * [Version 2 (current version)](../connector-file-system.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [File System connector in V2](../connector-file-system.md).


<span data-ttu-id="85614-108">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span><span class="sxs-lookup"><span data-stu-id="85614-108">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="85614-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="85614-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="85614-110">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="85614-110">Supported scenarios</span></span>
<span data-ttu-id="85614-111">You can copy data **from an on-premises file system** to the following data stores:</span><span class="sxs-lookup"><span data-stu-id="85614-111">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="85614-112">You can copy data from the following data stores **to an on-premises file system**:</span><span class="sxs-lookup"><span data-stu-id="85614-112">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Copy Activity does not delete the source file after it is successfully copied to the destination. If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline. 

## <a name="enabling-connectivity"></a><span data-ttu-id="85614-115">Enabling connectivity</span><span class="sxs-lookup"><span data-stu-id="85614-115">Enabling connectivity</span></span>
<span data-ttu-id="85614-116">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="85614-116">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="85614-117">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span><span class="sxs-lookup"><span data-stu-id="85614-117">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="85614-118">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="85614-118">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="85614-119">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span><span class="sxs-lookup"><span data-stu-id="85614-119">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="85614-120">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="85614-120">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="85614-121">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="85614-121">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="85614-122">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span><span class="sxs-lookup"><span data-stu-id="85614-122">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="85614-123">Installing Data Management Gateway on a Linux server is not supported.</span><span class="sxs-lookup"><span data-stu-id="85614-123">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="85614-124">Getting started</span><span class="sxs-lookup"><span data-stu-id="85614-124">Getting started</span></span>
<span data-ttu-id="85614-125">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="85614-125">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="85614-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="85614-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="85614-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="85614-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="85614-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="85614-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="85614-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="85614-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="85614-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="85614-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="85614-131">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="85614-131">Create a **data factory**.</span></span> <span data-ttu-id="85614-132">A data factory may contain one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="85614-132">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="85614-133">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="85614-133">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="85614-134">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="85614-134">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="85614-135">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="85614-135">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="85614-136">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="85614-136">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="85614-137">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="85614-137">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="85614-138">And, you create another dataset to specify the folder and file name (optional) in your file system.</span><span class="sxs-lookup"><span data-stu-id="85614-138">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="85614-139">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="85614-139">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="85614-140">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="85614-140">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="85614-141">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="85614-141">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="85614-142">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span><span class="sxs-lookup"><span data-stu-id="85614-142">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="85614-143">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="85614-143">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="85614-144">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span><span class="sxs-lookup"><span data-stu-id="85614-144">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="85614-145">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="85614-145">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="85614-146">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="85614-146">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="85614-147">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span><span class="sxs-lookup"><span data-stu-id="85614-147">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="85614-148">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span><span class="sxs-lookup"><span data-stu-id="85614-148">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="85614-149">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="85614-149">Linked service properties</span></span>
<span data-ttu-id="85614-150">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span><span class="sxs-lookup"><span data-stu-id="85614-150">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="85614-151">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span><span class="sxs-lookup"><span data-stu-id="85614-151">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="85614-152">Property</span><span class="sxs-lookup"><span data-stu-id="85614-152">Property</span></span> | <span data-ttu-id="85614-153">Description</span><span class="sxs-lookup"><span data-stu-id="85614-153">Description</span></span> | <span data-ttu-id="85614-154">Required</span><span class="sxs-lookup"><span data-stu-id="85614-154">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85614-155">type</span><span class="sxs-lookup"><span data-stu-id="85614-155">type</span></span> |<span data-ttu-id="85614-156">Ensure that the type property is set to **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="85614-156">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="85614-157">Yes</span><span class="sxs-lookup"><span data-stu-id="85614-157">Yes</span></span> |
| <span data-ttu-id="85614-158">host</span><span class="sxs-lookup"><span data-stu-id="85614-158">host</span></span> |<span data-ttu-id="85614-159">Specifies the root path of the folder that you want to copy.</span><span class="sxs-lookup"><span data-stu-id="85614-159">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="85614-160">Use the escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="85614-160">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="85614-161">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="85614-161">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="85614-162">Yes</span><span class="sxs-lookup"><span data-stu-id="85614-162">Yes</span></span> |
| <span data-ttu-id="85614-163">userid</span><span class="sxs-lookup"><span data-stu-id="85614-163">userid</span></span> |<span data-ttu-id="85614-164">Specify the ID of the user who has access to the server.</span><span class="sxs-lookup"><span data-stu-id="85614-164">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="85614-165">No (if you choose encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="85614-165">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="85614-166">password</span><span class="sxs-lookup"><span data-stu-id="85614-166">password</span></span> |<span data-ttu-id="85614-167">Specify the password for the user (userid).</span><span class="sxs-lookup"><span data-stu-id="85614-167">Specify the password for the user (userid).</span></span> |<span data-ttu-id="85614-168">No (if you choose encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="85614-168">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="85614-169">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="85614-169">encryptedCredential</span></span> |<span data-ttu-id="85614-170">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="85614-170">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="85614-171">No (if you choose to specify userid and password in plain text)</span><span class="sxs-lookup"><span data-stu-id="85614-171">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="85614-172">gatewayName</span><span class="sxs-lookup"><span data-stu-id="85614-172">gatewayName</span></span> |<span data-ttu-id="85614-173">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span><span class="sxs-lookup"><span data-stu-id="85614-173">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="85614-174">Yes</span><span class="sxs-lookup"><span data-stu-id="85614-174">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="85614-175">Sample linked service and dataset definitions</span><span class="sxs-lookup"><span data-stu-id="85614-175">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="85614-176">Scenario</span><span class="sxs-lookup"><span data-stu-id="85614-176">Scenario</span></span> | <span data-ttu-id="85614-177">Host in linked service definition</span><span class="sxs-lookup"><span data-stu-id="85614-177">Host in linked service definition</span></span> | <span data-ttu-id="85614-178">folderPath in dataset definition</span><span class="sxs-lookup"><span data-stu-id="85614-178">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85614-179">Local folder on Data Management Gateway machine:</span><span class="sxs-lookup"><span data-stu-id="85614-179">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="85614-180">Examples: D:\\\* or D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="85614-180">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="85614-181">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="85614-181">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="85614-182">localhost (for earlier versions than Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="85614-182">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="85614-183">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="85614-183">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="85614-184">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span><span class="sxs-lookup"><span data-stu-id="85614-184">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="85614-185">Remote shared folder:</span><span class="sxs-lookup"><span data-stu-id="85614-185">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="85614-186">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="85614-186">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="85614-187">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="85614-187">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="85614-188">.\\\\ or folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="85614-188">.\\\\ or folder\\\\subfolder</span></span> |

>[!NOTE]
>When authoring via UI, you don't need to input double backslash (`\\`) to escape like you do via JSON, specify single backslash.

### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="85614-190">Example: Using username and password in plain text</span><span class="sxs-lookup"><span data-stu-id="85614-190">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="85614-191">Example: Using encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="85614-191">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="85614-192">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="85614-192">Dataset properties</span></span>
<span data-ttu-id="85614-193">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="85614-193">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="85614-194">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="85614-194">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="85614-195">The typeProperties section is different for each type of dataset.</span><span class="sxs-lookup"><span data-stu-id="85614-195">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="85614-196">It provides information such as the location and format of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="85614-196">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="85614-197">The typeProperties section for the dataset of type **FileShare** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="85614-197">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="85614-198">Property</span><span class="sxs-lookup"><span data-stu-id="85614-198">Property</span></span> | <span data-ttu-id="85614-199">Description</span><span class="sxs-lookup"><span data-stu-id="85614-199">Description</span></span> | <span data-ttu-id="85614-200">Required</span><span class="sxs-lookup"><span data-stu-id="85614-200">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85614-201">folderPath</span><span class="sxs-lookup"><span data-stu-id="85614-201">folderPath</span></span> |<span data-ttu-id="85614-202">Specifies the subpath to the folder.</span><span class="sxs-lookup"><span data-stu-id="85614-202">Specifies the subpath to the folder.</span></span> <span data-ttu-id="85614-203">Use the escape character '\' for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="85614-203">Use the escape character '\' for special characters in the string.</span></span> <span data-ttu-id="85614-204">Wildcard filter is not supported.</span><span class="sxs-lookup"><span data-stu-id="85614-204">Wildcard filter is not supported.</span></span> <span data-ttu-id="85614-205">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="85614-205">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="85614-206">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="85614-206">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="85614-207">Yes</span><span class="sxs-lookup"><span data-stu-id="85614-207">Yes</span></span> |
| <span data-ttu-id="85614-208">fileName</span><span class="sxs-lookup"><span data-stu-id="85614-208">fileName</span></span> |<span data-ttu-id="85614-209">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="85614-209">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="85614-210">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="85614-210">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="85614-211">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="85614-211">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="85614-212">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="85614-212">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="85614-213">No</span><span class="sxs-lookup"><span data-stu-id="85614-213">No</span></span> |
| <span data-ttu-id="85614-214">fileFilter</span><span class="sxs-lookup"><span data-stu-id="85614-214">fileFilter</span></span> |<span data-ttu-id="85614-215">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="85614-215">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="85614-216">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="85614-216">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="85614-217">Example 1: "fileFilter": "\*.log"</span><span class="sxs-lookup"><span data-stu-id="85614-217">Example 1: "fileFilter": "\*.log"</span></span><br/><span data-ttu-id="85614-218">Example 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="85614-218">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="85614-219">Note that fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="85614-219">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="85614-220">No</span><span class="sxs-lookup"><span data-stu-id="85614-220">No</span></span> |
| <span data-ttu-id="85614-221">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="85614-221">partitionedBy</span></span> |<span data-ttu-id="85614-222">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span><span class="sxs-lookup"><span data-stu-id="85614-222">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="85614-223">An example is folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="85614-223">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="85614-224">No</span><span class="sxs-lookup"><span data-stu-id="85614-224">No</span></span> |
| <span data-ttu-id="85614-225">format</span><span class="sxs-lookup"><span data-stu-id="85614-225">format</span></span> | <span data-ttu-id="85614-226">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="85614-226">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="85614-227">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="85614-227">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="85614-228">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="85614-228">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="85614-229">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="85614-229">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="85614-230">No</span><span class="sxs-lookup"><span data-stu-id="85614-230">No</span></span> |
| <span data-ttu-id="85614-231">compression</span><span class="sxs-lookup"><span data-stu-id="85614-231">compression</span></span> | <span data-ttu-id="85614-232">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="85614-232">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="85614-233">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="85614-233">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="85614-234">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="85614-234">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="85614-235">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="85614-235">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="85614-236">No</span><span class="sxs-lookup"><span data-stu-id="85614-236">No</span></span> |

> [!NOTE]
> You cannot use fileName and fileFilter simultaneously.

### <a name="using-partitionedby-property"></a><span data-ttu-id="85614-238">Using partitionedBy property</span><span class="sxs-lookup"><span data-stu-id="85614-238">Using partitionedBy property</span></span>
<span data-ttu-id="85614-239">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="85614-239">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="85614-240">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="85614-240">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="85614-241">Sample 1:</span><span class="sxs-lookup"><span data-stu-id="85614-241">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="85614-242">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="85614-242">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="85614-243">SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="85614-243">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="85614-244">The folderPath is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="85614-244">The folderPath is different for each slice.</span></span> <span data-ttu-id="85614-245">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="85614-245">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="85614-246">Sample 2:</span><span class="sxs-lookup"><span data-stu-id="85614-246">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="85614-247">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span><span class="sxs-lookup"><span data-stu-id="85614-247">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="85614-248">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="85614-248">Copy activity properties</span></span>
<span data-ttu-id="85614-249">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="85614-249">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="85614-250">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="85614-250">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="85614-251">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="85614-251">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="85614-252">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="85614-252">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="85614-253">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="85614-253">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="85614-254">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="85614-254">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="85614-255">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="85614-255">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="85614-256">**FileSystemSource** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="85614-256">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="85614-257">Property</span><span class="sxs-lookup"><span data-stu-id="85614-257">Property</span></span> | <span data-ttu-id="85614-258">Description</span><span class="sxs-lookup"><span data-stu-id="85614-258">Description</span></span> | <span data-ttu-id="85614-259">Allowed values</span><span class="sxs-lookup"><span data-stu-id="85614-259">Allowed values</span></span> | <span data-ttu-id="85614-260">Required</span><span class="sxs-lookup"><span data-stu-id="85614-260">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="85614-261">recursive</span><span class="sxs-lookup"><span data-stu-id="85614-261">recursive</span></span> |<span data-ttu-id="85614-262">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="85614-262">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="85614-263">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="85614-263">True, False (default)</span></span> |<span data-ttu-id="85614-264">No</span><span class="sxs-lookup"><span data-stu-id="85614-264">No</span></span> |

<span data-ttu-id="85614-265">**FileSystemSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="85614-265">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="85614-266">Property</span><span class="sxs-lookup"><span data-stu-id="85614-266">Property</span></span> | <span data-ttu-id="85614-267">Description</span><span class="sxs-lookup"><span data-stu-id="85614-267">Description</span></span> | <span data-ttu-id="85614-268">Allowed values</span><span class="sxs-lookup"><span data-stu-id="85614-268">Allowed values</span></span> | <span data-ttu-id="85614-269">Required</span><span class="sxs-lookup"><span data-stu-id="85614-269">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="85614-270">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="85614-270">copyBehavior</span></span> |<span data-ttu-id="85614-271">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="85614-271">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="85614-272">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="85614-272">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="85614-273">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span><span class="sxs-lookup"><span data-stu-id="85614-273">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="85614-274">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="85614-274">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="85614-275">The target files are created with an autogenerated name.</span><span class="sxs-lookup"><span data-stu-id="85614-275">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="85614-276">**MergeFiles:** Merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="85614-276">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="85614-277">If the file name/blob name is specified, the merged file name is the specified name.</span><span class="sxs-lookup"><span data-stu-id="85614-277">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="85614-278">Otherwise, it is an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="85614-278">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="85614-279">No</span><span class="sxs-lookup"><span data-stu-id="85614-279">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="85614-280">recursive and copyBehavior examples</span><span class="sxs-lookup"><span data-stu-id="85614-280">recursive and copyBehavior examples</span></span>
<span data-ttu-id="85614-281">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span><span class="sxs-lookup"><span data-stu-id="85614-281">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="85614-282">recursive value</span><span class="sxs-lookup"><span data-stu-id="85614-282">recursive value</span></span> | <span data-ttu-id="85614-283">copyBehavior value</span><span class="sxs-lookup"><span data-stu-id="85614-283">copyBehavior value</span></span> | <span data-ttu-id="85614-284">Resulting behavior</span><span class="sxs-lookup"><span data-stu-id="85614-284">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85614-285">true</span><span class="sxs-lookup"><span data-stu-id="85614-285">true</span></span> |<span data-ttu-id="85614-286">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="85614-286">preserveHierarchy</span></span> |<span data-ttu-id="85614-287">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="85614-287">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="85614-288">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-288">Folder1</span></span><br/><span data-ttu-id="85614-289">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-289">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-290">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-290">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="85614-291">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="85614-291">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="85614-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="85614-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="85614-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="85614-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="85614-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="85614-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="85614-295">the target folder Folder1 is created with the same structure as the source:</span><span class="sxs-lookup"><span data-stu-id="85614-295">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="85614-296">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-296">Folder1</span></span><br/><span data-ttu-id="85614-297">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-297">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-298">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-298">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="85614-299">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="85614-299">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="85614-300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="85614-300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="85614-301">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="85614-301">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="85614-302">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="85614-302">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="85614-303">true</span><span class="sxs-lookup"><span data-stu-id="85614-303">true</span></span> |<span data-ttu-id="85614-304">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="85614-304">flattenHierarchy</span></span> |<span data-ttu-id="85614-305">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="85614-305">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="85614-306">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-306">Folder1</span></span><br/><span data-ttu-id="85614-307">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-307">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-308">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-308">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="85614-309">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="85614-309">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="85614-310">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="85614-310">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="85614-311">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="85614-311">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="85614-312">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="85614-312">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="85614-313">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="85614-313">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="85614-314">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-314">Folder1</span></span><br/><span data-ttu-id="85614-315">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="85614-315">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="85614-316">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="85614-316">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="85614-317">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span><span class="sxs-lookup"><span data-stu-id="85614-317">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="85614-318">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span><span class="sxs-lookup"><span data-stu-id="85614-318">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="85614-319">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span><span class="sxs-lookup"><span data-stu-id="85614-319">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="85614-320">true</span><span class="sxs-lookup"><span data-stu-id="85614-320">true</span></span> |<span data-ttu-id="85614-321">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="85614-321">mergeFiles</span></span> |<span data-ttu-id="85614-322">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="85614-322">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="85614-323">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-323">Folder1</span></span><br/><span data-ttu-id="85614-324">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-324">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-325">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-325">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="85614-326">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="85614-326">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="85614-327">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="85614-327">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="85614-328">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="85614-328">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="85614-329">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="85614-329">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="85614-330">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="85614-330">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="85614-331">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-331">Folder1</span></span><br/><span data-ttu-id="85614-332">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="85614-332">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="85614-333">false</span><span class="sxs-lookup"><span data-stu-id="85614-333">false</span></span> |<span data-ttu-id="85614-334">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="85614-334">preserveHierarchy</span></span> |<span data-ttu-id="85614-335">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="85614-335">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="85614-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-336">Folder1</span></span><br/><span data-ttu-id="85614-337">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-337">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-338">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-338">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="85614-339">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="85614-339">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="85614-340">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="85614-340">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="85614-341">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="85614-341">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="85614-342">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="85614-342">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="85614-343">the target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="85614-343">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="85614-344">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-344">Folder1</span></span><br/><span data-ttu-id="85614-345">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-345">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-346">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-346">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="85614-347">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="85614-347">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="85614-348">false</span><span class="sxs-lookup"><span data-stu-id="85614-348">false</span></span> |<span data-ttu-id="85614-349">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="85614-349">flattenHierarchy</span></span> |<span data-ttu-id="85614-350">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="85614-350">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="85614-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-351">Folder1</span></span><br/><span data-ttu-id="85614-352">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-352">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-353">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-353">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="85614-354">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="85614-354">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="85614-355">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="85614-355">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="85614-356">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="85614-356">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="85614-357">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="85614-357">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="85614-358">the target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="85614-358">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="85614-359">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-359">Folder1</span></span><br/><span data-ttu-id="85614-360">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="85614-360">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="85614-361">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="85614-361">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="85614-362">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="85614-362">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="85614-363">false</span><span class="sxs-lookup"><span data-stu-id="85614-363">false</span></span> |<span data-ttu-id="85614-364">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="85614-364">mergeFiles</span></span> |<span data-ttu-id="85614-365">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="85614-365">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="85614-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-366">Folder1</span></span><br/><span data-ttu-id="85614-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="85614-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="85614-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="85614-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="85614-369">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="85614-369">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="85614-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="85614-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="85614-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="85614-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="85614-372">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="85614-372">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="85614-373">the target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="85614-373">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="85614-374">Folder1</span><span class="sxs-lookup"><span data-stu-id="85614-374">Folder1</span></span><br/><span data-ttu-id="85614-375">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="85614-375">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="85614-376">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="85614-376">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="85614-377">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="85614-377">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="85614-378">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="85614-378">Supported file and compression formats</span></span>
<span data-ttu-id="85614-379">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span><span class="sxs-lookup"><span data-stu-id="85614-379">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="85614-380">JSON examples for copying data to and from file system</span><span class="sxs-lookup"><span data-stu-id="85614-380">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="85614-381">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="85614-381">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="85614-382">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="85614-382">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="85614-383">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="85614-383">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="85614-384">Example: Copy data from an on-premises file system to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="85614-384">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="85614-385">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="85614-385">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="85614-386">The sample has the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="85614-386">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="85614-387">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-387">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="85614-388">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-388">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="85614-389">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-389">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="85614-390">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-390">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="85614-391">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-391">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="85614-392">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span><span class="sxs-lookup"><span data-stu-id="85614-392">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="85614-393">The JSON properties that are used in these samples are described in the sections after the samples.</span><span class="sxs-lookup"><span data-stu-id="85614-393">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="85614-394">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="85614-394">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="85614-395">**On-Premises File Server linked service:**</span><span class="sxs-lookup"><span data-stu-id="85614-395">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="85614-396">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span><span class="sxs-lookup"><span data-stu-id="85614-396">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="85614-397">See [File Server linked service](#linked-service-properties) for details about this linked service.</span><span class="sxs-lookup"><span data-stu-id="85614-397">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="85614-398">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="85614-398">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="85614-399">**On-premises file system input dataset:**</span><span class="sxs-lookup"><span data-stu-id="85614-399">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="85614-400">Data is picked up from a new file every hour.</span><span class="sxs-lookup"><span data-stu-id="85614-400">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="85614-401">The folderPath and fileName properties are determined based on the start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="85614-401">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="85614-402">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="85614-402">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="85614-403">**Azure Blob storage output dataset:**</span><span class="sxs-lookup"><span data-stu-id="85614-403">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="85614-404">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="85614-404">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="85614-405">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="85614-405">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="85614-406">The folder path uses the year, month, day, and hour parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="85614-406">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="85614-407">**A copy activity in a pipeline with File System source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="85614-407">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="85614-408">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="85614-408">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="85614-409">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="85614-409">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="85614-410">Example: Copy data from Azure SQL Database to an on-premises file system</span><span class="sxs-lookup"><span data-stu-id="85614-410">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="85614-411">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="85614-411">The following sample shows:</span></span>

* <span data-ttu-id="85614-412">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="85614-412">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="85614-413">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-413">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="85614-414">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-414">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="85614-415">An output dataset of type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-415">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="85614-416">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="85614-416">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="85614-417">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span><span class="sxs-lookup"><span data-stu-id="85614-417">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="85614-418">The JSON properties that are used in these samples are described in sections after the samples.</span><span class="sxs-lookup"><span data-stu-id="85614-418">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="85614-419">**Azure SQL Database linked service:**</span><span class="sxs-lookup"><span data-stu-id="85614-419">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="85614-420">**On-Premises File Server linked service:**</span><span class="sxs-lookup"><span data-stu-id="85614-420">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="85614-421">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span><span class="sxs-lookup"><span data-stu-id="85614-421">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="85614-422">See [File System linked service](#linked-service-properties) for details about this linked service.</span><span class="sxs-lookup"><span data-stu-id="85614-422">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="85614-423">**Azure SQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="85614-423">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="85614-424">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span><span class="sxs-lookup"><span data-stu-id="85614-424">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="85614-425">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="85614-425">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="85614-426">**On-premises file system output dataset:**</span><span class="sxs-lookup"><span data-stu-id="85614-426">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="85614-427">Data is copied to a new file every hour.</span><span class="sxs-lookup"><span data-stu-id="85614-427">Data is copied to a new file every hour.</span></span> <span data-ttu-id="85614-428">The folderPath and fileName for the blob are determined based on the start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="85614-428">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="85614-429">**A copy activity in a pipeline with SQL source and File System sink:**</span><span class="sxs-lookup"><span data-stu-id="85614-429">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="85614-430">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="85614-430">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="85614-431">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="85614-431">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="85614-432">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="85614-432">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="85614-433">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span><span class="sxs-lookup"><span data-stu-id="85614-433">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="85614-434">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="85614-434">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="85614-435">Performance and tuning</span><span class="sxs-lookup"><span data-stu-id="85614-435">Performance and tuning</span></span>
 <span data-ttu-id="85614-436">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="85614-436">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
