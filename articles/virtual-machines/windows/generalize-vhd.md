---
title: Generalize a Windows VM to use in Azure | Microsoft Docs
description: Learn to use Sysprep to generalize a Windows VM to use with the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a745d400-c8be-48b4-a891-4a18495ef3fd
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: cynthn
ms.openlocfilehash: beecec579df01bc01ae00aab530e2d8a66cf3116
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551466"
---
# <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Generalize a Windows virtual machine using Sysprep
This section shows you how to generalize your Windows virtual machine for use as an image. Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image. For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Make sure the server roles running on the machine are supported by Sysprep. For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep. 
> 
> 

1. Sign in to the Windows virtual machine.
2. Open the Command Prompt window as an administrator. Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.
3. In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.
4. In **Shutdown Options**, select **Shutdown**.
5. Click **OK**.
   
    ![Start Sysprep](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/upload-generalized-managed/sysprepgeneral.png)
6. When Sysprep completes, it shuts down the virtual machine. 

> [!IMPORTANT]
> Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM. If the VM accidentally gets restarted, run Sysprep to generalize it again.
> 
> 

## <a name="next-steps"></a>Next Steps
* If the VM is on-premises, you can now [upload the VHD to Azure](upload-image.md).
* If the VM is already in Azure, you can now [create an image from the generalized VM](capture-image.md).


