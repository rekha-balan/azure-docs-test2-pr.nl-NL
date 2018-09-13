---
title: Capture an image of an Azure Windows VM | Microsoft Docs
description: Capture an image of an Azure Windows virtual machine created with the classic deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: cynthn
ms.openlocfilehash: 04de36d8a3bd2f3639cd4cca649386e138fa01bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554160"
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="2f497-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2f497-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2f497-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2f497-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2f497-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2f497-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="2f497-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="2f497-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="2f497-107">For Resource Manager model information, see [Create a copy Windows VM running in Azure](../../virtual-machines-windows-vhd-copy.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f497-107">For Resource Manager model information, see [Create a copy Windows VM running in Azure](../../virtual-machines-windows-vhd-copy.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2f497-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2f497-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="2f497-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f497-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="2f497-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span><span class="sxs-lookup"><span data-stu-id="2f497-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="2f497-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span><span class="sxs-lookup"><span data-stu-id="2f497-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="2f497-112">This is the same place where any images you've uploaded are stored.</span><span class="sxs-lookup"><span data-stu-id="2f497-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="2f497-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f497-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2f497-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2f497-114">Before you begin</span></span>
<span data-ttu-id="2f497-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span><span class="sxs-lookup"><span data-stu-id="2f497-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="2f497-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="2f497-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="2f497-117">Create a virtual machine from an image</span><span class="sxs-lookup"><span data-stu-id="2f497-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="2f497-118">How to attach a data disk to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="2f497-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="2f497-119">Make sure the server roles are supported with Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2f497-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="2f497-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="2f497-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="2f497-121">This process deletes the original virtual machine after it's captured.</span><span class="sxs-lookup"><span data-stu-id="2f497-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="2f497-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span><span class="sxs-lookup"><span data-stu-id="2f497-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="2f497-123">Azure virtual machines can be backed up using Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="2f497-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="2f497-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="2f497-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="2f497-125">Other solutions are available from certified partners.</span><span class="sxs-lookup"><span data-stu-id="2f497-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="2f497-126">To find out what’s currently available, search the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2f497-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="2f497-127">Capture the virtual machine</span><span class="sxs-lookup"><span data-stu-id="2f497-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="2f497-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f497-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="2f497-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="2f497-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="2f497-130">Open a Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2f497-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="2f497-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="2f497-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="2f497-132">The **System Preparation Tool** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="2f497-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="2f497-133">Do the following:</span><span class="sxs-lookup"><span data-stu-id="2f497-133">Do the following:</span></span>

   * <span data-ttu-id="2f497-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span><span class="sxs-lookup"><span data-stu-id="2f497-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="2f497-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="2f497-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="2f497-136">In **Shutdown Options**, select **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="2f497-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="2f497-137">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f497-137">Click **OK**.</span></span>

   ![Run Sysprep](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/sysprepgeneral.png)
5. <span data-ttu-id="2f497-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure classic portal to **Stopped**.</span><span class="sxs-lookup"><span data-stu-id="2f497-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure classic portal to **Stopped**.</span></span>
6. <span data-ttu-id="2f497-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span><span class="sxs-lookup"><span data-stu-id="2f497-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="2f497-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span><span class="sxs-lookup"><span data-stu-id="2f497-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="2f497-142">On the command bar, click **Capture**.</span><span class="sxs-lookup"><span data-stu-id="2f497-142">On the command bar, click **Capture**.</span></span>

   ![Capture virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/capturevm.png)

   <span data-ttu-id="2f497-144">The **Capture the Virtual Machine** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="2f497-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="2f497-145">In **Image name**, type a name for the new image.</span><span class="sxs-lookup"><span data-stu-id="2f497-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="2f497-146">In **Image label**, type a label for the new image.</span><span class="sxs-lookup"><span data-stu-id="2f497-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="2f497-147">Click **I've run Sysprep on the virtual machine**.</span><span class="sxs-lookup"><span data-stu-id="2f497-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="2f497-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span><span class="sxs-lookup"><span data-stu-id="2f497-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="2f497-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span><span class="sxs-lookup"><span data-stu-id="2f497-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="2f497-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span><span class="sxs-lookup"><span data-stu-id="2f497-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![Image capture successful](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/vmcapturedimageavailable.png)

## <a name="next-steps"></a><span data-ttu-id="2f497-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f497-152">Next steps</span></span>
<span data-ttu-id="2f497-153">The image is ready to be used to create virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2f497-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="2f497-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span><span class="sxs-lookup"><span data-stu-id="2f497-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="2f497-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="2f497-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/sysprepgeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/capturevm.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png





