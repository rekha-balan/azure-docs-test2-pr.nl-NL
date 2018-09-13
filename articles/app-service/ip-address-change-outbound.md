---
title: How to prepare for an outbound IP address change - Azure
description: If your outbound IP address is going to be changed, learn what to do so that your app continues to work after the change.
services: app-service\web
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service-web
ms.workload: web
ms.topic: article
ms.date: 06/28/2018
ms.author: cephalin
ms.openlocfilehash: dfc0a13c1804d8ea74c78a61bfa85e9f5bdd1685
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969319"
---
# <a name="how-to-prepare-for-an-outbound-ip-address-change"></a><span data-ttu-id="e44a7-103">How to prepare for an outbound IP address change</span><span class="sxs-lookup"><span data-stu-id="e44a7-103">How to prepare for an outbound IP address change</span></span>

<span data-ttu-id="e44a7-104">If you received a notification that the outbound IP addresses of your Azure App Service app are changing, follow the instructions in this article.</span><span class="sxs-lookup"><span data-stu-id="e44a7-104">If you received a notification that the outbound IP addresses of your Azure App Service app are changing, follow the instructions in this article.</span></span>

## <a name="determine-if-you-have-to-do-anything"></a><span data-ttu-id="e44a7-105">Determine if you have to do anything</span><span class="sxs-lookup"><span data-stu-id="e44a7-105">Determine if you have to do anything</span></span>

* <span data-ttu-id="e44a7-106">Option 1: If your App Service app does not use IP filtering, an explicit inclusion list, or special handling of outbound traffic such as routing or firewall, no action is required.</span><span class="sxs-lookup"><span data-stu-id="e44a7-106">Option 1: If your App Service app does not use IP filtering, an explicit inclusion list, or special handling of outbound traffic such as routing or firewall, no action is required.</span></span>

* <span data-ttu-id="e44a7-107">Option 2: If your app does have special handling for the outbound IP addresses (see examples below), add the new outbound IP addresses wherever the existing ones appear.</span><span class="sxs-lookup"><span data-stu-id="e44a7-107">Option 2: If your app does have special handling for the outbound IP addresses (see examples below), add the new outbound IP addresses wherever the existing ones appear.</span></span> <span data-ttu-id="e44a7-108">Don’t replace the existing IP addresses.</span><span class="sxs-lookup"><span data-stu-id="e44a7-108">Don’t replace the existing IP addresses.</span></span> <span data-ttu-id="e44a7-109">You can find the new outbound IP addresses by following the instructions in the next section.</span><span class="sxs-lookup"><span data-stu-id="e44a7-109">You can find the new outbound IP addresses by following the instructions in the next section.</span></span>

  <span data-ttu-id="e44a7-110">For example, an outbound IP address may be explicitly included in a firewall outside your app, or an external payment service may have an allowed list that contains the outbound IP address for your app.</span><span class="sxs-lookup"><span data-stu-id="e44a7-110">For example, an outbound IP address may be explicitly included in a firewall outside your app, or an external payment service may have an allowed list that contains the outbound IP address for your app.</span></span> <span data-ttu-id="e44a7-111">If your outbound address is configured in a list anywhere outside your app, that needs to change.</span><span class="sxs-lookup"><span data-stu-id="e44a7-111">If your outbound address is configured in a list anywhere outside your app, that needs to change.</span></span>

## <a name="find-the-outbound-ip-addresses-in-the-azure-portal"></a><span data-ttu-id="e44a7-112">Find the outbound IP addresses in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e44a7-112">Find the outbound IP addresses in the Azure portal</span></span>

<span data-ttu-id="e44a7-113">The new outbound IP addresses are shown in the portal before they take effect.</span><span class="sxs-lookup"><span data-stu-id="e44a7-113">The new outbound IP addresses are shown in the portal before they take effect.</span></span> <span data-ttu-id="e44a7-114">When Azure starts using the new ones, the old ones will no longer be used.</span><span class="sxs-lookup"><span data-stu-id="e44a7-114">When Azure starts using the new ones, the old ones will no longer be used.</span></span> <span data-ttu-id="e44a7-115">Only one set at a time is used, so entries in inclusion lists must have both old and new IP addresses to prevent an outage when the switch happens.</span><span class="sxs-lookup"><span data-stu-id="e44a7-115">Only one set at a time is used, so entries in inclusion lists must have both old and new IP addresses to prevent an outage when the switch happens.</span></span> 

1.  <span data-ttu-id="e44a7-116">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e44a7-116">Open the [Azure portal](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="e44a7-117">In the left-hand navigation menu, select **App Services**.</span><span class="sxs-lookup"><span data-stu-id="e44a7-117">In the left-hand navigation menu, select **App Services**.</span></span>

3.  <span data-ttu-id="e44a7-118">Select your App Service app from the list.</span><span class="sxs-lookup"><span data-stu-id="e44a7-118">Select your App Service app from the list.</span></span>

4.  <span data-ttu-id="e44a7-119">If the app is a function app, see [Function app outbound IP addresses](../azure-functions/ip-addresses.md#find-outbound-ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="e44a7-119">If the app is a function app, see [Function app outbound IP addresses](../azure-functions/ip-addresses.md#find-outbound-ip-addresses).</span></span>

4.  <span data-ttu-id="e44a7-120">Under the **Settings** header, click **Properties** in the left navigation, and find the section labeled **Outbound IP addresses**.</span><span class="sxs-lookup"><span data-stu-id="e44a7-120">Under the **Settings** header, click **Properties** in the left navigation, and find the section labeled **Outbound IP addresses**.</span></span>

5. <span data-ttu-id="e44a7-121">Copy the IP addresses, and add them to your special handling of outbound traffic such as a filter or allowed list.</span><span class="sxs-lookup"><span data-stu-id="e44a7-121">Copy the IP addresses, and add them to your special handling of outbound traffic such as a filter or allowed list.</span></span> <span data-ttu-id="e44a7-122">Don't delete the existing IP addresses in the list.</span><span class="sxs-lookup"><span data-stu-id="e44a7-122">Don't delete the existing IP addresses in the list.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e44a7-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="e44a7-123">Next steps</span></span>

<span data-ttu-id="e44a7-124">This article explained how to prepare for an IP address change that was initiated by Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a7-124">This article explained how to prepare for an IP address change that was initiated by Azure.</span></span> <span data-ttu-id="e44a7-125">For more information about IP addresses in Azure App Service, see [outbound and outbound IP addresses in Azure App Service](app-service-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="e44a7-125">For more information about IP addresses in Azure App Service, see [outbound and outbound IP addresses in Azure App Service](app-service-ip-addresses.md).</span></span>
