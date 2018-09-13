---
title: Create and upload a VM image using Powershell | Microsoft Docs
description: Learn to create and upload a generalized Windows Server image (VHD) using the classic deployment model and Azure Powershell.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/21/2016
ms.author: cynthn
ms.openlocfilehash: 0faf98be331c2b765dbb0f80b8bcc69743b45bf4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552872"
---
# <a name="create-and-upload-a-windows-server-vhd-to-azure"></a><span data-ttu-id="afb49-103">Create and upload a Windows Server VHD to Azure</span><span class="sxs-lookup"><span data-stu-id="afb49-103">Create and upload a Windows Server VHD to Azure</span></span>
<span data-ttu-id="afb49-104">This article shows you how to upload your own generalized VM image as a virtual hard disk (VHD) so you can use it to create virtual machines.</span><span class="sxs-lookup"><span data-stu-id="afb49-104">This article shows you how to upload your own generalized VM image as a virtual hard disk (VHD) so you can use it to create virtual machines.</span></span> <span data-ttu-id="afb49-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afb49-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afb49-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="afb49-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="afb49-107">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="afb49-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="afb49-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="afb49-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="afb49-109">You can also [upload](../../virtual-machines-windows-upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a virtual machine using the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="afb49-109">You can also [upload](../../virtual-machines-windows-upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a virtual machine using the Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afb49-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="afb49-110">Prerequisites</span></span>
<span data-ttu-id="afb49-111">This article assumes you have:</span><span class="sxs-lookup"><span data-stu-id="afb49-111">This article assumes you have:</span></span>

* <span data-ttu-id="afb49-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="afb49-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="afb49-113">**[Microsoft Azure PowerShell](/powershell/azureps-cmdlets-docs)** - You have the Microsoft Azure PowerShell module installed and configured to use your subscription.</span><span class="sxs-lookup"><span data-stu-id="afb49-113">**[Microsoft Azure PowerShell](/powershell/azureps-cmdlets-docs)** - You have the Microsoft Azure PowerShell module installed and configured to use your subscription.</span></span>
* <span data-ttu-id="afb49-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afb49-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached to a virtual machine.</span></span> <span data-ttu-id="afb49-115">Check to see if the server roles running on the VHD are supported by Sysprep.</span><span class="sxs-lookup"><span data-stu-id="afb49-115">Check to see if the server roles running on the VHD are supported by Sysprep.</span></span> <span data-ttu-id="afb49-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="afb49-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="afb49-117">The VHDX format is not supported in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="afb49-117">The VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="afb49-118">You can convert the disk to VHD format using Hyper-V Manager or the [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="afb49-118">You can convert the disk to VHD format using Hyper-V Manager or the [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="afb49-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="afb49-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-the-vhd"></a><span data-ttu-id="afb49-120">Step 1: Prep the VHD</span><span class="sxs-lookup"><span data-stu-id="afb49-120">Step 1: Prep the VHD</span></span>
<span data-ttu-id="afb49-121">Before you upload the VHD to Azure, it needs to be generalized by using the Sysprep tool.</span><span class="sxs-lookup"><span data-stu-id="afb49-121">Before you upload the VHD to Azure, it needs to be generalized by using the Sysprep tool.</span></span> <span data-ttu-id="afb49-122">This prepares the VHD to be used as an image.</span><span class="sxs-lookup"><span data-stu-id="afb49-122">This prepares the VHD to be used as an image.</span></span> <span data-ttu-id="afb49-123">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="afb49-123">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="afb49-124">Back up the VM before running Sysprep.</span><span class="sxs-lookup"><span data-stu-id="afb49-124">Back up the VM before running Sysprep.</span></span>

<span data-ttu-id="afb49-125">From the virtual machine that the operating system was installed to, complete the following procedure:</span><span class="sxs-lookup"><span data-stu-id="afb49-125">From the virtual machine that the operating system was installed to, complete the following procedure:</span></span>

1. <span data-ttu-id="afb49-126">Sign in to the operating system.</span><span class="sxs-lookup"><span data-stu-id="afb49-126">Sign in to the operating system.</span></span>
2. <span data-ttu-id="afb49-127">Open a command prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="afb49-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="afb49-128">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="afb49-128">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Open a Command Prompt window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="afb49-130">The **System Preparation Tool** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="afb49-130">The **System Preparation Tool** dialog box appears.</span></span>

   ![Start Sysprep](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="afb49-132">In the **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span><span class="sxs-lookup"><span data-stu-id="afb49-132">In the **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="afb49-133">In **Shutdown Options**, select **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="afb49-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="afb49-134">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="afb49-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="afb49-135">Step 2: Create a storage account and a container</span><span class="sxs-lookup"><span data-stu-id="afb49-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="afb49-136">You need a storage account in Azure so you have a place to upload the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="afb49-136">You need a storage account in Azure so you have a place to upload the .vhd file.</span></span> <span data-ttu-id="afb49-137">This step shows you how to create an account, or get the info you need from an existing account.</span><span class="sxs-lookup"><span data-stu-id="afb49-137">This step shows you how to create an account, or get the info you need from an existing account.</span></span> <span data-ttu-id="afb49-138">Replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span><span class="sxs-lookup"><span data-stu-id="afb49-138">Replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="afb49-139">Login</span><span class="sxs-lookup"><span data-stu-id="afb49-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="afb49-140">Set your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="afb49-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="afb49-141">Create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="afb49-141">Create a new storage account.</span></span> <span data-ttu-id="afb49-142">The name of the storage account should be unique, 3-24 characters.</span><span class="sxs-lookup"><span data-stu-id="afb49-142">The name of the storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="afb49-143">The name can be any combination of letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="afb49-143">The name can be any combination of letters and numbers.</span></span> <span data-ttu-id="afb49-144">You also need to specify a location like "East US"</span><span class="sxs-lookup"><span data-stu-id="afb49-144">You also need to specify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="afb49-145">Set the new storage account as the default.</span><span class="sxs-lookup"><span data-stu-id="afb49-145">Set the new storage account as the default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="afb49-146">Create a new container.</span><span class="sxs-lookup"><span data-stu-id="afb49-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-the-vhd-file"></a><span data-ttu-id="afb49-147">Step 3: Upload the .vhd file</span><span class="sxs-lookup"><span data-stu-id="afb49-147">Step 3: Upload the .vhd file</span></span>
<span data-ttu-id="afb49-148">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) to upload the VHD.</span><span class="sxs-lookup"><span data-stu-id="afb49-148">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) to upload the VHD.</span></span>

<span data-ttu-id="afb49-149">From the Azure PowerShell window you used in the previous step, type the following command and replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span><span class="sxs-lookup"><span data-stu-id="afb49-149">From the Azure PowerShell window you used in the previous step, type the following command and replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-the-image-to-your-list-of-custom-images"></a><span data-ttu-id="afb49-150">Step 4: Add the image to your list of custom images</span><span class="sxs-lookup"><span data-stu-id="afb49-150">Step 4: Add the image to your list of custom images</span></span>
<span data-ttu-id="afb49-151">Use the [Add-AzureVMImage](https://msdn.microsoft.com/library/mt589167.aspx) cmdlet to add the image to the list of your custom images.</span><span class="sxs-lookup"><span data-stu-id="afb49-151">Use the [Add-AzureVMImage](https://msdn.microsoft.com/library/mt589167.aspx) cmdlet to add the image to the list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="afb49-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="afb49-152">Next steps</span></span>
<span data-ttu-id="afb49-153">You can now [create a custom VM](createportal.md) using the image you uploaded.</span><span class="sxs-lookup"><span data-stu-id="afb49-153">You can now [create a custom VM](createportal.md) using the image you uploaded.</span></span>


