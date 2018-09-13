---
title: Supported data destinations and outputs available with Azure Machine Learning data preparation  | Microsoft Docs
description: This document provides a complete list of supported destinations and outputs available for Azure Machine Learning data preparation
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: 123328010758eea6e7eadce29440e204f91dcef6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870554"
---
# <a name="supported-data-exports-for-this-preview"></a><span data-ttu-id="03960-103">Supported data exports for this preview</span><span class="sxs-lookup"><span data-stu-id="03960-103">Supported data exports for this preview</span></span> 
<span data-ttu-id="03960-104">It is possible to export to several different formats.</span><span class="sxs-lookup"><span data-stu-id="03960-104">It is possible to export to several different formats.</span></span> <span data-ttu-id="03960-105">You can use these formats to retain the intermediate results of data preparation before you integrate the results into the rest of the Machine Learning workflow.</span><span class="sxs-lookup"><span data-stu-id="03960-105">You can use these formats to retain the intermediate results of data preparation before you integrate the results into the rest of the Machine Learning workflow.</span></span>

## <a name="types"></a><span data-ttu-id="03960-106">Types</span><span class="sxs-lookup"><span data-stu-id="03960-106">Types</span></span> 
### <a name="csv-file"></a><span data-ttu-id="03960-107">CSV file</span><span class="sxs-lookup"><span data-stu-id="03960-107">CSV file</span></span> 
<span data-ttu-id="03960-108">Write a comma-separated-value file to storage.</span><span class="sxs-lookup"><span data-stu-id="03960-108">Write a comma-separated-value file to storage.</span></span>

#### <a name="options"></a><span data-ttu-id="03960-109">Options</span><span class="sxs-lookup"><span data-stu-id="03960-109">Options</span></span>
- <span data-ttu-id="03960-110">Line endings</span><span class="sxs-lookup"><span data-stu-id="03960-110">Line endings</span></span>
- <span data-ttu-id="03960-111">Replace nulls with</span><span class="sxs-lookup"><span data-stu-id="03960-111">Replace nulls with</span></span>
- <span data-ttu-id="03960-112">Replace errors with</span><span class="sxs-lookup"><span data-stu-id="03960-112">Replace errors with</span></span> 
- <span data-ttu-id="03960-113">Separator</span><span class="sxs-lookup"><span data-stu-id="03960-113">Separator</span></span>


### <a name="parquet"></a><span data-ttu-id="03960-114">Parquet</span><span class="sxs-lookup"><span data-stu-id="03960-114">Parquet</span></span> 
<span data-ttu-id="03960-115">Write a dataset to storage as Parquet.</span><span class="sxs-lookup"><span data-stu-id="03960-115">Write a dataset to storage as Parquet.</span></span>

<span data-ttu-id="03960-116">Parquet as a format can take various forms in storage.</span><span class="sxs-lookup"><span data-stu-id="03960-116">Parquet as a format can take various forms in storage.</span></span> <span data-ttu-id="03960-117">For smaller datasets, a single .parquet file is sometimes used.</span><span class="sxs-lookup"><span data-stu-id="03960-117">For smaller datasets, a single .parquet file is sometimes used.</span></span> <span data-ttu-id="03960-118">Various Python libraries support reading and writing to single .parquet files.</span><span class="sxs-lookup"><span data-stu-id="03960-118">Various Python libraries support reading and writing to single .parquet files.</span></span> 

<span data-ttu-id="03960-119">Currently, Azure Machine Learning Workbench relies on the PyArrow Python library for writing out Parquet during local interactive use.</span><span class="sxs-lookup"><span data-stu-id="03960-119">Currently, Azure Machine Learning Workbench relies on the PyArrow Python library for writing out Parquet during local interactive use.</span></span> <span data-ttu-id="03960-120">This means that single-file Parquet is currently the only Parquet output format that's supported during local interactive use.</span><span class="sxs-lookup"><span data-stu-id="03960-120">This means that single-file Parquet is currently the only Parquet output format that's supported during local interactive use.</span></span>

<span data-ttu-id="03960-121">During scale-out runs (on Spark), Azure Machine Learning Workbench relies on Spark's Parquet reading and writing capabilities.</span><span class="sxs-lookup"><span data-stu-id="03960-121">During scale-out runs (on Spark), Azure Machine Learning Workbench relies on Spark's Parquet reading and writing capabilities.</span></span> <span data-ttu-id="03960-122">Spark's default output format for Parquet (currently the only one supported) is similar in structure to a Hive dataset.</span><span class="sxs-lookup"><span data-stu-id="03960-122">Spark's default output format for Parquet (currently the only one supported) is similar in structure to a Hive dataset.</span></span> <span data-ttu-id="03960-123">This means that a folder contains many .parquet files that are each a smaller partition of a larger dataset.</span><span class="sxs-lookup"><span data-stu-id="03960-123">This means that a folder contains many .parquet files that are each a smaller partition of a larger dataset.</span></span> 

#### <a name="caveats"></a><span data-ttu-id="03960-124">Caveats</span><span class="sxs-lookup"><span data-stu-id="03960-124">Caveats</span></span> 
<span data-ttu-id="03960-125">Parquet as a format is relatively young and has some implementation inconsistencies across different libraries.</span><span class="sxs-lookup"><span data-stu-id="03960-125">Parquet as a format is relatively young and has some implementation inconsistencies across different libraries.</span></span> <span data-ttu-id="03960-126">For instance, Spark places restrictions on which characters are valid in column names when writing out to Parquet.</span><span class="sxs-lookup"><span data-stu-id="03960-126">For instance, Spark places restrictions on which characters are valid in column names when writing out to Parquet.</span></span> <span data-ttu-id="03960-127">PyArrow does not do this.</span><span class="sxs-lookup"><span data-stu-id="03960-127">PyArrow does not do this.</span></span> <span data-ttu-id="03960-128">The following characters can't be in a column name:</span><span class="sxs-lookup"><span data-stu-id="03960-128">The following characters can't be in a column name:</span></span> 
- <span data-ttu-id="03960-129">,</span><span class="sxs-lookup"><span data-stu-id="03960-129">,</span></span>
- <span data-ttu-id="03960-130">;</span><span class="sxs-lookup"><span data-stu-id="03960-130">;</span></span>
- {}
- <span data-ttu-id="03960-131">()</span><span class="sxs-lookup"><span data-stu-id="03960-131">()</span></span>
- <span data-ttu-id="03960-132">\\n</span><span class="sxs-lookup"><span data-stu-id="03960-132">\\n</span></span>
- <span data-ttu-id="03960-133">\\t</span><span class="sxs-lookup"><span data-stu-id="03960-133">\\t</span></span>
- =

>[!NOTE]
>- <span data-ttu-id="03960-134">To ensure compatibility with Spark, any time you write data  to Parquet, occurrences of these characters in column names are replaced with and underscore ( _ ).</span><span class="sxs-lookup"><span data-stu-id="03960-134">To ensure compatibility with Spark, any time you write data  to Parquet, occurrences of these characters in column names are replaced with and underscore ( _ ).</span></span>
>- <span data-ttu-id="03960-135">To ensure consistency across local and scale-out runs, any data written to Parquet, via the app, Python, or Spark, has its column names sanitized to ensure Spark compatibility.</span><span class="sxs-lookup"><span data-stu-id="03960-135">To ensure consistency across local and scale-out runs, any data written to Parquet, via the app, Python, or Spark, has its column names sanitized to ensure Spark compatibility.</span></span> <span data-ttu-id="03960-136">To ensure expected column names when writing to Parquet characters in Spark, remove the invalid set from the columns before writing them out.</span><span class="sxs-lookup"><span data-stu-id="03960-136">To ensure expected column names when writing to Parquet characters in Spark, remove the invalid set from the columns before writing them out.</span></span>



## <a name="locations"></a><span data-ttu-id="03960-137">Locations</span><span class="sxs-lookup"><span data-stu-id="03960-137">Locations</span></span> 
### <a name="local"></a><span data-ttu-id="03960-138">Local</span><span class="sxs-lookup"><span data-stu-id="03960-138">Local</span></span> 
<span data-ttu-id="03960-139">Local hard drive or mapped network storage location.</span><span class="sxs-lookup"><span data-stu-id="03960-139">Local hard drive or mapped network storage location.</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="03960-140">Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="03960-140">Azure Blob storage</span></span>
<span data-ttu-id="03960-141">Azure Blob storage requires an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="03960-141">Azure Blob storage requires an Azure subscription.</span></span>

