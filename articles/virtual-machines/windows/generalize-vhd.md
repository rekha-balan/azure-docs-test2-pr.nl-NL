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
# <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="98256-103">Generalize a Windows virtual machine using Sysprep</span><span class="sxs-lookup"><span data-stu-id="98256-103">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="98256-104">This section shows you how to generalize your Windows virtual machine for use as an image.</span><span class="sxs-lookup"><span data-stu-id="98256-104">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="98256-105">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span><span class="sxs-lookup"><span data-stu-id="98256-105">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="98256-106">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="98256-106">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="98256-107">Make sure the server roles running on the machine are supported by Sysprep.</span><span class="sxs-lookup"><span data-stu-id="98256-107">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="98256-108">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="98256-108">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98256-109">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span><span class="sxs-lookup"><span data-stu-id="98256-109">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="98256-110">Sign in to the Windows virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98256-110">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="98256-111">Open the Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="98256-111">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="98256-112">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="98256-112">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="98256-113">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="98256-113">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="98256-114">In **Shutdown Options**, select **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="98256-114">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="98256-115">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="98256-115">Click **OK**.</span></span>
   
    ![Start Sysprep](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="98256-117">When Sysprep completes, it shuts down the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98256-117">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="98256-118">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span><span class="sxs-lookup"><span data-stu-id="98256-118">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="98256-119">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span><span class="sxs-lookup"><span data-stu-id="98256-119">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="98256-120">Next Steps</span><span class="sxs-lookup"><span data-stu-id="98256-120">Next Steps</span></span>
* <span data-ttu-id="98256-121">If the VM is on-premises, you can now [upload the VHD to Azure](upload-image.md).</span><span class="sxs-lookup"><span data-stu-id="98256-121">If the VM is on-premises, you can now [upload the VHD to Azure](upload-image.md).</span></span>
* <span data-ttu-id="98256-122">If the VM is already in Azure, you can now [create an image from the generalized VM](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="98256-122">If the VM is already in Azure, you can now [create an image from the generalized VM](capture-image.md).</span></span>


