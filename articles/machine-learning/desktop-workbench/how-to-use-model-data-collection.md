---
title: Use the model data collection feature in Azure Machine Learning Workbench | Microsoft Docs
description: This article talks about how to use the model data collection feature in Azure Machine Learning Workbench
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
ms.openlocfilehash: 5c1a884ebe6216c4e8099f2ada2182ccff68b63e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868583"
---
# <a name="collect-model-data-by-using-data-collection"></a><span data-ttu-id="d5d59-103">Collect model data by using data collection</span><span class="sxs-lookup"><span data-stu-id="d5d59-103">Collect model data by using data collection</span></span>

<span data-ttu-id="d5d59-104">You can use the model data collection feature in Azure Machine Learning to archive model inputs and predictions from a web service.</span><span class="sxs-lookup"><span data-stu-id="d5d59-104">You can use the model data collection feature in Azure Machine Learning to archive model inputs and predictions from a web service.</span></span>

## <a name="install-the-data-collection-package"></a><span data-ttu-id="d5d59-105">Install the data collection package</span><span class="sxs-lookup"><span data-stu-id="d5d59-105">Install the data collection package</span></span>
<span data-ttu-id="d5d59-106">You can install the data collection library natively on Linux and Windows.</span><span class="sxs-lookup"><span data-stu-id="d5d59-106">You can install the data collection library natively on Linux and Windows.</span></span>

### <a name="windows"></a><span data-ttu-id="d5d59-107">Windows</span><span class="sxs-lookup"><span data-stu-id="d5d59-107">Windows</span></span>
<span data-ttu-id="d5d59-108">On Windows, install the data collector module by using the following command:</span><span class="sxs-lookup"><span data-stu-id="d5d59-108">On Windows, install the data collector module by using the following command:</span></span>

    pip install azureml.datacollector

### <a name="linux"></a><span data-ttu-id="d5d59-109">Linux</span><span class="sxs-lookup"><span data-stu-id="d5d59-109">Linux</span></span>
<span data-ttu-id="d5d59-110">On Linux, install the libxml++ library first.</span><span class="sxs-lookup"><span data-stu-id="d5d59-110">On Linux, install the libxml++ library first.</span></span> <span data-ttu-id="d5d59-111">Run the following command, which must be issued under sudo:</span><span class="sxs-lookup"><span data-stu-id="d5d59-111">Run the following command, which must be issued under sudo:</span></span>

    sudo apt-get install libxml++2.6-2v5

<span data-ttu-id="d5d59-112">Then run the following command:</span><span class="sxs-lookup"><span data-stu-id="d5d59-112">Then run the following command:</span></span>

    pip install azureml.datacollector

## <a name="set-environment-variables"></a><span data-ttu-id="d5d59-113">Set environment variables</span><span class="sxs-lookup"><span data-stu-id="d5d59-113">Set environment variables</span></span>

<span data-ttu-id="d5d59-114">Model data collection depends on two environment variables.</span><span class="sxs-lookup"><span data-stu-id="d5d59-114">Model data collection depends on two environment variables.</span></span> <span data-ttu-id="d5d59-115">AML_MODEL_DC_STORAGE_ENABLED must be set to **true** (all lowercase) and AML_MODEL_DC_STORAGE must be set to the connection string for the Azure Storage account where you want to store the data.</span><span class="sxs-lookup"><span data-stu-id="d5d59-115">AML_MODEL_DC_STORAGE_ENABLED must be set to **true** (all lowercase) and AML_MODEL_DC_STORAGE must be set to the connection string for the Azure Storage account where you want to store the data.</span></span>

<span data-ttu-id="d5d59-116">These environment variables are already set for you when the web service is running on a cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="d5d59-116">These environment variables are already set for you when the web service is running on a cluster in Azure.</span></span> <span data-ttu-id="d5d59-117">When running locally you have to set them yourself.</span><span class="sxs-lookup"><span data-stu-id="d5d59-117">When running locally you have to set them yourself.</span></span> <span data-ttu-id="d5d59-118">If you are using Docker, use the -e parameter of the docker run command to pass environment variables.</span><span class="sxs-lookup"><span data-stu-id="d5d59-118">If you are using Docker, use the -e parameter of the docker run command to pass environment variables.</span></span>

## <a name="collect-data"></a><span data-ttu-id="d5d59-119">Collect data</span><span class="sxs-lookup"><span data-stu-id="d5d59-119">Collect data</span></span>

<span data-ttu-id="d5d59-120">To use model data collection, make the following changes to your scoring file:</span><span class="sxs-lookup"><span data-stu-id="d5d59-120">To use model data collection, make the following changes to your scoring file:</span></span>

1. <span data-ttu-id="d5d59-121">Add the following code at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="d5d59-121">Add the following code at the top of the file:</span></span>
   
    ```python
    from azureml.datacollector import ModelDataCollector
    ```

1. <span data-ttu-id="d5d59-122">Add the following lines of code to the `init()` function:</span><span class="sxs-lookup"><span data-stu-id="d5d59-122">Add the following lines of code to the `init()` function:</span></span>
    
    ```python
    global inputs_dc, prediction_dc
    inputs_dc = ModelDataCollector('model.pkl',identifier="inputs")
    prediction_dc = ModelDataCollector('model.pkl', identifier="prediction")
    ```

1. <span data-ttu-id="d5d59-123">Add the following lines of code to the `run(input_df)` function:</span><span class="sxs-lookup"><span data-stu-id="d5d59-123">Add the following lines of code to the `run(input_df)` function:</span></span>
    
    ```python
    global inputs_dc, prediction_dc
    inputs_dc.collect(input_df)
    prediction_dc.collect(pred)
    ```

    <span data-ttu-id="d5d59-124">Make sure that the variables `input_df` and `pred` (prediction value from `model.predict()`) are initialized before you call the `collect()` function on them.</span><span class="sxs-lookup"><span data-stu-id="d5d59-124">Make sure that the variables `input_df` and `pred` (prediction value from `model.predict()`) are initialized before you call the `collect()` function on them.</span></span>

1. <span data-ttu-id="d5d59-125">Use the `az ml service create realtime` command with the `--collect-model-data true` switch to create a real-time web service.</span><span class="sxs-lookup"><span data-stu-id="d5d59-125">Use the `az ml service create realtime` command with the `--collect-model-data true` switch to create a real-time web service.</span></span> <span data-ttu-id="d5d59-126">This step makes sure that the model data is collected when the service is run.</span><span class="sxs-lookup"><span data-stu-id="d5d59-126">This step makes sure that the model data is collected when the service is run.</span></span>

     ```batch
    c:\temp\myIris> az ml service create realtime -f iris_score.py --model-file model.pkl -s service_schema.json -n irisapp -r python --collect-model-data true 
    ```
    
1. <span data-ttu-id="d5d59-127">To test the data collection, run the `az ml service run realtime` command:</span><span class="sxs-lookup"><span data-stu-id="d5d59-127">To test the data collection, run the `az ml service run realtime` command:</span></span>

    ```
    C:\Temp\myIris> az ml service run realtime -i irisapp -d "ADD YOUR INPUT DATA HERE!!" 
    ``` 
    
## <a name="view-the-collected-data"></a><span data-ttu-id="d5d59-128">View the collected data</span><span class="sxs-lookup"><span data-stu-id="d5d59-128">View the collected data</span></span>
<span data-ttu-id="d5d59-129">To view the collected data in blob storage:</span><span class="sxs-lookup"><span data-stu-id="d5d59-129">To view the collected data in blob storage:</span></span>

1. <span data-ttu-id="d5d59-130">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5d59-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="d5d59-131">Select **All Services**.</span><span class="sxs-lookup"><span data-stu-id="d5d59-131">Select **All Services**.</span></span>
1. <span data-ttu-id="d5d59-132">In the search box, type **Storage accounts** and select the Enter key.</span><span class="sxs-lookup"><span data-stu-id="d5d59-132">In the search box, type **Storage accounts** and select the Enter key.</span></span>
1. <span data-ttu-id="d5d59-133">From the **Storage accounts** search blade, select the **Storage account** resource.</span><span class="sxs-lookup"><span data-stu-id="d5d59-133">From the **Storage accounts** search blade, select the **Storage account** resource.</span></span> <span data-ttu-id="d5d59-134">To determine your storage account, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="d5d59-134">To determine your storage account, use the following steps:</span></span>

    <span data-ttu-id="d5d59-135">a.</span><span class="sxs-lookup"><span data-stu-id="d5d59-135">a.</span></span> <span data-ttu-id="d5d59-136">Go to Azure Machine Learning Workbench, select the project you're working on, and open a command prompt from the **File** menu.</span><span class="sxs-lookup"><span data-stu-id="d5d59-136">Go to Azure Machine Learning Workbench, select the project you're working on, and open a command prompt from the **File** menu.</span></span>
    
    <span data-ttu-id="d5d59-137">b.</span><span class="sxs-lookup"><span data-stu-id="d5d59-137">b.</span></span> <span data-ttu-id="d5d59-138">Enter `az ml env show -v` and check the *storage_account* value.</span><span class="sxs-lookup"><span data-stu-id="d5d59-138">Enter `az ml env show -v` and check the *storage_account* value.</span></span> <span data-ttu-id="d5d59-139">This is the name of your storage account.</span><span class="sxs-lookup"><span data-stu-id="d5d59-139">This is the name of your storage account.</span></span>

1. <span data-ttu-id="d5d59-140">Select **Containers** on the resource blade menu, and then the container called **modeldata**.</span><span class="sxs-lookup"><span data-stu-id="d5d59-140">Select **Containers** on the resource blade menu, and then the container called **modeldata**.</span></span> <span data-ttu-id="d5d59-141">To see data start propagating to the storage account, you might need to wait up to 10 minutes after the first web service request.</span><span class="sxs-lookup"><span data-stu-id="d5d59-141">To see data start propagating to the storage account, you might need to wait up to 10 minutes after the first web service request.</span></span> <span data-ttu-id="d5d59-142">Data flows into blobs with the following container path:</span><span class="sxs-lookup"><span data-stu-id="d5d59-142">Data flows into blobs with the following container path:</span></span>

    `/modeldata/<subscription_id>/<resource_group_name>/<model_management_account_name>/<webservice_name>/<model_id>-<model_name>-<model_version>/<identifier>/<year>/<month>/<day>/data.csv`

<span data-ttu-id="d5d59-143">Data can be consumed from Azure blobs in a variety of ways, through both Microsoft software and open-source tools.</span><span class="sxs-lookup"><span data-stu-id="d5d59-143">Data can be consumed from Azure blobs in a variety of ways, through both Microsoft software and open-source tools.</span></span> <span data-ttu-id="d5d59-144">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="d5d59-144">Here are some examples:</span></span>
- <span data-ttu-id="d5d59-145">Azure Machine Learning Workbench: Open the .csv file in Azure Machine Learning Workbench by adding the .csv file as a data source.</span><span class="sxs-lookup"><span data-stu-id="d5d59-145">Azure Machine Learning Workbench: Open the .csv file in Azure Machine Learning Workbench by adding the .csv file as a data source.</span></span>
- <span data-ttu-id="d5d59-146">Excel: Open the daily .csv files as a spreadsheet.</span><span class="sxs-lookup"><span data-stu-id="d5d59-146">Excel: Open the daily .csv files as a spreadsheet.</span></span>
- <span data-ttu-id="d5d59-147">[Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/): Create charts with data pulled from .csv data in blobs.</span><span class="sxs-lookup"><span data-stu-id="d5d59-147">[Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/): Create charts with data pulled from .csv data in blobs.</span></span>
- <span data-ttu-id="d5d59-148">[Spark](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-overview): Create a data frame with a large portion of .csv data.</span><span class="sxs-lookup"><span data-stu-id="d5d59-148">[Spark](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-overview): Create a data frame with a large portion of .csv data.</span></span>
    ```python
    var df = spark.read.format("com.databricks.spark.csv").option("inferSchema","true").option("header","true").load("wasb://modeldata@<storageaccount>.blob.core.windows.net/<subscription_id>/<resource_group_name>/<model_management_account_name>/<webservice_name>/<model_id>-<model_name>-<model_version>/<identifier>/<year>/<month>/<date>/*")
    ```
- <span data-ttu-id="d5d59-149">[Hive](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-tutorial-get-started): Load .csv data into a Hive table and perform SQL queries directly against the blob.</span><span class="sxs-lookup"><span data-stu-id="d5d59-149">[Hive](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-tutorial-get-started): Load .csv data into a Hive table and perform SQL queries directly against the blob.</span></span>

