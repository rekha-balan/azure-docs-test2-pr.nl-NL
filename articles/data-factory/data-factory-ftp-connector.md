---
title: Move data from an FTP server by using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from an FTP server using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: spelluru
ms.openlocfilehash: 1c37802e2b908747773afa093a28ea218dd60509
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554552"
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="1b79a-103">Move data from an FTP server by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b79a-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="1b79a-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="1b79a-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1b79a-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="1b79a-106">You can copy data from an FTP server to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="1b79a-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="1b79a-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="1b79a-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1b79a-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="1b79a-109">It supports both on-premises and cloud FTP servers.</span><span class="sxs-lookup"><span data-stu-id="1b79a-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="1b79a-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="1b79a-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="1b79a-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="1b79a-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="1b79a-112">Enable connectivity</span><span class="sxs-lookup"><span data-stu-id="1b79a-112">Enable connectivity</span></span>
<span data-ttu-id="1b79a-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="1b79a-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="1b79a-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="1b79a-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="1b79a-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="1b79a-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="1b79a-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="1b79a-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="1b79a-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="1b79a-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span><span class="sxs-lookup"><span data-stu-id="1b79a-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="1b79a-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="1b79a-121">Get started</span><span class="sxs-lookup"><span data-stu-id="1b79a-121">Get started</span></span>
<span data-ttu-id="1b79a-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span><span class="sxs-lookup"><span data-stu-id="1b79a-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="1b79a-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="1b79a-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="1b79a-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span><span class="sxs-lookup"><span data-stu-id="1b79a-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="1b79a-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="1b79a-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1b79a-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="1b79a-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="1b79a-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="1b79a-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="1b79a-128">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="1b79a-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="1b79a-129">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="1b79a-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="1b79a-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="1b79a-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="1b79a-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="1b79a-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1b79a-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="1b79a-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="1b79a-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="1b79a-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="1b79a-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="1b79a-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span><span class="sxs-lookup"><span data-stu-id="1b79a-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1b79a-136">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="1b79a-136">Linked service properties</span></span>
<span data-ttu-id="1b79a-137">The following table describes JSON elements specific to an FTP linked service.</span><span class="sxs-lookup"><span data-stu-id="1b79a-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="1b79a-138">Property</span><span class="sxs-lookup"><span data-stu-id="1b79a-138">Property</span></span> | <span data-ttu-id="1b79a-139">Description</span><span class="sxs-lookup"><span data-stu-id="1b79a-139">Description</span></span> | <span data-ttu-id="1b79a-140">Required</span><span class="sxs-lookup"><span data-stu-id="1b79a-140">Required</span></span> | <span data-ttu-id="1b79a-141">Default</span><span class="sxs-lookup"><span data-stu-id="1b79a-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b79a-142">type</span><span class="sxs-lookup"><span data-stu-id="1b79a-142">type</span></span> |<span data-ttu-id="1b79a-143">Set this to FtpServer.</span><span class="sxs-lookup"><span data-stu-id="1b79a-143">Set this to FtpServer.</span></span> |<span data-ttu-id="1b79a-144">Yes</span><span class="sxs-lookup"><span data-stu-id="1b79a-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="1b79a-145">host</span><span class="sxs-lookup"><span data-stu-id="1b79a-145">host</span></span> |<span data-ttu-id="1b79a-146">Specify the name or IP address of the FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="1b79a-147">Yes</span><span class="sxs-lookup"><span data-stu-id="1b79a-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="1b79a-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1b79a-148">authenticationType</span></span> |<span data-ttu-id="1b79a-149">Specify the authentication type.</span><span class="sxs-lookup"><span data-stu-id="1b79a-149">Specify the authentication type.</span></span> |<span data-ttu-id="1b79a-150">Yes</span><span class="sxs-lookup"><span data-stu-id="1b79a-150">Yes</span></span> |<span data-ttu-id="1b79a-151">Basic, Anonymous</span><span class="sxs-lookup"><span data-stu-id="1b79a-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="1b79a-152">username</span><span class="sxs-lookup"><span data-stu-id="1b79a-152">username</span></span> |<span data-ttu-id="1b79a-153">Specify the user who has access to the FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="1b79a-154">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-154">No</span></span> |&nbsp; |
| <span data-ttu-id="1b79a-155">password</span><span class="sxs-lookup"><span data-stu-id="1b79a-155">password</span></span> |<span data-ttu-id="1b79a-156">Specify the password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="1b79a-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="1b79a-157">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-157">No</span></span> |&nbsp; |
| <span data-ttu-id="1b79a-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1b79a-158">encryptedCredential</span></span> |<span data-ttu-id="1b79a-159">Specify the encrypted credential to access the FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="1b79a-160">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-160">No</span></span> |&nbsp; |
| <span data-ttu-id="1b79a-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1b79a-161">gatewayName</span></span> |<span data-ttu-id="1b79a-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span><span class="sxs-lookup"><span data-stu-id="1b79a-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="1b79a-163">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-163">No</span></span> |&nbsp; |
| <span data-ttu-id="1b79a-164">port</span><span class="sxs-lookup"><span data-stu-id="1b79a-164">port</span></span> |<span data-ttu-id="1b79a-165">Specify the port on which the FTP server is listening.</span><span class="sxs-lookup"><span data-stu-id="1b79a-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="1b79a-166">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-166">No</span></span> |<span data-ttu-id="1b79a-167">21</span><span class="sxs-lookup"><span data-stu-id="1b79a-167">21</span></span> |
| <span data-ttu-id="1b79a-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="1b79a-168">enableSsl</span></span> |<span data-ttu-id="1b79a-169">Specify whether to use FTP over an SSL/TLS channel.</span><span class="sxs-lookup"><span data-stu-id="1b79a-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="1b79a-170">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-170">No</span></span> |<span data-ttu-id="1b79a-171">true</span><span class="sxs-lookup"><span data-stu-id="1b79a-171">true</span></span> |
| <span data-ttu-id="1b79a-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1b79a-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="1b79a-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span><span class="sxs-lookup"><span data-stu-id="1b79a-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="1b79a-174">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-174">No</span></span> |<span data-ttu-id="1b79a-175">true</span><span class="sxs-lookup"><span data-stu-id="1b79a-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="1b79a-176">Use Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="1b79a-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="1b79a-177">Use username and password in plain text for basic authentication</span><span class="sxs-lookup"><span data-stu-id="1b79a-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="1b79a-178">Use port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1b79a-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="1b79a-179">Use encryptedCredential for authentication and gateway</span><span class="sxs-lookup"><span data-stu-id="1b79a-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="1b79a-180">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="1b79a-180">Dataset properties</span></span>
<span data-ttu-id="1b79a-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="1b79a-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="1b79a-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="1b79a-183">The **typeProperties** section is different for each type of dataset.</span><span class="sxs-lookup"><span data-stu-id="1b79a-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="1b79a-184">It provides information that is specific to the dataset type.</span><span class="sxs-lookup"><span data-stu-id="1b79a-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="1b79a-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="1b79a-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="1b79a-186">Property</span><span class="sxs-lookup"><span data-stu-id="1b79a-186">Property</span></span> | <span data-ttu-id="1b79a-187">Description</span><span class="sxs-lookup"><span data-stu-id="1b79a-187">Description</span></span> | <span data-ttu-id="1b79a-188">Required</span><span class="sxs-lookup"><span data-stu-id="1b79a-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b79a-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="1b79a-189">folderPath</span></span> |<span data-ttu-id="1b79a-190">Subpath to the folder.</span><span class="sxs-lookup"><span data-stu-id="1b79a-190">Subpath to the folder.</span></span> <span data-ttu-id="1b79a-191">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="1b79a-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="1b79a-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="1b79a-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="1b79a-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span><span class="sxs-lookup"><span data-stu-id="1b79a-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="1b79a-194">Yes</span><span class="sxs-lookup"><span data-stu-id="1b79a-194">Yes</span></span> |
| <span data-ttu-id="1b79a-195">fileName</span><span class="sxs-lookup"><span data-stu-id="1b79a-195">fileName</span></span> |<span data-ttu-id="1b79a-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="1b79a-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="1b79a-197">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="1b79a-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="1b79a-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="1b79a-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="1b79a-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="1b79a-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="1b79a-200">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-200">No</span></span> |
| <span data-ttu-id="1b79a-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="1b79a-201">fileFilter</span></span> |<span data-ttu-id="1b79a-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span><span class="sxs-lookup"><span data-stu-id="1b79a-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="1b79a-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="1b79a-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="1b79a-204">Example 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="1b79a-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="1b79a-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="1b79a-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="1b79a-206">**fileFilter** is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="1b79a-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="1b79a-207">This property is not supported with Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="1b79a-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="1b79a-208">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-208">No</span></span> |
| <span data-ttu-id="1b79a-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1b79a-209">partitionedBy</span></span> |<span data-ttu-id="1b79a-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span><span class="sxs-lookup"><span data-stu-id="1b79a-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="1b79a-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="1b79a-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="1b79a-212">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-212">No</span></span> |
| <span data-ttu-id="1b79a-213">format</span><span class="sxs-lookup"><span data-stu-id="1b79a-213">format</span></span> | <span data-ttu-id="1b79a-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1b79a-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1b79a-215">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="1b79a-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1b79a-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="1b79a-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1b79a-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="1b79a-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1b79a-218">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-218">No</span></span> |
| <span data-ttu-id="1b79a-219">compression</span><span class="sxs-lookup"><span data-stu-id="1b79a-219">compression</span></span> | <span data-ttu-id="1b79a-220">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="1b79a-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1b79a-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1b79a-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1b79a-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1b79a-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1b79a-223">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-223">No</span></span> |
| <span data-ttu-id="1b79a-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="1b79a-224">useBinaryTransfer</span></span> |<span data-ttu-id="1b79a-225">Specify whether to use the binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="1b79a-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="1b79a-226">The values are true for binary mode (this is the default value), and false for ASCII.</span><span class="sxs-lookup"><span data-stu-id="1b79a-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="1b79a-227">This property can only be used when the associated linked service type is of type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="1b79a-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="1b79a-228">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1b79a-229">**fileName** and **fileFilter** cannot be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="1b79a-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="1b79a-230">Use the partionedBy property</span><span class="sxs-lookup"><span data-stu-id="1b79a-230">Use the partionedBy property</span></span>
<span data-ttu-id="1b79a-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span><span class="sxs-lookup"><span data-stu-id="1b79a-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="1b79a-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="1b79a-233">Sample 1</span><span class="sxs-lookup"><span data-stu-id="1b79a-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="1b79a-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="1b79a-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="1b79a-235">The SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="1b79a-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="1b79a-236">The folder path is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="1b79a-236">The folder path is different for each slice.</span></span> <span data-ttu-id="1b79a-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="1b79a-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="1b79a-238">Sample 2</span><span class="sxs-lookup"><span data-stu-id="1b79a-238">Sample 2</span></span>

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
<span data-ttu-id="1b79a-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span><span class="sxs-lookup"><span data-stu-id="1b79a-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="1b79a-240">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="1b79a-240">Copy activity properties</span></span>
<span data-ttu-id="1b79a-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="1b79a-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="1b79a-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="1b79a-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="1b79a-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="1b79a-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="1b79a-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1b79a-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="1b79a-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="1b79a-246">Property</span><span class="sxs-lookup"><span data-stu-id="1b79a-246">Property</span></span> | <span data-ttu-id="1b79a-247">Description</span><span class="sxs-lookup"><span data-stu-id="1b79a-247">Description</span></span> | <span data-ttu-id="1b79a-248">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1b79a-248">Allowed values</span></span> | <span data-ttu-id="1b79a-249">Required</span><span class="sxs-lookup"><span data-stu-id="1b79a-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b79a-250">recursive</span><span class="sxs-lookup"><span data-stu-id="1b79a-250">recursive</span></span> |<span data-ttu-id="1b79a-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="1b79a-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="1b79a-252">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="1b79a-252">True, False (default)</span></span> |<span data-ttu-id="1b79a-253">No</span><span class="sxs-lookup"><span data-stu-id="1b79a-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob-storage"></a><span data-ttu-id="1b79a-254">JSON example: Copy data from FTP server to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="1b79a-254">JSON example: Copy data from FTP server to Azure Blob storage</span></span>
<span data-ttu-id="1b79a-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="1b79a-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="1b79a-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1b79a-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="1b79a-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="1b79a-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="1b79a-258">A linked service of type [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1b79a-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="1b79a-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1b79a-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="1b79a-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="1b79a-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="1b79a-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="1b79a-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="1b79a-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="1b79a-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="1b79a-263">The sample copies data from an FTP server to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="1b79a-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="1b79a-264">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="1b79a-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="1b79a-265">FTP linked service</span><span class="sxs-lookup"><span data-stu-id="1b79a-265">FTP linked service</span></span>

<span data-ttu-id="1b79a-266">This example uses basic authentication, with the user name and password in plain text.</span><span class="sxs-lookup"><span data-stu-id="1b79a-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="1b79a-267">You can also use one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="1b79a-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="1b79a-268">Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="1b79a-268">Anonymous authentication</span></span>
* <span data-ttu-id="1b79a-269">Basic authentication with encrypted credentials</span><span class="sxs-lookup"><span data-stu-id="1b79a-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="1b79a-270">FTP over SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="1b79a-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="1b79a-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="1b79a-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="1b79a-272">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="1b79a-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="1b79a-273">FTP input dataset</span><span class="sxs-lookup"><span data-stu-id="1b79a-273">FTP input dataset</span></span>

<span data-ttu-id="1b79a-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="1b79a-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="1b79a-275">The pipeline copies the file to the destination.</span><span class="sxs-lookup"><span data-stu-id="1b79a-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="1b79a-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1b79a-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="1b79a-277">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="1b79a-277">Azure Blob output dataset</span></span>

<span data-ttu-id="1b79a-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1b79a-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1b79a-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="1b79a-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1b79a-280">The folder path uses the year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="1b79a-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="1b79a-281">A copy activity in a pipeline with file system source and blob sink</span><span class="sxs-lookup"><span data-stu-id="1b79a-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="1b79a-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="1b79a-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="1b79a-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1b79a-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="1b79a-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b79a-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b79a-285">Next steps</span></span>
<span data-ttu-id="1b79a-286">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="1b79a-286">See the following articles:</span></span>

* <span data-ttu-id="1b79a-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="1b79a-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1b79a-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
