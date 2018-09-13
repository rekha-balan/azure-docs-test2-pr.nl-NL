---
title: Supported inspectors available with Azure Machine Learning Data Preparation  | Microsoft Docs
description: This document provides a complete list of inspectors available for Azure Machine Learning data preparation
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
ms.openlocfilehash: ef5f6f3dc7ae0c555b2afe000b54c443313800f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855899"
---
# <a name="supported-inspectors-for-the-azure-machine-learning-data-preparation-preview"></a><span data-ttu-id="36019-103">Supported inspectors for the Azure Machine Learning data preparation preview</span><span class="sxs-lookup"><span data-stu-id="36019-103">Supported inspectors for the Azure Machine Learning data preparation preview</span></span>
<span data-ttu-id="36019-104">This document outlines the set of inspectors that are available in this preview.</span><span class="sxs-lookup"><span data-stu-id="36019-104">This document outlines the set of inspectors that are available in this preview.</span></span>

## <a name="the-halo-effect"></a><span data-ttu-id="36019-105">The halo effect</span><span class="sxs-lookup"><span data-stu-id="36019-105">The halo effect</span></span> 
<span data-ttu-id="36019-106">Some inspectors support the halo effect.</span><span class="sxs-lookup"><span data-stu-id="36019-106">Some inspectors support the halo effect.</span></span> <span data-ttu-id="36019-107">This effect uses two different colors to immediately show the change visually from a transform.</span><span class="sxs-lookup"><span data-stu-id="36019-107">This effect uses two different colors to immediately show the change visually from a transform.</span></span> <span data-ttu-id="36019-108">The gray represents the value prior to the latest transform, and the blue shows the current value.</span><span class="sxs-lookup"><span data-stu-id="36019-108">The gray represents the value prior to the latest transform, and the blue shows the current value.</span></span> <span data-ttu-id="36019-109">This effect can be enabled and disabled in options.</span><span class="sxs-lookup"><span data-stu-id="36019-109">This effect can be enabled and disabled in options.</span></span>

## <a name="graphical-filtering"></a><span data-ttu-id="36019-110">Graphical filtering</span><span class="sxs-lookup"><span data-stu-id="36019-110">Graphical filtering</span></span> 
<span data-ttu-id="36019-111">Some of the inspectors support the filtering of data by using the inspector as an editor.</span><span class="sxs-lookup"><span data-stu-id="36019-111">Some of the inspectors support the filtering of data by using the inspector as an editor.</span></span> <span data-ttu-id="36019-112">Using the inspector as an editor involves selecting graphical elements, and then using the toolbar in the upper-right part of the inspector window to filter in or out the selected values.</span><span class="sxs-lookup"><span data-stu-id="36019-112">Using the inspector as an editor involves selecting graphical elements, and then using the toolbar in the upper-right part of the inspector window to filter in or out the selected values.</span></span> 

## <a name="column-statistics"></a><span data-ttu-id="36019-113">Column statistics</span><span class="sxs-lookup"><span data-stu-id="36019-113">Column statistics</span></span>
<span data-ttu-id="36019-114">For numeric columns, this inspector provides a variety of different stats about the column.</span><span class="sxs-lookup"><span data-stu-id="36019-114">For numeric columns, this inspector provides a variety of different stats about the column.</span></span> <span data-ttu-id="36019-115">Statistics include the following measurements:</span><span class="sxs-lookup"><span data-stu-id="36019-115">Statistics include the following measurements:</span></span> 
- <span data-ttu-id="36019-116">Minimum</span><span class="sxs-lookup"><span data-stu-id="36019-116">Minimum</span></span>
- <span data-ttu-id="36019-117">Lower quartile</span><span class="sxs-lookup"><span data-stu-id="36019-117">Lower quartile</span></span>
- <span data-ttu-id="36019-118">Median</span><span class="sxs-lookup"><span data-stu-id="36019-118">Median</span></span>
- <span data-ttu-id="36019-119">Upper quartile</span><span class="sxs-lookup"><span data-stu-id="36019-119">Upper quartile</span></span>
- <span data-ttu-id="36019-120">Maximum</span><span class="sxs-lookup"><span data-stu-id="36019-120">Maximum</span></span>
- <span data-ttu-id="36019-121">Average</span><span class="sxs-lookup"><span data-stu-id="36019-121">Average</span></span>
- <span data-ttu-id="36019-122">Standard deviation</span><span class="sxs-lookup"><span data-stu-id="36019-122">Standard deviation</span></span>


### <a name="options"></a><span data-ttu-id="36019-123">Options</span><span class="sxs-lookup"><span data-stu-id="36019-123">Options</span></span> 
- <span data-ttu-id="36019-124">None</span><span class="sxs-lookup"><span data-stu-id="36019-124">None</span></span>

## <a name="histogram"></a><span data-ttu-id="36019-125">Histogram</span><span class="sxs-lookup"><span data-stu-id="36019-125">Histogram</span></span> 
<span data-ttu-id="36019-126">Computes and displays a histogram of a single numeric column.</span><span class="sxs-lookup"><span data-stu-id="36019-126">Computes and displays a histogram of a single numeric column.</span></span> <span data-ttu-id="36019-127">The default number of buckets is calculated using Scott’s Rule.</span><span class="sxs-lookup"><span data-stu-id="36019-127">The default number of buckets is calculated using Scott’s Rule.</span></span> <span data-ttu-id="36019-128">However, the rule can be overridden via the options.</span><span class="sxs-lookup"><span data-stu-id="36019-128">However, the rule can be overridden via the options.</span></span>

<span data-ttu-id="36019-129">This Inspector supports the halo effect.</span><span class="sxs-lookup"><span data-stu-id="36019-129">This Inspector supports the halo effect.</span></span>


### <a name="options"></a><span data-ttu-id="36019-130">Options</span><span class="sxs-lookup"><span data-stu-id="36019-130">Options</span></span>
- <span data-ttu-id="36019-131">Minimum number of buckets (applies even when default bucketing is checked)</span><span class="sxs-lookup"><span data-stu-id="36019-131">Minimum number of buckets (applies even when default bucketing is checked)</span></span>
- <span data-ttu-id="36019-132">Default number of buckets (Scott's Rule)</span><span class="sxs-lookup"><span data-stu-id="36019-132">Default number of buckets (Scott's Rule)</span></span> 
- <span data-ttu-id="36019-133">Show halo</span><span class="sxs-lookup"><span data-stu-id="36019-133">Show halo</span></span>
- <span data-ttu-id="36019-134">Kernel density plot overlay (Gaussian kernel)</span><span class="sxs-lookup"><span data-stu-id="36019-134">Kernel density plot overlay (Gaussian kernel)</span></span> 
- <span data-ttu-id="36019-135">Use logarithmic scale</span><span class="sxs-lookup"><span data-stu-id="36019-135">Use logarithmic scale</span></span>


### <a name="actions"></a><span data-ttu-id="36019-136">Actions</span><span class="sxs-lookup"><span data-stu-id="36019-136">Actions</span></span>
<span data-ttu-id="36019-137">This inspector supports filtering via buckets, which can include single or multi-select buckets.</span><span class="sxs-lookup"><span data-stu-id="36019-137">This inspector supports filtering via buckets, which can include single or multi-select buckets.</span></span> <span data-ttu-id="36019-138">Apply filters as previously described.</span><span class="sxs-lookup"><span data-stu-id="36019-138">Apply filters as previously described.</span></span>

## <a name="value-counts"></a><span data-ttu-id="36019-139">Value counts</span><span class="sxs-lookup"><span data-stu-id="36019-139">Value counts</span></span>
<span data-ttu-id="36019-140">This inspector presents a frequency table of values for the column that is currently selected.</span><span class="sxs-lookup"><span data-stu-id="36019-140">This inspector presents a frequency table of values for the column that is currently selected.</span></span> <span data-ttu-id="36019-141">The default display is for the top six values.</span><span class="sxs-lookup"><span data-stu-id="36019-141">The default display is for the top six values.</span></span> <span data-ttu-id="36019-142">You can change the limit to any number, however.</span><span class="sxs-lookup"><span data-stu-id="36019-142">You can change the limit to any number, however.</span></span> <span data-ttu-id="36019-143">You can also set the display to count from the bottom instead of the top.</span><span class="sxs-lookup"><span data-stu-id="36019-143">You can also set the display to count from the bottom instead of the top.</span></span> <span data-ttu-id="36019-144">This inspector supports the halo effect.</span><span class="sxs-lookup"><span data-stu-id="36019-144">This inspector supports the halo effect.</span></span>

### <a name="options"></a><span data-ttu-id="36019-145">Options</span><span class="sxs-lookup"><span data-stu-id="36019-145">Options</span></span> 
- <span data-ttu-id="36019-146">Number of top values</span><span class="sxs-lookup"><span data-stu-id="36019-146">Number of top values</span></span>
- <span data-ttu-id="36019-147">Descending</span><span class="sxs-lookup"><span data-stu-id="36019-147">Descending</span></span>
- <span data-ttu-id="36019-148">Include null/error values</span><span class="sxs-lookup"><span data-stu-id="36019-148">Include null/error values</span></span>
- <span data-ttu-id="36019-149">Show halo</span><span class="sxs-lookup"><span data-stu-id="36019-149">Show halo</span></span>
- <span data-ttu-id="36019-150">Use logarithmic scale</span><span class="sxs-lookup"><span data-stu-id="36019-150">Use logarithmic scale</span></span>


### <a name="actions"></a><span data-ttu-id="36019-151">Actions</span><span class="sxs-lookup"><span data-stu-id="36019-151">Actions</span></span> 
<span data-ttu-id="36019-152">This inspector supports filtering via bars, which can include single or multi-select bars.</span><span class="sxs-lookup"><span data-stu-id="36019-152">This inspector supports filtering via bars, which can include single or multi-select bars.</span></span> <span data-ttu-id="36019-153">Apply filters as previously described.</span><span class="sxs-lookup"><span data-stu-id="36019-153">Apply filters as previously described.</span></span>

## <a name="box-plot"></a><span data-ttu-id="36019-154">Box plot</span><span class="sxs-lookup"><span data-stu-id="36019-154">Box plot</span></span> 
<span data-ttu-id="36019-155">A box whisker plot of a numeric column.</span><span class="sxs-lookup"><span data-stu-id="36019-155">A box whisker plot of a numeric column.</span></span>

### <a name="options"></a><span data-ttu-id="36019-156">Options</span><span class="sxs-lookup"><span data-stu-id="36019-156">Options</span></span> 
- <span data-ttu-id="36019-157">Group by column</span><span class="sxs-lookup"><span data-stu-id="36019-157">Group by column</span></span>

## <a name="scatter-plot"></a><span data-ttu-id="36019-158">Scatter plot</span><span class="sxs-lookup"><span data-stu-id="36019-158">Scatter plot</span></span>
<span data-ttu-id="36019-159">A scatter plot for two numeric columns.</span><span class="sxs-lookup"><span data-stu-id="36019-159">A scatter plot for two numeric columns.</span></span> <span data-ttu-id="36019-160">The data is down-sampled for performance reasons.</span><span class="sxs-lookup"><span data-stu-id="36019-160">The data is down-sampled for performance reasons.</span></span> <span data-ttu-id="36019-161">The sample size can be overridden in the options.</span><span class="sxs-lookup"><span data-stu-id="36019-161">The sample size can be overridden in the options.</span></span>

### <a name="options"></a><span data-ttu-id="36019-162">Options</span><span class="sxs-lookup"><span data-stu-id="36019-162">Options</span></span>  
- <span data-ttu-id="36019-163">X-axis column</span><span class="sxs-lookup"><span data-stu-id="36019-163">X-axis column</span></span>
- <span data-ttu-id="36019-164">Y-axis column</span><span class="sxs-lookup"><span data-stu-id="36019-164">Y-axis column</span></span>
- <span data-ttu-id="36019-165">Sample size</span><span class="sxs-lookup"><span data-stu-id="36019-165">Sample size</span></span>
- <span data-ttu-id="36019-166">Group by column</span><span class="sxs-lookup"><span data-stu-id="36019-166">Group by column</span></span>


## <a name="time-series"></a><span data-ttu-id="36019-167">Time series</span><span class="sxs-lookup"><span data-stu-id="36019-167">Time series</span></span>
<span data-ttu-id="36019-168">A line graph with time awareness on the x-axis.</span><span class="sxs-lookup"><span data-stu-id="36019-168">A line graph with time awareness on the x-axis.</span></span>

### <a name="options"></a><span data-ttu-id="36019-169">Options</span><span class="sxs-lookup"><span data-stu-id="36019-169">Options</span></span>
- <span data-ttu-id="36019-170">Date column</span><span class="sxs-lookup"><span data-stu-id="36019-170">Date column</span></span>
- <span data-ttu-id="36019-171">Numeric column</span><span class="sxs-lookup"><span data-stu-id="36019-171">Numeric column</span></span>
- <span data-ttu-id="36019-172">Sample size</span><span class="sxs-lookup"><span data-stu-id="36019-172">Sample size</span></span>


### <a name="actions"></a><span data-ttu-id="36019-173">Actions</span><span class="sxs-lookup"><span data-stu-id="36019-173">Actions</span></span>
<span data-ttu-id="36019-174">This inspector supports filtering via a click-and-drag select method to select a range on the graph.</span><span class="sxs-lookup"><span data-stu-id="36019-174">This inspector supports filtering via a click-and-drag select method to select a range on the graph.</span></span> <span data-ttu-id="36019-175">After you complete selection, apply filters as previously described.</span><span class="sxs-lookup"><span data-stu-id="36019-175">After you complete selection, apply filters as previously described.</span></span>


## <a name="map"></a><span data-ttu-id="36019-176">Map</span><span class="sxs-lookup"><span data-stu-id="36019-176">Map</span></span> 
<span data-ttu-id="36019-177">A map with points that are plotted, assuming that latitude and longitude have been specified.</span><span class="sxs-lookup"><span data-stu-id="36019-177">A map with points that are plotted, assuming that latitude and longitude have been specified.</span></span> <span data-ttu-id="36019-178">Latitude must be selected first.</span><span class="sxs-lookup"><span data-stu-id="36019-178">Latitude must be selected first.</span></span>

### <a name="options"></a><span data-ttu-id="36019-179">Options</span><span class="sxs-lookup"><span data-stu-id="36019-179">Options</span></span>
- <span data-ttu-id="36019-180">Latitude column</span><span class="sxs-lookup"><span data-stu-id="36019-180">Latitude column</span></span>
- <span data-ttu-id="36019-181">Longitude column</span><span class="sxs-lookup"><span data-stu-id="36019-181">Longitude column</span></span>
- <span data-ttu-id="36019-182">Clustering on</span><span class="sxs-lookup"><span data-stu-id="36019-182">Clustering on</span></span>
- <span data-ttu-id="36019-183">Group by column</span><span class="sxs-lookup"><span data-stu-id="36019-183">Group by column</span></span>


### <a name="actions"></a><span data-ttu-id="36019-184">Actions</span><span class="sxs-lookup"><span data-stu-id="36019-184">Actions</span></span>
<span data-ttu-id="36019-185">This inspector supports filtering via point selection on the map.</span><span class="sxs-lookup"><span data-stu-id="36019-185">This inspector supports filtering via point selection on the map.</span></span> <span data-ttu-id="36019-186">Press the **Ctrl** key, and then click and drag with the mouse to form a square around the points.</span><span class="sxs-lookup"><span data-stu-id="36019-186">Press the **Ctrl** key, and then click and drag with the mouse to form a square around the points.</span></span> <span data-ttu-id="36019-187">Then apply filters as previously described.</span><span class="sxs-lookup"><span data-stu-id="36019-187">Then apply filters as previously described.</span></span>

<span data-ttu-id="36019-188">You can quickly size the map to show only the possible points by pressing the **E** on the left side of the map.</span><span class="sxs-lookup"><span data-stu-id="36019-188">You can quickly size the map to show only the possible points by pressing the **E** on the left side of the map.</span></span>


## <a name="pattern-frequency"></a><span data-ttu-id="36019-189">Pattern Frequency</span><span class="sxs-lookup"><span data-stu-id="36019-189">Pattern Frequency</span></span> 

<span data-ttu-id="36019-190">This inspector shows a list of patterns in the selected String column.</span><span class="sxs-lookup"><span data-stu-id="36019-190">This inspector shows a list of patterns in the selected String column.</span></span> <span data-ttu-id="36019-191">The patterns are represented using a regular expression like syntax.</span><span class="sxs-lookup"><span data-stu-id="36019-191">The patterns are represented using a regular expression like syntax.</span></span> <span data-ttu-id="36019-192">Hovering on the pattern shows the examples of values represented by that pattern.</span><span class="sxs-lookup"><span data-stu-id="36019-192">Hovering on the pattern shows the examples of values represented by that pattern.</span></span> <span data-ttu-id="36019-193">Along with the patterns, the approximate coverages in terms of percentage is also shown.</span><span class="sxs-lookup"><span data-stu-id="36019-193">Along with the patterns, the approximate coverages in terms of percentage is also shown.</span></span>

![Image of the pattern inspector](media/data-prep-appendix4-supported-inspectors/PatternInspectorProductNumber.png)

### <a name="options"></a><span data-ttu-id="36019-195">Options</span><span class="sxs-lookup"><span data-stu-id="36019-195">Options</span></span>
- <span data-ttu-id="36019-196">Number of top values</span><span class="sxs-lookup"><span data-stu-id="36019-196">Number of top values</span></span>
- <span data-ttu-id="36019-197">Descending</span><span class="sxs-lookup"><span data-stu-id="36019-197">Descending</span></span>
- <span data-ttu-id="36019-198">Show halo</span><span class="sxs-lookup"><span data-stu-id="36019-198">Show halo</span></span>

### <a name="actions"></a><span data-ttu-id="36019-199">Actions</span><span class="sxs-lookup"><span data-stu-id="36019-199">Actions</span></span>
<span data-ttu-id="36019-200">This inspector supports filtering based on displayed patterns.</span><span class="sxs-lookup"><span data-stu-id="36019-200">This inspector supports filtering based on displayed patterns.</span></span> <span data-ttu-id="36019-201">Press the **Ctrl** key, and then select the filled bars in pattern inspector.</span><span class="sxs-lookup"><span data-stu-id="36019-201">Press the **Ctrl** key, and then select the filled bars in pattern inspector.</span></span> <span data-ttu-id="36019-202">Then apply filters as previously described.</span><span class="sxs-lookup"><span data-stu-id="36019-202">Then apply filters as previously described.</span></span> <span data-ttu-id="36019-203">As a result of the user acion, an Advanced filter step is added.</span><span class="sxs-lookup"><span data-stu-id="36019-203">As a result of the user acion, an Advanced filter step is added.</span></span> <span data-ttu-id="36019-204">You can see and modify the generated Python code by invoking the edit option of the Advanced Filter step.</span><span class="sxs-lookup"><span data-stu-id="36019-204">You can see and modify the generated Python code by invoking the edit option of the Advanced Filter step.</span></span>
