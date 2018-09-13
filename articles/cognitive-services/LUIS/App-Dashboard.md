---
title: Application dashboard for LUIS apps | Microsoft Docs
description: Learn about the application dashboard, a visualized reporting tool that enables you to monitor your apps at a single glance.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: 351f208d173bbabdbe47c71fdac94800e3554232
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660535"
---
# <a name="application-dashboard"></a><span data-ttu-id="07627-103">Application Dashboard</span><span class="sxs-lookup"><span data-stu-id="07627-103">Application Dashboard</span></span>
<span data-ttu-id="07627-104">The app dashboard is a visualized reporting tool which enables you to monitor your app at a single glance.</span><span class="sxs-lookup"><span data-stu-id="07627-104">The app dashboard is a visualized reporting tool which enables you to monitor your app at a single glance.</span></span> <span data-ttu-id="07627-105">The **Dashboard** is the main page that is displayed when you open an app by clicking the application name on **My Apps** page.</span><span class="sxs-lookup"><span data-stu-id="07627-105">The **Dashboard** is the main page that is displayed when you open an app by clicking the application name on **My Apps** page.</span></span> <span data-ttu-id="07627-106">Also, you can access the **Dashboard** page from inside your app by clicking **Dashboard** in the application's left panel.</span><span class="sxs-lookup"><span data-stu-id="07627-106">Also, you can access the **Dashboard** page from inside your app by clicking **Dashboard** in the application's left panel.</span></span> 

<span data-ttu-id="07627-107">The **Dashboard** page gives you an overview of the app and displays significant data compiled from multiple app pages.</span><span class="sxs-lookup"><span data-stu-id="07627-107">The **Dashboard** page gives you an overview of the app and displays significant data compiled from multiple app pages.</span></span> <span data-ttu-id="07627-108">Some data are analyzed and visualized by graphs and charts to help you get more insight into the app.</span><span class="sxs-lookup"><span data-stu-id="07627-108">Some data are analyzed and visualized by graphs and charts to help you get more insight into the app.</span></span> <span data-ttu-id="07627-109">The dashboard incorporates the latest updates in the app up to the moment and reflects any model changes.</span><span class="sxs-lookup"><span data-stu-id="07627-109">The dashboard incorporates the latest updates in the app up to the moment and reflects any model changes.</span></span> <span data-ttu-id="07627-110">The screenshot below shows the **Dashboard** page.</span><span class="sxs-lookup"><span data-stu-id="07627-110">The screenshot below shows the **Dashboard** page.</span></span>

![The Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard.JPG)

<span data-ttu-id="07627-112">At the top of the **Dashboard** page, a contextual notification bar constantly displays notifications to update you on the required or recommended actions appropriate for the current state of your app.</span><span class="sxs-lookup"><span data-stu-id="07627-112">At the top of the **Dashboard** page, a contextual notification bar constantly displays notifications to update you on the required or recommended actions appropriate for the current state of your app.</span></span> <span data-ttu-id="07627-113">It also provides useful tips and alerts as needed.</span><span class="sxs-lookup"><span data-stu-id="07627-113">It also provides useful tips and alerts as needed.</span></span> <span data-ttu-id="07627-114">Below is a detailed description of the data reported on the **Dashboard** page.</span><span class="sxs-lookup"><span data-stu-id="07627-114">Below is a detailed description of the data reported on the **Dashboard** page.</span></span>
 
  
## <a name="app-status"></a><span data-ttu-id="07627-115">App Status</span><span class="sxs-lookup"><span data-stu-id="07627-115">App Status</span></span>
<span data-ttu-id="07627-116">The dashboard displays the application's training and publishing status, including the date and time when the app was last trained and published.</span><span class="sxs-lookup"><span data-stu-id="07627-116">The dashboard displays the application's training and publishing status, including the date and time when the app was last trained and published.</span></span>  

![Dashboard - App Status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-AppStatus.JPG)

## <a name="model-data-statistics"></a><span data-ttu-id="07627-118">Model Data Statistics</span><span class="sxs-lookup"><span data-stu-id="07627-118">Model Data Statistics</span></span>
<span data-ttu-id="07627-119">The dashboard displays the total numbers of intents, entities & labeled utterances existing in the app.</span><span class="sxs-lookup"><span data-stu-id="07627-119">The dashboard displays the total numbers of intents, entities & labeled utterances existing in the app.</span></span> 

![App Data Statistics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-statistics.JPG)

## <a name="endpoint-hits"></a><span data-ttu-id="07627-121">Endpoint Hits</span><span class="sxs-lookup"><span data-stu-id="07627-121">Endpoint Hits</span></span>
<span data-ttu-id="07627-122">The dashboard displays the total endpoint hits received to the app and enables you to display hits within a period that you specify.</span><span class="sxs-lookup"><span data-stu-id="07627-122">The dashboard displays the total endpoint hits received to the app and enables you to display hits within a period that you specify.</span></span>

![Endpoint Hits](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-endpointHits.JPG)
 
### <a name="total-endpoint-hits"></a><span data-ttu-id="07627-124">Total endpoint hits</span><span class="sxs-lookup"><span data-stu-id="07627-124">Total endpoint hits</span></span>
<span data-ttu-id="07627-125">The total number of endpoint hits received to your app since app creation up to the current date.</span><span class="sxs-lookup"><span data-stu-id="07627-125">The total number of endpoint hits received to your app since app creation up to the current date.</span></span>

### <a name="endpoint-hits-per-period"></a><span data-ttu-id="07627-126">Endpoint hits per period</span><span class="sxs-lookup"><span data-stu-id="07627-126">Endpoint hits per period</span></span>
<span data-ttu-id="07627-127">The number of hits received within a past period, displayed per day.</span><span class="sxs-lookup"><span data-stu-id="07627-127">The number of hits received within a past period, displayed per day.</span></span> <span data-ttu-id="07627-128">A visualized line chart shows the period span from the calculated start date up to the current date (end date).</span><span class="sxs-lookup"><span data-stu-id="07627-128">A visualized line chart shows the period span from the calculated start date up to the current date (end date).</span></span> <span data-ttu-id="07627-129">The points between the start and end dates represent the days falling in this period.</span><span class="sxs-lookup"><span data-stu-id="07627-129">The points between the start and end dates represent the days falling in this period.</span></span> <span data-ttu-id="07627-130">Hover your mouse pointer over each point to see the hits count in each day within the period.</span><span class="sxs-lookup"><span data-stu-id="07627-130">Hover your mouse pointer over each point to see the hits count in each day within the period.</span></span> <span data-ttu-id="07627-131">The screenshot below shows the line chart.</span><span class="sxs-lookup"><span data-stu-id="07627-131">The screenshot below shows the line chart.</span></span>
 
![Hits per Period](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-PeriodHitsChart.jpg)

<span data-ttu-id="07627-133">To select a period to view its hits on the chart:</span><span class="sxs-lookup"><span data-stu-id="07627-133">To select a period to view its hits on the chart:</span></span>
 
1. <span data-ttu-id="07627-134">Click **Additional Settings** ![Additional Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-Settings-btn.JPG) to access the periods list.</span><span class="sxs-lookup"><span data-stu-id="07627-134">Click **Additional Settings** ![Additional Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-Settings-btn.JPG) to access the periods list.</span></span> <span data-ttu-id="07627-135">You can select periods ranging from one week up to one year beforehand.</span><span class="sxs-lookup"><span data-stu-id="07627-135">You can select periods ranging from one week up to one year beforehand.</span></span> 

    ![Endpoint Hits per Period](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-hitsPerPeriod.JPG)

2. <span data-ttu-id="07627-137">Select a period from the list and then click the back arrow</span><span class="sxs-lookup"><span data-stu-id="07627-137">Select a period from the list and then click the back arrow</span></span> ![Back Arrow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-backArrow.JPG) <span data-ttu-id="07627-139">to display its hits on the chart.</span><span class="sxs-lookup"><span data-stu-id="07627-139">to display its hits on the chart.</span></span>

### <a name="key-usage"></a><span data-ttu-id="07627-140">Key usage</span><span class="sxs-lookup"><span data-stu-id="07627-140">Key usage</span></span>
<span data-ttu-id="07627-141">The number of hits consumed from the application's subscription key.</span><span class="sxs-lookup"><span data-stu-id="07627-141">The number of hits consumed from the application's subscription key.</span></span> <span data-ttu-id="07627-142">For more details about subscription keys, see [Manage your keys](manage-keys.md).</span><span class="sxs-lookup"><span data-stu-id="07627-142">For more details about subscription keys, see [Manage your keys](manage-keys.md).</span></span> 
  
## <a name="intent-breakdown"></a><span data-ttu-id="07627-143">Intent Breakdown</span><span class="sxs-lookup"><span data-stu-id="07627-143">Intent Breakdown</span></span>
<span data-ttu-id="07627-144">The dashboard displays a breakdown of intents based on labeled utterances or endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="07627-144">The dashboard displays a breakdown of intents based on labeled utterances or endpoint hits.</span></span> <span data-ttu-id="07627-145">It visualizes the distribution of intents across labeled utterances/endpoint hits, so that you can see the relative importance of each intent in the app.</span><span class="sxs-lookup"><span data-stu-id="07627-145">It visualizes the distribution of intents across labeled utterances/endpoint hits, so that you can see the relative importance of each intent in the app.</span></span> <span data-ttu-id="07627-146">The intent breakdown is visualized by a pie chart with the slices representing intents.</span><span class="sxs-lookup"><span data-stu-id="07627-146">The intent breakdown is visualized by a pie chart with the slices representing intents.</span></span> <span data-ttu-id="07627-147">When you hover your mouse pointer over a slice, you'll see the intent name and the percentage it represents of the total count of labeled utterances/endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="07627-147">When you hover your mouse pointer over a slice, you'll see the intent name and the percentage it represents of the total count of labeled utterances/endpoint hits.</span></span> 

![Intent Breakdown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-IntentBreakdown.jpg)

<span data-ttu-id="07627-149">To control whether the breakdown is based on labeled utterances or endpoint hits:</span><span class="sxs-lookup"><span data-stu-id="07627-149">To control whether the breakdown is based on labeled utterances or endpoint hits:</span></span>

1. <span data-ttu-id="07627-150">Click **Additional Settings** ![Additional Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-Settings-btn.JPG) to access the list as in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="07627-150">Click **Additional Settings** ![Additional Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-Settings-btn.JPG) to access the list as in the screenshot below.</span></span>

    ![Intent Breakdown List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-IntentBreakdownlist.jpg)
2. <span data-ttu-id="07627-152">Select a value from the list and then click the back arrow</span><span class="sxs-lookup"><span data-stu-id="07627-152">Select a value from the list and then click the back arrow</span></span> ![Back Arrow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-backArrow.JPG) <span data-ttu-id="07627-154">to display the chart accordingly.</span><span class="sxs-lookup"><span data-stu-id="07627-154">to display the chart accordingly.</span></span>

## <a name="entity-breakdown"></a><span data-ttu-id="07627-155">Entity Breakdown</span><span class="sxs-lookup"><span data-stu-id="07627-155">Entity Breakdown</span></span>
<span data-ttu-id="07627-156">The dashboard displays a breakdown of entities based on labeled utterances or endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="07627-156">The dashboard displays a breakdown of entities based on labeled utterances or endpoint hits.</span></span> <span data-ttu-id="07627-157">It visualizes the distribution of entities across labeled utterances/endpoint hits, showing the usage of each entity in labeled utterances/endpoint hits compared to the other entities.</span><span class="sxs-lookup"><span data-stu-id="07627-157">It visualizes the distribution of entities across labeled utterances/endpoint hits, showing the usage of each entity in labeled utterances/endpoint hits compared to the other entities.</span></span> <span data-ttu-id="07627-158">The entity breakdown is visualized by a column chart where entities are displayed along the horizontal axis while their count in labeled utterances/endpoint hits along the vertical axis.</span><span class="sxs-lookup"><span data-stu-id="07627-158">The entity breakdown is visualized by a column chart where entities are displayed along the horizontal axis while their count in labeled utterances/endpoint hits along the vertical axis.</span></span> <span data-ttu-id="07627-159">When you hover your mouse pointer over a rectangular bar, you'll see the entity name and its count (number of occurrences) in labeled utterances/endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="07627-159">When you hover your mouse pointer over a rectangular bar, you'll see the entity name and its count (number of occurrences) in labeled utterances/endpoint hits.</span></span> 

![Entity Breakdown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-EntityBreakdown.jpg)

<span data-ttu-id="07627-161">To control whether the breakdown is based on labeled utterances or endpoint hits:</span><span class="sxs-lookup"><span data-stu-id="07627-161">To control whether the breakdown is based on labeled utterances or endpoint hits:</span></span>

1. <span data-ttu-id="07627-162">Click **Additional Settings** ![Additional Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-Settings-btn.JPG) to access the list as in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="07627-162">Click **Additional Settings** ![Additional Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-Settings-btn.JPG) to access the list as in the screenshot below.</span></span>

    ![Entity Breakdown List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-EntityBreakdownlist.jpg)
2. <span data-ttu-id="07627-164">Select a value from the list and then click the back arrow</span><span class="sxs-lookup"><span data-stu-id="07627-164">Select a value from the list and then click the back arrow</span></span> ![Back Arrow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Dashboard-backArrow.JPG) <span data-ttu-id="07627-166">to display the chart accordingly.</span><span class="sxs-lookup"><span data-stu-id="07627-166">to display the chart accordingly.</span></span>
















