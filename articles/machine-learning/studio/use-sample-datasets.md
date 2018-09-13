---
title: Use the sample datasets in Machine Learning Studio | Microsoft Docs
description: Descriptions of the datasets used in sample models included in Machine Learning Studio. You can use these sample datasets for your experiments.
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2018
ms.openlocfilehash: 7a90a8f05082e2c0731f9f112d3e56ecaf4ea55b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857886"
---
# <a name="use-the-sample-datasets-in-azure-machine-learning-studio"></a><span data-ttu-id="519e2-104">Use the sample datasets in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="519e2-104">Use the sample datasets in Azure Machine Learning Studio</span></span>
[top]: #machine-learning-sample-datasets

<span data-ttu-id="519e2-105">When you create a new workspace in Azure Machine Learning, a number of sample datasets and experiments are included by default.</span><span class="sxs-lookup"><span data-stu-id="519e2-105">When you create a new workspace in Azure Machine Learning, a number of sample datasets and experiments are included by default.</span></span> <span data-ttu-id="519e2-106">Many of these sample datasets are used by the sample models in the [Azure AI Gallery](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="519e2-106">Many of these sample datasets are used by the sample models in the [Azure AI Gallery](http://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="519e2-107">Others are included as examples of various types of data typically used in machine learning.</span><span class="sxs-lookup"><span data-stu-id="519e2-107">Others are included as examples of various types of data typically used in machine learning.</span></span>

<span data-ttu-id="519e2-108">Some of these datasets are available in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="519e2-108">Some of these datasets are available in Azure Blob storage.</span></span> <span data-ttu-id="519e2-109">For these datasets, the following table provides a direct link.</span><span class="sxs-lookup"><span data-stu-id="519e2-109">For these datasets, the following table provides a direct link.</span></span> <span data-ttu-id="519e2-110">You can use these datasets in your experiments by using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="519e2-110">You can use these datasets in your experiments by using the [Import Data][import-data] module.</span></span>

<span data-ttu-id="519e2-111">The rest of these sample datasets are available in your workspace under **Saved Datasets**.</span><span class="sxs-lookup"><span data-stu-id="519e2-111">The rest of these sample datasets are available in your workspace under **Saved Datasets**.</span></span> <span data-ttu-id="519e2-112">You can find this in the module palette to the left of the experiment canvas in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="519e2-112">You can find this in the module palette to the left of the experiment canvas in Machine Learning Studio.</span></span>
<span data-ttu-id="519e2-113">You can use any of these datasets in your own experiment by dragging it to your experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="519e2-113">You can use any of these datasets in your own experiment by dragging it to your experiment canvas.</span></span>


[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th><span data-ttu-id="519e2-114">Dataset name</span><span class="sxs-lookup"><span data-stu-id="519e2-114">Dataset name</span></span></th>
  <th><span data-ttu-id="519e2-115">Dataset description</span><span class="sxs-lookup"><span data-stu-id="519e2-115">Dataset description</span></span></th>
</tr>

<tr>
  <td><span data-ttu-id="519e2-116">Adult Census Income Binary Classification dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-116">Adult Census Income Binary Classification dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-117">A subset of the 1994 Census database, using working adults over the age of 16 with an adjusted income index of > 100.</span><span class="sxs-lookup"><span data-stu-id="519e2-117">A subset of the 1994 Census database, using working adults over the age of 16 with an adjusted income index of > 100.</span></span>
<p></p><span data-ttu-id="519e2-118">
<b>Usage:</b> Classify people using demographics to predict whether a person earns over 50K a year.</span><span class="sxs-lookup"><span data-stu-id="519e2-118">
<b>Usage:</b> Classify people using demographics to predict whether a person earns over 50K a year.</span></span>
<p></p><span data-ttu-id="519e2-119">
<b>Related Research:</b> Kohavi, R., Becker, B., (1996).</span><span class="sxs-lookup"><span data-stu-id="519e2-119">
<b>Related Research:</b> Kohavi, R., Becker, B., (1996).</span></span> <span data-ttu-id="519e2-120">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-120">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-121">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-121">Irvine, CA: University of California, School of Information and Computer Science</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-122">Airport Codes Dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-122">Airport Codes Dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-123">U.S. airport codes.</span><span class="sxs-lookup"><span data-stu-id="519e2-123">U.S. airport codes.</span></span>
<p></p>
<span data-ttu-id="519e2-124">This dataset contains one row for each U.S. airport, providing the airport ID number and name along with the location city and state.</span><span class="sxs-lookup"><span data-stu-id="519e2-124">This dataset contains one row for each U.S. airport, providing the airport ID number and name along with the location city and state.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-125">Automobile price data (Raw)</span><span class="sxs-lookup"><span data-stu-id="519e2-125">Automobile price data (Raw)</span></span></td>
  <td>
<span data-ttu-id="519e2-126">Information about automobiles by make and model, including the price, features such as the number of cylinders and MPG, as well as an insurance risk score.</span><span class="sxs-lookup"><span data-stu-id="519e2-126">Information about automobiles by make and model, including the price, features such as the number of cylinders and MPG, as well as an insurance risk score.</span></span>
<p></p>
<span data-ttu-id="519e2-127">The risk score is initially associated with auto price.</span><span class="sxs-lookup"><span data-stu-id="519e2-127">The risk score is initially associated with auto price.</span></span> <span data-ttu-id="519e2-128">It is then adjusted for actual risk in a process known to actuaries as symboling.</span><span class="sxs-lookup"><span data-stu-id="519e2-128">It is then adjusted for actual risk in a process known to actuaries as symboling.</span></span> <span data-ttu-id="519e2-129">A value of +3 indicates that the auto is risky, and a value of -3 that it is probably safe.</span><span class="sxs-lookup"><span data-stu-id="519e2-129">A value of +3 indicates that the auto is risky, and a value of -3 that it is probably safe.</span></span>
<p></p><span data-ttu-id="519e2-130">
<b>Usage:</b> Predict the risk score by features, using regression or multivariate classification.</span><span class="sxs-lookup"><span data-stu-id="519e2-130">
<b>Usage:</b> Predict the risk score by features, using regression or multivariate classification.</span></span> 
<p></p><span data-ttu-id="519e2-131">
<b>Related Research:</b> Schlimmer, J.C.</span><span class="sxs-lookup"><span data-stu-id="519e2-131">
<b>Related Research:</b> Schlimmer, J.C.</span></span> <span data-ttu-id="519e2-132">(1987).</span><span class="sxs-lookup"><span data-stu-id="519e2-132">(1987).</span></span> <span data-ttu-id="519e2-133">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-133">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-134">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-134">Irvine, CA: University of California, School of Information and Computer Science</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-135">Bike Rental UCI dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-135">Bike Rental UCI dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-136">UCI Bike Rental dataset that is based on real data from Capital Bikeshare company that maintains a bike rental network in Washington DC.</span><span class="sxs-lookup"><span data-stu-id="519e2-136">UCI Bike Rental dataset that is based on real data from Capital Bikeshare company that maintains a bike rental network in Washington DC.</span></span>
<p></p>
<span data-ttu-id="519e2-137">The dataset has one row for each hour of each day in 2011 and 2012, for a total of 17,379 rows.</span><span class="sxs-lookup"><span data-stu-id="519e2-137">The dataset has one row for each hour of each day in 2011 and 2012, for a total of 17,379 rows.</span></span> <span data-ttu-id="519e2-138">The range of hourly bike rentals is from 1 to 977.</span><span class="sxs-lookup"><span data-stu-id="519e2-138">The range of hourly bike rentals is from 1 to 977.</span></span>

  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-139">Bill Gates RGB Image</span><span class="sxs-lookup"><span data-stu-id="519e2-139">Bill Gates RGB Image</span></span></td>
  <td>
<span data-ttu-id="519e2-140">Publicly available image file converted to CSV data.</span><span class="sxs-lookup"><span data-stu-id="519e2-140">Publicly available image file converted to CSV data.</span></span>
<p></p>
<span data-ttu-id="519e2-141">The code for converting the image is provided in the <strong>Color quantization using K-Means clustering</strong> model detail page.</span><span class="sxs-lookup"><span data-stu-id="519e2-141">The code for converting the image is provided in the <strong>Color quantization using K-Means clustering</strong> model detail page.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-142">Blood donation data</span><span class="sxs-lookup"><span data-stu-id="519e2-142">Blood donation data</span></span></td>
  <td>
<span data-ttu-id="519e2-143">A subset of data from the blood donor database of the Blood Transfusion Service Center of Hsin-Chu City, Taiwan.</span><span class="sxs-lookup"><span data-stu-id="519e2-143">A subset of data from the blood donor database of the Blood Transfusion Service Center of Hsin-Chu City, Taiwan.</span></span>
<p></p>
<span data-ttu-id="519e2-144">Donor data includes the months since last donation), and frequency, or the total number of donations, time since last donation, and amount of blood donated.</span><span class="sxs-lookup"><span data-stu-id="519e2-144">Donor data includes the months since last donation), and frequency, or the total number of donations, time since last donation, and amount of blood donated.</span></span>
<p></p><span data-ttu-id="519e2-145">
<b>Usage:</b> The goal is to predict via classification whether the donor donated blood in March 2007, where 1 indicates a donor during the target period, and 0 a non-donor.</span><span class="sxs-lookup"><span data-stu-id="519e2-145">
<b>Usage:</b> The goal is to predict via classification whether the donor donated blood in March 2007, where 1 indicates a donor during the target period, and 0 a non-donor.</span></span> 
<p></p><span data-ttu-id="519e2-146">
<b>Related Research:</b> Yeh, I.C., (2008).</span><span class="sxs-lookup"><span data-stu-id="519e2-146">
<b>Related Research:</b> Yeh, I.C., (2008).</span></span> <span data-ttu-id="519e2-147">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-147">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-148">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-148">Irvine, CA: University of California, School of Information and Computer Science</span></span>
<p></p>
<span data-ttu-id="519e2-149">Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence, "Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </span><span class="sxs-lookup"><span data-stu-id="519e2-149">Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence, "Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </span></span></td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-150">Breast cancer data</span><span class="sxs-lookup"><span data-stu-id="519e2-150">Breast cancer data</span></span></td>
  <td>
<span data-ttu-id="519e2-151">One of three cancer-related datasets provided by the Oncology Institute that appears frequently in machine learning literature.</span><span class="sxs-lookup"><span data-stu-id="519e2-151">One of three cancer-related datasets provided by the Oncology Institute that appears frequently in machine learning literature.</span></span> <span data-ttu-id="519e2-152">Combines diagnostic information with features from laboratory analysis of about 300 tissue samples.</span><span class="sxs-lookup"><span data-stu-id="519e2-152">Combines diagnostic information with features from laboratory analysis of about 300 tissue samples.</span></span>
<p></p><span data-ttu-id="519e2-153">
<b>Usage:</b> Classify the type of cancer, based on 9 attributes, some of which are linear and some are categorical.</span><span class="sxs-lookup"><span data-stu-id="519e2-153">
<b>Usage:</b> Classify the type of cancer, based on 9 attributes, some of which are linear and some are categorical.</span></span> 
<p></p><span data-ttu-id="519e2-154">
<b>Related Research:</b> Wohlberg, W.H., Street, W.N., & Mangasarian, O.L.</span><span class="sxs-lookup"><span data-stu-id="519e2-154">
<b>Related Research:</b> Wohlberg, W.H., Street, W.N., & Mangasarian, O.L.</span></span> <span data-ttu-id="519e2-155">(1995).</span><span class="sxs-lookup"><span data-stu-id="519e2-155">(1995).</span></span> <span data-ttu-id="519e2-156">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-156">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-157">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-157">Irvine, CA: University of California, School of Information and Computer Science</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-158">Breast Cancer Features</span><span class="sxs-lookup"><span data-stu-id="519e2-158">Breast Cancer Features</span></span> <td>
<span data-ttu-id="519e2-159">The dataset contains information for 102K suspicious regions (candidates) of X-ray images, each described by 117 features.</span><span class="sxs-lookup"><span data-stu-id="519e2-159">The dataset contains information for 102K suspicious regions (candidates) of X-ray images, each described by 117 features.</span></span> <span data-ttu-id="519e2-160">The features are proprietary and their meaning is not revealed by the dataset creators (Siemens Healthcare).</span><span class="sxs-lookup"><span data-stu-id="519e2-160">The features are proprietary and their meaning is not revealed by the dataset creators (Siemens Healthcare).</span></span> 
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-161">Breast Cancer Info</span><span class="sxs-lookup"><span data-stu-id="519e2-161">Breast Cancer Info</span></span></td>
  <td>
<span data-ttu-id="519e2-162">The dataset contains additional information for each suspicious region of X-ray image.</span><span class="sxs-lookup"><span data-stu-id="519e2-162">The dataset contains additional information for each suspicious region of X-ray image.</span></span> <span data-ttu-id="519e2-163">Each example provides information (for example, label, patient ID, coordinates of patch relative to the whole image) about the corresponding row number in the Breast Cancer Features dataset.</span><span class="sxs-lookup"><span data-stu-id="519e2-163">Each example provides information (for example, label, patient ID, coordinates of patch relative to the whole image) about the corresponding row number in the Breast Cancer Features dataset.</span></span> <span data-ttu-id="519e2-164">Each patient has a number of examples.</span><span class="sxs-lookup"><span data-stu-id="519e2-164">Each patient has a number of examples.</span></span> <span data-ttu-id="519e2-165">For patients who have a cancer, some examples are positive and some are negative.</span><span class="sxs-lookup"><span data-stu-id="519e2-165">For patients who have a cancer, some examples are positive and some are negative.</span></span> <span data-ttu-id="519e2-166">For patients who don't have a cancer, all examples are negative.</span><span class="sxs-lookup"><span data-stu-id="519e2-166">For patients who don't have a cancer, all examples are negative.</span></span> <span data-ttu-id="519e2-167">The dataset has 102K examples.</span><span class="sxs-lookup"><span data-stu-id="519e2-167">The dataset has 102K examples.</span></span> <span data-ttu-id="519e2-168">The dataset is biased, 0.6% of the points are positive, the rest are negative.</span><span class="sxs-lookup"><span data-stu-id="519e2-168">The dataset is biased, 0.6% of the points are positive, the rest are negative.</span></span> <span data-ttu-id="519e2-169">The dataset was made available by Siemens Healthcare.</span><span class="sxs-lookup"><span data-stu-id="519e2-169">The dataset was made available by Siemens Healthcare.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-170">CRM Appetency Labels Shared</span><span class="sxs-lookup"><span data-stu-id="519e2-170">CRM Appetency Labels Shared</span></span></td>
  <td>
<span data-ttu-id="519e2-171">Labels from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-171">Labels from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-172">CRM Churn Labels Shared</span><span class="sxs-lookup"><span data-stu-id="519e2-172">CRM Churn Labels Shared</span></span></td>
  <td>
<span data-ttu-id="519e2-173">Labels from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-173">Labels from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-174">CRM Dataset Shared</span><span class="sxs-lookup"><span data-stu-id="519e2-174">CRM Dataset Shared</span></span></td>
  <td>
<span data-ttu-id="519e2-175">This data comes from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train.data.zip">orange_small_train.data.zip</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-175">This data comes from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train.data.zip">orange_small_train.data.zip</a>).</span></span>
<p></p>
<span data-ttu-id="519e2-176">The dataset contains 50K customers from the French Telecom company Orange.</span><span class="sxs-lookup"><span data-stu-id="519e2-176">The dataset contains 50K customers from the French Telecom company Orange.</span></span> <span data-ttu-id="519e2-177">Each customer has 230 anonymized features, 190 of which are numeric and 40 are categorical.</span><span class="sxs-lookup"><span data-stu-id="519e2-177">Each customer has 230 anonymized features, 190 of which are numeric and 40 are categorical.</span></span> <span data-ttu-id="519e2-178">The features are very sparse.</span><span class="sxs-lookup"><span data-stu-id="519e2-178">The features are very sparse.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-179">CRM Upselling Labels Shared</span><span class="sxs-lookup"><span data-stu-id="519e2-179">CRM Upselling Labels Shared</span></span></td>
  <td>
<span data-ttu-id="519e2-180">Labels from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-180">Labels from the KDD Cup 2009 customer relationship prediction challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-181">Energy-Efficiency Regression data</span><span class="sxs-lookup"><span data-stu-id="519e2-181">Energy-Efficiency Regression data</span></span></td>
  <td>
<span data-ttu-id="519e2-182">A collection of simulated energy profiles, based on 12 different building shapes.</span><span class="sxs-lookup"><span data-stu-id="519e2-182">A collection of simulated energy profiles, based on 12 different building shapes.</span></span> <span data-ttu-id="519e2-183">The buildings are differentiated by eight features.</span><span class="sxs-lookup"><span data-stu-id="519e2-183">The buildings are differentiated by eight features.</span></span> <span data-ttu-id="519e2-184">This includes glazing area, the glazing area distribution, and orientation.</span><span class="sxs-lookup"><span data-stu-id="519e2-184">This includes glazing area, the glazing area distribution, and orientation.</span></span>
<p></p><span data-ttu-id="519e2-185">
<b>Usage:</b> Use either regression or classification to predict the energy-efficiency rating based as one of two real valued responses.</span><span class="sxs-lookup"><span data-stu-id="519e2-185">
<b>Usage:</b> Use either regression or classification to predict the energy-efficiency rating based as one of two real valued responses.</span></span> <span data-ttu-id="519e2-186">For multi-class classification, is round the response variable to the nearest integer.</span><span class="sxs-lookup"><span data-stu-id="519e2-186">For multi-class classification, is round the response variable to the nearest integer.</span></span> 
<p></p><span data-ttu-id="519e2-187">
<b>Related Research:</b> Xifara, A. & Tsanas, A. (2012).</span><span class="sxs-lookup"><span data-stu-id="519e2-187">
<b>Related Research:</b> Xifara, A. & Tsanas, A. (2012).</span></span> <span data-ttu-id="519e2-188">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-188">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-189">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-189">Irvine, CA: University of California, School of Information and Computer Science</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-190">Flight Delays Data</span><span class="sxs-lookup"><span data-stu-id="519e2-190">Flight Delays Data</span></span></td>
  <td>
<span data-ttu-id="519e2-191">Passenger flight on-time performance data taken from the TranStats data collection of the U.S. Department of Transportation (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">On-Time</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-191">Passenger flight on-time performance data taken from the TranStats data collection of the U.S. Department of Transportation (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">On-Time</a>).</span></span>
<p></p>
<span data-ttu-id="519e2-192">The dataset covers the time period April-October 2013.</span><span class="sxs-lookup"><span data-stu-id="519e2-192">The dataset covers the time period April-October 2013.</span></span> <span data-ttu-id="519e2-193">Before uploading to Azure Machine Learning Studio, the dataset was processed as follows:</span><span class="sxs-lookup"><span data-stu-id="519e2-193">Before uploading to Azure Machine Learning Studio, the dataset was processed as follows:</span></span>
<ul>
  <li><span data-ttu-id="519e2-194">The dataset was filtered to cover only the 70 busiest airports in the continental US</span><span class="sxs-lookup"><span data-stu-id="519e2-194">The dataset was filtered to cover only the 70 busiest airports in the continental US</span></span></li>
  <li><span data-ttu-id="519e2-195">Canceled flights were labeled as delayed by more than 15 minutes</span><span class="sxs-lookup"><span data-stu-id="519e2-195">Canceled flights were labeled as delayed by more than 15 minutes</span></span></li>
  <li><span data-ttu-id="519e2-196">Diverted flights were filtered out</span><span class="sxs-lookup"><span data-stu-id="519e2-196">Diverted flights were filtered out</span></span></li>
  <li><span data-ttu-id="519e2-197">The following columns were selected: Year, Month, DayofMonth, DayOfWeek, Carrier, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, Canceled</span><span class="sxs-lookup"><span data-stu-id="519e2-197">The following columns were selected: Year, Month, DayofMonth, DayOfWeek, Carrier, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, Canceled</span></span></li>
</ul>
</td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-198">Flight on-time performance (Raw)</span><span class="sxs-lookup"><span data-stu-id="519e2-198">Flight on-time performance (Raw)</span></span></td>
  <td>
<span data-ttu-id="519e2-199">Records of airplane flight arrivals and departures within United States from October 2011.</span><span class="sxs-lookup"><span data-stu-id="519e2-199">Records of airplane flight arrivals and departures within United States from October 2011.</span></span>
<p></p><span data-ttu-id="519e2-200">
<b>Usage:</b> Predict flight delays.</span><span class="sxs-lookup"><span data-stu-id="519e2-200">
<b>Usage:</b> Predict flight delays.</span></span> 
<p></p><span data-ttu-id="519e2-201">
<b>Related Research:</b> From US Dept. of Transportation <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-201">
<b>Related Research:</b> From US Dept. of Transportation <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-202">Forest fires data</span><span class="sxs-lookup"><span data-stu-id="519e2-202">Forest fires data</span></span></td>
  <td>
<span data-ttu-id="519e2-203">Contains weather data, such as temperature and humidity indices and wind speed.</span><span class="sxs-lookup"><span data-stu-id="519e2-203">Contains weather data, such as temperature and humidity indices and wind speed.</span></span> <span data-ttu-id="519e2-204">The data is taken from an area of northeast Portugal, combined with records of forest fires.</span><span class="sxs-lookup"><span data-stu-id="519e2-204">The data is taken from an area of northeast Portugal, combined with records of forest fires.</span></span>
<p></p><span data-ttu-id="519e2-205">
<b>Usage:</b> This is a difficult regression task, where the aim is to predict the burned area of forest fires.</span><span class="sxs-lookup"><span data-stu-id="519e2-205">
<b>Usage:</b> This is a difficult regression task, where the aim is to predict the burned area of forest fires.</span></span> 
<p></p><span data-ttu-id="519e2-206">
<b>Related Research:</b> Cortez, P., & Morais, A. (2008).</span><span class="sxs-lookup"><span data-stu-id="519e2-206">
<b>Related Research:</b> Cortez, P., & Morais, A. (2008).</span></span> <span data-ttu-id="519e2-207">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-207">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-208">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-208">Irvine, CA: University of California, School of Information and Computer Science</span></span>
<p></p>
<span data-ttu-id="519e2-209">[Cortez and Morais, 2007] P. Cortez and A. Morais.</span><span class="sxs-lookup"><span data-stu-id="519e2-209">[Cortez and Morais, 2007] P. Cortez and A. Morais.</span></span> <span data-ttu-id="519e2-210">A Data Mining Approach to Predict Forest Fires using Meteorological Data.</span><span class="sxs-lookup"><span data-stu-id="519e2-210">A Data Mining Approach to Predict Forest Fires using Meteorological Data.</span></span> <span data-ttu-id="519e2-211">In J. Neves, M. F.</span><span class="sxs-lookup"><span data-stu-id="519e2-211">In J. Neves, M. F.</span></span> <span data-ttu-id="519e2-212">Santos and J. Machado Eds., New Trends in Artificial Intelligence, Proceedings of the 13th EPIA 2007 - Portuguese Conference on Artificial Intelligence, December, Guimarães, Portugal, pp. 512-523, 2007.</span><span class="sxs-lookup"><span data-stu-id="519e2-212">Santos and J. Machado Eds., New Trends in Artificial Intelligence, Proceedings of the 13th EPIA 2007 - Portuguese Conference on Artificial Intelligence, December, Guimarães, Portugal, pp. 512-523, 2007.</span></span> <span data-ttu-id="519e2-213">APPIA, ISBN-13 978-989-95618-0-9.</span><span class="sxs-lookup"><span data-stu-id="519e2-213">APPIA, ISBN-13 978-989-95618-0-9.</span></span> <span data-ttu-id="519e2-214">Available at: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-214">Available at: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-215">German Credit Card UCI dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-215">German Credit Card UCI dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-216">The UCI Statlog (German Credit Card) dataset (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog+German+Credit+Data</a>), using the german.data file.</span><span class="sxs-lookup"><span data-stu-id="519e2-216">The UCI Statlog (German Credit Card) dataset (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog+German+Credit+Data</a>), using the german.data file.</span></span>
<p></p>
<span data-ttu-id="519e2-217">The dataset classifies people, described by a set of attributes, as low or high credit risks.</span><span class="sxs-lookup"><span data-stu-id="519e2-217">The dataset classifies people, described by a set of attributes, as low or high credit risks.</span></span> <span data-ttu-id="519e2-218">Each example represents a person.</span><span class="sxs-lookup"><span data-stu-id="519e2-218">Each example represents a person.</span></span> <span data-ttu-id="519e2-219">There are 20 features, both numerical and categorical, and a binary label (the credit risk value).</span><span class="sxs-lookup"><span data-stu-id="519e2-219">There are 20 features, both numerical and categorical, and a binary label (the credit risk value).</span></span> <span data-ttu-id="519e2-220">High credit risk entries have label = 2, low credit risk entries have label = 1.</span><span class="sxs-lookup"><span data-stu-id="519e2-220">High credit risk entries have label = 2, low credit risk entries have label = 1.</span></span> <span data-ttu-id="519e2-221">The cost of misclassifying a low risk example as high is 1, whereas the cost of misclassifying a high risk example as low is 5.</span><span class="sxs-lookup"><span data-stu-id="519e2-221">The cost of misclassifying a low risk example as high is 1, whereas the cost of misclassifying a high risk example as low is 5.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-222">IMDB Movie Titles</span><span class="sxs-lookup"><span data-stu-id="519e2-222">IMDB Movie Titles</span></span></td>
  <td>
<span data-ttu-id="519e2-223">The dataset contains information about movies that were rated in Twitter tweets: IMDB movie ID, movie name, genre, and production year.</span><span class="sxs-lookup"><span data-stu-id="519e2-223">The dataset contains information about movies that were rated in Twitter tweets: IMDB movie ID, movie name, genre, and production year.</span></span> <span data-ttu-id="519e2-224">There are 17K movies in the dataset.</span><span class="sxs-lookup"><span data-stu-id="519e2-224">There are 17K movies in the dataset.</span></span> <span data-ttu-id="519e2-225">The dataset was introduced in the paper "S.</span><span class="sxs-lookup"><span data-stu-id="519e2-225">The dataset was introduced in the paper "S.</span></span> <span data-ttu-id="519e2-226">Dooms, T. De Pessemier and L. Martens.</span><span class="sxs-lookup"><span data-stu-id="519e2-226">Dooms, T. De Pessemier and L. Martens.</span></span> <span data-ttu-id="519e2-227">MovieTweetings: a Movie Rating Dataset Collected From Twitter.</span><span class="sxs-lookup"><span data-stu-id="519e2-227">MovieTweetings: a Movie Rating Dataset Collected From Twitter.</span></span> <span data-ttu-id="519e2-228">Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013."</span><span class="sxs-lookup"><span data-stu-id="519e2-228">Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013."</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-229">Iris two class data</span><span class="sxs-lookup"><span data-stu-id="519e2-229">Iris two class data</span></span></td>
  <td>
<span data-ttu-id="519e2-230">This is perhaps the best known database to be found in the pattern recognition literature.</span><span class="sxs-lookup"><span data-stu-id="519e2-230">This is perhaps the best known database to be found in the pattern recognition literature.</span></span> <span data-ttu-id="519e2-231">The dataset is relatively small, containing 50 examples each of petal measurements from three iris varieties.</span><span class="sxs-lookup"><span data-stu-id="519e2-231">The dataset is relatively small, containing 50 examples each of petal measurements from three iris varieties.</span></span>
<p></p><span data-ttu-id="519e2-232">
<b>Usage:</b> Predict the iris type from the measurements.</span><span class="sxs-lookup"><span data-stu-id="519e2-232">
<b>Usage:</b> Predict the iris type from the measurements.</span></span>  
<p></p><span data-ttu-id="519e2-233">
<b>Related Research:</b> Fisher, R.A.</span><span class="sxs-lookup"><span data-stu-id="519e2-233">
<b>Related Research:</b> Fisher, R.A.</span></span> <span data-ttu-id="519e2-234">(1988).</span><span class="sxs-lookup"><span data-stu-id="519e2-234">(1988).</span></span> <span data-ttu-id="519e2-235">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-235">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-236">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-236">Irvine, CA: University of California, School of Information and Computer Science</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-237">Movie Tweets</span><span class="sxs-lookup"><span data-stu-id="519e2-237">Movie Tweets</span></span></td>
  <td>
<span data-ttu-id="519e2-238">The dataset is an extended version of the Movie Tweetings dataset.</span><span class="sxs-lookup"><span data-stu-id="519e2-238">The dataset is an extended version of the Movie Tweetings dataset.</span></span> <span data-ttu-id="519e2-239">The dataset has 170K ratings for movies, extracted from well-structured tweets on Twitter.</span><span class="sxs-lookup"><span data-stu-id="519e2-239">The dataset has 170K ratings for movies, extracted from well-structured tweets on Twitter.</span></span> <span data-ttu-id="519e2-240">Each instance represents a tweet and is a tuple: user ID, IMDB movie ID, rating, timestamp, numer of favorites for this tweet, and number of retweets of this tweet.</span><span class="sxs-lookup"><span data-stu-id="519e2-240">Each instance represents a tweet and is a tuple: user ID, IMDB movie ID, rating, timestamp, numer of favorites for this tweet, and number of retweets of this tweet.</span></span> <span data-ttu-id="519e2-241">The dataset was made available by A. Said, S. Dooms, B. Loni and D. Tikk for Recommender Systems Challenge 2014.</span><span class="sxs-lookup"><span data-stu-id="519e2-241">The dataset was made available by A. Said, S. Dooms, B. Loni and D. Tikk for Recommender Systems Challenge 2014.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-242">MPG data for various automobiles</span><span class="sxs-lookup"><span data-stu-id="519e2-242">MPG data for various automobiles</span></span></td>
  <td>
<span data-ttu-id="519e2-243">This dataset is a slightly modified version of the dataset provided by the StatLib library of Carnegie Mellon University.</span><span class="sxs-lookup"><span data-stu-id="519e2-243">This dataset is a slightly modified version of the dataset provided by the StatLib library of Carnegie Mellon University.</span></span> <span data-ttu-id="519e2-244">The dataset was used in the 1983 American Statistical Association Exposition.</span><span class="sxs-lookup"><span data-stu-id="519e2-244">The dataset was used in the 1983 American Statistical Association Exposition.</span></span>
<p></p>
<span data-ttu-id="519e2-245">The data lists fuel consumption for various automobiles in miles per gallon.</span><span class="sxs-lookup"><span data-stu-id="519e2-245">The data lists fuel consumption for various automobiles in miles per gallon.</span></span> <span data-ttu-id="519e2-246">It also includes information such as the number of cylinders, engine displacement, horsepower, total weight, and acceleration.</span><span class="sxs-lookup"><span data-stu-id="519e2-246">It also includes information such as the number of cylinders, engine displacement, horsepower, total weight, and acceleration.</span></span>
<p></p><span data-ttu-id="519e2-247">
<b>Usage:</b> Predict fuel economy based on three multivalued discrete attributes and five continuous attributes.</span><span class="sxs-lookup"><span data-stu-id="519e2-247">
<b>Usage:</b> Predict fuel economy based on three multivalued discrete attributes and five continuous attributes.</span></span> 
<p></p><span data-ttu-id="519e2-248">
<b>Related Research:</b> StatLib, Carnegie Mellon University, (1993).</span><span class="sxs-lookup"><span data-stu-id="519e2-248">
<b>Related Research:</b> StatLib, Carnegie Mellon University, (1993).</span></span> <span data-ttu-id="519e2-249">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-249">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-250">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-250">Irvine, CA: University of California, School of Information and Computer Science</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-251">Pima Indians Diabetes Binary Classification dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-251">Pima Indians Diabetes Binary Classification dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-252">A subset of data from the National Institute of Diabetes and Digestive and Kidney Diseases database.</span><span class="sxs-lookup"><span data-stu-id="519e2-252">A subset of data from the National Institute of Diabetes and Digestive and Kidney Diseases database.</span></span> <span data-ttu-id="519e2-253">The dataset was filtered to focus on female patients of Pima Indian heritage.</span><span class="sxs-lookup"><span data-stu-id="519e2-253">The dataset was filtered to focus on female patients of Pima Indian heritage.</span></span> <span data-ttu-id="519e2-254">The data includes medical data such as glucose and insulin levels, as well as lifestyle factors.</span><span class="sxs-lookup"><span data-stu-id="519e2-254">The data includes medical data such as glucose and insulin levels, as well as lifestyle factors.</span></span>
<p></p><span data-ttu-id="519e2-255">
<b>Usage:</b> Predict whether the subject has diabetes (binary classification).</span><span class="sxs-lookup"><span data-stu-id="519e2-255">
<b>Usage:</b> Predict whether the subject has diabetes (binary classification).</span></span> 
<p></p><span data-ttu-id="519e2-256">
<b>Related Research:</b> Sigillito, V. (1990).</span><span class="sxs-lookup"><span data-stu-id="519e2-256">
<b>Related Research:</b> Sigillito, V. (1990).</span></span> <span data-ttu-id="519e2-257">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml"</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-257">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml"</a>.</span></span> <span data-ttu-id="519e2-258">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-258">Irvine, CA: University of California, School of Information and Computer Science</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-259">Restaurant customer data</span><span class="sxs-lookup"><span data-stu-id="519e2-259">Restaurant customer data</span></span></td>
  <td>
<span data-ttu-id="519e2-260">A set of metadata about customers, including demographics and preferences.</span><span class="sxs-lookup"><span data-stu-id="519e2-260">A set of metadata about customers, including demographics and preferences.</span></span>
<p></p><span data-ttu-id="519e2-261">
<b>Usage:</b> Use this dataset, in combination with the other two restaurant datasets, to train and test a recommender system.</span><span class="sxs-lookup"><span data-stu-id="519e2-261">
<b>Usage:</b> Use this dataset, in combination with the other two restaurant datasets, to train and test a recommender system.</span></span> 
<p></p><span data-ttu-id="519e2-262">
<b>Related Research:</b> Bache, K. and Lichman, M. (2013).</span><span class="sxs-lookup"><span data-stu-id="519e2-262">
<b>Related Research:</b> Bache, K. and Lichman, M. (2013).</span></span> <span data-ttu-id="519e2-263">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-263">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-264">Irvine, CA: University of California, School of Information and Computer Science.</span><span class="sxs-lookup"><span data-stu-id="519e2-264">Irvine, CA: University of California, School of Information and Computer Science.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-265">Restaurant feature data</span><span class="sxs-lookup"><span data-stu-id="519e2-265">Restaurant feature data</span></span></td>
  <td>
<span data-ttu-id="519e2-266">A set of metadata about restaurants and their features, such as food type, dining style, and location.</span><span class="sxs-lookup"><span data-stu-id="519e2-266">A set of metadata about restaurants and their features, such as food type, dining style, and location.</span></span>
<p></p><span data-ttu-id="519e2-267">
<b>Usage:</b> Use this dataset, in combination with the other two restaurant datasets, to train and test a recommender system.</span><span class="sxs-lookup"><span data-stu-id="519e2-267">
<b>Usage:</b> Use this dataset, in combination with the other two restaurant datasets, to train and test a recommender system.</span></span> 
<p></p><span data-ttu-id="519e2-268">
<b>Related Research:</b> Bache, K. and Lichman, M. (2013).</span><span class="sxs-lookup"><span data-stu-id="519e2-268">
<b>Related Research:</b> Bache, K. and Lichman, M. (2013).</span></span> <span data-ttu-id="519e2-269">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-269">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-270">Irvine, CA: University of California, School of Information and Computer Science.</span><span class="sxs-lookup"><span data-stu-id="519e2-270">Irvine, CA: University of California, School of Information and Computer Science.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-271">Restaurant ratings</span><span class="sxs-lookup"><span data-stu-id="519e2-271">Restaurant ratings</span></span></td>
  <td>
<span data-ttu-id="519e2-272">Contains ratings given by users to restaurants on a scale from 0 to 2.</span><span class="sxs-lookup"><span data-stu-id="519e2-272">Contains ratings given by users to restaurants on a scale from 0 to 2.</span></span>
<p></p><span data-ttu-id="519e2-273">
<b>Usage:</b> Use this dataset, in combination with the other two restaurant datasets, to train and test a recommender system.</span><span class="sxs-lookup"><span data-stu-id="519e2-273">
<b>Usage:</b> Use this dataset, in combination with the other two restaurant datasets, to train and test a recommender system.</span></span> 
<p></p><span data-ttu-id="519e2-274">
<b>Related Research:</b> Bache, K. and Lichman, M. (2013).</span><span class="sxs-lookup"><span data-stu-id="519e2-274">
<b>Related Research:</b> Bache, K. and Lichman, M. (2013).</span></span> <span data-ttu-id="519e2-275">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-275">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-276">Irvine, CA: University of California, School of Information and Computer Science.</span><span class="sxs-lookup"><span data-stu-id="519e2-276">Irvine, CA: University of California, School of Information and Computer Science.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-277">Steel Annealing multi-class dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-277">Steel Annealing multi-class dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-278">This dataset contains a series of records from steel annealing trials.</span><span class="sxs-lookup"><span data-stu-id="519e2-278">This dataset contains a series of records from steel annealing trials.</span></span> <span data-ttu-id="519e2-279">It contains the physical attributes (width, thickness, type (coil, sheet, etc.) of the resulting steel types.</span><span class="sxs-lookup"><span data-stu-id="519e2-279">It contains the physical attributes (width, thickness, type (coil, sheet, etc.) of the resulting steel types.</span></span>
<p></p><span data-ttu-id="519e2-280">
<b>Usage:</b> Predict any of two numeric class attributes; hardness or strength.</span><span class="sxs-lookup"><span data-stu-id="519e2-280">
<b>Usage:</b> Predict any of two numeric class attributes; hardness or strength.</span></span> <span data-ttu-id="519e2-281">You might also analyze correlations among attributes.</span><span class="sxs-lookup"><span data-stu-id="519e2-281">You might also analyze correlations among attributes.</span></span>
<p></p>
<span data-ttu-id="519e2-282">Steel grades follow a set standard, defined by SAE and other organizations.</span><span class="sxs-lookup"><span data-stu-id="519e2-282">Steel grades follow a set standard, defined by SAE and other organizations.</span></span> <span data-ttu-id="519e2-283">You are looking for a specific 'grade' (the class variable) and want to understand the values needed.</span><span class="sxs-lookup"><span data-stu-id="519e2-283">You are looking for a specific 'grade' (the class variable) and want to understand the values needed.</span></span> 
<p></p><span data-ttu-id="519e2-284">
<b>Related Research:</b> Sterling, D. & Buntine, W. (NA).</span><span class="sxs-lookup"><span data-stu-id="519e2-284">
<b>Related Research:</b> Sterling, D. & Buntine, W. (NA).</span></span> <span data-ttu-id="519e2-285">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-285">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-286">Irvine, CA: University of California, School of Information and Computer Science</span><span class="sxs-lookup"><span data-stu-id="519e2-286">Irvine, CA: University of California, School of Information and Computer Science</span></span>
<p></p>
<span data-ttu-id="519e2-287">A useful guide to steel grades can be found here: <a href="https://otk-sitecore-prod-v2-cdn.azureedge.net/-/media/from-sharepoint/documents/product/outokumpu-steel-grades-properties-global-standards.pdf">https://otk-sitecore-prod-v2-cdn.azureedge.net/-/media/from-sharepoint/documents/product/outokumpu-steel-grades-properties-global-standards.pdf</a>
  </span><span class="sxs-lookup"><span data-stu-id="519e2-287">A useful guide to steel grades can be found here: <a href="https://otk-sitecore-prod-v2-cdn.azureedge.net/-/media/from-sharepoint/documents/product/outokumpu-steel-grades-properties-global-standards.pdf">https://otk-sitecore-prod-v2-cdn.azureedge.net/-/media/from-sharepoint/documents/product/outokumpu-steel-grades-properties-global-standards.pdf</a>
  </span></span></td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-288">Telescope data</span><span class="sxs-lookup"><span data-stu-id="519e2-288">Telescope data</span></span></td>
  <td>
<span data-ttu-id="519e2-289">Record of high energy gamma particle bursts along with background noise, both simulated using a Monte Carlo process.</span><span class="sxs-lookup"><span data-stu-id="519e2-289">Record of high energy gamma particle bursts along with background noise, both simulated using a Monte Carlo process.</span></span>
<p></p>
<span data-ttu-id="519e2-290">The intent of the simulation was to improve the accuracy of ground-based atmospheric Cherenkov gamma telescopes.</span><span class="sxs-lookup"><span data-stu-id="519e2-290">The intent of the simulation was to improve the accuracy of ground-based atmospheric Cherenkov gamma telescopes.</span></span> <span data-ttu-id="519e2-291">This is done by using statistical methods to differentiate between the desired signal (Cherenkov radiation showers) and background noise (hadronic showers initiated by cosmic rays in the upper atmosphere).</span><span class="sxs-lookup"><span data-stu-id="519e2-291">This is done by using statistical methods to differentiate between the desired signal (Cherenkov radiation showers) and background noise (hadronic showers initiated by cosmic rays in the upper atmosphere).</span></span>
<p></p>
<span data-ttu-id="519e2-292">The data has been pre-processed to create an elongated cluster with the long axis is oriented towards the camera center.</span><span class="sxs-lookup"><span data-stu-id="519e2-292">The data has been pre-processed to create an elongated cluster with the long axis is oriented towards the camera center.</span></span> <span data-ttu-id="519e2-293">The characteristics of this ellipse (often called Hillas parameters) are among the image parameters that can be used for discrimination.</span><span class="sxs-lookup"><span data-stu-id="519e2-293">The characteristics of this ellipse (often called Hillas parameters) are among the image parameters that can be used for discrimination.</span></span>
<p></p><span data-ttu-id="519e2-294">
<b>Usage:</b> Predict whether image of a shower represents signal or background noise.</span><span class="sxs-lookup"><span data-stu-id="519e2-294">
<b>Usage:</b> Predict whether image of a shower represents signal or background noise.</span></span>
<p></p><span data-ttu-id="519e2-295">
<b>Notes:</b> Simple classification accuracy is not meaningful for this data, since classifying a background event as signal is worse than classifying a signal event as background.</span><span class="sxs-lookup"><span data-stu-id="519e2-295">
<b>Notes:</b> Simple classification accuracy is not meaningful for this data, since classifying a background event as signal is worse than classifying a signal event as background.</span></span> <span data-ttu-id="519e2-296">For comparison of different classifiers, the ROC graph should be used.</span><span class="sxs-lookup"><span data-stu-id="519e2-296">For comparison of different classifiers, the ROC graph should be used.</span></span> <span data-ttu-id="519e2-297">The probability of accepting a background event as signal must be below one of the following thresholds: 0.01, 0.02, 0.05, 0.1, or 0.2.</span><span class="sxs-lookup"><span data-stu-id="519e2-297">The probability of accepting a background event as signal must be below one of the following thresholds: 0.01, 0.02, 0.05, 0.1, or 0.2.</span></span>
<p></p>
<span data-ttu-id="519e2-298">Also, note that the number of background events (h, for hadronic showers) is underestimated.</span><span class="sxs-lookup"><span data-stu-id="519e2-298">Also, note that the number of background events (h, for hadronic showers) is underestimated.</span></span> <span data-ttu-id="519e2-299">In real measurements, the h or noise class represents the majority of events.</span><span class="sxs-lookup"><span data-stu-id="519e2-299">In real measurements, the h or noise class represents the majority of events.</span></span> 
<p></p><span data-ttu-id="519e2-300">
<b>Related Research:</b> Bock, R.K.</span><span class="sxs-lookup"><span data-stu-id="519e2-300">
<b>Related Research:</b> Bock, R.K.</span></span> <span data-ttu-id="519e2-301">(1995).</span><span class="sxs-lookup"><span data-stu-id="519e2-301">(1995).</span></span> <span data-ttu-id="519e2-302">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-302">UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>.</span></span> <span data-ttu-id="519e2-303">Irvine, CA: University of California, School of Information</span><span class="sxs-lookup"><span data-stu-id="519e2-303">Irvine, CA: University of California, School of Information</span></span> </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-304">Weather Dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-304">Weather Dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-305">Hourly land-based weather observations from NOAA (<a href="http://az754797.vo.msecnd.net/data/WeatherDataset.csv">merged data from 201304 to 201310</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-305">Hourly land-based weather observations from NOAA (<a href="http://az754797.vo.msecnd.net/data/WeatherDataset.csv">merged data from 201304 to 201310</a>).</span></span>
<p></p>
<span data-ttu-id="519e2-306">The weather data covers observations made from airport weather stations, covering the time period April-October 2013.</span><span class="sxs-lookup"><span data-stu-id="519e2-306">The weather data covers observations made from airport weather stations, covering the time period April-October 2013.</span></span> <span data-ttu-id="519e2-307">Before uploading to Azure Machine Learning Studio, the dataset was processed as follows:</span><span class="sxs-lookup"><span data-stu-id="519e2-307">Before uploading to Azure Machine Learning Studio, the dataset was processed as follows:</span></span>
<ul>
  <li><span data-ttu-id="519e2-308">Weather station IDs were mapped to corresponding airport IDs</span><span class="sxs-lookup"><span data-stu-id="519e2-308">Weather station IDs were mapped to corresponding airport IDs</span></span></li>
  <li><span data-ttu-id="519e2-309">Weather stations not associated with the 70 busiest airports were filtered out</span><span class="sxs-lookup"><span data-stu-id="519e2-309">Weather stations not associated with the 70 busiest airports were filtered out</span></span></li>
  <li><span data-ttu-id="519e2-310">The Date column was split into separate Year, Month, and Day columns</span><span class="sxs-lookup"><span data-stu-id="519e2-310">The Date column was split into separate Year, Month, and Day columns</span></span></li>
  <li><span data-ttu-id="519e2-311">The following columns were selected: AirportID, Year, Month, Day, Time, TimeZone, SkyCondition, Visibility, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, WindSpeed, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, Altimeter</span><span class="sxs-lookup"><span data-stu-id="519e2-311">The following columns were selected: AirportID, Year, Month, Day, Time, TimeZone, SkyCondition, Visibility, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, WindSpeed, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, Altimeter</span></span></li>
</ul>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-312">Wikipedia SP 500 Dataset</span><span class="sxs-lookup"><span data-stu-id="519e2-312">Wikipedia SP 500 Dataset</span></span></td>
  <td>
<span data-ttu-id="519e2-313">Data is derived from Wikipedia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) based on articles of each S&P 500 company, stored as XML data.</span><span class="sxs-lookup"><span data-stu-id="519e2-313">Data is derived from Wikipedia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) based on articles of each S&P 500 company, stored as XML data.</span></span>
<p></p>
<span data-ttu-id="519e2-314">Before uploading to Azure Machine Learning Studio, the dataset was processed as follows:</span><span class="sxs-lookup"><span data-stu-id="519e2-314">Before uploading to Azure Machine Learning Studio, the dataset was processed as follows:</span></span>
<ul>
  <li><span data-ttu-id="519e2-315">Extract text content for each specific company</span><span class="sxs-lookup"><span data-stu-id="519e2-315">Extract text content for each specific company</span></span></li>
  <li><span data-ttu-id="519e2-316">Remove wiki formatting</span><span class="sxs-lookup"><span data-stu-id="519e2-316">Remove wiki formatting</span></span></li>
  <li><span data-ttu-id="519e2-317">Remove non-alphanumeric characters</span><span class="sxs-lookup"><span data-stu-id="519e2-317">Remove non-alphanumeric characters</span></span></li>
  <li><span data-ttu-id="519e2-318">Convert all text to lowercase</span><span class="sxs-lookup"><span data-stu-id="519e2-318">Convert all text to lowercase</span></span></li>
  <li><span data-ttu-id="519e2-319">Known company categories were added</span><span class="sxs-lookup"><span data-stu-id="519e2-319">Known company categories were added</span></span></li>
</ul>
<p></p>
<span data-ttu-id="519e2-320">Note that for some companies an article could not be found, so the number of records is less than 500.</span><span class="sxs-lookup"><span data-stu-id="519e2-320">Note that for some companies an article could not be found, so the number of records is less than 500.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-321"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></span><span class="sxs-lookup"><span data-stu-id="519e2-321"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></span></span></td>
  <td>
<span data-ttu-id="519e2-322">The dataset contains customer data and indications about their response to a direct mailing campaign.</span><span class="sxs-lookup"><span data-stu-id="519e2-322">The dataset contains customer data and indications about their response to a direct mailing campaign.</span></span> <span data-ttu-id="519e2-323">Each row represents a customer.</span><span class="sxs-lookup"><span data-stu-id="519e2-323">Each row represents a customer.</span></span> <span data-ttu-id="519e2-324">The dataset contains nine features about user demographics and past behavior, and three label columns (visit, conversion, and spend).</span><span class="sxs-lookup"><span data-stu-id="519e2-324">The dataset contains nine features about user demographics and past behavior, and three label columns (visit, conversion, and spend).</span></span>  <span data-ttu-id="519e2-325">Visit is a binary column that indicates that a customer visited after the marketing campaign.</span><span class="sxs-lookup"><span data-stu-id="519e2-325">Visit is a binary column that indicates that a customer visited after the marketing campaign.</span></span> <span data-ttu-id="519e2-326">Conversion indicates a customer purchased something.</span><span class="sxs-lookup"><span data-stu-id="519e2-326">Conversion indicates a customer purchased something.</span></span> <span data-ttu-id="519e2-327">Spend is the amount that was spent.</span><span class="sxs-lookup"><span data-stu-id="519e2-327">Spend is the amount that was spent.</span></span>  <span data-ttu-id="519e2-328">The dataset was made available by Kevin Hillstrom for MineThatData E-Mail Analytics And Data Mining Challenge.</span><span class="sxs-lookup"><span data-stu-id="519e2-328">The dataset was made available by Kevin Hillstrom for MineThatData E-Mail Analytics And Data Mining Challenge.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-329"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></span><span class="sxs-lookup"><span data-stu-id="519e2-329"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></span></span></td>
  <td>
<span data-ttu-id="519e2-330">Features of test examples in the RCV1-V2 Reuters news dataset.</span><span class="sxs-lookup"><span data-stu-id="519e2-330">Features of test examples in the RCV1-V2 Reuters news dataset.</span></span> <span data-ttu-id="519e2-331">The dataset has 781K news articles along with their IDs (first column of the dataset).</span><span class="sxs-lookup"><span data-stu-id="519e2-331">The dataset has 781K news articles along with their IDs (first column of the dataset).</span></span> <span data-ttu-id="519e2-332">Each article is tokenized, stopworded, and stemmed.</span><span class="sxs-lookup"><span data-stu-id="519e2-332">Each article is tokenized, stopworded, and stemmed.</span></span> <span data-ttu-id="519e2-333">The dataset was made available by David.</span><span class="sxs-lookup"><span data-stu-id="519e2-333">The dataset was made available by David.</span></span> <span data-ttu-id="519e2-334">D.</span><span class="sxs-lookup"><span data-stu-id="519e2-334">D.</span></span> <span data-ttu-id="519e2-335">Lewis.</span><span class="sxs-lookup"><span data-stu-id="519e2-335">Lewis.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-336"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></span><span class="sxs-lookup"><span data-stu-id="519e2-336"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></span></span></td>
  <td>
<span data-ttu-id="519e2-337">Features of training examples in the RCV1-V2 Reuters news dataset.</span><span class="sxs-lookup"><span data-stu-id="519e2-337">Features of training examples in the RCV1-V2 Reuters news dataset.</span></span> <span data-ttu-id="519e2-338">The dataset has 23K news articles along with their IDs (first column of the dataset).</span><span class="sxs-lookup"><span data-stu-id="519e2-338">The dataset has 23K news articles along with their IDs (first column of the dataset).</span></span> <span data-ttu-id="519e2-339">Each article is tokenized, stopworded, and stemmed.</span><span class="sxs-lookup"><span data-stu-id="519e2-339">Each article is tokenized, stopworded, and stemmed.</span></span> <span data-ttu-id="519e2-340">The dataset was made available by David.</span><span class="sxs-lookup"><span data-stu-id="519e2-340">The dataset was made available by David.</span></span> <span data-ttu-id="519e2-341">D.</span><span class="sxs-lookup"><span data-stu-id="519e2-341">D.</span></span> <span data-ttu-id="519e2-342">Lewis.</span><span class="sxs-lookup"><span data-stu-id="519e2-342">Lewis.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-343"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a></span><span class="sxs-lookup"><span data-stu-id="519e2-343"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a></span></span><br></td>
  <td>
<span data-ttu-id="519e2-344">Dataset from the KDD Cup 1999 Knowledge Discovery and Data Mining Tools Competition (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-344">Dataset from the KDD Cup 1999 Knowledge Discovery and Data Mining Tools Competition (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).</span></span>
<p></p>
<span data-ttu-id="519e2-345">The dataset was downloaded and stored in Azure Blob storage (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) and includes both training and testing datasets.</span><span class="sxs-lookup"><span data-stu-id="519e2-345">The dataset was downloaded and stored in Azure Blob storage (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) and includes both training and testing datasets.</span></span> <span data-ttu-id="519e2-346">The training dataset has approximately 126K rows and 43 columns, including the labels.</span><span class="sxs-lookup"><span data-stu-id="519e2-346">The training dataset has approximately 126K rows and 43 columns, including the labels.</span></span> <span data-ttu-id="519e2-347">Three columns are part of the label information, and 40 columns, consisting of numeric and string/categorical features, are available for training the model.</span><span class="sxs-lookup"><span data-stu-id="519e2-347">Three columns are part of the label information, and 40 columns, consisting of numeric and string/categorical features, are available for training the model.</span></span> <span data-ttu-id="519e2-348">The test data has approximately 22.5K test examples with the same 43 columns as in the training data.</span><span class="sxs-lookup"><span data-stu-id="519e2-348">The test data has approximately 22.5K test examples with the same 43 columns as in the training data.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-349"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></span><span class="sxs-lookup"><span data-stu-id="519e2-349"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></span></span></td>
  <td>
<span data-ttu-id="519e2-350">Topic assignments for news articles in the RCV1-V2 Reuters news dataset.</span><span class="sxs-lookup"><span data-stu-id="519e2-350">Topic assignments for news articles in the RCV1-V2 Reuters news dataset.</span></span> <span data-ttu-id="519e2-351">A news article can be assigned to several topics.</span><span class="sxs-lookup"><span data-stu-id="519e2-351">A news article can be assigned to several topics.</span></span> <span data-ttu-id="519e2-352">The format of each row is "&lt;topic name&gt; &lt;document id&gt; 1".</span><span class="sxs-lookup"><span data-stu-id="519e2-352">The format of each row is "&lt;topic name&gt; &lt;document id&gt; 1".</span></span> <span data-ttu-id="519e2-353">The dataset contains 2.6M topic assignments.</span><span class="sxs-lookup"><span data-stu-id="519e2-353">The dataset contains 2.6M topic assignments.</span></span> <span data-ttu-id="519e2-354">The dataset was made available by David.</span><span class="sxs-lookup"><span data-stu-id="519e2-354">The dataset was made available by David.</span></span> <span data-ttu-id="519e2-355">D.</span><span class="sxs-lookup"><span data-stu-id="519e2-355">D.</span></span> <span data-ttu-id="519e2-356">Lewis.</span><span class="sxs-lookup"><span data-stu-id="519e2-356">Lewis.</span></span>
  </td>
</tr>

<tr>
  <td><span data-ttu-id="519e2-357"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></span><span class="sxs-lookup"><span data-stu-id="519e2-357"><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></span></span></td>
  <td>
<span data-ttu-id="519e2-358">This data comes from the KDD Cup 2010 Student performance evaluation challenge (<a href="http://www.kdd.org/kdd-cup/view/kdd-cup-2010-student-performance-evaluation">student performance evaluation</a>).</span><span class="sxs-lookup"><span data-stu-id="519e2-358">This data comes from the KDD Cup 2010 Student performance evaluation challenge (<a href="http://www.kdd.org/kdd-cup/view/kdd-cup-2010-student-performance-evaluation">student performance evaluation</a>).</span></span> <span data-ttu-id="519e2-359">The data used is the Algebra_2008_2009 training set (Stamper, J., Niculescu-Mizil, A., Ritter, S., Gordon, G.J., & Koedinger, K.R.</span><span class="sxs-lookup"><span data-stu-id="519e2-359">The data used is the Algebra_2008_2009 training set (Stamper, J., Niculescu-Mizil, A., Ritter, S., Gordon, G.J., & Koedinger, K.R.</span></span> <span data-ttu-id="519e2-360">(2010).</span><span class="sxs-lookup"><span data-stu-id="519e2-360">(2010).</span></span> <span data-ttu-id="519e2-361">Algebra I 2008-2009.</span><span class="sxs-lookup"><span data-stu-id="519e2-361">Algebra I 2008-2009.</span></span> <span data-ttu-id="519e2-362">Challenge dataset from KDD Cup 2010 Educational Data Mining Challenge.</span><span class="sxs-lookup"><span data-stu-id="519e2-362">Challenge dataset from KDD Cup 2010 Educational Data Mining Challenge.</span></span> <span data-ttu-id="519e2-363">Find it at <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a>.</span><span class="sxs-lookup"><span data-stu-id="519e2-363">Find it at <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a>.</span></span>
<p></p>
<span data-ttu-id="519e2-364">The dataset was downloaded and stored in Azure Blob storage (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) and contains log files from a student tutoring system.</span><span class="sxs-lookup"><span data-stu-id="519e2-364">The dataset was downloaded and stored in Azure Blob storage (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) and contains log files from a student tutoring system.</span></span> <span data-ttu-id="519e2-365">The supplied features include problem ID and its brief description, student ID, timestamp, and how many attempts the student made before solving the problem in the right way.</span><span class="sxs-lookup"><span data-stu-id="519e2-365">The supplied features include problem ID and its brief description, student ID, timestamp, and how many attempts the student made before solving the problem in the right way.</span></span> <span data-ttu-id="519e2-366">The original dataset has 8.9M records; this dataset has been down-sampled to the first 100K rows.</span><span class="sxs-lookup"><span data-stu-id="519e2-366">The original dataset has 8.9M records; this dataset has been down-sampled to the first 100K rows.</span></span> <span data-ttu-id="519e2-367">The dataset has 23 tab-separated columns of various types: numeric, categorical, and timestamp.</span><span class="sxs-lookup"><span data-stu-id="519e2-367">The dataset has 23 tab-separated columns of various types: numeric, categorical, and timestamp.</span></span>
  </td>
</tr>

</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
