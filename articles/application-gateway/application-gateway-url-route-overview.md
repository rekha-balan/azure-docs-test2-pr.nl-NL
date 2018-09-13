---
title: URL-based content routing overview | Microsoft Docs
description: This page provides an overview of the Application Gateway URL-based content routing, UrlPathMap configuration and PathBasedRouting rule .
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/16/2016
ms.author: gwallace
ms.openlocfilehash: 4324b15286317ff109b6c6bab2794f7c67a002c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662202"
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="2fa82-103">URL Path Based Routing overview</span><span class="sxs-lookup"><span data-stu-id="2fa82-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="2fa82-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span><span class="sxs-lookup"><span data-stu-id="2fa82-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> <span data-ttu-id="2fa82-105">One of the scenarios is to route requests for different content types to different backend server pools.</span><span class="sxs-lookup"><span data-stu-id="2fa82-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>
<span data-ttu-id="2fa82-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="2fa82-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="2fa82-108">Requests for http://contoso.com/video\* are routed to VideoServerPool, and http://contoso.com/images\* are routed to ImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="2fa82-108">Requests for http://contoso.com/video\* are routed to VideoServerPool, and http://contoso.com/images\* are routed to ImageServerPool.</span></span> <span data-ttu-id="2fa82-109">DefaultServerPool is selected if none of the path patterns match.</span><span class="sxs-lookup"><span data-stu-id="2fa82-109">DefaultServerPool is selected if none of the path patterns match.</span></span>
    
## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="2fa82-110">UrlPathMap configuration element</span><span class="sxs-lookup"><span data-stu-id="2fa82-110">UrlPathMap configuration element</span></span>

<span data-ttu-id="2fa82-111">UrlPathMap element is used to specify Path patterns to back-end server pool mappings.</span><span class="sxs-lookup"><span data-stu-id="2fa82-111">UrlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="2fa82-112">The following code example is the snippet of urlPathMap element from template file.</span><span class="sxs-lookup"><span data-stu-id="2fa82-112">The following code example is the snippet of urlPathMap element from template file.</span></span>

```json
"urlPathMaps": [{
    "name": "<urlPathMapName>",
    "id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/urlPathMaps/<urlPathMapName>",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/backendAddressPools/<poolName>"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/backendHttpSettingsList/<settingsName>"
        },
        "pathRules": [{
            "name": "<pathRuleName>",
            "properties": {
                "paths": [
                    "<pathPattern>"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/backendAddressPools/<poolName2>"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/backendHttpsettingsList/<settingsName2>"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> <span data-ttu-id="2fa82-113">PathPattern: This setting is a list of path patterns to match.</span><span class="sxs-lookup"><span data-stu-id="2fa82-113">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="2fa82-114">Each must start with / and the only place a "\*" is allowed is at the end following a "/".</span><span class="sxs-lookup"><span data-stu-id="2fa82-114">Each must start with / and the only place a "\*" is allowed is at the end following a "/".</span></span> <span data-ttu-id="2fa82-115">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span><span class="sxs-lookup"><span data-stu-id="2fa82-115">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="2fa82-116">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span><span class="sxs-lookup"><span data-stu-id="2fa82-116">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="2fa82-117">PathBasedRouting rule</span><span class="sxs-lookup"><span data-stu-id="2fa82-117">PathBasedRouting rule</span></span>

<span data-ttu-id="2fa82-118">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="2fa82-118">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="2fa82-119">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="2fa82-119">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="2fa82-120">Snippet of PathBasedRouting rule:</span><span class="sxs-lookup"><span data-stu-id="2fa82-120">Snippet of PathBasedRouting rule:</span></span>

```json
"requestRoutingRules": [
    {

"name": "<ruleName>",
"id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/requestRoutingRules/<ruleName>",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/<subscriptionId>/../microsoft.network/applicationGateways/<gatewayName>/ urlPathMaps/<urlPathMapName>"
    },

}
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="2fa82-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="2fa82-121">Next steps</span></span>

<span data-ttu-id="2fa82-122">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span><span class="sxs-lookup"><span data-stu-id="2fa82-122">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>


