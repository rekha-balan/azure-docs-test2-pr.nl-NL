---
title: How to work with 'big data' data sources in Azure Data Catalog
description: How-to article highlighting patterns for using Azure Data Catalog  with 'big data' data sources, including Azure Blob Storage, Azure Data Lake, and Hadoop HDFS.
services: data-catalog
author: steelanddata
ms.author: maroche
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.topic: conceptual
ms.date: 01/18/2018
ms.openlocfilehash: d59b637d1c5ad2335492883503e738a80071a8dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803197"
---
# <a name="how-to-work-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="a82d5-103">How to work with big data sources in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="a82d5-103">How to work with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="a82d5-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="a82d5-104">Introduction</span></span>
<span data-ttu-id="a82d5-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span><span class="sxs-lookup"><span data-stu-id="a82d5-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="a82d5-106">It is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data sources, including big data.</span><span class="sxs-lookup"><span data-stu-id="a82d5-106">It is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="a82d5-107">**Azure Data Catalog** supports the registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span><span class="sxs-lookup"><span data-stu-id="a82d5-107">**Azure Data Catalog** supports the registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="a82d5-108">The semi-structured nature of these data sources provides great flexibility.</span><span class="sxs-lookup"><span data-stu-id="a82d5-108">The semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="a82d5-109">However, to get the most value from registering them with **Azure Data Catalog**, users must consider how the data sources are organized.</span><span class="sxs-lookup"><span data-stu-id="a82d5-109">However, to get the most value from registering them with **Azure Data Catalog**, users must consider how the data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="a82d5-110">Directories as logical data sets</span><span class="sxs-lookup"><span data-stu-id="a82d5-110">Directories as logical data sets</span></span>
<span data-ttu-id="a82d5-111">A common pattern for organizing big data sources is to treat directories as logical data sets.</span><span class="sxs-lookup"><span data-stu-id="a82d5-111">A common pattern for organizing big data sources is to treat directories as logical data sets.</span></span> <span data-ttu-id="a82d5-112">Top-level directories are used to define a data set, while subfolders define partitions, and the files they contain store the data itself.</span><span class="sxs-lookup"><span data-stu-id="a82d5-112">Top-level directories are used to define a data set, while subfolders define partitions, and the files they contain store the data itself.</span></span>

<span data-ttu-id="a82d5-113">An example of this pattern might be:</span><span class="sxs-lookup"><span data-stu-id="a82d5-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="a82d5-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span><span class="sxs-lookup"><span data-stu-id="a82d5-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="a82d5-115">Each of these folders contains data files that are organized by year and month into subfolders.</span><span class="sxs-lookup"><span data-stu-id="a82d5-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="a82d5-116">Each of these folders could potentially contain hundreds or thousands of files.</span><span class="sxs-lookup"><span data-stu-id="a82d5-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="a82d5-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span><span class="sxs-lookup"><span data-stu-id="a82d5-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="a82d5-118">Instead, register the directories that represent the data sets that be meaningful to the users working with the data.</span><span class="sxs-lookup"><span data-stu-id="a82d5-118">Instead, register the directories that represent the data sets that be meaningful to the users working with the data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="a82d5-119">Reference data files</span><span class="sxs-lookup"><span data-stu-id="a82d5-119">Reference data files</span></span>
<span data-ttu-id="a82d5-120">A complementary pattern is to store reference data sets as individual files.</span><span class="sxs-lookup"><span data-stu-id="a82d5-120">A complementary pattern is to store reference data sets as individual files.</span></span> <span data-ttu-id="a82d5-121">These data sets may be thought of as the 'small' side of big data, and are often similar to dimensions in an analytical data model.</span><span class="sxs-lookup"><span data-stu-id="a82d5-121">These data sets may be thought of as the 'small' side of big data, and are often similar to dimensions in an analytical data model.</span></span> <span data-ttu-id="a82d5-122">Reference data files contain records that are used to provide context for the bulk of the data files stored elsewhere in the big data store.</span><span class="sxs-lookup"><span data-stu-id="a82d5-122">Reference data files contain records that are used to provide context for the bulk of the data files stored elsewhere in the big data store.</span></span>

<span data-ttu-id="a82d5-123">An example of this pattern might be:</span><span class="sxs-lookup"><span data-stu-id="a82d5-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="a82d5-124">When an analyst or data scientist is working with the data contained in the larger directory structures, the data in these reference files can be used to provide more detailed information for entities that are referred to only by name or ID in the larger data set.</span><span class="sxs-lookup"><span data-stu-id="a82d5-124">When an analyst or data scientist is working with the data contained in the larger directory structures, the data in these reference files can be used to provide more detailed information for entities that are referred to only by name or ID in the larger data set.</span></span>

<span data-ttu-id="a82d5-125">In this pattern, it makes sense to register the individual reference data files with **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="a82d5-125">In this pattern, it makes sense to register the individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="a82d5-126">Each file represents a data set, and each one can be annotated and discovered individually.</span><span class="sxs-lookup"><span data-stu-id="a82d5-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="a82d5-127">Alternate patterns</span><span class="sxs-lookup"><span data-stu-id="a82d5-127">Alternate patterns</span></span>
<span data-ttu-id="a82d5-128">The patterns described in the preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span><span class="sxs-lookup"><span data-stu-id="a82d5-128">The patterns described in the preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="a82d5-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering the files and directories that represent the data sets that are of value to others within your organization.</span><span class="sxs-lookup"><span data-stu-id="a82d5-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering the files and directories that represent the data sets that are of value to others within your organization.</span></span> <span data-ttu-id="a82d5-130">Registering all files and directories can clutter the catalog, making it harder for users to find what they need.</span><span class="sxs-lookup"><span data-stu-id="a82d5-130">Registering all files and directories can clutter the catalog, making it harder for users to find what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="a82d5-131">Summary</span><span class="sxs-lookup"><span data-stu-id="a82d5-131">Summary</span></span>
<span data-ttu-id="a82d5-132">Registering data sources with **Azure Data Catalog** makes them easier to discover and understand.</span><span class="sxs-lookup"><span data-stu-id="a82d5-132">Registering data sources with **Azure Data Catalog** makes them easier to discover and understand.</span></span> <span data-ttu-id="a82d5-133">By registering and annotating the big data files and directories that represent logical data sets, you can help users find and use the big data sources they need.</span><span class="sxs-lookup"><span data-stu-id="a82d5-133">By registering and annotating the big data files and directories that represent logical data sets, you can help users find and use the big data sources they need.</span></span>
