---
title: Create a Windows VM with PowerShell | Microsoft Docs
description: Create Windows virtual machines using Azure PowerShell and the classic deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: cynthn
ms.openlocfilehash: d9b713460f98104017ae73ea27f30b0d8d1ca7ee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555017"
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-the-classic-deployment-model"></a><span data-ttu-id="cbf50-103">Create a Windows virtual machine with PowerShell and the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="cbf50-103">Create a Windows virtual machine with PowerShell and the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [Azure classic portal - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to [perform these steps using the Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<span data-ttu-id="cbf50-110">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span><span class="sxs-lookup"><span data-stu-id="cbf50-110">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="cbf50-111">You can use this process to quickly create a command set for a new Windows-based virtual machine and expand an existing deployment or to create multiple command sets that quickly build out a custom dev/test or IT pro environment.</span><span class="sxs-lookup"><span data-stu-id="cbf50-111">You can use this process to quickly create a command set for a new Windows-based virtual machine and expand an existing deployment or to create multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="cbf50-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span><span class="sxs-lookup"><span data-stu-id="cbf50-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="cbf50-113">This approach can be useful if you are new to PowerShell or you just want to know what values to specify for successful configuration.</span><span class="sxs-lookup"><span data-stu-id="cbf50-113">This approach can be useful if you are new to PowerShell or you just want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="cbf50-114">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span><span class="sxs-lookup"><span data-stu-id="cbf50-114">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="cbf50-115">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install Azure PowerShell on your local computer.</span><span class="sxs-lookup"><span data-stu-id="cbf50-115">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="cbf50-116">Then, open a Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="cbf50-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="cbf50-117">Step 1: Add your account</span><span class="sxs-lookup"><span data-stu-id="cbf50-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="cbf50-118">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cbf50-118">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="cbf50-119">Type in the email address associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="cbf50-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="cbf50-120">Type in the password for your account.</span><span class="sxs-lookup"><span data-stu-id="cbf50-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="cbf50-121">Click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="cbf50-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="cbf50-122">Step 2: Set your subscription and storage account</span><span class="sxs-lookup"><span data-stu-id="cbf50-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="cbf50-123">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="cbf50-123">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="cbf50-124">Replace everything within the quotes, including the < and > characters, with the correct names.</span><span class="sxs-lookup"><span data-stu-id="cbf50-124">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="cbf50-125">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span><span class="sxs-lookup"><span data-stu-id="cbf50-125">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="cbf50-126">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span><span class="sxs-lookup"><span data-stu-id="cbf50-126">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-the-imagefamily"></a><span data-ttu-id="cbf50-127">Step 3: Determine the ImageFamily</span><span class="sxs-lookup"><span data-stu-id="cbf50-127">Step 3: Determine the ImageFamily</span></span>
<span data-ttu-id="cbf50-128">Next, you need to determine the ImageFamily or Label value for the specific image corresponding to the Azure virtual machine you want to create.</span><span class="sxs-lookup"><span data-stu-id="cbf50-128">Next, you need to determine the ImageFamily or Label value for the specific image corresponding to the Azure virtual machine you want to create.</span></span> <span data-ttu-id="cbf50-129">You can get the list of available ImageFamily values with this command.</span><span class="sxs-lookup"><span data-stu-id="cbf50-129">You can get the list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="cbf50-130">Here are some examples of ImageFamily values for Windows-based computers:</span><span class="sxs-lookup"><span data-stu-id="cbf50-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="cbf50-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="cbf50-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="cbf50-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="cbf50-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="cbf50-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="cbf50-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="cbf50-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="cbf50-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="cbf50-135">If you find the image you are looking for, open a fresh instance of the text editor of your choice or the PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="cbf50-135">If you find the image you are looking for, open a fresh instance of the text editor of your choice or the PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="cbf50-136">Copy the following into the new text file or the PowerShell ISE, substituting the ImageFamily value.</span><span class="sxs-lookup"><span data-stu-id="cbf50-136">Copy the following into the new text file or the PowerShell ISE, substituting the ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="cbf50-137">In some cases, the image name is in the Label property instead of the ImageFamily value.</span><span class="sxs-lookup"><span data-stu-id="cbf50-137">In some cases, the image name is in the Label property instead of the ImageFamily value.</span></span> <span data-ttu-id="cbf50-138">If you didn't find the image that you are looking for using the ImageFamily property, list the images by their Label property with this command.</span><span class="sxs-lookup"><span data-stu-id="cbf50-138">If you didn't find the image that you are looking for using the ImageFamily property, list the images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="cbf50-139">If you find the right image with this command, open a fresh instance of the text editor of your choice or the PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="cbf50-139">If you find the right image with this command, open a fresh instance of the text editor of your choice or the PowerShell ISE.</span></span> <span data-ttu-id="cbf50-140">Copy the following into the new text file or the PowerShell ISE, substituting the Label value.</span><span class="sxs-lookup"><span data-stu-id="cbf50-140">Copy the following into the new text file or the PowerShell ISE, substituting the Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="cbf50-141">Step 4: Build your command set</span><span class="sxs-lookup"><span data-stu-id="cbf50-141">Step 4: Build your command set</span></span>
<span data-ttu-id="cbf50-142">Build the rest of your command set by copying the appropriate set of blocks below into your new text file or the ISE and then filling in the variable values and removing the < and > characters.</span><span class="sxs-lookup"><span data-stu-id="cbf50-142">Build the rest of your command set by copying the appropriate set of blocks below into your new text file or the ISE and then filling in the variable values and removing the < and > characters.</span></span> <span data-ttu-id="cbf50-143">See the two [examples](#examples) at the end of this article for an idea of the final result.</span><span class="sxs-lookup"><span data-stu-id="cbf50-143">See the two [examples](#examples) at the end of this article for an idea of the final result.</span></span>

<span data-ttu-id="cbf50-144">Start your command set by choosing one of these two command blocks (required).</span><span class="sxs-lookup"><span data-stu-id="cbf50-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="cbf50-145">Option 1: Specify a virtual machine name and a size.</span><span class="sxs-lookup"><span data-stu-id="cbf50-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="cbf50-146">Option 2: Specify a name, size, and availability set name.</span><span class="sxs-lookup"><span data-stu-id="cbf50-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="cbf50-147">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbf50-147">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> If you have an Enterprise Agreement with Software Assurance, and intend to take advantage of the Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter to the **New-AzureVMConfig** cmdlet, passing the value **Windows_Server** for the typical use case.  Be sure you are using an image you have uploaded; you cannot use a standard image from the Gallery with the Hybrid Use Benefit.
> 
> 

<span data-ttu-id="cbf50-150">Optionally, for a standalone Windows computer, specify the local administrator account and password.</span><span class="sxs-lookup"><span data-stu-id="cbf50-150">Optionally, for a standalone Windows computer, specify the local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="cbf50-151">Choose a strong password.</span><span class="sxs-lookup"><span data-stu-id="cbf50-151">Choose a strong password.</span></span> <span data-ttu-id="cbf50-152">To check its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbf50-152">To check its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="cbf50-153">Optionally, to add the Windows computer to an existing Active Directory domain, specify the local administrator account and password, the domain, and the name and password of a domain account.</span><span class="sxs-lookup"><span data-stu-id="cbf50-153">Optionally, to add the Windows computer to an existing Active Directory domain, specify the local administrator account and password, the domain, and the name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="<FQDN of the domain that the machine is joining>"
    $domacctdomain="<domain of the account that has permission to add the machine to the domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="cbf50-154">For additional pre-configuration options for Windows-based virtual machines, see the syntax for the **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbf50-154">For additional pre-configuration options for Windows-based virtual machines, see the syntax for the **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx).</span></span>

<span data-ttu-id="cbf50-155">Optionally, assign the virtual machine a specific IP address, known as a static DIP.</span><span class="sxs-lookup"><span data-stu-id="cbf50-155">Optionally, assign the virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="cbf50-156">You can verify that a specific IP address is available with:</span><span class="sxs-lookup"><span data-stu-id="cbf50-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="cbf50-157">Optionally, assign the virtual machine to a specific subnet in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="cbf50-157">Optionally, assign the virtual machine to a specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of the subnet>"

<span data-ttu-id="cbf50-158">Optionally, add a single data disk to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cbf50-158">Optionally, add a single data disk to the virtual machine.</span></span>

    $disksize=<size of the disk in GB>
    $disklabel="<the label on the disk>"
    $lun=<Logical Unit Number (LUN) of the disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="cbf50-159">For an Active Directory domain controller, set $hcaching to "None".</span><span class="sxs-lookup"><span data-stu-id="cbf50-159">For an Active Directory domain controller, set $hcaching to "None".</span></span>

<span data-ttu-id="cbf50-160">Optionally, add the virtual machine to an existing load-balanced set for external traffic.</span><span class="sxs-lookup"><span data-stu-id="cbf50-160">Optionally, add the virtual machine to an existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of the internal port>
    $pubport=<port number of the external port>
    $endpointname="<name of the endpoint>"
    $lbsetname="<name of the existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="cbf50-161">Finally, choose one of these required command blocks for creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cbf50-161">Finally, choose one of these required command blocks for creating the virtual machine.</span></span>

<span data-ttu-id="cbf50-162">Option 1: Create the virtual machine in an existing cloud service.</span><span class="sxs-lookup"><span data-stu-id="cbf50-162">Option 1: Create the virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of the cloud service>" -VMs $vm1

<span data-ttu-id="cbf50-163">The short name of the cloud service is the name that appears in the list of Cloud Services in the Azure classic portal or in the list of Resource Groups in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cbf50-163">The short name of the cloud service is the name that appears in the list of Cloud Services in the Azure classic portal or in the list of Resource Groups in the Azure portal.</span></span>

<span data-ttu-id="cbf50-164">Option 2: Create the virtual machine in an existing cloud service and virtual network.</span><span class="sxs-lookup"><span data-stu-id="cbf50-164">Option 2: Create the virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of the cloud service>"
    $vnetname="<name of the virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="cbf50-165">Step 5: Run your command set</span><span class="sxs-lookup"><span data-stu-id="cbf50-165">Step 5: Run your command set</span></span>
<span data-ttu-id="cbf50-166">Review the Azure PowerShell command set you built in your text editor or the PowerShell ISE consisting of multiple blocks of commands from step 4.</span><span class="sxs-lookup"><span data-stu-id="cbf50-166">Review the Azure PowerShell command set you built in your text editor or the PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="cbf50-167">Ensure that you have specified all the needed variables and that they have the correct values.</span><span class="sxs-lookup"><span data-stu-id="cbf50-167">Ensure that you have specified all the needed variables and that they have the correct values.</span></span> <span data-ttu-id="cbf50-168">Also make sure that you have removed all the < and > characters.</span><span class="sxs-lookup"><span data-stu-id="cbf50-168">Also make sure that you have removed all the < and > characters.</span></span>

<span data-ttu-id="cbf50-169">If you are using a text editor, copy the command set to the clipboard and then right-click your open Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="cbf50-169">If you are using a text editor, copy the command set to the clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="cbf50-170">This will issue the command set as a series of PowerShell commands and create your Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cbf50-170">This will issue the command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="cbf50-171">Alternately, run the command set in the PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="cbf50-171">Alternately, run the command set in the PowerShell ISE.</span></span>

<span data-ttu-id="cbf50-172">If you will be creating this virtual machine again or a similar one, you can:</span><span class="sxs-lookup"><span data-stu-id="cbf50-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="cbf50-173">Save this command set as a PowerShell script file (\*.ps1).</span><span class="sxs-lookup"><span data-stu-id="cbf50-173">Save this command set as a PowerShell script file (\*.ps1).</span></span>
* <span data-ttu-id="cbf50-174">Save this command set as an Azure Automation runbook in the **Automation** section of the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="cbf50-174">Save this command set as an Azure Automation runbook in the **Automation** section of the Azure classic portal.</span></span>

## <a id="examples"></a><span data-ttu-id="cbf50-175">Examples</span><span class="sxs-lookup"><span data-stu-id="cbf50-175">Examples</span></span>
<span data-ttu-id="cbf50-176">Here are two examples of using the steps above to build Azure PowerShell command sets that create Windows-based Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="cbf50-176">Here are two examples of using the steps above to build Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="cbf50-177">Example 1</span><span class="sxs-lookup"><span data-stu-id="cbf50-177">Example 1</span></span>
<span data-ttu-id="cbf50-178">I need a PowerShell command set to create the initial virtual machine for an Active Directory domain controller that:</span><span class="sxs-lookup"><span data-stu-id="cbf50-178">I need a PowerShell command set to create the initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="cbf50-179">Uses the Windows Server 2012 R2 Datacenter image.</span><span class="sxs-lookup"><span data-stu-id="cbf50-179">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="cbf50-180">Has the name AZDC1.</span><span class="sxs-lookup"><span data-stu-id="cbf50-180">Has the name AZDC1.</span></span>
* <span data-ttu-id="cbf50-181">Is a standalone computer.</span><span class="sxs-lookup"><span data-stu-id="cbf50-181">Is a standalone computer.</span></span>
* <span data-ttu-id="cbf50-182">Has an additional data disk of 20 GB.</span><span class="sxs-lookup"><span data-stu-id="cbf50-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="cbf50-183">Has the static IP address 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="cbf50-183">Has the static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="cbf50-184">Is in the BackEnd subnet of the AZDatacenter virtual network.</span><span class="sxs-lookup"><span data-stu-id="cbf50-184">Is in the BackEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="cbf50-185">Is in the Azure-TailspinToys cloud service.</span><span class="sxs-lookup"><span data-stu-id="cbf50-185">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="cbf50-186">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span><span class="sxs-lookup"><span data-stu-id="cbf50-186">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="cbf50-187">Example 2</span><span class="sxs-lookup"><span data-stu-id="cbf50-187">Example 2</span></span>
<span data-ttu-id="cbf50-188">I need a PowerShell command set to create a virtual machine for a line-of-business server that:</span><span class="sxs-lookup"><span data-stu-id="cbf50-188">I need a PowerShell command set to create a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="cbf50-189">Uses the Windows Server 2012 R2 Datacenter image.</span><span class="sxs-lookup"><span data-stu-id="cbf50-189">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="cbf50-190">Has the name LOB1.</span><span class="sxs-lookup"><span data-stu-id="cbf50-190">Has the name LOB1.</span></span>
* <span data-ttu-id="cbf50-191">Is a member of the corp.contoso.com domain.</span><span class="sxs-lookup"><span data-stu-id="cbf50-191">Is a member of the corp.contoso.com domain.</span></span>
* <span data-ttu-id="cbf50-192">Has an additional data disk of 200 GB.</span><span class="sxs-lookup"><span data-stu-id="cbf50-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="cbf50-193">Is in the FrontEnd subnet of the AZDatacenter virtual network.</span><span class="sxs-lookup"><span data-stu-id="cbf50-193">Is in the FrontEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="cbf50-194">Is in the Azure-TailspinToys cloud service.</span><span class="sxs-lookup"><span data-stu-id="cbf50-194">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="cbf50-195">Here is the corresponding Azure PowerShell command set to create this virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cbf50-195">Here is the corresponding Azure PowerShell command set to create this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="cbf50-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="cbf50-196">Next steps</span></span>
<span data-ttu-id="cbf50-197">If you need an OS disk that is larger than 127 GB, you can [expand the OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbf50-197">If you need an OS disk that is larger than 127 GB, you can [expand the OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

