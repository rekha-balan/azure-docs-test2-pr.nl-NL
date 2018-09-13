---
title: Classic portal Azure AD App Proxy connectors | Microsoft Docs
description: Covers how to create and manage groups of connectors in Azure AD Application Proxy.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: harshja
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: kgremban
ms.openlocfilehash: 629ed532da49a6445ae7a969138b48df48cd4096
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564044"
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="9b364-103">Publish applications on separate networks and locations using connector groups</span><span class="sxs-lookup"><span data-stu-id="9b364-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Azure classic portal](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="9b364-106">Connector groups are useful for various scenarios, including:</span><span class="sxs-lookup"><span data-stu-id="9b364-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="9b364-107">Sites with multiple interconnected datacenters.</span><span class="sxs-lookup"><span data-stu-id="9b364-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="9b364-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are usually expensive and slow.</span><span class="sxs-lookup"><span data-stu-id="9b364-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are usually expensive and slow.</span></span> <span data-ttu-id="9b364-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span><span class="sxs-lookup"><span data-stu-id="9b364-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="9b364-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span><span class="sxs-lookup"><span data-stu-id="9b364-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="9b364-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span><span class="sxs-lookup"><span data-stu-id="9b364-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="9b364-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span><span class="sxs-lookup"><span data-stu-id="9b364-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="9b364-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span><span class="sxs-lookup"><span data-stu-id="9b364-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="9b364-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span><span class="sxs-lookup"><span data-stu-id="9b364-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="9b364-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span><span class="sxs-lookup"><span data-stu-id="9b364-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="9b364-116">You can install several connectors to achieve high availability.</span><span class="sxs-lookup"><span data-stu-id="9b364-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="9b364-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span><span class="sxs-lookup"><span data-stu-id="9b364-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="9b364-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span><span class="sxs-lookup"><span data-stu-id="9b364-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="9b364-119">Connector groups can also be used to serve multiple companies from a single tenant.</span><span class="sxs-lookup"><span data-stu-id="9b364-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="9b364-120">Prerequisite: Create your connectors</span><span class="sxs-lookup"><span data-stu-id="9b364-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="9b364-121">In order to group your connectors, you have to make sure you [installed multiple connectors](active-directory-application-proxy-enable.md), and that you name them and then group them.</span><span class="sxs-lookup"><span data-stu-id="9b364-121">In order to group your connectors, you have to make sure you [installed multiple connectors](active-directory-application-proxy-enable.md), and that you name them and then group them.</span></span> <span data-ttu-id="9b364-122">Finally you have to assign them to specific apps.</span><span class="sxs-lookup"><span data-stu-id="9b364-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="9b364-123">Step 1: Create connector groups</span><span class="sxs-lookup"><span data-stu-id="9b364-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="9b364-124">You can create as many connector groups as you want.</span><span class="sxs-lookup"><span data-stu-id="9b364-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="9b364-125">Connector group creation is accomplished in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9b364-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="9b364-126">Select your directory and click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="9b364-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="9b364-127">![Application proxy, configure screenshot - click manage connector groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="9b364-127">![Application proxy, configure screenshot - click manage connector groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="9b364-128">Under Application Proxy, click **Manage Connector Groups** and create a new connector group by giving the group a name.</span><span class="sxs-lookup"><span data-stu-id="9b364-128">Under Application Proxy, click **Manage Connector Groups** and create a new connector group by giving the group a name.</span></span>  
    <span data-ttu-id="9b364-129">![Application proxy connector groups screenshot - name new group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="9b364-129">![Application proxy connector groups screenshot - name new group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="9b364-130">Step 2: Assign connectors to your groups</span><span class="sxs-lookup"><span data-stu-id="9b364-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="9b364-131">Once the connector groups are created, move the connectors to the appropriate group.</span><span class="sxs-lookup"><span data-stu-id="9b364-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="9b364-132">Under **Application Proxy**, click **Manage Connectors**.</span><span class="sxs-lookup"><span data-stu-id="9b364-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="9b364-133">Under **Group**, select the group you want for each connector.</span><span class="sxs-lookup"><span data-stu-id="9b364-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="9b364-134">It might take the connectors up to 10 minutes to become active in the new group.</span><span class="sxs-lookup"><span data-stu-id="9b364-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="9b364-135">![Application proxy connectors screenshot - select group from dropdown menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="9b364-135">![Application proxy connectors screenshot - select group from dropdown menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="9b364-136">Step 3: Assign applications to your connector groups</span><span class="sxs-lookup"><span data-stu-id="9b364-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="9b364-137">The last step is to set each application to the connector group that will serve it.</span><span class="sxs-lookup"><span data-stu-id="9b364-137">The last step is to set each application to the connector group that will serve it.</span></span>

1. <span data-ttu-id="9b364-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="9b364-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="9b364-139">Under **Connector group**, select the group you want the application to use.</span><span class="sxs-lookup"><span data-stu-id="9b364-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="9b364-140">This change is immediately applied.</span><span class="sxs-lookup"><span data-stu-id="9b364-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="9b364-141">![Application proxy connector group screenshot - select group from dropdown menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="9b364-141">![Application proxy connector group screenshot - select group from dropdown menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="9b364-142">See also</span><span class="sxs-lookup"><span data-stu-id="9b364-142">See also</span></span>
* [<span data-ttu-id="9b364-143">Enable Application Proxy</span><span class="sxs-lookup"><span data-stu-id="9b364-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="9b364-144">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="9b364-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="9b364-145">Enable conditional access</span><span class="sxs-lookup"><span data-stu-id="9b364-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="9b364-146">Troubleshoot issues you're having with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="9b364-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="9b364-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="9b364-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>




