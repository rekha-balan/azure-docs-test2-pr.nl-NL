---
title: Advanced Azure Stack evaluation tasks | Microsoft Docs
description: This article describes advanced Azure Stack evaluation tasks.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: c4bf76aa07ec5025d9e53b5518929199ace27e18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871329"
---
# <a name="advanced-azure-stack-development-kit-evaluation-tasks"></a><span data-ttu-id="a401e-103">Advanced Azure Stack Development Kit evaluation tasks</span><span class="sxs-lookup"><span data-stu-id="a401e-103">Advanced Azure Stack Development Kit evaluation tasks</span></span>
<span data-ttu-id="a401e-104">After you have gained familiarity with the basic Azure Stack Development Kit (ASDK) service features and capabilities, you can deepen your understanding of Azure Stack further by testing out more advanced scenarios.</span><span class="sxs-lookup"><span data-stu-id="a401e-104">After you have gained familiarity with the basic Azure Stack Development Kit (ASDK) service features and capabilities, you can deepen your understanding of Azure Stack further by testing out more advanced scenarios.</span></span> <span data-ttu-id="a401e-105">These more advanced evaluation tasks are documented fully in the Azure Stack Operator documentation.</span><span class="sxs-lookup"><span data-stu-id="a401e-105">These more advanced evaluation tasks are documented fully in the Azure Stack Operator documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="a401e-106">While many operator tasks are supported for both ASDK and production, multi-node Azure Stack deployments, not all usage scenarios are supported for ASDK deployments.</span><span class="sxs-lookup"><span data-stu-id="a401e-106">While many operator tasks are supported for both ASDK and production, multi-node Azure Stack deployments, not all usage scenarios are supported for ASDK deployments.</span></span> <span data-ttu-id="a401e-107">See [ASDK and multi-node Azure Stack differences](asdk-what-is.md#asdk-and-multi-node-azure-stack-differences) for more information.</span><span class="sxs-lookup"><span data-stu-id="a401e-107">See [ASDK and multi-node Azure Stack differences](asdk-what-is.md#asdk-and-multi-node-azure-stack-differences) for more information.</span></span>

## <a name="delegate-offers-in-azure-stack"></a><span data-ttu-id="a401e-108">Delegate offers in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a401e-108">Delegate offers in Azure Stack</span></span>
<span data-ttu-id="a401e-109">As the Azure Stack Operator, you often want to put other people in charge of creating offers and signing up users.</span><span class="sxs-lookup"><span data-stu-id="a401e-109">As the Azure Stack Operator, you often want to put other people in charge of creating offers and signing up users.</span></span> <span data-ttu-id="a401e-110">For example, if you're a service provider, you might want resellers to sign up customers and manage them on your behalf.</span><span class="sxs-lookup"><span data-stu-id="a401e-110">For example, if you're a service provider, you might want resellers to sign up customers and manage them on your behalf.</span></span> <span data-ttu-id="a401e-111">Or if you're part of a central IT group in an enterprise, you might want subsidiaries to sign up users without your intervention.</span><span class="sxs-lookup"><span data-stu-id="a401e-111">Or if you're part of a central IT group in an enterprise, you might want subsidiaries to sign up users without your intervention.</span></span>

<span data-ttu-id="a401e-112">[Delegating offers in Azure Stack](.\.\azure-stack-delegated-provider.md) helps you with these tasks by making it possible to reach and manage more users than you can directly.</span><span class="sxs-lookup"><span data-stu-id="a401e-112">[Delegating offers in Azure Stack](.\.\azure-stack-delegated-provider.md) helps you with these tasks by making it possible to reach and manage more users than you can directly.</span></span> 

## <a name="make-sql-databases-available-to-your-azure-stack-users"></a><span data-ttu-id="a401e-113">Make SQL databases available to your Azure Stack users</span><span class="sxs-lookup"><span data-stu-id="a401e-113">Make SQL databases available to your Azure Stack users</span></span>
<span data-ttu-id="a401e-114">As an Azure Stack Operator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span><span class="sxs-lookup"><span data-stu-id="a401e-114">As an Azure Stack Operator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span></span> <span data-ttu-id="a401e-115">By providing these custom, on-demand, cloud-based databases to your users, you can save them time and resources.</span><span class="sxs-lookup"><span data-stu-id="a401e-115">By providing these custom, on-demand, cloud-based databases to your users, you can save them time and resources.</span></span> 

<span data-ttu-id="a401e-116">Use the SQL Server resource provider adapter to [make SQL databases available to your Azure Stack users](.\.\azure-stack-tutorial-sql-server.md) as a service of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a401e-116">Use the SQL Server resource provider adapter to [make SQL databases available to your Azure Stack users](.\.\azure-stack-tutorial-sql-server.md) as a service of Azure Stack.</span></span> <span data-ttu-id="a401e-117">After you install the resource provider you connect it to one or more SQL Server instances.</span><span class="sxs-lookup"><span data-stu-id="a401e-117">After you install the resource provider you connect it to one or more SQL Server instances.</span></span>

## <a name="make-web-and-api-apps-available-to-your-azure-stack-users"></a><span data-ttu-id="a401e-118">Make web and API apps available to your Azure Stack users</span><span class="sxs-lookup"><span data-stu-id="a401e-118">Make web and API apps available to your Azure Stack users</span></span>
<span data-ttu-id="a401e-119">As an Azure Stack Operator, you can create offers that let your users (tenants) create Azure Functions and web, and API applications.</span><span class="sxs-lookup"><span data-stu-id="a401e-119">As an Azure Stack Operator, you can create offers that let your users (tenants) create Azure Functions and web, and API applications.</span></span> <span data-ttu-id="a401e-120">By providing access to these on-demand, cloud-based apps to your users, you can save them time and resources.</span><span class="sxs-lookup"><span data-stu-id="a401e-120">By providing access to these on-demand, cloud-based apps to your users, you can save them time and resources.</span></span>

<span data-ttu-id="a401e-121">Deploy the App Service resource provider to [make web and API apps available to your Azure Stack users](.\.\azure-stack-tutorial-app-service.md)</span><span class="sxs-lookup"><span data-stu-id="a401e-121">Deploy the App Service resource provider to [make web and API apps available to your Azure Stack users](.\.\azure-stack-tutorial-app-service.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a401e-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a401e-122">Next steps</span></span>
[<span data-ttu-id="a401e-123">Learn more about offering services with Azure Stack integrated systems</span><span class="sxs-lookup"><span data-stu-id="a401e-123">Learn more about offering services with Azure Stack integrated systems</span></span>](.\.\azure-stack-offer-services-overview.md)