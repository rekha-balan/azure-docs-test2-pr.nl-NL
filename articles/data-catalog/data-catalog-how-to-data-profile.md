---
title: How to Data profile data sources
description: How-to article highlighting how to include table- and column-level data profiles when registering data sources in Azure Data Catalog, and how to use data profiles to understand data sources.
services: data-catalog
documentationcenter: ''
author: spelluru
manager: NA
editor: ''
tags: ''
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/19/2017
ms.author: spelluru
ms.openlocfilehash: d23d9acb55d4ea546d919ed66a043a31b16416e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549152"
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="9ab16-103">Data profile data sources</span><span class="sxs-lookup"><span data-stu-id="9ab16-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="9ab16-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="9ab16-104">Introduction</span></span>
<span data-ttu-id="9ab16-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span><span class="sxs-lookup"><span data-stu-id="9ab16-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="9ab16-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span><span class="sxs-lookup"><span data-stu-id="9ab16-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="9ab16-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span><span class="sxs-lookup"><span data-stu-id="9ab16-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="9ab16-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span><span class="sxs-lookup"><span data-stu-id="9ab16-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="9ab16-109">It's easy to include a profile of your data assets.</span><span class="sxs-lookup"><span data-stu-id="9ab16-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="9ab16-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span><span class="sxs-lookup"><span data-stu-id="9ab16-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="9ab16-111">What is Data Profiling</span><span class="sxs-lookup"><span data-stu-id="9ab16-111">What is Data Profiling</span></span>
<span data-ttu-id="9ab16-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span><span class="sxs-lookup"><span data-stu-id="9ab16-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="9ab16-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span><span class="sxs-lookup"><span data-stu-id="9ab16-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="9ab16-114">The following data sources support data profiling:</span><span class="sxs-lookup"><span data-stu-id="9ab16-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="9ab16-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span><span class="sxs-lookup"><span data-stu-id="9ab16-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="9ab16-116">Oracle tables and views</span><span class="sxs-lookup"><span data-stu-id="9ab16-116">Oracle tables and views</span></span>
* <span data-ttu-id="9ab16-117">Teradata tables and views</span><span class="sxs-lookup"><span data-stu-id="9ab16-117">Teradata tables and views</span></span>
* <span data-ttu-id="9ab16-118">Hive tables</span><span class="sxs-lookup"><span data-stu-id="9ab16-118">Hive tables</span></span>

<span data-ttu-id="9ab16-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span><span class="sxs-lookup"><span data-stu-id="9ab16-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="9ab16-120">Can it be used to solve my business problem?</span><span class="sxs-lookup"><span data-stu-id="9ab16-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="9ab16-121">Does the data conform to particular standards or patterns?</span><span class="sxs-lookup"><span data-stu-id="9ab16-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="9ab16-122">What are some of the anomalies of the data source?</span><span class="sxs-lookup"><span data-stu-id="9ab16-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="9ab16-123">What are possible challenges of integrating this data into my application?</span><span class="sxs-lookup"><span data-stu-id="9ab16-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="9ab16-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span><span class="sxs-lookup"><span data-stu-id="9ab16-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="9ab16-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="9ab16-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="9ab16-126">How to include a data profile when registering a data source</span><span class="sxs-lookup"><span data-stu-id="9ab16-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="9ab16-127">It's easy to include a profile of your data source.</span><span class="sxs-lookup"><span data-stu-id="9ab16-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="9ab16-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span><span class="sxs-lookup"><span data-stu-id="9ab16-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="9ab16-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9ab16-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="9ab16-130">Filtering on data assets that include data profiles</span><span class="sxs-lookup"><span data-stu-id="9ab16-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="9ab16-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span><span class="sxs-lookup"><span data-stu-id="9ab16-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab16-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span><span class="sxs-lookup"><span data-stu-id="9ab16-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="9ab16-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span><span class="sxs-lookup"><span data-stu-id="9ab16-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="9ab16-134">Viewing data profile information</span><span class="sxs-lookup"><span data-stu-id="9ab16-134">Viewing data profile information</span></span>
<span data-ttu-id="9ab16-135">Once you find a suitable data source with a profile, you can view the data profile details.</span><span class="sxs-lookup"><span data-stu-id="9ab16-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="9ab16-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span><span class="sxs-lookup"><span data-stu-id="9ab16-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="9ab16-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span><span class="sxs-lookup"><span data-stu-id="9ab16-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="9ab16-138">Object data profile</span><span class="sxs-lookup"><span data-stu-id="9ab16-138">Object data profile</span></span>
* <span data-ttu-id="9ab16-139">Number of rows</span><span class="sxs-lookup"><span data-stu-id="9ab16-139">Number of rows</span></span>
* <span data-ttu-id="9ab16-140">Table size</span><span class="sxs-lookup"><span data-stu-id="9ab16-140">Table size</span></span>
* <span data-ttu-id="9ab16-141">When the object was last updated</span><span class="sxs-lookup"><span data-stu-id="9ab16-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="9ab16-142">Column data profile</span><span class="sxs-lookup"><span data-stu-id="9ab16-142">Column data profile</span></span>
* <span data-ttu-id="9ab16-143">Column data type</span><span class="sxs-lookup"><span data-stu-id="9ab16-143">Column data type</span></span>
* <span data-ttu-id="9ab16-144">Number of distinct values</span><span class="sxs-lookup"><span data-stu-id="9ab16-144">Number of distinct values</span></span>
* <span data-ttu-id="9ab16-145">Number of rows with NULL values</span><span class="sxs-lookup"><span data-stu-id="9ab16-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="9ab16-146">Minimum, maximum, average, and standard deviation for column values</span><span class="sxs-lookup"><span data-stu-id="9ab16-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="9ab16-147">Summary</span><span class="sxs-lookup"><span data-stu-id="9ab16-147">Summary</span></span>
<span data-ttu-id="9ab16-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span><span class="sxs-lookup"><span data-stu-id="9ab16-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="9ab16-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span><span class="sxs-lookup"><span data-stu-id="9ab16-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="9ab16-150">See Also</span><span class="sxs-lookup"><span data-stu-id="9ab16-150">See Also</span></span>
* [<span data-ttu-id="9ab16-151">How to register data sources</span><span class="sxs-lookup"><span data-stu-id="9ab16-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="9ab16-152">Get started with Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="9ab16-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)


