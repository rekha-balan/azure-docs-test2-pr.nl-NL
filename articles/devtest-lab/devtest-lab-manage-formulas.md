---
title: Manage formulas in Azure DevTest Labs to create VMs | Microsoft Docs
description: Learn how to update and remove Azure DevTest Labs formulas
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b55c06e32667e65b7f99ffd335851a637f910e7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556508"
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="f082d-103">Manage Azure DevTest Labs formulas</span><span class="sxs-lookup"><span data-stu-id="f082d-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="f082d-104">The article, [Create Azure DevTest Labs formulas](devtest-lab-create-formulas.md#create-a-formula), walks you through the process of creating a formula in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="f082d-104">The article, [Create Azure DevTest Labs formulas](devtest-lab-create-formulas.md#create-a-formula), walks you through the process of creating a formula in Azure DevTest Labs.</span></span> <span data-ttu-id="f082d-105">Once you have a formula, this article guides you through managing formulas.</span><span class="sxs-lookup"><span data-stu-id="f082d-105">Once you have a formula, this article guides you through managing formulas.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="f082d-106">Modify a formula</span><span class="sxs-lookup"><span data-stu-id="f082d-106">Modify a formula</span></span>
<span data-ttu-id="f082d-107">To modify a formula, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f082d-107">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="f082d-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f082d-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f082d-109">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="f082d-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="f082d-110">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="f082d-110">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="f082d-111">On the lab's blade, select **Formulas (reusable bases)**.</span><span class="sxs-lookup"><span data-stu-id="f082d-111">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formula menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="f082d-113">On the **Lab formulas** blade, select the formula you wish to modify.</span><span class="sxs-lookup"><span data-stu-id="f082d-113">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="f082d-114">On the **Update formula** blade, make the desired edits, and select **Update**.</span><span class="sxs-lookup"><span data-stu-id="f082d-114">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="f082d-115">Delete a formula</span><span class="sxs-lookup"><span data-stu-id="f082d-115">Delete a formula</span></span>
<span data-ttu-id="f082d-116">To delete a formula, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f082d-116">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="f082d-117">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f082d-117">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f082d-118">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="f082d-118">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="f082d-119">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="f082d-119">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="f082d-120">On the lab **Settings** blade, select **Formulas**.</span><span class="sxs-lookup"><span data-stu-id="f082d-120">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Formula menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="f082d-122">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="f082d-122">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Formula menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="f082d-124">On the formula's context menu, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f082d-124">On the formula's context menu, select **Delete**.</span></span>
   
    ![Formula context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="f082d-126">Select **Yes** to the deletion confirmation dialog.</span><span class="sxs-lookup"><span data-stu-id="f082d-126">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="f082d-127">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="f082d-127">Related blog posts</span></span>
* [<span data-ttu-id="f082d-128">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="f082d-128">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="f082d-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="f082d-129">Next steps</span></span>
<span data-ttu-id="f082d-130">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="f082d-130">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>





