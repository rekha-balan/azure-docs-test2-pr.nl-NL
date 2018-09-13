---
title: Create or modify labs automatically using Azure Resource Manager templates with PowerShell | Microsoft Docs
description: Learn how to use Azure Resource Manager templates with PowerShell to create or modify labs automatically in a DevTest lab
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 8f54553bc60d6ba374462d87285dfaf4ca6395c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548846"
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="8504a-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504a-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="8504a-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span><span class="sxs-lookup"><span data-stu-id="8504a-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="8504a-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span><span class="sxs-lookup"><span data-stu-id="8504a-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="8504a-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="8504a-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="8504a-107">Step 1: Gather your templates and scripts</span><span class="sxs-lookup"><span data-stu-id="8504a-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="8504a-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span><span class="sxs-lookup"><span data-stu-id="8504a-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="8504a-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-repo.md).</span><span class="sxs-lookup"><span data-stu-id="8504a-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="8504a-110">Step 2: Modify your Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="8504a-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="8504a-111">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) shows you how to use Azure Resource Manager templates within DevTest labs to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span><span class="sxs-lookup"><span data-stu-id="8504a-111">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) shows you how to use Azure Resource Manager templates within DevTest labs to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span></span>

<span data-ttu-id="8504a-112">For example, if you created a new virtual network and wanted to apply it to all of your existing labs, you could quickly do so by using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="8504a-112">For example, if you created a new virtual network and wanted to apply it to all of your existing labs, you could quickly do so by using an Azure Resource Manager template.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="8504a-113">Step 3: Deploy resources with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504a-113">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="8504a-114">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="8504a-114">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="8504a-115">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span><span class="sxs-lookup"><span data-stu-id="8504a-115">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="8504a-116">Common tasks you can perform in DevTest labs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504a-116">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="8504a-117">There are many other common tasks that you can automate by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8504a-117">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="8504a-118">The following sections of the documentation outline the steps required to perform these tasks.</span><span class="sxs-lookup"><span data-stu-id="8504a-118">The following sections of the documentation outline the steps required to perform these tasks.</span></span>

* [<span data-ttu-id="8504a-119">Create a custom image from a VHD file using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504a-119">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="8504a-120">Upload VHD file to lab's storage account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504a-120">Upload VHD file to lab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="8504a-121">Add an external user to a lab using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504a-121">Add an external user to a lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="8504a-122">Create a lab custom role using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504a-122">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="8504a-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="8504a-123">Next steps</span></span>
* <span data-ttu-id="8504a-124">Learn how to create a [private Git repository](devtest-lab-add-repo.md) where you will store your customized templates or scripts.</span><span class="sxs-lookup"><span data-stu-id="8504a-124">Learn how to create a [private Git repository](devtest-lab-add-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="8504a-125">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="8504a-125">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
