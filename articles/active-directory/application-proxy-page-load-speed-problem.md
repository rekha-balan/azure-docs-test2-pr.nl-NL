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
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="c610f-103">An Application Proxy application takes too long to load</span><span class="sxs-lookup"><span data-stu-id="c610f-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="c610f-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="c610f-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="c610f-105">Overview</span><span class="sxs-lookup"><span data-stu-id="c610f-105">Overview</span></span>
<span data-ttu-id="c610f-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span><span class="sxs-lookup"><span data-stu-id="c610f-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="c610f-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="c610f-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="c610f-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span><span class="sxs-lookup"><span data-stu-id="c610f-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="c610f-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span><span class="sxs-lookup"><span data-stu-id="c610f-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="c610f-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="c610f-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="c610f-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="c610f-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="c610f-112">Feedback on Application Proxy data center locations</span><span class="sxs-lookup"><span data-stu-id="c610f-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="c610f-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span><span class="sxs-lookup"><span data-stu-id="c610f-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="c610f-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span><span class="sxs-lookup"><span data-stu-id="c610f-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="c610f-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span><span class="sxs-lookup"><span data-stu-id="c610f-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c610f-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="c610f-116">Next steps</span></span>
[<span data-ttu-id="c610f-117">Work with existing on-premises proxy servers</span><span class="sxs-lookup"><span data-stu-id="c610f-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
