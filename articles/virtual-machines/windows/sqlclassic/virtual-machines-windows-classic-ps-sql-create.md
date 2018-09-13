---
title: Create a SQL Server Virtual Machine in Azure PowerShell (Classic) | Microsoft Docs
description: Provides steps and PowerShell scripts for creating an Azure VM with SQL Server virtual machine gallery images. This topic uses the classic deployment mode.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: craigg
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 7672d7a278bf0ee20bf3ffdd92395e9c519aba0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809912"
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="3df4e-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="3df4e-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="3df4e-105">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3df4e-105">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3df4e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3df4e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3df4e-107">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="3df4e-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3df4e-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="3df4e-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="3df4e-109">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="3df4e-109">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="3df4e-110">Install and configure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3df4e-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="3df4e-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3df4e-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="3df4e-112">[Download and install the latest Azure PowerShell commands](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3df4e-112">[Download and install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="3df4e-113">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span><span class="sxs-lookup"><span data-stu-id="3df4e-113">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="3df4e-114">Determine your target Azure region</span><span class="sxs-lookup"><span data-stu-id="3df4e-114">Determine your target Azure region</span></span>

<span data-ttu-id="3df4e-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span><span class="sxs-lookup"><span data-stu-id="3df4e-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="3df4e-116">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="3df4e-116">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span></span>

1. <span data-ttu-id="3df4e-117">Determine the data center that you want to use to host your SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="3df4e-117">Determine the data center that you want to use to host your SQL Server VM.</span></span> <span data-ttu-id="3df4e-118">The following PowerShell command displays a list of available region names.</span><span class="sxs-lookup"><span data-stu-id="3df4e-118">The following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="3df4e-119">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span><span class="sxs-lookup"><span data-stu-id="3df4e-119">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span></span> <span data-ttu-id="3df4e-120">For example, the following command sets the region to "East US":</span><span class="sxs-lookup"><span data-stu-id="3df4e-120">For example, the following command sets the region to "East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="3df4e-121">Set your subscription and storage account</span><span class="sxs-lookup"><span data-stu-id="3df4e-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="3df4e-122">Determine the Azure subscription you will use for the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3df4e-122">Determine the Azure subscription you will use for the new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="3df4e-123">Assign your target Azure subscription to the **$subscr** variable.</span><span class="sxs-lookup"><span data-stu-id="3df4e-123">Assign your target Azure subscription to the **$subscr** variable.</span></span> <span data-ttu-id="3df4e-124">Then set this as your current Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3df4e-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="3df4e-125">Then check for existing storage accounts.</span><span class="sxs-lookup"><span data-stu-id="3df4e-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="3df4e-126">The following script displays all storage accounts that exist in your chosen region:</span><span class="sxs-lookup"><span data-stu-id="3df4e-126">The following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="3df4e-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="3df4e-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="3df4e-128">Assign the target storage account name to the **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="3df4e-128">Assign the target storage account name to the **$staccount**.</span></span> <span data-ttu-id="3df4e-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span><span class="sxs-lookup"><span data-stu-id="3df4e-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="3df4e-130">Select a SQL Server virtual machine image</span><span class="sxs-lookup"><span data-stu-id="3df4e-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="3df4e-131">Find out the list of available SQL Server virtual machines images from the gallery.</span><span class="sxs-lookup"><span data-stu-id="3df4e-131">Find out the list of available SQL Server virtual machines images from the gallery.</span></span> <span data-ttu-id="3df4e-132">These images all have an **ImageFamily** property that starts with "SQL".</span><span class="sxs-lookup"><span data-stu-id="3df4e-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="3df4e-133">The following query displays the image family available to you that have SQL Server preinstalled.</span><span class="sxs-lookup"><span data-stu-id="3df4e-133">The following query displays the image family available to you that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="3df4e-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span><span class="sxs-lookup"><span data-stu-id="3df4e-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="3df4e-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="3df4e-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-the-virtual-machine"></a><span data-ttu-id="3df4e-136">Create the virtual machine</span><span class="sxs-lookup"><span data-stu-id="3df4e-136">Create the virtual machine</span></span>

<span data-ttu-id="3df4e-137">Finally, create the virtual machine with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3df4e-137">Finally, create the virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="3df4e-138">Create a cloud service to host the new VM.</span><span class="sxs-lookup"><span data-stu-id="3df4e-138">Create a cloud service to host the new VM.</span></span> <span data-ttu-id="3df4e-139">Note that it is also possible to use an existing cloud service instead.</span><span class="sxs-lookup"><span data-stu-id="3df4e-139">Note that it is also possible to use an existing cloud service instead.</span></span> <span data-ttu-id="3df4e-140">Create a new variable **$svcname** with the short name of the cloud service.</span><span class="sxs-lookup"><span data-stu-id="3df4e-140">Create a new variable **$svcname** with the short name of the cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="3df4e-141">Specify the virtual machine name and a size.</span><span class="sxs-lookup"><span data-stu-id="3df4e-141">Specify the virtual machine name and a size.</span></span> <span data-ttu-id="3df4e-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3df4e-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="3df4e-143">Specify the local administrator account and password.</span><span class="sxs-lookup"><span data-stu-id="3df4e-143">Specify the local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type the name and password of the local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="3df4e-144">Run the following script to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3df4e-144">Run the following script to create the virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="3df4e-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3df4e-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="3df4e-146">Example PowerShell script</span><span class="sxs-lookup"><span data-stu-id="3df4e-146">Example PowerShell script</span></span>

<span data-ttu-id="3df4e-147">The following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3df4e-147">The following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="3df4e-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span><span class="sxs-lookup"><span data-stu-id="3df4e-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span></span>

```powershell
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
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="3df4e-149">Connect with remote desktop</span><span class="sxs-lookup"><span data-stu-id="3df4e-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="3df4e-150">Create the RDP files in the current user's document folder to launch these virtual machines to complete setup:</span><span class="sxs-lookup"><span data-stu-id="3df4e-150">Create the RDP files in the current user's document folder to launch these virtual machines to complete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="3df4e-151">In the documents directory, launch the RDP file.</span><span class="sxs-lookup"><span data-stu-id="3df4e-151">In the documents directory, launch the RDP file.</span></span> <span data-ttu-id="3df4e-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span><span class="sxs-lookup"><span data-stu-id="3df4e-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a><span data-ttu-id="3df4e-153">Complete the configuration of the SQL Server Machine for remote access</span><span class="sxs-lookup"><span data-stu-id="3df4e-153">Complete the configuration of the SQL Server Machine for remote access</span></span>

<span data-ttu-id="3df4e-154">After logging on to the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="3df4e-154">After logging on to the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3df4e-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="3df4e-155">Next steps</span></span>

<span data-ttu-id="3df4e-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3df4e-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="3df4e-157">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="3df4e-157">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span></span> <span data-ttu-id="3df4e-158">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3df4e-158">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="3df4e-159">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="3df4e-159">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="3df4e-160">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span><span class="sxs-lookup"><span data-stu-id="3df4e-160">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="3df4e-161">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3df4e-161">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
