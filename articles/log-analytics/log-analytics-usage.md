---
title: Analyze data usage in Log Analytics | Microsoft Docs
description: You can use the Usage dashboard in Log Analytics to view how much data is being sent to the OMS service.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: 13ae96979e51dc62a8712837edf03b7b13ee30a7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563405"
---
# <a name="analyze-data-usage-in-log-analytics"></a><span data-ttu-id="a170c-103">Analyze data usage in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a170c-103">Analyze data usage in Log Analytics</span></span>
<span data-ttu-id="a170c-104">Log Analytics collects data and sends it to the OMS service periodically.</span><span class="sxs-lookup"><span data-stu-id="a170c-104">Log Analytics collects data and sends it to the OMS service periodically.</span></span>  <span data-ttu-id="a170c-105">You can use the **Log Analytics Usage** dashboard to view how much data is being sent to the OMS service.</span><span class="sxs-lookup"><span data-stu-id="a170c-105">You can use the **Log Analytics Usage** dashboard to view how much data is being sent to the OMS service.</span></span> <span data-ttu-id="a170c-106">The dashboard also shows you how much data is being sent by solutions and how often your servers are sending data.</span><span class="sxs-lookup"><span data-stu-id="a170c-106">The dashboard also shows you how much data is being sent by solutions and how often your servers are sending data.</span></span>

> [!NOTE]
> <span data-ttu-id="a170c-107">If you have a free account, you're limited to sending 500 MB of data to the OMS service daily.</span><span class="sxs-lookup"><span data-stu-id="a170c-107">If you have a free account, you're limited to sending 500 MB of data to the OMS service daily.</span></span> <span data-ttu-id="a170c-108">If you reach the daily limit, data analysis stops and resumes at the start of the next day.</span><span class="sxs-lookup"><span data-stu-id="a170c-108">If you reach the daily limit, data analysis stops and resumes at the start of the next day.</span></span> <span data-ttu-id="a170c-109">In that case, you need to resend any data that wasn't accepted or processed by OMS.</span><span class="sxs-lookup"><span data-stu-id="a170c-109">In that case, you need to resend any data that wasn't accepted or processed by OMS.</span></span>

<span data-ttu-id="a170c-110">If you have exceeded or are near your daily usage limit, you can optionally remove a solution to reduce the amount of data to send to the OMS service.</span><span class="sxs-lookup"><span data-stu-id="a170c-110">If you have exceeded or are near your daily usage limit, you can optionally remove a solution to reduce the amount of data to send to the OMS service.</span></span> <span data-ttu-id="a170c-111">For more information about removing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="a170c-111">For more information about removing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

![usage dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/usage-dashboard01.png)

<span data-ttu-id="a170c-113">The **Log Analytics usage** dashboard displays the following information:</span><span class="sxs-lookup"><span data-stu-id="a170c-113">The **Log Analytics usage** dashboard displays the following information:</span></span>

- <span data-ttu-id="a170c-114">Data volume</span><span class="sxs-lookup"><span data-stu-id="a170c-114">Data volume</span></span>
    - <span data-ttu-id="a170c-115">Data volume over time (based on your current time scope)</span><span class="sxs-lookup"><span data-stu-id="a170c-115">Data volume over time (based on your current time scope)</span></span>
    - <span data-ttu-id="a170c-116">Data volume by solution</span><span class="sxs-lookup"><span data-stu-id="a170c-116">Data volume by solution</span></span>
    - <span data-ttu-id="a170c-117">Data not associated with a computer</span><span class="sxs-lookup"><span data-stu-id="a170c-117">Data not associated with a computer</span></span>
- <span data-ttu-id="a170c-118">Computers</span><span class="sxs-lookup"><span data-stu-id="a170c-118">Computers</span></span>
    - <span data-ttu-id="a170c-119">Computers sending data</span><span class="sxs-lookup"><span data-stu-id="a170c-119">Computers sending data</span></span>
    - <span data-ttu-id="a170c-120">Computers with no data in last 24 hours</span><span class="sxs-lookup"><span data-stu-id="a170c-120">Computers with no data in last 24 hours</span></span>
- <span data-ttu-id="a170c-121">Offerings</span><span class="sxs-lookup"><span data-stu-id="a170c-121">Offerings</span></span>
    - <span data-ttu-id="a170c-122">Insight and Analytics nodes</span><span class="sxs-lookup"><span data-stu-id="a170c-122">Insight and Analytics nodes</span></span>
    - <span data-ttu-id="a170c-123">Automation and Control nodes</span><span class="sxs-lookup"><span data-stu-id="a170c-123">Automation and Control nodes</span></span>
    - <span data-ttu-id="a170c-124">Security nodes</span><span class="sxs-lookup"><span data-stu-id="a170c-124">Security nodes</span></span>
- <span data-ttu-id="a170c-125">Performance</span><span class="sxs-lookup"><span data-stu-id="a170c-125">Performance</span></span>
    - <span data-ttu-id="a170c-126">Time taken to collect and index data</span><span class="sxs-lookup"><span data-stu-id="a170c-126">Time taken to collect and index data</span></span>
- <span data-ttu-id="a170c-127">List of queries</span><span class="sxs-lookup"><span data-stu-id="a170c-127">List of queries</span></span>

## <a name="understanding-nodes-for-oms-offers"></a><span data-ttu-id="a170c-128">Understanding nodes for OMS offers</span><span class="sxs-lookup"><span data-stu-id="a170c-128">Understanding nodes for OMS offers</span></span>

<span data-ttu-id="a170c-129">If you are on the *per node (OMS)* pricing tier, then you are charged based on the number of nodes and solutions you have enabled.</span><span class="sxs-lookup"><span data-stu-id="a170c-129">If you are on the *per node (OMS)* pricing tier, then you are charged based on the number of nodes and solutions you have enabled.</span></span> <span data-ttu-id="a170c-130">You can see how many nodes of each offer are being used in the *offerings* section of the usage dashboard.</span><span class="sxs-lookup"><span data-stu-id="a170c-130">You can see how many nodes of each offer are being used in the *offerings* section of the usage dashboard.</span></span>

![usage dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/log-analytics-usage-offerings.png)

## <a name="to-work-with-usage-data"></a><span data-ttu-id="a170c-132">To work with usage data</span><span class="sxs-lookup"><span data-stu-id="a170c-132">To work with usage data</span></span>
1. <span data-ttu-id="a170c-133">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com) using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a170c-133">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com) using your Azure subscription.</span></span>
2. <span data-ttu-id="a170c-134">On the **Hub** menu, click **More services** and in the list of resources, type **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="a170c-134">On the **Hub** menu, click **More services** and in the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="a170c-135">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="a170c-135">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="a170c-136">Click **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="a170c-136">Click **Log Analytics**.</span></span>  
    <span data-ttu-id="a170c-137">![Azure hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/hub.png)</span><span class="sxs-lookup"><span data-stu-id="a170c-137">![Azure hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/hub.png)</span></span>
3. <span data-ttu-id="a170c-138">The **Log Analytics** dashboard shows a list of your workspaces.</span><span class="sxs-lookup"><span data-stu-id="a170c-138">The **Log Analytics** dashboard shows a list of your workspaces.</span></span> <span data-ttu-id="a170c-139">Select a workspace.</span><span class="sxs-lookup"><span data-stu-id="a170c-139">Select a workspace.</span></span>
4. <span data-ttu-id="a170c-140">In the *workspace* dashboard, click **Log Analytics usage**.</span><span class="sxs-lookup"><span data-stu-id="a170c-140">In the *workspace* dashboard, click **Log Analytics usage**.</span></span>
5. <span data-ttu-id="a170c-141">On the **Log Analytics Usage** dashboard, click **Time: Last 24 hours** to change the time interval.</span><span class="sxs-lookup"><span data-stu-id="a170c-141">On the **Log Analytics Usage** dashboard, click **Time: Last 24 hours** to change the time interval.</span></span>  
    <span data-ttu-id="a170c-142">![time interval](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/time.png)</span><span class="sxs-lookup"><span data-stu-id="a170c-142">![time interval](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/time.png)</span></span>
6. <span data-ttu-id="a170c-143">View the usage category blades that show areas you’re interested in.</span><span class="sxs-lookup"><span data-stu-id="a170c-143">View the usage category blades that show areas you’re interested in.</span></span> <span data-ttu-id="a170c-144">Choose a blade and then click an item in it to view more details in [Log Search](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="a170c-144">Choose a blade and then click an item in it to view more details in [Log Search](log-analytics-log-searches.md).</span></span>  
    <span data-ttu-id="a170c-145">![example data usage blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/blade.png)</span><span class="sxs-lookup"><span data-stu-id="a170c-145">![example data usage blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/blade.png)</span></span>
7. <span data-ttu-id="a170c-146">On the Log Search dashboard, review the results that are returned from the search.</span><span class="sxs-lookup"><span data-stu-id="a170c-146">On the Log Search dashboard, review the results that are returned from the search.</span></span>  
    ![example usage log search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/usage-log-search.png)


## <a name="next-steps"></a><span data-ttu-id="a170c-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="a170c-148">Next steps</span></span>
* <span data-ttu-id="a170c-149">See [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed information that is gathered and sent to OMS by features and solutions.</span><span class="sxs-lookup"><span data-stu-id="a170c-149">See [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed information that is gathered and sent to OMS by features and solutions.</span></span>






