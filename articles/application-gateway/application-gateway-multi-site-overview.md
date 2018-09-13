---
title: Hosting multiple sites on Application Gateway | Microsoft Docs
description: This page provides an overview of the Application Gateway multi-site support.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: amsriva
ms.openlocfilehash: baeb1930ed73f837f19fa4741dcb2bd6291525ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670658"
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="1162c-103">Application Gateway multiple site hosting</span><span class="sxs-lookup"><span data-stu-id="1162c-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="1162c-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span><span class="sxs-lookup"><span data-stu-id="1162c-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="1162c-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span><span class="sxs-lookup"><span data-stu-id="1162c-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="1162c-106">Each website can be directed to its own backend pool.</span><span class="sxs-lookup"><span data-stu-id="1162c-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="1162c-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="1162c-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-multi-site-overview/multisite.png)

<span data-ttu-id="1162c-109">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="1162c-109">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="1162c-110">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span><span class="sxs-lookup"><span data-stu-id="1162c-110">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="1162c-111">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span><span class="sxs-lookup"><span data-stu-id="1162c-111">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="1162c-112">Host headers and Server Name Indication (SNI)</span><span class="sxs-lookup"><span data-stu-id="1162c-112">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="1162c-113">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1162c-113">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="1162c-114">Host multiple web applications each on a unique IP address.</span><span class="sxs-lookup"><span data-stu-id="1162c-114">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="1162c-115">Use host name to host multiple web applications on the same IP address.</span><span class="sxs-lookup"><span data-stu-id="1162c-115">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="1162c-116">Use different ports to host multiple web applications on the same IP address.</span><span class="sxs-lookup"><span data-stu-id="1162c-116">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="1162c-117">Currently an application gateway gets a single public IP address on which it listens for traffic.</span><span class="sxs-lookup"><span data-stu-id="1162c-117">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="1162c-118">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="1162c-118">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="1162c-119">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span><span class="sxs-lookup"><span data-stu-id="1162c-119">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="1162c-120">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span><span class="sxs-lookup"><span data-stu-id="1162c-120">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="1162c-121">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span><span class="sxs-lookup"><span data-stu-id="1162c-121">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="1162c-122">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="1162c-122">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="1162c-123">Listener configuration element</span><span class="sxs-lookup"><span data-stu-id="1162c-123">Listener configuration element</span></span>

<span data-ttu-id="1162c-124">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span><span class="sxs-lookup"><span data-stu-id="1162c-124">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="1162c-125">The following code example is the snippet of HttpListeners element from template file.</span><span class="sxs-lookup"><span data-stu-id="1162c-125">The following code example is the snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="1162c-126">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span><span class="sxs-lookup"><span data-stu-id="1162c-126">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="1162c-127">Routing rule</span><span class="sxs-lookup"><span data-stu-id="1162c-127">Routing rule</span></span>

<span data-ttu-id="1162c-128">There is no change required in the routing rule.</span><span class="sxs-lookup"><span data-stu-id="1162c-128">There is no change required in the routing rule.</span></span> <span data-ttu-id="1162c-129">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span><span class="sxs-lookup"><span data-stu-id="1162c-129">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1162c-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="1162c-130">Next steps</span></span>

<span data-ttu-id="1162c-131">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span><span class="sxs-lookup"><span data-stu-id="1162c-131">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>


