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
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="0aaee-103">An Application Proxy application takes too long to load</span><span class="sxs-lookup"><span data-stu-id="0aaee-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="0aaee-104">This article helps you to understand why an Azure AD Application Proxy application may take a long time to load.</span><span class="sxs-lookup"><span data-stu-id="0aaee-104">This article helps you to understand why an Azure AD Application Proxy application may take a long time to load.</span></span> <span data-ttu-id="0aaee-105">It also explains what you can do to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="0aaee-105">It also explains what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="0aaee-106">Overview</span><span class="sxs-lookup"><span data-stu-id="0aaee-106">Overview</span></span>
<span data-ttu-id="0aaee-107">Although your applications are working, they can experience a long latency.</span><span class="sxs-lookup"><span data-stu-id="0aaee-107">Although your applications are working, they can experience a long latency.</span></span> <span data-ttu-id="0aaee-108">There might be network topology tweaks that you can make to improve speed.</span><span class="sxs-lookup"><span data-stu-id="0aaee-108">There might be network topology tweaks that you can make to improve speed.</span></span> <span data-ttu-id="0aaee-109">For an evaluation of different topologies, see the [network considerations document](application-proxy-network-topology.md).</span><span class="sxs-lookup"><span data-stu-id="0aaee-109">For an evaluation of different topologies, see the [network considerations document](application-proxy-network-topology.md).</span></span>

<span data-ttu-id="0aaee-110">Besides network topology, there are currently no further recommendations for performance tuning.</span><span class="sxs-lookup"><span data-stu-id="0aaee-110">Besides network topology, there are currently no further recommendations for performance tuning.</span></span> <span data-ttu-id="0aaee-111">As the Application Proxy service expands it might come to a data center that is physically closer.</span><span class="sxs-lookup"><span data-stu-id="0aaee-111">As the Application Proxy service expands it might come to a data center that is physically closer.</span></span> <span data-ttu-id="0aaee-112">The closer proximity might help with latency.</span><span class="sxs-lookup"><span data-stu-id="0aaee-112">The closer proximity might help with latency.</span></span> <span data-ttu-id="0aaee-113">For a list of Azure data centers, see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="0aaee-113">For a list of Azure data centers, see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="0aaee-114">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="0aaee-114">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="0aaee-115">Feedback on Application Proxy data center locations</span><span class="sxs-lookup"><span data-stu-id="0aaee-115">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="0aaee-116">There may be Azure data centers that don’t yet include Application Proxy, but would lead to a great latency improvement for you.</span><span class="sxs-lookup"><span data-stu-id="0aaee-116">There may be Azure data centers that don’t yet include Application Proxy, but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="0aaee-117">Send the data center location to aadapfeedback@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="0aaee-117">Send the data center location to aadapfeedback@microsoft.com.</span></span> <span data-ttu-id="0aaee-118">Microsoft uses your feedback for expansion plans.</span><span class="sxs-lookup"><span data-stu-id="0aaee-118">Microsoft uses your feedback for expansion plans.</span></span>

<span data-ttu-id="0aaee-119">Microsoft is working on additional capabilities to improve latency.</span><span class="sxs-lookup"><span data-stu-id="0aaee-119">Microsoft is working on additional capabilities to improve latency.</span></span> <span data-ttu-id="0aaee-120">As soon as these improvements are available, the documentation will be updated.</span><span class="sxs-lookup"><span data-stu-id="0aaee-120">As soon as these improvements are available, the documentation will be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aaee-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="0aaee-121">Next steps</span></span>
[<span data-ttu-id="0aaee-122">Work with existing on-premises proxy servers</span><span class="sxs-lookup"><span data-stu-id="0aaee-122">Work with existing on-premises proxy servers</span></span>](application-proxy-configure-connectors-with-proxy-servers.md)
