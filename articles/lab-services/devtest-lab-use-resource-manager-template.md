---
title: View and use a virtual machine's Azure Resource Manager template | Microsoft Docs
description: Learn how to use the Azure Resource Manager template from a virtual machine to create other VMs
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 1b96c801e3c5a43f23d4c63c13a611c24dd6705b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868814"
---
# <a name="create-virtual-machines-using-an-azure-resource-manager-template"></a><span data-ttu-id="aad8f-103">Create virtual machines using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="aad8f-103">Create virtual machines using an Azure Resource Manager template</span></span> 

<span data-ttu-id="aad8f-104">When you are creating a virtual machine (VM) in DevTest Labs through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), you can view the Azure Resource Manager template before you save the VM.</span><span class="sxs-lookup"><span data-stu-id="aad8f-104">When you are creating a virtual machine (VM) in DevTest Labs through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), you can view the Azure Resource Manager template before you save the VM.</span></span> <span data-ttu-id="aad8f-105">The template can then be used as a basis to create more lab VMs with the same settings.</span><span class="sxs-lookup"><span data-stu-id="aad8f-105">The template can then be used as a basis to create more lab VMs with the same settings.</span></span>

<span data-ttu-id="aad8f-106">This article describes Multi-VM vs. single-VM Resource Manager templates and shows you how to view and save a template when creating a VM.</span><span class="sxs-lookup"><span data-stu-id="aad8f-106">This article describes Multi-VM vs. single-VM Resource Manager templates and shows you how to view and save a template when creating a VM.</span></span>

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a><span data-ttu-id="aad8f-107">Multi-VM vs. single-VM Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="aad8f-107">Multi-VM vs. single-VM Resource Manager templates</span></span>
<span data-ttu-id="aad8f-108">There are two ways to create VMs in DevTest Labs using a Resource Manager template: provision the Microsoft.DevTestLab/labs/virtualmachines resource or provision the Microsoft.Commpute/virtualmachines resource.</span><span class="sxs-lookup"><span data-stu-id="aad8f-108">There are two ways to create VMs in DevTest Labs using a Resource Manager template: provision the Microsoft.DevTestLab/labs/virtualmachines resource or provision the Microsoft.Commpute/virtualmachines resource.</span></span> <span data-ttu-id="aad8f-109">Each is used in different scenarios and requires different permissions.</span><span class="sxs-lookup"><span data-stu-id="aad8f-109">Each is used in different scenarios and requires different permissions.</span></span>

- <span data-ttu-id="aad8f-110">Resource Manager templates that use a Microsoft.DevTestLab/labs/virtualmachines resource type (as declared in the “resource” property in the template) can provision individual lab VMs.</span><span class="sxs-lookup"><span data-stu-id="aad8f-110">Resource Manager templates that use a Microsoft.DevTestLab/labs/virtualmachines resource type (as declared in the “resource” property in the template) can provision individual lab VMs.</span></span> <span data-ttu-id="aad8f-111">Each VM then shows up as a single item in the DevTest Labs virtual machines list:</span><span class="sxs-lookup"><span data-stu-id="aad8f-111">Each VM then shows up as a single item in the DevTest Labs virtual machines list:</span></span>

   ![List of VMs as single items in the DevTest Labs virtual machines list](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   <span data-ttu-id="aad8f-113">This type of Resource Manager template can be provisioned through the Azure PowerShell command **New-AzureRmResourceGroupDeployment** or through the Azure CLI command **az group deployment create**.</span><span class="sxs-lookup"><span data-stu-id="aad8f-113">This type of Resource Manager template can be provisioned through the Azure PowerShell command **New-AzureRmResourceGroupDeployment** or through the Azure CLI command **az group deployment create**.</span></span> <span data-ttu-id="aad8f-114">It requires administrator permissions, so users who are assigned with a DevTest Labs user role can’t perform the deployment.</span><span class="sxs-lookup"><span data-stu-id="aad8f-114">It requires administrator permissions, so users who are assigned with a DevTest Labs user role can’t perform the deployment.</span></span> 

- <span data-ttu-id="aad8f-115">Resource Manager templates that use a Microsoft.Compute/virtualmachines resource type can provision multiple VMs as a single environment in the DevTest Labs virtual machines list:</span><span class="sxs-lookup"><span data-stu-id="aad8f-115">Resource Manager templates that use a Microsoft.Compute/virtualmachines resource type can provision multiple VMs as a single environment in the DevTest Labs virtual machines list:</span></span>

   ![List of VMs as single items in the DevTest Labs virtual machines list](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   <span data-ttu-id="aad8f-117">VMs in the same environment can be managed together and share the same lifecycle.</span><span class="sxs-lookup"><span data-stu-id="aad8f-117">VMs in the same environment can be managed together and share the same lifecycle.</span></span> <span data-ttu-id="aad8f-118">Users who are assigned with a DevTest Labs user role can create environments using those templates as long as the administrator has configured the lab that way.</span><span class="sxs-lookup"><span data-stu-id="aad8f-118">Users who are assigned with a DevTest Labs user role can create environments using those templates as long as the administrator has configured the lab that way.</span></span>

<span data-ttu-id="aad8f-119">The remainder of this article discusses Resource Manager templates that use Mirosoft.DevTestLab/labs/virtualmachines.</span><span class="sxs-lookup"><span data-stu-id="aad8f-119">The remainder of this article discusses Resource Manager templates that use Mirosoft.DevTestLab/labs/virtualmachines.</span></span> <span data-ttu-id="aad8f-120">These are used by lab admins to automate lab VM creation (for example, claimable VMs) or golden image generation (for example, image factory).</span><span class="sxs-lookup"><span data-stu-id="aad8f-120">These are used by lab admins to automate lab VM creation (for example, claimable VMs) or golden image generation (for example, image factory).</span></span>

<span data-ttu-id="aad8f-121">[Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span><span class="sxs-lookup"><span data-stu-id="aad8f-121">[Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span>

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a><span data-ttu-id="aad8f-122">View and save a virtual machine's Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="aad8f-122">View and save a virtual machine's Resource Manager template</span></span>
1. <span data-ttu-id="aad8f-123">Follow the steps at [Create your first VM in a lab](devtest-lab-create-first-vm.md) to begin creating a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aad8f-123">Follow the steps at [Create your first VM in a lab](devtest-lab-create-first-vm.md) to begin creating a virtual machine.</span></span>
1. <span data-ttu-id="aad8f-124">Enter the required information for your virtual machine and add any artifacts you want for this VM.</span><span class="sxs-lookup"><span data-stu-id="aad8f-124">Enter the required information for your virtual machine and add any artifacts you want for this VM.</span></span>
1. <span data-ttu-id="aad8f-125">At the bottom of the Configure settings window, choose **View ARM template**.</span><span class="sxs-lookup"><span data-stu-id="aad8f-125">At the bottom of the Configure settings window, choose **View ARM template**.</span></span>

   ![View ARM template button](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. <span data-ttu-id="aad8f-127">Copy and save the Resource Manager template to use later to create another virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aad8f-127">Copy and save the Resource Manager template to use later to create another virtual machine.</span></span>

   ![Resource Manager template to save for later use](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

<span data-ttu-id="aad8f-129">After you have saved the Resource Manager template, you must update the parameters section of the template before you can use it.</span><span class="sxs-lookup"><span data-stu-id="aad8f-129">After you have saved the Resource Manager template, you must update the parameters section of the template before you can use it.</span></span> <span data-ttu-id="aad8f-130">You can create a parameter.json that customizes just the parameters, outside of the actual Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="aad8f-130">You can create a parameter.json that customizes just the parameters, outside of the actual Resource Manager template.</span></span> 

![Customize parameters using a JSON file](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

<span data-ttu-id="aad8f-132">The Resource Manager template is now ready to use to [create a VM](devtest-lab-create-environment-from-arm.md).</span><span class="sxs-lookup"><span data-stu-id="aad8f-132">The Resource Manager template is now ready to use to [create a VM](devtest-lab-create-environment-from-arm.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="aad8f-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="aad8f-133">Next steps</span></span>
* <span data-ttu-id="aad8f-134">Learn how to [Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span><span class="sxs-lookup"><span data-stu-id="aad8f-134">Learn how to [Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span></span>
* [<span data-ttu-id="aad8f-135">Deploy a Resource Manager template to create a VM</span><span class="sxs-lookup"><span data-stu-id="aad8f-135">Deploy a Resource Manager template to create a VM</span></span>](devtest-lab-create-environment-from-arm.md#deploy-a-resource-manager-template-to-create-a-vm)
* <span data-ttu-id="aad8f-136">Explore more quickstart Resource Manager templates for DevTest Labs automation from the [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="aad8f-136">Explore more quickstart Resource Manager templates for DevTest Labs automation from the [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span></span>
