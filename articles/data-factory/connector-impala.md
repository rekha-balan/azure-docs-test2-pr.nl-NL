---
title: Copy data from Impala by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Impala to supported sink data stores by using a copy activity in a data factory pipeline.
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
ms.date: 06/15/2018
ms.author: jingwang
ms.openlocfilehash: 366d0945bfac8546aa757648b6f797c2605a43ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871084"
---
# <a name="copy-data-from-impala-by-using-azure-data-factory"></a><span data-ttu-id="1f5a5-103">Copy data from Impala by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1f5a5-103">Copy data from Impala by using Azure Data Factory</span></span>

<span data-ttu-id="1f5a5-104">This article outlines how to use Copy Activity in Azure Data Factory to copy data from Impala.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-104">This article outlines how to use Copy Activity in Azure Data Factory to copy data from Impala.</span></span> <span data-ttu-id="1f5a5-105">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-105">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f5a5-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-106">This connector is currently in preview.</span></span> <span data-ttu-id="1f5a5-107">You can try it out and provide feedback.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-107">You can try it out and provide feedback.</span></span> <span data-ttu-id="1f5a5-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="1f5a5-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="1f5a5-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="1f5a5-109">Supported capabilities</span></span>

<span data-ttu-id="1f5a5-110">You can copy data from Impala to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-110">You can copy data from Impala to any supported sink data store.</span></span> <span data-ttu-id="1f5a5-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

 <span data-ttu-id="1f5a5-112">Data Factory provides a built-in driver to enable connectivity.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-112">Data Factory provides a built-in driver to enable connectivity.</span></span> <span data-ttu-id="1f5a5-113">Therefore, you don't need to manually install a driver to use this connector.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-113">Therefore, you don't need to manually install a driver to use this connector.</span></span>

## <a name="get-started"></a><span data-ttu-id="1f5a5-114">Get started</span><span class="sxs-lookup"><span data-stu-id="1f5a5-114">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="1f5a5-115">The following sections provide details about properties that are used to define Data Factory entities specific to the Impala connector.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-115">The following sections provide details about properties that are used to define Data Factory entities specific to the Impala connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1f5a5-116">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="1f5a5-116">Linked service properties</span></span>

<span data-ttu-id="1f5a5-117">The following properties are supported for Impala linked service.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-117">The following properties are supported for Impala linked service.</span></span>

| <span data-ttu-id="1f5a5-118">Property</span><span class="sxs-lookup"><span data-stu-id="1f5a5-118">Property</span></span> | <span data-ttu-id="1f5a5-119">Description</span><span class="sxs-lookup"><span data-stu-id="1f5a5-119">Description</span></span> | <span data-ttu-id="1f5a5-120">Required</span><span class="sxs-lookup"><span data-stu-id="1f5a5-120">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1f5a5-121">type</span><span class="sxs-lookup"><span data-stu-id="1f5a5-121">type</span></span> | <span data-ttu-id="1f5a5-122">The type property must be set to **Impala**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-122">The type property must be set to **Impala**.</span></span> | <span data-ttu-id="1f5a5-123">Yes</span><span class="sxs-lookup"><span data-stu-id="1f5a5-123">Yes</span></span> |
| <span data-ttu-id="1f5a5-124">host</span><span class="sxs-lookup"><span data-stu-id="1f5a5-124">host</span></span> | <span data-ttu-id="1f5a5-125">The IP address or host name of the Impala server (that is, 192.168.222.160).</span><span class="sxs-lookup"><span data-stu-id="1f5a5-125">The IP address or host name of the Impala server (that is, 192.168.222.160).</span></span>  | <span data-ttu-id="1f5a5-126">Yes</span><span class="sxs-lookup"><span data-stu-id="1f5a5-126">Yes</span></span> |
| <span data-ttu-id="1f5a5-127">port</span><span class="sxs-lookup"><span data-stu-id="1f5a5-127">port</span></span> | <span data-ttu-id="1f5a5-128">The TCP port that the Impala server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-128">The TCP port that the Impala server uses to listen for client connections.</span></span> <span data-ttu-id="1f5a5-129">The default value is 21050.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-129">The default value is 21050.</span></span>  | <span data-ttu-id="1f5a5-130">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-130">No</span></span> |
| <span data-ttu-id="1f5a5-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1f5a5-131">authenticationType</span></span> | <span data-ttu-id="1f5a5-132">The authentication type to use.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-132">The authentication type to use.</span></span> <br/><span data-ttu-id="1f5a5-133">Allowed values are **Anonymous**, **SASLUsername**, and **UsernameAndPassword**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-133">Allowed values are **Anonymous**, **SASLUsername**, and **UsernameAndPassword**.</span></span> | <span data-ttu-id="1f5a5-134">Yes</span><span class="sxs-lookup"><span data-stu-id="1f5a5-134">Yes</span></span> |
| <span data-ttu-id="1f5a5-135">username</span><span class="sxs-lookup"><span data-stu-id="1f5a5-135">username</span></span> | <span data-ttu-id="1f5a5-136">The user name used to access the Impala server.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-136">The user name used to access the Impala server.</span></span> <span data-ttu-id="1f5a5-137">The default value is anonymous when you use SASLUsername.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-137">The default value is anonymous when you use SASLUsername.</span></span>  | <span data-ttu-id="1f5a5-138">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-138">No</span></span> |
| <span data-ttu-id="1f5a5-139">password</span><span class="sxs-lookup"><span data-stu-id="1f5a5-139">password</span></span> | <span data-ttu-id="1f5a5-140">The password that corresponds to the user name when you use UsernameAndPassword.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-140">The password that corresponds to the user name when you use UsernameAndPassword.</span></span> <span data-ttu-id="1f5a5-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="1f5a5-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="1f5a5-142">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-142">No</span></span> |
| <span data-ttu-id="1f5a5-143">enableSsl</span><span class="sxs-lookup"><span data-stu-id="1f5a5-143">enableSsl</span></span> | <span data-ttu-id="1f5a5-144">Specifies whether the connections to the server are encrypted by using SSL.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-144">Specifies whether the connections to the server are encrypted by using SSL.</span></span> <span data-ttu-id="1f5a5-145">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-145">The default value is **false**.</span></span>  | <span data-ttu-id="1f5a5-146">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-146">No</span></span> |
| <span data-ttu-id="1f5a5-147">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="1f5a5-147">trustedCertPath</span></span> | <span data-ttu-id="1f5a5-148">The full path of the .pem file that contains trusted CA certificates used to verify the server when you connect over SSL.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-148">The full path of the .pem file that contains trusted CA certificates used to verify the server when you connect over SSL.</span></span> <span data-ttu-id="1f5a5-149">This property can be set only when you use SSL on Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-149">This property can be set only when you use SSL on Self-hosted Integration Runtime.</span></span> <span data-ttu-id="1f5a5-150">The default value is the cacerts.pem file installed with the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-150">The default value is the cacerts.pem file installed with the integration runtime.</span></span>  | <span data-ttu-id="1f5a5-151">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-151">No</span></span> |
| <span data-ttu-id="1f5a5-152">useSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="1f5a5-152">useSystemTrustStore</span></span> | <span data-ttu-id="1f5a5-153">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-153">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span></span> <span data-ttu-id="1f5a5-154">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-154">The default value is **false**.</span></span>  | <span data-ttu-id="1f5a5-155">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-155">No</span></span> |
| <span data-ttu-id="1f5a5-156">allowHostNameCNMismatch</span><span class="sxs-lookup"><span data-stu-id="1f5a5-156">allowHostNameCNMismatch</span></span> | <span data-ttu-id="1f5a5-157">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when you connect over SSL.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-157">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when you connect over SSL.</span></span> <span data-ttu-id="1f5a5-158">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-158">The default value is **false**.</span></span>  | <span data-ttu-id="1f5a5-159">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-159">No</span></span> |
| <span data-ttu-id="1f5a5-160">allowSelfSignedServerCert</span><span class="sxs-lookup"><span data-stu-id="1f5a5-160">allowSelfSignedServerCert</span></span> | <span data-ttu-id="1f5a5-161">Specifies whether to allow self-signed certificates from the server.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-161">Specifies whether to allow self-signed certificates from the server.</span></span> <span data-ttu-id="1f5a5-162">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-162">The default value is **false**.</span></span>  | <span data-ttu-id="1f5a5-163">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-163">No</span></span> |
| <span data-ttu-id="1f5a5-164">connectVia</span><span class="sxs-lookup"><span data-stu-id="1f5a5-164">connectVia</span></span> | <span data-ttu-id="1f5a5-165">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-165">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="1f5a5-166">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="1f5a5-166">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="1f5a5-167">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-167">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="1f5a5-168">No</span><span class="sxs-lookup"><span data-stu-id="1f5a5-168">No</span></span> |

<span data-ttu-id="1f5a5-169">**Example:**</span><span class="sxs-lookup"><span data-stu-id="1f5a5-169">**Example:**</span></span>

```json
{
    "name": "ImpalaLinkedService",
    "properties": {
        "type": "Impala",
        "typeProperties": {
            "host" : "<host>",
            "port" : "<port>",
            "authenticationType" : "UsernameAndPassword",
            "username" : "<username>",
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

## <a name="dataset-properties"></a><span data-ttu-id="1f5a5-170">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="1f5a5-170">Dataset properties</span></span>

<span data-ttu-id="1f5a5-171">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-171">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="1f5a5-172">This section provides a list of properties supported by the Impala dataset.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-172">This section provides a list of properties supported by the Impala dataset.</span></span>

<span data-ttu-id="1f5a5-173">To copy data from Impala, set the type property of the dataset to **ImpalaObject**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-173">To copy data from Impala, set the type property of the dataset to **ImpalaObject**.</span></span> <span data-ttu-id="1f5a5-174">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-174">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="1f5a5-175">**Example**</span><span class="sxs-lookup"><span data-stu-id="1f5a5-175">**Example**</span></span>

```json
{
    "name": "ImpalaDataset",
    "properties": {
        "type": "ImpalaObject",
        "linkedServiceName": {
            "referenceName": "<Impala linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="1f5a5-176">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="1f5a5-176">Copy activity properties</span></span>

<span data-ttu-id="1f5a5-177">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-177">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="1f5a5-178">This section provides a list of properties supported by the Impala source type.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-178">This section provides a list of properties supported by the Impala source type.</span></span>

### <a name="impala-as-a-source-type"></a><span data-ttu-id="1f5a5-179">Impala as a source type</span><span class="sxs-lookup"><span data-stu-id="1f5a5-179">Impala as a source type</span></span>

<span data-ttu-id="1f5a5-180">To copy data from Impala, set the source type in the copy activity to **ImpalaSource**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-180">To copy data from Impala, set the source type in the copy activity to **ImpalaSource**.</span></span> <span data-ttu-id="1f5a5-181">The following properties are supported in the copy activity **source** section.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-181">The following properties are supported in the copy activity **source** section.</span></span>

| <span data-ttu-id="1f5a5-182">Property</span><span class="sxs-lookup"><span data-stu-id="1f5a5-182">Property</span></span> | <span data-ttu-id="1f5a5-183">Description</span><span class="sxs-lookup"><span data-stu-id="1f5a5-183">Description</span></span> | <span data-ttu-id="1f5a5-184">Required</span><span class="sxs-lookup"><span data-stu-id="1f5a5-184">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1f5a5-185">type</span><span class="sxs-lookup"><span data-stu-id="1f5a5-185">type</span></span> | <span data-ttu-id="1f5a5-186">The type property of the copy activity source must be set to **ImpalaSource**.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-186">The type property of the copy activity source must be set to **ImpalaSource**.</span></span> | <span data-ttu-id="1f5a5-187">Yes</span><span class="sxs-lookup"><span data-stu-id="1f5a5-187">Yes</span></span> |
| <span data-ttu-id="1f5a5-188">query</span><span class="sxs-lookup"><span data-stu-id="1f5a5-188">query</span></span> | <span data-ttu-id="1f5a5-189">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-189">Use the custom SQL query to read data.</span></span> <span data-ttu-id="1f5a5-190">An example is `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="1f5a5-190">An example is `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="1f5a5-191">Yes</span><span class="sxs-lookup"><span data-stu-id="1f5a5-191">Yes</span></span> |

<span data-ttu-id="1f5a5-192">**Example:**</span><span class="sxs-lookup"><span data-stu-id="1f5a5-192">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromImpala",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Impala input dataset name>",
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
                "type": "ImpalaSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="1f5a5-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f5a5-193">Next steps</span></span>
<span data-ttu-id="1f5a5-194">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1f5a5-194">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
