---
title: Store credentials in Azure Key Vault | Microsoft Docs
description: Learn how to store credentials for data stores used in an Azure key vault that Azure Data Factory can automatically retrieve at runtime.
services: data-factory
author: linda33wj
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/25/2017
ms.author: jingwang
ms.openlocfilehash: e1be16ec6a7536cedf3a27ffacb9c4dffe42bbef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856833"
---
# <a name="store-credential-in-azure-key-vault"></a><span data-ttu-id="fb7f7-103">Store credential in Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="fb7f7-103">Store credential in Azure Key Vault</span></span>

<span data-ttu-id="fb7f7-104">You can store credentials for data stores and computes in an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb7f7-104">You can store credentials for data stores and computes in an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="fb7f7-105">Azure Data Factory retrieves the credentials when executing an activity that uses the data store/compute.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-105">Azure Data Factory retrieves the credentials when executing an activity that uses the data store/compute.</span></span>

<span data-ttu-id="fb7f7-106">Currently, all activity types except custom activity support this feature.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-106">Currently, all activity types except custom activity support this feature.</span></span> <span data-ttu-id="fb7f7-107">For connector configuration specifically, check the "linked service properties" section in [each connector topic](copy-activity-overview.md#supported-data-stores-and-formats) for details.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-107">For connector configuration specifically, check the "linked service properties" section in [each connector topic](copy-activity-overview.md#supported-data-stores-and-formats) for details.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb7f7-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fb7f7-108">Prerequisites</span></span>

<span data-ttu-id="fb7f7-109">This feature relies on the data factory service identity.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-109">This feature relies on the data factory service identity.</span></span> <span data-ttu-id="fb7f7-110">Learn how it works from [Data factory service identity](data-factory-service-identity.md) and make sure your data factory have an associated one.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-110">Learn how it works from [Data factory service identity](data-factory-service-identity.md) and make sure your data factory have an associated one.</span></span>

>[!TIP]
><span data-ttu-id="fb7f7-111">In Azure Key Vault, when you create a secret, **put the entire value of a secret property that ADF linked service asks for (e.g. connection string/password/service principal key/etc)**.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-111">In Azure Key Vault, when you create a secret, **put the entire value of a secret property that ADF linked service asks for (e.g. connection string/password/service principal key/etc)**.</span></span> <span data-ttu-id="fb7f7-112">For example, for Azure Storage linked service, put `DefaultEndpointsProtocol=http;AccountName=myAccount;AccountKey=myKey;` as AKV secret, then reference in "connectionString" field from ADF; for Dynamics linked service, put `myPassword` as AKV secret, then reference in "paassword" field from ADF.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-112">For example, for Azure Storage linked service, put `DefaultEndpointsProtocol=http;AccountName=myAccount;AccountKey=myKey;` as AKV secret, then reference in "connectionString" field from ADF; for Dynamics linked service, put `myPassword` as AKV secret, then reference in "paassword" field from ADF.</span></span> <span data-ttu-id="fb7f7-113">Refer to each connector/compute article on supported property details.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-113">Refer to each connector/compute article on supported property details.</span></span>

## <a name="steps"></a><span data-ttu-id="fb7f7-114">Steps</span><span class="sxs-lookup"><span data-stu-id="fb7f7-114">Steps</span></span>

<span data-ttu-id="fb7f7-115">To reference a credential stored in Azure Key Vault, you need to:</span><span class="sxs-lookup"><span data-stu-id="fb7f7-115">To reference a credential stored in Azure Key Vault, you need to:</span></span>

1. <span data-ttu-id="fb7f7-116">**Retrieve data factory service identity** by copying the value of "SERVICE IDENTITY APPLICATION ID" generated along with your factory.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-116">**Retrieve data factory service identity** by copying the value of "SERVICE IDENTITY APPLICATION ID" generated along with your factory.</span></span> <span data-ttu-id="fb7f7-117">If you use ADF authoring UI, the service identity ID will be shown on the Azure Key Vault linked service creation window; you can also retrieve it from Azure portal, refer to [Retrieve data factory service identity](data-factory-service-identity.md#retrieve-service-identity).</span><span class="sxs-lookup"><span data-stu-id="fb7f7-117">If you use ADF authoring UI, the service identity ID will be shown on the Azure Key Vault linked service creation window; you can also retrieve it from Azure portal, refer to [Retrieve data factory service identity](data-factory-service-identity.md#retrieve-service-identity).</span></span>
2. <span data-ttu-id="fb7f7-118">**Grant the service identity access to your Azure Key Vault.**</span><span class="sxs-lookup"><span data-stu-id="fb7f7-118">**Grant the service identity access to your Azure Key Vault.**</span></span> <span data-ttu-id="fb7f7-119">In your key vault -> Access policies -> Add new -> search this service identity application ID to grant **Get** permission in Secret permissions dropdown.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-119">In your key vault -> Access policies -> Add new -> search this service identity application ID to grant **Get** permission in Secret permissions dropdown.</span></span> <span data-ttu-id="fb7f7-120">It allows this designated factory to access secret in key vault.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-120">It allows this designated factory to access secret in key vault.</span></span>
3. <span data-ttu-id="fb7f7-121">**Create a linked service pointing to your Azure Key Vault.**</span><span class="sxs-lookup"><span data-stu-id="fb7f7-121">**Create a linked service pointing to your Azure Key Vault.**</span></span> <span data-ttu-id="fb7f7-122">Refer to [Azure Key Vault linked service](#azure-key-vault-linked-service).</span><span class="sxs-lookup"><span data-stu-id="fb7f7-122">Refer to [Azure Key Vault linked service](#azure-key-vault-linked-service).</span></span>
4. <span data-ttu-id="fb7f7-123">**Create data store linked service, inside which reference the corresponding secret stored in key vault.**</span><span class="sxs-lookup"><span data-stu-id="fb7f7-123">**Create data store linked service, inside which reference the corresponding secret stored in key vault.**</span></span> <span data-ttu-id="fb7f7-124">Refer to [reference secret stored in key vault](#reference-secret-stored-in-key-vault).</span><span class="sxs-lookup"><span data-stu-id="fb7f7-124">Refer to [reference secret stored in key vault](#reference-secret-stored-in-key-vault).</span></span>

## <a name="azure-key-vault-linked-service"></a><span data-ttu-id="fb7f7-125">Azure Key Vault linked service</span><span class="sxs-lookup"><span data-stu-id="fb7f7-125">Azure Key Vault linked service</span></span>

<span data-ttu-id="fb7f7-126">The following properties are supported for Azure Key Vault linked service:</span><span class="sxs-lookup"><span data-stu-id="fb7f7-126">The following properties are supported for Azure Key Vault linked service:</span></span>

| <span data-ttu-id="fb7f7-127">Property</span><span class="sxs-lookup"><span data-stu-id="fb7f7-127">Property</span></span> | <span data-ttu-id="fb7f7-128">Description</span><span class="sxs-lookup"><span data-stu-id="fb7f7-128">Description</span></span> | <span data-ttu-id="fb7f7-129">Required</span><span class="sxs-lookup"><span data-stu-id="fb7f7-129">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fb7f7-130">type</span><span class="sxs-lookup"><span data-stu-id="fb7f7-130">type</span></span> | <span data-ttu-id="fb7f7-131">The type property must be set to: **AzureKeyVault**.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-131">The type property must be set to: **AzureKeyVault**.</span></span> | <span data-ttu-id="fb7f7-132">Yes</span><span class="sxs-lookup"><span data-stu-id="fb7f7-132">Yes</span></span> |
| <span data-ttu-id="fb7f7-133">baseUrl</span><span class="sxs-lookup"><span data-stu-id="fb7f7-133">baseUrl</span></span> | <span data-ttu-id="fb7f7-134">Specify the Azure Key Vault URL.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-134">Specify the Azure Key Vault URL.</span></span> | <span data-ttu-id="fb7f7-135">Yes</span><span class="sxs-lookup"><span data-stu-id="fb7f7-135">Yes</span></span> |

<span data-ttu-id="fb7f7-136">**Using authoring UI:**</span><span class="sxs-lookup"><span data-stu-id="fb7f7-136">**Using authoring UI:**</span></span>

<span data-ttu-id="fb7f7-137">Click **Connections** -> **Linked Services** -> **+New** -> search for "Azure Key Vault":</span><span class="sxs-lookup"><span data-stu-id="fb7f7-137">Click **Connections** -> **Linked Services** -> **+New** -> search for "Azure Key Vault":</span></span>

![Search AKV](media/store-credentials-in-key-vault/search-akv.png)

<span data-ttu-id="fb7f7-139">Select the provisioned Azure Key Vault where your credentials are stored.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-139">Select the provisioned Azure Key Vault where your credentials are stored.</span></span> <span data-ttu-id="fb7f7-140">You can do **Test Connection** to make sure your AKV connection is valid.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-140">You can do **Test Connection** to make sure your AKV connection is valid.</span></span> 

![Configure AKV](media/store-credentials-in-key-vault/configure-akv.png)

<span data-ttu-id="fb7f7-142">**JSON example:**</span><span class="sxs-lookup"><span data-stu-id="fb7f7-142">**JSON example:**</span></span>

```json
{
    "name": "AzureKeyVaultLinkedService",
    "properties": {
        "type": "AzureKeyVault",
        "typeProperties": {
            "baseUrl": "https://<azureKeyVaultName>.vault.azure.net"
        }
    }
}
```

## <a name="reference-secret-stored-in-key-vault"></a><span data-ttu-id="fb7f7-143">Reference secret stored in key vault</span><span class="sxs-lookup"><span data-stu-id="fb7f7-143">Reference secret stored in key vault</span></span>

<span data-ttu-id="fb7f7-144">The following properties are supported when you configure a field in linked service referencing a key vault secret:</span><span class="sxs-lookup"><span data-stu-id="fb7f7-144">The following properties are supported when you configure a field in linked service referencing a key vault secret:</span></span>

| <span data-ttu-id="fb7f7-145">Property</span><span class="sxs-lookup"><span data-stu-id="fb7f7-145">Property</span></span> | <span data-ttu-id="fb7f7-146">Description</span><span class="sxs-lookup"><span data-stu-id="fb7f7-146">Description</span></span> | <span data-ttu-id="fb7f7-147">Required</span><span class="sxs-lookup"><span data-stu-id="fb7f7-147">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fb7f7-148">type</span><span class="sxs-lookup"><span data-stu-id="fb7f7-148">type</span></span> | <span data-ttu-id="fb7f7-149">The type property of the field must be set to: **AzureKeyVaultSecret**.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-149">The type property of the field must be set to: **AzureKeyVaultSecret**.</span></span> | <span data-ttu-id="fb7f7-150">Yes</span><span class="sxs-lookup"><span data-stu-id="fb7f7-150">Yes</span></span> |
| <span data-ttu-id="fb7f7-151">secretName</span><span class="sxs-lookup"><span data-stu-id="fb7f7-151">secretName</span></span> | <span data-ttu-id="fb7f7-152">The name of secret in azure key vault.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-152">The name of secret in azure key vault.</span></span> | <span data-ttu-id="fb7f7-153">Yes</span><span class="sxs-lookup"><span data-stu-id="fb7f7-153">Yes</span></span> |
| <span data-ttu-id="fb7f7-154">secretVersion</span><span class="sxs-lookup"><span data-stu-id="fb7f7-154">secretVersion</span></span> | <span data-ttu-id="fb7f7-155">The version of secret in azure key vault.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-155">The version of secret in azure key vault.</span></span><br/><span data-ttu-id="fb7f7-156">If not specified, it always uses the latest version of the secret.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-156">If not specified, it always uses the latest version of the secret.</span></span><br/><span data-ttu-id="fb7f7-157">If specified, then it sticks to the given version.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-157">If specified, then it sticks to the given version.</span></span>| <span data-ttu-id="fb7f7-158">No</span><span class="sxs-lookup"><span data-stu-id="fb7f7-158">No</span></span> |
| <span data-ttu-id="fb7f7-159">store</span><span class="sxs-lookup"><span data-stu-id="fb7f7-159">store</span></span> | <span data-ttu-id="fb7f7-160">Refers to an Azure Key Vault linked service that you use to store the credential.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-160">Refers to an Azure Key Vault linked service that you use to store the credential.</span></span> | <span data-ttu-id="fb7f7-161">Yes</span><span class="sxs-lookup"><span data-stu-id="fb7f7-161">Yes</span></span> |

<span data-ttu-id="fb7f7-162">**Using authoring UI:**</span><span class="sxs-lookup"><span data-stu-id="fb7f7-162">**Using authoring UI:**</span></span>

<span data-ttu-id="fb7f7-163">Select **Azure Key Vault** for secret fields while creating the connection to your data store/compute.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-163">Select **Azure Key Vault** for secret fields while creating the connection to your data store/compute.</span></span> <span data-ttu-id="fb7f7-164">Select the provisioned Azure Key Vault Linked Service and provide the **Secret name**.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-164">Select the provisioned Azure Key Vault Linked Service and provide the **Secret name**.</span></span> <span data-ttu-id="fb7f7-165">You can optionally provide a secret version as well.</span><span class="sxs-lookup"><span data-stu-id="fb7f7-165">You can optionally provide a secret version as well.</span></span> 

![Configure AKV secret](media/store-credentials-in-key-vault/configure-akv-secret.png)

<span data-ttu-id="fb7f7-167">**JSON example: (see the "password" section)**</span><span class="sxs-lookup"><span data-stu-id="fb7f7-167">**JSON example: (see the "password" section)**</span></span>

```json
{
    "name": "DynamicsLinkedService",
    "properties": {
        "type": "Dynamics",
        "typeProperties": {
            "deploymentType": "<>",
            "organizationName": "<>",
            "authenticationType": "<>",
            "username": "<>",
            "password": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="fb7f7-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb7f7-168">Next steps</span></span>
<span data-ttu-id="fb7f7-169">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fb7f7-169">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
