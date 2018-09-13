---
title: Manage VM artifacts in Azure DevTest Labs | Microsoft Docs
description: Learn how to manage VM artifacts in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 576509ce-6a33-4c26-87c7-de8b40271efa
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: ece36316fdf3044f1e1d9dbdc41ea0b14633e89e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555134"
---
# <a name="manage-vm-artifacts-in-azure-devtest-labs"></a><span data-ttu-id="09ca2-103">Manage VM artifacts in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="09ca2-103">Manage VM artifacts in Azure DevTest Labs</span></span>
<span data-ttu-id="09ca2-104">Azure DevTest Labs *artifacts* let you specify *actions* that are performed when the VM is provisioned.</span><span class="sxs-lookup"><span data-stu-id="09ca2-104">Azure DevTest Labs *artifacts* let you specify *actions* that are performed when the VM is provisioned.</span></span> 

<span data-ttu-id="09ca2-105">Artifact actions can perform procedures such as running Windows PowerShell scripts, running Bash commands, and installing software.</span><span class="sxs-lookup"><span data-stu-id="09ca2-105">Artifact actions can perform procedures such as running Windows PowerShell scripts, running Bash commands, and installing software.</span></span> 

<span data-ttu-id="09ca2-106">Artifact *parameters* let you customize the artifact for your particular scenario.</span><span class="sxs-lookup"><span data-stu-id="09ca2-106">Artifact *parameters* let you customize the artifact for your particular scenario.</span></span>

<span data-ttu-id="09ca2-107">This article shows you how to manage the artifacts for a VM in your lab.</span><span class="sxs-lookup"><span data-stu-id="09ca2-107">This article shows you how to manage the artifacts for a VM in your lab.</span></span>

## <a name="add-an-existing-artifact-to-a-vm"></a><span data-ttu-id="09ca2-108">Add an existing artifact to a VM</span><span class="sxs-lookup"><span data-stu-id="09ca2-108">Add an existing artifact to a VM</span></span>
<span data-ttu-id="09ca2-109">While creating a VM, you can add existing artifacts.</span><span class="sxs-lookup"><span data-stu-id="09ca2-109">While creating a VM, you can add existing artifacts.</span></span> <span data-ttu-id="09ca2-110">Each lab includes artifacts from the Public DevTest Labs Artifact Repository as well as artifacts that you've created and added to your own Artifact Repository.</span><span class="sxs-lookup"><span data-stu-id="09ca2-110">Each lab includes artifacts from the Public DevTest Labs Artifact Repository as well as artifacts that you've created and added to your own Artifact Repository.</span></span>
<span data-ttu-id="09ca2-111">To discover how to create artifacts, see the article, [Learn how to author your own artifacts for use with DevTest Labs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="09ca2-111">To discover how to create artifacts, see the article, [Learn how to author your own artifacts for use with DevTest Labs](devtest-lab-artifact-author.md).</span></span>

1. <span data-ttu-id="09ca2-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="09ca2-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="09ca2-113">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="09ca2-113">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="09ca2-114">From the list of labs, select the lab containing the VM with which you want to work.</span><span class="sxs-lookup"><span data-stu-id="09ca2-114">From the list of labs, select the lab containing the VM with which you want to work.</span></span>  
1. <span data-ttu-id="09ca2-115">Select **My virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="09ca2-115">Select **My virtual machines**.</span></span>
1. <span data-ttu-id="09ca2-116">Select the desired VM.</span><span class="sxs-lookup"><span data-stu-id="09ca2-116">Select the desired VM.</span></span>
1. <span data-ttu-id="09ca2-117">Select **Artifacts**.</span><span class="sxs-lookup"><span data-stu-id="09ca2-117">Select **Artifacts**.</span></span> 
1. <span data-ttu-id="09ca2-118">Select **Apply artifacts**.</span><span class="sxs-lookup"><span data-stu-id="09ca2-118">Select **Apply artifacts**.</span></span>
1. <span data-ttu-id="09ca2-119">On the **Apply artifacts** blade, select the artifact you wish to add to the VM.</span><span class="sxs-lookup"><span data-stu-id="09ca2-119">On the **Apply artifacts** blade, select the artifact you wish to add to the VM.</span></span>
1. <span data-ttu-id="09ca2-120">On the **Add artifact** blade, enter the required parameter values and any optional parameters that you need.</span><span class="sxs-lookup"><span data-stu-id="09ca2-120">On the **Add artifact** blade, enter the required parameter values and any optional parameters that you need.</span></span>  
1. <span data-ttu-id="09ca2-121">Select **Add** to add the artifact and return to the **Apply artifacts** blade.</span><span class="sxs-lookup"><span data-stu-id="09ca2-121">Select **Add** to add the artifact and return to the **Apply artifacts** blade.</span></span>
1. <span data-ttu-id="09ca2-122">Continue adding artifacts as needed for your VM.</span><span class="sxs-lookup"><span data-stu-id="09ca2-122">Continue adding artifacts as needed for your VM.</span></span>
1. <span data-ttu-id="09ca2-123">Once you've added your artifacts, you can [change the order in which the artifacts are run](#change-the-order-in-which-artifacts-are-run).</span><span class="sxs-lookup"><span data-stu-id="09ca2-123">Once you've added your artifacts, you can [change the order in which the artifacts are run](#change-the-order-in-which-artifacts-are-run).</span></span> <span data-ttu-id="09ca2-124">You can also go back to [view or modify an artifact](#view-or-modify-an-artifact).</span><span class="sxs-lookup"><span data-stu-id="09ca2-124">You can also go back to [view or modify an artifact](#view-or-modify-an-artifact).</span></span>
1. <span data-ttu-id="09ca2-125">When you're done adding artifacts, select **Apply**</span><span class="sxs-lookup"><span data-stu-id="09ca2-125">When you're done adding artifacts, select **Apply**</span></span>

## <a name="change-the-order-in-which-artifacts-are-run"></a><span data-ttu-id="09ca2-126">Change the order in which artifacts are run</span><span class="sxs-lookup"><span data-stu-id="09ca2-126">Change the order in which artifacts are run</span></span>
<span data-ttu-id="09ca2-127">By default, the actions of the artifacts are executed in the order in which they are added to the VM.</span><span class="sxs-lookup"><span data-stu-id="09ca2-127">By default, the actions of the artifacts are executed in the order in which they are added to the VM.</span></span> <span data-ttu-id="09ca2-128">The following steps illustrate how to change the order in which the artifacts are run.</span><span class="sxs-lookup"><span data-stu-id="09ca2-128">The following steps illustrate how to change the order in which the artifacts are run.</span></span>

1. <span data-ttu-id="09ca2-129">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span><span class="sxs-lookup"><span data-stu-id="09ca2-129">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![Number of artifacts added to VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="09ca2-131">On the **Selected artifacts** blade, drag and drop the artifacts into the desired order.</span><span class="sxs-lookup"><span data-stu-id="09ca2-131">On the **Selected artifacts** blade, drag and drop the artifacts into the desired order.</span></span> <span data-ttu-id="09ca2-132">**Note:** If you have trouble dragging the artifact, make sure that you are dragging from the left side of the artifact.</span><span class="sxs-lookup"><span data-stu-id="09ca2-132">**Note:** If you have trouble dragging the artifact, make sure that you are dragging from the left side of the artifact.</span></span> 
1. <span data-ttu-id="09ca2-133">Select **OK** when done.</span><span class="sxs-lookup"><span data-stu-id="09ca2-133">Select **OK** when done.</span></span>  

## <a name="view-or-modify-an-artifact"></a><span data-ttu-id="09ca2-134">View or modify an artifact</span><span class="sxs-lookup"><span data-stu-id="09ca2-134">View or modify an artifact</span></span>
<span data-ttu-id="09ca2-135">The following steps illustrate how to view or modify the parameters of an artifact:</span><span class="sxs-lookup"><span data-stu-id="09ca2-135">The following steps illustrate how to view or modify the parameters of an artifact:</span></span>

1. <span data-ttu-id="09ca2-136">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span><span class="sxs-lookup"><span data-stu-id="09ca2-136">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![Number of artifacts added to VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="09ca2-138">On the **Selected artifacts** blade, select the artifact that you want to view or edit.</span><span class="sxs-lookup"><span data-stu-id="09ca2-138">On the **Selected artifacts** blade, select the artifact that you want to view or edit.</span></span>  
1. <span data-ttu-id="09ca2-139">On the **Add artifact** blade, make any needed changes, and select **OK** to close the **Add artifact** blade.</span><span class="sxs-lookup"><span data-stu-id="09ca2-139">On the **Add artifact** blade, make any needed changes, and select **OK** to close the **Add artifact** blade.</span></span>
1. <span data-ttu-id="09ca2-140">Select **OK** to close the **Selected artifacts** blade.</span><span class="sxs-lookup"><span data-stu-id="09ca2-140">Select **OK** to close the **Selected artifacts** blade.</span></span>

## <a name="save-azure-resource-manager-template"></a><span data-ttu-id="09ca2-141">Save Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="09ca2-141">Save Azure Resource Manager template</span></span>
<span data-ttu-id="09ca2-142">An Azure Resource Manager template provides a declarative way to define a repeatable deployment.</span><span class="sxs-lookup"><span data-stu-id="09ca2-142">An Azure Resource Manager template provides a declarative way to define a repeatable deployment.</span></span> <span data-ttu-id="09ca2-143">The following steps explain how to save the Azure Resource Manager template for the VM being created.</span><span class="sxs-lookup"><span data-stu-id="09ca2-143">The following steps explain how to save the Azure Resource Manager template for the VM being created.</span></span>
<span data-ttu-id="09ca2-144">Once saved, you can use the Azure Resource Manager template to [deploy new VMs with Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).</span><span class="sxs-lookup"><span data-stu-id="09ca2-144">Once saved, you can use the Azure Resource Manager template to [deploy new VMs with Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span>

1. <span data-ttu-id="09ca2-145">On the **Virtual machine** blade, select **View ARM Template**.</span><span class="sxs-lookup"><span data-stu-id="09ca2-145">On the **Virtual machine** blade, select **View ARM Template**.</span></span>
2. <span data-ttu-id="09ca2-146">On the **View Azure Resource Manager template** blade, select the template text.</span><span class="sxs-lookup"><span data-stu-id="09ca2-146">On the **View Azure Resource Manager template** blade, select the template text.</span></span>
3. <span data-ttu-id="09ca2-147">Copy the selected text to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="09ca2-147">Copy the selected text to the clipboard.</span></span>
4. <span data-ttu-id="09ca2-148">Select **OK** to close the **View Azure Resource Manager Template blade**.</span><span class="sxs-lookup"><span data-stu-id="09ca2-148">Select **OK** to close the **View Azure Resource Manager Template blade**.</span></span>
5. <span data-ttu-id="09ca2-149">Open a text editor.</span><span class="sxs-lookup"><span data-stu-id="09ca2-149">Open a text editor.</span></span>
6. <span data-ttu-id="09ca2-150">Paste in the template text from the clipboard.</span><span class="sxs-lookup"><span data-stu-id="09ca2-150">Paste in the template text from the clipboard.</span></span>
7. <span data-ttu-id="09ca2-151">Save the file for later use.</span><span class="sxs-lookup"><span data-stu-id="09ca2-151">Save the file for later use.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="09ca2-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="09ca2-152">Next steps</span></span>
* <span data-ttu-id="09ca2-153">Learn how to [create custom artifacts for your DevTest Labs VM](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="09ca2-153">Learn how to [create custom artifacts for your DevTest Labs VM](devtest-lab-artifact-author.md).</span></span>


