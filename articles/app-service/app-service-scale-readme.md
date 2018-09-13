---
title: 'Azure App Service: Scaling App Service Applications'
description: Learn the ins and outs of scaling Application in App Service.
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: ''
author: btardif
manager: erikre
editor: ''
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660542"
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="e097e-104">Azure App Service: Scaling App Service Applications</span><span class="sxs-lookup"><span data-stu-id="e097e-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="e097e-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="e097e-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="e097e-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span><span class="sxs-lookup"><span data-stu-id="e097e-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="e097e-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span><span class="sxs-lookup"><span data-stu-id="e097e-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="e097e-108">Understanding your application architecture and its weaknesses.</span><span class="sxs-lookup"><span data-stu-id="e097e-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="e097e-109">Is your Application Stateful?</span><span class="sxs-lookup"><span data-stu-id="e097e-109">Is your Application Stateful?</span></span> <span data-ttu-id="e097e-110">Stateless?</span><span class="sxs-lookup"><span data-stu-id="e097e-110">Stateless?</span></span>
   * <span data-ttu-id="e097e-111">What are all the components of your application?</span><span class="sxs-lookup"><span data-stu-id="e097e-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="e097e-112">Where are the bottlenecks in the application?</span><span class="sxs-lookup"><span data-stu-id="e097e-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="e097e-113">When load is applied to your app, what will break first?</span><span class="sxs-lookup"><span data-stu-id="e097e-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="e097e-114">Understanding the expected load and performance requirements.</span><span class="sxs-lookup"><span data-stu-id="e097e-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="e097e-115">Does the application need to serve one thousand users? or one million?</span><span class="sxs-lookup"><span data-stu-id="e097e-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="e097e-116">Will traffic come from a single geographic location or globally?</span><span class="sxs-lookup"><span data-stu-id="e097e-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="e097e-117">Are there seasonal variations? traffic peaks?</span><span class="sxs-lookup"><span data-stu-id="e097e-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="e097e-118">How fast should the app respond?</span><span class="sxs-lookup"><span data-stu-id="e097e-118">How fast should the app respond?</span></span> <span data-ttu-id="e097e-119">1 second?</span><span class="sxs-lookup"><span data-stu-id="e097e-119">1 second?</span></span> <span data-ttu-id="e097e-120">1 millisecond?</span><span class="sxs-lookup"><span data-stu-id="e097e-120">1 millisecond?</span></span>
3. <span data-ttu-id="e097e-121">Understanding and correctly leverage the platform hosting your app.</span><span class="sxs-lookup"><span data-stu-id="e097e-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="e097e-122">What features should I leverage to achieve my scale goals?</span><span class="sxs-lookup"><span data-stu-id="e097e-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="e097e-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span><span class="sxs-lookup"><span data-stu-id="e097e-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

