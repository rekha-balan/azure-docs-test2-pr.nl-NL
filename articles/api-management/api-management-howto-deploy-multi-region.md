---
title: Deploy Azure API Management services to multiple Azure regions | Microsoft Docs
description: Learn how to deploy an Azure API Management service instance to multiple Azure regions.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 194e3bb853be3831fed02c47fd95ce1616b0479b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555612"
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="13a08-103">How to deploy an Azure API Management service instance to multiple Azure regions</span><span class="sxs-lookup"><span data-stu-id="13a08-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="13a08-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span><span class="sxs-lookup"><span data-stu-id="13a08-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="13a08-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span><span class="sxs-lookup"><span data-stu-id="13a08-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="13a08-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span><span class="sxs-lookup"><span data-stu-id="13a08-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="13a08-107">Additional regions can be easily added through the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="13a08-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="13a08-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span><span class="sxs-lookup"><span data-stu-id="13a08-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="13a08-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span><span class="sxs-lookup"><span data-stu-id="13a08-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="13a08-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span><span class="sxs-lookup"><span data-stu-id="13a08-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="13a08-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span><span class="sxs-lookup"><span data-stu-id="13a08-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="13a08-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="13a08-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="13a08-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="13a08-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Scale tab][api-management-scale-service]

<span data-ttu-id="13a08-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span><span class="sxs-lookup"><span data-stu-id="13a08-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Add region][api-management-add-region]

<span data-ttu-id="13a08-117">Select the location from the drop-down list and set the number of units for with the slider.</span><span class="sxs-lookup"><span data-stu-id="13a08-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Specify units][api-management-select-location-units]

<span data-ttu-id="13a08-119">Click **Add** to place your selection in the Locations table.</span><span class="sxs-lookup"><span data-stu-id="13a08-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="13a08-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span><span class="sxs-lookup"><span data-stu-id="13a08-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="13a08-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span><span class="sxs-lookup"><span data-stu-id="13a08-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="13a08-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="13a08-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Scale tab][api-management-scale-service]

<span data-ttu-id="13a08-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span><span class="sxs-lookup"><span data-stu-id="13a08-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="13a08-125">Select the **Delete** option.</span><span class="sxs-lookup"><span data-stu-id="13a08-125">Select the **Delete** option.</span></span>

![Remove region][api-management-remove-region]

<span data-ttu-id="13a08-127">Confirm the deletion and click **Save** to apply the changes.</span><span class="sxs-lookup"><span data-stu-id="13a08-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/






