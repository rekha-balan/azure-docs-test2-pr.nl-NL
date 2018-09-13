---
title: Viewing and analyzing data in Azure Log Analytics | Microsoft Docs
description: This article describes the portals that you can use in Azure Log Analytics to create and edit log searches.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/20/2018
ms.author: magoedte; bwren
ms.component: na
ms.openlocfilehash: 386aad94461fa3f2ceafb7564342797eefa2f086
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866499"
---
# <a name="viewing-and-analyzing-data-in-log-analytics"></a><span data-ttu-id="80e5c-103">Viewing and analyzing data in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="80e5c-103">Viewing and analyzing data in Log Analytics</span></span>
<span data-ttu-id="80e5c-104">There are two options available in the Azure portal for analyzing data stored in Log analytics and for creating queries for ad hoc analysis.</span><span class="sxs-lookup"><span data-stu-id="80e5c-104">There are two options available in the Azure portal for analyzing data stored in Log analytics and for creating queries for ad hoc analysis.</span></span> <span data-ttu-id="80e5c-105">The queries that you create using these portals can be used for other features such as alerts and dashboards.</span><span class="sxs-lookup"><span data-stu-id="80e5c-105">The queries that you create using these portals can be used for other features such as alerts and dashboards.</span></span>

## <a name="log-analytics-page-preview"></a><span data-ttu-id="80e5c-106">Log Analytics page (preview)</span><span class="sxs-lookup"><span data-stu-id="80e5c-106">Log Analytics page (preview)</span></span>
<span data-ttu-id="80e5c-107">Open the Log Analytics page from **Logs (preview)** in the Log Analytics menu.</span><span class="sxs-lookup"><span data-stu-id="80e5c-107">Open the Log Analytics page from **Logs (preview)** in the Log Analytics menu.</span></span> <span data-ttu-id="80e5c-108">This is a new experience for working with log data and creating queries.</span><span class="sxs-lookup"><span data-stu-id="80e5c-108">This is a new experience for working with log data and creating queries.</span></span> <span data-ttu-id="80e5c-109">You can get an introduction to this portal and inspect its features at [Get started with the Log Analytics page in the Azure portal](query-language/get-started-analytics-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80e5c-109">You can get an introduction to this portal and inspect its features at [Get started with the Log Analytics page in the Azure portal](query-language/get-started-analytics-portal.md).</span></span>

<span data-ttu-id="80e5c-110">The Log Analytics page provides the following improvements over the [Log search](#log-search) experience.</span><span class="sxs-lookup"><span data-stu-id="80e5c-110">The Log Analytics page provides the following improvements over the [Log search](#log-search) experience.</span></span>

* <span data-ttu-id="80e5c-111">Multiple tabs – create separate tabs to work with multiple queries.</span><span class="sxs-lookup"><span data-stu-id="80e5c-111">Multiple tabs – create separate tabs to work with multiple queries.</span></span>
* <span data-ttu-id="80e5c-112">Rich visualizations – variety of charting options.</span><span class="sxs-lookup"><span data-stu-id="80e5c-112">Rich visualizations – variety of charting options.</span></span>
* <span data-ttu-id="80e5c-113">Improved Intellisense and language auto-completion.</span><span class="sxs-lookup"><span data-stu-id="80e5c-113">Improved Intellisense and language auto-completion.</span></span>
* <span data-ttu-id="80e5c-114">Syntax highlighting – improves readability of queries.</span><span class="sxs-lookup"><span data-stu-id="80e5c-114">Syntax highlighting – improves readability of queries.</span></span> 
* <span data-ttu-id="80e5c-115">Query explorer – access saved queries and functions.</span><span class="sxs-lookup"><span data-stu-id="80e5c-115">Query explorer – access saved queries and functions.</span></span>
* <span data-ttu-id="80e5c-116">Schema view – review the structure of your data to assist in writing queries.</span><span class="sxs-lookup"><span data-stu-id="80e5c-116">Schema view – review the structure of your data to assist in writing queries.</span></span>
* <span data-ttu-id="80e5c-117">Share – create links to queries, or pin queries to any shared Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="80e5c-117">Share – create links to queries, or pin queries to any shared Azure dashboard.</span></span>
* <span data-ttu-id="80e5c-118">Smart Analytics - identifies spikes in your charts and a quick analysis of the cause.</span><span class="sxs-lookup"><span data-stu-id="80e5c-118">Smart Analytics - identifies spikes in your charts and a quick analysis of the cause.</span></span>
* <span data-ttu-id="80e5c-119">Column selection – sort and group columns in the query results.</span><span class="sxs-lookup"><span data-stu-id="80e5c-119">Column selection – sort and group columns in the query results.</span></span>

> [!NOTE]
> <span data-ttu-id="80e5c-120">The Log Analytics page has the same functionality as the Advanced Analytics portal which is an external tool outside of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="80e5c-120">The Log Analytics page has the same functionality as the Advanced Analytics portal which is an external tool outside of the Azure portal.</span></span> <span data-ttu-id="80e5c-121">The Advanced Analytics portal is still available, but links and other references to it in the Azure portal are being replaced with this new page.</span><span class="sxs-lookup"><span data-stu-id="80e5c-121">The Advanced Analytics portal is still available, but links and other references to it in the Azure portal are being replaced with this new page.</span></span>

![Advanced Analytics portal](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


### <a name="firewall-requirements"></a><span data-ttu-id="80e5c-123">Firewall requirements</span><span class="sxs-lookup"><span data-stu-id="80e5c-123">Firewall requirements</span></span>
<span data-ttu-id="80e5c-124">Your browser requires access to the following addresses to access the Log Analytics page and the Advanced Analytics portal.</span><span class="sxs-lookup"><span data-stu-id="80e5c-124">Your browser requires access to the following addresses to access the Log Analytics page and the Advanced Analytics portal.</span></span>  <span data-ttu-id="80e5c-125">If your browser is accessing the Azure portal through a firewall, you must enable access to these addresses.</span><span class="sxs-lookup"><span data-stu-id="80e5c-125">If your browser is accessing the Azure portal through a firewall, you must enable access to these addresses.</span></span>

| <span data-ttu-id="80e5c-126">Uri</span><span class="sxs-lookup"><span data-stu-id="80e5c-126">Uri</span></span> | <span data-ttu-id="80e5c-127">IP</span><span class="sxs-lookup"><span data-stu-id="80e5c-127">IP</span></span> | <span data-ttu-id="80e5c-128">Ports</span><span class="sxs-lookup"><span data-stu-id="80e5c-128">Ports</span></span> |
|:---|:---|:---|
| <span data-ttu-id="80e5c-129">portal.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="80e5c-129">portal.loganalytics.io</span></span> | <span data-ttu-id="80e5c-130">Dynamic</span><span class="sxs-lookup"><span data-stu-id="80e5c-130">Dynamic</span></span> | <span data-ttu-id="80e5c-131">80,443</span><span class="sxs-lookup"><span data-stu-id="80e5c-131">80,443</span></span> |
| <span data-ttu-id="80e5c-132">api.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="80e5c-132">api.loganalytics.io</span></span>    | <span data-ttu-id="80e5c-133">Dynamic</span><span class="sxs-lookup"><span data-stu-id="80e5c-133">Dynamic</span></span> | <span data-ttu-id="80e5c-134">80,443</span><span class="sxs-lookup"><span data-stu-id="80e5c-134">80,443</span></span> |
| <span data-ttu-id="80e5c-135">docs.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="80e5c-135">docs.loganalytics.io</span></span>   | <span data-ttu-id="80e5c-136">Dynamic</span><span class="sxs-lookup"><span data-stu-id="80e5c-136">Dynamic</span></span> | <span data-ttu-id="80e5c-137">80,443</span><span class="sxs-lookup"><span data-stu-id="80e5c-137">80,443</span></span> |


## <a name="log-search"></a><span data-ttu-id="80e5c-138">Log search</span><span class="sxs-lookup"><span data-stu-id="80e5c-138">Log search</span></span>
<span data-ttu-id="80e5c-139">Open the Log search page from **Logs** in the Log Analytics menu or from **Log Analytics** in the Azure Monitor menu.</span><span class="sxs-lookup"><span data-stu-id="80e5c-139">Open the Log search page from **Logs** in the Log Analytics menu or from **Log Analytics** in the Azure Monitor menu.</span></span> <span data-ttu-id="80e5c-140">This is suitable for analyzing log data using basic queries.</span><span class="sxs-lookup"><span data-stu-id="80e5c-140">This is suitable for analyzing log data using basic queries.</span></span> <span data-ttu-id="80e5c-141">It provides multiple features for editing queries without having a full knowledge of the query language.</span><span class="sxs-lookup"><span data-stu-id="80e5c-141">It provides multiple features for editing queries without having a full knowledge of the query language.</span></span>  <span data-ttu-id="80e5c-142">You can get a summary of these features in [Create log searches in Azure Log Analytics using Log Search](log-analytics-log-search-log-search-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80e5c-142">You can get a summary of these features in [Create log searches in Azure Log Analytics using Log Search](log-analytics-log-search-log-search-portal.md).</span></span> 


![Log Search page](media/log-analytics-log-search-portals/log-search-portal.png)


## <a name="next-steps"></a><span data-ttu-id="80e5c-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="80e5c-144">Next steps</span></span>

- <span data-ttu-id="80e5c-145">Walk through a [tutorial using Log Search](log-analytics-tutorial-viewdata.md) to learn how to create queries using the query language</span><span class="sxs-lookup"><span data-stu-id="80e5c-145">Walk through a [tutorial using Log Search](log-analytics-tutorial-viewdata.md) to learn how to create queries using the query language</span></span>
- <span data-ttu-id="80e5c-146">Walk through a [lesson using the Advanced Analytics portal](query-language/get-started-analytics-portal.md) which provides the same experience as the Log Analytics page.</span><span class="sxs-lookup"><span data-stu-id="80e5c-146">Walk through a [lesson using the Advanced Analytics portal](query-language/get-started-analytics-portal.md) which provides the same experience as the Log Analytics page.</span></span>

