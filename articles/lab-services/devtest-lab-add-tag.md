---
title: Add tags to a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to add a tag to a lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.assetid: dc5b327a-62e4-41bc-80ef-deb3c23d51b2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 3d9a5b3c0ae0b6058d3e8ccf8cdb340bd1200edc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857093"
---
# <a name="add-tags-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="6e587-103">Add tags to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6e587-103">Add tags to a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="6e587-104">You can create custom tags and apply them to your DevTest Labs resources to logically categorize your resources.</span><span class="sxs-lookup"><span data-stu-id="6e587-104">You can create custom tags and apply them to your DevTest Labs resources to logically categorize your resources.</span></span> <span data-ttu-id="6e587-105">Later, you can quickly and easily see all the resources in your subscription that have that tag.</span><span class="sxs-lookup"><span data-stu-id="6e587-105">Later, you can quickly and easily see all the resources in your subscription that have that tag.</span></span> <span data-ttu-id="6e587-106">Tags are helpful when you need to organize resources for billing or management.</span><span class="sxs-lookup"><span data-stu-id="6e587-106">Tags are helpful when you need to organize resources for billing or management.</span></span>

<span data-ttu-id="6e587-107">Resources that are supported by tags include</span><span class="sxs-lookup"><span data-stu-id="6e587-107">Resources that are supported by tags include</span></span>

* <span data-ttu-id="6e587-108">Compute VMs</span><span class="sxs-lookup"><span data-stu-id="6e587-108">Compute VMs</span></span>
* <span data-ttu-id="6e587-109">NICs</span><span class="sxs-lookup"><span data-stu-id="6e587-109">NICs</span></span>
* <span data-ttu-id="6e587-110">IP addresses</span><span class="sxs-lookup"><span data-stu-id="6e587-110">IP addresses</span></span>
* <span data-ttu-id="6e587-111">Load balancers</span><span class="sxs-lookup"><span data-stu-id="6e587-111">Load balancers</span></span>
* <span data-ttu-id="6e587-112">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="6e587-112">Storage accounts</span></span>
* <span data-ttu-id="6e587-113">Managed disks</span><span class="sxs-lookup"><span data-stu-id="6e587-113">Managed disks</span></span>

<span data-ttu-id="6e587-114">You can apply tags when you [Create a lab](devtest-lab-create-lab.md) and later manage them through the Tags blade under Configuration and settings.</span><span class="sxs-lookup"><span data-stu-id="6e587-114">You can apply tags when you [Create a lab](devtest-lab-create-lab.md) and later manage them through the Tags blade under Configuration and settings.</span></span>

<span data-ttu-id="6e587-115">Every tag is made up of a **name**/**value** pair.</span><span class="sxs-lookup"><span data-stu-id="6e587-115">Every tag is made up of a **name**/**value** pair.</span></span> <span data-ttu-id="6e587-116">For example, you might create a tag with the name *costcenter* that has a value of *34543*.</span><span class="sxs-lookup"><span data-stu-id="6e587-116">For example, you might create a tag with the name *costcenter* that has a value of *34543*.</span></span> <span data-ttu-id="6e587-117">A tag such as this might help you later identify lab resources that are billable to this specific area of your organization.</span><span class="sxs-lookup"><span data-stu-id="6e587-117">A tag such as this might help you later identify lab resources that are billable to this specific area of your organization.</span></span> <span data-ttu-id="6e587-118">You get to choose names and values that make sense for how you want to organize your subscription.</span><span class="sxs-lookup"><span data-stu-id="6e587-118">You get to choose names and values that make sense for how you want to organize your subscription.</span></span>

## <a name="steps-to-manage-tags-in-an-existing-lab"></a><span data-ttu-id="6e587-119">Steps to manage tags in an existing lab</span><span class="sxs-lookup"><span data-stu-id="6e587-119">Steps to manage tags in an existing lab</span></span>

1. <span data-ttu-id="6e587-120">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6e587-120">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="6e587-121">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="6e587-121">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span></span> <span data-ttu-id="6e587-122">Your lab might already be shown on the Dashboard under **All Resources**.</span><span class="sxs-lookup"><span data-stu-id="6e587-122">Your lab might already be shown on the Dashboard under **All Resources**.</span></span>
1. <span data-ttu-id="6e587-123">From the list of labs, select the lab in which you want to add or manage tags.</span><span class="sxs-lookup"><span data-stu-id="6e587-123">From the list of labs, select the lab in which you want to add or manage tags.</span></span>  
1. <span data-ttu-id="6e587-124">On the lab's **Overview** area, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="6e587-124">On the lab's **Overview** area, select **Configuration and policies**.</span></span>  

    ![Configuration and policies button](./media/devtest-lab-add-tag/devtestlab-config-and-policies.png)

1. <span data-ttu-id="6e587-126">On the left under **MANAGE**, select **Tags**.</span><span class="sxs-lookup"><span data-stu-id="6e587-126">On the left under **MANAGE**, select **Tags**.</span></span>
1. <span data-ttu-id="6e587-127">To create a new tag for this lab, enter a **Name**/**Value** pair and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6e587-127">To create a new tag for this lab, enter a **Name**/**Value** pair and select **Save**.</span></span> <span data-ttu-id="6e587-128">You can also select an existing tag from the list to view or manage the resources associated with that tag.</span><span class="sxs-lookup"><span data-stu-id="6e587-128">You can also select an existing tag from the list to view or manage the resources associated with that tag.</span></span>

    ![Manage tags](./media/devtest-lab-add-tag/devtestlab-manage-tags.png)

## <a name="understanding-limitations-to-tags"></a><span data-ttu-id="6e587-130">Understanding limitations to tags</span><span class="sxs-lookup"><span data-stu-id="6e587-130">Understanding limitations to tags</span></span>

<span data-ttu-id="6e587-131">The following limitations apply to tags:</span><span class="sxs-lookup"><span data-stu-id="6e587-131">The following limitations apply to tags:</span></span>

* <span data-ttu-id="6e587-132">Each resource or resource group can have a maximum of 15 tag name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="6e587-132">Each resource or resource group can have a maximum of 15 tag name/value pairs.</span></span> <span data-ttu-id="6e587-133">This limitation applies only to tags directly applied to the resource group or resource.</span><span class="sxs-lookup"><span data-stu-id="6e587-133">This limitation applies only to tags directly applied to the resource group or resource.</span></span> <span data-ttu-id="6e587-134">A resource group can contain many resources that each have 15 tag name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="6e587-134">A resource group can contain many resources that each have 15 tag name/value pairs.</span></span> 
* <span data-ttu-id="6e587-135">The tag name is limited to 512 characters, and the tag value is limited to 256 characters.</span><span class="sxs-lookup"><span data-stu-id="6e587-135">The tag name is limited to 512 characters, and the tag value is limited to 256 characters.</span></span> <span data-ttu-id="6e587-136">For storage accounts, the tag name is limited to 128 characters, and the tag value is limited to 256 characters.</span><span class="sxs-lookup"><span data-stu-id="6e587-136">For storage accounts, the tag name is limited to 128 characters, and the tag value is limited to 256 characters.</span></span>
* <span data-ttu-id="6e587-137">Tags applied to the resource group are not inherited by the resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="6e587-137">Tags applied to the resource group are not inherited by the resources in that resource group.</span></span>

<span data-ttu-id="6e587-138">[Use tags to organize your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) provides greater details about using tags in Azure, including how to manage tags using PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6e587-138">[Use tags to organize your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) provides greater details about using tags in Azure, including how to manage tags using PowerShell or Azure CLI.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="6e587-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="6e587-139">Next steps</span></span>
* <span data-ttu-id="6e587-140">You can apply restrictions and conventions across your subscription by using customized policies.</span><span class="sxs-lookup"><span data-stu-id="6e587-140">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="6e587-141">A policy that you define might require that all resources have a value for a particular tag.</span><span class="sxs-lookup"><span data-stu-id="6e587-141">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="6e587-142">For more information, see [Set policies and schedules](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="6e587-142">For more information, see [Set policies and schedules](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="6e587-143">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="6e587-143">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
