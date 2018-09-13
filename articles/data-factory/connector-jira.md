---
title: Copy data from Jira using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Jira to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 743c0322152b555137b2bc37641377c3cfb3d0b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867873"
---
# <a name="copy-data-from-jira-using-azure-data-factory"></a><span data-ttu-id="566a1-103">Copy data from Jira using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="566a1-103">Copy data from Jira using Azure Data Factory</span></span>

<span data-ttu-id="566a1-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Jira.</span><span class="sxs-lookup"><span data-stu-id="566a1-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Jira.</span></span> <span data-ttu-id="566a1-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="566a1-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="566a1-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="566a1-106">This connector is currently in preview.</span></span> <span data-ttu-id="566a1-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="566a1-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="566a1-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="566a1-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="566a1-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="566a1-109">Supported capabilities</span></span>

<span data-ttu-id="566a1-110">You can copy data from Jira to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="566a1-110">You can copy data from Jira to any supported sink data store.</span></span> <span data-ttu-id="566a1-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="566a1-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="566a1-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="566a1-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="566a1-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="566a1-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="566a1-114">The following sections provide details about properties that are used to define Data Factory entities specific to Jira connector.</span><span class="sxs-lookup"><span data-stu-id="566a1-114">The following sections provide details about properties that are used to define Data Factory entities specific to Jira connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="566a1-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="566a1-115">Linked service properties</span></span>

<span data-ttu-id="566a1-116">The following properties are supported for Jira linked service:</span><span class="sxs-lookup"><span data-stu-id="566a1-116">The following properties are supported for Jira linked service:</span></span>

| <span data-ttu-id="566a1-117">Property</span><span class="sxs-lookup"><span data-stu-id="566a1-117">Property</span></span> | <span data-ttu-id="566a1-118">Description</span><span class="sxs-lookup"><span data-stu-id="566a1-118">Description</span></span> | <span data-ttu-id="566a1-119">Required</span><span class="sxs-lookup"><span data-stu-id="566a1-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566a1-120">type</span><span class="sxs-lookup"><span data-stu-id="566a1-120">type</span></span> | <span data-ttu-id="566a1-121">The type property must be set to: **Jira**</span><span class="sxs-lookup"><span data-stu-id="566a1-121">The type property must be set to: **Jira**</span></span> | <span data-ttu-id="566a1-122">Yes</span><span class="sxs-lookup"><span data-stu-id="566a1-122">Yes</span></span> |
| <span data-ttu-id="566a1-123">host</span><span class="sxs-lookup"><span data-stu-id="566a1-123">host</span></span> | <span data-ttu-id="566a1-124">The IP address or host name of the Jira service.</span><span class="sxs-lookup"><span data-stu-id="566a1-124">The IP address or host name of the Jira service.</span></span> <span data-ttu-id="566a1-125">(for example, jira.example.com)</span><span class="sxs-lookup"><span data-stu-id="566a1-125">(for example, jira.example.com)</span></span>  | <span data-ttu-id="566a1-126">Yes</span><span class="sxs-lookup"><span data-stu-id="566a1-126">Yes</span></span> |
| <span data-ttu-id="566a1-127">port</span><span class="sxs-lookup"><span data-stu-id="566a1-127">port</span></span> | <span data-ttu-id="566a1-128">The TCP port that the Jira server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="566a1-128">The TCP port that the Jira server uses to listen for client connections.</span></span> <span data-ttu-id="566a1-129">The default value is 443 if connecting through HTTPS, or 8080 if connecting through HTTP.</span><span class="sxs-lookup"><span data-stu-id="566a1-129">The default value is 443 if connecting through HTTPS, or 8080 if connecting through HTTP.</span></span>  | <span data-ttu-id="566a1-130">No</span><span class="sxs-lookup"><span data-stu-id="566a1-130">No</span></span> |
| <span data-ttu-id="566a1-131">username</span><span class="sxs-lookup"><span data-stu-id="566a1-131">username</span></span> | <span data-ttu-id="566a1-132">The user name that you use to access Jira Service.</span><span class="sxs-lookup"><span data-stu-id="566a1-132">The user name that you use to access Jira Service.</span></span>  | <span data-ttu-id="566a1-133">Yes</span><span class="sxs-lookup"><span data-stu-id="566a1-133">Yes</span></span> |
| <span data-ttu-id="566a1-134">password</span><span class="sxs-lookup"><span data-stu-id="566a1-134">password</span></span> | <span data-ttu-id="566a1-135">The password corresponding to the user name that you provided in the username field.</span><span class="sxs-lookup"><span data-stu-id="566a1-135">The password corresponding to the user name that you provided in the username field.</span></span> <span data-ttu-id="566a1-136">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="566a1-136">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="566a1-137">Yes</span><span class="sxs-lookup"><span data-stu-id="566a1-137">Yes</span></span> |
| <span data-ttu-id="566a1-138">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="566a1-138">useEncryptedEndpoints</span></span> | <span data-ttu-id="566a1-139">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="566a1-139">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="566a1-140">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="566a1-140">The default value is true.</span></span>  | <span data-ttu-id="566a1-141">No</span><span class="sxs-lookup"><span data-stu-id="566a1-141">No</span></span> |
| <span data-ttu-id="566a1-142">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="566a1-142">useHostVerification</span></span> | <span data-ttu-id="566a1-143">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="566a1-143">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="566a1-144">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="566a1-144">The default value is true.</span></span>  | <span data-ttu-id="566a1-145">No</span><span class="sxs-lookup"><span data-stu-id="566a1-145">No</span></span> |
| <span data-ttu-id="566a1-146">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="566a1-146">usePeerVerification</span></span> | <span data-ttu-id="566a1-147">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="566a1-147">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="566a1-148">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="566a1-148">The default value is true.</span></span>  | <span data-ttu-id="566a1-149">No</span><span class="sxs-lookup"><span data-stu-id="566a1-149">No</span></span> |

<span data-ttu-id="566a1-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="566a1-150">**Example:**</span></span>

```json
{
    "name": "JiraLinkedService",
    "properties": {
        "type": "Jira",
        "typeProperties": {
            "host" : "<host>",
            "port" : "<port>",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="566a1-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="566a1-151">Dataset properties</span></span>

<span data-ttu-id="566a1-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="566a1-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="566a1-153">This section provides a list of properties supported by Jira dataset.</span><span class="sxs-lookup"><span data-stu-id="566a1-153">This section provides a list of properties supported by Jira dataset.</span></span>

<span data-ttu-id="566a1-154">To copy data from Jira, set the type property of the dataset to **JiraObject**.</span><span class="sxs-lookup"><span data-stu-id="566a1-154">To copy data from Jira, set the type property of the dataset to **JiraObject**.</span></span> <span data-ttu-id="566a1-155">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="566a1-155">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="566a1-156">**Example**</span><span class="sxs-lookup"><span data-stu-id="566a1-156">**Example**</span></span>

```json
{
    "name": "JiraDataset",
    "properties": {
        "type": "JiraObject",
        "linkedServiceName": {
            "referenceName": "<Jira linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="566a1-157">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="566a1-157">Copy activity properties</span></span>

<span data-ttu-id="566a1-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="566a1-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="566a1-159">This section provides a list of properties supported by Jira source.</span><span class="sxs-lookup"><span data-stu-id="566a1-159">This section provides a list of properties supported by Jira source.</span></span>

### <a name="jirasource-as-source"></a><span data-ttu-id="566a1-160">JiraSource as source</span><span class="sxs-lookup"><span data-stu-id="566a1-160">JiraSource as source</span></span>

<span data-ttu-id="566a1-161">To copy data from Jira, set the source type in the copy activity to **JiraSource**.</span><span class="sxs-lookup"><span data-stu-id="566a1-161">To copy data from Jira, set the source type in the copy activity to **JiraSource**.</span></span> <span data-ttu-id="566a1-162">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="566a1-162">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="566a1-163">Property</span><span class="sxs-lookup"><span data-stu-id="566a1-163">Property</span></span> | <span data-ttu-id="566a1-164">Description</span><span class="sxs-lookup"><span data-stu-id="566a1-164">Description</span></span> | <span data-ttu-id="566a1-165">Required</span><span class="sxs-lookup"><span data-stu-id="566a1-165">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="566a1-166">type</span><span class="sxs-lookup"><span data-stu-id="566a1-166">type</span></span> | <span data-ttu-id="566a1-167">The type property of the copy activity source must be set to: **JiraSource**</span><span class="sxs-lookup"><span data-stu-id="566a1-167">The type property of the copy activity source must be set to: **JiraSource**</span></span> | <span data-ttu-id="566a1-168">Yes</span><span class="sxs-lookup"><span data-stu-id="566a1-168">Yes</span></span> |
| <span data-ttu-id="566a1-169">query</span><span class="sxs-lookup"><span data-stu-id="566a1-169">query</span></span> | <span data-ttu-id="566a1-170">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="566a1-170">Use the custom SQL query to read data.</span></span> <span data-ttu-id="566a1-171">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="566a1-171">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="566a1-172">Yes</span><span class="sxs-lookup"><span data-stu-id="566a1-172">Yes</span></span> |

<span data-ttu-id="566a1-173">**Example:**</span><span class="sxs-lookup"><span data-stu-id="566a1-173">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromJira",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Jira input dataset name>",
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
                "type": "JiraSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="566a1-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="566a1-174">Next steps</span></span>
<span data-ttu-id="566a1-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="566a1-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
