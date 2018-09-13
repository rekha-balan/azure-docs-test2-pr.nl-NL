---
title: Copy data from Xero using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Xero to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 17341e8431ffd5cc41fdda86a7511688dcabaf45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866315"
---
# <a name="copy-data-from-xero-using-azure-data-factory"></a><span data-ttu-id="9776a-103">Copy data from Xero using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9776a-103">Copy data from Xero using Azure Data Factory</span></span>

<span data-ttu-id="9776a-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Xero.</span><span class="sxs-lookup"><span data-stu-id="9776a-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Xero.</span></span> <span data-ttu-id="9776a-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="9776a-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9776a-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="9776a-106">This connector is currently in preview.</span></span> <span data-ttu-id="9776a-107">You can try it out and provide feedback.</span><span class="sxs-lookup"><span data-stu-id="9776a-107">You can try it out and provide feedback.</span></span> <span data-ttu-id="9776a-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="9776a-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="9776a-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="9776a-109">Supported capabilities</span></span>

<span data-ttu-id="9776a-110">You can copy data from Xero to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="9776a-110">You can copy data from Xero to any supported sink data store.</span></span> <span data-ttu-id="9776a-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="9776a-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="9776a-112">Specifically, this Xero connector supports:</span><span class="sxs-lookup"><span data-stu-id="9776a-112">Specifically, this Xero connector supports:</span></span>

- <span data-ttu-id="9776a-113">Xero [private application](https://developer.xero.com/documentation/getting-started/api-application-types) but not public application.</span><span class="sxs-lookup"><span data-stu-id="9776a-113">Xero [private application](https://developer.xero.com/documentation/getting-started/api-application-types) but not public application.</span></span>
- <span data-ttu-id="9776a-114">All Xero tables (API endpoints) except "Reports".</span><span class="sxs-lookup"><span data-stu-id="9776a-114">All Xero tables (API endpoints) except "Reports".</span></span> 

<span data-ttu-id="9776a-115">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="9776a-115">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9776a-116">Getting started</span><span class="sxs-lookup"><span data-stu-id="9776a-116">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="9776a-117">The following sections provide details about properties that are used to define Data Factory entities specific to Xero connector.</span><span class="sxs-lookup"><span data-stu-id="9776a-117">The following sections provide details about properties that are used to define Data Factory entities specific to Xero connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9776a-118">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="9776a-118">Linked service properties</span></span>

<span data-ttu-id="9776a-119">The following properties are supported for Xero linked service:</span><span class="sxs-lookup"><span data-stu-id="9776a-119">The following properties are supported for Xero linked service:</span></span>

| <span data-ttu-id="9776a-120">Property</span><span class="sxs-lookup"><span data-stu-id="9776a-120">Property</span></span> | <span data-ttu-id="9776a-121">Description</span><span class="sxs-lookup"><span data-stu-id="9776a-121">Description</span></span> | <span data-ttu-id="9776a-122">Required</span><span class="sxs-lookup"><span data-stu-id="9776a-122">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9776a-123">type</span><span class="sxs-lookup"><span data-stu-id="9776a-123">type</span></span> | <span data-ttu-id="9776a-124">The type property must be set to: **Xero**</span><span class="sxs-lookup"><span data-stu-id="9776a-124">The type property must be set to: **Xero**</span></span> | <span data-ttu-id="9776a-125">Yes</span><span class="sxs-lookup"><span data-stu-id="9776a-125">Yes</span></span> |
| <span data-ttu-id="9776a-126">host</span><span class="sxs-lookup"><span data-stu-id="9776a-126">host</span></span> | <span data-ttu-id="9776a-127">The endpoint of the Xero server (`api.xero.com`).</span><span class="sxs-lookup"><span data-stu-id="9776a-127">The endpoint of the Xero server (`api.xero.com`).</span></span>  | <span data-ttu-id="9776a-128">Yes</span><span class="sxs-lookup"><span data-stu-id="9776a-128">Yes</span></span> |
| <span data-ttu-id="9776a-129">consumerKey</span><span class="sxs-lookup"><span data-stu-id="9776a-129">consumerKey</span></span> | <span data-ttu-id="9776a-130">The consumer key associated with the Xero application.</span><span class="sxs-lookup"><span data-stu-id="9776a-130">The consumer key associated with the Xero application.</span></span> <span data-ttu-id="9776a-131">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="9776a-131">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="9776a-132">Yes</span><span class="sxs-lookup"><span data-stu-id="9776a-132">Yes</span></span> |
| <span data-ttu-id="9776a-133">privateKey</span><span class="sxs-lookup"><span data-stu-id="9776a-133">privateKey</span></span> | <span data-ttu-id="9776a-134">The private key from the .pem file that was generated for your Xero private application, see [Create a public/private key pair](https://developer.xero.com/documentation/api-guides/create-publicprivate-key).</span><span class="sxs-lookup"><span data-stu-id="9776a-134">The private key from the .pem file that was generated for your Xero private application, see [Create a public/private key pair](https://developer.xero.com/documentation/api-guides/create-publicprivate-key).</span></span> <span data-ttu-id="9776a-135">Note to **generate the privatekey.pem with numbits of 512** using `openssl genrsa -out privatekey.pem 512`; 1024 is not supported.</span><span class="sxs-lookup"><span data-stu-id="9776a-135">Note to **generate the privatekey.pem with numbits of 512** using `openssl genrsa -out privatekey.pem 512`; 1024 is not supported.</span></span> <span data-ttu-id="9776a-136">Include all the text from the .pem file including the Unix line endings(\n), see sample below.</span><span class="sxs-lookup"><span data-stu-id="9776a-136">Include all the text from the .pem file including the Unix line endings(\n), see sample below.</span></span><br/><br/><span data-ttu-id="9776a-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="9776a-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="9776a-138">Yes</span><span class="sxs-lookup"><span data-stu-id="9776a-138">Yes</span></span> |
| <span data-ttu-id="9776a-139">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="9776a-139">useEncryptedEndpoints</span></span> | <span data-ttu-id="9776a-140">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9776a-140">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="9776a-141">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="9776a-141">The default value is true.</span></span>  | <span data-ttu-id="9776a-142">No</span><span class="sxs-lookup"><span data-stu-id="9776a-142">No</span></span> |
| <span data-ttu-id="9776a-143">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="9776a-143">useHostVerification</span></span> | <span data-ttu-id="9776a-144">Specifies whether the host name is required in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="9776a-144">Specifies whether the host name is required in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="9776a-145">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="9776a-145">The default value is true.</span></span>  | <span data-ttu-id="9776a-146">No</span><span class="sxs-lookup"><span data-stu-id="9776a-146">No</span></span> |
| <span data-ttu-id="9776a-147">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="9776a-147">usePeerVerification</span></span> | <span data-ttu-id="9776a-148">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="9776a-148">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="9776a-149">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="9776a-149">The default value is true.</span></span>  | <span data-ttu-id="9776a-150">No</span><span class="sxs-lookup"><span data-stu-id="9776a-150">No</span></span> |

<span data-ttu-id="9776a-151">**Example:**</span><span class="sxs-lookup"><span data-stu-id="9776a-151">**Example:**</span></span>

```json
{
    "name": "XeroLinkedService",
    "properties": {
        "type": "Xero",
        "typeProperties": {
            "host" : "api.xero.com",
            "consumerKey": {
                 "type": "SecureString",
                 "value": "<consumerKey>"
            },
            "privateKey": {
                 "type": "SecureString",
                 "value": "<privateKey>"
            }
        }
    }
}
```

<span data-ttu-id="9776a-152">**Sample private key value:**</span><span class="sxs-lookup"><span data-stu-id="9776a-152">**Sample private key value:**</span></span>

<span data-ttu-id="9776a-153">Include all the text from the .pem file including the Unix line endings(\n).</span><span class="sxs-lookup"><span data-stu-id="9776a-153">Include all the text from the .pem file including the Unix line endings(\n).</span></span>

```
"-----BEGIN RSA PRIVATE KEY-----\nMII***************************************************P\nbu****************************************************s\nU/****************************************************B\nA*****************************************************W\njH****************************************************e\nsx*****************************************************l\nq******************************************************X\nh*****************************************************i\nd*****************************************************s\nA*****************************************************dsfb\nN*****************************************************M\np*****************************************************Ly\nK*****************************************************Y=\n-----END RSA PRIVATE KEY-----"
```

## <a name="dataset-properties"></a><span data-ttu-id="9776a-154">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="9776a-154">Dataset properties</span></span>

<span data-ttu-id="9776a-155">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="9776a-155">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="9776a-156">This section provides a list of properties supported by Xero dataset.</span><span class="sxs-lookup"><span data-stu-id="9776a-156">This section provides a list of properties supported by Xero dataset.</span></span>

<span data-ttu-id="9776a-157">To copy data from Xero, set the type property of the dataset to **XeroObject**.</span><span class="sxs-lookup"><span data-stu-id="9776a-157">To copy data from Xero, set the type property of the dataset to **XeroObject**.</span></span> <span data-ttu-id="9776a-158">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="9776a-158">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="9776a-159">**Example**</span><span class="sxs-lookup"><span data-stu-id="9776a-159">**Example**</span></span>

```json
{
    "name": "XeroDataset",
    "properties": {
        "type": "XeroObject",
        "linkedServiceName": {
            "referenceName": "<Xero linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="9776a-160">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="9776a-160">Copy activity properties</span></span>

<span data-ttu-id="9776a-161">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="9776a-161">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="9776a-162">This section provides a list of properties supported by Xero source.</span><span class="sxs-lookup"><span data-stu-id="9776a-162">This section provides a list of properties supported by Xero source.</span></span>

### <a name="xero-as-source"></a><span data-ttu-id="9776a-163">Xero as source</span><span class="sxs-lookup"><span data-stu-id="9776a-163">Xero as source</span></span>

<span data-ttu-id="9776a-164">To copy data from Xero, set the source type in the copy activity to **XeroSource**.</span><span class="sxs-lookup"><span data-stu-id="9776a-164">To copy data from Xero, set the source type in the copy activity to **XeroSource**.</span></span> <span data-ttu-id="9776a-165">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="9776a-165">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="9776a-166">Property</span><span class="sxs-lookup"><span data-stu-id="9776a-166">Property</span></span> | <span data-ttu-id="9776a-167">Description</span><span class="sxs-lookup"><span data-stu-id="9776a-167">Description</span></span> | <span data-ttu-id="9776a-168">Required</span><span class="sxs-lookup"><span data-stu-id="9776a-168">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9776a-169">type</span><span class="sxs-lookup"><span data-stu-id="9776a-169">type</span></span> | <span data-ttu-id="9776a-170">The type property of the copy activity source must be set to: **XeroSource**</span><span class="sxs-lookup"><span data-stu-id="9776a-170">The type property of the copy activity source must be set to: **XeroSource**</span></span> | <span data-ttu-id="9776a-171">Yes</span><span class="sxs-lookup"><span data-stu-id="9776a-171">Yes</span></span> |
| <span data-ttu-id="9776a-172">query</span><span class="sxs-lookup"><span data-stu-id="9776a-172">query</span></span> | <span data-ttu-id="9776a-173">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="9776a-173">Use the custom SQL query to read data.</span></span> <span data-ttu-id="9776a-174">For example: `"SELECT * FROM Contacts"`.</span><span class="sxs-lookup"><span data-stu-id="9776a-174">For example: `"SELECT * FROM Contacts"`.</span></span> | <span data-ttu-id="9776a-175">Yes</span><span class="sxs-lookup"><span data-stu-id="9776a-175">Yes</span></span> |

<span data-ttu-id="9776a-176">**Example:**</span><span class="sxs-lookup"><span data-stu-id="9776a-176">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromXero",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Xero input dataset name>",
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
                "type": "XeroSource",
                "query": "SELECT * FROM Contacts"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

<span data-ttu-id="9776a-177">Note the following when specifying the Xero query:</span><span class="sxs-lookup"><span data-stu-id="9776a-177">Note the following when specifying the Xero query:</span></span>

- <span data-ttu-id="9776a-178">Tables with complex items will be split to multiple tables.</span><span class="sxs-lookup"><span data-stu-id="9776a-178">Tables with complex items will be split to multiple tables.</span></span> <span data-ttu-id="9776a-179">For example, Bank transactions has a complex data structure "LineItems", so data of bank transaction is mapped to table `Bank_Transaction` and `Bank_Transaction_Line_Items`, with `Bank_Transaction_ID` as foreign key to link them together.</span><span class="sxs-lookup"><span data-stu-id="9776a-179">For example, Bank transactions has a complex data structure "LineItems", so data of bank transaction is mapped to table `Bank_Transaction` and `Bank_Transaction_Line_Items`, with `Bank_Transaction_ID` as foreign key to link them together.</span></span>

- <span data-ttu-id="9776a-180">Xero data is available through two schemas: `Minimal` (default) and `Complete`.</span><span class="sxs-lookup"><span data-stu-id="9776a-180">Xero data is available through two schemas: `Minimal` (default) and `Complete`.</span></span> <span data-ttu-id="9776a-181">The Complete schema contains prerequisite call tables which require additional data (e.g. ID column) before making the desired query.</span><span class="sxs-lookup"><span data-stu-id="9776a-181">The Complete schema contains prerequisite call tables which require additional data (e.g. ID column) before making the desired query.</span></span>

<span data-ttu-id="9776a-182">The following tables have the same information in the Minimal and Complete schema.</span><span class="sxs-lookup"><span data-stu-id="9776a-182">The following tables have the same information in the Minimal and Complete schema.</span></span> <span data-ttu-id="9776a-183">To reduce the number of API calls, use Minimal schema (default).</span><span class="sxs-lookup"><span data-stu-id="9776a-183">To reduce the number of API calls, use Minimal schema (default).</span></span>

- <span data-ttu-id="9776a-184">Bank_Transactions</span><span class="sxs-lookup"><span data-stu-id="9776a-184">Bank_Transactions</span></span>
- <span data-ttu-id="9776a-185">Contact_Groups</span><span class="sxs-lookup"><span data-stu-id="9776a-185">Contact_Groups</span></span> 
- <span data-ttu-id="9776a-186">Contacts</span><span class="sxs-lookup"><span data-stu-id="9776a-186">Contacts</span></span> 
- <span data-ttu-id="9776a-187">Contacts_Sales_Tracking_Categories</span><span class="sxs-lookup"><span data-stu-id="9776a-187">Contacts_Sales_Tracking_Categories</span></span> 
- <span data-ttu-id="9776a-188">Contacts_Phones</span><span class="sxs-lookup"><span data-stu-id="9776a-188">Contacts_Phones</span></span> 
- <span data-ttu-id="9776a-189">Contacts_Addresses</span><span class="sxs-lookup"><span data-stu-id="9776a-189">Contacts_Addresses</span></span> 
- <span data-ttu-id="9776a-190">Contacts_Purchases_Tracking_Categories</span><span class="sxs-lookup"><span data-stu-id="9776a-190">Contacts_Purchases_Tracking_Categories</span></span> 
- <span data-ttu-id="9776a-191">Credit_Notes</span><span class="sxs-lookup"><span data-stu-id="9776a-191">Credit_Notes</span></span> 
- <span data-ttu-id="9776a-192">Credit_Notes_Allocations</span><span class="sxs-lookup"><span data-stu-id="9776a-192">Credit_Notes_Allocations</span></span> 
- <span data-ttu-id="9776a-193">Expense_Claims</span><span class="sxs-lookup"><span data-stu-id="9776a-193">Expense_Claims</span></span> 
- <span data-ttu-id="9776a-194">Expense_Claim_Validation_Errors</span><span class="sxs-lookup"><span data-stu-id="9776a-194">Expense_Claim_Validation_Errors</span></span>
- <span data-ttu-id="9776a-195">Invoices</span><span class="sxs-lookup"><span data-stu-id="9776a-195">Invoices</span></span> 
- <span data-ttu-id="9776a-196">Invoices_Credit_Notes</span><span class="sxs-lookup"><span data-stu-id="9776a-196">Invoices_Credit_Notes</span></span>
- <span data-ttu-id="9776a-197">Invoices_ Prepayments</span><span class="sxs-lookup"><span data-stu-id="9776a-197">Invoices_ Prepayments</span></span> 
- <span data-ttu-id="9776a-198">Invoices_Overpayments</span><span class="sxs-lookup"><span data-stu-id="9776a-198">Invoices_Overpayments</span></span> 
- <span data-ttu-id="9776a-199">Manual_Journals</span><span class="sxs-lookup"><span data-stu-id="9776a-199">Manual_Journals</span></span> 
- <span data-ttu-id="9776a-200">Overpayments</span><span class="sxs-lookup"><span data-stu-id="9776a-200">Overpayments</span></span> 
- <span data-ttu-id="9776a-201">Overpayments_Allocations</span><span class="sxs-lookup"><span data-stu-id="9776a-201">Overpayments_Allocations</span></span> 
- <span data-ttu-id="9776a-202">Prepayments</span><span class="sxs-lookup"><span data-stu-id="9776a-202">Prepayments</span></span> 
- <span data-ttu-id="9776a-203">Prepayments_Allocations</span><span class="sxs-lookup"><span data-stu-id="9776a-203">Prepayments_Allocations</span></span> 
- <span data-ttu-id="9776a-204">Receipts</span><span class="sxs-lookup"><span data-stu-id="9776a-204">Receipts</span></span> 
- <span data-ttu-id="9776a-205">Receipt_Validation_Errors</span><span class="sxs-lookup"><span data-stu-id="9776a-205">Receipt_Validation_Errors</span></span> 
- <span data-ttu-id="9776a-206">Tracking_Categories</span><span class="sxs-lookup"><span data-stu-id="9776a-206">Tracking_Categories</span></span>

<span data-ttu-id="9776a-207">The following tables can only be queried with complete schema:</span><span class="sxs-lookup"><span data-stu-id="9776a-207">The following tables can only be queried with complete schema:</span></span>

- <span data-ttu-id="9776a-208">Complete.Bank_Transaction_Line_Items</span><span class="sxs-lookup"><span data-stu-id="9776a-208">Complete.Bank_Transaction_Line_Items</span></span> 
- <span data-ttu-id="9776a-209">Complete.Bank_Transaction_Line_Item_Tracking</span><span class="sxs-lookup"><span data-stu-id="9776a-209">Complete.Bank_Transaction_Line_Item_Tracking</span></span> 
- <span data-ttu-id="9776a-210">Complete.Contact_Group_Contacts</span><span class="sxs-lookup"><span data-stu-id="9776a-210">Complete.Contact_Group_Contacts</span></span> 
- <span data-ttu-id="9776a-211">Complete.Contacts_Contact_ Persons</span><span class="sxs-lookup"><span data-stu-id="9776a-211">Complete.Contacts_Contact_ Persons</span></span> 
- <span data-ttu-id="9776a-212">Complete.Credit_Note_Line_Items</span><span class="sxs-lookup"><span data-stu-id="9776a-212">Complete.Credit_Note_Line_Items</span></span> 
- <span data-ttu-id="9776a-213">Complete.Credit_Notes_Line_Items_Tracking</span><span class="sxs-lookup"><span data-stu-id="9776a-213">Complete.Credit_Notes_Line_Items_Tracking</span></span> 
- <span data-ttu-id="9776a-214">Complete.Expense_Claim_ Payments</span><span class="sxs-lookup"><span data-stu-id="9776a-214">Complete.Expense_Claim_ Payments</span></span> 
- <span data-ttu-id="9776a-215">Complete.Expense_Claim_Receipts</span><span class="sxs-lookup"><span data-stu-id="9776a-215">Complete.Expense_Claim_Receipts</span></span> 
- <span data-ttu-id="9776a-216">Complete.Invoice_Line_Items</span><span class="sxs-lookup"><span data-stu-id="9776a-216">Complete.Invoice_Line_Items</span></span> 
- <span data-ttu-id="9776a-217">Complete.Invoices_Line_Items_Tracking</span><span class="sxs-lookup"><span data-stu-id="9776a-217">Complete.Invoices_Line_Items_Tracking</span></span>
- <span data-ttu-id="9776a-218">Complete.Manual_Journal_Lines</span><span class="sxs-lookup"><span data-stu-id="9776a-218">Complete.Manual_Journal_Lines</span></span> 
- <span data-ttu-id="9776a-219">Complete.Manual_Journal_Line_Tracking</span><span class="sxs-lookup"><span data-stu-id="9776a-219">Complete.Manual_Journal_Line_Tracking</span></span> 
- <span data-ttu-id="9776a-220">Complete.Overpayment_Line_Items</span><span class="sxs-lookup"><span data-stu-id="9776a-220">Complete.Overpayment_Line_Items</span></span> 
- <span data-ttu-id="9776a-221">Complete.Overpayment_Line_Items_Tracking</span><span class="sxs-lookup"><span data-stu-id="9776a-221">Complete.Overpayment_Line_Items_Tracking</span></span> 
- <span data-ttu-id="9776a-222">Complete.Prepayment_Line_Items</span><span class="sxs-lookup"><span data-stu-id="9776a-222">Complete.Prepayment_Line_Items</span></span> 
- <span data-ttu-id="9776a-223">Complete.Prepayment_Line_Item_Tracking</span><span class="sxs-lookup"><span data-stu-id="9776a-223">Complete.Prepayment_Line_Item_Tracking</span></span> 
- <span data-ttu-id="9776a-224">Complete.Receipt_Line_Items</span><span class="sxs-lookup"><span data-stu-id="9776a-224">Complete.Receipt_Line_Items</span></span> 
- <span data-ttu-id="9776a-225">Complete.Receipt_Line_Item_Tracking</span><span class="sxs-lookup"><span data-stu-id="9776a-225">Complete.Receipt_Line_Item_Tracking</span></span> 
- <span data-ttu-id="9776a-226">Complete.Tracking_Category_Options</span><span class="sxs-lookup"><span data-stu-id="9776a-226">Complete.Tracking_Category_Options</span></span>

## <a name="next-steps"></a><span data-ttu-id="9776a-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="9776a-227">Next steps</span></span>
<span data-ttu-id="9776a-228">For a list of supported data stores by the copy activity, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9776a-228">For a list of supported data stores by the copy activity, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
