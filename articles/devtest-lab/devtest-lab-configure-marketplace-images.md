---
title: Configure Azure Marketplace image settings in Azure DevTest Labs | Microsoft Docs
description: Configure which Azure Marketplace images can be used when creating a VM in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 8b613624864ab60219583e069bc768c750f25ccf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44668932"
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="c35a5-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c35a5-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="c35a5-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span><span class="sxs-lookup"><span data-stu-id="c35a5-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="c35a5-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span><span class="sxs-lookup"><span data-stu-id="c35a5-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="c35a5-106">This ensures that your team only has access to the Marketplace images they need.</span><span class="sxs-lookup"><span data-stu-id="c35a5-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="c35a5-107">Select which Azure Marketplace images are allowed when creating a VM</span><span class="sxs-lookup"><span data-stu-id="c35a5-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="c35a5-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c35a5-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="c35a5-109">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="c35a5-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="c35a5-110">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="c35a5-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="c35a5-111">On the lab's blade, select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="c35a5-111">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="c35a5-112">On lab's **Configuration** blade, select **Marketplace images**</span><span class="sxs-lookup"><span data-stu-id="c35a5-112">On lab's **Configuration** blade, select **Marketplace images**</span></span>
6. <span data-ttu-id="c35a5-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span><span class="sxs-lookup"><span data-stu-id="c35a5-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="c35a5-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span><span class="sxs-lookup"><span data-stu-id="c35a5-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="c35a5-115">The image creates a single VM, **and**</span><span class="sxs-lookup"><span data-stu-id="c35a5-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="c35a5-116">The image uses Azure Resource Manager to provision VMs, **and**</span><span class="sxs-lookup"><span data-stu-id="c35a5-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="c35a5-117">The image doesn't require purchasing an extra licensing plan</span><span class="sxs-lookup"><span data-stu-id="c35a5-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
     <span data-ttu-id="c35a5-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span><span class="sxs-lookup"><span data-stu-id="c35a5-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![Option to allow all Marketplace images to be used as base images for VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="c35a5-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span><span class="sxs-lookup"><span data-stu-id="c35a5-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="c35a5-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span><span class="sxs-lookup"><span data-stu-id="c35a5-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   <span data-ttu-id="c35a5-122">You can also select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span><span class="sxs-lookup"><span data-stu-id="c35a5-122">You can also select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   <span data-ttu-id="c35a5-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span><span class="sxs-lookup"><span data-stu-id="c35a5-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![You can specify which Azure Marketplace images can be used as base images for VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="c35a5-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="c35a5-125">Next steps</span></span>
<span data-ttu-id="c35a5-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="c35a5-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>



