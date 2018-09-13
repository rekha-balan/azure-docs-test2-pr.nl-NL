---
title: An Application Proxy application takes too long to load | Microsoft Docs
description: Troubleshoot page load performance issues with the Azure AD Application Proxy
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 8340169fe333d6921cdf39bfc70ea207ff7eadbf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554509"
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a>An Application Proxy application takes too long to load

This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.

## <a name="overview"></a>Overview
If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed. For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning. As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly. To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency). 

The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Feedback on Application Proxy data center locations 
There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you. The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.

We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.

## <a name="next-steps"></a>Next steps
[Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md)
