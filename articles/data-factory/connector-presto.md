---
title: Copy data from Presto using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Presto to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 06/15/2017
ms.author: jingwang
ms.openlocfilehash: 4b3e022bd22242bdc246e1dd30aa6cc3e00134e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966177"
---
# <a name="copy-data-from-presto-using-azure-data-factory"></a><span data-ttu-id="57635-103">Copy data from Presto using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="57635-103">Copy data from Presto using Azure Data Factory</span></span>

<span data-ttu-id="57635-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Presto.</span><span class="sxs-lookup"><span data-stu-id="57635-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Presto.</span></span> <span data-ttu-id="57635-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="57635-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57635-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="57635-106">This connector is currently in preview.</span></span> <span data-ttu-id="57635-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="57635-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="57635-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="57635-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="57635-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="57635-109">Supported capabilities</span></span>

<span data-ttu-id="57635-110">You can copy data from Presto to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="57635-110">You can copy data from Presto to any supported sink data store.</span></span> <span data-ttu-id="57635-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="57635-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="57635-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="57635-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="57635-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="57635-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="57635-114">The following sections provide details about properties that are used to define Data Factory entities specific to Presto connector.</span><span class="sxs-lookup"><span data-stu-id="57635-114">The following sections provide details about properties that are used to define Data Factory entities specific to Presto connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="57635-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="57635-115">Linked service properties</span></span>

<span data-ttu-id="57635-116">The following properties are supported for Presto linked service:</span><span class="sxs-lookup"><span data-stu-id="57635-116">The following properties are supported for Presto linked service:</span></span>

| <span data-ttu-id="57635-117">Property</span><span class="sxs-lookup"><span data-stu-id="57635-117">Property</span></span> | <span data-ttu-id="57635-118">Description</span><span class="sxs-lookup"><span data-stu-id="57635-118">Description</span></span> | <span data-ttu-id="57635-119">Required</span><span class="sxs-lookup"><span data-stu-id="57635-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="57635-120">type</span><span class="sxs-lookup"><span data-stu-id="57635-120">type</span></span> | <span data-ttu-id="57635-121">The type property must be set to: **Presto**</span><span class="sxs-lookup"><span data-stu-id="57635-121">The type property must be set to: **Presto**</span></span> | <span data-ttu-id="57635-122">Yes</span><span class="sxs-lookup"><span data-stu-id="57635-122">Yes</span></span> |
| <span data-ttu-id="57635-123">host</span><span class="sxs-lookup"><span data-stu-id="57635-123">host</span></span> | <span data-ttu-id="57635-124">The IP address or host name of the Presto server.</span><span class="sxs-lookup"><span data-stu-id="57635-124">The IP address or host name of the Presto server.</span></span> <span data-ttu-id="57635-125">(i.e. 192.168.222.160)</span><span class="sxs-lookup"><span data-stu-id="57635-125">(i.e. 192.168.222.160)</span></span>  | <span data-ttu-id="57635-126">Yes</span><span class="sxs-lookup"><span data-stu-id="57635-126">Yes</span></span> |
| <span data-ttu-id="57635-127">serverVersion</span><span class="sxs-lookup"><span data-stu-id="57635-127">serverVersion</span></span> | <span data-ttu-id="57635-128">The version of the Presto server.</span><span class="sxs-lookup"><span data-stu-id="57635-128">The version of the Presto server.</span></span> <span data-ttu-id="57635-129">(i.e. 0.148-t)</span><span class="sxs-lookup"><span data-stu-id="57635-129">(i.e. 0.148-t)</span></span>  | <span data-ttu-id="57635-130">Yes</span><span class="sxs-lookup"><span data-stu-id="57635-130">Yes</span></span> |
| <span data-ttu-id="57635-131">catalog</span><span class="sxs-lookup"><span data-stu-id="57635-131">catalog</span></span> | <span data-ttu-id="57635-132">The catalog context for all request against the server.</span><span class="sxs-lookup"><span data-stu-id="57635-132">The catalog context for all request against the server.</span></span>  | <span data-ttu-id="57635-133">Yes</span><span class="sxs-lookup"><span data-stu-id="57635-133">Yes</span></span> |
| <span data-ttu-id="57635-134">port</span><span class="sxs-lookup"><span data-stu-id="57635-134">port</span></span> | <span data-ttu-id="57635-135">The TCP port that the Presto server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="57635-135">The TCP port that the Presto server uses to listen for client connections.</span></span> <span data-ttu-id="57635-136">The default value is 8080.</span><span class="sxs-lookup"><span data-stu-id="57635-136">The default value is 8080.</span></span>  | <span data-ttu-id="57635-137">No</span><span class="sxs-lookup"><span data-stu-id="57635-137">No</span></span> |
| <span data-ttu-id="57635-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="57635-138">authenticationType</span></span> | <span data-ttu-id="57635-139">The authentication mechanism used to connect to the Presto server.</span><span class="sxs-lookup"><span data-stu-id="57635-139">The authentication mechanism used to connect to the Presto server.</span></span> <br/><span data-ttu-id="57635-140">Allowed values are: **Anonymous**, **LDAP**</span><span class="sxs-lookup"><span data-stu-id="57635-140">Allowed values are: **Anonymous**, **LDAP**</span></span> | <span data-ttu-id="57635-141">Yes</span><span class="sxs-lookup"><span data-stu-id="57635-141">Yes</span></span> |
| <span data-ttu-id="57635-142">username</span><span class="sxs-lookup"><span data-stu-id="57635-142">username</span></span> | <span data-ttu-id="57635-143">The user name used to connect to the Presto server.</span><span class="sxs-lookup"><span data-stu-id="57635-143">The user name used to connect to the Presto server.</span></span>  | <span data-ttu-id="57635-144">No</span><span class="sxs-lookup"><span data-stu-id="57635-144">No</span></span> |
| <span data-ttu-id="57635-145">password</span><span class="sxs-lookup"><span data-stu-id="57635-145">password</span></span> | <span data-ttu-id="57635-146">The password corresponding to the user name.</span><span class="sxs-lookup"><span data-stu-id="57635-146">The password corresponding to the user name.</span></span> <span data-ttu-id="57635-147">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="57635-147">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="57635-148">No</span><span class="sxs-lookup"><span data-stu-id="57635-148">No</span></span> |
| <span data-ttu-id="57635-149">enableSsl</span><span class="sxs-lookup"><span data-stu-id="57635-149">enableSsl</span></span> | <span data-ttu-id="57635-150">Specifies whether the connections to the server are encrypted using SSL.</span><span class="sxs-lookup"><span data-stu-id="57635-150">Specifies whether the connections to the server are encrypted using SSL.</span></span> <span data-ttu-id="57635-151">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="57635-151">The default value is false.</span></span>  | <span data-ttu-id="57635-152">No</span><span class="sxs-lookup"><span data-stu-id="57635-152">No</span></span> |
| <span data-ttu-id="57635-153">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="57635-153">trustedCertPath</span></span> | <span data-ttu-id="57635-154">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="57635-154">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span></span> <span data-ttu-id="57635-155">This property can only be set when using SSL on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="57635-155">This property can only be set when using SSL on self-hosted IR.</span></span> <span data-ttu-id="57635-156">The default value is the cacerts.pem file installed with the IR.</span><span class="sxs-lookup"><span data-stu-id="57635-156">The default value is the cacerts.pem file installed with the IR.</span></span>  | <span data-ttu-id="57635-157">No</span><span class="sxs-lookup"><span data-stu-id="57635-157">No</span></span> |
| <span data-ttu-id="57635-158">useSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="57635-158">useSystemTrustStore</span></span> | <span data-ttu-id="57635-159">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="57635-159">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span></span> <span data-ttu-id="57635-160">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="57635-160">The default value is false.</span></span>  | <span data-ttu-id="57635-161">No</span><span class="sxs-lookup"><span data-stu-id="57635-161">No</span></span> |
| <span data-ttu-id="57635-162">allowHostNameCNMismatch</span><span class="sxs-lookup"><span data-stu-id="57635-162">allowHostNameCNMismatch</span></span> | <span data-ttu-id="57635-163">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="57635-163">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="57635-164">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="57635-164">The default value is false.</span></span>  | <span data-ttu-id="57635-165">No</span><span class="sxs-lookup"><span data-stu-id="57635-165">No</span></span> |
| <span data-ttu-id="57635-166">allowSelfSignedServerCert</span><span class="sxs-lookup"><span data-stu-id="57635-166">allowSelfSignedServerCert</span></span> | <span data-ttu-id="57635-167">Specifies whether to allow self-signed certificates from the server.</span><span class="sxs-lookup"><span data-stu-id="57635-167">Specifies whether to allow self-signed certificates from the server.</span></span> <span data-ttu-id="57635-168">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="57635-168">The default value is false.</span></span>  | <span data-ttu-id="57635-169">No</span><span class="sxs-lookup"><span data-stu-id="57635-169">No</span></span> |
| <span data-ttu-id="57635-170">timeZoneID</span><span class="sxs-lookup"><span data-stu-id="57635-170">timeZoneID</span></span> | <span data-ttu-id="57635-171">The local time zone used by the connection.</span><span class="sxs-lookup"><span data-stu-id="57635-171">The local time zone used by the connection.</span></span> <span data-ttu-id="57635-172">Valid values for this option are specified in the IANA Time Zone Database.</span><span class="sxs-lookup"><span data-stu-id="57635-172">Valid values for this option are specified in the IANA Time Zone Database.</span></span> <span data-ttu-id="57635-173">The default value is the system time zone.</span><span class="sxs-lookup"><span data-stu-id="57635-173">The default value is the system time zone.</span></span>  | <span data-ttu-id="57635-174">No</span><span class="sxs-lookup"><span data-stu-id="57635-174">No</span></span> |

<span data-ttu-id="57635-175">**Example:**</span><span class="sxs-lookup"><span data-stu-id="57635-175">**Example:**</span></span>

```json
{
    "name": "PrestoLinkedService",
    "properties": {
        "type": "Presto",
        "typeProperties": {
            "host" : "<host>",
            "serverVersion" : "0.148-t",
            "catalog" : "<catalog>",
            "port" : "<port>",
            "authenticationType" : "LDAP",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            },
            "timeZoneID" : "Europe/Berlin"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="57635-176">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="57635-176">Dataset properties</span></span>

<span data-ttu-id="57635-177">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="57635-177">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="57635-178">This section provides a list of properties supported by Presto dataset.</span><span class="sxs-lookup"><span data-stu-id="57635-178">This section provides a list of properties supported by Presto dataset.</span></span>

<span data-ttu-id="57635-179">To copy data from Presto, set the type property of the dataset to **PrestoObject**.</span><span class="sxs-lookup"><span data-stu-id="57635-179">To copy data from Presto, set the type property of the dataset to **PrestoObject**.</span></span> <span data-ttu-id="57635-180">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="57635-180">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="57635-181">**Example**</span><span class="sxs-lookup"><span data-stu-id="57635-181">**Example**</span></span>

```json
{
    "name": "PrestoDataset",
    "properties": {
        "type": "PrestoObject",
        "linkedServiceName": {
            "referenceName": "<Presto linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="57635-182">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="57635-182">Copy activity properties</span></span>

<span data-ttu-id="57635-183">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="57635-183">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="57635-184">This section provides a list of properties supported by Presto source.</span><span class="sxs-lookup"><span data-stu-id="57635-184">This section provides a list of properties supported by Presto source.</span></span>

### <a name="prestosource-as-source"></a><span data-ttu-id="57635-185">PrestoSource as source</span><span class="sxs-lookup"><span data-stu-id="57635-185">PrestoSource as source</span></span>

<span data-ttu-id="57635-186">To copy data from Presto, set the source type in the copy activity to **PrestoSource**.</span><span class="sxs-lookup"><span data-stu-id="57635-186">To copy data from Presto, set the source type in the copy activity to **PrestoSource**.</span></span> <span data-ttu-id="57635-187">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="57635-187">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="57635-188">Property</span><span class="sxs-lookup"><span data-stu-id="57635-188">Property</span></span> | <span data-ttu-id="57635-189">Description</span><span class="sxs-lookup"><span data-stu-id="57635-189">Description</span></span> | <span data-ttu-id="57635-190">Required</span><span class="sxs-lookup"><span data-stu-id="57635-190">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="57635-191">type</span><span class="sxs-lookup"><span data-stu-id="57635-191">type</span></span> | <span data-ttu-id="57635-192">The type property of the copy activity source must be set to: **PrestoSource**</span><span class="sxs-lookup"><span data-stu-id="57635-192">The type property of the copy activity source must be set to: **PrestoSource**</span></span> | <span data-ttu-id="57635-193">Yes</span><span class="sxs-lookup"><span data-stu-id="57635-193">Yes</span></span> |
| <span data-ttu-id="57635-194">query</span><span class="sxs-lookup"><span data-stu-id="57635-194">query</span></span> | <span data-ttu-id="57635-195">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="57635-195">Use the custom SQL query to read data.</span></span> <span data-ttu-id="57635-196">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="57635-196">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="57635-197">Yes</span><span class="sxs-lookup"><span data-stu-id="57635-197">Yes</span></span> |

<span data-ttu-id="57635-198">**Example:**</span><span class="sxs-lookup"><span data-stu-id="57635-198">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromPresto",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Presto input dataset name>",
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
                "type": "PrestoSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="57635-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="57635-199">Next steps</span></span>
<span data-ttu-id="57635-200">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="57635-200">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
