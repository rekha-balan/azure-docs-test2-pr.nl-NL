---
title: Create an Azure RemoteApp image based on an Azure VM | Microsoft Docs
description: Learn how to create an image for Azure RemoteApp by starting with an Azure virtual machine.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c7ecd590503fcd2bc3ba06919a2f1a5c0fd0943e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661374"
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="fe58f-103">Create a Azure RemoteApp image based on an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="fe58f-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fe58f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="fe58f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fe58f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="fe58f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fe58f-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fe58f-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="fe58f-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span><span class="sxs-lookup"><span data-stu-id="fe58f-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="fe58f-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span><span class="sxs-lookup"><span data-stu-id="fe58f-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span></span>

<span data-ttu-id="fe58f-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fe58f-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="fe58f-110">Create a custom image based on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="fe58f-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="fe58f-111">Use these steps to create an image based on an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="fe58f-111">Use these steps to create an image based on an Azure VM.</span></span>

1. <span data-ttu-id="fe58f-112">Create an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fe58f-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="fe58f-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span><span class="sxs-lookup"><span data-stu-id="fe58f-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span></span> <span data-ttu-id="fe58f-114">This image meets all the Azure RemoteApp template image requirements.</span><span class="sxs-lookup"><span data-stu-id="fe58f-114">This image meets all the Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="fe58f-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe58f-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="fe58f-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fe58f-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span></span> <span data-ttu-id="fe58f-117">Make sure to perform any additional Windows configurations required by your apps.</span><span class="sxs-lookup"><span data-stu-id="fe58f-117">Make sure to perform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="fe58f-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe58f-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="fe58f-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="fe58f-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span></span> <span data-ttu-id="fe58f-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span><span class="sxs-lookup"><span data-stu-id="fe58f-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span></span> <span data-ttu-id="fe58f-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span><span class="sxs-lookup"><span data-stu-id="fe58f-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span></span>
4. <span data-ttu-id="fe58f-122">SYSPREP generalize and capture the image.</span><span class="sxs-lookup"><span data-stu-id="fe58f-122">SYSPREP generalize and capture the image.</span></span> <span data-ttu-id="fe58f-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span><span class="sxs-lookup"><span data-stu-id="fe58f-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a><span data-ttu-id="fe58f-124">Import the image into the Azure RemoteApp image library</span><span class="sxs-lookup"><span data-stu-id="fe58f-124">Import the image into the Azure RemoteApp image library</span></span>
<span data-ttu-id="fe58f-125">Use these steps to import the new image into Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="fe58f-125">Use these steps to import the new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="fe58f-126">In the **Template Images** tab:</span><span class="sxs-lookup"><span data-stu-id="fe58f-126">In the **Template Images** tab:</span></span>
   
   * <span data-ttu-id="fe58f-127">If you have no existing images, click **Upload or Import a Template Image**.</span><span class="sxs-lookup"><span data-stu-id="fe58f-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="fe58f-128">If you have at least one image already, click **+** to add a new image.</span><span class="sxs-lookup"><span data-stu-id="fe58f-128">If you have at least one image already, click **+** to add a new image.</span></span>
2. <span data-ttu-id="fe58f-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe58f-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="fe58f-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span><span class="sxs-lookup"><span data-stu-id="fe58f-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span></span> <span data-ttu-id="fe58f-131">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fe58f-131">Click **Next**.</span></span>
4. <span data-ttu-id="fe58f-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span><span class="sxs-lookup"><span data-stu-id="fe58f-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span></span>

> [!NOTE]
> <span data-ttu-id="fe58f-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fe58f-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="fe58f-134">Depending on the locations the import can take up to 25 minutes.</span><span class="sxs-lookup"><span data-stu-id="fe58f-134">Depending on the locations the import can take up to 25 minutes.</span></span>
> 
> 

<span data-ttu-id="fe58f-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span><span class="sxs-lookup"><span data-stu-id="fe58f-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

