---
title: Create a SQL Server Virtual Machine in Azure PowerShell (Classic) | Microsoft Docs
description: Provides steps and PowerShell scripts for creating an Azure VM with SQL Server virtual machine gallery images. This topic uses the classic deployment mode.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/02/2017
ms.author: jroth
ms.openlocfilehash: e2e751886407a1fceffa0c09b6f7fb5664c03b1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549716"
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="03c24-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="03c24-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>
## <a name="overview"></a><span data-ttu-id="03c24-105">Overview</span><span class="sxs-lookup"><span data-stu-id="03c24-105">Overview</span></span>
<span data-ttu-id="03c24-106">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="03c24-106">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="03c24-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="03c24-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="03c24-108">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="03c24-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="03c24-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="03c24-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="03c24-110">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="03c24-110">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="03c24-111">Install and configure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="03c24-111">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="03c24-112">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03c24-112">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="03c24-113">[Download and install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="03c24-113">[Download and install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span></span>
3. <span data-ttu-id="03c24-114">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span><span class="sxs-lookup"><span data-stu-id="03c24-114">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>
   
        Add-AzureAccount

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="03c24-115">Determine your target Azure region</span><span class="sxs-lookup"><span data-stu-id="03c24-115">Determine your target Azure region</span></span>
<span data-ttu-id="03c24-116">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span><span class="sxs-lookup"><span data-stu-id="03c24-116">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="03c24-117">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="03c24-117">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span></span>

1. <span data-ttu-id="03c24-118">Determine the data center that you want to use to host your SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="03c24-118">Determine the data center that you want to use to host your SQL Server VM.</span></span> <span data-ttu-id="03c24-119">The following PowerShell commands will display the available regions in detail with a summary list at the end.</span><span class="sxs-lookup"><span data-stu-id="03c24-119">The following PowerShell commands will display the available regions in detail with a summary list at the end.</span></span>
   
        Get-AzureLocation
        (Get-AzureLocation).Name
2. <span data-ttu-id="03c24-120">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span><span class="sxs-lookup"><span data-stu-id="03c24-120">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span></span>
   
       $dcLocation = "<region name>"

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="03c24-121">Set your subscription and storage account</span><span class="sxs-lookup"><span data-stu-id="03c24-121">Set your subscription and storage account</span></span>
1. <span data-ttu-id="03c24-122">Determine the Azure subscription you will use for the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="03c24-122">Determine the Azure subscription you will use for the new virtual machine.</span></span>
   
        (Get-AzureSubscription).SubscriptionName
2. <span data-ttu-id="03c24-123">Assign your target Azure subscription to the **$subscr** variable.</span><span class="sxs-lookup"><span data-stu-id="03c24-123">Assign your target Azure subscription to the **$subscr** variable.</span></span> <span data-ttu-id="03c24-124">Then set this as your current Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="03c24-124">Then set this as your current Azure subscription.</span></span>
   
        $subscr="<subscription name>"
        Select-AzureSubscription -SubscriptionName $subscr –Current
3. <span data-ttu-id="03c24-125">Then check for existing storage accounts.</span><span class="sxs-lookup"><span data-stu-id="03c24-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="03c24-126">The following script displays all storage accounts that exist in your chosen region:</span><span class="sxs-lookup"><span data-stu-id="03c24-126">The following script displays all storage accounts that exist in your chosen region:</span></span>
   
        (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   
   > [!NOTE]
   > <span data-ttu-id="03c24-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: **New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation**</span><span class="sxs-lookup"><span data-stu-id="03c24-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: **New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation**</span></span>
   > 
   > 
4. <span data-ttu-id="03c24-128">Assign the target storage account name to the **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="03c24-128">Assign the target storage account name to the **$staccount**.</span></span> <span data-ttu-id="03c24-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span><span class="sxs-lookup"><span data-stu-id="03c24-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span></span>
   
        $staccount="<storage account name>"
        Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="03c24-130">Select a SQL Server virtual machine image</span><span class="sxs-lookup"><span data-stu-id="03c24-130">Select a SQL Server virtual machine image</span></span>
1. <span data-ttu-id="03c24-131">Find out the list of available SQL Server virtual machines images from the gallery.</span><span class="sxs-lookup"><span data-stu-id="03c24-131">Find out the list of available SQL Server virtual machines images from the gallery.</span></span> <span data-ttu-id="03c24-132">These images all have an **ImageFamily** property that starts with "SQL".</span><span class="sxs-lookup"><span data-stu-id="03c24-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="03c24-133">The following query displays the image family available to you that have SQL Server preinstalled.</span><span class="sxs-lookup"><span data-stu-id="03c24-133">The following query displays the image family available to you that have SQL Server preinstalled.</span></span>
   
        Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
2. <span data-ttu-id="03c24-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span><span class="sxs-lookup"><span data-stu-id="03c24-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="03c24-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="03c24-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>
   
        $family="<ImageFamily value>"
        $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
   
        echo "Selected SQL Server image name:"
        echo "   $image"

## <a name="create-the-virtual-machine"></a><span data-ttu-id="03c24-136">Create the virtual machine</span><span class="sxs-lookup"><span data-stu-id="03c24-136">Create the virtual machine</span></span>
<span data-ttu-id="03c24-137">Finally, create the virtual machine with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="03c24-137">Finally, create the virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="03c24-138">Create a cloud service to host the new VM.</span><span class="sxs-lookup"><span data-stu-id="03c24-138">Create a cloud service to host the new VM.</span></span> <span data-ttu-id="03c24-139">Note that it is also possible to use an existing cloud service instead.</span><span class="sxs-lookup"><span data-stu-id="03c24-139">Note that it is also possible to use an existing cloud service instead.</span></span> <span data-ttu-id="03c24-140">Create a new variable **$svcname** with the short name of the cloud service.</span><span class="sxs-lookup"><span data-stu-id="03c24-140">Create a new variable **$svcname** with the short name of the cloud service.</span></span>
   
        $svcname = "<cloud service name>"
        New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
2. <span data-ttu-id="03c24-141">Specify the virtual machine name and a size.</span><span class="sxs-lookup"><span data-stu-id="03c24-141">Specify the virtual machine name and a size.</span></span> <span data-ttu-id="03c24-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03c24-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
   
        $vmname="<machine name>"
        $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
        $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
3. <span data-ttu-id="03c24-143">Specify the local administrator account and password.</span><span class="sxs-lookup"><span data-stu-id="03c24-143">Specify the local administrator account and password.</span></span>
   
        $cred=Get-Credential -Message "Type the name and password of the local administrator account."
        $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
4. <span data-ttu-id="03c24-144">Run the following script to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="03c24-144">Run the following script to create the virtual machine.</span></span>
   
        New-AzureVM –ServiceName $svcname -VMs $vm1

> [!NOTE]
> <span data-ttu-id="03c24-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03c24-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
> 
> 

## <a name="example-powershell-script"></a><span data-ttu-id="03c24-146">Example PowerShell script</span><span class="sxs-lookup"><span data-stu-id="03c24-146">Example PowerShell script</span></span>
<span data-ttu-id="03c24-147">The following script provides and example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span><span class="sxs-lookup"><span data-stu-id="03c24-147">The following script provides and example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="03c24-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span><span class="sxs-lookup"><span data-stu-id="03c24-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span></span>

    # Customize these variables based on your settings and requirements:
    $dcLocation = "East US"
    $subscr="mysubscription"
    $staccount="mystorageaccount"
    $family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
    $svcname = "mycloudservice"
    $vmname="myvirtualmachine"
    $vmsize="A5"

    # Set the current subscription and storage account
    # Comment out the New-AzureStorageAccount line if the account already exists
    Select-AzureSubscription -SubscriptionName $subscr –Current
    New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

    # Select the most recent VM image in this image family:
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    # Create the new cloud service; comment out this line if cloud service exists already:
    New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

    # Create the VM config:
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    # Set administrator credentials:
    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

    # Create the SQL Server VM:
    New-AzureVM –ServiceName $svcname -VMs $vm1


## <a name="connect-with-remote-desktop"></a><span data-ttu-id="03c24-149">Connect with remote desktop</span><span class="sxs-lookup"><span data-stu-id="03c24-149">Connect with remote desktop</span></span>
1. <span data-ttu-id="03c24-150">Create the .RDP files in the current user's document folder to launch these virtual machines to complete setup:</span><span class="sxs-lookup"><span data-stu-id="03c24-150">Create the .RDP files in the current user's document folder to launch these virtual machines to complete setup:</span></span>
   
        $documentspath = [environment]::getfolderpath("mydocuments")
        Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
2. <span data-ttu-id="03c24-151">In the documents directory, launch the RDP file.</span><span class="sxs-lookup"><span data-stu-id="03c24-151">In the documents directory, launch the RDP file.</span></span> <span data-ttu-id="03c24-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span><span class="sxs-lookup"><span data-stu-id="03c24-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span></span>
   
        cd $documentspath
        .\vm1.rdp

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a><span data-ttu-id="03c24-153">Complete the configuration of the SQL Server Machine for remote access</span><span class="sxs-lookup"><span data-stu-id="03c24-153">Complete the configuration of the SQL Server Machine for remote access</span></span>
<span data-ttu-id="03c24-154">After logging onto the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="03c24-154">After logging onto the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="03c24-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="03c24-155">Next steps</span></span>
<span data-ttu-id="03c24-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03c24-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="03c24-157">For additional scripts related to SQL Server and Premium Storage, see [Use Azure Premium Storage with SQL Server on Virtual Machines](../classic/sql-server-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="03c24-157">For additional scripts related to SQL Server and Premium Storage, see [Use Azure Premium Storage with SQL Server on Virtual Machines](../classic/sql-server-premium-storage.md).</span></span>

<span data-ttu-id="03c24-158">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="03c24-158">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span></span> <span data-ttu-id="03c24-159">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03c24-159">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="03c24-160">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="03c24-160">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="03c24-161">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span><span class="sxs-lookup"><span data-stu-id="03c24-161">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="03c24-162">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03c24-162">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

