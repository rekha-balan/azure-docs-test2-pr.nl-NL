---
title: Install Trend Micro Deep Security on a VM | Microsoft Docs
description: This article describes how to install and configure Trend Micro security on a VM created with the Classic deployment model in Azure.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: ee6ac04cf33b2f1c4545899a5d27e5e45b810715
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549066"
---
# <a name="how-to-install-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="2125d-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="2125d-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2125d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2125d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2125d-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2125d-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="2125d-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="2125d-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="2125d-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2125d-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="2125d-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span><span class="sxs-lookup"><span data-stu-id="2125d-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="2125d-109">The client is installed as a security extension via the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="2125d-109">The client is installed as a security extension via the VM Agent.</span></span> <span data-ttu-id="2125d-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2125d-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span></span>

<span data-ttu-id="2125d-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span><span class="sxs-lookup"><span data-stu-id="2125d-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="2125d-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span><span class="sxs-lookup"><span data-stu-id="2125d-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span></span> <span data-ttu-id="2125d-113">This article covers both situations.</span><span class="sxs-lookup"><span data-stu-id="2125d-113">This article covers both situations.</span></span>

<span data-ttu-id="2125d-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2125d-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span></span> <span data-ttu-id="2125d-115">If you're not a customer yet, you can sign up for a trial subscription.</span><span class="sxs-lookup"><span data-stu-id="2125d-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="2125d-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="2125d-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-the-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="2125d-117">Install the Deep Security Agent on a new VM</span><span class="sxs-lookup"><span data-stu-id="2125d-117">Install the Deep Security Agent on a new VM</span></span>

<!-- old portal [Azure classic portal](http://manage.windowsazure.com) -->

<span data-ttu-id="2125d-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2125d-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span></span> <span data-ttu-id="2125d-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="2125d-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span></span>

<span data-ttu-id="2125d-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2125d-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span></span> <span data-ttu-id="2125d-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span><span class="sxs-lookup"><span data-stu-id="2125d-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span></span>  <span data-ttu-id="2125d-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2125d-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>

<span data-ttu-id="2125d-123">When you get to the **Settings** blade of the wizard, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="2125d-123">When you get to the **Settings** blade of the wizard, do the following steps:</span></span>

1. <span data-ttu-id="2125d-124">Click **Extensions**, then click **Add extension** in the next pane.</span><span class="sxs-lookup"><span data-stu-id="2125d-124">Click **Extensions**, then click **Add extension** in the next pane.</span></span>

   ![Start adding the extension][1]

2. <span data-ttu-id="2125d-126">Select **Deep Security Agent** in the **New resource** pane.</span><span class="sxs-lookup"><span data-stu-id="2125d-126">Select **Deep Security Agent** in the **New resource** pane.</span></span> <span data-ttu-id="2125d-127">In the Deep Security Agent pane, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2125d-127">In the Deep Security Agent pane, click **Create**.</span></span>

   ![Identify Deep Security Agent][2]

3. <span data-ttu-id="2125d-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span><span class="sxs-lookup"><span data-stu-id="2125d-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span></span> <span data-ttu-id="2125d-130">Optionally, you can enter a **Security Policy Identifier**.</span><span class="sxs-lookup"><span data-stu-id="2125d-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="2125d-131">Then, click **OK** to add the client.</span><span class="sxs-lookup"><span data-stu-id="2125d-131">Then, click **OK** to add the client.</span></span>

   ![Provide extension details][3]

## <a name="install-the-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="2125d-133">Install the Deep Security Agent on an existing VM</span><span class="sxs-lookup"><span data-stu-id="2125d-133">Install the Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="2125d-134">To install the agent on an existing VM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2125d-134">To install the agent on an existing VM, you need the following items:</span></span>

* <span data-ttu-id="2125d-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span><span class="sxs-lookup"><span data-stu-id="2125d-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="2125d-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span><span class="sxs-lookup"><span data-stu-id="2125d-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="2125d-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2125d-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="2125d-138">Log in to your Azure subscription using `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="2125d-138">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="2125d-139">The VM Agent installed on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2125d-139">The VM Agent installed on the target virtual machine.</span></span>

<span data-ttu-id="2125d-140">First, verify that the VM Agent is already installed.</span><span class="sxs-lookup"><span data-stu-id="2125d-140">First, verify that the VM Agent is already installed.</span></span> <span data-ttu-id="2125d-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="2125d-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="2125d-142">Replace everything within the quotes, including the < and > characters.</span><span class="sxs-lookup"><span data-stu-id="2125d-142">Replace everything within the quotes, including the < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="2125d-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span><span class="sxs-lookup"><span data-stu-id="2125d-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span></span>

<span data-ttu-id="2125d-144">If the **write-host** command returns **True**, the VM Agent is installed.</span><span class="sxs-lookup"><span data-stu-id="2125d-144">If the **write-host** command returns **True**, the VM Agent is installed.</span></span> <span data-ttu-id="2125d-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="2125d-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="2125d-146">If the VM Agent is installed, run these commands.</span><span class="sxs-lookup"><span data-stu-id="2125d-146">If the VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="2125d-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="2125d-147">Next steps</span></span>
<span data-ttu-id="2125d-148">It takes a few minutes for the agent to start running when it is installed.</span><span class="sxs-lookup"><span data-stu-id="2125d-148">It takes a few minutes for the agent to start running when it is installed.</span></span> <span data-ttu-id="2125d-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span><span class="sxs-lookup"><span data-stu-id="2125d-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="2125d-150">See the following articles for additional instructions:</span><span class="sxs-lookup"><span data-stu-id="2125d-150">See the following articles for additional instructions:</span></span>

* <span data-ttu-id="2125d-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="2125d-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="2125d-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span><span class="sxs-lookup"><span data-stu-id="2125d-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span></span>
* <span data-ttu-id="2125d-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span><span class="sxs-lookup"><span data-stu-id="2125d-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2125d-154">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2125d-154">Additional resources</span></span>
<span data-ttu-id="2125d-155">[How to log on to a virtual machine running Windows Server]</span><span class="sxs-lookup"><span data-stu-id="2125d-155">[How to log on to a virtual machine running Windows Server]</span></span>

<span data-ttu-id="2125d-156">[Azure VM Extensions and features]</span><span class="sxs-lookup"><span data-stu-id="2125d-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/install-trend/new_vm_Blade3.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/install-trend/find_SecurityAgent.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[How to log on to a virtual machine running Windows Server]:connect-logon.md
[Azure VM Extensions and features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409



