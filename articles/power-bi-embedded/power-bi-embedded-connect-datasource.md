---
title: Microsoft Power BI Embedded - Connecting to a data source
description: Power BI Embedded, connect to data sources
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550203"
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="0d7ec-103">Connect to a data source</span><span class="sxs-lookup"><span data-stu-id="0d7ec-103">Connect to a data source</span></span>
<span data-ttu-id="0d7ec-104">With **Power BI Embedded**, you can embed reports into your own app.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="0d7ec-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="0d7ec-106">Here are the differences between using **Import** and **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="0d7ec-107">Import</span><span class="sxs-lookup"><span data-stu-id="0d7ec-107">Import</span></span> | <span data-ttu-id="0d7ec-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="0d7ec-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="0d7ec-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="0d7ec-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="0d7ec-111">Only *tables and columns* are imported or copied into the report's dataset.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="0d7ec-112">You always view the most current data.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-112">You always view the most current data.</span></span> |

<span data-ttu-id="0d7ec-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="0d7ec-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="0d7ec-115">This means you cannot use DirectQuery with on-premises data sources.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="0d7ec-116">Supported data sources</span><span class="sxs-lookup"><span data-stu-id="0d7ec-116">Supported data sources</span></span>

<span data-ttu-id="0d7ec-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="0d7ec-117">**DirectQuery**</span></span>
* <span data-ttu-id="0d7ec-118">Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="0d7ec-118">Azure SQL database</span></span>
* <span data-ttu-id="0d7ec-119">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0d7ec-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="0d7ec-120">**Import**</span><span class="sxs-lookup"><span data-stu-id="0d7ec-120">**Import**</span></span>

<span data-ttu-id="0d7ec-121">You can import using all of the available data sources within Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="0d7ec-122">You will **not** be able to refresh that data within Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="0d7ec-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="0d7ec-124">This is due to no available gateway.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="0d7ec-125">Benefits of using DirectQuery</span><span class="sxs-lookup"><span data-stu-id="0d7ec-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="0d7ec-126">There are two primary benefits when using **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="0d7ec-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="0d7ec-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="0d7ec-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="0d7ec-129">By contrast, **DirectQuery** reports always use current data.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="0d7ec-130">Limitations of DirectQuery</span><span class="sxs-lookup"><span data-stu-id="0d7ec-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="0d7ec-131">There are a few limitations to using **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="0d7ec-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="0d7ec-132">All tables must come from a single database.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="0d7ec-133">If the query is overly complex, an error will occur.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="0d7ec-134">To remedy the error you must refactor the query so it is less complex.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="0d7ec-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="0d7ec-136">Relationship filtering is limited to a single direction, rather than both directions.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="0d7ec-137">You cannot change the data type of a column.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="0d7ec-138">By default, limitations are placed on DAX expressions allowed in measures.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="0d7ec-139">See [DirectQuery and measures](#measures).</span><span class="sxs-lookup"><span data-stu-id="0d7ec-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="0d7ec-140">DirectQuery and measures</span><span class="sxs-lookup"><span data-stu-id="0d7ec-140">DirectQuery and measures</span></span>
<span data-ttu-id="0d7ec-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="0d7ec-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="0d7ec-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="0d7ec-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="0d7ec-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span><span class="sxs-lookup"><span data-stu-id="0d7ec-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="0d7ec-146">See Also</span><span class="sxs-lookup"><span data-stu-id="0d7ec-146">See Also</span></span>
* [<span data-ttu-id="0d7ec-147">Get started with Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0d7ec-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="0d7ec-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0d7ec-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="0d7ec-149">More questions?</span><span class="sxs-lookup"><span data-stu-id="0d7ec-149">More questions?</span></span> [<span data-ttu-id="0d7ec-150">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="0d7ec-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

