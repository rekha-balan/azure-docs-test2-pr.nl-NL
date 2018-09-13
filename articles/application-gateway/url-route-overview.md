---
title: Azure Application Gateway URL-based content routing overview
description: This article provides an overview of the Application Gateway URL-based content routing, UrlPathMap configuration and PathBasedRouting rule.
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 4/23/2018
ms.author: victorh
ms.openlocfilehash: cf3e051e4833c6b654e5ff89cd084911521b3d67
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968217"
---
# <a name="azure-application-gateway-url-path-based-routing-overview"></a><span data-ttu-id="30838-103">Azure Application Gateway URL path based routing overview</span><span class="sxs-lookup"><span data-stu-id="30838-103">Azure Application Gateway URL path based routing overview</span></span>

<span data-ttu-id="30838-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span><span class="sxs-lookup"><span data-stu-id="30838-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="30838-105">One of the scenarios is to route requests for different content types to different backend server pools.</span><span class="sxs-lookup"><span data-stu-id="30838-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="30838-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="30838-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/url-route-overview/figure1.png)

<span data-ttu-id="30838-108">Requests for http://contoso.com/video/\* are routed to VideoServerPool, and http://contoso.com/images/\* are routed to ImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="30838-108">Requests for http://contoso.com/video/\* are routed to VideoServerPool, and http://contoso.com/images/\* are routed to ImageServerPool.</span></span> <span data-ttu-id="30838-109">DefaultServerPool is selected if none of the path patterns match.</span><span class="sxs-lookup"><span data-stu-id="30838-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30838-110">Rules are processed in the order they are listed in the portal.</span><span class="sxs-lookup"><span data-stu-id="30838-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="30838-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span><span class="sxs-lookup"><span data-stu-id="30838-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="30838-112">This ensures that traffic gets routed to the right back end.</span><span class="sxs-lookup"><span data-stu-id="30838-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="30838-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span><span class="sxs-lookup"><span data-stu-id="30838-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="30838-114">UrlPathMap configuration element</span><span class="sxs-lookup"><span data-stu-id="30838-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="30838-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span><span class="sxs-lookup"><span data-stu-id="30838-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="30838-116">The following code example is the snippet of urlPathMap element from template file.</span><span class="sxs-lookup"><span data-stu-id="30838-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> <span data-ttu-id="30838-117">PathPattern: This setting is a list of path patterns to match.</span><span class="sxs-lookup"><span data-stu-id="30838-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="30838-118">Each must start with / and the only place a "\*" is allowed is at the end following a "/."</span><span class="sxs-lookup"><span data-stu-id="30838-118">Each must start with / and the only place a "\*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="30838-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span><span class="sxs-lookup"><span data-stu-id="30838-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="30838-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span><span class="sxs-lookup"><span data-stu-id="30838-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="30838-121">PathBasedRouting rule</span><span class="sxs-lookup"><span data-stu-id="30838-121">PathBasedRouting rule</span></span>

<span data-ttu-id="30838-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="30838-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="30838-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="30838-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="30838-124">Snippet of PathBasedRouting rule:</span><span class="sxs-lookup"><span data-stu-id="30838-124">Snippet of PathBasedRouting rule:</span></span>

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="30838-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="30838-125">Next steps</span></span>

<span data-ttu-id="30838-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](tutorial-url-route-powershell.md) to create an application gateway with URL routing rules.</span><span class="sxs-lookup"><span data-stu-id="30838-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](tutorial-url-route-powershell.md) to create an application gateway with URL routing rules.</span></span>
