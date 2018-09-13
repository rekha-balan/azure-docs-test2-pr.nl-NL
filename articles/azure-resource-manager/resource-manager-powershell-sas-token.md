---
title: Deploy Azure template with SAS token and PowerShell | Microsoft Docs
description: Use Azure Resource Manager and Azure PowerShell to deploy resources to Azure from a template that is protected with SAS token.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: f138cceb88cb9a43efdd3f11b24203378a288286
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866479"
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="73071-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="73071-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="73071-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span><span class="sxs-lookup"><span data-stu-id="73071-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="73071-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span><span class="sxs-lookup"><span data-stu-id="73071-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="73071-106">Add private template to storage account</span><span class="sxs-lookup"><span data-stu-id="73071-106">Add private template to storage account</span></span>

<span data-ttu-id="73071-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span><span class="sxs-lookup"><span data-stu-id="73071-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73071-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span><span class="sxs-lookup"><span data-stu-id="73071-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="73071-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span><span class="sxs-lookup"><span data-stu-id="73071-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="73071-110">If another user intercepts the URI, that user is able to access the template.</span><span class="sxs-lookup"><span data-stu-id="73071-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="73071-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span><span class="sxs-lookup"><span data-stu-id="73071-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="73071-112">The following example sets up a private storage account container and uploads a template:</span><span class="sxs-lookup"><span data-stu-id="73071-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="73071-113">Provide SAS token during deployment</span><span class="sxs-lookup"><span data-stu-id="73071-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="73071-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span><span class="sxs-lookup"><span data-stu-id="73071-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="73071-115">Set the expiry time to allow enough time to complete the deployment.</span><span class="sxs-lookup"><span data-stu-id="73071-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get the URI with the SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="73071-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73071-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="73071-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="73071-117">Next steps</span></span>
* <span data-ttu-id="73071-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="73071-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="73071-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="73071-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="73071-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="73071-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
