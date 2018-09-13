---
title: 'Make the D: drive of a VM a data disk | Microsoft Docs'
description: 'Describes how to change drive letters for a Windows VM so that you can use the D: drive as a data drive.'
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: cynthn
ms.openlocfilehash: af2661e831d8926abb61afd999cf53fb07b2186e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548869"
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="5b1b9-103">Use the D: drive as a data drive on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="5b1b9-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="5b1b9-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="5b1b9-105">Never use the temporary disk to store data that you need to keep.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="5b1b9-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="5b1b9-107">A planned or unplanned maintenance event may also trigger this placement.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="5b1b9-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="5b1b9-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="5b1b9-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="5b1b9-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="5b1b9-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="attach-the-data-disk"></a><span data-ttu-id="5b1b9-112">Attach the data disk</span><span class="sxs-lookup"><span data-stu-id="5b1b9-112">Attach the data disk</span></span>
<span data-ttu-id="5b1b9-113">First, you'll need to attach the data disk to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-113">First, you'll need to attach the data disk to the virtual machine.</span></span> 

* <span data-ttu-id="5b1b9-114">To use the portal, see [How to attach a data disk in the Azure portal](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5b1b9-114">To use the portal, see [How to attach a data disk in the Azure portal](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* <span data-ttu-id="5b1b9-115">To use the classic portal, see [How to attach a data disk to a Windows virtual machine](classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b1b9-115">To use the classic portal, see [How to attach a data disk to a Windows virtual machine](classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> 

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="5b1b9-116">Temporarily move pagefile.sys to C drive</span><span class="sxs-lookup"><span data-stu-id="5b1b9-116">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="5b1b9-117">Connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-117">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="5b1b9-118">Right-click the **Start** menu and select **System**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-118">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="5b1b9-119">In the left-hand menu, select **Advanced system settings**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-119">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="5b1b9-120">In the **Performance** section, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-120">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="5b1b9-121">Select the **Advanced** tab.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-121">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="5b1b9-122">In the **Virtual memory** section, select **Change**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-122">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="5b1b9-123">Select the **C** drive and then click **System managed size** and then click **Set**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-123">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="5b1b9-124">Select the **D** drive and then click **No paging file** and then click **Set**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-124">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="5b1b9-125">Click Apply.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-125">Click Apply.</span></span> <span data-ttu-id="5b1b9-126">You will get a warning that the computer needs to be restarted for the changes to take affect.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-126">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="5b1b9-127">Restart the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-127">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="5b1b9-128">Change the drive letters</span><span class="sxs-lookup"><span data-stu-id="5b1b9-128">Change the drive letters</span></span>
1. <span data-ttu-id="5b1b9-129">Once the VM restarts, log back on to the VM.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-129">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="5b1b9-130">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-130">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="5b1b9-131">Disk Management will start.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-131">Disk Management will start.</span></span>
3. <span data-ttu-id="5b1b9-132">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-132">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="5b1b9-133">Under Drive letter, select a new drive such as **T** and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-133">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="5b1b9-134">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-134">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="5b1b9-135">Under Drive letter, select drive **D** and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-135">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="5b1b9-136">Move pagefile.sys back to the temporary storage drive</span><span class="sxs-lookup"><span data-stu-id="5b1b9-136">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="5b1b9-137">Right-click the **Start** menu and select **System**</span><span class="sxs-lookup"><span data-stu-id="5b1b9-137">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="5b1b9-138">In the left-hand menu, select **Advanced system settings**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-138">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="5b1b9-139">In the **Performance** section, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-139">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="5b1b9-140">Select the **Advanced** tab.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-140">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="5b1b9-141">In the **Virtual memory** section, select **Change**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-141">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="5b1b9-142">Select the OS drive **C** and click **No paging file** and then click **Set**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-142">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="5b1b9-143">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-143">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="5b1b9-144">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-144">Click **Apply**.</span></span> <span data-ttu-id="5b1b9-145">You will get a warning that the computer needs to be restarted for the changes to take affect.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-145">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="5b1b9-146">Restart the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5b1b9-146">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1b9-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b1b9-147">Next steps</span></span>
* <span data-ttu-id="5b1b9-148">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b1b9-148">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

