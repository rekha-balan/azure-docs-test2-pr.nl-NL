---
title: Move data to/from a file system using Azure Data Factory | Microsoft Docs
description: Learn how to move data to and from an on-premises file system by using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: jingwang
ms.openlocfilehash: 6c26bf3eda7ef15e7a580a31ab7b6624c8a7a826
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562828"
---
# <a name="move-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="745da-103">Move data to and from an on-premises file system by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="745da-103">Move data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="745da-104">You can copy data from HDFS to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="745da-104">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="745da-105">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="745da-105">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="745da-106">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span><span class="sxs-lookup"><span data-stu-id="745da-106">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

<span data-ttu-id="745da-107">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from an on-premises file system.</span><span class="sxs-lookup"><span data-stu-id="745da-107">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from an on-premises file system.</span></span> <span data-ttu-id="745da-108">You can copy data from an on-premises file system to any supported sink data store or from any supported source data store .</span><span class="sxs-lookup"><span data-stu-id="745da-108">You can copy data from an on-premises file system to any supported sink data store or from any supported source data store .</span></span> <span data-ttu-id="745da-109">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="745da-109">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="745da-110">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="745da-110">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> <span data-ttu-id="745da-111">See [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for a list of data stores that can be used as sources or sinks with the on-premises file system.</span><span class="sxs-lookup"><span data-stu-id="745da-111">See [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for a list of data stores that can be used as sources or sinks with the on-premises file system.</span></span>

> [!NOTE]
> <span data-ttu-id="745da-112">Copy Activity does not delete the source file after it is successfully copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="745da-112">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="745da-113">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="745da-113">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="745da-114">Enabling connectivity</span><span class="sxs-lookup"><span data-stu-id="745da-114">Enabling connectivity</span></span>
<span data-ttu-id="745da-115">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="745da-115">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="745da-116">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span><span class="sxs-lookup"><span data-stu-id="745da-116">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="745da-117">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="745da-117">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="745da-118">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span><span class="sxs-lookup"><span data-stu-id="745da-118">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="745da-119">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="745da-119">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="745da-120">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="745da-120">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="745da-121">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span><span class="sxs-lookup"><span data-stu-id="745da-121">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="745da-122">Installing Data Management Gateway on a Linux server is not supported.</span><span class="sxs-lookup"><span data-stu-id="745da-122">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="745da-123">Getting started</span><span class="sxs-lookup"><span data-stu-id="745da-123">Getting started</span></span>
<span data-ttu-id="745da-124">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="745da-124">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="745da-125">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="745da-125">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="745da-126">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="745da-126">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="745da-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="745da-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="745da-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="745da-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="745da-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="745da-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="745da-130">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="745da-130">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="745da-131">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="745da-131">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="745da-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="745da-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="745da-133">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="745da-133">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="745da-134">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="745da-134">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="745da-135">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an file system, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="745da-135">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an file system, see [JSON examples](#json-examples) section of this article.</span></span>

<span data-ttu-id="745da-136">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span><span class="sxs-lookup"><span data-stu-id="745da-136">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="745da-137">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="745da-137">Linked service properties</span></span>
<span data-ttu-id="745da-138">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span><span class="sxs-lookup"><span data-stu-id="745da-138">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="745da-139">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span><span class="sxs-lookup"><span data-stu-id="745da-139">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="745da-140">Property</span><span class="sxs-lookup"><span data-stu-id="745da-140">Property</span></span> | <span data-ttu-id="745da-141">Description</span><span class="sxs-lookup"><span data-stu-id="745da-141">Description</span></span> | <span data-ttu-id="745da-142">Required</span><span class="sxs-lookup"><span data-stu-id="745da-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="745da-143">type</span><span class="sxs-lookup"><span data-stu-id="745da-143">type</span></span> |<span data-ttu-id="745da-144">Ensure that the type property is set to **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="745da-144">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="745da-145">Yes</span><span class="sxs-lookup"><span data-stu-id="745da-145">Yes</span></span> |
| <span data-ttu-id="745da-146">host</span><span class="sxs-lookup"><span data-stu-id="745da-146">host</span></span> |<span data-ttu-id="745da-147">Specifies the root path of the folder that you want to copy.</span><span class="sxs-lookup"><span data-stu-id="745da-147">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="745da-148">Use the escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="745da-148">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="745da-149">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="745da-149">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="745da-150">Yes</span><span class="sxs-lookup"><span data-stu-id="745da-150">Yes</span></span> |
| <span data-ttu-id="745da-151">userid</span><span class="sxs-lookup"><span data-stu-id="745da-151">userid</span></span> |<span data-ttu-id="745da-152">Specify the ID of the user who has access to the server.</span><span class="sxs-lookup"><span data-stu-id="745da-152">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="745da-153">No (if you choose encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="745da-153">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="745da-154">password</span><span class="sxs-lookup"><span data-stu-id="745da-154">password</span></span> |<span data-ttu-id="745da-155">Specify the password for the user (userid).</span><span class="sxs-lookup"><span data-stu-id="745da-155">Specify the password for the user (userid).</span></span> |<span data-ttu-id="745da-156">No (if you choose encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="745da-156">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="745da-157">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="745da-157">encryptedCredential</span></span> |<span data-ttu-id="745da-158">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="745da-158">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="745da-159">No (if you choose to specify userid and password in plain text)</span><span class="sxs-lookup"><span data-stu-id="745da-159">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="745da-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="745da-160">gatewayName</span></span> |<span data-ttu-id="745da-161">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span><span class="sxs-lookup"><span data-stu-id="745da-161">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="745da-162">Yes</span><span class="sxs-lookup"><span data-stu-id="745da-162">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="745da-163">Sample linked service and dataset definitions</span><span class="sxs-lookup"><span data-stu-id="745da-163">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="745da-164">Scenario</span><span class="sxs-lookup"><span data-stu-id="745da-164">Scenario</span></span> | <span data-ttu-id="745da-165">Host in linked service definition</span><span class="sxs-lookup"><span data-stu-id="745da-165">Host in linked service definition</span></span> | <span data-ttu-id="745da-166">folderPath in dataset definition</span><span class="sxs-lookup"><span data-stu-id="745da-166">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="745da-167">Local folder on Data Management Gateway machine:</span><span class="sxs-lookup"><span data-stu-id="745da-167">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="745da-168">Examples: D:\\\* or D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="745da-168">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="745da-169">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="745da-169">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="745da-170">localhost (for earlier versions than Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="745da-170">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="745da-171">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="745da-171">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="745da-172">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span><span class="sxs-lookup"><span data-stu-id="745da-172">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="745da-173">Remote shared folder:</span><span class="sxs-lookup"><span data-stu-id="745da-173">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="745da-174">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="745da-174">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="745da-175">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="745da-175">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="745da-176">.\\\\ or folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="745da-176">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="745da-177">Example: Using username and password in plain text</span><span class="sxs-lookup"><span data-stu-id="745da-177">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="745da-178">Example: Using encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="745da-178">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="745da-179">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="745da-179">Dataset properties</span></span>
<span data-ttu-id="745da-180">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="745da-180">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="745da-181">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="745da-181">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="745da-182">The typeProperties section is different for each type of dataset.</span><span class="sxs-lookup"><span data-stu-id="745da-182">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="745da-183">It provides information such as the location and format of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="745da-183">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="745da-184">The typeProperties section for the dataset of type **FileShare** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="745da-184">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="745da-185">Property</span><span class="sxs-lookup"><span data-stu-id="745da-185">Property</span></span> | <span data-ttu-id="745da-186">Description</span><span class="sxs-lookup"><span data-stu-id="745da-186">Description</span></span> | <span data-ttu-id="745da-187">Required</span><span class="sxs-lookup"><span data-stu-id="745da-187">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="745da-188">folderPath</span><span class="sxs-lookup"><span data-stu-id="745da-188">folderPath</span></span> |<span data-ttu-id="745da-189">Specifies the subpath to the folder.</span><span class="sxs-lookup"><span data-stu-id="745da-189">Specifies the subpath to the folder.</span></span> <span data-ttu-id="745da-190">Use the escape character ‘\’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="745da-190">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="745da-191">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="745da-191">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="745da-192">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="745da-192">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="745da-193">Yes</span><span class="sxs-lookup"><span data-stu-id="745da-193">Yes</span></span> |
| <span data-ttu-id="745da-194">fileName</span><span class="sxs-lookup"><span data-stu-id="745da-194">fileName</span></span> |<span data-ttu-id="745da-195">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="745da-195">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="745da-196">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="745da-196">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="745da-197">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="745da-197">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="745da-198">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="745da-198">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="745da-199">No</span><span class="sxs-lookup"><span data-stu-id="745da-199">No</span></span> |
| <span data-ttu-id="745da-200">fileFilter</span><span class="sxs-lookup"><span data-stu-id="745da-200">fileFilter</span></span> |<span data-ttu-id="745da-201">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="745da-201">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="745da-202">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="745da-202">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="745da-203">Example 1: "fileFilter": "\*.log"</span><span class="sxs-lookup"><span data-stu-id="745da-203">Example 1: "fileFilter": "\*.log"</span></span><br/><span data-ttu-id="745da-204">Example 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="745da-204">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="745da-205">Note that fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="745da-205">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="745da-206">No</span><span class="sxs-lookup"><span data-stu-id="745da-206">No</span></span> |
| <span data-ttu-id="745da-207">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="745da-207">partitionedBy</span></span> |<span data-ttu-id="745da-208">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span><span class="sxs-lookup"><span data-stu-id="745da-208">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="745da-209">An example is folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="745da-209">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="745da-210">No</span><span class="sxs-lookup"><span data-stu-id="745da-210">No</span></span> |
| <span data-ttu-id="745da-211">format</span><span class="sxs-lookup"><span data-stu-id="745da-211">format</span></span> | <span data-ttu-id="745da-212">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="745da-212">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="745da-213">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="745da-213">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="745da-214">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="745da-214">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="745da-215">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="745da-215">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="745da-216">No</span><span class="sxs-lookup"><span data-stu-id="745da-216">No</span></span> |
| <span data-ttu-id="745da-217">compression</span><span class="sxs-lookup"><span data-stu-id="745da-217">compression</span></span> | <span data-ttu-id="745da-218">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="745da-218">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="745da-219">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="745da-219">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="745da-220">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="745da-220">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="745da-221">No</span><span class="sxs-lookup"><span data-stu-id="745da-221">No</span></span> |

> [!NOTE]
> <span data-ttu-id="745da-222">You cannot use fileName and fileFilter simultaneously.</span><span class="sxs-lookup"><span data-stu-id="745da-222">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="745da-223">Using partitionedBy property</span><span class="sxs-lookup"><span data-stu-id="745da-223">Using partitionedBy property</span></span>
<span data-ttu-id="745da-224">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="745da-224">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="745da-225">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="745da-225">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="745da-226">Sample 1:</span><span class="sxs-lookup"><span data-stu-id="745da-226">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="745da-227">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="745da-227">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="745da-228">SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="745da-228">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="745da-229">The folderPath is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="745da-229">The folderPath is different for each slice.</span></span> <span data-ttu-id="745da-230">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="745da-230">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="745da-231">Sample 2:</span><span class="sxs-lookup"><span data-stu-id="745da-231">Sample 2:</span></span>

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

<span data-ttu-id="745da-232">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span><span class="sxs-lookup"><span data-stu-id="745da-232">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="745da-233">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="745da-233">Copy activity properties</span></span>
<span data-ttu-id="745da-234">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="745da-234">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="745da-235">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="745da-235">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="745da-236">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="745da-236">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="745da-237">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="745da-237">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="745da-238">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="745da-238">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="745da-239">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="745da-239">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="745da-240">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="745da-240">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="745da-241">**FileSystemSource** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="745da-241">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="745da-242">Property</span><span class="sxs-lookup"><span data-stu-id="745da-242">Property</span></span> | <span data-ttu-id="745da-243">Description</span><span class="sxs-lookup"><span data-stu-id="745da-243">Description</span></span> | <span data-ttu-id="745da-244">Allowed values</span><span class="sxs-lookup"><span data-stu-id="745da-244">Allowed values</span></span> | <span data-ttu-id="745da-245">Required</span><span class="sxs-lookup"><span data-stu-id="745da-245">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="745da-246">recursive</span><span class="sxs-lookup"><span data-stu-id="745da-246">recursive</span></span> |<span data-ttu-id="745da-247">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="745da-247">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="745da-248">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="745da-248">True, False (default)</span></span> |<span data-ttu-id="745da-249">No</span><span class="sxs-lookup"><span data-stu-id="745da-249">No</span></span> |

<span data-ttu-id="745da-250">**FileSystemSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="745da-250">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="745da-251">Property</span><span class="sxs-lookup"><span data-stu-id="745da-251">Property</span></span> | <span data-ttu-id="745da-252">Description</span><span class="sxs-lookup"><span data-stu-id="745da-252">Description</span></span> | <span data-ttu-id="745da-253">Allowed values</span><span class="sxs-lookup"><span data-stu-id="745da-253">Allowed values</span></span> | <span data-ttu-id="745da-254">Required</span><span class="sxs-lookup"><span data-stu-id="745da-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="745da-255">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="745da-255">copyBehavior</span></span> |<span data-ttu-id="745da-256">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="745da-256">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="745da-257">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="745da-257">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="745da-258">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span><span class="sxs-lookup"><span data-stu-id="745da-258">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="745da-259">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="745da-259">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="745da-260">The target files are created with an autogenerated name.</span><span class="sxs-lookup"><span data-stu-id="745da-260">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="745da-261">**MergeFiles:** Merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="745da-261">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="745da-262">If the file name/blob name is specified, the merged file name is the specified name.</span><span class="sxs-lookup"><span data-stu-id="745da-262">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="745da-263">Otherwise, it is an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="745da-263">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="745da-264">No</span><span class="sxs-lookup"><span data-stu-id="745da-264">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="745da-265">recursive and copyBehavior examples</span><span class="sxs-lookup"><span data-stu-id="745da-265">recursive and copyBehavior examples</span></span>
<span data-ttu-id="745da-266">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span><span class="sxs-lookup"><span data-stu-id="745da-266">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="745da-267">recursive value</span><span class="sxs-lookup"><span data-stu-id="745da-267">recursive value</span></span> | <span data-ttu-id="745da-268">copyBehavior value</span><span class="sxs-lookup"><span data-stu-id="745da-268">copyBehavior value</span></span> | <span data-ttu-id="745da-269">Resulting behavior</span><span class="sxs-lookup"><span data-stu-id="745da-269">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="745da-270">true</span><span class="sxs-lookup"><span data-stu-id="745da-270">true</span></span> |<span data-ttu-id="745da-271">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="745da-271">preserveHierarchy</span></span> |<span data-ttu-id="745da-272">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="745da-272">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="745da-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-273">Folder1</span></span><br/><span data-ttu-id="745da-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="745da-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="745da-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="745da-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="745da-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="745da-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="745da-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="745da-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="745da-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="745da-280">the target folder Folder1 is created with the same structure as the source:</span><span class="sxs-lookup"><span data-stu-id="745da-280">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="745da-281">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-281">Folder1</span></span><br/><span data-ttu-id="745da-282">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-282">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-283">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-283">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="745da-284">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="745da-284">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="745da-285">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="745da-285">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="745da-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="745da-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="745da-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="745da-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="745da-288">true</span><span class="sxs-lookup"><span data-stu-id="745da-288">true</span></span> |<span data-ttu-id="745da-289">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="745da-289">flattenHierarchy</span></span> |<span data-ttu-id="745da-290">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="745da-290">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="745da-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-291">Folder1</span></span><br/><span data-ttu-id="745da-292">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-292">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-293">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-293">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="745da-294">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="745da-294">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="745da-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="745da-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="745da-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="745da-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="745da-297">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="745da-297">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="745da-298">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="745da-298">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="745da-299">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-299">Folder1</span></span><br/><span data-ttu-id="745da-300">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="745da-300">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="745da-301">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="745da-301">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="745da-302">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span><span class="sxs-lookup"><span data-stu-id="745da-302">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="745da-303">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span><span class="sxs-lookup"><span data-stu-id="745da-303">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="745da-304">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span><span class="sxs-lookup"><span data-stu-id="745da-304">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="745da-305">true</span><span class="sxs-lookup"><span data-stu-id="745da-305">true</span></span> |<span data-ttu-id="745da-306">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="745da-306">mergeFiles</span></span> |<span data-ttu-id="745da-307">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="745da-307">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="745da-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-308">Folder1</span></span><br/><span data-ttu-id="745da-309">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-309">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-310">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-310">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="745da-311">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="745da-311">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="745da-312">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="745da-312">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="745da-313">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="745da-313">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="745da-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="745da-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="745da-315">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="745da-315">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="745da-316">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-316">Folder1</span></span><br/><span data-ttu-id="745da-317">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="745da-317">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="745da-318">false</span><span class="sxs-lookup"><span data-stu-id="745da-318">false</span></span> |<span data-ttu-id="745da-319">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="745da-319">preserveHierarchy</span></span> |<span data-ttu-id="745da-320">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="745da-320">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="745da-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-321">Folder1</span></span><br/><span data-ttu-id="745da-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="745da-324">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="745da-324">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="745da-325">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="745da-325">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="745da-326">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="745da-326">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="745da-327">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="745da-327">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="745da-328">the target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="745da-328">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="745da-329">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-329">Folder1</span></span><br/><span data-ttu-id="745da-330">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-330">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-331">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-331">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="745da-332">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="745da-332">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="745da-333">false</span><span class="sxs-lookup"><span data-stu-id="745da-333">false</span></span> |<span data-ttu-id="745da-334">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="745da-334">flattenHierarchy</span></span> |<span data-ttu-id="745da-335">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="745da-335">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="745da-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-336">Folder1</span></span><br/><span data-ttu-id="745da-337">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-337">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-338">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-338">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="745da-339">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="745da-339">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="745da-340">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="745da-340">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="745da-341">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="745da-341">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="745da-342">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="745da-342">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="745da-343">the target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="745da-343">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="745da-344">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-344">Folder1</span></span><br/><span data-ttu-id="745da-345">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="745da-345">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="745da-346">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="745da-346">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="745da-347">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="745da-347">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="745da-348">false</span><span class="sxs-lookup"><span data-stu-id="745da-348">false</span></span> |<span data-ttu-id="745da-349">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="745da-349">mergeFiles</span></span> |<span data-ttu-id="745da-350">For a source folder Folder1 with the following structure,</span><span class="sxs-lookup"><span data-stu-id="745da-350">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="745da-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-351">Folder1</span></span><br/><span data-ttu-id="745da-352">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="745da-352">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="745da-353">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="745da-353">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="745da-354">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="745da-354">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="745da-355">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="745da-355">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="745da-356">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="745da-356">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="745da-357">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="745da-357">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="745da-358">the target folder Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="745da-358">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="745da-359">Folder1</span><span class="sxs-lookup"><span data-stu-id="745da-359">Folder1</span></span><br/><span data-ttu-id="745da-360">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="745da-360">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="745da-361">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="745da-361">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="745da-362">Subfolder1 with File3, File4, and File5 is not picked up.</span><span class="sxs-lookup"><span data-stu-id="745da-362">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="745da-363">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="745da-363">Supported file and compression formats</span></span>
<span data-ttu-id="745da-364">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span><span class="sxs-lookup"><span data-stu-id="745da-364">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="745da-365">JSON examples</span><span class="sxs-lookup"><span data-stu-id="745da-365">JSON examples</span></span>
<span data-ttu-id="745da-366">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="745da-366">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="745da-367">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="745da-367">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="745da-368">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="745da-368">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="745da-369">Example: Copy data from an on-premises file system to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="745da-369">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="745da-370">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="745da-370">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="745da-371">The sample has the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="745da-371">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="745da-372">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-372">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="745da-373">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-373">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="745da-374">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-374">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="745da-375">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-375">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="745da-376">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-376">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="745da-377">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span><span class="sxs-lookup"><span data-stu-id="745da-377">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="745da-378">The JSON properties that are used in these samples are described in the sections after the samples.</span><span class="sxs-lookup"><span data-stu-id="745da-378">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="745da-379">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="745da-379">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="745da-380">**On-Premises File Server linked service:**</span><span class="sxs-lookup"><span data-stu-id="745da-380">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="745da-381">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span><span class="sxs-lookup"><span data-stu-id="745da-381">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="745da-382">See [File Server linked service](#linked-service-properties) for details about this linked service.</span><span class="sxs-lookup"><span data-stu-id="745da-382">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="745da-383">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="745da-383">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="745da-384">**On-premises file system input dataset:**</span><span class="sxs-lookup"><span data-stu-id="745da-384">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="745da-385">Data is picked up from a new file every hour.</span><span class="sxs-lookup"><span data-stu-id="745da-385">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="745da-386">The folderPath and fileName properties are determined based on the start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="745da-386">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="745da-387">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="745da-387">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="745da-388">**Azure Blob storage output dataset:**</span><span class="sxs-lookup"><span data-stu-id="745da-388">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="745da-389">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="745da-389">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="745da-390">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="745da-390">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="745da-391">The folder path uses the year, month, day, and hour parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="745da-391">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="745da-392">**A copy activity in a pipeline with File System source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="745da-392">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="745da-393">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="745da-393">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="745da-394">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="745da-394">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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

## <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="745da-395">Example: Copy data from Azure SQL Database to an on-premises file system</span><span class="sxs-lookup"><span data-stu-id="745da-395">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="745da-396">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="745da-396">The following sample shows:</span></span>

* <span data-ttu-id="745da-397">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="745da-397">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="745da-398">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-398">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="745da-399">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-399">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="745da-400">An output dataset of type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-400">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="745da-401">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="745da-401">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="745da-402">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span><span class="sxs-lookup"><span data-stu-id="745da-402">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="745da-403">The JSON properties that are used in these samples are described in sections after the samples.</span><span class="sxs-lookup"><span data-stu-id="745da-403">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="745da-404">**Azure SQL Database linked service:**</span><span class="sxs-lookup"><span data-stu-id="745da-404">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="745da-405">**On-Premises File Server linked service:**</span><span class="sxs-lookup"><span data-stu-id="745da-405">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="745da-406">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span><span class="sxs-lookup"><span data-stu-id="745da-406">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="745da-407">See [File System linked service](#linked-service-properties) for details about this linked service.</span><span class="sxs-lookup"><span data-stu-id="745da-407">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="745da-408">**Azure SQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="745da-408">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="745da-409">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span><span class="sxs-lookup"><span data-stu-id="745da-409">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="745da-410">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="745da-410">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="745da-411">**On-premises file system output dataset:**</span><span class="sxs-lookup"><span data-stu-id="745da-411">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="745da-412">Data is copied to a new file every hour.</span><span class="sxs-lookup"><span data-stu-id="745da-412">Data is copied to a new file every hour.</span></span> <span data-ttu-id="745da-413">The folderPath and fileName for the blob are determined based on the start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="745da-413">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

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

<span data-ttu-id="745da-414">**A copy activity in a pipeline with SQL source and File System sink:**</span><span class="sxs-lookup"><span data-stu-id="745da-414">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="745da-415">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="745da-415">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="745da-416">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="745da-416">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="745da-417">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="745da-417">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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


<span data-ttu-id="745da-418">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span><span class="sxs-lookup"><span data-stu-id="745da-418">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="745da-419">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="745da-419">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="745da-420">Performance and tuning</span><span class="sxs-lookup"><span data-stu-id="745da-420">Performance and tuning</span></span>
 <span data-ttu-id="745da-421">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="745da-421">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
