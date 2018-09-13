---
title: Azure Virtual Machine Agent Overview | Microsoft Docs
description: Azure Virtual Machine Agent Overview
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563798"
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="a4e46-103">Azure Virtual Machine Agent overview</span><span class="sxs-lookup"><span data-stu-id="a4e46-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="a4e46-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span><span class="sxs-lookup"><span data-stu-id="a4e46-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="a4e46-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span><span class="sxs-lookup"><span data-stu-id="a4e46-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="a4e46-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span><span class="sxs-lookup"><span data-stu-id="a4e46-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="a4e46-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4e46-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="a4e46-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span><span class="sxs-lookup"><span data-stu-id="a4e46-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="a4e46-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span><span class="sxs-lookup"><span data-stu-id="a4e46-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="a4e46-110">Install the VM Agent</span><span class="sxs-lookup"><span data-stu-id="a4e46-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="a4e46-111">Azure gallery image</span><span class="sxs-lookup"><span data-stu-id="a4e46-111">Azure gallery image</span></span>

<span data-ttu-id="a4e46-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span><span class="sxs-lookup"><span data-stu-id="a4e46-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="a4e46-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span><span class="sxs-lookup"><span data-stu-id="a4e46-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="a4e46-114">Manual installation</span><span class="sxs-lookup"><span data-stu-id="a4e46-114">Manual installation</span></span>

<span data-ttu-id="a4e46-115">The Windows VM agent can be manually installed using a Windows installer package.</span><span class="sxs-lookup"><span data-stu-id="a4e46-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="a4e46-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="a4e46-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="a4e46-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="a4e46-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="a4e46-118">The VM Agent can be installed by double-clicking the windows installer file.</span><span class="sxs-lookup"><span data-stu-id="a4e46-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="a4e46-119">For an automated or unattended installation of the VM agent, run the following command.</span><span class="sxs-lookup"><span data-stu-id="a4e46-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="a4e46-120">Detect the VM Agent</span><span class="sxs-lookup"><span data-stu-id="a4e46-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="a4e46-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4e46-121">PowerShell</span></span>

<span data-ttu-id="a4e46-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="a4e46-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="a4e46-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="a4e46-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="a4e46-124">The following is just a subset of the `Get-AzureRmVM` output.</span><span class="sxs-lookup"><span data-stu-id="a4e46-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="a4e46-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4e46-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="a4e46-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="a4e46-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="a4e46-127">Manual Detection</span><span class="sxs-lookup"><span data-stu-id="a4e46-127">Manual Detection</span></span>

<span data-ttu-id="a4e46-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span><span class="sxs-lookup"><span data-stu-id="a4e46-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="a4e46-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="a4e46-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="a4e46-130">The presence of this process indicates that the VM agent is installed.</span><span class="sxs-lookup"><span data-stu-id="a4e46-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="a4e46-131">Upgrade the VM Agent</span><span class="sxs-lookup"><span data-stu-id="a4e46-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="a4e46-132">The Azure VM Agent for Windows is automatically upgraded.</span><span class="sxs-lookup"><span data-stu-id="a4e46-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="a4e46-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span><span class="sxs-lookup"><span data-stu-id="a4e46-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="a4e46-134">Custom VM images should be manually updated to include the new VM agent.</span><span class="sxs-lookup"><span data-stu-id="a4e46-134">Custom VM images should be manually updated to include the new VM agent.</span></span>