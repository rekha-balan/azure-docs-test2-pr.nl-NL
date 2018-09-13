---
title: Create SharePoint server farms in Azure | Microsoft Docs
description: Quickly create a new SharePoint 2013 or SharePoint 2016 farm in Azure using the Azure portal marketplace.
services: virtual-machines-windows
documentationcenter: ''
author: JoeDavies-MSFT
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0341e8273425147bcd4b0e48b5cca1f1e0a8466e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548728"
---
# <a name="create-sharepoint-server-farms-using-the-azure-portal-marketplace"></a><span data-ttu-id="a6c7c-103">Create SharePoint server farms using the Azure portal marketplace</span><span class="sxs-lookup"><span data-stu-id="a6c7c-103">Create SharePoint server farms using the Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="a6c7c-104">SharePoint 2013 farms</span><span class="sxs-lookup"><span data-stu-id="a6c7c-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="a6c7c-105">With the Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-105">With the Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="a6c7c-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="a6c7c-107">The **SharePoint Server Farm** item in the Azure Marketplace of the Azure portal has been removed.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-107">The **SharePoint Server Farm** item in the Azure Marketplace of the Azure portal has been removed.</span></span> <span data-ttu-id="a6c7c-108">It has been replaced with the **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-108">It has been replaced with the **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="a6c7c-109">The basic SharePoint farm consists of three virtual machines in this configuration.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-109">The basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sharepoint-farm/non-hafarm.png)

<span data-ttu-id="a6c7c-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="a6c7c-112">To create the basic (three-server) SharePoint farm:</span><span class="sxs-lookup"><span data-stu-id="a6c7c-112">To create the basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="a6c7c-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="a6c7c-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="a6c7c-114">Click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="a6c7c-115">On the **SharePoint 2013 non-HA Farm** pane, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-115">On the **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="a6c7c-116">Specify settings on the steps of the **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-116">Specify settings on the steps of the **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="a6c7c-117">The high-availability SharePoint farm consists of nine virtual machines in this configuration.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-117">The high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sharepoint-farm/hafarm.png)

<span data-ttu-id="a6c7c-119">You can use this farm configuration to test higher client loads, high availability of the external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-119">You can use this farm configuration to test higher client loads, high availability of the external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="a6c7c-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="a6c7c-121">To create the high-availability (nine-server) SharePoint farm:</span><span class="sxs-lookup"><span data-stu-id="a6c7c-121">To create the high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="a6c7c-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="a6c7c-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="a6c7c-123">Click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="a6c7c-124">On the **SharePoint 2013 HA Farm** pane, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-124">On the **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="a6c7c-125">Specify settings on the seven steps of the **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-125">Specify settings on the seven steps of the **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="a6c7c-126">You cannot create the **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-126">You cannot create the **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="a6c7c-127">The Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-127">The Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="a6c7c-128">There is no site-to-site VPN or ExpressRoute connection back to your organization network.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-128">There is no site-to-site VPN or ExpressRoute connection back to your organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="a6c7c-129">When you create the basic or high-availability SharePoint farms using the Azure portal, you cannot specify an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-129">When you create the basic or high-availability SharePoint farms using the Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="a6c7c-130">To work around this limitation, create these farms with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-130">To work around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="a6c7c-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="a6c7c-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="a6c7c-132">SharePoint 2016 farms</span><span class="sxs-lookup"><span data-stu-id="a6c7c-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="a6c7c-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for the instructions to build the following single-server SharePoint Server 2016 farm.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for the instructions to build the following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sharepoint-farm/sp2016farm.png)

## <a name="managing-the-sharepoint-farms"></a><span data-ttu-id="a6c7c-135">Managing the SharePoint farms</span><span class="sxs-lookup"><span data-stu-id="a6c7c-135">Managing the SharePoint farms</span></span>
<span data-ttu-id="a6c7c-136">You can administer the servers of these farms through Remote Desktop connections.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-136">You can administer the servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="a6c7c-137">For more information, see [Log on to the virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="a6c7c-137">For more information, see [Log on to the virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="a6c7c-138">From the Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-138">From the Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="a6c7c-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6c7c-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6c7c-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6c7c-140">Next steps</span></span>
* <span data-ttu-id="a6c7c-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span><span class="sxs-lookup"><span data-stu-id="a6c7c-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>



