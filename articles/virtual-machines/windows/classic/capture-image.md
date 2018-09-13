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
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a>Capture an image of an Azure Windows virtual machine created with the classic deployment model.
> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For Resource Manager model information, see [Create a copy Windows VM running in Azure](../../virtual-machines-windows-vhd-copy.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines. This image includes the operating system disk and any data disks that are attached to the virtual machine. It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.

Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services. This is the same place where any images you've uploaded are stored. For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Before you begin
These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks. If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:

* [Create a virtual machine from an image](createportal.md)
* [How to attach a data disk to a virtual machine](attach-disk.md)
* Make sure the server roles are supported with Sysprep. For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> This process deletes the original virtual machine after it's captured.
>
>

Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up. Azure virtual machines can be backed up using Azure Backup. For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md). Other solutions are available from certified partners. To find out what’s currently available, search the Azure Marketplace.

## <a name="capture-the-virtual-machine"></a>Capture the virtual machine
1. In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine. For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].
2. Open a Command Prompt window as an administrator.
3. Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.
4. The **System Preparation Tool** dialog box appears. Do the following:

   * In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked. For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].
   * In **Shutdown Options**, select **Shutdown**.
   * Click **OK**.

   ![Run Sysprep](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/sysprepgeneral.png)
5. Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure classic portal to **Stopped**.
6. In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture. The **VM images (classic)** group is listed under **Compute** when you view **More services**.

7. On the command bar, click **Capture**.

   ![Capture virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/capturevm.png)

   The **Capture the Virtual Machine** dialog box appears.

8. In **Image name**, type a name for the new image. In **Image label**, type a label for the new image.

9. Click **I've run Sysprep on the virtual machine**. This checkbox refers to the actions with Sysprep in steps 3-5. An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.

10. Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.

    ![Image capture successful](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/vmcapturedimageavailable.png)

## <a name="next-steps"></a>Next steps
The image is ready to be used to create virtual machines. To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group. For instructions, see [Create a virtual machine from an image](createportal.md).

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/sysprepgeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/capture-image/capturevm.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png





