---
title: How to open the firewall ports required for an Application Proxy application | Microsoft Docs
description: Find out what ports to open for the Azure AD Application Proxy to work correctly
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
ms.openlocfilehash: 5cbb9cc09e577b257d1f9b0cf8317ccf1468d681
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669319"
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="ae2de-103">How to open the firewall ports required for an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="ae2de-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="ae2de-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="ae2de-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="ae2de-105">note that Application Proxy only uses outbound ports.</span><span class="sxs-lookup"><span data-stu-id="ae2de-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="ae2de-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span><span class="sxs-lookup"><span data-stu-id="ae2de-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="ae2de-107">More green checkmarks means greater resiliency.</span><span class="sxs-lookup"><span data-stu-id="ae2de-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="ae2de-108">App Proxy regions</span><span class="sxs-lookup"><span data-stu-id="ae2de-108">App Proxy regions</span></span>

<span data-ttu-id="ae2de-109">We are working on a way to let you know which of these regions needs to be green for you.</span><span class="sxs-lookup"><span data-stu-id="ae2de-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="ae2de-110">For now, make sure they all are.</span><span class="sxs-lookup"><span data-stu-id="ae2de-110">For now, make sure they all are.</span></span> <span data-ttu-id="ae2de-111">Central US is also required regardless of which region you are in.</span><span class="sxs-lookup"><span data-stu-id="ae2de-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="ae2de-112">To make sure the tool gives you the right results, be sure to:</span><span class="sxs-lookup"><span data-stu-id="ae2de-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="ae2de-113">Open the tool on a browser from the server where you have installed the Connector.</span><span class="sxs-lookup"><span data-stu-id="ae2de-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="ae2de-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span><span class="sxs-lookup"><span data-stu-id="ae2de-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="ae2de-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span><span class="sxs-lookup"><span data-stu-id="ae2de-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="ae2de-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span><span class="sxs-lookup"><span data-stu-id="ae2de-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="ae2de-117">Select this box, and put the proxy address into the “Address” field.</span><span class="sxs-lookup"><span data-stu-id="ae2de-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae2de-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae2de-118">Next steps</span></span>
[<span data-ttu-id="ae2de-119">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="ae2de-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
