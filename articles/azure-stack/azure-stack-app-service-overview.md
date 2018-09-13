---
title: App Service Overview - Azure Stack | Microsoft Docs
description: Overview of App Service on Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9e6ff610f33a2e4cbd4f3c39074f8809f156ec4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551770"
---
# <a name="app-service-on-azure-stack-overview"></a><span data-ttu-id="c6a70-103">App Service on Azure Stack Overview</span><span class="sxs-lookup"><span data-stu-id="c6a70-103">App Service on Azure Stack Overview</span></span>

<span data-ttu-id="c6a70-104">App Service on Azure Stack is the Azure offering brought to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c6a70-104">App Service on Azure Stack is the Azure offering brought to Azure Stack.</span></span> <span data-ttu-id="c6a70-105">The App Service on Azure Stack installer will create the following set of role instances:</span><span class="sxs-lookup"><span data-stu-id="c6a70-105">The App Service on Azure Stack installer will create the following set of role instances:</span></span>
*  <span data-ttu-id="c6a70-106">Controller;</span><span class="sxs-lookup"><span data-stu-id="c6a70-106">Controller;</span></span>
*  <span data-ttu-id="c6a70-107">Management (Two instances will be created);</span><span class="sxs-lookup"><span data-stu-id="c6a70-107">Management (Two instances will be created);</span></span>
*  <span data-ttu-id="c6a70-108">Front-End;</span><span class="sxs-lookup"><span data-stu-id="c6a70-108">Front-End;</span></span>
*  <span data-ttu-id="c6a70-109">Publisher;</span><span class="sxs-lookup"><span data-stu-id="c6a70-109">Publisher;</span></span>
*  <span data-ttu-id="c6a70-110">Worker (in Shared mode)</span><span class="sxs-lookup"><span data-stu-id="c6a70-110">Worker (in Shared mode)</span></span>

<span data-ttu-id="c6a70-111">In addition, the App Service on Azure Stack installer will create a file server.</span><span class="sxs-lookup"><span data-stu-id="c6a70-111">In addition, the App Service on Azure Stack installer will create a file server.</span></span>
    
## <a name="whats-new-in-technical-preview-3-of-app-service-on-azure-stack"></a><span data-ttu-id="c6a70-112">What's New in Technical Preview 3 of App Service on Azure Stack?</span><span class="sxs-lookup"><span data-stu-id="c6a70-112">What's New in Technical Preview 3 of App Service on Azure Stack?</span></span>
![App Service in the Azure Stack Portal][1]

<span data-ttu-id="c6a70-114">Technical Preview 3 of App Service on Azure Stack, builds on top of the second preview and brings a preview of Azure Functions to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c6a70-114">Technical Preview 3 of App Service on Azure Stack, builds on top of the second preview and brings a preview of Azure Functions to Azure Stack.</span></span>  <span data-ttu-id="c6a70-115">Azure Functions is an event-based serverless compute experience to accelerate your development.</span><span class="sxs-lookup"><span data-stu-id="c6a70-115">Azure Functions is an event-based serverless compute experience to accelerate your development.</span></span>  <span data-ttu-id="c6a70-116">New improvements to the stability of the service, updates to the Tenant Portal experience along with updates to the installer experience to give more configuration options.</span><span class="sxs-lookup"><span data-stu-id="c6a70-116">New improvements to the stability of the service, updates to the Tenant Portal experience along with updates to the installer experience to give more configuration options.</span></span>

## <a name="limitations-of-the-technical-preview"></a><span data-ttu-id="c6a70-117">Limitations of the Technical Preview</span><span class="sxs-lookup"><span data-stu-id="c6a70-117">Limitations of the Technical Preview</span></span>

<span data-ttu-id="c6a70-118">There is no support for the App Service on Azure Stack preview releases, although we do monitor the Azure Stack MSDN Forum.</span><span class="sxs-lookup"><span data-stu-id="c6a70-118">There is no support for the App Service on Azure Stack preview releases, although we do monitor the Azure Stack MSDN Forum.</span></span> <span data-ttu-id="c6a70-119">Don't put production workloads on this preview release.</span><span class="sxs-lookup"><span data-stu-id="c6a70-119">Don't put production workloads on this preview release.</span></span> <span data-ttu-id="c6a70-120">There is also no upgrade between App Service on Azure Stack preview releases.</span><span class="sxs-lookup"><span data-stu-id="c6a70-120">There is also no upgrade between App Service on Azure Stack preview releases.</span></span> <span data-ttu-id="c6a70-121">The primary purposes of these preview releases are to show what we are providing and to obtain feedback.</span><span class="sxs-lookup"><span data-stu-id="c6a70-121">The primary purposes of these preview releases are to show what we are providing and to obtain feedback.</span></span> 

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="c6a70-122">What is an App Service Plan?</span><span class="sxs-lookup"><span data-stu-id="c6a70-122">What is an App Service Plan?</span></span>

<span data-ttu-id="c6a70-123">The App Service resource provider uses the same code that Azure App Service uses.</span><span class="sxs-lookup"><span data-stu-id="c6a70-123">The App Service resource provider uses the same code that Azure App Service uses.</span></span> <span data-ttu-id="c6a70-124">As a result, some common concepts are worth describing.</span><span class="sxs-lookup"><span data-stu-id="c6a70-124">As a result, some common concepts are worth describing.</span></span> <span data-ttu-id="c6a70-125">In App Service, the pricing container for applications is called the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c6a70-125">In App Service, the pricing container for applications is called the App Service plan.</span></span> <span data-ttu-id="c6a70-126">It represents the set of dedicated virtual machines used to hold your apps.</span><span class="sxs-lookup"><span data-stu-id="c6a70-126">It represents the set of dedicated virtual machines used to hold your apps.</span></span> <span data-ttu-id="c6a70-127">Within a given subscription, you can have multiple App Service plans.</span><span class="sxs-lookup"><span data-stu-id="c6a70-127">Within a given subscription, you can have multiple App Service plans.</span></span> 

<span data-ttu-id="c6a70-128">In Azure, there are shared and dedicated workers.</span><span class="sxs-lookup"><span data-stu-id="c6a70-128">In Azure, there are shared and dedicated workers.</span></span> <span data-ttu-id="c6a70-129">A shared worker supports high-density multitenant app hosting and there is only one set of shared workers.</span><span class="sxs-lookup"><span data-stu-id="c6a70-129">A shared worker supports high-density multitenant app hosting and there is only one set of shared workers.</span></span> <span data-ttu-id="c6a70-130">Dedicated servers are only used by one tenant and come in three sizes: small, medium, and large.</span><span class="sxs-lookup"><span data-stu-id="c6a70-130">Dedicated servers are only used by one tenant and come in three sizes: small, medium, and large.</span></span> <span data-ttu-id="c6a70-131">The needs of on-premises customers can't always be described by using those terms.</span><span class="sxs-lookup"><span data-stu-id="c6a70-131">The needs of on-premises customers can't always be described by using those terms.</span></span> <span data-ttu-id="c6a70-132">In App Service on Azure Stack, resource provider administrators can define the worker tiers they want to make available.</span><span class="sxs-lookup"><span data-stu-id="c6a70-132">In App Service on Azure Stack, resource provider administrators can define the worker tiers they want to make available.</span></span>  <span data-ttu-id="c6a70-133">Therefore having multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span><span class="sxs-lookup"><span data-stu-id="c6a70-133">Therefore having multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span></span> <span data-ttu-id="c6a70-134">Using those worker tier definitions, they can then define their own pricing SKUs.</span><span class="sxs-lookup"><span data-stu-id="c6a70-134">Using those worker tier definitions, they can then define their own pricing SKUs.</span></span>

## <a name="portal-features"></a><span data-ttu-id="c6a70-135">Portal Features</span><span class="sxs-lookup"><span data-stu-id="c6a70-135">Portal Features</span></span>

<span data-ttu-id="c6a70-136">App Service on Azure Stack uses the same UI that Azure App Service uses, as is true with the back end.</span><span class="sxs-lookup"><span data-stu-id="c6a70-136">App Service on Azure Stack uses the same UI that Azure App Service uses, as is true with the back end.</span></span> <span data-ttu-id="c6a70-137">Some features are disabled and aren't yet functional in Azure Stack, because Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c6a70-137">Some features are disabled and aren't yet functional in Azure Stack, because Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c6a70-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6a70-138">Next steps</span></span>

- [<span data-ttu-id="c6a70-139">Before you get started with App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c6a70-139">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
- [<span data-ttu-id="c6a70-140">Install the App Service Resource Provider</span><span class="sxs-lookup"><span data-stu-id="c6a70-140">Install the App Service Resource Provider</span></span>](azure-stack-app-service-deploy.md)

<span data-ttu-id="c6a70-141">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c6a70-141">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-overview/AppService_Portal.png

