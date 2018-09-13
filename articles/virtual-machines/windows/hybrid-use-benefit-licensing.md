---
title: Azure Hybrid Use Benefit for Window Server and Windows Client| Microsoft Docs
description: Learn how to maximize your Windows Software Assurance benefits to bring on-premises licenses to Azure
services: virtual-machines-windows
documentationcenter: ''
author: george-moore
manager: timlt
editor: ''
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 4/10/2017
ms.author: georgem
ms.openlocfilehash: 9c4f88f3fcfe9a9582bb7bfe6d1c1baef83f612b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563584"
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="13c63-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span><span class="sxs-lookup"><span data-stu-id="13c63-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="13c63-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you to use your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span><span class="sxs-lookup"><span data-stu-id="13c63-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you to use your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="13c63-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="13c63-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="13c63-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span><span class="sxs-lookup"><span data-stu-id="13c63-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="13c63-107">For more information, please see the [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="13c63-107">For more information, please see the [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="13c63-108">Azure Hybrid Use Benefits for WIndows Client is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="13c63-108">Azure Hybrid Use Benefits for WIndows Client is currently in Preview.</span></span> <span data-ttu-id="13c63-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span><span class="sxs-lookup"><span data-stu-id="13c63-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-to-use-azure-hybrid-use-benefit"></a><span data-ttu-id="13c63-110">Ways to use Azure Hybrid Use Benefit</span><span class="sxs-lookup"><span data-stu-id="13c63-110">Ways to use Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="13c63-111">There are a couple of different ways to deploy Windows VMs with the Azure Hybrid Use Benefit:</span><span class="sxs-lookup"><span data-stu-id="13c63-111">There are a couple of different ways to deploy Windows VMs with the Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="13c63-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="13c63-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="13c63-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="13c63-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-the-azure-marketplace"></a><span data-ttu-id="13c63-114">Deploy a VM using the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="13c63-114">Deploy a VM using the Azure Marketplace</span></span>
<span data-ttu-id="13c63-115">Following images are available in the Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="13c63-115">Following images are available in the Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="13c63-116">These images can be deployed directly from the Azure portal, Resource Manager templates, or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13c63-116">These images can be deployed directly from the Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="13c63-117">You can deploy these images directly from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="13c63-117">You can deploy these images directly from the Azure portal.</span></span> <span data-ttu-id="13c63-118">For use in Resource Manager templates and with Azure PowerShell, view the list of images as follows:</span><span class="sxs-lookup"><span data-stu-id="13c63-118">For use in Resource Manager templates and with Azure PowerShell, view the list of images as follows:</span></span>

<span data-ttu-id="13c63-119">For Windows Server:</span><span class="sxs-lookup"><span data-stu-id="13c63-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
<span data-ttu-id="13c63-120">2016-Datacenter version 2016.127.20170406 or above</span><span class="sxs-lookup"><span data-stu-id="13c63-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

<span data-ttu-id="13c63-121">2012-R2-Datacenter version 4.127.20170406 or above</span><span class="sxs-lookup"><span data-stu-id="13c63-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

<span data-ttu-id="13c63-122">2012-Datacenter version 3.127.20170406 or above</span><span class="sxs-lookup"><span data-stu-id="13c63-122">2012-Datacenter version 3.127.20170406 or above</span></span>

<span data-ttu-id="13c63-123">2008-R2-SP1 version 2.127.20170406 or above</span><span class="sxs-lookup"><span data-stu-id="13c63-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="13c63-124">For Windows Client:</span><span class="sxs-lookup"><span data-stu-id="13c63-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-vhd"></a><span data-ttu-id="13c63-125">Upload a Windows VHD</span><span class="sxs-lookup"><span data-stu-id="13c63-125">Upload a Windows VHD</span></span>
<span data-ttu-id="13c63-126">To deploy a Windows VM in Azure, you first need to create a VHD that contains your base Windows build.</span><span class="sxs-lookup"><span data-stu-id="13c63-126">To deploy a Windows VM in Azure, you first need to create a VHD that contains your base Windows build.</span></span> <span data-ttu-id="13c63-127">This VHD must be appropriately prepared via Sysprep before you upload it to Azure.</span><span class="sxs-lookup"><span data-stu-id="13c63-127">This VHD must be appropriately prepared via Sysprep before you upload it to Azure.</span></span> <span data-ttu-id="13c63-128">You can [read more about the VHD requirements and Sysprep process](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="13c63-128">You can [read more about the VHD requirements and Sysprep process](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="13c63-129">Back up the VM before running Sysprep.</span><span class="sxs-lookup"><span data-stu-id="13c63-129">Back up the VM before running Sysprep.</span></span> 

<span data-ttu-id="13c63-130">Make sure you have [installed and configured the latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="13c63-130">Make sure you have [installed and configured the latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="13c63-131">Once you have prepared your VHD, upload the VHD to your Azure Storage account using the `Add-AzureRmVhd` cmdlet as follows:</span><span class="sxs-lookup"><span data-stu-id="13c63-131">Once you have prepared your VHD, upload the VHD to your Azure Storage account using the `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="13c63-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span><span class="sxs-lookup"><span data-stu-id="13c63-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="13c63-133">You still need to prepare the Windows Server image by installing your application components and providing license keys accordingly, then uploading the disk image to Azure.</span><span class="sxs-lookup"><span data-stu-id="13c63-133">You still need to prepare the Windows Server image by installing your application components and providing license keys accordingly, then uploading the disk image to Azure.</span></span> <span data-ttu-id="13c63-134">Review the appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="13c63-134">Review the appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="13c63-135">You can also read more about [uploading the VHD to Azure process](upload-image.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="13c63-135">You can also read more about [uploading the VHD to Azure process](upload-image.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-an-uploaded-vm-via-resource-manager"></a><span data-ttu-id="13c63-136">Deploy an uploaded VM via Resource Manager</span><span class="sxs-lookup"><span data-stu-id="13c63-136">Deploy an uploaded VM via Resource Manager</span></span>
<span data-ttu-id="13c63-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span><span class="sxs-lookup"><span data-stu-id="13c63-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="13c63-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="13c63-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="13c63-139">Once you have your VHD uploaded to Azure, edit you Resource Manager template to include the license type as part of the compute provider and deploy your template as normal:</span><span class="sxs-lookup"><span data-stu-id="13c63-139">Once you have your VHD uploaded to Azure, edit you Resource Manager template to include the license type as part of the compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="13c63-140">For Windows Server:</span><span class="sxs-lookup"><span data-stu-id="13c63-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="13c63-141">For Windows Client:</span><span class="sxs-lookup"><span data-stu-id="13c63-141">For Windows Client:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-an-uploaded-vm-via-powershell-quickstart"></a><span data-ttu-id="13c63-142">Deploy an uploaded VM via PowerShell quickstart</span><span class="sxs-lookup"><span data-stu-id="13c63-142">Deploy an uploaded VM via PowerShell quickstart</span></span>
<span data-ttu-id="13c63-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="13c63-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="13c63-144">Once you have your VHD uploaded to Azure, you create a VM using `New-AzureRmVM` and specify the licensing type as follows:</span><span class="sxs-lookup"><span data-stu-id="13c63-144">Once you have your VHD uploaded to Azure, you create a VM using `New-AzureRmVM` and specify the licensing type as follows:</span></span>

<span data-ttu-id="13c63-145">For Windows Server:</span><span class="sxs-lookup"><span data-stu-id="13c63-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="13c63-146">For Windows Client:</span><span class="sxs-lookup"><span data-stu-id="13c63-146">For Windows Client:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="13c63-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on the different steps to [create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13c63-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on the different steps to [create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-the-licensing-benefit"></a><span data-ttu-id="13c63-148">Verify your VM is utilizing the licensing benefit</span><span class="sxs-lookup"><span data-stu-id="13c63-148">Verify your VM is utilizing the licensing benefit</span></span>
<span data-ttu-id="13c63-149">Once you have deployed your VM through either the PowerShell or Resource Manager deployment method, verify the license type with `Get-AzureRmVM` as follows:</span><span class="sxs-lookup"><span data-stu-id="13c63-149">Once you have deployed your VM through either the PowerShell or Resource Manager deployment method, verify the license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="13c63-150">The output is similar to the following example for Windows Server:</span><span class="sxs-lookup"><span data-stu-id="13c63-150">The output is similar to the following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="13c63-151">This output contrasts with the following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from the Azure Gallery:</span><span class="sxs-lookup"><span data-stu-id="13c63-151">This output contrasts with the following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from the Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="13c63-152">Detailed PowerShell deployment walkthrough</span><span class="sxs-lookup"><span data-stu-id="13c63-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="13c63-153">The following detailed PowerShell steps show a full deployment of a VM.</span><span class="sxs-lookup"><span data-stu-id="13c63-153">The following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="13c63-154">You can read more context as to the actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13c63-154">You can read more context as to the actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="13c63-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span><span class="sxs-lookup"><span data-stu-id="13c63-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="13c63-156">First, securely obtain credentials, set a location, and resource group name:</span><span class="sxs-lookup"><span data-stu-id="13c63-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="13c63-157">Create a public IP:</span><span class="sxs-lookup"><span data-stu-id="13c63-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="13c63-158">Define your subnet, NIC, and VNET:</span><span class="sxs-lookup"><span data-stu-id="13c63-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="13c63-159">Name your VM and create a VM config:</span><span class="sxs-lookup"><span data-stu-id="13c63-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="13c63-160">Define your OS:</span><span class="sxs-lookup"><span data-stu-id="13c63-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="13c63-161">Add your NIC to the VM:</span><span class="sxs-lookup"><span data-stu-id="13c63-161">Add your NIC to the VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="13c63-162">Define the storage account to use:</span><span class="sxs-lookup"><span data-stu-id="13c63-162">Define the storage account to use:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="13c63-163">Upload your VHD, suitably prepared, and attach to your VM for use:</span><span class="sxs-lookup"><span data-stu-id="13c63-163">Upload your VHD, suitably prepared, and attach to your VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="13c63-164">Finally, create your VM and define the licensing type to utilize Azure Hybrid Use Benefit:</span><span class="sxs-lookup"><span data-stu-id="13c63-164">Finally, create your VM and define the licensing type to utilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="13c63-165">For Windows Server:</span><span class="sxs-lookup"><span data-stu-id="13c63-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="13c63-166">For Windows Client:</span><span class="sxs-lookup"><span data-stu-id="13c63-166">For Windows Client:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Client"
```

## <a name="next-steps"></a><span data-ttu-id="13c63-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="13c63-167">Next steps</span></span>
<span data-ttu-id="13c63-168">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="13c63-168">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="13c63-169">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13c63-169">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="13c63-170">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications to Azure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="13c63-170">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications to Azure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
