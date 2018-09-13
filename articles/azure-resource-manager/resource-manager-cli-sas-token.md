---
title: Deploy Azure template with SAS token and Azure CLI | Microsoft Docs
description: Use Azure Resource Manager and Azure CLI to deploy resources to Azure from a template that is protected with SAS token.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: d09aa46eabe705082edafe12da8442a79d1080b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870912"
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="0c70c-103">Deploy private Resource Manager template with SAS token and Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0c70c-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="0c70c-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span><span class="sxs-lookup"><span data-stu-id="0c70c-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="0c70c-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span><span class="sxs-lookup"><span data-stu-id="0c70c-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="0c70c-106">Add private template to storage account</span><span class="sxs-lookup"><span data-stu-id="0c70c-106">Add private template to storage account</span></span>

<span data-ttu-id="0c70c-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span><span class="sxs-lookup"><span data-stu-id="0c70c-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c70c-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span><span class="sxs-lookup"><span data-stu-id="0c70c-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="0c70c-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span><span class="sxs-lookup"><span data-stu-id="0c70c-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="0c70c-110">If another user intercepts the URI, that user is able to access the template.</span><span class="sxs-lookup"><span data-stu-id="0c70c-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="0c70c-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span><span class="sxs-lookup"><span data-stu-id="0c70c-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="0c70c-112">The following example sets up a private storage account container and uploads a template:</span><span class="sxs-lookup"><span data-stu-id="0c70c-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="0c70c-113">Provide SAS token during deployment</span><span class="sxs-lookup"><span data-stu-id="0c70c-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="0c70c-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span><span class="sxs-lookup"><span data-stu-id="0c70c-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="0c70c-115">Set the expiry time to allow enough time to complete the deployment.</span><span class="sxs-lookup"><span data-stu-id="0c70c-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="0c70c-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0c70c-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c70c-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c70c-117">Next steps</span></span>
* <span data-ttu-id="0c70c-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0c70c-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="0c70c-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="0c70c-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="0c70c-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="0c70c-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
