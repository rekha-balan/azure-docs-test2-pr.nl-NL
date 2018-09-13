---
title: Copy data from HTTP source using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from a cloud or on-premises HTTP source to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/24/2018
ms.author: jingwang
ms.openlocfilehash: 5afb2fccd5c7b8ca306079941837d854c0b21349
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968159"
---
# <a name="copy-data-from-http-endpoint-using-azure-data-factory"></a><span data-ttu-id="b4a20-103">Copy data from HTTP endpoint using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b4a20-103">Copy data from HTTP endpoint using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-http-connector.md)
> * [Current version](connector-http.md)

<span data-ttu-id="b4a20-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4a20-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an HTTP endpoint.</span></span> <span data-ttu-id="b4a20-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="b4a20-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="b4a20-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="b4a20-108">Supported capabilities</span></span>

<span data-ttu-id="b4a20-109">You can copy data from HTTP source to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="b4a20-109">You can copy data from HTTP source to any supported sink data store.</span></span> <span data-ttu-id="b4a20-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="b4a20-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="b4a20-111">Specifically, this HTTP connector supports:</span><span class="sxs-lookup"><span data-stu-id="b4a20-111">Specifically, this HTTP connector supports:</span></span>

- <span data-ttu-id="b4a20-112">Retrieving data from HTTP/s endpoint by using HTTP **GET** or **POST** method.</span><span class="sxs-lookup"><span data-stu-id="b4a20-112">Retrieving data from HTTP/s endpoint by using HTTP **GET** or **POST** method.</span></span>
- <span data-ttu-id="b4a20-113">Retrieving data using the following authentications: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-113">Retrieving data using the following authentications: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span>
- <span data-ttu-id="b4a20-114">Copying the HTTP response as-is or parsing it with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span><span class="sxs-lookup"><span data-stu-id="b4a20-114">Copying the HTTP response as-is or parsing it with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span></span>

<span data-ttu-id="b4a20-115">The difference between this connector and the [Web table connector](connector-web-table.md) is that the latter is used to extract table content from web HTML page.</span><span class="sxs-lookup"><span data-stu-id="b4a20-115">The difference between this connector and the [Web table connector](connector-web-table.md) is that the latter is used to extract table content from web HTML page.</span></span>

>[!TIP]
>To test HTTP request for data retrieving before configuring HTTP connector in ADF, you can learn from the API spec on header and body requirements, and use tools like Postman or web browser to validate.

## <a name="getting-started"></a><span data-ttu-id="b4a20-117">Getting started</span><span class="sxs-lookup"><span data-stu-id="b4a20-117">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="b4a20-118">The following sections provide details about properties that are used to define Data Factory entities specific to HTTP connector.</span><span class="sxs-lookup"><span data-stu-id="b4a20-118">The following sections provide details about properties that are used to define Data Factory entities specific to HTTP connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b4a20-119">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="b4a20-119">Linked service properties</span></span>

<span data-ttu-id="b4a20-120">The following properties are supported for HTTP linked service:</span><span class="sxs-lookup"><span data-stu-id="b4a20-120">The following properties are supported for HTTP linked service:</span></span>

| <span data-ttu-id="b4a20-121">Property</span><span class="sxs-lookup"><span data-stu-id="b4a20-121">Property</span></span> | <span data-ttu-id="b4a20-122">Description</span><span class="sxs-lookup"><span data-stu-id="b4a20-122">Description</span></span> | <span data-ttu-id="b4a20-123">Required</span><span class="sxs-lookup"><span data-stu-id="b4a20-123">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b4a20-124">type</span><span class="sxs-lookup"><span data-stu-id="b4a20-124">type</span></span> | <span data-ttu-id="b4a20-125">The type property must be set to: **HttpServer**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-125">The type property must be set to: **HttpServer**.</span></span> | <span data-ttu-id="b4a20-126">Yes</span><span class="sxs-lookup"><span data-stu-id="b4a20-126">Yes</span></span> |
| <span data-ttu-id="b4a20-127">url</span><span class="sxs-lookup"><span data-stu-id="b4a20-127">url</span></span> | <span data-ttu-id="b4a20-128">Base URL to the Web Server</span><span class="sxs-lookup"><span data-stu-id="b4a20-128">Base URL to the Web Server</span></span> | <span data-ttu-id="b4a20-129">Yes</span><span class="sxs-lookup"><span data-stu-id="b4a20-129">Yes</span></span> |
| <span data-ttu-id="b4a20-130">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="b4a20-130">enableServerCertificateValidation</span></span> | <span data-ttu-id="b4a20-131">Specify whether to enable server SSL certificate validation when connecting to HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4a20-131">Specify whether to enable server SSL certificate validation when connecting to HTTP endpoint.</span></span> <span data-ttu-id="b4a20-132">When your HTTPS server is using self-signed certificate, set this to false.</span><span class="sxs-lookup"><span data-stu-id="b4a20-132">When your HTTPS server is using self-signed certificate, set this to false.</span></span> | <span data-ttu-id="b4a20-133">No, default is true</span><span class="sxs-lookup"><span data-stu-id="b4a20-133">No, default is true</span></span> |
| <span data-ttu-id="b4a20-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b4a20-134">authenticationType</span></span> | <span data-ttu-id="b4a20-135">Specifies the authentication type.</span><span class="sxs-lookup"><span data-stu-id="b4a20-135">Specifies the authentication type.</span></span> <span data-ttu-id="b4a20-136">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-136">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="b4a20-137">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span><span class="sxs-lookup"><span data-stu-id="b4a20-137">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="b4a20-138">Yes</span><span class="sxs-lookup"><span data-stu-id="b4a20-138">Yes</span></span> |
| <span data-ttu-id="b4a20-139">connectVia</span><span class="sxs-lookup"><span data-stu-id="b4a20-139">connectVia</span></span> | <span data-ttu-id="b4a20-140">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="b4a20-140">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="b4a20-141">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="b4a20-141">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="b4a20-142">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="b4a20-142">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="b4a20-143">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-143">No</span></span> |

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="b4a20-144">Using Basic, Digest, or Windows authentication</span><span class="sxs-lookup"><span data-stu-id="b4a20-144">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="b4a20-145">Set "authenticationType" property to **Basic**, **Digest**, or **Windows**, and specify the following properties along with generic properties described in the previous section:</span><span class="sxs-lookup"><span data-stu-id="b4a20-145">Set "authenticationType" property to **Basic**, **Digest**, or **Windows**, and specify the following properties along with generic properties described in the previous section:</span></span>

| <span data-ttu-id="b4a20-146">Property</span><span class="sxs-lookup"><span data-stu-id="b4a20-146">Property</span></span> | <span data-ttu-id="b4a20-147">Description</span><span class="sxs-lookup"><span data-stu-id="b4a20-147">Description</span></span> | <span data-ttu-id="b4a20-148">Required</span><span class="sxs-lookup"><span data-stu-id="b4a20-148">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b4a20-149">userName</span><span class="sxs-lookup"><span data-stu-id="b4a20-149">userName</span></span> | <span data-ttu-id="b4a20-150">User name to access the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4a20-150">User name to access the HTTP endpoint.</span></span> | <span data-ttu-id="b4a20-151">Yes</span><span class="sxs-lookup"><span data-stu-id="b4a20-151">Yes</span></span> |
| <span data-ttu-id="b4a20-152">password</span><span class="sxs-lookup"><span data-stu-id="b4a20-152">password</span></span> | <span data-ttu-id="b4a20-153">Password for the user (userName).</span><span class="sxs-lookup"><span data-stu-id="b4a20-153">Password for the user (userName).</span></span> <span data-ttu-id="b4a20-154">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="b4a20-154">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="b4a20-155">Yes</span><span class="sxs-lookup"><span data-stu-id="b4a20-155">Yes</span></span> |

<span data-ttu-id="b4a20-156">**Example**</span><span class="sxs-lookup"><span data-stu-id="b4a20-156">**Example**</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "HttpServer",
        "typeProperties": {
            "authenticationType": "Basic",
            "url" : "<HTTP endpoint>",
            "userName": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="b4a20-157">Using ClientCertificate authentication</span><span class="sxs-lookup"><span data-stu-id="b4a20-157">Using ClientCertificate authentication</span></span>

<span data-ttu-id="b4a20-158">To use ClientCertificate authentication, set "authenticationType" property to **ClientCertificate**, and specify the following properties along with the generic properties described in the previous section:</span><span class="sxs-lookup"><span data-stu-id="b4a20-158">To use ClientCertificate authentication, set "authenticationType" property to **ClientCertificate**, and specify the following properties along with the generic properties described in the previous section:</span></span>

| <span data-ttu-id="b4a20-159">Property</span><span class="sxs-lookup"><span data-stu-id="b4a20-159">Property</span></span> | <span data-ttu-id="b4a20-160">Description</span><span class="sxs-lookup"><span data-stu-id="b4a20-160">Description</span></span> | <span data-ttu-id="b4a20-161">Required</span><span class="sxs-lookup"><span data-stu-id="b4a20-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b4a20-162">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="b4a20-162">embeddedCertData</span></span> | <span data-ttu-id="b4a20-163">Base64 encoded certificate data.</span><span class="sxs-lookup"><span data-stu-id="b4a20-163">Base64 encoded certificate data.</span></span> | <span data-ttu-id="b4a20-164">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="b4a20-164">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="b4a20-165">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="b4a20-165">certThumbprint</span></span> | <span data-ttu-id="b4a20-166">The thumbprint of the certificate that is installed on your Self-hosted Integration Runtime machine's cert store.</span><span class="sxs-lookup"><span data-stu-id="b4a20-166">The thumbprint of the certificate that is installed on your Self-hosted Integration Runtime machine's cert store.</span></span> <span data-ttu-id="b4a20-167">Applies only when Self-hosted type of Integration Runtime is specified in connectVia.</span><span class="sxs-lookup"><span data-stu-id="b4a20-167">Applies only when Self-hosted type of Integration Runtime is specified in connectVia.</span></span> | <span data-ttu-id="b4a20-168">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="b4a20-168">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="b4a20-169">password</span><span class="sxs-lookup"><span data-stu-id="b4a20-169">password</span></span> | <span data-ttu-id="b4a20-170">Password associated with the certificate.</span><span class="sxs-lookup"><span data-stu-id="b4a20-170">Password associated with the certificate.</span></span> <span data-ttu-id="b4a20-171">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="b4a20-171">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="b4a20-172">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-172">No</span></span> |

<span data-ttu-id="b4a20-173">If you use "certThumbprint" for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the Self-hosted Integration Runtime:</span><span class="sxs-lookup"><span data-stu-id="b4a20-173">If you use "certThumbprint" for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the Self-hosted Integration Runtime:</span></span>

1. <span data-ttu-id="b4a20-174">Launch Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="b4a20-174">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="b4a20-175">Add the **Certificates** snap-in that targets the **Local Computer**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-175">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="b4a20-176">Expand **Certificates**, **Personal**, and click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-176">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="b4a20-177">Right-click the certificate from the personal store, and select **All Tasks** -> **Manage Private Keys...**</span><span class="sxs-lookup"><span data-stu-id="b4a20-177">Right-click the certificate from the personal store, and select **All Tasks** -> **Manage Private Keys...**</span></span>
3. <span data-ttu-id="b4a20-178">On the **Security** tab, add the user account under which Integration Runtime Host Service (DIAHostService) is running with the read access to the certificate.</span><span class="sxs-lookup"><span data-stu-id="b4a20-178">On the **Security** tab, add the user account under which Integration Runtime Host Service (DIAHostService) is running with the read access to the certificate.</span></span>

<span data-ttu-id="b4a20-179">**Example 1: using certThumbprint**</span><span class="sxs-lookup"><span data-stu-id="b4a20-179">**Example 1: using certThumbprint**</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "HttpServer",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "<HTTP endpoint>",
            "certThumbprint": "<thumbprint of certificate>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="b4a20-180">**Example 2: using embeddedCertData**</span><span class="sxs-lookup"><span data-stu-id="b4a20-180">**Example 2: using embeddedCertData**</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "HttpServer",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "<HTTP endpoint>",
            "embeddedCertData": "<base64 encoded cert data>",
            "password": {
                "type": "SecureString",
                "value": "password of cert"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="b4a20-181">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="b4a20-181">Dataset properties</span></span>

<span data-ttu-id="b4a20-182">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="b4a20-182">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="b4a20-183">This section provides a list of properties supported by HTTP dataset.</span><span class="sxs-lookup"><span data-stu-id="b4a20-183">This section provides a list of properties supported by HTTP dataset.</span></span>

<span data-ttu-id="b4a20-184">To copy data from HTTP, set the type property of the dataset to **HttpFile**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-184">To copy data from HTTP, set the type property of the dataset to **HttpFile**.</span></span> <span data-ttu-id="b4a20-185">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="b4a20-185">The following properties are supported:</span></span>

| <span data-ttu-id="b4a20-186">Property</span><span class="sxs-lookup"><span data-stu-id="b4a20-186">Property</span></span> | <span data-ttu-id="b4a20-187">Description</span><span class="sxs-lookup"><span data-stu-id="b4a20-187">Description</span></span> | <span data-ttu-id="b4a20-188">Required</span><span class="sxs-lookup"><span data-stu-id="b4a20-188">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b4a20-189">type</span><span class="sxs-lookup"><span data-stu-id="b4a20-189">type</span></span> | <span data-ttu-id="b4a20-190">The type property of the dataset must be set to: **HttpFile**</span><span class="sxs-lookup"><span data-stu-id="b4a20-190">The type property of the dataset must be set to: **HttpFile**</span></span> | <span data-ttu-id="b4a20-191">Yes</span><span class="sxs-lookup"><span data-stu-id="b4a20-191">Yes</span></span> |
| <span data-ttu-id="b4a20-192">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="b4a20-192">relativeUrl</span></span> | <span data-ttu-id="b4a20-193">A relative URL to the resource that contains the data.</span><span class="sxs-lookup"><span data-stu-id="b4a20-193">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="b4a20-194">When this property is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="b4a20-194">When this property is not specified, only the URL specified in the linked service definition is used.</span></span> | <span data-ttu-id="b4a20-195">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-195">No</span></span> |
| <span data-ttu-id="b4a20-196">requestMethod</span><span class="sxs-lookup"><span data-stu-id="b4a20-196">requestMethod</span></span> | <span data-ttu-id="b4a20-197">Http method.</span><span class="sxs-lookup"><span data-stu-id="b4a20-197">Http method.</span></span><br/><span data-ttu-id="b4a20-198">Allowed values are **Get** (default) or **Post**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-198">Allowed values are **Get** (default) or **Post**.</span></span> | <span data-ttu-id="b4a20-199">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-199">No</span></span> |
| <span data-ttu-id="b4a20-200">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="b4a20-200">additionalHeaders</span></span> | <span data-ttu-id="b4a20-201">Additional HTTP request headers.</span><span class="sxs-lookup"><span data-stu-id="b4a20-201">Additional HTTP request headers.</span></span> | <span data-ttu-id="b4a20-202">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-202">No</span></span> |
| <span data-ttu-id="b4a20-203">requestBody</span><span class="sxs-lookup"><span data-stu-id="b4a20-203">requestBody</span></span> | <span data-ttu-id="b4a20-204">Body for HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b4a20-204">Body for HTTP request.</span></span> | <span data-ttu-id="b4a20-205">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-205">No</span></span> |
| <span data-ttu-id="b4a20-206">format</span><span class="sxs-lookup"><span data-stu-id="b4a20-206">format</span></span> | <span data-ttu-id="b4a20-207">If you want to **retrieve data from HTTP endpoint as-is** without parsing it and copy to a file-based store, skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="b4a20-207">If you want to **retrieve data from HTTP endpoint as-is** without parsing it and copy to a file-based store, skip the format section in both input and output dataset definitions.</span></span><br/><br/><span data-ttu-id="b4a20-208">If you want to parse the HTTP response content during copy, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-208">If you want to parse the HTTP response content during copy, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="b4a20-209">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="b4a20-209">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="b4a20-210">For more information, see [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="b4a20-210">For more information, see [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span></span> |<span data-ttu-id="b4a20-211">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-211">No</span></span> |
| <span data-ttu-id="b4a20-212">compression</span><span class="sxs-lookup"><span data-stu-id="b4a20-212">compression</span></span> | <span data-ttu-id="b4a20-213">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="b4a20-213">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="b4a20-214">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="b4a20-214">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span></span><br/><span data-ttu-id="b4a20-215">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-215">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span><br/><span data-ttu-id="b4a20-216">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-216">Supported levels are: **Optimal** and **Fastest**.</span></span> |<span data-ttu-id="b4a20-217">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-217">No</span></span> |

>[!NOTE]
>The supported HTTP request payload size is around 500KB. If the payload size you want to pass to your web endpoint is larger than this, consider to batch into smaller chunks.

<span data-ttu-id="b4a20-220">**Example 1: using Get method (default)**</span><span class="sxs-lookup"><span data-stu-id="b4a20-220">**Example 1: using Get method (default)**</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "HttpFile",
        "linkedServiceName": {
            "referenceName": "<HTTP linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "relativeUrl": "<relative url>",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        }
    }
}
```

<span data-ttu-id="b4a20-221">**Example 2: using Post method**</span><span class="sxs-lookup"><span data-stu-id="b4a20-221">**Example 2: using Post method**</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "HttpFile",
        "linkedServiceName": {
            "referenceName": "<HTTP linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "relativeUrl": "<relative url>",
            "requestMethod": "Post",
            "requestBody": "<body for POST HTTP request>"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="b4a20-222">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="b4a20-222">Copy activity properties</span></span>

<span data-ttu-id="b4a20-223">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="b4a20-223">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="b4a20-224">This section provides a list of properties supported by HTTP source.</span><span class="sxs-lookup"><span data-stu-id="b4a20-224">This section provides a list of properties supported by HTTP source.</span></span>

### <a name="http-as-source"></a><span data-ttu-id="b4a20-225">HTTP as source</span><span class="sxs-lookup"><span data-stu-id="b4a20-225">HTTP as source</span></span>

<span data-ttu-id="b4a20-226">To copy data from HTTP, set the source type in the copy activity to **HttpSource**.</span><span class="sxs-lookup"><span data-stu-id="b4a20-226">To copy data from HTTP, set the source type in the copy activity to **HttpSource**.</span></span> <span data-ttu-id="b4a20-227">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="b4a20-227">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="b4a20-228">Property</span><span class="sxs-lookup"><span data-stu-id="b4a20-228">Property</span></span> | <span data-ttu-id="b4a20-229">Description</span><span class="sxs-lookup"><span data-stu-id="b4a20-229">Description</span></span> | <span data-ttu-id="b4a20-230">Required</span><span class="sxs-lookup"><span data-stu-id="b4a20-230">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b4a20-231">type</span><span class="sxs-lookup"><span data-stu-id="b4a20-231">type</span></span> | <span data-ttu-id="b4a20-232">The type property of the copy activity source must be set to: **HttpSource**</span><span class="sxs-lookup"><span data-stu-id="b4a20-232">The type property of the copy activity source must be set to: **HttpSource**</span></span> | <span data-ttu-id="b4a20-233">Yes</span><span class="sxs-lookup"><span data-stu-id="b4a20-233">Yes</span></span> |
| <span data-ttu-id="b4a20-234">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="b4a20-234">httpRequestTimeout</span></span> | <span data-ttu-id="b4a20-235">The timeout (TimeSpan) for the HTTP request to get a response.</span><span class="sxs-lookup"><span data-stu-id="b4a20-235">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="b4a20-236">It is the timeout to get a response, not the timeout to read response data.</span><span class="sxs-lookup"><span data-stu-id="b4a20-236">It is the timeout to get a response, not the timeout to read response data.</span></span><br/> <span data-ttu-id="b4a20-237">Default value is: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="b4a20-237">Default value is: 00:01:40</span></span>  | <span data-ttu-id="b4a20-238">No</span><span class="sxs-lookup"><span data-stu-id="b4a20-238">No</span></span> |

<span data-ttu-id="b4a20-239">**Example:**</span><span class="sxs-lookup"><span data-stu-id="b4a20-239">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromHTTP",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<HTTP input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "HttpSource",
                "httpRequestTimeout": "00:01:00"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```


## <a name="next-steps"></a><span data-ttu-id="b4a20-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4a20-240">Next steps</span></span>
<span data-ttu-id="b4a20-241">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b4a20-241">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
