---
title: Enabling SSL Policy and end to end SSL on Application Gateway | Microsoft Docs
description: This page provides an overview of the Application Gateway end to end SSL support.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: amsriva
ms.openlocfilehash: d1f4ec6dbe428eef2f3b13637fc389026589cc90
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564364"
---
# <a name="overview-of-end-to-end-ssl-and-ssl-policy-on-application-gateway"></a><span data-ttu-id="0fa58-103">Overview of end to end SSL and SSL Policy on Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0fa58-103">Overview of end to end SSL and SSL Policy on Application Gateway</span></span>

<span data-ttu-id="0fa58-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span><span class="sxs-lookup"><span data-stu-id="0fa58-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span></span> <span data-ttu-id="0fa58-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span><span class="sxs-lookup"><span data-stu-id="0fa58-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="0fa58-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span><span class="sxs-lookup"><span data-stu-id="0fa58-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span></span> <span data-ttu-id="0fa58-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span><span class="sxs-lookup"><span data-stu-id="0fa58-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span></span> <span data-ttu-id="0fa58-108">For such applications, application gateway supports end to end SSL encryption.</span><span class="sxs-lookup"><span data-stu-id="0fa58-108">For such applications, application gateway supports end to end SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="0fa58-109">Overview</span><span class="sxs-lookup"><span data-stu-id="0fa58-109">Overview</span></span>

<span data-ttu-id="0fa58-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span><span class="sxs-lookup"><span data-stu-id="0fa58-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="0fa58-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-\* headers.</span><span class="sxs-lookup"><span data-stu-id="0fa58-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-\* headers.</span></span>

<span data-ttu-id="0fa58-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span><span class="sxs-lookup"><span data-stu-id="0fa58-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span></span> <span data-ttu-id="0fa58-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span><span class="sxs-lookup"><span data-stu-id="0fa58-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span></span> <span data-ttu-id="0fa58-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span><span class="sxs-lookup"><span data-stu-id="0fa58-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span></span> <span data-ttu-id="0fa58-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span><span class="sxs-lookup"><span data-stu-id="0fa58-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span></span> <span data-ttu-id="0fa58-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span><span class="sxs-lookup"><span data-stu-id="0fa58-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span></span>

![end to end ssl scenario][1]

<span data-ttu-id="0fa58-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span><span class="sxs-lookup"><span data-stu-id="0fa58-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span></span>

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="0fa58-119">End to end SSL and whitelisting of certificates</span><span class="sxs-lookup"><span data-stu-id="0fa58-119">End to end SSL and whitelisting of certificates</span></span>

<span data-ttu-id="0fa58-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0fa58-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span></span> <span data-ttu-id="0fa58-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span><span class="sxs-lookup"><span data-stu-id="0fa58-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span></span> <span data-ttu-id="0fa58-122">Only connections to known and whitelisted backends are then allowed.</span><span class="sxs-lookup"><span data-stu-id="0fa58-122">Only connections to known and whitelisted backends are then allowed.</span></span> <span data-ttu-id="0fa58-123">The remaining backends results in a gateway error.</span><span class="sxs-lookup"><span data-stu-id="0fa58-123">The remaining backends results in a gateway error.</span></span> <span data-ttu-id="0fa58-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span><span class="sxs-lookup"><span data-stu-id="0fa58-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="0fa58-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span><span class="sxs-lookup"><span data-stu-id="0fa58-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span></span>

## <a name="application-gateway-ssl-policy"></a><span data-ttu-id="0fa58-126">Application Gateway SSL Policy</span><span class="sxs-lookup"><span data-stu-id="0fa58-126">Application Gateway SSL Policy</span></span>

<span data-ttu-id="0fa58-127">Application gateway supports user configurable SSL negotiation policies, which allow customers more control over SSL connections at the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0fa58-127">Application gateway supports user configurable SSL negotiation policies, which allow customers more control over SSL connections at the application gateway.</span></span>

1. <span data-ttu-id="0fa58-128">SSL 2.0 and 3.0 disabled by default for all Application Gateways.</span><span class="sxs-lookup"><span data-stu-id="0fa58-128">SSL 2.0 and 3.0 disabled by default for all Application Gateways.</span></span> <span data-ttu-id="0fa58-129">These policies are not configurable at all.</span><span class="sxs-lookup"><span data-stu-id="0fa58-129">These policies are not configurable at all.</span></span>
2. <span data-ttu-id="0fa58-130">SSL policy definition gives you option to disable any of the following three protocols - **TLSv1\_0**, **TLSv1\_1**, **TLSv1\_2**.</span><span class="sxs-lookup"><span data-stu-id="0fa58-130">SSL policy definition gives you option to disable any of the following three protocols - **TLSv1\_0**, **TLSv1\_1**, **TLSv1\_2**.</span></span>
3. <span data-ttu-id="0fa58-131">If no SSL policy is defined all three (TLSv1\_0, TLSv1\_1, TLSv1_2) are enabled.</span><span class="sxs-lookup"><span data-stu-id="0fa58-131">If no SSL policy is defined all three (TLSv1\_0, TLSv1\_1, TLSv1_2) are enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fa58-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fa58-132">Next steps</span></span>

<span data-ttu-id="0fa58-133">After learning about end to end SSL and SSL policy, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span><span class="sxs-lookup"><span data-stu-id="0fa58-133">After learning about end to end SSL and SSL policy, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span></span>

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-backend-ssl/scenario.png

