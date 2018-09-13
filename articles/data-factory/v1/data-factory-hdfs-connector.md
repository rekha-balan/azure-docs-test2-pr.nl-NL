---
title: Move data from on-premises HDFS | Microsoft Docs
description: Learn about how to move data from on-premises HDFS using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: ac9ba682079f735aa2fdd416070c5d206d526ad4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965817"
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="c2f8c-103">Move data from on-premises HDFS using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c2f8c-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-hdfs-connector.md)
> * [Version 2 (current version)](../connector-hdfs.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [HDFS connector in V2](../connector-hdfs.md).

<span data-ttu-id="c2f8c-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span></span> <span data-ttu-id="c2f8c-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c2f8c-110">You can copy data from HDFS to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-110">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="c2f8c-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c2f8c-112">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-112">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

> [!NOTE]
> Copy Activity does not delete the source file after it is successfully copied to the destination. If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline. 

## <a name="enabling-connectivity"></a><span data-ttu-id="c2f8c-115">Enabling connectivity</span><span class="sxs-lookup"><span data-stu-id="c2f8c-115">Enabling connectivity</span></span>
<span data-ttu-id="c2f8c-116">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-116">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span></span> <span data-ttu-id="c2f8c-117">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-117">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="c2f8c-118">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-118">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> Make sure the Data Management Gateway can access to **ALL** the [name node server]:[name node port] and [data node servers]:[data node port] of the Hadoop cluster. Default [name node port] is 50070, and default [data node port] is 50075.

<span data-ttu-id="c2f8c-121">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-121">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="c2f8c-122">Having gateway on a separate machine reduces resource contention and improves performance.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-122">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="c2f8c-123">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-123">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c2f8c-124">Getting started</span><span class="sxs-lookup"><span data-stu-id="c2f8c-124">Getting started</span></span>
<span data-ttu-id="c2f8c-125">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-125">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="c2f8c-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c2f8c-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="c2f8c-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c2f8c-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="c2f8c-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c2f8c-131">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c2f8c-132">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-132">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="c2f8c-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="c2f8c-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c2f8c-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c2f8c-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="c2f8c-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c2f8c-138">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="c2f8c-138">Linked service properties</span></span>
<span data-ttu-id="c2f8c-139">A linked service links a data store to a data factory.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-139">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="c2f8c-140">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-140">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span></span> <span data-ttu-id="c2f8c-141">The following table provides description for JSON elements specific to HDFS linked service.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-141">The following table provides description for JSON elements specific to HDFS linked service.</span></span>

| <span data-ttu-id="c2f8c-142">Property</span><span class="sxs-lookup"><span data-stu-id="c2f8c-142">Property</span></span> | <span data-ttu-id="c2f8c-143">Description</span><span class="sxs-lookup"><span data-stu-id="c2f8c-143">Description</span></span> | <span data-ttu-id="c2f8c-144">Required</span><span class="sxs-lookup"><span data-stu-id="c2f8c-144">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2f8c-145">type</span><span class="sxs-lookup"><span data-stu-id="c2f8c-145">type</span></span> |<span data-ttu-id="c2f8c-146">The type property must be set to: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-146">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="c2f8c-147">Yes</span><span class="sxs-lookup"><span data-stu-id="c2f8c-147">Yes</span></span> |
| <span data-ttu-id="c2f8c-148">Url</span><span class="sxs-lookup"><span data-stu-id="c2f8c-148">Url</span></span> |<span data-ttu-id="c2f8c-149">URL to the HDFS</span><span class="sxs-lookup"><span data-stu-id="c2f8c-149">URL to the HDFS</span></span> |<span data-ttu-id="c2f8c-150">Yes</span><span class="sxs-lookup"><span data-stu-id="c2f8c-150">Yes</span></span> |
| <span data-ttu-id="c2f8c-151">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c2f8c-151">authenticationType</span></span> |<span data-ttu-id="c2f8c-152">Anonymous, or Windows.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-152">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="c2f8c-153">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-153">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="c2f8c-154">Yes</span><span class="sxs-lookup"><span data-stu-id="c2f8c-154">Yes</span></span> |
| <span data-ttu-id="c2f8c-155">userName</span><span class="sxs-lookup"><span data-stu-id="c2f8c-155">userName</span></span> |<span data-ttu-id="c2f8c-156">Username for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-156">Username for Windows authentication.</span></span> <span data-ttu-id="c2f8c-157">For Kerberos authentication, specify `<username>@<domain>.com`.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-157">For Kerberos authentication, specify `<username>@<domain>.com`.</span></span> |<span data-ttu-id="c2f8c-158">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="c2f8c-158">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="c2f8c-159">password</span><span class="sxs-lookup"><span data-stu-id="c2f8c-159">password</span></span> |<span data-ttu-id="c2f8c-160">Password for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-160">Password for Windows authentication.</span></span> |<span data-ttu-id="c2f8c-161">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="c2f8c-161">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="c2f8c-162">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c2f8c-162">gatewayName</span></span> |<span data-ttu-id="c2f8c-163">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-163">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="c2f8c-164">Yes</span><span class="sxs-lookup"><span data-stu-id="c2f8c-164">Yes</span></span> |
| <span data-ttu-id="c2f8c-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c2f8c-165">encryptedCredential</span></span> |<span data-ttu-id="c2f8c-166">[New-AzureRMDataFactoryEncryptValue](https://docs.microsoft.com/powershell/module/azurerm.datafactories/new-azurermdatafactoryencryptvalue) output of the access credential.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-166">[New-AzureRMDataFactoryEncryptValue](https://docs.microsoft.com/powershell/module/azurerm.datafactories/new-azurermdatafactoryencryptvalue) output of the access credential.</span></span> |<span data-ttu-id="c2f8c-167">No</span><span class="sxs-lookup"><span data-stu-id="c2f8c-167">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="c2f8c-168">Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="c2f8c-168">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="c2f8c-169">Using Windows authentication</span><span class="sxs-lookup"><span data-stu-id="c2f8c-169">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "<username>@<domain>.com (for Kerberos auth)",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="c2f8c-170">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="c2f8c-170">Dataset properties</span></span>
<span data-ttu-id="c2f8c-171">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-171">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c2f8c-172">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-172">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c2f8c-173">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-173">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c2f8c-174">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span><span class="sxs-lookup"><span data-stu-id="c2f8c-174">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span></span>

| <span data-ttu-id="c2f8c-175">Property</span><span class="sxs-lookup"><span data-stu-id="c2f8c-175">Property</span></span> | <span data-ttu-id="c2f8c-176">Description</span><span class="sxs-lookup"><span data-stu-id="c2f8c-176">Description</span></span> | <span data-ttu-id="c2f8c-177">Required</span><span class="sxs-lookup"><span data-stu-id="c2f8c-177">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2f8c-178">folderPath</span><span class="sxs-lookup"><span data-stu-id="c2f8c-178">folderPath</span></span> |<span data-ttu-id="c2f8c-179">Path to the folder.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-179">Path to the folder.</span></span> <span data-ttu-id="c2f8c-180">Example: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="c2f8c-180">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="c2f8c-181">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-181">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="c2f8c-182">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-182">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="c2f8c-183">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-183">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="c2f8c-184">Yes</span><span class="sxs-lookup"><span data-stu-id="c2f8c-184">Yes</span></span> |
| <span data-ttu-id="c2f8c-185">fileName</span><span class="sxs-lookup"><span data-stu-id="c2f8c-185">fileName</span></span> |<span data-ttu-id="c2f8c-186">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-186">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="c2f8c-187">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-187">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="c2f8c-188">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-188">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="c2f8c-189">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="c2f8c-189">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="c2f8c-190">No</span><span class="sxs-lookup"><span data-stu-id="c2f8c-190">No</span></span> |
| <span data-ttu-id="c2f8c-191">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c2f8c-191">partitionedBy</span></span> |<span data-ttu-id="c2f8c-192">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-192">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="c2f8c-193">Example: folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-193">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="c2f8c-194">No</span><span class="sxs-lookup"><span data-stu-id="c2f8c-194">No</span></span> |
| <span data-ttu-id="c2f8c-195">format</span><span class="sxs-lookup"><span data-stu-id="c2f8c-195">format</span></span> | <span data-ttu-id="c2f8c-196">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-196">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c2f8c-197">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-197">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="c2f8c-198">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-198">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="c2f8c-199">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-199">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c2f8c-200">No</span><span class="sxs-lookup"><span data-stu-id="c2f8c-200">No</span></span> |
| <span data-ttu-id="c2f8c-201">compression</span><span class="sxs-lookup"><span data-stu-id="c2f8c-201">compression</span></span> | <span data-ttu-id="c2f8c-202">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-202">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="c2f8c-203">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-203">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c2f8c-204">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-204">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c2f8c-205">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-205">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c2f8c-206">No</span><span class="sxs-lookup"><span data-stu-id="c2f8c-206">No</span></span> |

> [!NOTE]
> filename and fileFilter cannot be used simultaneously.

### <a name="using-partionedby-property"></a><span data-ttu-id="c2f8c-208">Using partionedBy property</span><span class="sxs-lookup"><span data-stu-id="c2f8c-208">Using partionedBy property</span></span>
<span data-ttu-id="c2f8c-209">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-209">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="c2f8c-210">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-210">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="c2f8c-211">Sample 1:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-211">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="c2f8c-212">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-212">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="c2f8c-213">The SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-213">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="c2f8c-214">The folderPath is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-214">The folderPath is different for each slice.</span></span> <span data-ttu-id="c2f8c-215">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-215">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="c2f8c-216">Sample 2:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-216">Sample 2:</span></span>

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
<span data-ttu-id="c2f8c-217">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-217">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c2f8c-218">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="c2f8c-218">Copy activity properties</span></span>
<span data-ttu-id="c2f8c-219">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-219">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c2f8c-220">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-220">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="c2f8c-221">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-221">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="c2f8c-222">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-222">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c2f8c-223">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-223">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span></span>

<span data-ttu-id="c2f8c-224">**FileSystemSource** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-224">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="c2f8c-225">Property</span><span class="sxs-lookup"><span data-stu-id="c2f8c-225">Property</span></span> | <span data-ttu-id="c2f8c-226">Description</span><span class="sxs-lookup"><span data-stu-id="c2f8c-226">Description</span></span> | <span data-ttu-id="c2f8c-227">Allowed values</span><span class="sxs-lookup"><span data-stu-id="c2f8c-227">Allowed values</span></span> | <span data-ttu-id="c2f8c-228">Required</span><span class="sxs-lookup"><span data-stu-id="c2f8c-228">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c2f8c-229">recursive</span><span class="sxs-lookup"><span data-stu-id="c2f8c-229">recursive</span></span> |<span data-ttu-id="c2f8c-230">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-230">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="c2f8c-231">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="c2f8c-231">True, False (default)</span></span> |<span data-ttu-id="c2f8c-232">No</span><span class="sxs-lookup"><span data-stu-id="c2f8c-232">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="c2f8c-233">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="c2f8c-233">Supported file and compression formats</span></span>
<span data-ttu-id="c2f8c-234">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-234">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-to-azure-blob"></a><span data-ttu-id="c2f8c-235">JSON example: Copy data from on-premises HDFS to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="c2f8c-235">JSON example: Copy data from on-premises HDFS to Azure Blob</span></span>
<span data-ttu-id="c2f8c-236">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-236">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span></span> <span data-ttu-id="c2f8c-237">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-237">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="c2f8c-238">The sample provides JSON definitions for the following Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-238">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="c2f8c-239">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-239">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="c2f8c-240">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-240">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="c2f8c-241">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-241">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c2f8c-242">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-242">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="c2f8c-243">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-243">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c2f8c-244">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-244">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c2f8c-245">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-245">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span></span> <span data-ttu-id="c2f8c-246">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-246">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c2f8c-247">As a first step, set up the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-247">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="c2f8c-248">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-248">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c2f8c-249">**HDFS linked service:** This example uses the Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-249">**HDFS linked service:** This example uses the Windows authentication.</span></span> <span data-ttu-id="c2f8c-250">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-250">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="c2f8c-251">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-251">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="c2f8c-252">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-252">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="c2f8c-253">The pipeline copies all the files in this folder to the destination.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-253">The pipeline copies all the files in this folder to the destination.</span></span>

<span data-ttu-id="c2f8c-254">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-254">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="c2f8c-255">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-255">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c2f8c-256">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c2f8c-256">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c2f8c-257">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-257">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c2f8c-258">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-258">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c2f8c-259">**A copy activity in a pipeline with File System source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-259">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="c2f8c-260">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-260">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c2f8c-261">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-261">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c2f8c-262">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-262">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="c2f8c-263">Use Kerberos authentication for HDFS connector</span><span class="sxs-lookup"><span data-stu-id="c2f8c-263">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="c2f8c-264">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-264">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="c2f8c-265">You can choose the one better fits your case.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-265">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="c2f8c-266">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="c2f8c-266">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="c2f8c-267">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="c2f8c-267">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <a name="kerberos-join-realm"></a><span data-ttu-id="c2f8c-268">Option 1: Join gateway machine in Kerberos realm</span><span class="sxs-lookup"><span data-stu-id="c2f8c-268">Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="c2f8c-269">Requirement:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-269">Requirement:</span></span>

* <span data-ttu-id="c2f8c-270">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-270">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="c2f8c-271">How to configure:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-271">How to configure:</span></span>

<span data-ttu-id="c2f8c-272">**On gateway machine:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-272">**On gateway machine:**</span></span>

1.  <span data-ttu-id="c2f8c-273">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-273">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="c2f8c-274">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-274">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="c2f8c-275">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-275">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="c2f8c-276">Replace *REALM.COM* with your own respective realm as needed.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-276">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="c2f8c-277">**Restart** the machine after executing these 2 commands.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-277">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="c2f8c-278">Verify the configuration with **Ksetup** command.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-278">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="c2f8c-279">The output should be like:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-279">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="c2f8c-280">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-280">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="c2f8c-281">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-281">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="c2f8c-282">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-282">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <a name="kerberos-mutual-trust"></a><span data-ttu-id="c2f8c-283">Option 2: Enable mutual trust between Windows domain and Kerberos realm</span><span class="sxs-lookup"><span data-stu-id="c2f8c-283">Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="c2f8c-284">Requirement:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-284">Requirement:</span></span>
*   <span data-ttu-id="c2f8c-285">The gateway machine must join a Windows domain.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-285">The gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="c2f8c-286">You need permission to update the domain controller's settings.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-286">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="c2f8c-287">How to configure:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-287">How to configure:</span></span>

> [!NOTE]
> Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.

<span data-ttu-id="c2f8c-289">**On KDC server:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-289">**On KDC server:**</span></span>

1.  <span data-ttu-id="c2f8c-290">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-290">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="c2f8c-291">By default, the configuration is located at **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-291">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="c2f8c-292">**Restart** the KDC service after configuration.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-292">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="c2f8c-293">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-293">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="c2f8c-294">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-294">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="c2f8c-295">**On domain controller:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-295">**On domain controller:**</span></span>

1.  <span data-ttu-id="c2f8c-296">Run the following **Ksetup** commands to add a realm entry:</span><span class="sxs-lookup"><span data-stu-id="c2f8c-296">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="c2f8c-297">Establish trust from Windows Domain to Kerberos Realm.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-297">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="c2f8c-298">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-298">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="c2f8c-299">Select encryption algorithm used in Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-299">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="c2f8c-300">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-300">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="c2f8c-301">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-301">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="c2f8c-302">Select the encryption algorithm you want to use when connect to KDC.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-302">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="c2f8c-303">Commonly, you can simply select all the options.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-303">Commonly, you can simply select all the options.</span></span>

        ![Config Encryption Types for Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="c2f8c-305">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-305">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="c2f8c-306">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-306">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="c2f8c-307">Start the Administrative tools > **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-307">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="c2f8c-308">Configure advanced features by clicking **View** > **Advanced Features**.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-308">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="c2f8c-309">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-309">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="c2f8c-310">Add a principal from the realm.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-310">Add a principal from the realm.</span></span>

        ![Map Security Identity](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="c2f8c-312">**On gateway machine:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-312">**On gateway machine:**</span></span>

* <span data-ttu-id="c2f8c-313">Run the following **Ksetup** commands to add a realm entry.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-313">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="c2f8c-314">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="c2f8c-314">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="c2f8c-315">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-315">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="c2f8c-316">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-316">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a><span data-ttu-id="c2f8c-318">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="c2f8c-318">Performance and Tuning</span></span>
<span data-ttu-id="c2f8c-319">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="c2f8c-319">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
