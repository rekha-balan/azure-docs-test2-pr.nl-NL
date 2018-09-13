---
title: Example transform data flow transformations possible with Azure Machine Learning Data Preparation  | Microsoft Docs
description: This document provides a set of examples of transform data flow transforms possible with Azure Machine Learning data preparation
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
ms.openlocfilehash: ca780b51973a960caec3b9b7a80c8ba5621b5a0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869554"
---
# <a name="sample-of-custom-data-flow-transforms-python"></a><span data-ttu-id="5709d-103">Sample of custom data flow transforms (Python)</span><span class="sxs-lookup"><span data-stu-id="5709d-103">Sample of custom data flow transforms (Python)</span></span> 
<span data-ttu-id="5709d-104">The name of the transform in the menu is **Transform Dataflow (Script)**.</span><span class="sxs-lookup"><span data-stu-id="5709d-104">The name of the transform in the menu is **Transform Dataflow (Script)**.</span></span> <span data-ttu-id="5709d-105">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5709d-105">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span></span>

## <a name="transform-frame"></a><span data-ttu-id="5709d-106">Transform frame</span><span class="sxs-lookup"><span data-stu-id="5709d-106">Transform frame</span></span>
### <a name="create-a-new-column-dynamically"></a><span data-ttu-id="5709d-107">Create a new column dynamically</span><span class="sxs-lookup"><span data-stu-id="5709d-107">Create a new column dynamically</span></span> 
<span data-ttu-id="5709d-108">Creates a column dynamically (**city2**) and reconciles multiple different versions of San Francisco to one from the existing city column.</span><span class="sxs-lookup"><span data-stu-id="5709d-108">Creates a column dynamically (**city2**) and reconciles multiple different versions of San Francisco to one from the existing city column.</span></span>
```python
    df.loc[(df['city'] == 'San Francisco') | (df['city'] == 'SF') | (df['city'] == 'S.F.') | (df['city'] == 'SAN FRANCISCO'), 'city2'] = 'San Francisco'
```

### <a name="add-new-aggregates"></a><span data-ttu-id="5709d-109">Add new aggregates</span><span class="sxs-lookup"><span data-stu-id="5709d-109">Add new aggregates</span></span>
<span data-ttu-id="5709d-110">Creates a new frame with the first and last aggregates computed for the score column.</span><span class="sxs-lookup"><span data-stu-id="5709d-110">Creates a new frame with the first and last aggregates computed for the score column.</span></span> <span data-ttu-id="5709d-111">These are grouped by the **risk_category** column.</span><span class="sxs-lookup"><span data-stu-id="5709d-111">These are grouped by the **risk_category** column.</span></span>
```python
    df = df.groupby(['risk_category'])['Score'].agg(['first','last'])
```
### <a name="winsorize-a-column"></a><span data-ttu-id="5709d-112">Winsorize a column</span><span class="sxs-lookup"><span data-stu-id="5709d-112">Winsorize a column</span></span> 
<span data-ttu-id="5709d-113">Reformulates the data to meet a formula for reducing the outliers in a column.</span><span class="sxs-lookup"><span data-stu-id="5709d-113">Reformulates the data to meet a formula for reducing the outliers in a column.</span></span>
```python
    import scipy.stats as stats
    df['Last Order'] = stats.mstats.winsorize(df['Last Order'].values, limits=0.4)
```

## <a name="transform-data-flow"></a><span data-ttu-id="5709d-114">Transform data flow</span><span class="sxs-lookup"><span data-stu-id="5709d-114">Transform data flow</span></span>
### <a name="fill-down"></a><span data-ttu-id="5709d-115">Fill down</span><span class="sxs-lookup"><span data-stu-id="5709d-115">Fill down</span></span> 

<span data-ttu-id="5709d-116">Fill down requires two transforms.</span><span class="sxs-lookup"><span data-stu-id="5709d-116">Fill down requires two transforms.</span></span> <span data-ttu-id="5709d-117">It assumes data that looks like the following table:</span><span class="sxs-lookup"><span data-stu-id="5709d-117">It assumes data that looks like the following table:</span></span>

|<span data-ttu-id="5709d-118">State</span><span class="sxs-lookup"><span data-stu-id="5709d-118">State</span></span>         |<span data-ttu-id="5709d-119">City</span><span class="sxs-lookup"><span data-stu-id="5709d-119">City</span></span>       |
|--------------|-----------|
|<span data-ttu-id="5709d-120">Washington</span><span class="sxs-lookup"><span data-stu-id="5709d-120">Washington</span></span>    |<span data-ttu-id="5709d-121">Redmond</span><span class="sxs-lookup"><span data-stu-id="5709d-121">Redmond</span></span>    |
|              |<span data-ttu-id="5709d-122">Bellevue</span><span class="sxs-lookup"><span data-stu-id="5709d-122">Bellevue</span></span>   |
|              |<span data-ttu-id="5709d-123">Issaquah</span><span class="sxs-lookup"><span data-stu-id="5709d-123">Issaquah</span></span>   |
|              |<span data-ttu-id="5709d-124">Seattle</span><span class="sxs-lookup"><span data-stu-id="5709d-124">Seattle</span></span>    |
|<span data-ttu-id="5709d-125">California</span><span class="sxs-lookup"><span data-stu-id="5709d-125">California</span></span>    |<span data-ttu-id="5709d-126">Los Angeles</span><span class="sxs-lookup"><span data-stu-id="5709d-126">Los Angeles</span></span>|
|              |<span data-ttu-id="5709d-127">San Diego</span><span class="sxs-lookup"><span data-stu-id="5709d-127">San Diego</span></span>  |
|              |<span data-ttu-id="5709d-128">San Jose</span><span class="sxs-lookup"><span data-stu-id="5709d-128">San Jose</span></span>   |
|<span data-ttu-id="5709d-129">Texas</span><span class="sxs-lookup"><span data-stu-id="5709d-129">Texas</span></span>         |<span data-ttu-id="5709d-130">Dallas</span><span class="sxs-lookup"><span data-stu-id="5709d-130">Dallas</span></span>     |
|              |<span data-ttu-id="5709d-131">San Antonio</span><span class="sxs-lookup"><span data-stu-id="5709d-131">San Antonio</span></span>|
|              |<span data-ttu-id="5709d-132">Houston</span><span class="sxs-lookup"><span data-stu-id="5709d-132">Houston</span></span>    |

1. <span data-ttu-id="5709d-133">Create an "Add Column (Script)" transform using the following code:</span><span class="sxs-lookup"><span data-stu-id="5709d-133">Create an "Add Column (Script)" transform using the following code:</span></span>
```python
    row['State'] if len(row['State']) > 0 else None
```

2. <span data-ttu-id="5709d-134">Create a "Transform Data Flow (Script)" transform that contains the following code:</span><span class="sxs-lookup"><span data-stu-id="5709d-134">Create a "Transform Data Flow (Script)" transform that contains the following code:</span></span>
```python
    df = df.fillna( method='pad')
```

<span data-ttu-id="5709d-135">The data now looks like the following table:</span><span class="sxs-lookup"><span data-stu-id="5709d-135">The data now looks like the following table:</span></span>

|<span data-ttu-id="5709d-136">State</span><span class="sxs-lookup"><span data-stu-id="5709d-136">State</span></span>         |<span data-ttu-id="5709d-137">newState</span><span class="sxs-lookup"><span data-stu-id="5709d-137">newState</span></span>         |<span data-ttu-id="5709d-138">City</span><span class="sxs-lookup"><span data-stu-id="5709d-138">City</span></span>       |
|--------------|--------------|-----------|
|<span data-ttu-id="5709d-139">Washington</span><span class="sxs-lookup"><span data-stu-id="5709d-139">Washington</span></span>    |<span data-ttu-id="5709d-140">Washington</span><span class="sxs-lookup"><span data-stu-id="5709d-140">Washington</span></span>    |<span data-ttu-id="5709d-141">Redmond</span><span class="sxs-lookup"><span data-stu-id="5709d-141">Redmond</span></span>    |
|              |<span data-ttu-id="5709d-142">Washington</span><span class="sxs-lookup"><span data-stu-id="5709d-142">Washington</span></span>    |<span data-ttu-id="5709d-143">Bellevue</span><span class="sxs-lookup"><span data-stu-id="5709d-143">Bellevue</span></span>   |
|              |<span data-ttu-id="5709d-144">Washington</span><span class="sxs-lookup"><span data-stu-id="5709d-144">Washington</span></span>    |<span data-ttu-id="5709d-145">Issaquah</span><span class="sxs-lookup"><span data-stu-id="5709d-145">Issaquah</span></span>   |
|              |<span data-ttu-id="5709d-146">Washington</span><span class="sxs-lookup"><span data-stu-id="5709d-146">Washington</span></span>    |<span data-ttu-id="5709d-147">Seattle</span><span class="sxs-lookup"><span data-stu-id="5709d-147">Seattle</span></span>    |
|<span data-ttu-id="5709d-148">California</span><span class="sxs-lookup"><span data-stu-id="5709d-148">California</span></span>    |<span data-ttu-id="5709d-149">California</span><span class="sxs-lookup"><span data-stu-id="5709d-149">California</span></span>    |<span data-ttu-id="5709d-150">Los Angeles</span><span class="sxs-lookup"><span data-stu-id="5709d-150">Los Angeles</span></span>|
|              |<span data-ttu-id="5709d-151">California</span><span class="sxs-lookup"><span data-stu-id="5709d-151">California</span></span>    |<span data-ttu-id="5709d-152">San Diego</span><span class="sxs-lookup"><span data-stu-id="5709d-152">San Diego</span></span>  |
|              |<span data-ttu-id="5709d-153">California</span><span class="sxs-lookup"><span data-stu-id="5709d-153">California</span></span>    |<span data-ttu-id="5709d-154">San Jose</span><span class="sxs-lookup"><span data-stu-id="5709d-154">San Jose</span></span>   |
|<span data-ttu-id="5709d-155">Texas</span><span class="sxs-lookup"><span data-stu-id="5709d-155">Texas</span></span>         |<span data-ttu-id="5709d-156">Texas</span><span class="sxs-lookup"><span data-stu-id="5709d-156">Texas</span></span>         |<span data-ttu-id="5709d-157">Dallas</span><span class="sxs-lookup"><span data-stu-id="5709d-157">Dallas</span></span>     |
|              |<span data-ttu-id="5709d-158">Texas</span><span class="sxs-lookup"><span data-stu-id="5709d-158">Texas</span></span>         |<span data-ttu-id="5709d-159">San Antonio</span><span class="sxs-lookup"><span data-stu-id="5709d-159">San Antonio</span></span>|
|              |<span data-ttu-id="5709d-160">Texas</span><span class="sxs-lookup"><span data-stu-id="5709d-160">Texas</span></span>         |<span data-ttu-id="5709d-161">Houston</span><span class="sxs-lookup"><span data-stu-id="5709d-161">Houston</span></span>    |


### <a name="min-max-normalization"></a><span data-ttu-id="5709d-162">Min-max normalization</span><span class="sxs-lookup"><span data-stu-id="5709d-162">Min-max normalization</span></span>
```python
    df["NewCol"] = (df["Col1"]-df["Col1"].mean())/df["Col1"].std()
```