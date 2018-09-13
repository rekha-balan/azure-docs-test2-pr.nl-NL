---
title: Create an Azure DevTest Labs custom image from a VHD file | Microsoft Docs
description: Learn how to create a custom image in Azure DevTest Labs from a VHD file using the Azure portal
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 5cfc90532e516a4c511332e391891a33d99810d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550807"
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="ebe57-103">Create a custom image from a VHD file</span><span class="sxs-lookup"><span data-stu-id="ebe57-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="ebe57-104">Step-by-step instructions</span><span class="sxs-lookup"><span data-stu-id="ebe57-104">Step-by-step instructions</span></span>

<span data-ttu-id="ebe57-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="ebe57-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="ebe57-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ebe57-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="ebe57-107">Select **More services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="ebe57-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="ebe57-108">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="ebe57-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="ebe57-109">On the lab's blade, select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="ebe57-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="ebe57-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="ebe57-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="ebe57-111">On the **Custom images** blade, select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="ebe57-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Add Custom image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="ebe57-113">Enter the name of the custom image.</span><span class="sxs-lookup"><span data-stu-id="ebe57-113">Enter the name of the custom image.</span></span> <span data-ttu-id="ebe57-114">This name is displayed in the list of base images when creating a VM.</span><span class="sxs-lookup"><span data-stu-id="ebe57-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="ebe57-115">Enter the description of the custom image.</span><span class="sxs-lookup"><span data-stu-id="ebe57-115">Enter the description of the custom image.</span></span> <span data-ttu-id="ebe57-116">This description is displayed in the list of base images when creating a VM.</span><span class="sxs-lookup"><span data-stu-id="ebe57-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="ebe57-117">Select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="ebe57-117">Select **VHD**.</span></span>

1. <span data-ttu-id="ebe57-118">From the **VHD** blade, select the desired VHD file.</span><span class="sxs-lookup"><span data-stu-id="ebe57-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="ebe57-119">Select **OK** to close the **VHD** blade.</span><span class="sxs-lookup"><span data-stu-id="ebe57-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="ebe57-120">Select **OS configuration**.</span><span class="sxs-lookup"><span data-stu-id="ebe57-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="ebe57-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="ebe57-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="ebe57-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span><span class="sxs-lookup"><span data-stu-id="ebe57-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="ebe57-123">Select **OK** to close the **OS configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="ebe57-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="ebe57-124">Select **OK** to create the custom image.</span><span class="sxs-lookup"><span data-stu-id="ebe57-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="ebe57-125">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="ebe57-125">Related blog posts</span></span>

- [<span data-ttu-id="ebe57-126">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="ebe57-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="ebe57-127">Copying Custom Images between Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ebe57-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="ebe57-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="ebe57-128">Next steps</span></span>

- [<span data-ttu-id="ebe57-129">Add a VM to your lab</span><span class="sxs-lookup"><span data-stu-id="ebe57-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)

