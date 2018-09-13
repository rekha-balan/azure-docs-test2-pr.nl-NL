---
title: Azure Machine Learning Model Data Collection API reference | Microsoft Docs
description: Azure Machine Learning Model Data Collection API reference.
services: machine-learning
author: aashishb
ms.author: aashishb
manager: hjerez
ms.reviewer: jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 09/12/2017
ms.openlocfilehash: d9fee56d7748cdfd34f982fe79467f7d61c54926
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869954"
---
# <a name="azure-machine-learning-model-data-collection-api-reference"></a><span data-ttu-id="620da-103">Azure Machine Learning Model Data Collection API reference</span><span class="sxs-lookup"><span data-stu-id="620da-103">Azure Machine Learning Model Data Collection API reference</span></span>

<span data-ttu-id="620da-104">Model data collection allows you to archive model inputs and predictions from a machine learning web service.</span><span class="sxs-lookup"><span data-stu-id="620da-104">Model data collection allows you to archive model inputs and predictions from a machine learning web service.</span></span> <span data-ttu-id="620da-105">See the [model data collection how-to guide](how-to-use-model-data-collection.md) to understand how to install `azureml.datacollector` on your Windows and Linux machine.</span><span class="sxs-lookup"><span data-stu-id="620da-105">See the [model data collection how-to guide](how-to-use-model-data-collection.md) to understand how to install `azureml.datacollector` on your Windows and Linux machine.</span></span>

<span data-ttu-id="620da-106">In this API reference guide, we use a step-by-step approach on how to collect model inputs and predictions from a machine learning web service.</span><span class="sxs-lookup"><span data-stu-id="620da-106">In this API reference guide, we use a step-by-step approach on how to collect model inputs and predictions from a machine learning web service.</span></span>

## <a name="enable-model-data-collection-in-azure-ml-workbench-environment"></a><span data-ttu-id="620da-107">Enable model data collection in Azure ML Workbench environment</span><span class="sxs-lookup"><span data-stu-id="620da-107">Enable model data collection in Azure ML Workbench environment</span></span>

 <span data-ttu-id="620da-108">Look for conda\_dependencies.yml file in your project under the aml_config folder and have your conda\_dependencies.yml file include the azureml.datacollector module under the pip section as shown below.</span><span class="sxs-lookup"><span data-stu-id="620da-108">Look for conda\_dependencies.yml file in your project under the aml_config folder and have your conda\_dependencies.yml file include the azureml.datacollector module under the pip section as shown below.</span></span> <span data-ttu-id="620da-109">Note that this is only a subsection of a full conda\_dependencies.yml file:</span><span class="sxs-lookup"><span data-stu-id="620da-109">Note that this is only a subsection of a full conda\_dependencies.yml file:</span></span>

    dependencies:
      - python=3.5.2
      - pip:
        - azureml.datacollector==0.1.0a13

>[!NOTE] 
><span data-ttu-id="620da-110">Currently, you can use the data collector module in Azure ML Workbench by running in docker mode.</span><span class="sxs-lookup"><span data-stu-id="620da-110">Currently, you can use the data collector module in Azure ML Workbench by running in docker mode.</span></span> <span data-ttu-id="620da-111">Local mode may not work for all environments.</span><span class="sxs-lookup"><span data-stu-id="620da-111">Local mode may not work for all environments.</span></span>




## <a name="enable-model-data-collection-in-the-scoring-file"></a><span data-ttu-id="620da-112">Enable model data collection in the scoring file</span><span class="sxs-lookup"><span data-stu-id="620da-112">Enable model data collection in the scoring file</span></span>

<span data-ttu-id="620da-113">In the scoring file that is being used for operationalization, import the data collector module and ModelDataCollector class:</span><span class="sxs-lookup"><span data-stu-id="620da-113">In the scoring file that is being used for operationalization, import the data collector module and ModelDataCollector class:</span></span>

    from azureml.datacollector import ModelDataCollector


## <a name="model-data-collector-instantiation"></a><span data-ttu-id="620da-114">Model data collector instantiation</span><span class="sxs-lookup"><span data-stu-id="620da-114">Model data collector instantiation</span></span>
<span data-ttu-id="620da-115">Instantiate a new instance of a ModelDataCollector:</span><span class="sxs-lookup"><span data-stu-id="620da-115">Instantiate a new instance of a ModelDataCollector:</span></span>

    dc = ModelDataCollector(model_name, identifier='default', feature_names=None, model_management_account_id='unknown', webservice_name='unknown', model_id='unknown', model_version='unknown')

<span data-ttu-id="620da-116">See Class and Parameter details:</span><span class="sxs-lookup"><span data-stu-id="620da-116">See Class and Parameter details:</span></span>

### <a name="class"></a><span data-ttu-id="620da-117">Class</span><span class="sxs-lookup"><span data-stu-id="620da-117">Class</span></span>
| <span data-ttu-id="620da-118">Name</span><span class="sxs-lookup"><span data-stu-id="620da-118">Name</span></span> | <span data-ttu-id="620da-119">Description</span><span class="sxs-lookup"><span data-stu-id="620da-119">Description</span></span> |
|--------------------|--------------------|
| <span data-ttu-id="620da-120">ModelDataCollector</span><span class="sxs-lookup"><span data-stu-id="620da-120">ModelDataCollector</span></span> | <span data-ttu-id="620da-121">A class in azureml.datacollector namespace.</span><span class="sxs-lookup"><span data-stu-id="620da-121">A class in azureml.datacollector namespace.</span></span> <span data-ttu-id="620da-122">An instance of this class will be used to collect model data.</span><span class="sxs-lookup"><span data-stu-id="620da-122">An instance of this class will be used to collect model data.</span></span> <span data-ttu-id="620da-123">A single scoring file can contain multiple ModelDataCollectors.</span><span class="sxs-lookup"><span data-stu-id="620da-123">A single scoring file can contain multiple ModelDataCollectors.</span></span> <span data-ttu-id="620da-124">Each instance should be used for collecting data in one discrete location in the scoring file so that the schema of collected data remains consistent (that is, inputs and prediction)</span><span class="sxs-lookup"><span data-stu-id="620da-124">Each instance should be used for collecting data in one discrete location in the scoring file so that the schema of collected data remains consistent (that is, inputs and prediction)</span></span>|


### <a name="parameters"></a><span data-ttu-id="620da-125">Parameters</span><span class="sxs-lookup"><span data-stu-id="620da-125">Parameters</span></span>

| <span data-ttu-id="620da-126">Name</span><span class="sxs-lookup"><span data-stu-id="620da-126">Name</span></span> | <span data-ttu-id="620da-127">Type</span><span class="sxs-lookup"><span data-stu-id="620da-127">Type</span></span> | <span data-ttu-id="620da-128">Description</span><span class="sxs-lookup"><span data-stu-id="620da-128">Description</span></span> |
|-------------|------------|-------------------------|
| <span data-ttu-id="620da-129">model_name</span><span class="sxs-lookup"><span data-stu-id="620da-129">model_name</span></span> | <span data-ttu-id="620da-130">string</span><span class="sxs-lookup"><span data-stu-id="620da-130">string</span></span> | <span data-ttu-id="620da-131">the name of the model which data is being collected for</span><span class="sxs-lookup"><span data-stu-id="620da-131">the name of the model which data is being collected for</span></span> |
| <span data-ttu-id="620da-132">identifier</span><span class="sxs-lookup"><span data-stu-id="620da-132">identifier</span></span> | <span data-ttu-id="620da-133">string</span><span class="sxs-lookup"><span data-stu-id="620da-133">string</span></span> | <span data-ttu-id="620da-134">the location in code that identifies this data, i.e. 'RawInput' or 'Prediction'</span><span class="sxs-lookup"><span data-stu-id="620da-134">the location in code that identifies this data, i.e. 'RawInput' or 'Prediction'</span></span> |
| <span data-ttu-id="620da-135">feature_names</span><span class="sxs-lookup"><span data-stu-id="620da-135">feature_names</span></span> | <span data-ttu-id="620da-136">list of strings</span><span class="sxs-lookup"><span data-stu-id="620da-136">list of strings</span></span> | <span data-ttu-id="620da-137">a list of feature names that become the csv header when supplied</span><span class="sxs-lookup"><span data-stu-id="620da-137">a list of feature names that become the csv header when supplied</span></span> |
| <span data-ttu-id="620da-138">model_management_account_id</span><span class="sxs-lookup"><span data-stu-id="620da-138">model_management_account_id</span></span> | <span data-ttu-id="620da-139">string</span><span class="sxs-lookup"><span data-stu-id="620da-139">string</span></span> | <span data-ttu-id="620da-140">the identifier for the model management account where this model is stored.</span><span class="sxs-lookup"><span data-stu-id="620da-140">the identifier for the model management account where this model is stored.</span></span> <span data-ttu-id="620da-141">This is populated automatically when models are operationalized through AML</span><span class="sxs-lookup"><span data-stu-id="620da-141">This is populated automatically when models are operationalized through AML</span></span> |
| <span data-ttu-id="620da-142">webservice_name</span><span class="sxs-lookup"><span data-stu-id="620da-142">webservice_name</span></span> | <span data-ttu-id="620da-143">string</span><span class="sxs-lookup"><span data-stu-id="620da-143">string</span></span> | <span data-ttu-id="620da-144">the name of the webservice to which this model is currently deployed.</span><span class="sxs-lookup"><span data-stu-id="620da-144">the name of the webservice to which this model is currently deployed.</span></span> <span data-ttu-id="620da-145">This is populated automatically when models are operationalized through AML</span><span class="sxs-lookup"><span data-stu-id="620da-145">This is populated automatically when models are operationalized through AML</span></span> |
| <span data-ttu-id="620da-146">model_id</span><span class="sxs-lookup"><span data-stu-id="620da-146">model_id</span></span> | <span data-ttu-id="620da-147">string</span><span class="sxs-lookup"><span data-stu-id="620da-147">string</span></span> | <span data-ttu-id="620da-148">The unique identifier for this model in the context of a model management account.</span><span class="sxs-lookup"><span data-stu-id="620da-148">The unique identifier for this model in the context of a model management account.</span></span> <span data-ttu-id="620da-149">this is populated automatically when models are operationalized through AML</span><span class="sxs-lookup"><span data-stu-id="620da-149">this is populated automatically when models are operationalized through AML</span></span> |
| <span data-ttu-id="620da-150">model_version</span><span class="sxs-lookup"><span data-stu-id="620da-150">model_version</span></span> | <span data-ttu-id="620da-151">string</span><span class="sxs-lookup"><span data-stu-id="620da-151">string</span></span> | <span data-ttu-id="620da-152">the version number of this model in the context of a model management account.</span><span class="sxs-lookup"><span data-stu-id="620da-152">the version number of this model in the context of a model management account.</span></span> <span data-ttu-id="620da-153">This is populated automatically when models are operationalized through AML</span><span class="sxs-lookup"><span data-stu-id="620da-153">This is populated automatically when models are operationalized through AML</span></span> |



 

## <a name="collecting-the-model-data"></a><span data-ttu-id="620da-154">Collecting the model data</span><span class="sxs-lookup"><span data-stu-id="620da-154">Collecting the model data</span></span>

<span data-ttu-id="620da-155">You can collect the model data using an instance of the ModelDataCollector created above.</span><span class="sxs-lookup"><span data-stu-id="620da-155">You can collect the model data using an instance of the ModelDataCollector created above.</span></span>

    dc.collect(input_data, user_correlation_id="")

<span data-ttu-id="620da-156">See Method and Parameter details:</span><span class="sxs-lookup"><span data-stu-id="620da-156">See Method and Parameter details:</span></span>

### <a name="method"></a><span data-ttu-id="620da-157">Method</span><span class="sxs-lookup"><span data-stu-id="620da-157">Method</span></span>
| <span data-ttu-id="620da-158">Name</span><span class="sxs-lookup"><span data-stu-id="620da-158">Name</span></span> | <span data-ttu-id="620da-159">Description</span><span class="sxs-lookup"><span data-stu-id="620da-159">Description</span></span> |
|--------------------|--------------------|
| <span data-ttu-id="620da-160">collect</span><span class="sxs-lookup"><span data-stu-id="620da-160">collect</span></span> | <span data-ttu-id="620da-161">Used to collect the data for a model input or prediction</span><span class="sxs-lookup"><span data-stu-id="620da-161">Used to collect the data for a model input or prediction</span></span>|


### <a name="parameters"></a><span data-ttu-id="620da-162">Parameters</span><span class="sxs-lookup"><span data-stu-id="620da-162">Parameters</span></span>

| <span data-ttu-id="620da-163">Name</span><span class="sxs-lookup"><span data-stu-id="620da-163">Name</span></span> | <span data-ttu-id="620da-164">Type</span><span class="sxs-lookup"><span data-stu-id="620da-164">Type</span></span> | <span data-ttu-id="620da-165">Description</span><span class="sxs-lookup"><span data-stu-id="620da-165">Description</span></span> |
|-------------|------------|-------------------------|
| <span data-ttu-id="620da-166">input_data</span><span class="sxs-lookup"><span data-stu-id="620da-166">input_data</span></span> | <span data-ttu-id="620da-167">multiple types</span><span class="sxs-lookup"><span data-stu-id="620da-167">multiple types</span></span> | <span data-ttu-id="620da-168">the data to be collected (currently accepts the types list, numpy.array, pandas.DataFrame, pyspark.sql.DataFrame).</span><span class="sxs-lookup"><span data-stu-id="620da-168">the data to be collected (currently accepts the types list, numpy.array, pandas.DataFrame, pyspark.sql.DataFrame).</span></span> <span data-ttu-id="620da-169">For dataframe types, if a header exists with feature names, this information is included in the data destination (without needing to explicitly pass feature names in the ModelDataCollector constructor)</span><span class="sxs-lookup"><span data-stu-id="620da-169">For dataframe types, if a header exists with feature names, this information is included in the data destination (without needing to explicitly pass feature names in the ModelDataCollector constructor)</span></span> |
| <span data-ttu-id="620da-170">user_correlation_id</span><span class="sxs-lookup"><span data-stu-id="620da-170">user_correlation_id</span></span> | <span data-ttu-id="620da-171">string</span><span class="sxs-lookup"><span data-stu-id="620da-171">string</span></span> | <span data-ttu-id="620da-172">an optional correlation id, which can be provided by the user to correlate this prediction</span><span class="sxs-lookup"><span data-stu-id="620da-172">an optional correlation id, which can be provided by the user to correlate this prediction</span></span> |

