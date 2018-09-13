---
title: Install Symantec Endpoint Protection on a Windows VM in Azure | Microsoft Docs
description: Learn how to install and configure the Symantec Endpoint Protection security extension on a new or existing Azure VM created with the Classic deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 64f48f22c35724b536ff538b8e8efdee435cc181
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553088"
---
# <a name="how-to-install-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="b8e62-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="b8e62-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b8e62-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b8e62-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b8e62-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="b8e62-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b8e62-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="b8e62-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="b8e62-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b8e62-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="b8e62-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span><span class="sxs-lookup"><span data-stu-id="b8e62-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="b8e62-109">The client is installed as a security extension by using the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="b8e62-109">The client is installed as a security extension by using the VM Agent.</span></span>

<span data-ttu-id="b8e62-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b8e62-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span></span> <span data-ttu-id="b8e62-111">If you're not a customer yet, you can sign up for a trial subscription.</span><span class="sxs-lookup"><span data-stu-id="b8e62-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="b8e62-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span><span class="sxs-lookup"><span data-stu-id="b8e62-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="b8e62-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span><span class="sxs-lookup"><span data-stu-id="b8e62-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="b8e62-114">Install Symantec Endpoint Protection on an existing VM</span><span class="sxs-lookup"><span data-stu-id="b8e62-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="b8e62-115">Before you begin, you need the following:</span><span class="sxs-lookup"><span data-stu-id="b8e62-115">Before you begin, you need the following:</span></span>

* <span data-ttu-id="b8e62-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span><span class="sxs-lookup"><span data-stu-id="b8e62-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="b8e62-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span><span class="sxs-lookup"><span data-stu-id="b8e62-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="b8e62-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="b8e62-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="b8e62-119">Log in to your Azure subscription using `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="b8e62-119">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="b8e62-120">The VM Agent running on the Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="b8e62-120">The VM Agent running on the Azure Virtual Machine.</span></span>

<span data-ttu-id="b8e62-121">First, verify that the VM Agent is already installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b8e62-121">First, verify that the VM Agent is already installed on the virtual machine.</span></span> <span data-ttu-id="b8e62-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="b8e62-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="b8e62-123">Replace everything within the quotes, including the < and > characters.</span><span class="sxs-lookup"><span data-stu-id="b8e62-123">Replace everything within the quotes, including the < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="b8e62-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span><span class="sxs-lookup"><span data-stu-id="b8e62-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="b8e62-125">If the **write-host** command displays **True**, the VM Agent is installed.</span><span class="sxs-lookup"><span data-stu-id="b8e62-125">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="b8e62-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="b8e62-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="b8e62-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span><span class="sxs-lookup"><span data-stu-id="b8e62-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="b8e62-128">To verify that the Symantec security extension has been installed and is up-to-date:</span><span class="sxs-lookup"><span data-stu-id="b8e62-128">To verify that the Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="b8e62-129">Log on to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b8e62-129">Log on to the virtual machine.</span></span> <span data-ttu-id="b8e62-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="b8e62-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="b8e62-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="b8e62-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="b8e62-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="b8e62-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="b8e62-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span><span class="sxs-lookup"><span data-stu-id="b8e62-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8e62-134">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b8e62-134">Additional resources</span></span>
<span data-ttu-id="b8e62-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="b8e62-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="b8e62-136">[Azure VM Extensions and Features][Ext]</span><span class="sxs-lookup"><span data-stu-id="b8e62-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Portal]: http://manage.windowsazure.com

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
