---
title: IP addresses in Azure App Service | Microsoft Docs
description: Describes how inbound and outbound IP addresses are used in App Service and how to find information on them for your app.
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2018
ms.author: cephalin
ms.openlocfilehash: 752f9d82afafaf7324c0c63c0d7377b952fe0716
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969055"
---
# <a name="inbound-and-outbound-ip-addresses-in-azure-app-service"></a><span data-ttu-id="bad96-103">Inbound and outbound IP addresses in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bad96-103">Inbound and outbound IP addresses in Azure App Service</span></span>

<span data-ttu-id="bad96-104">[Azure App Service](app-service-web-overview.md) is a multi-tenant service, except for [App Service Environments](environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="bad96-104">[Azure App Service](app-service-web-overview.md) is a multi-tenant service, except for [App Service Environments](environment/intro.md).</span></span> <span data-ttu-id="bad96-105">Apps that are not in an App Service environment (not in the [Isolated tier](https://azure.microsoft.com/pricing/details/app-service/)) share network infrastructure with other apps.</span><span class="sxs-lookup"><span data-stu-id="bad96-105">Apps that are not in an App Service environment (not in the [Isolated tier](https://azure.microsoft.com/pricing/details/app-service/)) share network infrastructure with other apps.</span></span> <span data-ttu-id="bad96-106">As a result, the inbound and outbound IP addresses of an app can be different, and can even change in certain situations.</span><span class="sxs-lookup"><span data-stu-id="bad96-106">As a result, the inbound and outbound IP addresses of an app can be different, and can even change in certain situations.</span></span> 

<span data-ttu-id="bad96-107">[App Service Environments](environment/intro.md) use dedicated network infrastructures, so apps running in an App Service environment get static, dedicated IP addresses both for inbound and outbound connections.</span><span class="sxs-lookup"><span data-stu-id="bad96-107">[App Service Environments](environment/intro.md) use dedicated network infrastructures, so apps running in an App Service environment get static, dedicated IP addresses both for inbound and outbound connections.</span></span>

## <a name="when-inbound-ip-changes"></a><span data-ttu-id="bad96-108">When inbound IP changes</span><span class="sxs-lookup"><span data-stu-id="bad96-108">When inbound IP changes</span></span>

<span data-ttu-id="bad96-109">Regardless of the number of scaled-out instances, each app has a single inbound IP address.</span><span class="sxs-lookup"><span data-stu-id="bad96-109">Regardless of the number of scaled-out instances, each app has a single inbound IP address.</span></span> <span data-ttu-id="bad96-110">The inbound IP address may change when you perform one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="bad96-110">The inbound IP address may change when you perform one of the following actions:</span></span>

- <span data-ttu-id="bad96-111">Delete an app and recreate it in a different resource group.</span><span class="sxs-lookup"><span data-stu-id="bad96-111">Delete an app and recreate it in a different resource group.</span></span>
- <span data-ttu-id="bad96-112">Delete the last app in a resource group _and_ region combination and recreate it.</span><span class="sxs-lookup"><span data-stu-id="bad96-112">Delete the last app in a resource group _and_ region combination and recreate it.</span></span>
- <span data-ttu-id="bad96-113">Delete an existing SSL binding, such as during certificate renewal (see [Renew certificates](app-service-web-tutorial-custom-ssl.md#renew-certificates)).</span><span class="sxs-lookup"><span data-stu-id="bad96-113">Delete an existing SSL binding, such as during certificate renewal (see [Renew certificates](app-service-web-tutorial-custom-ssl.md#renew-certificates)).</span></span>

## <a name="get-static-inbound-ip"></a><span data-ttu-id="bad96-114">Get static inbound IP</span><span class="sxs-lookup"><span data-stu-id="bad96-114">Get static inbound IP</span></span>

<span data-ttu-id="bad96-115">Sometimes you might want a dedicated, static IP address for your app.</span><span class="sxs-lookup"><span data-stu-id="bad96-115">Sometimes you might want a dedicated, static IP address for your app.</span></span> <span data-ttu-id="bad96-116">To get a static inbound IP address, you need to configure an [IP-based SSL binding](app-service-web-tutorial-custom-ssl.md#bind-your-ssl-certificate).</span><span class="sxs-lookup"><span data-stu-id="bad96-116">To get a static inbound IP address, you need to configure an [IP-based SSL binding](app-service-web-tutorial-custom-ssl.md#bind-your-ssl-certificate).</span></span> <span data-ttu-id="bad96-117">If you don't actually need SSL functionality to secure your app, you can even upload a self-signed certificate for this binding.</span><span class="sxs-lookup"><span data-stu-id="bad96-117">If you don't actually need SSL functionality to secure your app, you can even upload a self-signed certificate for this binding.</span></span> <span data-ttu-id="bad96-118">In an IP-based SSL binding, the certificate is bound to the IP address itself, so App Service provisions a static IP address to make it happen.</span><span class="sxs-lookup"><span data-stu-id="bad96-118">In an IP-based SSL binding, the certificate is bound to the IP address itself, so App Service provisions a static IP address to make it happen.</span></span> 

## <a name="when-outbound-ips-change"></a><span data-ttu-id="bad96-119">When outbound IPs change</span><span class="sxs-lookup"><span data-stu-id="bad96-119">When outbound IPs change</span></span>

<span data-ttu-id="bad96-120">Regardless of the number of scaled-out instances, each app has a set number of outbound IP addresses at any given time.</span><span class="sxs-lookup"><span data-stu-id="bad96-120">Regardless of the number of scaled-out instances, each app has a set number of outbound IP addresses at any given time.</span></span> <span data-ttu-id="bad96-121">Any outbound connection from the App Service app, such as to a back-end database, uses one of the outbound IP addresses as the origin IP address.</span><span class="sxs-lookup"><span data-stu-id="bad96-121">Any outbound connection from the App Service app, such as to a back-end database, uses one of the outbound IP addresses as the origin IP address.</span></span> <span data-ttu-id="bad96-122">You can't know beforehand which IP address a given app instance will use to make the outbound connection, so your back-end service must open its firewall to all the outbound IP addresses of your app.</span><span class="sxs-lookup"><span data-stu-id="bad96-122">You can't know beforehand which IP address a given app instance will use to make the outbound connection, so your back-end service must open its firewall to all the outbound IP addresses of your app.</span></span>

<span data-ttu-id="bad96-123">The set of outbound IP addresses for your app changes when you scale your app between the lower tiers (**Basic**, **Standard**, and **Premium**) and the **Premium V2** tier.</span><span class="sxs-lookup"><span data-stu-id="bad96-123">The set of outbound IP addresses for your app changes when you scale your app between the lower tiers (**Basic**, **Standard**, and **Premium**) and the **Premium V2** tier.</span></span>

<span data-ttu-id="bad96-124">You can find the set of all possible outbound IP addresses your app can use, regardless of pricing tiers, by looking for the `possibleOutboundIPAddresses` property.</span><span class="sxs-lookup"><span data-stu-id="bad96-124">You can find the set of all possible outbound IP addresses your app can use, regardless of pricing tiers, by looking for the `possibleOutboundIPAddresses` property.</span></span> <span data-ttu-id="bad96-125">See [Find outbound IPs](#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="bad96-125">See [Find outbound IPs](#find-outbound-ips).</span></span>

## <a name="find-outbound-ips"></a><span data-ttu-id="bad96-126">Find outbound IPs</span><span class="sxs-lookup"><span data-stu-id="bad96-126">Find outbound IPs</span></span>

<span data-ttu-id="bad96-127">To find the outbound IP addresses currently used by your app in the Azure portal, click **Properties** in your app's left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="bad96-127">To find the outbound IP addresses currently used by your app in the Azure portal, click **Properties** in your app's left-hand navigation.</span></span> 

<span data-ttu-id="bad96-128">You can find the same information by running the following command in the [Cloud Shell](../cloud-shell/quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="bad96-128">You can find the same information by running the following command in the [Cloud Shell](../cloud-shell/quickstart.md).</span></span>

```azurecli-interactive
az webapp show --resource-group <group_name> --name <app_name> --query outboundIpAddresses --output tsv
```

<span data-ttu-id="bad96-129">To find all possible outbound IP addresses for your app, regardless of pricing tiers, run the following command in the [Cloud Shell](../cloud-shell/quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="bad96-129">To find all possible outbound IP addresses for your app, regardless of pricing tiers, run the following command in the [Cloud Shell](../cloud-shell/quickstart.md).</span></span>

```azurecli-interactive
az webapp show --resource-group <group_name> --name <app_name> --query possibleOutboundIpAddresses --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="bad96-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="bad96-130">Next steps</span></span>

<span data-ttu-id="bad96-131">Learn how to restrict inbound traffic by source IP addresses.</span><span class="sxs-lookup"><span data-stu-id="bad96-131">Learn how to restrict inbound traffic by source IP addresses.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bad96-132">Static IP restrictions</span><span class="sxs-lookup"><span data-stu-id="bad96-132">Static IP restrictions</span></span>](app-service-ip-restrictions.md)
