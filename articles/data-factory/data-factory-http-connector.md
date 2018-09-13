---
title: Move data from an HTTP source - Azure | Microsoft Docs
description: Learn about how to move data from an on-premises or a cloud HTTP source using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: jingwang
ms.openlocfilehash: 4870d2a0bbe35f3980864d8b4f3d011a189b650e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549355"
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="7ba3b-103">Move data from an HTTP source using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7ba3b-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="7ba3b-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="7ba3b-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="7ba3b-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="7ba3b-107">Supported scenarios and authentication types</span><span class="sxs-lookup"><span data-stu-id="7ba3b-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="7ba3b-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="7ba3b-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="7ba3b-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="7ba3b-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="7ba3b-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7ba3b-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="7ba3b-113">Getting started</span></span>
<span data-ttu-id="7ba3b-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="7ba3b-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7ba3b-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="7ba3b-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7ba3b-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="7ba3b-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7ba3b-120">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="7ba3b-120">Linked service properties</span></span>
<span data-ttu-id="7ba3b-121">The following table provides description for JSON elements specific to HTTP linked service.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="7ba3b-122">Property</span><span class="sxs-lookup"><span data-stu-id="7ba3b-122">Property</span></span> | <span data-ttu-id="7ba3b-123">Description</span><span class="sxs-lookup"><span data-stu-id="7ba3b-123">Description</span></span> | <span data-ttu-id="7ba3b-124">Required</span><span class="sxs-lookup"><span data-stu-id="7ba3b-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ba3b-125">type</span><span class="sxs-lookup"><span data-stu-id="7ba3b-125">type</span></span> | <span data-ttu-id="7ba3b-126">The type property must be set to: `Http`.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="7ba3b-127">Yes</span><span class="sxs-lookup"><span data-stu-id="7ba3b-127">Yes</span></span> |
| <span data-ttu-id="7ba3b-128">url</span><span class="sxs-lookup"><span data-stu-id="7ba3b-128">url</span></span> | <span data-ttu-id="7ba3b-129">Base URL to the Web Server</span><span class="sxs-lookup"><span data-stu-id="7ba3b-129">Base URL to the Web Server</span></span> | <span data-ttu-id="7ba3b-130">Yes</span><span class="sxs-lookup"><span data-stu-id="7ba3b-130">Yes</span></span> |
| <span data-ttu-id="7ba3b-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7ba3b-131">authenticationType</span></span> | <span data-ttu-id="7ba3b-132">Specifies the authentication type.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-132">Specifies the authentication type.</span></span> <span data-ttu-id="7ba3b-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="7ba3b-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="7ba3b-135">Yes</span><span class="sxs-lookup"><span data-stu-id="7ba3b-135">Yes</span></span> |
| <span data-ttu-id="7ba3b-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="7ba3b-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="7ba3b-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span><span class="sxs-lookup"><span data-stu-id="7ba3b-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="7ba3b-138">No, default is true</span><span class="sxs-lookup"><span data-stu-id="7ba3b-138">No, default is true</span></span> |
| <span data-ttu-id="7ba3b-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7ba3b-139">gatewayName</span></span> | <span data-ttu-id="7ba3b-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="7ba3b-141">Yes if copying data from an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="7ba3b-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="7ba3b-142">encryptedCredential</span></span> | <span data-ttu-id="7ba3b-143">Encrypted credential to access the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="7ba3b-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="7ba3b-145">No.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-145">No.</span></span> <span data-ttu-id="7ba3b-146">Apply only when copying data from an on-premises HTTP server.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="7ba3b-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7ba3b-148">Using Basic, Digest, or Windows authentication</span><span class="sxs-lookup"><span data-stu-id="7ba3b-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="7ba3b-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span><span class="sxs-lookup"><span data-stu-id="7ba3b-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7ba3b-150">Property</span><span class="sxs-lookup"><span data-stu-id="7ba3b-150">Property</span></span> | <span data-ttu-id="7ba3b-151">Description</span><span class="sxs-lookup"><span data-stu-id="7ba3b-151">Description</span></span> | <span data-ttu-id="7ba3b-152">Required</span><span class="sxs-lookup"><span data-stu-id="7ba3b-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ba3b-153">username</span><span class="sxs-lookup"><span data-stu-id="7ba3b-153">username</span></span> | <span data-ttu-id="7ba3b-154">Username to access the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="7ba3b-155">Yes</span><span class="sxs-lookup"><span data-stu-id="7ba3b-155">Yes</span></span> |
| <span data-ttu-id="7ba3b-156">password</span><span class="sxs-lookup"><span data-stu-id="7ba3b-156">password</span></span> | <span data-ttu-id="7ba3b-157">Password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-157">Password for the user (username).</span></span> | <span data-ttu-id="7ba3b-158">Yes</span><span class="sxs-lookup"><span data-stu-id="7ba3b-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7ba3b-159">Example: using Basic, Digest, or Windows authentication</span><span class="sxs-lookup"><span data-stu-id="7ba3b-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="7ba3b-160">Using ClientCertificate authentication</span><span class="sxs-lookup"><span data-stu-id="7ba3b-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="7ba3b-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span><span class="sxs-lookup"><span data-stu-id="7ba3b-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7ba3b-162">Property</span><span class="sxs-lookup"><span data-stu-id="7ba3b-162">Property</span></span> | <span data-ttu-id="7ba3b-163">Description</span><span class="sxs-lookup"><span data-stu-id="7ba3b-163">Description</span></span> | <span data-ttu-id="7ba3b-164">Required</span><span class="sxs-lookup"><span data-stu-id="7ba3b-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ba3b-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="7ba3b-165">embeddedCertData</span></span> | <span data-ttu-id="7ba3b-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="7ba3b-167">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7ba3b-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="7ba3b-168">certThumbprint</span></span> | <span data-ttu-id="7ba3b-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="7ba3b-170">Apply only when copying data from an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="7ba3b-171">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7ba3b-172">password</span><span class="sxs-lookup"><span data-stu-id="7ba3b-172">password</span></span> | <span data-ttu-id="7ba3b-173">Password associated with the certificate.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-173">Password associated with the certificate.</span></span> | <span data-ttu-id="7ba3b-174">No</span><span class="sxs-lookup"><span data-stu-id="7ba3b-174">No</span></span> |

<span data-ttu-id="7ba3b-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span><span class="sxs-lookup"><span data-stu-id="7ba3b-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="7ba3b-176">Launch Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="7ba3b-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="7ba3b-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="7ba3b-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span><span class="sxs-lookup"><span data-stu-id="7ba3b-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="7ba3b-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="7ba3b-181">Example: using client certificate</span><span class="sxs-lookup"><span data-stu-id="7ba3b-181">Example: using client certificate</span></span>
<span data-ttu-id="7ba3b-182">This linked service links your data factory to an on-premises HTTP web server.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="7ba3b-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="7ba3b-184">Example: using client certificate in a file</span><span class="sxs-lookup"><span data-stu-id="7ba3b-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="7ba3b-185">This linked service links your data factory to an on-premises HTTP web server.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="7ba3b-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="7ba3b-187">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="7ba3b-187">Dataset properties</span></span>
<span data-ttu-id="7ba3b-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7ba3b-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7ba3b-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="7ba3b-191">The typeProperties section for dataset of type **Http** has the following properties</span><span class="sxs-lookup"><span data-stu-id="7ba3b-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="7ba3b-192">Property</span><span class="sxs-lookup"><span data-stu-id="7ba3b-192">Property</span></span> | <span data-ttu-id="7ba3b-193">Description</span><span class="sxs-lookup"><span data-stu-id="7ba3b-193">Description</span></span> | <span data-ttu-id="7ba3b-194">Required</span><span class="sxs-lookup"><span data-stu-id="7ba3b-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7ba3b-195">type</span><span class="sxs-lookup"><span data-stu-id="7ba3b-195">type</span></span> | <span data-ttu-id="7ba3b-196">Specified the type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-196">Specified the type of the dataset.</span></span> <span data-ttu-id="7ba3b-197">must be set to `Http`.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-197">must be set to `Http`.</span></span> | <span data-ttu-id="7ba3b-198">Yes</span><span class="sxs-lookup"><span data-stu-id="7ba3b-198">Yes</span></span> |
| <span data-ttu-id="7ba3b-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="7ba3b-199">relativeUrl</span></span> | <span data-ttu-id="7ba3b-200">A relative URL to the resource that contains the data.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="7ba3b-201">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="7ba3b-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="7ba3b-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="7ba3b-203">No</span><span class="sxs-lookup"><span data-stu-id="7ba3b-203">No</span></span> |
| <span data-ttu-id="7ba3b-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="7ba3b-204">requestMethod</span></span> | <span data-ttu-id="7ba3b-205">Http method.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-205">Http method.</span></span> <span data-ttu-id="7ba3b-206">Allowed values are **GET** or **POST**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="7ba3b-207">No.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-207">No.</span></span> <span data-ttu-id="7ba3b-208">Default is `GET`.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-208">Default is `GET`.</span></span> |
| <span data-ttu-id="7ba3b-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="7ba3b-209">additionalHeaders</span></span> | <span data-ttu-id="7ba3b-210">Additional HTTP request headers.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="7ba3b-211">No</span><span class="sxs-lookup"><span data-stu-id="7ba3b-211">No</span></span> |
| <span data-ttu-id="7ba3b-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="7ba3b-212">requestBody</span></span> | <span data-ttu-id="7ba3b-213">Body for HTTP request.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-213">Body for HTTP request.</span></span> | <span data-ttu-id="7ba3b-214">No</span><span class="sxs-lookup"><span data-stu-id="7ba3b-214">No</span></span> |
| <span data-ttu-id="7ba3b-215">format</span><span class="sxs-lookup"><span data-stu-id="7ba3b-215">format</span></span> | <span data-ttu-id="7ba3b-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="7ba3b-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="7ba3b-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="7ba3b-219">No</span><span class="sxs-lookup"><span data-stu-id="7ba3b-219">No</span></span> |
| <span data-ttu-id="7ba3b-220">compression</span><span class="sxs-lookup"><span data-stu-id="7ba3b-220">compression</span></span> | <span data-ttu-id="7ba3b-221">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="7ba3b-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="7ba3b-223">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="7ba3b-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="7ba3b-225">No</span><span class="sxs-lookup"><span data-stu-id="7ba3b-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="7ba3b-226">Example: using the GET (default) method</span><span class="sxs-lookup"><span data-stu-id="7ba3b-226">Example: using the GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-the-post-method"></a><span data-ttu-id="7ba3b-227">Example: using the POST method</span><span class="sxs-lookup"><span data-stu-id="7ba3b-227">Example: using the POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="7ba3b-228">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="7ba3b-228">Copy activity properties</span></span>
<span data-ttu-id="7ba3b-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7ba3b-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7ba3b-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="7ba3b-232">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="7ba3b-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="7ba3b-234">Property</span><span class="sxs-lookup"><span data-stu-id="7ba3b-234">Property</span></span> | <span data-ttu-id="7ba3b-235">Description</span><span class="sxs-lookup"><span data-stu-id="7ba3b-235">Description</span></span> | <span data-ttu-id="7ba3b-236">Required</span><span class="sxs-lookup"><span data-stu-id="7ba3b-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="7ba3b-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="7ba3b-237">httpRequestTimeout</span></span> | <span data-ttu-id="7ba3b-238">The timeout (TimeSpan) for the HTTP request to get a response.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="7ba3b-239">It is the timeout to get a response, not the timeout to read response data.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="7ba3b-240">No.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-240">No.</span></span> <span data-ttu-id="7ba3b-241">Default value: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="7ba3b-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="7ba3b-242">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="7ba3b-242">Supported file and compression formats</span></span>
<span data-ttu-id="7ba3b-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="7ba3b-244">JSON examples</span><span class="sxs-lookup"><span data-stu-id="7ba3b-244">JSON examples</span></span>
<span data-ttu-id="7ba3b-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7ba3b-246">They show how to copy data from HTTP source to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="7ba3b-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="7ba3b-248">Example: Copy data from HTTP source to Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="7ba3b-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="7ba3b-249">The Data Factory solution for this sample contains the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="7ba3b-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="7ba3b-250">A linked service of type [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="7ba3b-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7ba3b-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="7ba3b-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7ba3b-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7ba3b-255">The sample copies data from an HTTP source to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="7ba3b-256">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="7ba3b-257">HTTP linked service</span><span class="sxs-lookup"><span data-stu-id="7ba3b-257">HTTP linked service</span></span>
<span data-ttu-id="7ba3b-258">This example uses the HTTP linked service with anonymous authentication.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="7ba3b-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="7ba3b-260">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="7ba3b-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="7ba3b-261">HTTP input dataset</span><span class="sxs-lookup"><span data-stu-id="7ba3b-261">HTTP input dataset</span></span>
<span data-ttu-id="7ba3b-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="7ba3b-263">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="7ba3b-263">Azure Blob output dataset</span></span>

<span data-ttu-id="7ba3b-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="7ba3b-265">Pipeline with Copy activity</span><span class="sxs-lookup"><span data-stu-id="7ba3b-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="7ba3b-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="7ba3b-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="7ba3b-268">See [HttpSource](#httpsource-in-copy-activity) for the list of properties supported by the HttpSource.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-268">See [HttpSource](#httpsource-in-copy-activity) for the list of properties supported by the HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> <span data-ttu-id="7ba3b-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7ba3b-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7ba3b-270">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="7ba3b-270">Performance and Tuning</span></span>
<span data-ttu-id="7ba3b-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="7ba3b-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
