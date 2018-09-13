---
title: Build and deploy a forecasting model using Azure Machine Learning Package for Forecasting.
description: Learn how to build, train, test and deploy a forecasting model using the Azure Machine Learning Package for Forecasting.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: mattcon
author: matthewconners
ms.date: 07/13/2018
ms.openlocfilehash: 60eecf134f067d68326fc23ade8ed2a5a7ae7ac4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856856"
---
# <a name="build-and-deploy-forecasting-models-with-azure-machine-learning"></a><span data-ttu-id="5cf56-103">Build and deploy forecasting models with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5cf56-103">Build and deploy forecasting models with Azure Machine Learning</span></span>

<span data-ttu-id="5cf56-104">In this article, learn how to use **Azure Machine Learning Package for Forecasting** (AMLPF) to quickly build and deploy a forecasting model.</span><span class="sxs-lookup"><span data-stu-id="5cf56-104">In this article, learn how to use **Azure Machine Learning Package for Forecasting** (AMLPF) to quickly build and deploy a forecasting model.</span></span> <span data-ttu-id="5cf56-105">The workflow is as follows:</span><span class="sxs-lookup"><span data-stu-id="5cf56-105">The workflow is as follows:</span></span>

1. <span data-ttu-id="5cf56-106">Load and explore data</span><span class="sxs-lookup"><span data-stu-id="5cf56-106">Load and explore data</span></span>
2. <span data-ttu-id="5cf56-107">Create features</span><span class="sxs-lookup"><span data-stu-id="5cf56-107">Create features</span></span>
3. <span data-ttu-id="5cf56-108">Train and select the best model</span><span class="sxs-lookup"><span data-stu-id="5cf56-108">Train and select the best model</span></span>
4. <span data-ttu-id="5cf56-109">Deploy the model and consume the web service</span><span class="sxs-lookup"><span data-stu-id="5cf56-109">Deploy the model and consume the web service</span></span>

<span data-ttu-id="5cf56-110">Consult the [package reference documentation](https://aka.ms/aml-packages/forecasting) for the full list of transformers and models as well as the detailed reference for each module and class.</span><span class="sxs-lookup"><span data-stu-id="5cf56-110">Consult the [package reference documentation](https://aka.ms/aml-packages/forecasting) for the full list of transformers and models as well as the detailed reference for each module and class.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cf56-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5cf56-111">Prerequisites</span></span>

1. <span data-ttu-id="5cf56-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="5cf56-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

1. <span data-ttu-id="5cf56-113">The following accounts and application must be set up and installed:</span><span class="sxs-lookup"><span data-stu-id="5cf56-113">The following accounts and application must be set up and installed:</span></span>
   - <span data-ttu-id="5cf56-114">An Azure Machine Learning Experimentation account</span><span class="sxs-lookup"><span data-stu-id="5cf56-114">An Azure Machine Learning Experimentation account</span></span> 
   - <span data-ttu-id="5cf56-115">An Azure Machine Learning Model Management account</span><span class="sxs-lookup"><span data-stu-id="5cf56-115">An Azure Machine Learning Model Management account</span></span>
   - <span data-ttu-id="5cf56-116">Azure Machine Learning Workbench installed</span><span class="sxs-lookup"><span data-stu-id="5cf56-116">Azure Machine Learning Workbench installed</span></span> 

 <span data-ttu-id="5cf56-117">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span><span class="sxs-lookup"><span data-stu-id="5cf56-117">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span></span>

1. <span data-ttu-id="5cf56-118">The Azure Machine Learning Package for Forecasting must be installed.</span><span class="sxs-lookup"><span data-stu-id="5cf56-118">The Azure Machine Learning Package for Forecasting must be installed.</span></span> <span data-ttu-id="5cf56-119">Learn how to [install this package here](https://aka.ms/aml-packages/forecasting).</span><span class="sxs-lookup"><span data-stu-id="5cf56-119">Learn how to [install this package here](https://aka.ms/aml-packages/forecasting).</span></span>

## <a name="sample-data-and-jupyter-notebook"></a><span data-ttu-id="5cf56-120">Sample data and Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="5cf56-120">Sample data and Jupyter notebook</span></span>

### <a name="sample-workflow"></a><span data-ttu-id="5cf56-121">Sample workflow</span><span class="sxs-lookup"><span data-stu-id="5cf56-121">Sample workflow</span></span> 
<span data-ttu-id="5cf56-122">The example follows the workflow:</span><span class="sxs-lookup"><span data-stu-id="5cf56-122">The example follows the workflow:</span></span>
 
1. <span data-ttu-id="5cf56-123">**Ingest Data**: Load the dataset and convert it into TimeSeriesDataFrame.</span><span class="sxs-lookup"><span data-stu-id="5cf56-123">**Ingest Data**: Load the dataset and convert it into TimeSeriesDataFrame.</span></span> <span data-ttu-id="5cf56-124">This dataframe is a time series data structure provided by Azure Machine Learning Package for Forecasting, herein referred to as **AMLPF**.</span><span class="sxs-lookup"><span data-stu-id="5cf56-124">This dataframe is a time series data structure provided by Azure Machine Learning Package for Forecasting, herein referred to as **AMLPF**.</span></span>

2. <span data-ttu-id="5cf56-125">**Create Features**: Use various featurization transformers provided by AMLPF to create features.</span><span class="sxs-lookup"><span data-stu-id="5cf56-125">**Create Features**: Use various featurization transformers provided by AMLPF to create features.</span></span>

3. <span data-ttu-id="5cf56-126">**Train and Select Best Model**: Compare the performance of various univariate time series models and machine learning models.</span><span class="sxs-lookup"><span data-stu-id="5cf56-126">**Train and Select Best Model**: Compare the performance of various univariate time series models and machine learning models.</span></span> 

4. <span data-ttu-id="5cf56-127">**Deploy Model**: Deploy the trained model pipeline as a web service via Azure Machine Learning Workbench so it can be consumed by others.</span><span class="sxs-lookup"><span data-stu-id="5cf56-127">**Deploy Model**: Deploy the trained model pipeline as a web service via Azure Machine Learning Workbench so it can be consumed by others.</span></span>

### <a name="get-the-jupyter-notebook"></a><span data-ttu-id="5cf56-128">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="5cf56-128">Get the Jupyter notebook</span></span>

<span data-ttu-id="5cf56-129">Download the notebook to run the code samples described herein yourself.</span><span class="sxs-lookup"><span data-stu-id="5cf56-129">Download the notebook to run the code samples described herein yourself.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5cf56-130">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="5cf56-130">Get the Jupyter notebook</span></span>](https://aka.ms/aml-packages/forecasting/notebooks/sales_forecasting)

### <a name="explore-the-sample-data"></a><span data-ttu-id="5cf56-131">Explore the sample data</span><span class="sxs-lookup"><span data-stu-id="5cf56-131">Explore the sample data</span></span>

<span data-ttu-id="5cf56-132">The machine learning forecasting examples in the follow code samples rely on the [University of Chicago's Dominick's Finer Foods dataset](https://research.chicagobooth.edu/kilts/marketing-databases/dominicks) to forecast orange juice sales.</span><span class="sxs-lookup"><span data-stu-id="5cf56-132">The machine learning forecasting examples in the follow code samples rely on the [University of Chicago's Dominick's Finer Foods dataset](https://research.chicagobooth.edu/kilts/marketing-databases/dominicks) to forecast orange juice sales.</span></span> <span data-ttu-id="5cf56-133">Dominick's was a grocery chain in the Chicago metropolitan area.</span><span class="sxs-lookup"><span data-stu-id="5cf56-133">Dominick's was a grocery chain in the Chicago metropolitan area.</span></span>

### <a name="import-any-dependencies-for-this-sample"></a><span data-ttu-id="5cf56-134">Import any dependencies for this sample</span><span class="sxs-lookup"><span data-stu-id="5cf56-134">Import any dependencies for this sample</span></span>

<span data-ttu-id="5cf56-135">These dependencies must be imported for the following code samples:</span><span class="sxs-lookup"><span data-stu-id="5cf56-135">These dependencies must be imported for the following code samples:</span></span>


```python
import pandas as pd
import numpy as np
import math
import pkg_resources
from datetime import timedelta
import matplotlib
matplotlib.use('agg')
%matplotlib inline
from matplotlib import pyplot as plt

from sklearn.linear_model import Lasso, ElasticNet
from sklearn.ensemble import RandomForestRegressor, GradientBoostingRegressor
from sklearn.neighbors import KNeighborsRegressor

from ftk import TimeSeriesDataFrame, ForecastDataFrame, AzureMLForecastPipeline
from ftk.ts_utils import last_n_periods_split

from ftk.transforms import TimeSeriesImputer, TimeIndexFeaturizer, DropColumns
from ftk.transforms.grain_index_featurizer import GrainIndexFeaturizer
from ftk.models import Arima, SeasonalNaive, Naive, RegressionForecaster, ETS, BestOfForecaster
from ftk.models.forecaster_union import ForecasterUnion
from ftk.model_selection import TSGridSearchCV, RollingOriginValidator

from azuremltkbase.deployment import AMLSettings
from ftk.operationalization.forecast_webservice_factory import ForecastWebserviceFactory
from ftk.operationalization import ScoreContext

from ftk.data import get_a_year_of_daily_weather_data
print('imports done')
```

    imports done
    

## <a name="load-data-and-explore"></a><span data-ttu-id="5cf56-136">Load data and explore</span><span class="sxs-lookup"><span data-stu-id="5cf56-136">Load data and explore</span></span>

<span data-ttu-id="5cf56-137">This code snippet shows the typical process of starting with a raw data set, in this case the [data from Dominick's Finer Foods](https://research.chicagobooth.edu/kilts/marketing-databases/dominicks).</span><span class="sxs-lookup"><span data-stu-id="5cf56-137">This code snippet shows the typical process of starting with a raw data set, in this case the [data from Dominick's Finer Foods](https://research.chicagobooth.edu/kilts/marketing-databases/dominicks).</span></span>  <span data-ttu-id="5cf56-138">You can also use the convenience function [load_dominicks_oj_data](https://docs.microsoft.com/en-us/python/api/ftk.data.dominicks_oj.load_dominicks_oj_data).</span><span class="sxs-lookup"><span data-stu-id="5cf56-138">You can also use the convenience function [load_dominicks_oj_data](https://docs.microsoft.com/en-us/python/api/ftk.data.dominicks_oj.load_dominicks_oj_data).</span></span>


```python
# Load the data into a pandas DataFrame
csv_path = pkg_resources.resource_filename('ftk', 'data/dominicks_oj/dominicks_oj.csv')
whole_df = pd.read_csv(csv_path, low_memory = False)
whole_df.head()
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th><span data-ttu-id="5cf56-139">store</span><span class="sxs-lookup"><span data-stu-id="5cf56-139">store</span></span></th>
      <th><span data-ttu-id="5cf56-140">brand</span><span class="sxs-lookup"><span data-stu-id="5cf56-140">brand</span></span></th>
      <th><span data-ttu-id="5cf56-141">week</span><span class="sxs-lookup"><span data-stu-id="5cf56-141">week</span></span></th>
      <th><span data-ttu-id="5cf56-142">logmove</span><span class="sxs-lookup"><span data-stu-id="5cf56-142">logmove</span></span></th>
      <th><span data-ttu-id="5cf56-143">feat</span><span class="sxs-lookup"><span data-stu-id="5cf56-143">feat</span></span></th>
      <th><span data-ttu-id="5cf56-144">price</span><span class="sxs-lookup"><span data-stu-id="5cf56-144">price</span></span></th>
      <th><span data-ttu-id="5cf56-145">AGE60</span><span class="sxs-lookup"><span data-stu-id="5cf56-145">AGE60</span></span></th>
      <th><span data-ttu-id="5cf56-146">EDUC</span><span class="sxs-lookup"><span data-stu-id="5cf56-146">EDUC</span></span></th>
      <th><span data-ttu-id="5cf56-147">ETHNIC</span><span class="sxs-lookup"><span data-stu-id="5cf56-147">ETHNIC</span></span></th>
      <th><span data-ttu-id="5cf56-148">INCOME</span><span class="sxs-lookup"><span data-stu-id="5cf56-148">INCOME</span></span></th>
      <th><span data-ttu-id="5cf56-149">HHLARGE</span><span class="sxs-lookup"><span data-stu-id="5cf56-149">HHLARGE</span></span></th>
      <th><span data-ttu-id="5cf56-150">WORKWOM</span><span class="sxs-lookup"><span data-stu-id="5cf56-150">WORKWOM</span></span></th>
      <th><span data-ttu-id="5cf56-151">HVAL150</span><span class="sxs-lookup"><span data-stu-id="5cf56-151">HVAL150</span></span></th>
      <th><span data-ttu-id="5cf56-152">SSTRDIST</span><span class="sxs-lookup"><span data-stu-id="5cf56-152">SSTRDIST</span></span></th>
      <th><span data-ttu-id="5cf56-153">SSTRVOL</span><span class="sxs-lookup"><span data-stu-id="5cf56-153">SSTRVOL</span></span></th>
      <th><span data-ttu-id="5cf56-154">CPDIST5</span><span class="sxs-lookup"><span data-stu-id="5cf56-154">CPDIST5</span></span></th>
      <th><span data-ttu-id="5cf56-155">CPWVOL5</span><span class="sxs-lookup"><span data-stu-id="5cf56-155">CPWVOL5</span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="5cf56-156">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-156">0</span></span></th>
      <td><span data-ttu-id="5cf56-157">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-157">2</span></span></td>
      <td><span data-ttu-id="5cf56-158">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-158">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-159">40</span><span class="sxs-lookup"><span data-stu-id="5cf56-159">40</span></span></td>
      <td><span data-ttu-id="5cf56-160">9.02</span><span class="sxs-lookup"><span data-stu-id="5cf56-160">9.02</span></span></td>
      <td><span data-ttu-id="5cf56-161">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-161">0</span></span></td>
      <td><span data-ttu-id="5cf56-162">3.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-162">3.87</span></span></td>
      <td><span data-ttu-id="5cf56-163">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-163">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-164">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-164">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-165">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-165">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-166">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-166">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-167">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-167">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-168">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-168">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-169">0.46</span><span class="sxs-lookup"><span data-stu-id="5cf56-169">0.46</span></span></td>
      <td><span data-ttu-id="5cf56-170">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-170">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-171">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-171">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-172">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-172">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-173">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-173">0.38</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-174">1</span><span class="sxs-lookup"><span data-stu-id="5cf56-174">1</span></span></th>
      <td><span data-ttu-id="5cf56-175">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-175">2</span></span></td>
      <td><span data-ttu-id="5cf56-176">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-176">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-177">46</span><span class="sxs-lookup"><span data-stu-id="5cf56-177">46</span></span></td>
      <td><span data-ttu-id="5cf56-178">8.72</span><span class="sxs-lookup"><span data-stu-id="5cf56-178">8.72</span></span></td>
      <td><span data-ttu-id="5cf56-179">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-179">0</span></span></td>
      <td><span data-ttu-id="5cf56-180">3.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-180">3.87</span></span></td>
      <td><span data-ttu-id="5cf56-181">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-181">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-182">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-182">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-183">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-183">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-184">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-184">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-185">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-185">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-186">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-186">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-187">0.46</span><span class="sxs-lookup"><span data-stu-id="5cf56-187">0.46</span></span></td>
      <td><span data-ttu-id="5cf56-188">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-188">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-189">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-189">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-190">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-190">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-191">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-191">0.38</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-192">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-192">2</span></span></th>
      <td><span data-ttu-id="5cf56-193">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-193">2</span></span></td>
      <td><span data-ttu-id="5cf56-194">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-194">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-195">47</span><span class="sxs-lookup"><span data-stu-id="5cf56-195">47</span></span></td>
      <td><span data-ttu-id="5cf56-196">8.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-196">8.25</span></span></td>
      <td><span data-ttu-id="5cf56-197">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-197">0</span></span></td>
      <td><span data-ttu-id="5cf56-198">3.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-198">3.87</span></span></td>
      <td><span data-ttu-id="5cf56-199">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-199">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-200">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-200">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-201">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-201">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-202">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-202">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-203">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-203">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-204">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-204">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-205">0.46</span><span class="sxs-lookup"><span data-stu-id="5cf56-205">0.46</span></span></td>
      <td><span data-ttu-id="5cf56-206">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-206">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-207">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-207">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-208">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-208">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-209">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-209">0.38</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-210">3</span><span class="sxs-lookup"><span data-stu-id="5cf56-210">3</span></span></th>
      <td><span data-ttu-id="5cf56-211">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-211">2</span></span></td>
      <td><span data-ttu-id="5cf56-212">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-212">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-213">48</span><span class="sxs-lookup"><span data-stu-id="5cf56-213">48</span></span></td>
      <td><span data-ttu-id="5cf56-214">8.99</span><span class="sxs-lookup"><span data-stu-id="5cf56-214">8.99</span></span></td>
      <td><span data-ttu-id="5cf56-215">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-215">0</span></span></td>
      <td><span data-ttu-id="5cf56-216">3.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-216">3.87</span></span></td>
      <td><span data-ttu-id="5cf56-217">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-217">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-218">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-218">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-219">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-219">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-220">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-220">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-221">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-221">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-222">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-222">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-223">0.46</span><span class="sxs-lookup"><span data-stu-id="5cf56-223">0.46</span></span></td>
      <td><span data-ttu-id="5cf56-224">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-224">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-225">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-225">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-226">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-226">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-227">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-227">0.38</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-228">4</span><span class="sxs-lookup"><span data-stu-id="5cf56-228">4</span></span></th>
      <td><span data-ttu-id="5cf56-229">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-229">2</span></span></td>
      <td><span data-ttu-id="5cf56-230">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-230">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-231">50</span><span class="sxs-lookup"><span data-stu-id="5cf56-231">50</span></span></td>
      <td><span data-ttu-id="5cf56-232">9.09</span><span class="sxs-lookup"><span data-stu-id="5cf56-232">9.09</span></span></td>
      <td><span data-ttu-id="5cf56-233">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-233">0</span></span></td>
      <td><span data-ttu-id="5cf56-234">3.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-234">3.87</span></span></td>
      <td><span data-ttu-id="5cf56-235">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-235">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-236">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-236">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-237">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-237">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-238">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-238">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-239">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-239">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-240">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-240">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-241">0.46</span><span class="sxs-lookup"><span data-stu-id="5cf56-241">0.46</span></span></td>
      <td><span data-ttu-id="5cf56-242">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-242">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-243">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-243">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-244">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-244">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-245">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-245">0.38</span></span></td>
    </tr>
  </tbody>
</table>



<span data-ttu-id="5cf56-246">The data consist of weekly sales by brand and store.</span><span class="sxs-lookup"><span data-stu-id="5cf56-246">The data consist of weekly sales by brand and store.</span></span> <span data-ttu-id="5cf56-247">The logarithm of the quantity sold is in the _logmove_ column.</span><span class="sxs-lookup"><span data-stu-id="5cf56-247">The logarithm of the quantity sold is in the _logmove_ column.</span></span> <span data-ttu-id="5cf56-248">The data also includes some customer demographic features.</span><span class="sxs-lookup"><span data-stu-id="5cf56-248">The data also includes some customer demographic features.</span></span> 

<span data-ttu-id="5cf56-249">To model the time series, you need to extract the following elements from this dataframe:</span><span class="sxs-lookup"><span data-stu-id="5cf56-249">To model the time series, you need to extract the following elements from this dataframe:</span></span> 
+ <span data-ttu-id="5cf56-250">A date/time axis</span><span class="sxs-lookup"><span data-stu-id="5cf56-250">A date/time axis</span></span> 
+ <span data-ttu-id="5cf56-251">The sales quantity to be forecast</span><span class="sxs-lookup"><span data-stu-id="5cf56-251">The sales quantity to be forecast</span></span>


```python
# The sales are contained in the 'logmove' column. 
# Values are logarithmic, so exponentiate and round them to get quantity sold
def expround(x):
    return math.floor(math.exp(x) + 0.5)
whole_df['Quantity'] = whole_df['logmove'].apply(expround)

# The time axis is in the 'week' column
# This is the week offset from the week of 1989-09-07 through 1989-09-13 inclusive
# Create new datetime columns containing the start and end of each week period
weekZeroStart = pd.to_datetime('1989-09-07 00:00:00')
weekZeroEnd = pd.to_datetime('1989-09-13 23:59:59')
whole_df['WeekFirstDay'] = whole_df['week'].apply(lambda n: weekZeroStart + timedelta(weeks=n))
whole_df['WeekLastDay'] = whole_df['week'].apply(lambda n: weekZeroEnd + timedelta(weeks=n))
whole_df[['store','brand','WeekLastDay','Quantity']].head()
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th><span data-ttu-id="5cf56-252">store</span><span class="sxs-lookup"><span data-stu-id="5cf56-252">store</span></span></th>
      <th><span data-ttu-id="5cf56-253">brand</span><span class="sxs-lookup"><span data-stu-id="5cf56-253">brand</span></span></th>
      <th><span data-ttu-id="5cf56-254">WeekLastDay</span><span class="sxs-lookup"><span data-stu-id="5cf56-254">WeekLastDay</span></span></th>
      <th><span data-ttu-id="5cf56-255">Quantity</span><span class="sxs-lookup"><span data-stu-id="5cf56-255">Quantity</span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="5cf56-256">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-256">0</span></span></th>
      <td><span data-ttu-id="5cf56-257">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-257">2</span></span></td>
      <td><span data-ttu-id="5cf56-258">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-258">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-259">1990-06-20 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-259">1990-06-20 23:59:59</span></span></td>
      <td><span data-ttu-id="5cf56-260">8256</span><span class="sxs-lookup"><span data-stu-id="5cf56-260">8256</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-261">1</span><span class="sxs-lookup"><span data-stu-id="5cf56-261">1</span></span></th>
      <td><span data-ttu-id="5cf56-262">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-262">2</span></span></td>
      <td><span data-ttu-id="5cf56-263">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-263">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-264">1990-08-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-264">1990-08-01 23:59:59</span></span></td>
      <td><span data-ttu-id="5cf56-265">6144</span><span class="sxs-lookup"><span data-stu-id="5cf56-265">6144</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-266">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-266">2</span></span></th>
      <td><span data-ttu-id="5cf56-267">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-267">2</span></span></td>
      <td><span data-ttu-id="5cf56-268">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-268">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-269">1990-08-08 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-269">1990-08-08 23:59:59</span></span></td>
      <td><span data-ttu-id="5cf56-270">3840</span><span class="sxs-lookup"><span data-stu-id="5cf56-270">3840</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-271">3</span><span class="sxs-lookup"><span data-stu-id="5cf56-271">3</span></span></th>
      <td><span data-ttu-id="5cf56-272">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-272">2</span></span></td>
      <td><span data-ttu-id="5cf56-273">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-273">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-274">1990-08-15 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-274">1990-08-15 23:59:59</span></span></td>
      <td><span data-ttu-id="5cf56-275">8000</span><span class="sxs-lookup"><span data-stu-id="5cf56-275">8000</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-276">4</span><span class="sxs-lookup"><span data-stu-id="5cf56-276">4</span></span></th>
      <td><span data-ttu-id="5cf56-277">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-277">2</span></span></td>
      <td><span data-ttu-id="5cf56-278">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-278">tropicana</span></span></td>
      <td><span data-ttu-id="5cf56-279">1990-08-29 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-279">1990-08-29 23:59:59</span></span></td>
      <td><span data-ttu-id="5cf56-280">8896</span><span class="sxs-lookup"><span data-stu-id="5cf56-280">8896</span></span></td>
    </tr>
  </tbody>
</table>




```python
nseries = whole_df.groupby(['store', 'brand']).ngroups
print('{} time series in the data frame.'.format(nseries))
```

    249 time series in the data frame.
    

<span data-ttu-id="5cf56-281">The data contains approximately 250 different combinations of store and brand in a data frame.</span><span class="sxs-lookup"><span data-stu-id="5cf56-281">The data contains approximately 250 different combinations of store and brand in a data frame.</span></span> <span data-ttu-id="5cf56-282">Each combination defines its own time series of sales.</span><span class="sxs-lookup"><span data-stu-id="5cf56-282">Each combination defines its own time series of sales.</span></span> 

<span data-ttu-id="5cf56-283">You can use the [TimeSeriesDataFrame](https://docs.microsoft.com/en-us/python/api/ftk.dataframe_ts.timeseriesdataframe?view=azure-ml-py-latest)  class to conveniently model multiple series in a single data structure using the _grain_.</span><span class="sxs-lookup"><span data-stu-id="5cf56-283">You can use the [TimeSeriesDataFrame](https://docs.microsoft.com/en-us/python/api/ftk.dataframe_ts.timeseriesdataframe?view=azure-ml-py-latest)  class to conveniently model multiple series in a single data structure using the _grain_.</span></span> <span data-ttu-id="5cf56-284">The grain is specified by the `store` and `brand` columns.</span><span class="sxs-lookup"><span data-stu-id="5cf56-284">The grain is specified by the `store` and `brand` columns.</span></span>

<span data-ttu-id="5cf56-285">The difference between _grain_ and _group_ is that grain is always physically meaningful in the real world, while group doesn't have to be.</span><span class="sxs-lookup"><span data-stu-id="5cf56-285">The difference between _grain_ and _group_ is that grain is always physically meaningful in the real world, while group doesn't have to be.</span></span> <span data-ttu-id="5cf56-286">Internal package functions use group to build a single model from multiple time series if the user believes this grouping helps improve model performance.</span><span class="sxs-lookup"><span data-stu-id="5cf56-286">Internal package functions use group to build a single model from multiple time series if the user believes this grouping helps improve model performance.</span></span> <span data-ttu-id="5cf56-287">By default, group is set to be equal to grain, and a single model is built for each grain.</span><span class="sxs-lookup"><span data-stu-id="5cf56-287">By default, group is set to be equal to grain, and a single model is built for each grain.</span></span> 


```python
# Create a TimeSeriesDataFrame
# Use end of period as the time index
# Store and brand combinations label the grain 
# i.e. there is one time series for each unique pair of store and grain
whole_tsdf = TimeSeriesDataFrame(whole_df, 
                                 grain_colnames=['store', 'brand'],
                                 time_colname='WeekLastDay', 
                                 ts_value_colname='Quantity',
                                 group_colnames='store')

whole_tsdf[['Quantity']].head()
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th><span data-ttu-id="5cf56-288">Quantity</span><span class="sxs-lookup"><span data-stu-id="5cf56-288">Quantity</span></span></th>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-289">WeekLastDay</span><span class="sxs-lookup"><span data-stu-id="5cf56-289">WeekLastDay</span></span></th>
      <th><span data-ttu-id="5cf56-290">store</span><span class="sxs-lookup"><span data-stu-id="5cf56-290">store</span></span></th>
      <th><span data-ttu-id="5cf56-291">brand</span><span class="sxs-lookup"><span data-stu-id="5cf56-291">brand</span></span></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="5cf56-292">1990-06-20 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-292">1990-06-20 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-293">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-293">2</span></span></th>
      <th><span data-ttu-id="5cf56-294">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-294">tropicana</span></span></th>
      <td><span data-ttu-id="5cf56-295">8256</span><span class="sxs-lookup"><span data-stu-id="5cf56-295">8256</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-296">1990-08-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-296">1990-08-01 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-297">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-297">2</span></span></th>
      <th><span data-ttu-id="5cf56-298">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-298">tropicana</span></span></th>
      <td><span data-ttu-id="5cf56-299">6144</span><span class="sxs-lookup"><span data-stu-id="5cf56-299">6144</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-300">1990-08-08 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-300">1990-08-08 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-301">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-301">2</span></span></th>
      <th><span data-ttu-id="5cf56-302">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-302">tropicana</span></span></th>
      <td><span data-ttu-id="5cf56-303">3840</span><span class="sxs-lookup"><span data-stu-id="5cf56-303">3840</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-304">1990-08-15 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-304">1990-08-15 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-305">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-305">2</span></span></th>
      <th><span data-ttu-id="5cf56-306">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-306">tropicana</span></span></th>
      <td><span data-ttu-id="5cf56-307">8000</span><span class="sxs-lookup"><span data-stu-id="5cf56-307">8000</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-308">1990-08-29 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-308">1990-08-29 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-309">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-309">2</span></span></th>
      <th><span data-ttu-id="5cf56-310">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-310">tropicana</span></span></th>
      <td><span data-ttu-id="5cf56-311">8896</span><span class="sxs-lookup"><span data-stu-id="5cf56-311">8896</span></span></td>
    </tr>
  </tbody>
</table>



<span data-ttu-id="5cf56-312">In the TimeSeriesDataFrame representation, the time axis and grain are now part of the data frame index, and allow easy access to pandas datetime slicing functionality.</span><span class="sxs-lookup"><span data-stu-id="5cf56-312">In the TimeSeriesDataFrame representation, the time axis and grain are now part of the data frame index, and allow easy access to pandas datetime slicing functionality.</span></span>


```python
# sort so we can slice
whole_tsdf.sort_index(inplace=True)

# Get sales of dominick's brand orange juice from store 2 during summer 1990
whole_tsdf.loc[pd.IndexSlice['1990-06':'1990-09', 2, 'dominicks'], ['Quantity']]
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th><span data-ttu-id="5cf56-313">Quantity</span><span class="sxs-lookup"><span data-stu-id="5cf56-313">Quantity</span></span></th>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-314">WeekLastDay</span><span class="sxs-lookup"><span data-stu-id="5cf56-314">WeekLastDay</span></span></th>
      <th><span data-ttu-id="5cf56-315">store</span><span class="sxs-lookup"><span data-stu-id="5cf56-315">store</span></span></th>
      <th><span data-ttu-id="5cf56-316">brand</span><span class="sxs-lookup"><span data-stu-id="5cf56-316">brand</span></span></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="5cf56-317">1990-06-20 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-317">1990-06-20 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-318">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-318">2</span></span></th>
      <th><span data-ttu-id="5cf56-319">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-319">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-320">10560</span><span class="sxs-lookup"><span data-stu-id="5cf56-320">10560</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-321">1990-08-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-321">1990-08-01 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-322">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-322">2</span></span></th>
      <th><span data-ttu-id="5cf56-323">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-323">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-324">8000</span><span class="sxs-lookup"><span data-stu-id="5cf56-324">8000</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-325">1990-08-08 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-325">1990-08-08 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-326">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-326">2</span></span></th>
      <th><span data-ttu-id="5cf56-327">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-327">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-328">6848</span><span class="sxs-lookup"><span data-stu-id="5cf56-328">6848</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-329">1990-08-15 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-329">1990-08-15 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-330">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-330">2</span></span></th>
      <th><span data-ttu-id="5cf56-331">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-331">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-332">2880</span><span class="sxs-lookup"><span data-stu-id="5cf56-332">2880</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-333">1990-08-29 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-333">1990-08-29 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-334">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-334">2</span></span></th>
      <th><span data-ttu-id="5cf56-335">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-335">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-336">1600</span><span class="sxs-lookup"><span data-stu-id="5cf56-336">1600</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-337">1990-09-05 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-337">1990-09-05 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-338">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-338">2</span></span></th>
      <th><span data-ttu-id="5cf56-339">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-339">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-340">25344</span><span class="sxs-lookup"><span data-stu-id="5cf56-340">25344</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-341">1990-09-12 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-341">1990-09-12 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-342">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-342">2</span></span></th>
      <th><span data-ttu-id="5cf56-343">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-343">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-344">10752</span><span class="sxs-lookup"><span data-stu-id="5cf56-344">10752</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-345">1990-09-19 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-345">1990-09-19 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-346">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-346">2</span></span></th>
      <th><span data-ttu-id="5cf56-347">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-347">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-348">6656</span><span class="sxs-lookup"><span data-stu-id="5cf56-348">6656</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-349">1990-09-26 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-349">1990-09-26 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-350">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-350">2</span></span></th>
      <th><span data-ttu-id="5cf56-351">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-351">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-352">6592</span><span class="sxs-lookup"><span data-stu-id="5cf56-352">6592</span></span></td>
    </tr>
  </tbody>
</table>



<span data-ttu-id="5cf56-353">The [TimeSeriesDataFrame.ts_report](https://docs.microsoft.com/en-us/python/api/ftk.dataframe_ts.timeseriesdataframe?view=azure-ml-py-latest#ts-report) function generates a comprehensive report of the time series data frame.</span><span class="sxs-lookup"><span data-stu-id="5cf56-353">The [TimeSeriesDataFrame.ts_report](https://docs.microsoft.com/en-us/python/api/ftk.dataframe_ts.timeseriesdataframe?view=azure-ml-py-latest#ts-report) function generates a comprehensive report of the time series data frame.</span></span> <span data-ttu-id="5cf56-354">The report includes both a general data description as well as statistics specific to time series data.</span><span class="sxs-lookup"><span data-stu-id="5cf56-354">The report includes both a general data description as well as statistics specific to time series data.</span></span> 


```python
whole_tsdf.ts_report()
```

    --------------------------------  Data Overview  ---------------------------------
    <class 'ftk.time_series_data_frame.TimeSeriesDataFrame'>
    MultiIndex: 28947 entries, (1990-06-20 23:59:59, 2, dominicks) to (1992-10-07 23:59:59, 137, tropicana)
    Data columns (total 17 columns):
    week            28947 non-null int64
    logmove         28947 non-null float64
    feat            28947 non-null int64
    price           28947 non-null float64
    AGE60           28947 non-null float64
    EDUC            28947 non-null float64
    ETHNIC          28947 non-null float64
    INCOME          28947 non-null float64
    HHLARGE         28947 non-null float64
    WORKWOM         28947 non-null float64
    HVAL150         28947 non-null float64
    SSTRDIST        28947 non-null float64
    SSTRVOL         28947 non-null float64
    CPDIST5         28947 non-null float64
    CPWVOL5         28947 non-null float64
    Quantity        28947 non-null int64
    WeekFirstDay    28947 non-null datetime64[ns]
    dtypes: datetime64[ns](1), float64(13), int64(3)
    memory usage: 3.8+ MB
    --------------------------  Numerical Variable Summary  --------------------------
              week  logmove     feat    price    AGE60     EDUC   ETHNIC   INCOME  \
    count 28947.00 28947.00 28947.00 28947.00 28947.00 28947.00 28947.00 28947.00   
    mean    100.46     9.17     0.24     2.28     0.17     0.23     0.16    10.62   
    std      34.69     1.02     0.43     0.65     0.06     0.11     0.19     0.28   
    min      40.00     4.16     0.00     0.52     0.06     0.05     0.02     9.87   
    25%      70.00     8.49     0.00     1.79     0.12     0.15     0.04    10.46   
    50%     101.00     9.03     0.00     2.17     0.17     0.23     0.07    10.64   
    75%     130.00     9.76     0.00     2.73     0.21     0.28     0.19    10.80   
    max     160.00    13.48     1.00     3.87     0.31     0.53     1.00    11.24   
    
           HHLARGE  WORKWOM  HVAL150  SSTRDIST  SSTRVOL  CPDIST5  CPWVOL5  \
    count 28947.00 28947.00 28947.00  28947.00 28947.00 28947.00 28947.00   
    mean      0.12     0.36     0.34      5.10     1.21     2.12     0.44   
    std       0.03     0.05     0.24      3.47     0.53     0.73     0.22   
    min       0.01     0.24     0.00      0.13     0.40     0.77     0.09   
    25%       0.10     0.31     0.12      2.77     0.73     1.63     0.27   
    50%       0.11     0.36     0.35      4.65     1.12     1.96     0.38   
    75%       0.14     0.40     0.53      6.65     1.54     2.53     0.56   
    max       0.22     0.47     0.92     17.86     2.57     4.11     1.14   
    
           Quantity  
    count  28947.00  
    mean   17312.21  
    std    27477.66  
    min       64.00  
    25%     4864.00  
    50%     8384.00  
    75%    17408.00  
    max   716416.00  
    ------------------------  Non-Numerical Variable Summary  -----------------------
                   WeekFirstDay
    count                 28947
    unique                  121
    top     1992-03-12 00:00:00
    freq                    249
    first   1990-06-14 00:00:00
    last    1992-10-01 00:00:00
    ------------------------------  Time Series Summary  -----------------------------
    Number of time series                 249
    Minimum time                    1990-06-20 23:59:59
    Maximum time                    1992-10-07 23:59:59
    
    Inferred frequencies
    Number of ['store', 'brand']s with frequency W-WED     249
    Use get_frequency_dict() method to explore ['store', 'brand']s with unusual frequency and clean data
    
    Detected seasonalities
    Number of ['store', 'brand']s with seasonality 1         190
    Number of ['store', 'brand']s with seasonality 15        15
    Number of ['store', 'brand']s with seasonality 14        11
    Number of ['store', 'brand']s with seasonality 7         9
    Number of ['store', 'brand']s with seasonality 6         8
    Number of ['store', 'brand']s with seasonality 8         5
    Number of ['store', 'brand']s with seasonality 2         4
    Number of ['store', 'brand']s with seasonality 23        2
    Number of ['store', 'brand']s with seasonality 3         1
    Number of ['store', 'brand']s with seasonality 11        1
    Number of ['store', 'brand']s with seasonality 12        1
    Number of ['store', 'brand']s with seasonality 13        1
    Number of ['store', 'brand']s with seasonality 47        1
    Use get_seasonality_dict() method to explore ['store', 'brand']s with unusual seasonality and clean data
    -----------------------------  Value Column Summary  -----------------------------
    Value column                        Quantity
    Percentage of missing values        0.00
    Percentage of zero values           0.00
    Mean coefficient of variation       31688.52
    Median coefficient of variation     24000.20
    Minimum coefficient of variation    ['store', 'brand'] (48, 'tropicana'): 4475.53
    Maximum coefficient of variation    ['store', 'brand'] (111, 'dominicks'): 193333.55
    ------------------------------  Correlation Matrix  ------------------------------
        week  logmove  feat  price  AGE60  EDUC  ETHNIC  INCOME  HHLARGE  WORKWOM  \
    0   1.00     0.10  0.04  -0.21  -0.01  0.01    0.00    0.00     0.01    -0.00   
    1   0.10     1.00  0.54  -0.43   0.09  0.00    0.06   -0.04    -0.06    -0.08   
    2   0.04     0.54  1.00  -0.29  -0.00  0.00    0.00   -0.00    -0.00     0.00   
    3  -0.21    -0.43 -0.29   1.00   0.04  0.02    0.04   -0.03    -0.04    -0.02   
    4  -0.01     0.09 -0.00   0.04   1.00 -0.31   -0.09   -0.15    -0.32    -0.63   
    5   0.01     0.00  0.00   0.02  -0.31  1.00   -0.34    0.66    -0.39     0.56   
    6   0.00     0.06  0.00   0.04  -0.09 -0.34    1.00   -0.72     0.25    -0.29   
    7   0.00    -0.04 -0.00  -0.03  -0.15  0.66   -0.72    1.00    -0.08     0.40   
    8   0.01    -0.06 -0.00  -0.04  -0.32 -0.39    0.25   -0.08     1.00    -0.28   
    9  -0.00    -0.08  0.00  -0.02  -0.63  0.56   -0.29    0.40    -0.28     1.00   
    10  0.01     0.02  0.00   0.04  -0.11  0.89   -0.42    0.64    -0.48     0.45   
    11  0.01    -0.00  0.00   0.08   0.07 -0.12    0.54   -0.41     0.06    -0.19   
    12 -0.01    -0.09 -0.00   0.03  -0.05 -0.13    0.23   -0.26     0.04    -0.06   
    13 -0.01     0.02 -0.00  -0.06   0.09 -0.20   -0.22    0.21     0.19    -0.13   
    14 -0.00    -0.12 -0.00  -0.01  -0.09  0.28   -0.38    0.36    -0.20     0.37   
    15  0.03     0.76  0.47  -0.36   0.08 -0.04    0.11   -0.08    -0.00    -0.10   
    
        HVAL150  SSTRDIST  SSTRVOL  CPDIST5  CPWVOL5  Quantity  
    0      0.01      0.01    -0.01    -0.01    -0.00      0.03  
    1      0.02     -0.00    -0.09     0.02    -0.12      0.76  
    2      0.00      0.00    -0.00    -0.00    -0.00      0.47  
    3      0.04      0.08     0.03    -0.06    -0.01     -0.36  
    4     -0.11      0.07    -0.05     0.09    -0.09      0.08  
    5      0.89     -0.12    -0.13    -0.20     0.28     -0.04  
    6     -0.42      0.54     0.23    -0.22    -0.38      0.11  
    7      0.64     -0.41    -0.26     0.21     0.36     -0.08  
    8     -0.48      0.06     0.04     0.19    -0.20     -0.00  
    9      0.45     -0.19    -0.06    -0.13     0.37     -0.10  
    10     1.00     -0.17    -0.24    -0.22     0.27     -0.04  
    11    -0.17      1.00     0.17    -0.11    -0.40      0.06  
    12    -0.24      0.17     1.00    -0.05     0.36     -0.02  
    13    -0.22     -0.11    -0.05     1.00     0.02     -0.00  
    14     0.27     -0.40     0.36     0.02     1.00     -0.11  
    15    -0.04      0.06    -0.02    -0.00    -0.11      1.00  
    You may call TimeSeriesDataFrame.plot_scatter_matrix() to get a correlation matrix plot. However, this
    is not recommended if your data is big.
    



![png](./media/how-to-build-deploy-forecast-models/output_15_1.png)



![png](./media/how-to-build-deploy-forecast-models/output_15_2.png)



![png](./media/how-to-build-deploy-forecast-models/output_15_3.png)



![png](./media/how-to-build-deploy-forecast-models/output_15_4.png)



![png](./media/how-to-build-deploy-forecast-models/output_15_5.png)



![png](./media/how-to-build-deploy-forecast-models/output_15_6.png)


## <a name="integrate-with-external-data"></a><span data-ttu-id="5cf56-361">Integrate with external data</span><span class="sxs-lookup"><span data-stu-id="5cf56-361">Integrate with external data</span></span>

<span data-ttu-id="5cf56-362">Sometimes it's useful to integrate external data as additional features for forecasting.</span><span class="sxs-lookup"><span data-stu-id="5cf56-362">Sometimes it's useful to integrate external data as additional features for forecasting.</span></span> <span data-ttu-id="5cf56-363">In this code sample, you join TimeSeriesDataFrame with external data related to weather.</span><span class="sxs-lookup"><span data-stu-id="5cf56-363">In this code sample, you join TimeSeriesDataFrame with external data related to weather.</span></span>


```python
# Load weather data
weather_1990 = get_a_year_of_daily_weather_data(year=1990)
weather_1991 = get_a_year_of_daily_weather_data(year=1991)
weather_1992 = get_a_year_of_daily_weather_data(year=1992)

# Preprocess weather data
weather_all = pd.concat([weather_1990, weather_1991, weather_1992])
weather_all.reset_index(inplace=True)

# Only use a subset of columns
weather_all = weather_all[['TEMP', 'DEWP', 'WDSP', 'PRCP']]

# Compute the WeekLastDay column, in order to merge with sales data
weather_all['WeekLastDay'] = pd.Series(
    weather_all.time_index - weekZeroStart, 
    index=weather_all.time_index).apply(lambda n: weekZeroEnd + timedelta(weeks=math.floor(n.days/7)))

# Resample daily weather data to weekly data
weather_all = weather_all.groupby('WeekLastDay').mean()

# Set WeekLastDay as new time index
weather_all = TimeSeriesDataFrame(weather_all, time_colname='WeekLastDay')

# Merge weather data with sales data
whole_tsdf = whole_tsdf.merge(weather_all, how='left', on='WeekLastDay')
whole_tsdf.head()
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th><span data-ttu-id="5cf56-364">week</span><span class="sxs-lookup"><span data-stu-id="5cf56-364">week</span></span></th>
      <th><span data-ttu-id="5cf56-365">logmove</span><span class="sxs-lookup"><span data-stu-id="5cf56-365">logmove</span></span></th>
      <th><span data-ttu-id="5cf56-366">feat</span><span class="sxs-lookup"><span data-stu-id="5cf56-366">feat</span></span></th>
      <th><span data-ttu-id="5cf56-367">price</span><span class="sxs-lookup"><span data-stu-id="5cf56-367">price</span></span></th>
      <th><span data-ttu-id="5cf56-368">AGE60</span><span class="sxs-lookup"><span data-stu-id="5cf56-368">AGE60</span></span></th>
      <th><span data-ttu-id="5cf56-369">EDUC</span><span class="sxs-lookup"><span data-stu-id="5cf56-369">EDUC</span></span></th>
      <th><span data-ttu-id="5cf56-370">ETHNIC</span><span class="sxs-lookup"><span data-stu-id="5cf56-370">ETHNIC</span></span></th>
      <th><span data-ttu-id="5cf56-371">INCOME</span><span class="sxs-lookup"><span data-stu-id="5cf56-371">INCOME</span></span></th>
      <th><span data-ttu-id="5cf56-372">HHLARGE</span><span class="sxs-lookup"><span data-stu-id="5cf56-372">HHLARGE</span></span></th>
      <th><span data-ttu-id="5cf56-373">WORKWOM</span><span class="sxs-lookup"><span data-stu-id="5cf56-373">WORKWOM</span></span></th>
      <th><span data-ttu-id="5cf56-374">...</span><span class="sxs-lookup"><span data-stu-id="5cf56-374">...</span></span></th>
      <th><span data-ttu-id="5cf56-375">SSTRDIST</span><span class="sxs-lookup"><span data-stu-id="5cf56-375">SSTRDIST</span></span></th>
      <th><span data-ttu-id="5cf56-376">SSTRVOL</span><span class="sxs-lookup"><span data-stu-id="5cf56-376">SSTRVOL</span></span></th>
      <th><span data-ttu-id="5cf56-377">CPDIST5</span><span class="sxs-lookup"><span data-stu-id="5cf56-377">CPDIST5</span></span></th>
      <th><span data-ttu-id="5cf56-378">CPWVOL5</span><span class="sxs-lookup"><span data-stu-id="5cf56-378">CPWVOL5</span></span></th>
      <th><span data-ttu-id="5cf56-379">Quantity</span><span class="sxs-lookup"><span data-stu-id="5cf56-379">Quantity</span></span></th>
      <th><span data-ttu-id="5cf56-380">WeekFirstDay</span><span class="sxs-lookup"><span data-stu-id="5cf56-380">WeekFirstDay</span></span></th>
      <th><span data-ttu-id="5cf56-381">TEMP</span><span class="sxs-lookup"><span data-stu-id="5cf56-381">TEMP</span></span></th>
      <th><span data-ttu-id="5cf56-382">DEWP</span><span class="sxs-lookup"><span data-stu-id="5cf56-382">DEWP</span></span></th>
      <th><span data-ttu-id="5cf56-383">WDSP</span><span class="sxs-lookup"><span data-stu-id="5cf56-383">WDSP</span></span></th>
      <th><span data-ttu-id="5cf56-384">PRCP</span><span class="sxs-lookup"><span data-stu-id="5cf56-384">PRCP</span></span></th>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-385">WeekLastDay</span><span class="sxs-lookup"><span data-stu-id="5cf56-385">WeekLastDay</span></span></th>
      <th><span data-ttu-id="5cf56-386">store</span><span class="sxs-lookup"><span data-stu-id="5cf56-386">store</span></span></th>
      <th><span data-ttu-id="5cf56-387">brand</span><span class="sxs-lookup"><span data-stu-id="5cf56-387">brand</span></span></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top"><span data-ttu-id="5cf56-388">1990-06-20 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-388">1990-06-20 23:59:59</span></span></th>
      <th rowspan="3" valign="top"><span data-ttu-id="5cf56-389">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-389">2</span></span></th>
      <th><span data-ttu-id="5cf56-390">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-390">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-391">40</span><span class="sxs-lookup"><span data-stu-id="5cf56-391">40</span></span></td>
      <td><span data-ttu-id="5cf56-392">9.26</span><span class="sxs-lookup"><span data-stu-id="5cf56-392">9.26</span></span></td>
      <td><span data-ttu-id="5cf56-393">1</span><span class="sxs-lookup"><span data-stu-id="5cf56-393">1</span></span></td>
      <td><span data-ttu-id="5cf56-394">1.59</span><span class="sxs-lookup"><span data-stu-id="5cf56-394">1.59</span></span></td>
      <td><span data-ttu-id="5cf56-395">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-395">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-396">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-396">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-397">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-397">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-398">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-398">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-399">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-399">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-400">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-400">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-401">...</span><span class="sxs-lookup"><span data-stu-id="5cf56-401">...</span></span></td>
      <td><span data-ttu-id="5cf56-402">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-402">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-403">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-403">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-404">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-404">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-405">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-405">0.38</span></span></td>
      <td><span data-ttu-id="5cf56-406">10560</span><span class="sxs-lookup"><span data-stu-id="5cf56-406">10560</span></span></td>
      <td><span data-ttu-id="5cf56-407">1990-06-14</span><span class="sxs-lookup"><span data-stu-id="5cf56-407">1990-06-14</span></span></td>
      <td><span data-ttu-id="5cf56-408">72.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-408">72.00</span></span></td>
      <td><span data-ttu-id="5cf56-409">61.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-409">61.87</span></span></td>
      <td><span data-ttu-id="5cf56-410">9.74</span><span class="sxs-lookup"><span data-stu-id="5cf56-410">9.74</span></span></td>
      <td><span data-ttu-id="5cf56-411">0.19</span><span class="sxs-lookup"><span data-stu-id="5cf56-411">0.19</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-412">minute.maid</span><span class="sxs-lookup"><span data-stu-id="5cf56-412">minute.maid</span></span></th>
      <td><span data-ttu-id="5cf56-413">40</span><span class="sxs-lookup"><span data-stu-id="5cf56-413">40</span></span></td>
      <td><span data-ttu-id="5cf56-414">8.41</span><span class="sxs-lookup"><span data-stu-id="5cf56-414">8.41</span></span></td>
      <td><span data-ttu-id="5cf56-415">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-415">0</span></span></td>
      <td><span data-ttu-id="5cf56-416">3.17</span><span class="sxs-lookup"><span data-stu-id="5cf56-416">3.17</span></span></td>
      <td><span data-ttu-id="5cf56-417">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-417">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-418">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-418">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-419">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-419">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-420">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-420">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-421">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-421">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-422">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-422">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-423">...</span><span class="sxs-lookup"><span data-stu-id="5cf56-423">...</span></span></td>
      <td><span data-ttu-id="5cf56-424">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-424">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-425">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-425">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-426">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-426">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-427">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-427">0.38</span></span></td>
      <td><span data-ttu-id="5cf56-428">4480</span><span class="sxs-lookup"><span data-stu-id="5cf56-428">4480</span></span></td>
      <td><span data-ttu-id="5cf56-429">1990-06-14</span><span class="sxs-lookup"><span data-stu-id="5cf56-429">1990-06-14</span></span></td>
      <td><span data-ttu-id="5cf56-430">72.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-430">72.00</span></span></td>
      <td><span data-ttu-id="5cf56-431">61.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-431">61.87</span></span></td>
      <td><span data-ttu-id="5cf56-432">9.74</span><span class="sxs-lookup"><span data-stu-id="5cf56-432">9.74</span></span></td>
      <td><span data-ttu-id="5cf56-433">0.19</span><span class="sxs-lookup"><span data-stu-id="5cf56-433">0.19</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-434">tropicana</span><span class="sxs-lookup"><span data-stu-id="5cf56-434">tropicana</span></span></th>
      <td><span data-ttu-id="5cf56-435">40</span><span class="sxs-lookup"><span data-stu-id="5cf56-435">40</span></span></td>
      <td><span data-ttu-id="5cf56-436">9.02</span><span class="sxs-lookup"><span data-stu-id="5cf56-436">9.02</span></span></td>
      <td><span data-ttu-id="5cf56-437">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-437">0</span></span></td>
      <td><span data-ttu-id="5cf56-438">3.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-438">3.87</span></span></td>
      <td><span data-ttu-id="5cf56-439">0.23</span><span class="sxs-lookup"><span data-stu-id="5cf56-439">0.23</span></span></td>
      <td><span data-ttu-id="5cf56-440">0.25</span><span class="sxs-lookup"><span data-stu-id="5cf56-440">0.25</span></span></td>
      <td><span data-ttu-id="5cf56-441">0.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-441">0.11</span></span></td>
      <td><span data-ttu-id="5cf56-442">10.55</span><span class="sxs-lookup"><span data-stu-id="5cf56-442">10.55</span></span></td>
      <td><span data-ttu-id="5cf56-443">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-443">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-444">0.30</span><span class="sxs-lookup"><span data-stu-id="5cf56-444">0.30</span></span></td>
      <td><span data-ttu-id="5cf56-445">...</span><span class="sxs-lookup"><span data-stu-id="5cf56-445">...</span></span></td>
      <td><span data-ttu-id="5cf56-446">2.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-446">2.11</span></span></td>
      <td><span data-ttu-id="5cf56-447">1.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-447">1.14</span></span></td>
      <td><span data-ttu-id="5cf56-448">1.93</span><span class="sxs-lookup"><span data-stu-id="5cf56-448">1.93</span></span></td>
      <td><span data-ttu-id="5cf56-449">0.38</span><span class="sxs-lookup"><span data-stu-id="5cf56-449">0.38</span></span></td>
      <td><span data-ttu-id="5cf56-450">8256</span><span class="sxs-lookup"><span data-stu-id="5cf56-450">8256</span></span></td>
      <td><span data-ttu-id="5cf56-451">1990-06-14</span><span class="sxs-lookup"><span data-stu-id="5cf56-451">1990-06-14</span></span></td>
      <td><span data-ttu-id="5cf56-452">72.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-452">72.00</span></span></td>
      <td><span data-ttu-id="5cf56-453">61.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-453">61.87</span></span></td>
      <td><span data-ttu-id="5cf56-454">9.74</span><span class="sxs-lookup"><span data-stu-id="5cf56-454">9.74</span></span></td>
      <td><span data-ttu-id="5cf56-455">0.19</span><span class="sxs-lookup"><span data-stu-id="5cf56-455">0.19</span></span></td>
    </tr>
    <tr>
      <th rowspan="2" valign="top"><span data-ttu-id="5cf56-456">5</span><span class="sxs-lookup"><span data-stu-id="5cf56-456">5</span></span></th>
      <th><span data-ttu-id="5cf56-457">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-457">dominicks</span></span></th>
      <td><span data-ttu-id="5cf56-458">40</span><span class="sxs-lookup"><span data-stu-id="5cf56-458">40</span></span></td>
      <td><span data-ttu-id="5cf56-459">7.49</span><span class="sxs-lookup"><span data-stu-id="5cf56-459">7.49</span></span></td>
      <td><span data-ttu-id="5cf56-460">1</span><span class="sxs-lookup"><span data-stu-id="5cf56-460">1</span></span></td>
      <td><span data-ttu-id="5cf56-461">1.59</span><span class="sxs-lookup"><span data-stu-id="5cf56-461">1.59</span></span></td>
      <td><span data-ttu-id="5cf56-462">0.12</span><span class="sxs-lookup"><span data-stu-id="5cf56-462">0.12</span></span></td>
      <td><span data-ttu-id="5cf56-463">0.32</span><span class="sxs-lookup"><span data-stu-id="5cf56-463">0.32</span></span></td>
      <td><span data-ttu-id="5cf56-464">0.05</span><span class="sxs-lookup"><span data-stu-id="5cf56-464">0.05</span></span></td>
      <td><span data-ttu-id="5cf56-465">10.92</span><span class="sxs-lookup"><span data-stu-id="5cf56-465">10.92</span></span></td>
      <td><span data-ttu-id="5cf56-466">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-466">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-467">0.41</span><span class="sxs-lookup"><span data-stu-id="5cf56-467">0.41</span></span></td>
      <td><span data-ttu-id="5cf56-468">...</span><span class="sxs-lookup"><span data-stu-id="5cf56-468">...</span></span></td>
      <td><span data-ttu-id="5cf56-469">3.80</span><span class="sxs-lookup"><span data-stu-id="5cf56-469">3.80</span></span></td>
      <td><span data-ttu-id="5cf56-470">0.68</span><span class="sxs-lookup"><span data-stu-id="5cf56-470">0.68</span></span></td>
      <td><span data-ttu-id="5cf56-471">1.60</span><span class="sxs-lookup"><span data-stu-id="5cf56-471">1.60</span></span></td>
      <td><span data-ttu-id="5cf56-472">0.74</span><span class="sxs-lookup"><span data-stu-id="5cf56-472">0.74</span></span></td>
      <td><span data-ttu-id="5cf56-473">1792</span><span class="sxs-lookup"><span data-stu-id="5cf56-473">1792</span></span></td>
      <td><span data-ttu-id="5cf56-474">1990-06-14</span><span class="sxs-lookup"><span data-stu-id="5cf56-474">1990-06-14</span></span></td>
      <td><span data-ttu-id="5cf56-475">72.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-475">72.00</span></span></td>
      <td><span data-ttu-id="5cf56-476">61.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-476">61.87</span></span></td>
      <td><span data-ttu-id="5cf56-477">9.74</span><span class="sxs-lookup"><span data-stu-id="5cf56-477">9.74</span></span></td>
      <td><span data-ttu-id="5cf56-478">0.19</span><span class="sxs-lookup"><span data-stu-id="5cf56-478">0.19</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-479">minute.maid</span><span class="sxs-lookup"><span data-stu-id="5cf56-479">minute.maid</span></span></th>
      <td><span data-ttu-id="5cf56-480">40</span><span class="sxs-lookup"><span data-stu-id="5cf56-480">40</span></span></td>
      <td><span data-ttu-id="5cf56-481">8.35</span><span class="sxs-lookup"><span data-stu-id="5cf56-481">8.35</span></span></td>
      <td><span data-ttu-id="5cf56-482">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-482">0</span></span></td>
      <td><span data-ttu-id="5cf56-483">2.99</span><span class="sxs-lookup"><span data-stu-id="5cf56-483">2.99</span></span></td>
      <td><span data-ttu-id="5cf56-484">0.12</span><span class="sxs-lookup"><span data-stu-id="5cf56-484">0.12</span></span></td>
      <td><span data-ttu-id="5cf56-485">0.32</span><span class="sxs-lookup"><span data-stu-id="5cf56-485">0.32</span></span></td>
      <td><span data-ttu-id="5cf56-486">0.05</span><span class="sxs-lookup"><span data-stu-id="5cf56-486">0.05</span></span></td>
      <td><span data-ttu-id="5cf56-487">10.92</span><span class="sxs-lookup"><span data-stu-id="5cf56-487">10.92</span></span></td>
      <td><span data-ttu-id="5cf56-488">0.10</span><span class="sxs-lookup"><span data-stu-id="5cf56-488">0.10</span></span></td>
      <td><span data-ttu-id="5cf56-489">0.41</span><span class="sxs-lookup"><span data-stu-id="5cf56-489">0.41</span></span></td>
      <td><span data-ttu-id="5cf56-490">...</span><span class="sxs-lookup"><span data-stu-id="5cf56-490">...</span></span></td>
      <td><span data-ttu-id="5cf56-491">3.80</span><span class="sxs-lookup"><span data-stu-id="5cf56-491">3.80</span></span></td>
      <td><span data-ttu-id="5cf56-492">0.68</span><span class="sxs-lookup"><span data-stu-id="5cf56-492">0.68</span></span></td>
      <td><span data-ttu-id="5cf56-493">1.60</span><span class="sxs-lookup"><span data-stu-id="5cf56-493">1.60</span></span></td>
      <td><span data-ttu-id="5cf56-494">0.74</span><span class="sxs-lookup"><span data-stu-id="5cf56-494">0.74</span></span></td>
      <td><span data-ttu-id="5cf56-495">4224</span><span class="sxs-lookup"><span data-stu-id="5cf56-495">4224</span></span></td>
      <td><span data-ttu-id="5cf56-496">1990-06-14</span><span class="sxs-lookup"><span data-stu-id="5cf56-496">1990-06-14</span></span></td>
      <td><span data-ttu-id="5cf56-497">72.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-497">72.00</span></span></td>
      <td><span data-ttu-id="5cf56-498">61.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-498">61.87</span></span></td>
      <td><span data-ttu-id="5cf56-499">9.74</span><span class="sxs-lookup"><span data-stu-id="5cf56-499">9.74</span></span></td>
      <td><span data-ttu-id="5cf56-500">0.19</span><span class="sxs-lookup"><span data-stu-id="5cf56-500">0.19</span></span></td>
    </tr>
  </tbody>
</table>


## <a name="preprocess-data-and-impute-missing-values"></a><span data-ttu-id="5cf56-501">Preprocess data and impute missing values</span><span class="sxs-lookup"><span data-stu-id="5cf56-501">Preprocess data and impute missing values</span></span>

<span data-ttu-id="5cf56-502">Start by splitting the data into training set and a testing set with the [last_n_periods_split](https://docs.microsoft.com/en-us/python/api/ftk.ts_utils?view=azure-ml-py-latest) utility function.</span><span class="sxs-lookup"><span data-stu-id="5cf56-502">Start by splitting the data into training set and a testing set with the [last_n_periods_split](https://docs.microsoft.com/en-us/python/api/ftk.ts_utils?view=azure-ml-py-latest) utility function.</span></span> <span data-ttu-id="5cf56-503">The resulting testing set contains the last 40 observations of each time series.</span><span class="sxs-lookup"><span data-stu-id="5cf56-503">The resulting testing set contains the last 40 observations of each time series.</span></span> 


```python
train_tsdf, test_tsdf = last_n_periods_split(whole_tsdf, 40)
```

<span data-ttu-id="5cf56-504">Basic time series models require contiguous time series.</span><span class="sxs-lookup"><span data-stu-id="5cf56-504">Basic time series models require contiguous time series.</span></span> <span data-ttu-id="5cf56-505">Check to see if the series are regular, meaning that they have a time index sampled at regular intervals, using the [check_regularity_by_grain](https://docs.microsoft.com/en-us/python/api/ftk.dataframe_ts.timeseriesdataframe?view=azure-ml-py-latest#check-regularity-by-grain) function.</span><span class="sxs-lookup"><span data-stu-id="5cf56-505">Check to see if the series are regular, meaning that they have a time index sampled at regular intervals, using the [check_regularity_by_grain](https://docs.microsoft.com/en-us/python/api/ftk.dataframe_ts.timeseriesdataframe?view=azure-ml-py-latest#check-regularity-by-grain) function.</span></span>


```python
ts_regularity = train_tsdf.check_regularity_by_grain()
print(ts_regularity[ts_regularity['regular'] == False])
```

                                              problems  regular
    store brand                                                
    2     dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    5     dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    8     dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    9     dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    12    dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    14    dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    18    dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    21    dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    28    dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    33    dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    ...                                            ...      ...
    119   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    121   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    123   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    126   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    128   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    129   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    130   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    131   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    134   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    137   dominicks    [Irregular datetime gaps exist]    False
          minute.maid  [Irregular datetime gaps exist]    False
          tropicana    [Irregular datetime gaps exist]    False
    
    [213 rows x 2 columns]
    

<span data-ttu-id="5cf56-506">You can see that most of the series (213 out of 249) are irregular.</span><span class="sxs-lookup"><span data-stu-id="5cf56-506">You can see that most of the series (213 out of 249) are irregular.</span></span> <span data-ttu-id="5cf56-507">An [imputation transform](https://docs.microsoft.com/en-us/python/api/ftk.transforms.ts_imputer.timeseriesimputer?view=azure-ml-py-latest) is required to fill in missing sales quantity values.</span><span class="sxs-lookup"><span data-stu-id="5cf56-507">An [imputation transform](https://docs.microsoft.com/en-us/python/api/ftk.transforms.ts_imputer.timeseriesimputer?view=azure-ml-py-latest) is required to fill in missing sales quantity values.</span></span> <span data-ttu-id="5cf56-508">While there are many imputation options, the following sample code uses a linear interpolation.</span><span class="sxs-lookup"><span data-stu-id="5cf56-508">While there are many imputation options, the following sample code uses a linear interpolation.</span></span>


```python
# Use a TimeSeriesImputer to linearly interpolate missing values
imputer = TimeSeriesImputer(input_column='Quantity', 
                            option='interpolate',
                            method='linear',
                            freq='W-WED')

train_imputed_tsdf = imputer.transform(train_tsdf)
```

<span data-ttu-id="5cf56-509">After the imputation code is run, the series all have a regular frequency:</span><span class="sxs-lookup"><span data-stu-id="5cf56-509">After the imputation code is run, the series all have a regular frequency:</span></span>


```python
ts_regularity_imputed = train_imputed_tsdf.check_regularity_by_grain()
print(ts_regularity_imputed[ts_regularity_imputed['regular'] == False])
```

    Empty DataFrame
    Columns: [problems, regular]
    Index: []
    

## <a name="univariate-time-series-models"></a><span data-ttu-id="5cf56-510">Univariate time series models</span><span class="sxs-lookup"><span data-stu-id="5cf56-510">Univariate time series models</span></span>

<span data-ttu-id="5cf56-511">Now that you have cleaned up the data, you can begin modeling.</span><span class="sxs-lookup"><span data-stu-id="5cf56-511">Now that you have cleaned up the data, you can begin modeling.</span></span>  <span data-ttu-id="5cf56-512">Start by creating three univariate models: the "naive" model, the "seasonal naive" model, and an "ARIMA" model.</span><span class="sxs-lookup"><span data-stu-id="5cf56-512">Start by creating three univariate models: the "naive" model, the "seasonal naive" model, and an "ARIMA" model.</span></span>
* <span data-ttu-id="5cf56-513">The Naive forecasting algorithm uses the actual target variable value of the last period as the forecasted value of the current period.</span><span class="sxs-lookup"><span data-stu-id="5cf56-513">The Naive forecasting algorithm uses the actual target variable value of the last period as the forecasted value of the current period.</span></span>

* <span data-ttu-id="5cf56-514">The Seasonal Naive algorithm uses the actual target variable value of the same time point of the previous season as the forecasted value of the current time point.</span><span class="sxs-lookup"><span data-stu-id="5cf56-514">The Seasonal Naive algorithm uses the actual target variable value of the same time point of the previous season as the forecasted value of the current time point.</span></span> <span data-ttu-id="5cf56-515">Some examples include using the actual value of the same month of last year to forecast months of the current year; use the same hour of yesterday to forecast hours today.</span><span class="sxs-lookup"><span data-stu-id="5cf56-515">Some examples include using the actual value of the same month of last year to forecast months of the current year; use the same hour of yesterday to forecast hours today.</span></span> 

* <span data-ttu-id="5cf56-516">The exponential smoothing (ETS) algorithm generates forecasts by computing the weighted averages of past observations, with the weights decaying exponentially as the observations get older.</span><span class="sxs-lookup"><span data-stu-id="5cf56-516">The exponential smoothing (ETS) algorithm generates forecasts by computing the weighted averages of past observations, with the weights decaying exponentially as the observations get older.</span></span> 

* <span data-ttu-id="5cf56-517">The AutoRegressive Integrated Moving Average (ARIMA) algorithm captures the autocorrelation in time series data.</span><span class="sxs-lookup"><span data-stu-id="5cf56-517">The AutoRegressive Integrated Moving Average (ARIMA) algorithm captures the autocorrelation in time series data.</span></span> <span data-ttu-id="5cf56-518">For more information about ARIMA, see [this link](https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average)</span><span class="sxs-lookup"><span data-stu-id="5cf56-518">For more information about ARIMA, see [this link](https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average)</span></span>

<span data-ttu-id="5cf56-519">Start by setting certain model parameters based on your data exploration.</span><span class="sxs-lookup"><span data-stu-id="5cf56-519">Start by setting certain model parameters based on your data exploration.</span></span> 


```python
oj_series_freq = 'W-WED'
oj_series_seasonality = 52
```

### <a name="initialize-models"></a><span data-ttu-id="5cf56-520">Initialize Models</span><span class="sxs-lookup"><span data-stu-id="5cf56-520">Initialize Models</span></span>


```python
# Initialize naive model.
naive_model = Naive(freq=oj_series_freq)

# Initialize seasonal naive model. 
seasonal_naive_model = SeasonalNaive(freq=oj_series_freq, 
                                     seasonality=oj_series_seasonality)

# Initialize ETS model.
ets_model = ETS(freq=oj_series_freq, seasonality=oj_series_seasonality)

# Initialize ARIMA(p,d,q) model.
arima_order = [2, 1, 0]
arima_model = Arima(oj_series_freq, arima_order)
```

### <a name="combine-multiple-models"></a><span data-ttu-id="5cf56-521">Combine Multiple Models</span><span class="sxs-lookup"><span data-stu-id="5cf56-521">Combine Multiple Models</span></span>

<span data-ttu-id="5cf56-522">The [ForecasterUnion](https://docs.microsoft.com/en-us/python/api/ftk.models.forecaster_union?view=azure-ml-py-latest) estimator allows you to combine multiple estimators and fit/predict on them using one line of code.</span><span class="sxs-lookup"><span data-stu-id="5cf56-522">The [ForecasterUnion](https://docs.microsoft.com/en-us/python/api/ftk.models.forecaster_union?view=azure-ml-py-latest) estimator allows you to combine multiple estimators and fit/predict on them using one line of code.</span></span>


```python
forecaster_union = ForecasterUnion(
    forecaster_list=[('naive', naive_model), ('seasonal_naive', seasonal_naive_model), 
                     ('ets', ets_model), ('arima', arima_model)]) 
```

### <a name="fit-and-predict"></a><span data-ttu-id="5cf56-523">Fit and Predict</span><span class="sxs-lookup"><span data-stu-id="5cf56-523">Fit and Predict</span></span>

<span data-ttu-id="5cf56-524">The estimators in AMLPF follow the same API as scikit-learn estimators: a fit method for model training and a predict method for generating forecasts.</span><span class="sxs-lookup"><span data-stu-id="5cf56-524">The estimators in AMLPF follow the same API as scikit-learn estimators: a fit method for model training and a predict method for generating forecasts.</span></span> 

<span data-ttu-id="5cf56-525">**Train models**</span><span class="sxs-lookup"><span data-stu-id="5cf56-525">**Train models**</span></span>  
<span data-ttu-id="5cf56-526">Since these models are all univariate models, one model is fit to each grain of the data.</span><span class="sxs-lookup"><span data-stu-id="5cf56-526">Since these models are all univariate models, one model is fit to each grain of the data.</span></span> <span data-ttu-id="5cf56-527">Using AMLPF, all 249 models can be fit with just one function call.</span><span class="sxs-lookup"><span data-stu-id="5cf56-527">Using AMLPF, all 249 models can be fit with just one function call.</span></span>


```python
forecaster_union_fitted = forecaster_union.fit(train_imputed_tsdf)
```

<span data-ttu-id="5cf56-528">**Forecast sales on test data**</span><span class="sxs-lookup"><span data-stu-id="5cf56-528">**Forecast sales on test data**</span></span>  
<span data-ttu-id="5cf56-529">Similar to the fit method, you can create predictions for all 249 series in the testing data set with one call to the `predict` function.</span><span class="sxs-lookup"><span data-stu-id="5cf56-529">Similar to the fit method, you can create predictions for all 249 series in the testing data set with one call to the `predict` function.</span></span> 


```python
forecaster_union_prediction = forecaster_union_fitted.predict(test_tsdf, retain_feature_column=True)
```

<span data-ttu-id="5cf56-530">**Evaluate model performance**</span><span class="sxs-lookup"><span data-stu-id="5cf56-530">**Evaluate model performance**</span></span>   

<span data-ttu-id="5cf56-531">Now you can calculate the forecast errors on the test set.</span><span class="sxs-lookup"><span data-stu-id="5cf56-531">Now you can calculate the forecast errors on the test set.</span></span> <span data-ttu-id="5cf56-532">You can use the mean absolute percentage error (MAPE) here.</span><span class="sxs-lookup"><span data-stu-id="5cf56-532">You can use the mean absolute percentage error (MAPE) here.</span></span> <span data-ttu-id="5cf56-533">MAPE is the mean absolute percent error relative to the actual sales values.</span><span class="sxs-lookup"><span data-stu-id="5cf56-533">MAPE is the mean absolute percent error relative to the actual sales values.</span></span> <span data-ttu-id="5cf56-534">The ```calc_error``` function provides a few built-in functions for commonly used error metrics.</span><span class="sxs-lookup"><span data-stu-id="5cf56-534">The ```calc_error``` function provides a few built-in functions for commonly used error metrics.</span></span> <span data-ttu-id="5cf56-535">You can also define our custom error function to calculate MedianAPE and pass it to the err_fun argument.</span><span class="sxs-lookup"><span data-stu-id="5cf56-535">You can also define our custom error function to calculate MedianAPE and pass it to the err_fun argument.</span></span>


```python
def calc_median_ape(y_true, y_pred):
    y_true = np.array(y_true).astype(float)
    y_pred = np.array(y_pred).astype(float)
    y_true_rm_na = y_true[~(np.isnan(y_true) | np.isnan(y_pred))]
    y_pred_rm_na = y_pred[~(np.isnan(y_true) | np.isnan(y_pred))]
    y_true = y_true_rm_na
    y_pred = y_pred_rm_na
    if len(y_true) == 0:
        # if there is no entries left after removing na data, return np.nan
        return(np.nan)
    y_true_rm_zero = y_true[y_true != 0]
    y_pred_rm_zero = y_pred[y_true != 0]
    if len(y_true_rm_zero) == 0:
        # if all values are zero, np.nan will be returned.
        return(np.nan)
    ape = np.abs((y_true_rm_zero - y_pred_rm_zero) / y_true_rm_zero) * 100
    median_ape = np.median(ape)
    return median_ape
```


```python
forecaster_union_MAPE = forecaster_union_prediction.calc_error(err_name='MAPE',
                                                               by='ModelName')
forecaster_union_MedianAPE = forecaster_union_prediction.calc_error(err_name='MedianAPE', 
                                                                    err_fun=calc_median_ape,
                                                                    by='ModelName')

univariate_model_errors = forecaster_union_MAPE.merge(forecaster_union_MedianAPE, on='ModelName')
univariate_model_errors
```



<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th><span data-ttu-id="5cf56-536">ModelName</span><span class="sxs-lookup"><span data-stu-id="5cf56-536">ModelName</span></span></th>
      <th><span data-ttu-id="5cf56-537">MAPE</span><span class="sxs-lookup"><span data-stu-id="5cf56-537">MAPE</span></span></th>
      <th><span data-ttu-id="5cf56-538">MedianAPE</span><span class="sxs-lookup"><span data-stu-id="5cf56-538">MedianAPE</span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="5cf56-539">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-539">0</span></span></th>
      <td><span data-ttu-id="5cf56-540">arima</span><span class="sxs-lookup"><span data-stu-id="5cf56-540">arima</span></span></td>
      <td><span data-ttu-id="5cf56-541">126.57</span><span class="sxs-lookup"><span data-stu-id="5cf56-541">126.57</span></span></td>
      <td><span data-ttu-id="5cf56-542">66.49</span><span class="sxs-lookup"><span data-stu-id="5cf56-542">66.49</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-543">1</span><span class="sxs-lookup"><span data-stu-id="5cf56-543">1</span></span></th>
      <td><span data-ttu-id="5cf56-544">ets</span><span class="sxs-lookup"><span data-stu-id="5cf56-544">ets</span></span></td>
      <td><span data-ttu-id="5cf56-545">187.89</span><span class="sxs-lookup"><span data-stu-id="5cf56-545">187.89</span></span></td>
      <td><span data-ttu-id="5cf56-546">75.73</span><span class="sxs-lookup"><span data-stu-id="5cf56-546">75.73</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-547">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-547">2</span></span></th>
      <td><span data-ttu-id="5cf56-548">naive</span><span class="sxs-lookup"><span data-stu-id="5cf56-548">naive</span></span></td>
      <td><span data-ttu-id="5cf56-549">103.57</span><span class="sxs-lookup"><span data-stu-id="5cf56-549">103.57</span></span></td>
      <td><span data-ttu-id="5cf56-550">59.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-550">59.14</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-551">3</span><span class="sxs-lookup"><span data-stu-id="5cf56-551">3</span></span></th>
      <td><span data-ttu-id="5cf56-552">seasonal_naive</span><span class="sxs-lookup"><span data-stu-id="5cf56-552">seasonal_naive</span></span></td>
      <td><span data-ttu-id="5cf56-553">180.54</span><span class="sxs-lookup"><span data-stu-id="5cf56-553">180.54</span></span></td>
      <td><span data-ttu-id="5cf56-554">65.99</span><span class="sxs-lookup"><span data-stu-id="5cf56-554">65.99</span></span></td>
    </tr>
  </tbody>
</table>



## <a name="build-machine-learning-models"></a><span data-ttu-id="5cf56-555">Build machine learning models</span><span class="sxs-lookup"><span data-stu-id="5cf56-555">Build machine learning models</span></span>

<span data-ttu-id="5cf56-556">In addition to traditional univariate models, Azure Machine Learning Package for Forecasting also enables you to create machine learning models.</span><span class="sxs-lookup"><span data-stu-id="5cf56-556">In addition to traditional univariate models, Azure Machine Learning Package for Forecasting also enables you to create machine learning models.</span></span>

<span data-ttu-id="5cf56-557">For these models, begin by creating features.</span><span class="sxs-lookup"><span data-stu-id="5cf56-557">For these models, begin by creating features.</span></span>

### <a name="feature-engineering"></a><span data-ttu-id="5cf56-558">Feature Engineering</span><span class="sxs-lookup"><span data-stu-id="5cf56-558">Feature Engineering</span></span>

<span data-ttu-id="5cf56-559">**Transformers** </span><span class="sxs-lookup"><span data-stu-id="5cf56-559">**Transformers** </span></span>  
<span data-ttu-id="5cf56-560">The package provides many transformers for time series data preprocessing and featurization.</span><span class="sxs-lookup"><span data-stu-id="5cf56-560">The package provides many transformers for time series data preprocessing and featurization.</span></span> <span data-ttu-id="5cf56-561">The examples that follow demonstrate some of the preprocessing and featurization functionality.</span><span class="sxs-lookup"><span data-stu-id="5cf56-561">The examples that follow demonstrate some of the preprocessing and featurization functionality.</span></span>


```python
# DropColumns: Drop columns that should not be included for modeling. `logmove` is the log of the number of 
# units sold, so providing this number would be cheating. `WeekFirstDay` would be 
# redundant since we already have a feature for the last day of the week.
columns_to_drop = ['logmove', 'WeekFirstDay', 'week']
column_dropper = DropColumns(columns_to_drop)

# TimeSeriesImputer: Fill missing values in the features
# First, we need to create a dictionary with key as column names and value as values used to fill missing 
# values for that column. We are going to use the mean to fill missing values for each column.
columns_with_missing_values = train_imputed_tsdf.columns[pd.DataFrame(train_imputed_tsdf).isnull().any()].tolist()
columns_with_missing_values = [c for c in columns_with_missing_values if c not in columns_to_drop]
missing_value_imputation_dictionary = {}
for c in columns_with_missing_values:
    missing_value_imputation_dictionary[c] = train_imputed_tsdf[c].mean()
fillna_imputer = TimeSeriesImputer(option='fillna', 
                                   input_column=columns_with_missing_values,
                                   value=missing_value_imputation_dictionary)

# TimeIndexFeaturizer: extract temporal features from timestamps
time_index_featurizer = TimeIndexFeaturizer(correlation_cutoff=0.1, overwrite_columns=True)

# GrainIndexFeaturizer: create indicator variables for stores and brands
grain_featurizer = GrainIndexFeaturizer(overwrite_columns=True, ts_frequency=oj_series_freq)
```

<span data-ttu-id="5cf56-562">**Pipelines** </span><span class="sxs-lookup"><span data-stu-id="5cf56-562">**Pipelines** </span></span>  
<span data-ttu-id="5cf56-563">Pipeline objects make it easy to save a set of steps so they can be applied over and over again to different objects.</span><span class="sxs-lookup"><span data-stu-id="5cf56-563">Pipeline objects make it easy to save a set of steps so they can be applied over and over again to different objects.</span></span> <span data-ttu-id="5cf56-564">Also, pipeline objects can be pickled to make them easily portable to other machines for deployment.</span><span class="sxs-lookup"><span data-stu-id="5cf56-564">Also, pipeline objects can be pickled to make them easily portable to other machines for deployment.</span></span> <span data-ttu-id="5cf56-565">You can chain all the transformers you've created so far using a pipeline.</span><span class="sxs-lookup"><span data-stu-id="5cf56-565">You can chain all the transformers you've created so far using a pipeline.</span></span> 


```python
pipeline_ml = AzureMLForecastPipeline([('drop_columns', column_dropper), 
                                       ('fillna_imputer', fillna_imputer),
                                       ('time_index_featurizer', time_index_featurizer),
                                       ('grain_featurizer', grain_featurizer)
                                      ])


train_feature_tsdf = pipeline_ml.fit_transform(train_imputed_tsdf)
test_feature_tsdf = pipeline_ml.transform(test_tsdf)

# Let's get a look at our new feature set
print(train_feature_tsdf.head())
```

    F1 2018-06-14 23:10:03,472 INFO azureml.timeseries - pipeline fit_transform started. 
    F1 2018-06-14 23:10:07,317 INFO azureml.timeseries - pipeline fit_transform finished. Time elapsed 0:00:03.845078
    F1 2018-06-14 23:10:07,317 INFO azureml.timeseries - pipeline transforms started. 
    F1 2018-06-14 23:10:16,499 INFO azureml.timeseries - pipeline transforms finished. Time elapsed 0:00:09.182314
                                           feat  price  AGE60  EDUC  ETHNIC  \
    WeekLastDay         store brand                                           
    1990-06-20 23:59:59 2     dominicks    1.00   1.59   0.23  0.25    0.11   
                              minute.maid  0.00   3.17   0.23  0.25    0.11   
                              tropicana    0.00   3.87   0.23  0.25    0.11   
                        5     dominicks    1.00   1.59   0.12  0.32    0.05   
                              minute.maid  0.00   2.99   0.12  0.32    0.05   
    
                                           INCOME  HHLARGE  WORKWOM  HVAL150  \
    WeekLastDay         store brand                                            
    1990-06-20 23:59:59 2     dominicks     10.55     0.10     0.30     0.46   
                              minute.maid   10.55     0.10     0.30     0.46   
                              tropicana     10.55     0.10     0.30     0.46   
                        5     dominicks     10.92     0.10     0.41     0.54   
                              minute.maid   10.92     0.10     0.41     0.54   
    
                                           SSTRDIST     ...       CPWVOL5  \
    WeekLastDay         store brand                     ...                 
    1990-06-20 23:59:59 2     dominicks        2.11     ...          0.38   
                              minute.maid      2.11     ...          0.38   
                              tropicana        2.11     ...          0.38   
                        5     dominicks        3.80     ...          0.74   
                              minute.maid      3.80     ...          0.74   
    
                                           Quantity  TEMP  DEWP  WDSP  PRCP  year  \
    WeekLastDay         store brand                                                 
    1990-06-20 23:59:59 2     dominicks    10560.00 72.00 61.87  9.74  0.19  1990   
                              minute.maid   4480.00 72.00 61.87  9.74  0.19  1990   
                              tropicana     8256.00 72.00 61.87  9.74  0.19  1990   
                        5     dominicks     1792.00 72.00 61.87  9.74  0.19  1990   
                              minute.maid   4224.00 72.00 61.87  9.74  0.19  1990   
    
                                           day  grain_brand  grain_store  
    WeekLastDay         store brand                                       
    1990-06-20 23:59:59 2     dominicks     20    dominicks            2  
                              minute.maid   20  minute.maid            2  
                              tropicana     20    tropicana            2  
                        5     dominicks     20    dominicks            5  
                              minute.maid   20  minute.maid            5  
    
    [5 rows x 22 columns]
    

 <span data-ttu-id="5cf56-566">**RegressionForecaster**</span><span class="sxs-lookup"><span data-stu-id="5cf56-566">**RegressionForecaster**</span></span>

<span data-ttu-id="5cf56-567">The [RegressionForecaster](https://docs.microsoft.com/en-us/python/api/ftk.models.regression_forecaster.regressionforecaster?view=azure-ml-py-latest)  function wraps sklearn regression estimators so that they can be trained on TimeSeriesDataFrame.</span><span class="sxs-lookup"><span data-stu-id="5cf56-567">The [RegressionForecaster](https://docs.microsoft.com/en-us/python/api/ftk.models.regression_forecaster.regressionforecaster?view=azure-ml-py-latest)  function wraps sklearn regression estimators so that they can be trained on TimeSeriesDataFrame.</span></span> <span data-ttu-id="5cf56-568">The wrapped forecaster also puts each group, in this case store, into the same model.</span><span class="sxs-lookup"><span data-stu-id="5cf56-568">The wrapped forecaster also puts each group, in this case store, into the same model.</span></span> <span data-ttu-id="5cf56-569">The forecaster can learn one model for a group of series that were deemed similar and can be pooled together.</span><span class="sxs-lookup"><span data-stu-id="5cf56-569">The forecaster can learn one model for a group of series that were deemed similar and can be pooled together.</span></span> <span data-ttu-id="5cf56-570">One model for a group of series often uses the data from longer series to improve forecasts for short series.</span><span class="sxs-lookup"><span data-stu-id="5cf56-570">One model for a group of series often uses the data from longer series to improve forecasts for short series.</span></span> <span data-ttu-id="5cf56-571">You can substitute these models for any other models in the library that support regression.</span><span class="sxs-lookup"><span data-stu-id="5cf56-571">You can substitute these models for any other models in the library that support regression.</span></span> 


```python
lasso_model = RegressionForecaster(estimator=Lasso(),
                                   make_grain_features=False)
elastic_net_model = RegressionForecaster(estimator=ElasticNet(),
                                         make_grain_features=False)
knn_model = RegressionForecaster(estimator=KNeighborsRegressor(),
                                 make_grain_features=False)
random_forest_model = RegressionForecaster(estimator=RandomForestRegressor(),
                                           make_grain_features=False)
boosted_trees_model = RegressionForecaster(estimator=GradientBoostingRegressor(),
                                           make_grain_features=False)

ml_union = ForecasterUnion(forecaster_list=[
    ('lasso', lasso_model), 
    ('elastic_net', elastic_net_model), 
    ('knn', knn_model), 
    ('random_forest', random_forest_model), 
    ('boosted_trees', boosted_trees_model)
]) 
```


```python
ml_union.fit(train_feature_tsdf, y=train_feature_tsdf.ts_value)
ml_results = ml_union.predict(test_feature_tsdf, retain_feature_column=True)
```


```python
ml_model_MAPE = ml_results.calc_error(err_name='MAPE', by='ModelName')
ml_model_MedianAPE = ml_results.calc_error(err_name='MedianAPE', 
                                           err_fun=calc_median_ape,
                                           by='ModelName')
ml_model_errors = ml_model_MAPE.merge(ml_model_MedianAPE, on='ModelName')
all_errors = pd.concat([univariate_model_errors, ml_model_errors])
all_errors.sort_values('MedianAPE')
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th><span data-ttu-id="5cf56-572">ModelName</span><span class="sxs-lookup"><span data-stu-id="5cf56-572">ModelName</span></span></th>
      <th><span data-ttu-id="5cf56-573">MAPE</span><span class="sxs-lookup"><span data-stu-id="5cf56-573">MAPE</span></span></th>
      <th><span data-ttu-id="5cf56-574">MedianAPE</span><span class="sxs-lookup"><span data-stu-id="5cf56-574">MedianAPE</span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="5cf56-575">4</span><span class="sxs-lookup"><span data-stu-id="5cf56-575">4</span></span></th>
      <td><span data-ttu-id="5cf56-576">random_forest</span><span class="sxs-lookup"><span data-stu-id="5cf56-576">random_forest</span></span></td>
      <td><span data-ttu-id="5cf56-577">78.82</span><span class="sxs-lookup"><span data-stu-id="5cf56-577">78.82</span></span></td>
      <td><span data-ttu-id="5cf56-578">42.81</span><span class="sxs-lookup"><span data-stu-id="5cf56-578">42.81</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-579">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-579">0</span></span></th>
      <td><span data-ttu-id="5cf56-580">boosted_trees</span><span class="sxs-lookup"><span data-stu-id="5cf56-580">boosted_trees</span></span></td>
      <td><span data-ttu-id="5cf56-581">78.46</span><span class="sxs-lookup"><span data-stu-id="5cf56-581">78.46</span></span></td>
      <td><span data-ttu-id="5cf56-582">45.37</span><span class="sxs-lookup"><span data-stu-id="5cf56-582">45.37</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-583">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-583">2</span></span></th>
      <td><span data-ttu-id="5cf56-584">naive</span><span class="sxs-lookup"><span data-stu-id="5cf56-584">naive</span></span></td>
      <td><span data-ttu-id="5cf56-585">103.57</span><span class="sxs-lookup"><span data-stu-id="5cf56-585">103.57</span></span></td>
      <td><span data-ttu-id="5cf56-586">59.14</span><span class="sxs-lookup"><span data-stu-id="5cf56-586">59.14</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-587">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-587">2</span></span></th>
      <td><span data-ttu-id="5cf56-588">knn</span><span class="sxs-lookup"><span data-stu-id="5cf56-588">knn</span></span></td>
      <td><span data-ttu-id="5cf56-589">129.85</span><span class="sxs-lookup"><span data-stu-id="5cf56-589">129.85</span></span></td>
      <td><span data-ttu-id="5cf56-590">65.37</span><span class="sxs-lookup"><span data-stu-id="5cf56-590">65.37</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-591">1</span><span class="sxs-lookup"><span data-stu-id="5cf56-591">1</span></span></th>
      <td><span data-ttu-id="5cf56-592">elastic_net</span><span class="sxs-lookup"><span data-stu-id="5cf56-592">elastic_net</span></span></td>
      <td><span data-ttu-id="5cf56-593">125.11</span><span class="sxs-lookup"><span data-stu-id="5cf56-593">125.11</span></span></td>
      <td><span data-ttu-id="5cf56-594">65.59</span><span class="sxs-lookup"><span data-stu-id="5cf56-594">65.59</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-595">3</span><span class="sxs-lookup"><span data-stu-id="5cf56-595">3</span></span></th>
      <td><span data-ttu-id="5cf56-596">seasonal_naive</span><span class="sxs-lookup"><span data-stu-id="5cf56-596">seasonal_naive</span></span></td>
      <td><span data-ttu-id="5cf56-597">180.54</span><span class="sxs-lookup"><span data-stu-id="5cf56-597">180.54</span></span></td>
      <td><span data-ttu-id="5cf56-598">65.99</span><span class="sxs-lookup"><span data-stu-id="5cf56-598">65.99</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-599">0</span><span class="sxs-lookup"><span data-stu-id="5cf56-599">0</span></span></th>
      <td><span data-ttu-id="5cf56-600">arima</span><span class="sxs-lookup"><span data-stu-id="5cf56-600">arima</span></span></td>
      <td><span data-ttu-id="5cf56-601">126.57</span><span class="sxs-lookup"><span data-stu-id="5cf56-601">126.57</span></span></td>
      <td><span data-ttu-id="5cf56-602">66.49</span><span class="sxs-lookup"><span data-stu-id="5cf56-602">66.49</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-603">3</span><span class="sxs-lookup"><span data-stu-id="5cf56-603">3</span></span></th>
      <td><span data-ttu-id="5cf56-604">lasso</span><span class="sxs-lookup"><span data-stu-id="5cf56-604">lasso</span></span></td>
      <td><span data-ttu-id="5cf56-605">112.87</span><span class="sxs-lookup"><span data-stu-id="5cf56-605">112.87</span></span></td>
      <td><span data-ttu-id="5cf56-606">67.92</span><span class="sxs-lookup"><span data-stu-id="5cf56-606">67.92</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-607">1</span><span class="sxs-lookup"><span data-stu-id="5cf56-607">1</span></span></th>
      <td><span data-ttu-id="5cf56-608">ets</span><span class="sxs-lookup"><span data-stu-id="5cf56-608">ets</span></span></td>
      <td><span data-ttu-id="5cf56-609">187.89</span><span class="sxs-lookup"><span data-stu-id="5cf56-609">187.89</span></span></td>
      <td><span data-ttu-id="5cf56-610">75.73</span><span class="sxs-lookup"><span data-stu-id="5cf56-610">75.73</span></span></td>
    </tr>
  </tbody>
</table>



<span data-ttu-id="5cf56-611">Some machine learning models were able to take advantage of the added features and the similarities between series to get better forecast accuracy.</span><span class="sxs-lookup"><span data-stu-id="5cf56-611">Some machine learning models were able to take advantage of the added features and the similarities between series to get better forecast accuracy.</span></span>

### <a name="cross-validation-parameter-and-model-sweeping"></a><span data-ttu-id="5cf56-612">Cross Validation, Parameter, and Model Sweeping</span><span class="sxs-lookup"><span data-stu-id="5cf56-612">Cross Validation, Parameter, and Model Sweeping</span></span>    

<span data-ttu-id="5cf56-613">The package adapts some traditional machine learning functions for a forecasting application.</span><span class="sxs-lookup"><span data-stu-id="5cf56-613">The package adapts some traditional machine learning functions for a forecasting application.</span></span>  <span data-ttu-id="5cf56-614">[RollingOriginValidator](https://docs.microsoft.com/python/api/ftk.model_selection.cross_validation.rollingoriginvalidator?view=azure-ml-py-latest) does cross-validation temporally, respecting what would and would not be known in a forecasting framework.</span><span class="sxs-lookup"><span data-stu-id="5cf56-614">[RollingOriginValidator](https://docs.microsoft.com/python/api/ftk.model_selection.cross_validation.rollingoriginvalidator?view=azure-ml-py-latest) does cross-validation temporally, respecting what would and would not be known in a forecasting framework.</span></span> 

<span data-ttu-id="5cf56-615">In the figure below, each square represents data from one time point.</span><span class="sxs-lookup"><span data-stu-id="5cf56-615">In the figure below, each square represents data from one time point.</span></span> <span data-ttu-id="5cf56-616">The blue squares represent training and orange squares represent testing in each fold.</span><span class="sxs-lookup"><span data-stu-id="5cf56-616">The blue squares represent training and orange squares represent testing in each fold.</span></span> <span data-ttu-id="5cf56-617">Testing data must come from the time points after the largest training time point.</span><span class="sxs-lookup"><span data-stu-id="5cf56-617">Testing data must come from the time points after the largest training time point.</span></span> <span data-ttu-id="5cf56-618">Otherwise, future data is leaked into training data causing the model evaluation to become invalid.</span><span class="sxs-lookup"><span data-stu-id="5cf56-618">Otherwise, future data is leaked into training data causing the model evaluation to become invalid.</span></span> 
<span data-ttu-id="5cf56-619">![png](./media/how-to-build-deploy-forecast-models/cv_figure.PNG)</span><span class="sxs-lookup"><span data-stu-id="5cf56-619">![png](./media/how-to-build-deploy-forecast-models/cv_figure.PNG)</span></span>

<span data-ttu-id="5cf56-620">**Parameter Sweeping**</span><span class="sxs-lookup"><span data-stu-id="5cf56-620">**Parameter Sweeping**</span></span>  
<span data-ttu-id="5cf56-621">The [TSGridSearchCV](https://docs.microsoft.com/en-us/python/api/ftk.model_selection.search.tsgridsearchcv?view=azure-ml-py-latest) class exhaustively searches over specified parameter values and uses `RollingOriginValidator` to evaluate parameter performance in order to find the best parameters.</span><span class="sxs-lookup"><span data-stu-id="5cf56-621">The [TSGridSearchCV](https://docs.microsoft.com/en-us/python/api/ftk.model_selection.search.tsgridsearchcv?view=azure-ml-py-latest) class exhaustively searches over specified parameter values and uses `RollingOriginValidator` to evaluate parameter performance in order to find the best parameters.</span></span>


```python
# Set up the `RollingOriginValidator` to do 2 folds of rolling origin cross-validation
rollcv = RollingOriginValidator(n_splits=2)
randomforest_model_for_cv = RegressionForecaster(estimator=RandomForestRegressor(),
                                                 make_grain_features=False)

# Set up our parameter grid and feed it to our grid search algorithm
param_grid_rf = {'estimator__n_estimators': np.array([10, 50, 100])}
grid_cv_rf = TSGridSearchCV(randomforest_model_for_cv, param_grid_rf, cv=rollcv)

# fit and predict
randomforest_cv_fitted= grid_cv_rf.fit(train_feature_tsdf, y=train_feature_tsdf.ts_value)
print('Best paramter: {}'.format(randomforest_cv_fitted.best_params_))
```

    Best paramter: {'estimator__n_estimators': 100}
    

<span data-ttu-id="5cf56-622">**Model Sweeping**</span><span class="sxs-lookup"><span data-stu-id="5cf56-622">**Model Sweeping**</span></span>  
<span data-ttu-id="5cf56-623">The `BestOfForecaster` class selects the model with the best performance from a list of given models.</span><span class="sxs-lookup"><span data-stu-id="5cf56-623">The `BestOfForecaster` class selects the model with the best performance from a list of given models.</span></span> <span data-ttu-id="5cf56-624">Similar to `TSGridSearchCV`, it also uses RollingOriginValidator for cross validation and performance evaluation.</span><span class="sxs-lookup"><span data-stu-id="5cf56-624">Similar to `TSGridSearchCV`, it also uses RollingOriginValidator for cross validation and performance evaluation.</span></span>  
<span data-ttu-id="5cf56-625">Here we pass a list of two models to demonstrate the usage of `BestOfForecaster`</span><span class="sxs-lookup"><span data-stu-id="5cf56-625">Here we pass a list of two models to demonstrate the usage of `BestOfForecaster`</span></span>


```python
best_of_forecaster = BestOfForecaster(forecaster_list=[('naive', naive_model), 
                                                       ('random_forest', random_forest_model)])
best_of_forecaster_fitted = best_of_forecaster.fit(train_feature_tsdf,
                                                   validator=RollingOriginValidator(n_step=20, max_horizon=40))
best_of_forecaster_prediction = best_of_forecaster_fitted.predict(test_feature_tsdf)
best_of_forecaster_prediction.head()
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th><span data-ttu-id="5cf56-626">PointForecast</span><span class="sxs-lookup"><span data-stu-id="5cf56-626">PointForecast</span></span></th>
      <th><span data-ttu-id="5cf56-627">DistributionForecast</span><span class="sxs-lookup"><span data-stu-id="5cf56-627">DistributionForecast</span></span></th>
      <th><span data-ttu-id="5cf56-628">Quantity</span><span class="sxs-lookup"><span data-stu-id="5cf56-628">Quantity</span></span></th>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-629">WeekLastDay</span><span class="sxs-lookup"><span data-stu-id="5cf56-629">WeekLastDay</span></span></th>
      <th><span data-ttu-id="5cf56-630">store</span><span class="sxs-lookup"><span data-stu-id="5cf56-630">store</span></span></th>
      <th><span data-ttu-id="5cf56-631">brand</span><span class="sxs-lookup"><span data-stu-id="5cf56-631">brand</span></span></th>
      <th><span data-ttu-id="5cf56-632">ForecastOriginTime</span><span class="sxs-lookup"><span data-stu-id="5cf56-632">ForecastOriginTime</span></span></th>
      <th><span data-ttu-id="5cf56-633">ModelName</span><span class="sxs-lookup"><span data-stu-id="5cf56-633">ModelName</span></span></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="5cf56-634">1992-01-08 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-634">1992-01-08 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-635">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-635">2</span></span></th>
      <th><span data-ttu-id="5cf56-636">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-636">dominicks</span></span></th>
      <th><span data-ttu-id="5cf56-637">1992-01-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-637">1992-01-01 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-638">random_forest</span><span class="sxs-lookup"><span data-stu-id="5cf56-638">random_forest</span></span></th>
      <td><span data-ttu-id="5cf56-639">9299.20</span><span class="sxs-lookup"><span data-stu-id="5cf56-639">9299.20</span></span></td>
      <td><span data-ttu-id="5cf56-640">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span><span class="sxs-lookup"><span data-stu-id="5cf56-640">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span></span></td>
      <td><span data-ttu-id="5cf56-641">11712.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-641">11712.00</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-642">1992-01-15 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-642">1992-01-15 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-643">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-643">2</span></span></th>
      <th><span data-ttu-id="5cf56-644">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-644">dominicks</span></span></th>
      <th><span data-ttu-id="5cf56-645">1992-01-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-645">1992-01-01 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-646">random_forest</span><span class="sxs-lookup"><span data-stu-id="5cf56-646">random_forest</span></span></th>
      <td><span data-ttu-id="5cf56-647">10259.20</span><span class="sxs-lookup"><span data-stu-id="5cf56-647">10259.20</span></span></td>
      <td><span data-ttu-id="5cf56-648">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span><span class="sxs-lookup"><span data-stu-id="5cf56-648">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span></span></td>
      <td><span data-ttu-id="5cf56-649">4032.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-649">4032.00</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-650">1992-01-22 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-650">1992-01-22 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-651">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-651">2</span></span></th>
      <th><span data-ttu-id="5cf56-652">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-652">dominicks</span></span></th>
      <th><span data-ttu-id="5cf56-653">1992-01-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-653">1992-01-01 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-654">random_forest</span><span class="sxs-lookup"><span data-stu-id="5cf56-654">random_forest</span></span></th>
      <td><span data-ttu-id="5cf56-655">6828.80</span><span class="sxs-lookup"><span data-stu-id="5cf56-655">6828.80</span></span></td>
      <td><span data-ttu-id="5cf56-656">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span><span class="sxs-lookup"><span data-stu-id="5cf56-656">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span></span></td>
      <td><span data-ttu-id="5cf56-657">6336.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-657">6336.00</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-658">1992-01-29 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-658">1992-01-29 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-659">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-659">2</span></span></th>
      <th><span data-ttu-id="5cf56-660">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-660">dominicks</span></span></th>
      <th><span data-ttu-id="5cf56-661">1992-01-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-661">1992-01-01 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-662">random_forest</span><span class="sxs-lookup"><span data-stu-id="5cf56-662">random_forest</span></span></th>
      <td><span data-ttu-id="5cf56-663">16633.60</span><span class="sxs-lookup"><span data-stu-id="5cf56-663">16633.60</span></span></td>
      <td><span data-ttu-id="5cf56-664">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span><span class="sxs-lookup"><span data-stu-id="5cf56-664">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span></span></td>
      <td><span data-ttu-id="5cf56-665">13632.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-665">13632.00</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="5cf56-666">1992-02-05 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-666">1992-02-05 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-667">2</span><span class="sxs-lookup"><span data-stu-id="5cf56-667">2</span></span></th>
      <th><span data-ttu-id="5cf56-668">dominicks</span><span class="sxs-lookup"><span data-stu-id="5cf56-668">dominicks</span></span></th>
      <th><span data-ttu-id="5cf56-669">1992-01-01 23:59:59</span><span class="sxs-lookup"><span data-stu-id="5cf56-669">1992-01-01 23:59:59</span></span></th>
      <th><span data-ttu-id="5cf56-670">random_forest</span><span class="sxs-lookup"><span data-stu-id="5cf56-670">random_forest</span></span></th>
      <td><span data-ttu-id="5cf56-671">12774.40</span><span class="sxs-lookup"><span data-stu-id="5cf56-671">12774.40</span></span></td>
      <td><span data-ttu-id="5cf56-672">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span><span class="sxs-lookup"><span data-stu-id="5cf56-672">&lt;scipy.stats._distn_infrastructure.rv_frozen o...</span></span></td>
      <td><span data-ttu-id="5cf56-673">45120.00</span><span class="sxs-lookup"><span data-stu-id="5cf56-673">45120.00</span></span></td>
    </tr>
  </tbody>
</table>



<span data-ttu-id="5cf56-674">**Build the final pipeline** </span><span class="sxs-lookup"><span data-stu-id="5cf56-674">**Build the final pipeline** </span></span>  
<span data-ttu-id="5cf56-675">Now that you have identified the best model, you can build and fit your final pipeline with all transformers and the best model.</span><span class="sxs-lookup"><span data-stu-id="5cf56-675">Now that you have identified the best model, you can build and fit your final pipeline with all transformers and the best model.</span></span> 


```python
random_forest_model_final = RegressionForecaster(estimator=RandomForestRegressor(100),make_grain_features=False)
pipeline_ml.add_pipeline_step('random_forest_estimator', random_forest_model_final)
pipeline_ml_fitted = pipeline_ml.fit(train_imputed_tsdf)
final_prediction = pipeline_ml_fitted.predict(test_tsdf)
final_median_ape = final_prediction.calc_error(err_name='MedianAPE', err_fun=calc_median_ape)
print('Median of APE of final pipeline: {0}'.format(final_median_ape))
```

    F1 2018-05-04 11:07:04,108 INFO azureml.timeseries - pipeline fit started. 
    F1 2018-05-04 11:07:43,121 INFO azureml.timeseries - pipeline fit finished. Time elapsed 0:00:39.012880
    F1 2018-05-04 11:07:43,136 INFO azureml.timeseries - pipeline predict started. 
    F1 2018-05-04 11:08:03,564 INFO azureml.timeseries - pipeline predict finished. Time elapsed 0:00:20.428147
    Median of APE of final pipeline: 42.54336821266968
    

## <a name="visualization"></a><span data-ttu-id="5cf56-676">Visualization</span><span class="sxs-lookup"><span data-stu-id="5cf56-676">Visualization</span></span>
<span data-ttu-id="5cf56-677">The `ForecastDataFrame` class provides plotting functions for visualizing and analyzing forecasting results.</span><span class="sxs-lookup"><span data-stu-id="5cf56-677">The `ForecastDataFrame` class provides plotting functions for visualizing and analyzing forecasting results.</span></span> <span data-ttu-id="5cf56-678">Use the commonly used charts with your data.</span><span class="sxs-lookup"><span data-stu-id="5cf56-678">Use the commonly used charts with your data.</span></span> <span data-ttu-id="5cf56-679">Please see the sample notebook below on plotting functions for all the functions available.</span><span class="sxs-lookup"><span data-stu-id="5cf56-679">Please see the sample notebook below on plotting functions for all the functions available.</span></span> 

<span data-ttu-id="5cf56-680">The `show_error` function plots performance metrics aggregated by an arbitrary column.</span><span class="sxs-lookup"><span data-stu-id="5cf56-680">The `show_error` function plots performance metrics aggregated by an arbitrary column.</span></span> <span data-ttu-id="5cf56-681">By default, the `show_error` function aggregates by the `grain_colnames` of the `ForecastDataFrame`.</span><span class="sxs-lookup"><span data-stu-id="5cf56-681">By default, the `show_error` function aggregates by the `grain_colnames` of the `ForecastDataFrame`.</span></span> <span data-ttu-id="5cf56-682">It's often useful to identify the grains/groups with the best or worst performance, especially when you have a large number of time series.</span><span class="sxs-lookup"><span data-stu-id="5cf56-682">It's often useful to identify the grains/groups with the best or worst performance, especially when you have a large number of time series.</span></span> <span data-ttu-id="5cf56-683">The `performance_percent` argument of `show_error` allows you to specify a performance interval and plot the error of a subset of grains/groups.</span><span class="sxs-lookup"><span data-stu-id="5cf56-683">The `performance_percent` argument of `show_error` allows you to specify a performance interval and plot the error of a subset of grains/groups.</span></span>

<span data-ttu-id="5cf56-684">Plot the grains with the bottom 5% performance, i.e. top 5% MedianAPE</span><span class="sxs-lookup"><span data-stu-id="5cf56-684">Plot the grains with the bottom 5% performance, i.e. top 5% MedianAPE</span></span>


```python
fig, ax = best_of_forecaster_prediction.show_error(err_name='MedianAPE', err_fun=calc_median_ape, performance_percent=(0.95, 1))
```

![png](./media/how-to-build-deploy-forecast-models/output_59_0.png)


<span data-ttu-id="5cf56-686">Plot the grains with the top 5% of performance, i.e. bottom 5% MedianAPE.</span><span class="sxs-lookup"><span data-stu-id="5cf56-686">Plot the grains with the top 5% of performance, i.e. bottom 5% MedianAPE.</span></span>


```python
fig, ax = best_of_forecaster_prediction.show_error(err_name='MedianAPE', err_fun=calc_median_ape, performance_percent=(0, 0.05))
```


![png](./media/how-to-build-deploy-forecast-models/output_61_0.png)


<span data-ttu-id="5cf56-688">Once you have an idea of the overall performance, you may want to explore individual grains, especially those that performed poorly.</span><span class="sxs-lookup"><span data-stu-id="5cf56-688">Once you have an idea of the overall performance, you may want to explore individual grains, especially those that performed poorly.</span></span> <span data-ttu-id="5cf56-689">The `plot_forecast_by_grain` method plots forecast vs. actual of specified grains.</span><span class="sxs-lookup"><span data-stu-id="5cf56-689">The `plot_forecast_by_grain` method plots forecast vs. actual of specified grains.</span></span> <span data-ttu-id="5cf56-690">Here, we plot the grain with the best performance and the grain with the worst performance discovered in the `show_error` plot.</span><span class="sxs-lookup"><span data-stu-id="5cf56-690">Here, we plot the grain with the best performance and the grain with the worst performance discovered in the `show_error` plot.</span></span>


```python
fig_ax = best_of_forecaster_prediction.plot_forecast_by_grain(grains=[(33, 'tropicana'), (128, 'minute.maid')])
```


![png](./media/how-to-build-deploy-forecast-models/output_63_0.png)



![png](./media/how-to-build-deploy-forecast-models/output_63_1.png)



## <a name="additional-notebooks"></a><span data-ttu-id="5cf56-693">Additional Notebooks</span><span class="sxs-lookup"><span data-stu-id="5cf56-693">Additional Notebooks</span></span>
<span data-ttu-id="5cf56-694">For a deeper dive on the major features of AMLPF, please refer to the following notebooks with more details and examples of each feature:</span><span class="sxs-lookup"><span data-stu-id="5cf56-694">For a deeper dive on the major features of AMLPF, please refer to the following notebooks with more details and examples of each feature:</span></span>  
[<span data-ttu-id="5cf56-695">Notebook on TimeSeriesDataFrame</span><span class="sxs-lookup"><span data-stu-id="5cf56-695">Notebook on TimeSeriesDataFrame</span></span>](https://azuremlftkrelease.blob.core.windows.net/samples/feature_notebooks/Introduction_to_TimeSeriesDataFrames.ipynb)  
[<span data-ttu-id="5cf56-696">Notebook on Data Wrangling</span><span class="sxs-lookup"><span data-stu-id="5cf56-696">Notebook on Data Wrangling</span></span>](https://azuremlftkrelease.blob.core.windows.net/samples/feature_notebooks/Data_Wrangling_Sample.ipynb)  
[<span data-ttu-id="5cf56-697">Notebook on Transformers</span><span class="sxs-lookup"><span data-stu-id="5cf56-697">Notebook on Transformers</span></span>](https://azuremlftkrelease.blob.core.windows.net/samples/feature_notebooks/Forecast_Package_Transforms.ipynb)  
[<span data-ttu-id="5cf56-698">Notebook on Models</span><span class="sxs-lookup"><span data-stu-id="5cf56-698">Notebook on Models</span></span>](https://azuremlftkrelease.blob.core.windows.net/samples/feature_notebooks/AMLPF_models_sample_notebook.ipynb)  
[<span data-ttu-id="5cf56-699">Notebook on Cross Validation</span><span class="sxs-lookup"><span data-stu-id="5cf56-699">Notebook on Cross Validation</span></span>](https://azuremlftkrelease.blob.core.windows.net/samples/feature_notebooks/Time_Series_Cross_Validation.ipynb)  
[<span data-ttu-id="5cf56-700">Notebook on Lag Transformer and OriginTime</span><span class="sxs-lookup"><span data-stu-id="5cf56-700">Notebook on Lag Transformer and OriginTime</span></span>](https://azuremlftkrelease.blob.core.windows.net/samples/feature_notebooks/Constructing_Lags_and_Explaining_Origin_Times.ipynb)  
[<span data-ttu-id="5cf56-701">Notebook on Plotting Functions</span><span class="sxs-lookup"><span data-stu-id="5cf56-701">Notebook on Plotting Functions</span></span>](https://azuremlftkrelease.blob.core.windows.net/samples/feature_notebooks/Plotting_Functions_in_AMLPF.ipynb)

## <a name="operationalization"></a><span data-ttu-id="5cf56-702">Operationalization</span><span class="sxs-lookup"><span data-stu-id="5cf56-702">Operationalization</span></span>

<span data-ttu-id="5cf56-703">In this section, you deploy a pipeline as an Azure Machine Learning web service and consume it for training and scoring.</span><span class="sxs-lookup"><span data-stu-id="5cf56-703">In this section, you deploy a pipeline as an Azure Machine Learning web service and consume it for training and scoring.</span></span>
<span data-ttu-id="5cf56-704">Currently, only pipelines there are not fitted are supported for deployment.</span><span class="sxs-lookup"><span data-stu-id="5cf56-704">Currently, only pipelines there are not fitted are supported for deployment.</span></span> <span data-ttu-id="5cf56-705">Scoring the deployed web service retrains the model and generates forecasts on new data.</span><span class="sxs-lookup"><span data-stu-id="5cf56-705">Scoring the deployed web service retrains the model and generates forecasts on new data.</span></span>

### <a name="set-model-deployment-parameters"></a><span data-ttu-id="5cf56-706">Set model deployment parameters</span><span class="sxs-lookup"><span data-stu-id="5cf56-706">Set model deployment parameters</span></span>

<span data-ttu-id="5cf56-707">Change the following parameters to your own values.</span><span class="sxs-lookup"><span data-stu-id="5cf56-707">Change the following parameters to your own values.</span></span> <span data-ttu-id="5cf56-708">Make sure your Azure Machine Learning environment, model management account, and resource group are located in the same region.</span><span class="sxs-lookup"><span data-stu-id="5cf56-708">Make sure your Azure Machine Learning environment, model management account, and resource group are located in the same region.</span></span>


```python
azure_subscription = '<subscription name>'

# Two deployment modes are supported: 'local' and 'cluster'. 
# 'local' deployment deploys to a local docker container.
# 'cluster' deployment deploys to a Azure Container Service Kubernetes-based cluster
deployment_type = '<deployment mode>'

# The deployment environment name. 
# This could be an existing environment or a new environment to be created automatically.
aml_env_name = '<deployment env name>'

# The resource group that contains the Azure resources related to the AML environment.
aml_env_resource_group = '<env resource group name>'

# The location where the Azure resources related to the AML environment are located at.
aml_env_location = '<env resource location>'

# The AML model management account name. This could be an existing model management account a new model management 
# account to be created automatically. 
model_management_account_name = '<model management account name>'

# The resource group that contains the Azure resources related to the model management account.
model_management_account_resource_group = '<model management account resource group>'

# The location where the Azure resources related to the model management account are located at.
model_management_account_location = '<model management account location>'

# The name of the deployment/web service.
deployment_name = '<web service name>'

# The directory to store deployment related files, such as pipeline pickle file, score script, 
# and conda dependencies file. 
deployment_working_directory = '<local working directory>'
```

### <a name="define-the-azure-machine-learning-environment-and-deployment"></a><span data-ttu-id="5cf56-709">Define the Azure Machine Learning environment and deployment</span><span class="sxs-lookup"><span data-stu-id="5cf56-709">Define the Azure Machine Learning environment and deployment</span></span>


```python
aml_settings = AMLSettings(azure_subscription=azure_subscription,
                     env_name=aml_env_name, 
                     env_resource_group=aml_env_resource_group,
                     env_location=aml_env_location, 
                     model_management_account_name=model_management_account_name, 
                     model_management_account_resource_group=model_management_account_resource_group,
                     model_management_account_location=model_management_account_location,
                     cluster=deployment_type)

random_forest_model_deploy = RegressionForecaster(estimator=RandomForestRegressor(),make_grain_features=False)
pipeline_deploy = AzureMLForecastPipeline([('drop_columns', column_dropper), 
                                           ('fillna_imputer', fillna_imputer),
                                           ('time_index_featurizer', time_index_featurizer),
                                           ('random_forest_estimator', random_forest_model_deploy)
                                          ])

aml_deployment = ForecastWebserviceFactory(deployment_name=deployment_name,
                                           aml_settings=aml_settings, 
                                           pipeline=pipeline_deploy,
                                           deployment_working_directory=deployment_working_directory,
                                           ftk_wheel_loc='https://azuremlftkrelease.blob.core.windows.net/dailyrelease/azuremlftk-0.1.18165.29a1-py3-none-any.whl')
```

### <a name="create-the-web-service"></a><span data-ttu-id="5cf56-710">Create the web service</span><span class="sxs-lookup"><span data-stu-id="5cf56-710">Create the web service</span></span>


```python
# This step can take 5 to 20 minutes
aml_deployment.deploy()
```

### <a name="score-the-web-service"></a><span data-ttu-id="5cf56-711">Score the web service</span><span class="sxs-lookup"><span data-stu-id="5cf56-711">Score the web service</span></span>

<span data-ttu-id="5cf56-712">To score a small dataset, use the [score](https://docs.microsoft.com/python/api/ftk.operationalization.deployment.amlwebservice)  method to submit one web service call for all the data.</span><span class="sxs-lookup"><span data-stu-id="5cf56-712">To score a small dataset, use the [score](https://docs.microsoft.com/python/api/ftk.operationalization.deployment.amlwebservice)  method to submit one web service call for all the data.</span></span>


```python
# Need to add empty prediction columns to the validation data frame and create a ForecastDataFrame.
# The scoring API will be updated in later versions to take TimeSeriesDataFrame directly. 
validate_tsdf = test_tsdf.assign(PointForecast=0.0, DistributionForecast=np.nan)
validate_fcast = ForecastDataFrame(validate_tsdf, pred_point='PointForecast', pred_dist='DistributionForecast')

# Define Score Context
score_context = ScoreContext(input_training_data_tsdf=train_imputed_tsdf,
                             input_scoring_data_fcdf=validate_fcast, 
                             pipeline_execution_type='train_predict')

# Get deployed web service
aml_web_service = aml_deployment.get_deployment()

# Score the web service
results = aml_web_service.score(score_context=score_context)
```

<span data-ttu-id="5cf56-713">To score a large dataset, use the [parallel scoring](https://docs.microsoft.com/python/api/ftk.operationalization.deployment.amlwebservice) mode to submit multiple web service calls, one for each group of data.</span><span class="sxs-lookup"><span data-stu-id="5cf56-713">To score a large dataset, use the [parallel scoring](https://docs.microsoft.com/python/api/ftk.operationalization.deployment.amlwebservice) mode to submit multiple web service calls, one for each group of data.</span></span>


```python
results = aml_web_service.score(score_context=score_context, method='parallel')
```

## <a name="next-steps"></a><span data-ttu-id="5cf56-714">Next steps</span><span class="sxs-lookup"><span data-stu-id="5cf56-714">Next steps</span></span>

<span data-ttu-id="5cf56-715">Learn more about the Azure Machine Learning Package for Forecasting in these articles:</span><span class="sxs-lookup"><span data-stu-id="5cf56-715">Learn more about the Azure Machine Learning Package for Forecasting in these articles:</span></span>

+ <span data-ttu-id="5cf56-716">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/forecasting).</span><span class="sxs-lookup"><span data-stu-id="5cf56-716">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/forecasting).</span></span>

+ <span data-ttu-id="5cf56-717">Explore the [reference docs](https://aka.ms/aml-packages/forecasting) for this package.</span><span class="sxs-lookup"><span data-stu-id="5cf56-717">Explore the [reference docs](https://aka.ms/aml-packages/forecasting) for this package.</span></span>

+ <span data-ttu-id="5cf56-718">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cf56-718">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span></span>
