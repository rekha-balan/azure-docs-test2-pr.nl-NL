---
title: An Application Proxy application takes too long to load | Microsoft Docs
description: Troubleshoot page load performance issues with the Azure AD Application Proxy
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 0c18647fbfc5e328276eef248f4b6aa1dc7f48a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858099"
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a>An Application Proxy application takes too long to load

This article helps you to understand why an Azure AD Application Proxy application may take a long time to load. It also explains what you can do to resolve this issue.

## <a name="overview"></a>Overview
Although your applications are working, they can experience a long latency. There might be network topology tweaks that you can make to improve speed. For an evaluation of different topologies, see the [network considerations document](application-proxy-network-topology.md).

Besides network topology, there are currently no further recommendations for performance tuning. As the Application Proxy service expands it might come to a data center that is physically closer. The closer proximity might help with latency. For a list of Azure data centers, see the [latency test page](http://www.azurespeed.com/Azure/Latency). 

The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Feedback on Application Proxy data center locations 
There may be Azure data centers that don’t yet include Application Proxy, but would lead to a great latency improvement for you. Send the data center location to aadapfeedback@microsoft.com. Microsoft uses your feedback for expansion plans.

Microsoft is working on additional capabilities to improve latency. As soon as these improvements are available, the documentation will be updated.

## <a name="next-steps"></a>Next steps
[Work with existing on-premises proxy servers](application-proxy-configure-connectors-with-proxy-servers.md)
