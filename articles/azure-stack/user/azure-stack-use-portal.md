---
title: Using the Azure Stack portal | Microsoft Docs
description: Learn how to access and use the user portal in Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2018
ms.author: mabrigg
ms.reviewer: efemmano
ms.openlocfilehash: 7ca29ee359349f69c3d5ff21bd9db3f93358206a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966972"
---
# <a name="use-the-azure-stack-portal"></a><span data-ttu-id="d2fdb-103">Use the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="d2fdb-103">Use the Azure Stack portal</span></span>

<span data-ttu-id="d2fdb-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="d2fdb-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="d2fdb-105">You can use the Azure Stack portal to subscribe to public offers, and use the services that these offers provide.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-105">You can use the Azure Stack portal to subscribe to public offers, and use the services that these offers provide.</span></span> <span data-ttu-id="d2fdb-106">If you've used the global Azure portal, you're already familiar with how the site works.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-106">If you've used the global Azure portal, you're already familiar with how the site works.</span></span>

## <a name="access-the-portal"></a><span data-ttu-id="d2fdb-107">Access the portal</span><span class="sxs-lookup"><span data-stu-id="d2fdb-107">Access the portal</span></span>

<span data-ttu-id="d2fdb-108">Your Azure Stack operator (either a service provider or an administrator in your organization), will let you know the correct URL to access the portal.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-108">Your Azure Stack operator (either a service provider or an administrator in your organization), will let you know the correct URL to access the portal.</span></span>

- <span data-ttu-id="d2fdb-109">For an integrated system, the URL varies based on your operator's region and external domain name, and will be in the format https://portal.&lt;*region*&gt;.&lt;*FQDN*&gt;.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-109">For an integrated system, the URL varies based on your operator's region and external domain name, and will be in the format https://portal.&lt;*region*&gt;.&lt;*FQDN*&gt;.</span></span>
- <span data-ttu-id="d2fdb-110">If you're using the Azure Stack Development Kit, the portal address is https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-110">If you're using the Azure Stack Development Kit, the portal address is https://portal.local.azurestack.external.</span></span>

![Screen capture of the Azure Stack user portal](media/azure-stack-use-portal/UserPortal.png)

## <a name="customize-the-dashboard"></a><span data-ttu-id="d2fdb-112">Customize the dashboard</span><span class="sxs-lookup"><span data-stu-id="d2fdb-112">Customize the dashboard</span></span>

<span data-ttu-id="d2fdb-113">The dashboard contains a default set of tiles.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-113">The dashboard contains a default set of tiles.</span></span> <span data-ttu-id="d2fdb-114">You can select **Edit dashboard** to modify the default dashboard, or select **New dashboard** to create a custom dashboard.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-114">You can select **Edit dashboard** to modify the default dashboard, or select **New dashboard** to create a custom dashboard.</span></span> <span data-ttu-id="d2fdb-115">You can easily customize a dashboard by adding or removing tiles.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-115">You can easily customize a dashboard by adding or removing tiles.</span></span> <span data-ttu-id="d2fdb-116">For example, to add a Compute tile, select **New**.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-116">For example, to add a Compute tile, select **New**.</span></span> <span data-ttu-id="d2fdb-117">Right-click **Compute**, and then select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-117">Right-click **Compute**, and then select **Pin to dashboard**.</span></span>

## <a name="create-subscription-and-browse-available-resources"></a><span data-ttu-id="d2fdb-118">Create subscription and browse available resources</span><span class="sxs-lookup"><span data-stu-id="d2fdb-118">Create subscription and browse available resources</span></span>

<span data-ttu-id="d2fdb-119">If you don't already have a subscription, the first thing you need to do is subscribe to an offer.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-119">If you don't already have a subscription, the first thing you need to do is subscribe to an offer.</span></span> <span data-ttu-id="d2fdb-120">After that, you can browse the available resources.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-120">After that, you can browse the available resources.</span></span> <span data-ttu-id="d2fdb-121">To browse and create resources, use any of the following approaches:</span><span class="sxs-lookup"><span data-stu-id="d2fdb-121">To browse and create resources, use any of the following approaches:</span></span>

- <span data-ttu-id="d2fdb-122">Select the **Marketplace** tile on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-122">Select the **Marketplace** tile on the dashboard.</span></span>
- <span data-ttu-id="d2fdb-123">On the **All resources** tile, select **Create resources**.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-123">On the **All resources** tile, select **Create resources**.</span></span>
- <span data-ttu-id="d2fdb-124">On the left navigation pane, select **New**.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-124">On the left navigation pane, select **New**.</span></span>

## <a name="learn-how-to-use-available-services"></a><span data-ttu-id="d2fdb-125">Learn how to use available services</span><span class="sxs-lookup"><span data-stu-id="d2fdb-125">Learn how to use available services</span></span>

<span data-ttu-id="d2fdb-126">If you need guidance for how to use available services, there may be different options available to you.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-126">If you need guidance for how to use available services, there may be different options available to you.</span></span>

- <span data-ttu-id="d2fdb-127">Your organization or service provider may provide their own documentation, which is typically the case if they offer customized services or apps.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-127">Your organization or service provider may provide their own documentation, which is typically the case if they offer customized services or apps.</span></span>
- <span data-ttu-id="d2fdb-128">Third-party apps have their own documentation.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-128">Third-party apps have their own documentation.</span></span>
- <span data-ttu-id="d2fdb-129">For Azure-consistent services, we strongly recommend that you first review the Azure Stack documentation.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-129">For Azure-consistent services, we strongly recommend that you first review the Azure Stack documentation.</span></span> <span data-ttu-id="d2fdb-130">To access the Azure Stack user documentation, select the Help icon, and then select **Help + support**.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-130">To access the Azure Stack user documentation, select the Help icon, and then select **Help + support**.</span></span>

    ![Help and support option in the UI](media/azure-stack-use-portal/HelpAndSupport.png)

    <span data-ttu-id="d2fdb-132">In particular, we suggest that you review the following articles to get started:</span><span class="sxs-lookup"><span data-stu-id="d2fdb-132">In particular, we suggest that you review the following articles to get started:</span></span>

    - [<span data-ttu-id="d2fdb-133">Key considerations: Using services or building apps for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d2fdb-133">Key considerations: Using services or building apps for Azure Stack</span></span>](azure-stack-considerations.md)
    - <span data-ttu-id="d2fdb-134">In the **Use services** section of the documentation, there is a considerations article for each service.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-134">In the **Use services** section of the documentation, there is a considerations article for each service.</span></span> <span data-ttu-id="d2fdb-135">The considerations page describes the differences between the service offered in Azure, and the same service offered in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-135">The considerations page describes the differences between the service offered in Azure, and the same service offered in Azure Stack.</span></span> <span data-ttu-id="d2fdb-136">For an example, see [VM considerations](azure-stack-vm-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="d2fdb-136">For an example, see [VM considerations](azure-stack-vm-considerations.md).</span></span> <span data-ttu-id="d2fdb-137">There may be other information in the **Use services** section that's unique to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-137">There may be other information in the **Use services** section that's unique to Azure Stack.</span></span>

      <span data-ttu-id="d2fdb-138">You can use the Azure documentation as general reference for a service, but you must be aware of these differences.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-138">You can use the Azure documentation as general reference for a service, but you must be aware of these differences.</span></span> <span data-ttu-id="d2fdb-139">Understand that the documentation links on the **Quickstart tutorials** tile point to Azure documentation.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-139">Understand that the documentation links on the **Quickstart tutorials** tile point to Azure documentation.</span></span>

## <a name="get-support"></a><span data-ttu-id="d2fdb-140">Get support</span><span class="sxs-lookup"><span data-stu-id="d2fdb-140">Get support</span></span>

<span data-ttu-id="d2fdb-141">If you need support, contact your organization or service provider for help.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-141">If you need support, contact your organization or service provider for help.</span></span>

<span data-ttu-id="d2fdb-142">If you're using the Azure Stack Development Kit, the [Azure Stack forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) is the only source of support.</span><span class="sxs-lookup"><span data-stu-id="d2fdb-142">If you're using the Azure Stack Development Kit, the [Azure Stack forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) is the only source of support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2fdb-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2fdb-143">Next steps</span></span>

[<span data-ttu-id="d2fdb-144">Key considerations: Using services or building apps for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d2fdb-144">Key considerations: Using services or building apps for Azure Stack</span></span>](azure-stack-considerations.md)
