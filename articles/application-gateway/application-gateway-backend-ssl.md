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
# <a name="overview-of-end-to-end-ssl-and-ssl-policy-on-application-gateway"></a>Overview of end to end SSL and SSL Policy on Application Gateway

Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers. This feature allows web servers to be unburdened from costly encryption and decryption overhead. However for some customers unencrypted communication to the backend servers is not an acceptable option. This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection. For such applications, application gateway supports end to end SSL encryption.

## <a name="overview"></a>Overview

End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides. Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-* headers.

When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic. It then applies the configured rules to select an appropriate backend pool instance to route traffic to. Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend. End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool. Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.

![end to end ssl scenario][1]

In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a>End to end SSL and whitelisting of certificates

Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway. To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate). Only connections to known and whitelisted backends are then allowed. The remaining backends results in a gateway error. Self-signed certificates are for test purposes only and not recommended for production workloads. Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.

## <a name="application-gateway-ssl-policy"></a>Application Gateway SSL Policy

Application gateway supports user configurable SSL negotiation policies, which allow customers more control over SSL connections at the application gateway.

1. SSL 2.0 and 3.0 disabled by default for all Application Gateways. These policies are not configurable at all.
2. SSL policy definition gives you option to disable any of the following three protocols - **TLSv1\_0**, **TLSv1\_1**, **TLSv1\_2**.
3. If no SSL policy is defined all three (TLSv1\_0, TLSv1\_1, TLSv1_2) are enabled.

## <a name="next-steps"></a>Next steps

After learning about end to end SSL and SSL policy, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-backend-ssl/scenario.png

