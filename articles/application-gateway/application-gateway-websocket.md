---
title: Application Gateway WebSocket support | Microsoft Docs
description: This page provides an overview of the Application Gateway WebSocket support.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/16/2016
ms.author: amsriva
ms.openlocfilehash: 5af1b1bacce2fe189a7b557527520795ed622b54
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44668944"
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="4879b-103">Overview of WebSocket support in Application Gateway</span><span class="sxs-lookup"><span data-stu-id="4879b-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="4879b-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span><span class="sxs-lookup"><span data-stu-id="4879b-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="4879b-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span><span class="sxs-lookup"><span data-stu-id="4879b-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> <span data-ttu-id="4879b-106">You can continue using a standard HTTPListener on port 80/443 to receive WebSocket traffic.</span><span class="sxs-lookup"><span data-stu-id="4879b-106">You can continue using a standard HTTPListener on port 80/443 to receive WebSocket traffic.</span></span> <span data-ttu-id="4879b-107">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span><span class="sxs-lookup"><span data-stu-id="4879b-107">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="4879b-108">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between server and client over a long running TCP connection.</span><span class="sxs-lookup"><span data-stu-id="4879b-108">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between server and client over a long running TCP connection.</span></span> <span data-ttu-id="4879b-109">This feature allows for a more interactive communication between web server and client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span><span class="sxs-lookup"><span data-stu-id="4879b-109">This feature allows for a more interactive communication between web server and client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span>  <span data-ttu-id="4879b-110">WebSocket have low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span><span class="sxs-lookup"><span data-stu-id="4879b-110">WebSocket have low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="4879b-111">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span><span class="sxs-lookup"><span data-stu-id="4879b-111">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="4879b-112">The backend server must respond to application gateway probes, which are described in [health probe overview](application-gateway-probe-overview.md) section.</span><span class="sxs-lookup"><span data-stu-id="4879b-112">The backend server must respond to application gateway probes, which are described in [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="4879b-113">Application gateway health probes are HTTP/HTTPS only, this implies that every backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span><span class="sxs-lookup"><span data-stu-id="4879b-113">Application gateway health probes are HTTP/HTTPS only, this implies that every backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="4879b-114">Listener configuration element</span><span class="sxs-lookup"><span data-stu-id="4879b-114">Listener configuration element</span></span>

<span data-ttu-id="4879b-115">Existing HTTPListener can be used to support WebSocket.</span><span class="sxs-lookup"><span data-stu-id="4879b-115">Existing HTTPListener can be used to support WebSocket.</span></span> <span data-ttu-id="4879b-116">Following is a snippet of HttpListeners element from a sample template file.</span><span class="sxs-lookup"><span data-stu-id="4879b-116">Following is a snippet of HttpListeners element from a sample template file.</span></span> <span data-ttu-id="4879b-117">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span><span class="sxs-lookup"><span data-stu-id="4879b-117">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="4879b-118">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span><span class="sxs-lookup"><span data-stu-id="4879b-118">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
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
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="4879b-119">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span><span class="sxs-lookup"><span data-stu-id="4879b-119">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="4879b-120">BackendAddressPool should be used to define a backend pool with WebSocket enabled servers.</span><span class="sxs-lookup"><span data-stu-id="4879b-120">BackendAddressPool should be used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="4879b-121">BackendHttpSetting should be defined with backend port 80/443 only.</span><span class="sxs-lookup"><span data-stu-id="4879b-121">BackendHttpSetting should be defined with backend port 80/443 only.</span></span> <span data-ttu-id="4879b-122">Properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span><span class="sxs-lookup"><span data-stu-id="4879b-122">Properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="4879b-123">There is no change required in routing rule.</span><span class="sxs-lookup"><span data-stu-id="4879b-123">There is no change required in routing rule.</span></span> <span data-ttu-id="4879b-124">Routing rule 'Basic' should continue to be used to tie the appropriate listener to the corresponding backend address pool.</span><span class="sxs-lookup"><span data-stu-id="4879b-124">Routing rule 'Basic' should continue to be used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a><span data-ttu-id="4879b-125">WebSocket enabled backend</span><span class="sxs-lookup"><span data-stu-id="4879b-125">WebSocket enabled backend</span></span>

<span data-ttu-id="4879b-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span><span class="sxs-lookup"><span data-stu-id="4879b-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="4879b-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with Upgrade to WebSocket protocol as a header field.</span><span class="sxs-lookup"><span data-stu-id="4879b-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with Upgrade to WebSocket protocol as a header field.</span></span>

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

<span data-ttu-id="4879b-128">Another reason for this is that application gateway backend health probe supports HTTP/HTTPS protocols only.</span><span class="sxs-lookup"><span data-stu-id="4879b-128">Another reason for this is that application gateway backend health probe supports HTTP/HTTPS protocols only.</span></span> <span data-ttu-id="4879b-129">If the backend server does not respond to HTTP/HTTPS probes, it would be taken out of backend pool and no requests including WebSocket requests, would reach this backend.</span><span class="sxs-lookup"><span data-stu-id="4879b-129">If the backend server does not respond to HTTP/HTTPS probes, it would be taken out of backend pool and no requests including WebSocket requests, would reach this backend.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4879b-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="4879b-130">Next steps</span></span>

<span data-ttu-id="4879b-131">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span><span class="sxs-lookup"><span data-stu-id="4879b-131">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

