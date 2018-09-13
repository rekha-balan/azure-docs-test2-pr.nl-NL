---
title: Create or modify labs automatically using Azure Resource Manager templates with PowerShell | Microsoft Docs
description: Learn how to use Azure Resource Manager templates with PowerShell to create or modify labs automatically in a DevTest lab
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 7cf6e5569e9d47b2a279f39cf837a4c0558bf3c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867040"
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="e7f8c-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f8c-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="e7f8c-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="e7f8c-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="e7f8c-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="e7f8c-107">Step 1: Gather your templates and scripts</span><span class="sxs-lookup"><span data-stu-id="e7f8c-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="e7f8c-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span><span class="sxs-lookup"><span data-stu-id="e7f8c-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="e7f8c-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="e7f8c-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="e7f8c-110">Step 2: Modify your Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="e7f8c-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="e7f8c-111">You can follow the steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-111">You can follow the steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="e7f8c-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="e7f8c-113">Typically, you will use a variation of one of the approaches or examples provided and modify your template for your needs.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-113">Typically, you will use a variation of one of the approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="e7f8c-114">Step 3: Deploy resources with PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f8c-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="e7f8c-115">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="e7f8c-115">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="e7f8c-116">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-116">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="e7f8c-117">Common tasks you can perform in DevTest labs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f8c-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="e7f8c-118">There are many other common tasks that you can automate by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="e7f8c-119">The following sections of the documentation outline the steps required to perform these tasks.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-119">The following sections of the documentation outline the steps required to perform these tasks.</span></span>

* [<span data-ttu-id="e7f8c-120">Create a custom image from a VHD file using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f8c-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="e7f8c-121">Upload VHD file to lab's storage account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f8c-121">Upload VHD file to lab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="e7f8c-122">Add an external user to a lab using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f8c-122">Add an external user to a lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="e7f8c-123">Create a lab custom role using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f8c-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="e7f8c-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7f8c-124">Next steps</span></span>
* <span data-ttu-id="e7f8c-125">Learn how to create a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span><span class="sxs-lookup"><span data-stu-id="e7f8c-125">Learn how to create a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="e7f8c-126">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e7f8c-126">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
