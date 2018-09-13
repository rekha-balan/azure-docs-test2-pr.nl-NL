---
title: Hosting multiple sites on Azure Application Gateway | Microsoft Docs
description: This page provides an overview of the Application Gateway multi-site support.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: ''
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: df98559a9476190d683812bf9f63d8ad9c4d3f0e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856824"
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="65ea2-103">Application Gateway multiple site hosting</span><span class="sxs-lookup"><span data-stu-id="65ea2-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="65ea2-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span><span class="sxs-lookup"><span data-stu-id="65ea2-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="65ea2-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span><span class="sxs-lookup"><span data-stu-id="65ea2-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="65ea2-106">Each website can be directed to its own backend pool.</span><span class="sxs-lookup"><span data-stu-id="65ea2-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="65ea2-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="65ea2-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/multiple-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="65ea2-109">Rules are processed in the order they are listed in the portal.</span><span class="sxs-lookup"><span data-stu-id="65ea2-109">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="65ea2-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span><span class="sxs-lookup"><span data-stu-id="65ea2-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="65ea2-111">This will ensure that traffic gets routed to the right back end.</span><span class="sxs-lookup"><span data-stu-id="65ea2-111">This will ensure that traffic gets routed to the right back end.</span></span> <span data-ttu-id="65ea2-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span><span class="sxs-lookup"><span data-stu-id="65ea2-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="65ea2-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="65ea2-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="65ea2-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span><span class="sxs-lookup"><span data-stu-id="65ea2-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="65ea2-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span><span class="sxs-lookup"><span data-stu-id="65ea2-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="65ea2-116">Host headers and Server Name Indication (SNI)</span><span class="sxs-lookup"><span data-stu-id="65ea2-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="65ea2-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span><span class="sxs-lookup"><span data-stu-id="65ea2-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="65ea2-118">Host multiple web applications each on a unique IP address.</span><span class="sxs-lookup"><span data-stu-id="65ea2-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="65ea2-119">Use host name to host multiple web applications on the same IP address.</span><span class="sxs-lookup"><span data-stu-id="65ea2-119">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="65ea2-120">Use different ports to host multiple web applications on the same IP address.</span><span class="sxs-lookup"><span data-stu-id="65ea2-120">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="65ea2-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span><span class="sxs-lookup"><span data-stu-id="65ea2-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="65ea2-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="65ea2-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="65ea2-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span><span class="sxs-lookup"><span data-stu-id="65ea2-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="65ea2-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span><span class="sxs-lookup"><span data-stu-id="65ea2-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="65ea2-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span><span class="sxs-lookup"><span data-stu-id="65ea2-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="65ea2-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="65ea2-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="65ea2-127">Listener configuration element</span><span class="sxs-lookup"><span data-stu-id="65ea2-127">Listener configuration element</span></span>

<span data-ttu-id="65ea2-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span><span class="sxs-lookup"><span data-stu-id="65ea2-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="65ea2-129">The following code example is the snippet of HttpListeners element from template file.</span><span class="sxs-lookup"><span data-stu-id="65ea2-129">The following code example is the snippet of HttpListeners element from template file.</span></span>

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

<span data-ttu-id="65ea2-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span><span class="sxs-lookup"><span data-stu-id="65ea2-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="65ea2-131">Routing rule</span><span class="sxs-lookup"><span data-stu-id="65ea2-131">Routing rule</span></span>

<span data-ttu-id="65ea2-132">There is no change required in the routing rule.</span><span class="sxs-lookup"><span data-stu-id="65ea2-132">There is no change required in the routing rule.</span></span> <span data-ttu-id="65ea2-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span><span class="sxs-lookup"><span data-stu-id="65ea2-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a><span data-ttu-id="65ea2-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="65ea2-134">Next steps</span></span>

<span data-ttu-id="65ea2-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](tutorial-multiple-sites-powershell.md) to create an application gateway with ability to support more than one web application.</span><span class="sxs-lookup"><span data-stu-id="65ea2-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](tutorial-multiple-sites-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>

