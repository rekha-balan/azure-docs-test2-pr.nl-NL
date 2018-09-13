---
title: Azure App Service and its impact on existing Azure services
description: Explains how the new Azure App Service and its features impact existing services in Azure.
services: app-service
documentationcenter: ''
author: yochay
manager: nirma
editor: ''
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555038"
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="f3894-103">Azure App Service and existing Azure services</span><span class="sxs-lookup"><span data-stu-id="f3894-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="f3894-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span><span class="sxs-lookup"><span data-stu-id="f3894-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="f3894-105">Overview</span><span class="sxs-lookup"><span data-stu-id="f3894-105">Overview</span></span>
<span data-ttu-id="f3894-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span><span class="sxs-lookup"><span data-stu-id="f3894-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="f3894-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span><span class="sxs-lookup"><span data-stu-id="f3894-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="f3894-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span><span class="sxs-lookup"><span data-stu-id="f3894-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="f3894-109">App Service allows you to host the following app types:</span><span class="sxs-lookup"><span data-stu-id="f3894-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="f3894-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-110">Web Apps</span></span>
* <span data-ttu-id="f3894-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-111">Mobile Apps</span></span>
* <span data-ttu-id="f3894-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-112">API Apps</span></span>
* <span data-ttu-id="f3894-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-113">Logic Apps</span></span>

<span data-ttu-id="f3894-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span><span class="sxs-lookup"><span data-stu-id="f3894-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="f3894-115">Existing Azure Service</span><span class="sxs-lookup"><span data-stu-id="f3894-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="f3894-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f3894-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="f3894-117">What changed</span><span class="sxs-lookup"><span data-stu-id="f3894-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="f3894-118">Azure Websites</span><span class="sxs-lookup"><span data-stu-id="f3894-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="f3894-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="f3894-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span><span class="sxs-lookup"><span data-stu-id="f3894-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="f3894-121">All your existing instances of Websites are now Web Apps in App Service.</span><span class="sxs-lookup"><span data-stu-id="f3894-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="f3894-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="f3894-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="f3894-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span><span class="sxs-lookup"><span data-stu-id="f3894-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="f3894-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span><span class="sxs-lookup"><span data-stu-id="f3894-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="f3894-125">Azure App Service Web Apps is in General Availability.</span><span class="sxs-lookup"><span data-stu-id="f3894-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="f3894-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="f3894-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="f3894-127">Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="f3894-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="f3894-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="f3894-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span><span class="sxs-lookup"><span data-stu-id="f3894-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="f3894-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span><span class="sxs-lookup"><span data-stu-id="f3894-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="f3894-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="f3894-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="f3894-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span><span class="sxs-lookup"><span data-stu-id="f3894-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="f3894-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="f3894-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="f3894-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="f3894-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="f3894-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="f3894-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="f3894-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="f3894-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="f3894-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span><span class="sxs-lookup"><span data-stu-id="f3894-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="f3894-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="f3894-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="f3894-140">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="f3894-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="f3894-141">BizTalk API Apps</span><span class="sxs-lookup"><span data-stu-id="f3894-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="f3894-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span><span class="sxs-lookup"><span data-stu-id="f3894-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="f3894-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span><span class="sxs-lookup"><span data-stu-id="f3894-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="f3894-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span><span class="sxs-lookup"><span data-stu-id="f3894-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="f3894-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f3894-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

