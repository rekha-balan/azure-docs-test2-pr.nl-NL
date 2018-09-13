---
title: Using New Relic with Azure | Microsoft Docs
description: Learn how to use the New Relic service to manage and monitor your Azure application.
services: ''
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: ''
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: f4f13c909a6ff640d403f5264004176c087925dd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550747"
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="51a0b-103">New Relic Application Performance Management on Azure</span><span class="sxs-lookup"><span data-stu-id="51a0b-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="51a0b-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span><span class="sxs-lookup"><span data-stu-id="51a0b-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span></span> <span data-ttu-id="51a0b-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span><span class="sxs-lookup"><span data-stu-id="51a0b-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="51a0b-106">What is New Relic?</span><span class="sxs-lookup"><span data-stu-id="51a0b-106">What is New Relic?</span></span>
<span data-ttu-id="51a0b-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span><span class="sxs-lookup"><span data-stu-id="51a0b-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span></span> <span data-ttu-id="51a0b-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span><span class="sxs-lookup"><span data-stu-id="51a0b-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span></span>

<span data-ttu-id="51a0b-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span><span class="sxs-lookup"><span data-stu-id="51a0b-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span></span> <span data-ttu-id="51a0b-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span><span class="sxs-lookup"><span data-stu-id="51a0b-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="51a0b-111">Special pricing</span><span class="sxs-lookup"><span data-stu-id="51a0b-111">Special pricing</span></span>
<span data-ttu-id="51a0b-112">New Relic Standard is free to Azure users.</span><span class="sxs-lookup"><span data-stu-id="51a0b-112">New Relic Standard is free to Azure users.</span></span> <span data-ttu-id="51a0b-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="51a0b-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="51a0b-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span><span class="sxs-lookup"><span data-stu-id="51a0b-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="51a0b-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span><span class="sxs-lookup"><span data-stu-id="51a0b-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-the-azure-store"></a><span data-ttu-id="51a0b-116">Sign up for New Relic using the Azure Store</span><span class="sxs-lookup"><span data-stu-id="51a0b-116">Sign up for New Relic using the Azure Store</span></span>
<span data-ttu-id="51a0b-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span><span class="sxs-lookup"><span data-stu-id="51a0b-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="51a0b-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span><span class="sxs-lookup"><span data-stu-id="51a0b-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span></span> <span data-ttu-id="51a0b-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span><span class="sxs-lookup"><span data-stu-id="51a0b-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="51a0b-120">View your data</span><span class="sxs-lookup"><span data-stu-id="51a0b-120">View your data</span></span>
<span data-ttu-id="51a0b-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span><span class="sxs-lookup"><span data-stu-id="51a0b-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="51a0b-122">To check your app's performance in New Relic:</span><span class="sxs-lookup"><span data-stu-id="51a0b-122">To check your app's performance in New Relic:</span></span>

1. <span data-ttu-id="51a0b-123">From the Azure Portal, select Manage.</span><span class="sxs-lookup"><span data-stu-id="51a0b-123">From the Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="51a0b-124">Sign in with your New Relic account email and password.</span><span class="sxs-lookup"><span data-stu-id="51a0b-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="51a0b-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="51a0b-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="51a0b-126">Using New Relic with Azure</span><span class="sxs-lookup"><span data-stu-id="51a0b-126">Using New Relic with Azure</span></span>
<span data-ttu-id="51a0b-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span><span class="sxs-lookup"><span data-stu-id="51a0b-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="51a0b-128">New Relic for .NET</span><span class="sxs-lookup"><span data-stu-id="51a0b-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="51a0b-129">Instrument a .NET Worker Role on Azure Cloud service</span><span class="sxs-lookup"><span data-stu-id="51a0b-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="51a0b-130">New Relic for the Microsoft Azure Cloud platform</span><span class="sxs-lookup"><span data-stu-id="51a0b-130">New Relic for the Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="51a0b-131">New Relic for the Microsoft Azure App Services</span><span class="sxs-lookup"><span data-stu-id="51a0b-131">New Relic for the Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="51a0b-132">New Relic/Azure troubleshooting</span><span class="sxs-lookup"><span data-stu-id="51a0b-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

