---
title: Manage Azure Traffic Manager profiles | Microsoft Docs
description: This article helps you create, disable, enable, and delete a Azure Traffic Manager profile.
services: traffic-manager
documentationcenter: ''
author: kumudd
manager: timlt
editor: ''
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: b17764dd8454a062dd9534bfa9f1e667846b3fcd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44820994"
---
# <a name="manage-an-azure-traffic-manager-profile"></a><span data-ttu-id="38315-103">Manage an Azure Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="38315-103">Manage an Azure Traffic Manager profile</span></span>

<span data-ttu-id="38315-104">Traffic Manager profiles use traffic-routing methods to control the distribution of traffic to your cloud services or website endpoints.</span><span class="sxs-lookup"><span data-stu-id="38315-104">Traffic Manager profiles use traffic-routing methods to control the distribution of traffic to your cloud services or website endpoints.</span></span> <span data-ttu-id="38315-105">This article explains how to create and manage these profiles.</span><span class="sxs-lookup"><span data-stu-id="38315-105">This article explains how to create and manage these profiles.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="38315-106">Create a Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="38315-106">Create a Traffic Manager profile</span></span>

<span data-ttu-id="38315-107">You can create a Traffic Manager profile by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="38315-107">You can create a Traffic Manager profile by using the Azure portal.</span></span> <span data-ttu-id="38315-108">After creating your profile, you can configure endpoints, monitoring, and other settings in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="38315-108">After creating your profile, you can configure endpoints, monitoring, and other settings in the Azure portal.</span></span> <span data-ttu-id="38315-109">Traffic Manager supports up to 200 endpoints per profile.</span><span class="sxs-lookup"><span data-stu-id="38315-109">Traffic Manager supports up to 200 endpoints per profile.</span></span> <span data-ttu-id="38315-110">However, most usage scenarios require only a few of endpoints.</span><span class="sxs-lookup"><span data-stu-id="38315-110">However, most usage scenarios require only a few of endpoints.</span></span>

### <a name="to-create-a-traffic-manager-profile"></a><span data-ttu-id="38315-111">To create a Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="38315-111">To create a Traffic Manager profile</span></span>

1. <span data-ttu-id="38315-112">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38315-112">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="38315-113">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="38315-113">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="38315-114">Click **Create a resource** > **Networking** > **Traffic Manager profile** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="38315-114">Click **Create a resource** > **Networking** > **Traffic Manager profile** > **Create**.</span></span>
4. <span data-ttu-id="38315-115">In the **Create Traffic Manager profile**, complete as follows:</span><span class="sxs-lookup"><span data-stu-id="38315-115">In the **Create Traffic Manager profile**, complete as follows:</span></span>
    1. <span data-ttu-id="38315-116">In **Name**, provide a name for your profile.</span><span class="sxs-lookup"><span data-stu-id="38315-116">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="38315-117">This name needs to be unique within the trafficmanager.net zone and results in the DNS name <name>, trafficmanager.net, that is used to access your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="38315-117">This name needs to be unique within the trafficmanager.net zone and results in the DNS name <name>, trafficmanager.net, that is used to access your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="38315-118">In **Routing method**, select the **Priority** routing method.</span><span class="sxs-lookup"><span data-stu-id="38315-118">In **Routing method**, select the **Priority** routing method.</span></span>
    3. <span data-ttu-id="38315-119">In **Subscription**, select the subscription you want to create this profile under</span><span class="sxs-lookup"><span data-stu-id="38315-119">In **Subscription**, select the subscription you want to create this profile under</span></span>
    4. <span data-ttu-id="38315-120">In **Resource Group**, create a new resource group to place this profile under.</span><span class="sxs-lookup"><span data-stu-id="38315-120">In **Resource Group**, create a new resource group to place this profile under.</span></span>
    5. <span data-ttu-id="38315-121">In **Resource group location**, select the location of the resource group.</span><span class="sxs-lookup"><span data-stu-id="38315-121">In **Resource group location**, select the location of the resource group.</span></span> <span data-ttu-id="38315-122">This setting refers to the location of the resource group, and has no impact on the Traffic Manager profile that will be deployed globally.</span><span class="sxs-lookup"><span data-stu-id="38315-122">This setting refers to the location of the resource group, and has no impact on the Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="38315-123">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="38315-123">Click **Create**.</span></span>
    7. <span data-ttu-id="38315-124">When the global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of the resources.</span><span class="sxs-lookup"><span data-stu-id="38315-124">When the global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of the resources.</span></span>

## <a name="disable-enable-or-delete-a-profile"></a><span data-ttu-id="38315-125">Disable, enable, or delete a profile</span><span class="sxs-lookup"><span data-stu-id="38315-125">Disable, enable, or delete a profile</span></span>

<span data-ttu-id="38315-126">You can disable an existing profile so that Traffic Manager does not refer user requests to the configured endpoints.</span><span class="sxs-lookup"><span data-stu-id="38315-126">You can disable an existing profile so that Traffic Manager does not refer user requests to the configured endpoints.</span></span> <span data-ttu-id="38315-127">When you disable a Traffic Manager profile, the profile and the information contained in the profile remain intact and can be edited in the Traffic Manager interface.</span><span class="sxs-lookup"><span data-stu-id="38315-127">When you disable a Traffic Manager profile, the profile and the information contained in the profile remain intact and can be edited in the Traffic Manager interface.</span></span>  <span data-ttu-id="38315-128">Referrals resume when you re-enable the profile.</span><span class="sxs-lookup"><span data-stu-id="38315-128">Referrals resume when you re-enable the profile.</span></span> <span data-ttu-id="38315-129">When you create a Traffic Manager profile in the Azure portal, it's automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="38315-129">When you create a Traffic Manager profile in the Azure portal, it's automatically enabled.</span></span> <span data-ttu-id="38315-130">If you decide a profile is no longer necessary, you can delete it.</span><span class="sxs-lookup"><span data-stu-id="38315-130">If you decide a profile is no longer necessary, you can delete it.</span></span>

### <a name="to-disable-a-profile"></a><span data-ttu-id="38315-131">To disable a profile</span><span class="sxs-lookup"><span data-stu-id="38315-131">To disable a profile</span></span>

1. <span data-ttu-id="38315-132">If you are using a custom domain name, change the CNAME record on your Internet DNS server so that it no longer points to your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="38315-132">If you are using a custom domain name, change the CNAME record on your Internet DNS server so that it no longer points to your Traffic Manager profile.</span></span>
2. <span data-ttu-id="38315-133">Traffic stops being directed to the endpoints through the Traffic Manager profile settings.</span><span class="sxs-lookup"><span data-stu-id="38315-133">Traffic stops being directed to the endpoints through the Traffic Manager profile settings.</span></span>
3. <span data-ttu-id="38315-134">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38315-134">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="38315-135">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span><span class="sxs-lookup"><span data-stu-id="38315-135">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="38315-136">Click **Overview** > **Disable**.</span><span class="sxs-lookup"><span data-stu-id="38315-136">Click **Overview** > **Disable**.</span></span>
4. <span data-ttu-id="38315-137">Confirm to disable the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="38315-137">Confirm to disable the Traffic Manager profile.</span></span>

### <a name="to-enable-a-profile"></a><span data-ttu-id="38315-138">To enable a profile</span><span class="sxs-lookup"><span data-stu-id="38315-138">To enable a profile</span></span>

1. <span data-ttu-id="38315-139">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38315-139">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="38315-140">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span><span class="sxs-lookup"><span data-stu-id="38315-140">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="38315-141">Click **Overview** > **Enable**.</span><span class="sxs-lookup"><span data-stu-id="38315-141">Click **Overview** > **Enable**.</span></span>
1. <span data-ttu-id="38315-142">If you are using a custom domain name, create a CNAME resource record on your Internet DNS server to point to the domain name of your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="38315-142">If you are using a custom domain name, create a CNAME resource record on your Internet DNS server to point to the domain name of your Traffic Manager profile.</span></span>
2. <span data-ttu-id="38315-143">Traffic is directed to the endpoints again.</span><span class="sxs-lookup"><span data-stu-id="38315-143">Traffic is directed to the endpoints again.</span></span>

### <a name="to-delete-a-profile"></a><span data-ttu-id="38315-144">To delete a profile</span><span class="sxs-lookup"><span data-stu-id="38315-144">To delete a profile</span></span>

1. <span data-ttu-id="38315-145">Ensure that the DNS resource record on your Internet DNS server no longer uses a CNAME resource record that points to the domain name of your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="38315-145">Ensure that the DNS resource record on your Internet DNS server no longer uses a CNAME resource record that points to the domain name of your Traffic Manager profile.</span></span>
2. <span data-ttu-id="38315-146">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span><span class="sxs-lookup"><span data-stu-id="38315-146">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="38315-147">Click **Overview** > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="38315-147">Click **Overview** > **Delete**.</span></span>
4. <span data-ttu-id="38315-148">Confirm to delete the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="38315-148">Confirm to delete the Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38315-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="38315-149">Next steps</span></span>

* [<span data-ttu-id="38315-150">Add an endpoint</span><span class="sxs-lookup"><span data-stu-id="38315-150">Add an endpoint</span></span>](traffic-manager-endpoints.md)
* [<span data-ttu-id="38315-151">Configure Priority routing method</span><span class="sxs-lookup"><span data-stu-id="38315-151">Configure Priority routing method</span></span>](traffic-manager-configure-priority-routing-method.md)
* [<span data-ttu-id="38315-152">Configure Geographic routing method</span><span class="sxs-lookup"><span data-stu-id="38315-152">Configure Geographic routing method</span></span>](traffic-manager-configure-geographic-routing-method.md) 
* [<span data-ttu-id="38315-153">Configure Weighted routing method</span><span class="sxs-lookup"><span data-stu-id="38315-153">Configure Weighted routing method</span></span>](traffic-manager-configure-weighted-routing-method.md)
* [<span data-ttu-id="38315-154">Configure Performance routing method</span><span class="sxs-lookup"><span data-stu-id="38315-154">Configure Performance routing method</span></span>](traffic-manager-configure-performance-routing-method.md)
