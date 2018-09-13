---
title: In-depth guide on how to use the Azure Machine Learning Data Preparations execution API | Microsoft Docs
description: This document provides details on executing previously designed Data Sources and Data Preparations packages
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
ms.openlocfilehash: 9f15f949ba76240da2788c1a01e7086ba3b42fd1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870312"
---
# <a name="execute-data-sources-and-data-preparations-packages-from-python"></a><span data-ttu-id="d3a7f-103">Execute Data Sources and Data Preparations packages from Python</span><span class="sxs-lookup"><span data-stu-id="d3a7f-103">Execute Data Sources and Data Preparations packages from Python</span></span>

<span data-ttu-id="d3a7f-104">To use an Azure Machine Learning Data Sources or Azure Machine Learning Data Preparations package within Python:</span><span class="sxs-lookup"><span data-stu-id="d3a7f-104">To use an Azure Machine Learning Data Sources or Azure Machine Learning Data Preparations package within Python:</span></span>

1. <span data-ttu-id="d3a7f-105">Go to the **Data** tab of your project.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-105">Go to the **Data** tab of your project.</span></span>

2. <span data-ttu-id="d3a7f-106">Right-click the appropriate source.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-106">Right-click the appropriate source.</span></span>

3. <span data-ttu-id="d3a7f-107">Choose **Generate Data Access Code File.**</span><span class="sxs-lookup"><span data-stu-id="d3a7f-107">Choose **Generate Data Access Code File.**</span></span>

<span data-ttu-id="d3a7f-108">This action creates a short Python script that executes the package and returns a dataframe.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-108">This action creates a short Python script that executes the package and returns a dataframe.</span></span>

## <a name="data-sources"></a><span data-ttu-id="d3a7f-109">Data Sources</span><span class="sxs-lookup"><span data-stu-id="d3a7f-109">Data Sources</span></span>

<span data-ttu-id="d3a7f-110">The `azureml.dataprep.datasource` module contains a single function to execute a data source and return a dataframe: `load_datasource(path, secrets=None, spark=None)`.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-110">The `azureml.dataprep.datasource` module contains a single function to execute a data source and return a dataframe: `load_datasource(path, secrets=None, spark=None)`.</span></span>
- <span data-ttu-id="d3a7f-111">`path` is the path to the data source (.dsource file).</span><span class="sxs-lookup"><span data-stu-id="d3a7f-111">`path` is the path to the data source (.dsource file).</span></span>
- <span data-ttu-id="d3a7f-112">`secrets` is an optional dictionary that maps keys to secrets.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-112">`secrets` is an optional dictionary that maps keys to secrets.</span></span>
- <span data-ttu-id="d3a7f-113">`spark` is an optional bool that specifies whether to return a Spark dataframe or a Pandas dataframe.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-113">`spark` is an optional bool that specifies whether to return a Spark dataframe or a Pandas dataframe.</span></span> <span data-ttu-id="d3a7f-114">By default, Azure Machine Learning Workbench determines which kind of dataframe to return at runtime based on context.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-114">By default, Azure Machine Learning Workbench determines which kind of dataframe to return at runtime based on context.</span></span>

## <a name="data-preparations-packages"></a><span data-ttu-id="d3a7f-115">Data Preparations packages</span><span class="sxs-lookup"><span data-stu-id="d3a7f-115">Data Preparations packages</span></span>

<span data-ttu-id="d3a7f-116">The `azureml.dataprep.package` module contains three functions that execute a data flow from a Data Preparations package.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-116">The `azureml.dataprep.package` module contains three functions that execute a data flow from a Data Preparations package.</span></span>

### <a name="execution-functions"></a><span data-ttu-id="d3a7f-117">Execution functions</span><span class="sxs-lookup"><span data-stu-id="d3a7f-117">Execution functions</span></span>

- <span data-ttu-id="d3a7f-118">`submit(package_path, dataflow_idx=0, secrets=None, spark=None)` submits the specified data flow for execution but does not return a dataframe.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-118">`submit(package_path, dataflow_idx=0, secrets=None, spark=None)` submits the specified data flow for execution but does not return a dataframe.</span></span>
- <span data-ttu-id="d3a7f-119">`run(package_path, dataflow_idx=0, secrets=None, spark=None)` runs the specified data flow and returns the results as a dataframe.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-119">`run(package_path, dataflow_idx=0, secrets=None, spark=None)` runs the specified data flow and returns the results as a dataframe.</span></span>
- <span data-ttu-id="d3a7f-120">`run_on_data(user_config, package_path, dataflow_idx=0, secrets=None, spark=None)` runs the specified data flow based on an in-memory data source and returns the results as a dataframe.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-120">`run_on_data(user_config, package_path, dataflow_idx=0, secrets=None, spark=None)` runs the specified data flow based on an in-memory data source and returns the results as a dataframe.</span></span> <span data-ttu-id="d3a7f-121">The `user_config` argument is a dictionary that maps the absolute path of a data source (.dsource file) to an in-memory data source represented as a list of lists.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-121">The `user_config` argument is a dictionary that maps the absolute path of a data source (.dsource file) to an in-memory data source represented as a list of lists.</span></span>

### <a name="common-arguments"></a><span data-ttu-id="d3a7f-122">Common arguments</span><span class="sxs-lookup"><span data-stu-id="d3a7f-122">Common arguments</span></span>

- <span data-ttu-id="d3a7f-123">`package_path` is the path to the Data Preparations package (.dprep file).</span><span class="sxs-lookup"><span data-stu-id="d3a7f-123">`package_path` is the path to the Data Preparations package (.dprep file).</span></span>
- <span data-ttu-id="d3a7f-124">`dataflow_idx` is the zero-based index of which data flow in the package to execute.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-124">`dataflow_idx` is the zero-based index of which data flow in the package to execute.</span></span> <span data-ttu-id="d3a7f-125">If the specified data flow references other data flows or data sources, they are executed as well.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-125">If the specified data flow references other data flows or data sources, they are executed as well.</span></span>
- <span data-ttu-id="d3a7f-126">`secrets` is an optional dictionary that maps keys to secrets.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-126">`secrets` is an optional dictionary that maps keys to secrets.</span></span>
- <span data-ttu-id="d3a7f-127">`spark` is an optional bool that specifies whether to return a Spark dataframe or a Pandas dataframe.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-127">`spark` is an optional bool that specifies whether to return a Spark dataframe or a Pandas dataframe.</span></span> <span data-ttu-id="d3a7f-128">By default, Workbench determines which kind of dataframe to return at runtime based on context.</span><span class="sxs-lookup"><span data-stu-id="d3a7f-128">By default, Workbench determines which kind of dataframe to return at runtime based on context.</span></span>
