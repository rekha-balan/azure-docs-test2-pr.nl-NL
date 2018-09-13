---
title: Import VMs from another lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to import virtual machines from another lab into the current lab in Azure DevTest Labs
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 8460f09e-482f-48ba-a57a-c95fe8afa001
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2018
ms.author: spelluru
ms.openlocfilehash: 4585d151e286917c67586a02539a10ade32bdd4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856363"
---
# <a name="import-vms-from-another-lab-in-azure-devtest-labs"></a><span data-ttu-id="eeb2b-103">Import VMs from another lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="eeb2b-103">Import VMs from another lab in Azure DevTest Labs</span></span>
<span data-ttu-id="eeb2b-104">The Azure DevTest Labs service significantly improves management of virtual machines (VMs) for development and testing activities.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-104">The Azure DevTest Labs service significantly improves management of virtual machines (VMs) for development and testing activities.</span></span> <span data-ttu-id="eeb2b-105">It allows you to move a VM from one lab to another as the team or infrastructure requirements change.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-105">It allows you to move a VM from one lab to another as the team or infrastructure requirements change.</span></span> <span data-ttu-id="eeb2b-106">Here are some common scenarios where you may need to do so:</span><span class="sxs-lookup"><span data-stu-id="eeb2b-106">Here are some common scenarios where you may need to do so:</span></span> 

- <span data-ttu-id="eeb2b-107">A person on the team moves to another group within the enterprise and wants to take development VMs to the new team’s lab.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-107">A person on the team moves to another group within the enterprise and wants to take development VMs to the new team’s lab.</span></span>
- <span data-ttu-id="eeb2b-108">The group has reached the subscription-level quota and wants to split up teams into multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-108">The group has reached the subscription-level quota and wants to split up teams into multiple subscriptions.</span></span>
- <span data-ttu-id="eeb2b-109">The company plans to move to Express Route (or some other new networking topology) and the team wants to move VMs to use this new infrastructure.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-109">The company plans to move to Express Route (or some other new networking topology) and the team wants to move VMs to use this new infrastructure.</span></span>

## <a name="solution-and-constraints"></a><span data-ttu-id="eeb2b-110">Solution and constraints</span><span class="sxs-lookup"><span data-stu-id="eeb2b-110">Solution and constraints</span></span>
<span data-ttu-id="eeb2b-111">Azure DevTest Labs enables a lab owner to import VMs in a source lab into a destination lab.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-111">Azure DevTest Labs enables a lab owner to import VMs in a source lab into a destination lab.</span></span> <span data-ttu-id="eeb2b-112">The lab owner can optionally provide a new name for the destination VM in the process.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-112">The lab owner can optionally provide a new name for the destination VM in the process.</span></span> <span data-ttu-id="eeb2b-113">The import process includes all the dependencies like disks, schedules, network settings, etc. The process does take some time and is impacted by the number/size of the disks attached to the source machine and the distance to the destination (For example, East US region to Southeast Asia region).</span><span class="sxs-lookup"><span data-stu-id="eeb2b-113">The import process includes all the dependencies like disks, schedules, network settings, etc. The process does take some time and is impacted by the number/size of the disks attached to the source machine and the distance to the destination (For example, East US region to Southeast Asia region).</span></span> <span data-ttu-id="eeb2b-114">Once the import process is complete, the source VM remains shutdown and the new one is running in the destination lab.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-114">Once the import process is complete, the source VM remains shutdown and the new one is running in the destination lab.</span></span>

<span data-ttu-id="eeb2b-115">There are two key constraints to be aware of when planning to import VMs to another lab:</span><span class="sxs-lookup"><span data-stu-id="eeb2b-115">There are two key constraints to be aware of when planning to import VMs to another lab:</span></span>

- <span data-ttu-id="eeb2b-116">Importing VMs across subscriptions and across regions are supported, but the subscriptions must be associated to the same Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-116">Importing VMs across subscriptions and across regions are supported, but the subscriptions must be associated to the same Azure Active Directory tenant.</span></span>
- <span data-ttu-id="eeb2b-117">VMs must not be in a claimable state in the source lab.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-117">VMs must not be in a claimable state in the source lab.</span></span>

<span data-ttu-id="eeb2b-118">In addition, to be able to import a VM from one lab to another, you need to be the owner of the VM in the source lab and owner of the lab in the destination lab.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-118">In addition, to be able to import a VM from one lab to another, you need to be the owner of the VM in the source lab and owner of the lab in the destination lab.</span></span>

## <a name="steps-to-import-a-vm-from-another-lab"></a><span data-ttu-id="eeb2b-119">Steps to import a VM from another lab</span><span class="sxs-lookup"><span data-stu-id="eeb2b-119">Steps to import a VM from another lab</span></span>
<span data-ttu-id="eeb2b-120">Currently, you can import a VM from one lab into another only by using Azure PowerShell and REST API.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-120">Currently, you can import a VM from one lab into another only by using Azure PowerShell and REST API.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="eeb2b-121">Use PowerShell</span><span class="sxs-lookup"><span data-stu-id="eeb2b-121">Use PowerShell</span></span>
<span data-ttu-id="eeb2b-122">Download the PowerShell script file ImportVirtualMachines.ps1 from [Azure DevTest Lab Git repository](https://github.com/Azure/azure-devtestlab/tree/master/Scripts/ImportVirtualMachines) to your local drive.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-122">Download the PowerShell script file ImportVirtualMachines.ps1 from [Azure DevTest Lab Git repository](https://github.com/Azure/azure-devtestlab/tree/master/Scripts/ImportVirtualMachines) to your local drive.</span></span> 

#### <a name="import-a-single-vm"></a><span data-ttu-id="eeb2b-123">Import a single VM</span><span class="sxs-lookup"><span data-stu-id="eeb2b-123">Import a single VM</span></span>
<span data-ttu-id="eeb2b-124">Run the ImportVirtualMachines.ps1 script to import a single VM from a source lab into a destination lab.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-124">Run the ImportVirtualMachines.ps1 script to import a single VM from a source lab into a destination lab.</span></span> <span data-ttu-id="eeb2b-125">You can specify a new name for the VM that's being copied by using the DestinationVirtualMachineName paramer.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-125">You can specify a new name for the VM that's being copied by using the DestinationVirtualMachineName paramer.</span></span> 

```powershell
./ImportVirtualMachines.ps1 -SourceSubscriptionId "<ID of the subscription that contains the source VM>" `
                            -SourceDevTestLabName "<Name of the lab that contains the source VM>" `
                            -SourceVirtualMachineName "<Name of the machine. Optional. If not specified, all VMs are copied>" `
                            -DestinationSubscriptionId "<ID of the target/destination subscription>" `
                            -DestinationDevTestLabName "<Name of the lab to which the VM is copied>" `
                            -DestinationVirtualMachineName "<New name for the VM. Optional>"
```


#### <a name="importing-all-vms"></a><span data-ttu-id="eeb2b-126">Importing all VMs</span><span class="sxs-lookup"><span data-stu-id="eeb2b-126">Importing all VMs</span></span>
<span data-ttu-id="eeb2b-127">When you run the ImportVirtualMachines.ps1 script, if you don't specify a VM in the source lab, the script imports all VMs in the source lab into the destination lab.</span><span class="sxs-lookup"><span data-stu-id="eeb2b-127">When you run the ImportVirtualMachines.ps1 script, if you don't specify a VM in the source lab, the script imports all VMs in the source lab into the destination lab.</span></span> 

```powershell
./ImportVirtualMachines.ps1 -SourceSubscriptionId "<ID of the subscription that contains the source VM>" `
                            -SourceDevTestLabName "<Name of the lab that contains the source VM>" `
                            -DestinationSubscriptionId "<ID of the target/destination subscription>" `
                            -DestinationDevTestLabName "<Name of the lab to which the VMs are copied>"
```

### <a name="use-rest-api"></a><span data-ttu-id="eeb2b-128">Use REST API</span><span class="sxs-lookup"><span data-stu-id="eeb2b-128">Use REST API</span></span>
<span data-ttu-id="eeb2b-129">Invoke the REST API against the target/destination lab and pass in the source lab, subscription, and VM information as parameters as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="eeb2b-129">Invoke the REST API against the target/destination lab and pass in the source lab, subscription, and VM information as parameters as shown in the following example:</span></span> 

```json
POST https://management.azure.com/subscriptions/<ID of the target/destination subscription>/resourceGroups/<Name of the resource group that contains the destination lab>/providers/Microsoft.DevTestLab/labs/<Name of the lab to which the VMs are copied>/ImportVirtualMachine?api-version=2017-04-26-preview
{
   sourceVirtualMachineResourceId: "/subscriptions/<ID of the subscription that contains the source VM>/resourcegroups/<Name of the resource group that contains the source lab>/providers/microsoft.devtestlab/labs/<Name of the lab that contains the source VM>/virtualmachines/MyVm",
   destinationVirtualMachineName: "MyVmNew"
}
```

## <a name="next-steps"></a><span data-ttu-id="eeb2b-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="eeb2b-130">Next steps</span></span>

- <span data-ttu-id="eeb2b-131">For information about resizing a VM, see [Resize a VM](devtest-lab-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="eeb2b-131">For information about resizing a VM, see [Resize a VM](devtest-lab-resize-vm.md).</span></span>
- <span data-ttu-id="eeb2b-132">For information about redeploying a VM, see [Redeploy a VM](devtest-lab-redeploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="eeb2b-132">For information about redeploying a VM, see [Redeploy a VM](devtest-lab-redeploy-vm.md).</span></span>

