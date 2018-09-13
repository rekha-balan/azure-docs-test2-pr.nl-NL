---
title: Move data from an FTP server by using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from an FTP server using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/02/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: bbbbaab6090941141abd7a2bbd2eac6dbf9fd354
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966020"
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="c91ea-103">Move data from an FTP server by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c91ea-103">Move data from an FTP server by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-ftp-connector.md)
> * [Version 2 (current version)](../connector-ftp.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [FTP connector in V2](../connector-ftp.md).

<span data-ttu-id="c91ea-108">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-108">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="c91ea-109">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="c91ea-109">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c91ea-110">You can copy data from an FTP server to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="c91ea-110">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="c91ea-111">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="c91ea-111">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c91ea-112">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-112">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="c91ea-113">It supports both on-premises and cloud FTP servers.</span><span class="sxs-lookup"><span data-stu-id="c91ea-113">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> The copy activity does not delete the source file after it is successfully copied to the destination. If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline. 

## <a name="enable-connectivity"></a><span data-ttu-id="c91ea-116">Enable connectivity</span><span class="sxs-lookup"><span data-stu-id="c91ea-116">Enable connectivity</span></span>
<span data-ttu-id="c91ea-117">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="c91ea-117">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="c91ea-118">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="c91ea-118">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="c91ea-119">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-119">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="c91ea-120">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-120">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="c91ea-121">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="c91ea-121">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="c91ea-122">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-122">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="c91ea-123">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span><span class="sxs-lookup"><span data-stu-id="c91ea-123">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="c91ea-124">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-124">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="c91ea-125">Get started</span><span class="sxs-lookup"><span data-stu-id="c91ea-125">Get started</span></span>
<span data-ttu-id="c91ea-126">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span><span class="sxs-lookup"><span data-stu-id="c91ea-126">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="c91ea-127">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-127">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="c91ea-128">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span><span class="sxs-lookup"><span data-stu-id="c91ea-128">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="c91ea-129">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-129">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c91ea-130">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="c91ea-130">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="c91ea-131">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="c91ea-131">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c91ea-132">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="c91ea-132">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c91ea-133">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="c91ea-133">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="c91ea-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="c91ea-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="c91ea-135">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="c91ea-135">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c91ea-136">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="c91ea-136">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="c91ea-137">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="c91ea-137">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

<span data-ttu-id="c91ea-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span><span class="sxs-lookup"><span data-stu-id="c91ea-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c91ea-140">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="c91ea-140">Linked service properties</span></span>
<span data-ttu-id="c91ea-141">The following table describes JSON elements specific to an FTP linked service.</span><span class="sxs-lookup"><span data-stu-id="c91ea-141">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="c91ea-142">Property</span><span class="sxs-lookup"><span data-stu-id="c91ea-142">Property</span></span> | <span data-ttu-id="c91ea-143">Description</span><span class="sxs-lookup"><span data-stu-id="c91ea-143">Description</span></span> | <span data-ttu-id="c91ea-144">Required</span><span class="sxs-lookup"><span data-stu-id="c91ea-144">Required</span></span> | <span data-ttu-id="c91ea-145">Default</span><span class="sxs-lookup"><span data-stu-id="c91ea-145">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c91ea-146">type</span><span class="sxs-lookup"><span data-stu-id="c91ea-146">type</span></span> |<span data-ttu-id="c91ea-147">Set this to FtpServer.</span><span class="sxs-lookup"><span data-stu-id="c91ea-147">Set this to FtpServer.</span></span> |<span data-ttu-id="c91ea-148">Yes</span><span class="sxs-lookup"><span data-stu-id="c91ea-148">Yes</span></span> |&nbsp; |
| <span data-ttu-id="c91ea-149">host</span><span class="sxs-lookup"><span data-stu-id="c91ea-149">host</span></span> |<span data-ttu-id="c91ea-150">Specify the name or IP address of the FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-150">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="c91ea-151">Yes</span><span class="sxs-lookup"><span data-stu-id="c91ea-151">Yes</span></span> |&nbsp; |
| <span data-ttu-id="c91ea-152">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c91ea-152">authenticationType</span></span> |<span data-ttu-id="c91ea-153">Specify the authentication type.</span><span class="sxs-lookup"><span data-stu-id="c91ea-153">Specify the authentication type.</span></span> |<span data-ttu-id="c91ea-154">Yes</span><span class="sxs-lookup"><span data-stu-id="c91ea-154">Yes</span></span> |<span data-ttu-id="c91ea-155">Basic, Anonymous</span><span class="sxs-lookup"><span data-stu-id="c91ea-155">Basic, Anonymous</span></span> |
| <span data-ttu-id="c91ea-156">username</span><span class="sxs-lookup"><span data-stu-id="c91ea-156">username</span></span> |<span data-ttu-id="c91ea-157">Specify the user who has access to the FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-157">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="c91ea-158">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-158">No</span></span> |&nbsp; |
| <span data-ttu-id="c91ea-159">password</span><span class="sxs-lookup"><span data-stu-id="c91ea-159">password</span></span> |<span data-ttu-id="c91ea-160">Specify the password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="c91ea-160">Specify the password for the user (username).</span></span> |<span data-ttu-id="c91ea-161">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-161">No</span></span> |&nbsp; |
| <span data-ttu-id="c91ea-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c91ea-162">encryptedCredential</span></span> |<span data-ttu-id="c91ea-163">Specify the encrypted credential to access the FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-163">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="c91ea-164">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-164">No</span></span> |&nbsp; |
| <span data-ttu-id="c91ea-165">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c91ea-165">gatewayName</span></span> |<span data-ttu-id="c91ea-166">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span><span class="sxs-lookup"><span data-stu-id="c91ea-166">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="c91ea-167">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-167">No</span></span> |&nbsp; |
| <span data-ttu-id="c91ea-168">port</span><span class="sxs-lookup"><span data-stu-id="c91ea-168">port</span></span> |<span data-ttu-id="c91ea-169">Specify the port on which the FTP server is listening.</span><span class="sxs-lookup"><span data-stu-id="c91ea-169">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="c91ea-170">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-170">No</span></span> |<span data-ttu-id="c91ea-171">21</span><span class="sxs-lookup"><span data-stu-id="c91ea-171">21</span></span> |
| <span data-ttu-id="c91ea-172">enableSsl</span><span class="sxs-lookup"><span data-stu-id="c91ea-172">enableSsl</span></span> |<span data-ttu-id="c91ea-173">Specify whether to use FTP over an SSL/TLS channel.</span><span class="sxs-lookup"><span data-stu-id="c91ea-173">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="c91ea-174">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-174">No</span></span> |<span data-ttu-id="c91ea-175">true</span><span class="sxs-lookup"><span data-stu-id="c91ea-175">true</span></span> |
| <span data-ttu-id="c91ea-176">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="c91ea-176">enableServerCertificateValidation</span></span> |<span data-ttu-id="c91ea-177">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span><span class="sxs-lookup"><span data-stu-id="c91ea-177">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="c91ea-178">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-178">No</span></span> |<span data-ttu-id="c91ea-179">true</span><span class="sxs-lookup"><span data-stu-id="c91ea-179">true</span></span> |

>[!NOTE]
>The FTP connector supports accessing FTP server with either no encryption or explicit SSL/TLS encryption; it doesn’t support implicit SSL/TLS encryption.

### <a name="use-anonymous-authentication"></a><span data-ttu-id="c91ea-181">Use Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="c91ea-181">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="c91ea-182">Use username and password in plain text for basic authentication</span><span class="sxs-lookup"><span data-stu-id="c91ea-182">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="c91ea-183">Use port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="c91ea-183">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="c91ea-184">Use encryptedCredential for authentication and gateway</span><span class="sxs-lookup"><span data-stu-id="c91ea-184">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c91ea-185">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="c91ea-185">Dataset properties</span></span>
<span data-ttu-id="c91ea-186">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-186">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="c91ea-187">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="c91ea-187">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="c91ea-188">The **typeProperties** section is different for each type of dataset.</span><span class="sxs-lookup"><span data-stu-id="c91ea-188">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="c91ea-189">It provides information that is specific to the dataset type.</span><span class="sxs-lookup"><span data-stu-id="c91ea-189">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="c91ea-190">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="c91ea-190">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="c91ea-191">Property</span><span class="sxs-lookup"><span data-stu-id="c91ea-191">Property</span></span> | <span data-ttu-id="c91ea-192">Description</span><span class="sxs-lookup"><span data-stu-id="c91ea-192">Description</span></span> | <span data-ttu-id="c91ea-193">Required</span><span class="sxs-lookup"><span data-stu-id="c91ea-193">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c91ea-194">folderPath</span><span class="sxs-lookup"><span data-stu-id="c91ea-194">folderPath</span></span> |<span data-ttu-id="c91ea-195">Subpath to the folder.</span><span class="sxs-lookup"><span data-stu-id="c91ea-195">Subpath to the folder.</span></span> <span data-ttu-id="c91ea-196">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="c91ea-196">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="c91ea-197">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="c91ea-197">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="c91ea-198">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span><span class="sxs-lookup"><span data-stu-id="c91ea-198">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="c91ea-199">Yes</span><span class="sxs-lookup"><span data-stu-id="c91ea-199">Yes</span></span> |
| <span data-ttu-id="c91ea-200">fileName</span><span class="sxs-lookup"><span data-stu-id="c91ea-200">fileName</span></span> |<span data-ttu-id="c91ea-201">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="c91ea-201">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="c91ea-202">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="c91ea-202">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="c91ea-203">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="c91ea-203">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="c91ea-204">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="c91ea-204">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="c91ea-205">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-205">No</span></span> |
| <span data-ttu-id="c91ea-206">fileFilter</span><span class="sxs-lookup"><span data-stu-id="c91ea-206">fileFilter</span></span> |<span data-ttu-id="c91ea-207">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span><span class="sxs-lookup"><span data-stu-id="c91ea-207">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="c91ea-208">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="c91ea-208">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="c91ea-209">Example 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="c91ea-209">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="c91ea-210">Example 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="c91ea-210">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="c91ea-211">**fileFilter** is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="c91ea-211">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="c91ea-212">This property is not supported with Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="c91ea-212">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="c91ea-213">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-213">No</span></span> |
| <span data-ttu-id="c91ea-214">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c91ea-214">partitionedBy</span></span> |<span data-ttu-id="c91ea-215">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span><span class="sxs-lookup"><span data-stu-id="c91ea-215">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="c91ea-216">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="c91ea-216">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="c91ea-217">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-217">No</span></span> |
| <span data-ttu-id="c91ea-218">format</span><span class="sxs-lookup"><span data-stu-id="c91ea-218">format</span></span> | <span data-ttu-id="c91ea-219">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-219">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c91ea-220">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="c91ea-220">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="c91ea-221">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="c91ea-221">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="c91ea-222">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="c91ea-222">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c91ea-223">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-223">No</span></span> |
| <span data-ttu-id="c91ea-224">compression</span><span class="sxs-lookup"><span data-stu-id="c91ea-224">compression</span></span> | <span data-ttu-id="c91ea-225">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="c91ea-225">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="c91ea-226">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-226">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c91ea-227">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c91ea-227">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c91ea-228">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-228">No</span></span> |
| <span data-ttu-id="c91ea-229">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="c91ea-229">useBinaryTransfer</span></span> |<span data-ttu-id="c91ea-230">Specify whether to use the binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="c91ea-230">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="c91ea-231">The values are true for binary mode (this is the default value), and false for ASCII.</span><span class="sxs-lookup"><span data-stu-id="c91ea-231">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="c91ea-232">This property can only be used when the associated linked service type is of type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="c91ea-232">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="c91ea-233">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-233">No</span></span> |

> [!NOTE]
> **fileName** and **fileFilter** cannot be used simultaneously.

### <a name="use-the-partionedby-property"></a><span data-ttu-id="c91ea-235">Use the partionedBy property</span><span class="sxs-lookup"><span data-stu-id="c91ea-235">Use the partionedBy property</span></span>
<span data-ttu-id="c91ea-236">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span><span class="sxs-lookup"><span data-stu-id="c91ea-236">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="c91ea-237">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-237">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="c91ea-238">Sample 1</span><span class="sxs-lookup"><span data-stu-id="c91ea-238">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="c91ea-239">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="c91ea-239">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="c91ea-240">The SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="c91ea-240">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="c91ea-241">The folder path is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="c91ea-241">The folder path is different for each slice.</span></span> <span data-ttu-id="c91ea-242">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="c91ea-242">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="c91ea-243">Sample 2</span><span class="sxs-lookup"><span data-stu-id="c91ea-243">Sample 2</span></span>

```json
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
<span data-ttu-id="c91ea-244">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span><span class="sxs-lookup"><span data-stu-id="c91ea-244">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c91ea-245">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="c91ea-245">Copy activity properties</span></span>
<span data-ttu-id="c91ea-246">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-246">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="c91ea-247">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="c91ea-247">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="c91ea-248">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="c91ea-248">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="c91ea-249">For the copy activity, the type properties vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="c91ea-249">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c91ea-250">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="c91ea-250">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="c91ea-251">Property</span><span class="sxs-lookup"><span data-stu-id="c91ea-251">Property</span></span> | <span data-ttu-id="c91ea-252">Description</span><span class="sxs-lookup"><span data-stu-id="c91ea-252">Description</span></span> | <span data-ttu-id="c91ea-253">Allowed values</span><span class="sxs-lookup"><span data-stu-id="c91ea-253">Allowed values</span></span> | <span data-ttu-id="c91ea-254">Required</span><span class="sxs-lookup"><span data-stu-id="c91ea-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c91ea-255">recursive</span><span class="sxs-lookup"><span data-stu-id="c91ea-255">recursive</span></span> |<span data-ttu-id="c91ea-256">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="c91ea-256">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="c91ea-257">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="c91ea-257">True, False (default)</span></span> |<span data-ttu-id="c91ea-258">No</span><span class="sxs-lookup"><span data-stu-id="c91ea-258">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="c91ea-259">JSON example: Copy data from FTP server to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="c91ea-259">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="c91ea-260">This sample shows how to copy data from an FTP server to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="c91ea-260">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="c91ea-261">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c91ea-261">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="c91ea-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="c91ea-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="c91ea-263">A linked service of type [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c91ea-263">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="c91ea-264">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c91ea-264">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="c91ea-265">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c91ea-265">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="c91ea-266">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c91ea-266">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="c91ea-267">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="c91ea-267">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="c91ea-268">The sample copies data from an FTP server to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="c91ea-268">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="c91ea-269">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="c91ea-269">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="c91ea-270">FTP linked service</span><span class="sxs-lookup"><span data-stu-id="c91ea-270">FTP linked service</span></span>

<span data-ttu-id="c91ea-271">This example uses basic authentication, with the user name and password in plain text.</span><span class="sxs-lookup"><span data-stu-id="c91ea-271">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="c91ea-272">You can also use one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="c91ea-272">You can also use one of the following ways:</span></span>

* <span data-ttu-id="c91ea-273">Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="c91ea-273">Anonymous authentication</span></span>
* <span data-ttu-id="c91ea-274">Basic authentication with encrypted credentials</span><span class="sxs-lookup"><span data-stu-id="c91ea-274">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="c91ea-275">FTP over SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="c91ea-275">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="c91ea-276">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="c91ea-276">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="c91ea-277">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="c91ea-277">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="c91ea-278">FTP input dataset</span><span class="sxs-lookup"><span data-stu-id="c91ea-278">FTP input dataset</span></span>

<span data-ttu-id="c91ea-279">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="c91ea-279">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="c91ea-280">The pipeline copies the file to the destination.</span><span class="sxs-lookup"><span data-stu-id="c91ea-280">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="c91ea-281">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="c91ea-281">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c91ea-282">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="c91ea-282">Azure Blob output dataset</span></span>

<span data-ttu-id="c91ea-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c91ea-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c91ea-284">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="c91ea-284">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c91ea-285">The folder path uses the year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="c91ea-285">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="c91ea-286">A copy activity in a pipeline with file system source and blob sink</span><span class="sxs-lookup"><span data-stu-id="c91ea-286">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="c91ea-287">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="c91ea-287">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="c91ea-288">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-288">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).

## <a name="next-steps"></a><span data-ttu-id="c91ea-290">Next steps</span><span class="sxs-lookup"><span data-stu-id="c91ea-290">Next steps</span></span>
<span data-ttu-id="c91ea-291">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="c91ea-291">See the following articles:</span></span>

* <span data-ttu-id="c91ea-292">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-292">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="c91ea-293">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-293">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
