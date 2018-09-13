---
title: 'Azure Active Directory Domain Services: Administration Guide | Microsoft Docs'
description: Join a Windows virtual machine to a managed domain using Azure PowerShell and the classic deployment model.
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ee6d1448f056caf4205b13b56b8ae758a6f37a62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550574"
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="facec-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span><span class="sxs-lookup"><span data-stu-id="facec-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Azure classic portal - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the classic deployment model. Azure AD Domain Services does not currently support the Resource Manager model.
>
>

<span data-ttu-id="facec-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span><span class="sxs-lookup"><span data-stu-id="facec-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="facec-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="facec-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="facec-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span><span class="sxs-lookup"><span data-stu-id="facec-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="facec-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span><span class="sxs-lookup"><span data-stu-id="facec-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="facec-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span><span class="sxs-lookup"><span data-stu-id="facec-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="facec-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install Azure PowerShell on your local computer.</span><span class="sxs-lookup"><span data-stu-id="facec-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="facec-115">Then, open a Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="facec-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="facec-116">Step 1: Add your account</span><span class="sxs-lookup"><span data-stu-id="facec-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="facec-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span><span class="sxs-lookup"><span data-stu-id="facec-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="facec-118">Type in the email address associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="facec-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="facec-119">Type in the password for your account.</span><span class="sxs-lookup"><span data-stu-id="facec-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="facec-120">Click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="facec-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="facec-121">Step 2: Set your subscription and storage account</span><span class="sxs-lookup"><span data-stu-id="facec-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="facec-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="facec-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="facec-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span><span class="sxs-lookup"><span data-stu-id="facec-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="facec-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span><span class="sxs-lookup"><span data-stu-id="facec-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="facec-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span><span class="sxs-lookup"><span data-stu-id="facec-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="facec-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span><span class="sxs-lookup"><span data-stu-id="facec-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="facec-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span><span class="sxs-lookup"><span data-stu-id="facec-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="facec-128">Specify information about the Windows virtual machine to be provisioned.</span><span class="sxs-lookup"><span data-stu-id="facec-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="facec-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="facec-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="facec-130">Provide information about the managed domain.</span><span class="sxs-lookup"><span data-stu-id="facec-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="facec-131">Specify the name of the cloud service.</span><span class="sxs-lookup"><span data-stu-id="facec-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="facec-132">Specify the name of the virtual network to which the VM should be joined.</span><span class="sxs-lookup"><span data-stu-id="facec-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="facec-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span><span class="sxs-lookup"><span data-stu-id="facec-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="facec-134">Select the VM image to be used to provision the VM.</span><span class="sxs-lookup"><span data-stu-id="facec-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="facec-135">Configure the VM - set VM name, instance size & image to be used.</span><span class="sxs-lookup"><span data-stu-id="facec-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="facec-136">Obtain local administrator credentials for the VM.</span><span class="sxs-lookup"><span data-stu-id="facec-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="facec-137">Choose a strong local administrator password.</span><span class="sxs-lookup"><span data-stu-id="facec-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="facec-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="facec-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="facec-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span><span class="sxs-lookup"><span data-stu-id="facec-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="facec-140">Configure the VM - specify domain join requirement & required credentials.</span><span class="sxs-lookup"><span data-stu-id="facec-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="facec-141">Set a subnet for the VM.</span><span class="sxs-lookup"><span data-stu-id="facec-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="facec-142">Optional: Point to the IP address of the domain.</span><span class="sxs-lookup"><span data-stu-id="facec-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="facec-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span><span class="sxs-lookup"><span data-stu-id="facec-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="facec-144">Now, provision the domain-joined Windows VM.</span><span class="sxs-lookup"><span data-stu-id="facec-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="facec-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="facec-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="facec-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span><span class="sxs-lookup"><span data-stu-id="facec-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="facec-147">Uses the Windows Server 2012 R2 Datacenter image.</span><span class="sxs-lookup"><span data-stu-id="facec-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="facec-148">Is an extra small virtual machine.</span><span class="sxs-lookup"><span data-stu-id="facec-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="facec-149">Has the name Contoso100-test.</span><span class="sxs-lookup"><span data-stu-id="facec-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="facec-150">Is automatically domain joined to the contoso100 managed domain.</span><span class="sxs-lookup"><span data-stu-id="facec-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="facec-151">Is added to the same virtual network as the managed domain.</span><span class="sxs-lookup"><span data-stu-id="facec-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="facec-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="facec-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="facec-153">Related Content</span><span class="sxs-lookup"><span data-stu-id="facec-153">Related Content</span></span>
* [<span data-ttu-id="facec-154">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="facec-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="facec-155">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="facec-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
