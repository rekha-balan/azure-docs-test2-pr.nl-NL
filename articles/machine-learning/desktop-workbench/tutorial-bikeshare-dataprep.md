---
title: Bike-share tutorial - Advanced data preparation with Azure Machine Learning Workbench
description: In this tutorial, you perform an end-to-end data preparation task by using Azure Machine Learning Workbench
services: machine-learning
author: ranvijaykumar
ms.author: ranku
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: tutorial
ms.date: 09/21/2017
ms.openlocfilehash: 2a50350b9ba49d82a20b92804ffb92ec6906186d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856482"
---
# <a name="tutorial-use-azure-machine-learning-workbench-for-advanced-data-preparation-bike-share-data"></a><span data-ttu-id="9c676-103">Tutorial: Use Azure Machine Learning Workbench for advanced data preparation (Bike share data)</span><span class="sxs-lookup"><span data-stu-id="9c676-103">Tutorial: Use Azure Machine Learning Workbench for advanced data preparation (Bike share data)</span></span>
<span data-ttu-id="9c676-104">Azure Machine Learning (preview) is an integrated, end-to-end data science and advanced analytics solution for professional data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="9c676-104">Azure Machine Learning (preview) is an integrated, end-to-end data science and advanced analytics solution for professional data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span></span>

<span data-ttu-id="9c676-105">In this tutorial, you use Machine Learning (preview) to learn how to:</span><span class="sxs-lookup"><span data-stu-id="9c676-105">In this tutorial, you use Machine Learning (preview) to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9c676-106">Prepare data interactively with the Machine Learning data preparation tool.</span><span class="sxs-lookup"><span data-stu-id="9c676-106">Prepare data interactively with the Machine Learning data preparation tool.</span></span>
> * <span data-ttu-id="9c676-107">Import, transform, and create a test dataset.</span><span class="sxs-lookup"><span data-stu-id="9c676-107">Import, transform, and create a test dataset.</span></span>
> * <span data-ttu-id="9c676-108">Generate a data preparation package.</span><span class="sxs-lookup"><span data-stu-id="9c676-108">Generate a data preparation package.</span></span>
> * <span data-ttu-id="9c676-109">Run the data preparation package by using Python.</span><span class="sxs-lookup"><span data-stu-id="9c676-109">Run the data preparation package by using Python.</span></span>
> * <span data-ttu-id="9c676-110">Generate a training dataset by reusing the data preparation package for additional input files.</span><span class="sxs-lookup"><span data-stu-id="9c676-110">Generate a training dataset by reusing the data preparation package for additional input files.</span></span>
> * <span data-ttu-id="9c676-111">Execute scripts in a local Azure CLI window.</span><span class="sxs-lookup"><span data-stu-id="9c676-111">Execute scripts in a local Azure CLI window.</span></span>
> * <span data-ttu-id="9c676-112">Execute scripts in a cloud Azure HDInsight environment.</span><span class="sxs-lookup"><span data-stu-id="9c676-112">Execute scripts in a cloud Azure HDInsight environment.</span></span>

<span data-ttu-id="9c676-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9c676-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c676-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c676-114">Prerequisites</span></span>

* <span data-ttu-id="9c676-115">A local installation of Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="9c676-115">A local installation of Azure Machine Learning Workbench.</span></span> <span data-ttu-id="9c676-116">For more information, follow the [installation quickstart](../service/quickstart-installation.md).</span><span class="sxs-lookup"><span data-stu-id="9c676-116">For more information, follow the [installation quickstart](../service/quickstart-installation.md).</span></span>
* <span data-ttu-id="9c676-117">If you don't have the Azure CLI installed, follow the instructions to [install the latest Azure CLI version](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="9c676-117">If you don't have the Azure CLI installed, follow the instructions to [install the latest Azure CLI version](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>
* <span data-ttu-id="9c676-118">An [HDInsights Spark cluster](how-to-create-dsvm-hdi.md#create-an-apache-spark-for-azure-hdinsight-cluster-in-azure-portal) created in Azure.</span><span class="sxs-lookup"><span data-stu-id="9c676-118">An [HDInsights Spark cluster](how-to-create-dsvm-hdi.md#create-an-apache-spark-for-azure-hdinsight-cluster-in-azure-portal) created in Azure.</span></span>
* <span data-ttu-id="9c676-119">An Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="9c676-119">An Azure storage account.</span></span>
* <span data-ttu-id="9c676-120">Familiarity with how to create a new project in Workbench.</span><span class="sxs-lookup"><span data-stu-id="9c676-120">Familiarity with how to create a new project in Workbench.</span></span>
* <span data-ttu-id="9c676-121">Although it's not required, it's helpful to have [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) installed so that you can upload, download, and view the blobs in your storage account.</span><span class="sxs-lookup"><span data-stu-id="9c676-121">Although it's not required, it's helpful to have [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) installed so that you can upload, download, and view the blobs in your storage account.</span></span>

## <a name="data-acquisition"></a><span data-ttu-id="9c676-122">Data acquisition</span><span class="sxs-lookup"><span data-stu-id="9c676-122">Data acquisition</span></span>
<span data-ttu-id="9c676-123">This tutorial uses the [Boston hubway dataset](https://s3.amazonaws.com/hubway-data/index.html) and Boston weather data from [NOAA](http://www.noaa.gov/).</span><span class="sxs-lookup"><span data-stu-id="9c676-123">This tutorial uses the [Boston hubway dataset](https://s3.amazonaws.com/hubway-data/index.html) and Boston weather data from [NOAA](http://www.noaa.gov/).</span></span>

1. <span data-ttu-id="9c676-124">Download the data files from the following links to your local development environment:</span><span class="sxs-lookup"><span data-stu-id="9c676-124">Download the data files from the following links to your local development environment:</span></span>

   * [<span data-ttu-id="9c676-125">Boston weather data</span><span class="sxs-lookup"><span data-stu-id="9c676-125">Boston weather data</span></span>](https://azuremluxcdnprod001.blob.core.windows.net/docs/azureml/bikeshare/BostonWeather.csv)

   * <span data-ttu-id="9c676-126">Hubway trip data from the hubway website:</span><span class="sxs-lookup"><span data-stu-id="9c676-126">Hubway trip data from the hubway website:</span></span>

      - [<span data-ttu-id="9c676-127">201501-hubway-tripdata.zip</span><span class="sxs-lookup"><span data-stu-id="9c676-127">201501-hubway-tripdata.zip</span></span>](https://s3.amazonaws.com/hubway-data/201501-hubway-tripdata.zip)
      - [<span data-ttu-id="9c676-128">201504-hubway-tripdata.zip</span><span class="sxs-lookup"><span data-stu-id="9c676-128">201504-hubway-tripdata.zip</span></span>](https://s3.amazonaws.com/hubway-data/201504-hubway-tripdata.zip)
      - [<span data-ttu-id="9c676-129">201510-hubway-tripdata.zip</span><span class="sxs-lookup"><span data-stu-id="9c676-129">201510-hubway-tripdata.zip</span></span>](https://s3.amazonaws.com/hubway-data/201510-hubway-tripdata.zip)
      - [<span data-ttu-id="9c676-130">201601-hubway-tripdata.zip</span><span class="sxs-lookup"><span data-stu-id="9c676-130">201601-hubway-tripdata.zip</span></span>](https://s3.amazonaws.com/hubway-data/201601-hubway-tripdata.zip)
      - [<span data-ttu-id="9c676-131">201604-hubway-tripdata.zip</span><span class="sxs-lookup"><span data-stu-id="9c676-131">201604-hubway-tripdata.zip</span></span>](https://s3.amazonaws.com/hubway-data/201604-hubway-tripdata.zip)
      - [<span data-ttu-id="9c676-132">201610-hubway-tripdata.zip</span><span class="sxs-lookup"><span data-stu-id="9c676-132">201610-hubway-tripdata.zip</span></span>](https://s3.amazonaws.com/hubway-data/201610-hubway-tripdata.zip)
      - [<span data-ttu-id="9c676-133">201701-hubway-tripdata.zip</span><span class="sxs-lookup"><span data-stu-id="9c676-133">201701-hubway-tripdata.zip</span></span>](https://s3.amazonaws.com/hubway-data/201701-hubway-tripdata.zip)

1. <span data-ttu-id="9c676-134">Unzip each .zip file after download.</span><span class="sxs-lookup"><span data-stu-id="9c676-134">Unzip each .zip file after download.</span></span>

## <a name="upload-data-files-to-azure-blob-storage"></a><span data-ttu-id="9c676-135">Upload data files to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="9c676-135">Upload data files to Azure Blob storage</span></span>
<span data-ttu-id="9c676-136">You can use Azure Blob storage to host your data files.</span><span class="sxs-lookup"><span data-stu-id="9c676-136">You can use Azure Blob storage to host your data files.</span></span>

1. <span data-ttu-id="9c676-137">Use the same storage account that is used for the HDInsight cluster you use.</span><span class="sxs-lookup"><span data-stu-id="9c676-137">Use the same storage account that is used for the HDInsight cluster you use.</span></span>

    ![HDInsight cluster storage account](media/tutorial-bikeshare-dataprep/hdinsightstorageaccount.png)

1. <span data-ttu-id="9c676-139">Create a new container named **data-files** to store the **BikeShare** data files.</span><span class="sxs-lookup"><span data-stu-id="9c676-139">Create a new container named **data-files** to store the **BikeShare** data files.</span></span>

1. <span data-ttu-id="9c676-140">Upload the data files.</span><span class="sxs-lookup"><span data-stu-id="9c676-140">Upload the data files.</span></span> <span data-ttu-id="9c676-141">Upload `BostonWeather.csv` to a folder named `weather`.</span><span class="sxs-lookup"><span data-stu-id="9c676-141">Upload `BostonWeather.csv` to a folder named `weather`.</span></span> <span data-ttu-id="9c676-142">Upload the trip data files to a folder named `tripdata`.</span><span class="sxs-lookup"><span data-stu-id="9c676-142">Upload the trip data files to a folder named `tripdata`.</span></span>

    ![Upload data files](media/tutorial-bikeshare-dataprep/azurestoragedatafile.png)

> [!TIP]
> <span data-ttu-id="9c676-144">You also can use Storage Explorer to upload blobs.</span><span class="sxs-lookup"><span data-stu-id="9c676-144">You also can use Storage Explorer to upload blobs.</span></span> <span data-ttu-id="9c676-145">Use this tool when you want to view the contents of any files generated in the tutorial, too.</span><span class="sxs-lookup"><span data-stu-id="9c676-145">Use this tool when you want to view the contents of any files generated in the tutorial, too.</span></span>

## <a name="learn-about-the-datasets"></a><span data-ttu-id="9c676-146">Learn about the datasets</span><span class="sxs-lookup"><span data-stu-id="9c676-146">Learn about the datasets</span></span>
1. <span data-ttu-id="9c676-147">The __Boston weather__ file contains the following weather-related fields, reported on an hourly basis:</span><span class="sxs-lookup"><span data-stu-id="9c676-147">The __Boston weather__ file contains the following weather-related fields, reported on an hourly basis:</span></span>

   * <span data-ttu-id="9c676-148">**DATE**</span><span class="sxs-lookup"><span data-stu-id="9c676-148">**DATE**</span></span>

   * <span data-ttu-id="9c676-149">**REPORTTPYE**</span><span class="sxs-lookup"><span data-stu-id="9c676-149">**REPORTTPYE**</span></span>

   * <span data-ttu-id="9c676-150">**HOURLYDRYBULBTEMPF**</span><span class="sxs-lookup"><span data-stu-id="9c676-150">**HOURLYDRYBULBTEMPF**</span></span>

   * <span data-ttu-id="9c676-151">**HOURLYRelativeHumidity**</span><span class="sxs-lookup"><span data-stu-id="9c676-151">**HOURLYRelativeHumidity**</span></span>

   * <span data-ttu-id="9c676-152">**HOURLYWindSpeed**</span><span class="sxs-lookup"><span data-stu-id="9c676-152">**HOURLYWindSpeed**</span></span>

1. <span data-ttu-id="9c676-153">The __hubway__ data is organized into files by year and month.</span><span class="sxs-lookup"><span data-stu-id="9c676-153">The __hubway__ data is organized into files by year and month.</span></span> <span data-ttu-id="9c676-154">For example, the file named `201501-hubway-tripdata.zip` contains a .csv file that contains data for January 2015.</span><span class="sxs-lookup"><span data-stu-id="9c676-154">For example, the file named `201501-hubway-tripdata.zip` contains a .csv file that contains data for January 2015.</span></span> <span data-ttu-id="9c676-155">The data contains the following fields, with each row representing a bike trip:</span><span class="sxs-lookup"><span data-stu-id="9c676-155">The data contains the following fields, with each row representing a bike trip:</span></span>

   * <span data-ttu-id="9c676-156">**Trip Duration (in seconds)**</span><span class="sxs-lookup"><span data-stu-id="9c676-156">**Trip Duration (in seconds)**</span></span>

   * <span data-ttu-id="9c676-157">**Start Time and Date**</span><span class="sxs-lookup"><span data-stu-id="9c676-157">**Start Time and Date**</span></span>

   * <span data-ttu-id="9c676-158">**Stop Time and Date**</span><span class="sxs-lookup"><span data-stu-id="9c676-158">**Stop Time and Date**</span></span>

   * <span data-ttu-id="9c676-159">**Start Station Name & ID**</span><span class="sxs-lookup"><span data-stu-id="9c676-159">**Start Station Name & ID**</span></span>

   * <span data-ttu-id="9c676-160">**End Station Name & ID**</span><span class="sxs-lookup"><span data-stu-id="9c676-160">**End Station Name & ID**</span></span>

   * <span data-ttu-id="9c676-161">**Bike ID**</span><span class="sxs-lookup"><span data-stu-id="9c676-161">**Bike ID**</span></span>

   * <span data-ttu-id="9c676-162">**User Type (Casual = 24-Hour or 72-Hour Pass user; Member = Annual or Monthly Member)**</span><span class="sxs-lookup"><span data-stu-id="9c676-162">**User Type (Casual = 24-Hour or 72-Hour Pass user; Member = Annual or Monthly Member)**</span></span>

   * <span data-ttu-id="9c676-163">**ZIP Code (if user is a member)**</span><span class="sxs-lookup"><span data-stu-id="9c676-163">**ZIP Code (if user is a member)**</span></span>

   * <span data-ttu-id="9c676-164">**Gender (self-reported by member)**</span><span class="sxs-lookup"><span data-stu-id="9c676-164">**Gender (self-reported by member)**</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="9c676-165">Create a new project</span><span class="sxs-lookup"><span data-stu-id="9c676-165">Create a new project</span></span>
1. <span data-ttu-id="9c676-166">Start **Machine Learning Workbench** from your Start menu or launcher.</span><span class="sxs-lookup"><span data-stu-id="9c676-166">Start **Machine Learning Workbench** from your Start menu or launcher.</span></span>

1. <span data-ttu-id="9c676-167">Create a new Machine Learning project.</span><span class="sxs-lookup"><span data-stu-id="9c676-167">Create a new Machine Learning project.</span></span> <span data-ttu-id="9c676-168">Select the **+** button on the **Projects** page, or select **File** > **New**.</span><span class="sxs-lookup"><span data-stu-id="9c676-168">Select the **+** button on the **Projects** page, or select **File** > **New**.</span></span>

   * <span data-ttu-id="9c676-169">Use the **Bike Share** template.</span><span class="sxs-lookup"><span data-stu-id="9c676-169">Use the **Bike Share** template.</span></span>

   * <span data-ttu-id="9c676-170">Name your project **BikeShare**.</span><span class="sxs-lookup"><span data-stu-id="9c676-170">Name your project **BikeShare**.</span></span> 

## <a id="newdatasource"></a><span data-ttu-id="9c676-171">Create a new data source</span><span class="sxs-lookup"><span data-stu-id="9c676-171">Create a new data source</span></span>

1. <span data-ttu-id="9c676-172">Create a new data source.</span><span class="sxs-lookup"><span data-stu-id="9c676-172">Create a new data source.</span></span> <span data-ttu-id="9c676-173">Select the **Data** button (cylinder icon) on the left toolbar to display the **Data** view.</span><span class="sxs-lookup"><span data-stu-id="9c676-173">Select the **Data** button (cylinder icon) on the left toolbar to display the **Data** view.</span></span>

   ![Data view tab](media/tutorial-bikeshare-dataprep/navigatetodatatab.png)

1. <span data-ttu-id="9c676-175">Add a data source.</span><span class="sxs-lookup"><span data-stu-id="9c676-175">Add a data source.</span></span> <span data-ttu-id="9c676-176">Select the **+** icon, and then select **Add Data Source**.</span><span class="sxs-lookup"><span data-stu-id="9c676-176">Select the **+** icon, and then select **Add Data Source**.</span></span>

   ![Add Data Source option](media/tutorial-bikeshare-dataprep/newdatasource.png)

## <a name="add-weather-data"></a><span data-ttu-id="9c676-178">Add weather data</span><span class="sxs-lookup"><span data-stu-id="9c676-178">Add weather data</span></span>

1. <span data-ttu-id="9c676-179">**Data Store**: Select the data store that contains the data.</span><span class="sxs-lookup"><span data-stu-id="9c676-179">**Data Store**: Select the data store that contains the data.</span></span> <span data-ttu-id="9c676-180">Because you're using files, select **File(s)/Directory**.</span><span class="sxs-lookup"><span data-stu-id="9c676-180">Because you're using files, select **File(s)/Directory**.</span></span> <span data-ttu-id="9c676-181">Select **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="9c676-181">Select **Next** to continue.</span></span>

   ![File(s)/Directory entry](media/tutorial-bikeshare-dataprep/datasources.png)

1. <span data-ttu-id="9c676-183">**File Selection**: Add the weather data.</span><span class="sxs-lookup"><span data-stu-id="9c676-183">**File Selection**: Add the weather data.</span></span> <span data-ttu-id="9c676-184">Browse and select the `BostonWeather.csv` file that you uploaded to Blob Storage earlier.</span><span class="sxs-lookup"><span data-stu-id="9c676-184">Browse and select the `BostonWeather.csv` file that you uploaded to Blob Storage earlier.</span></span> <span data-ttu-id="9c676-185">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9c676-185">Select **Next**.</span></span>

   ![File selection with BostonWeather.csv selected](media/tutorial-bikeshare-dataprep/azureblobpickweatherdatafile.png)

1. <span data-ttu-id="9c676-187">**File Details**: Verify the file schema that is detected.</span><span class="sxs-lookup"><span data-stu-id="9c676-187">**File Details**: Verify the file schema that is detected.</span></span> <span data-ttu-id="9c676-188">Machine Learning Workbench analyzes the data in the file and infers the schema to use.</span><span class="sxs-lookup"><span data-stu-id="9c676-188">Machine Learning Workbench analyzes the data in the file and infers the schema to use.</span></span>

   ![Verify file details](media/tutorial-bikeshare-dataprep/fileparameters.png)

   > [!IMPORTANT]
   > <span data-ttu-id="9c676-190">Workbench might not detect the correct schema in some cases.</span><span class="sxs-lookup"><span data-stu-id="9c676-190">Workbench might not detect the correct schema in some cases.</span></span> <span data-ttu-id="9c676-191">Always verify that the parameters are correct for your data set.</span><span class="sxs-lookup"><span data-stu-id="9c676-191">Always verify that the parameters are correct for your data set.</span></span> <span data-ttu-id="9c676-192">For the weather data, verify that they are set to the following values:</span><span class="sxs-lookup"><span data-stu-id="9c676-192">For the weather data, verify that they are set to the following values:</span></span>
   >
   > * <span data-ttu-id="9c676-193">__File Type__: Delimited File (csv, tsv, txt, etc.)</span><span class="sxs-lookup"><span data-stu-id="9c676-193">__File Type__: Delimited File (csv, tsv, txt, etc.)</span></span>
   > * <span data-ttu-id="9c676-194">__Separator__: Comma [,]</span><span class="sxs-lookup"><span data-stu-id="9c676-194">__Separator__: Comma [,]</span></span>
   > * <span data-ttu-id="9c676-195">__Comment Line Character__: No value is set.</span><span class="sxs-lookup"><span data-stu-id="9c676-195">__Comment Line Character__: No value is set.</span></span>
   > * <span data-ttu-id="9c676-196">__Skip Lines Mode__: Don't skip</span><span class="sxs-lookup"><span data-stu-id="9c676-196">__Skip Lines Mode__: Don't skip</span></span>
   > * <span data-ttu-id="9c676-197">__File Encoding__: utf-8</span><span class="sxs-lookup"><span data-stu-id="9c676-197">__File Encoding__: utf-8</span></span>
   > * <span data-ttu-id="9c676-198">__Promote Headers Mode__: Use Headers From First File</span><span class="sxs-lookup"><span data-stu-id="9c676-198">__Promote Headers Mode__: Use Headers From First File</span></span>

   <span data-ttu-id="9c676-199">The preview of the data should display the following columns:</span><span class="sxs-lookup"><span data-stu-id="9c676-199">The preview of the data should display the following columns:</span></span>

   * <span data-ttu-id="9c676-200">**Path**</span><span class="sxs-lookup"><span data-stu-id="9c676-200">**Path**</span></span>

   * <span data-ttu-id="9c676-201">**DATE**</span><span class="sxs-lookup"><span data-stu-id="9c676-201">**DATE**</span></span>

   * <span data-ttu-id="9c676-202">**REPORTTYPE**</span><span class="sxs-lookup"><span data-stu-id="9c676-202">**REPORTTYPE**</span></span>

   * <span data-ttu-id="9c676-203">**HOURLYDRYBULBTEMPF**</span><span class="sxs-lookup"><span data-stu-id="9c676-203">**HOURLYDRYBULBTEMPF**</span></span>
   
   * <span data-ttu-id="9c676-204">**HOURLYRelativeHumidity**</span><span class="sxs-lookup"><span data-stu-id="9c676-204">**HOURLYRelativeHumidity**</span></span>

   * <span data-ttu-id="9c676-205">**HOURLYWindSpeed**</span><span class="sxs-lookup"><span data-stu-id="9c676-205">**HOURLYWindSpeed**</span></span>

   <span data-ttu-id="9c676-206">To continue, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9c676-206">To continue, select **Next**.</span></span>

1. <span data-ttu-id="9c676-207">**Data Types**: Review the data types that are detected automatically.</span><span class="sxs-lookup"><span data-stu-id="9c676-207">**Data Types**: Review the data types that are detected automatically.</span></span> <span data-ttu-id="9c676-208">Machine Learning Workbench analyzes the data in the file and infers the data types to use.</span><span class="sxs-lookup"><span data-stu-id="9c676-208">Machine Learning Workbench analyzes the data in the file and infers the data types to use.</span></span>

   <span data-ttu-id="9c676-209">a.</span><span class="sxs-lookup"><span data-stu-id="9c676-209">a.</span></span> <span data-ttu-id="9c676-210">For this data, change **DATA TYPE** for all the columns to **String**.</span><span class="sxs-lookup"><span data-stu-id="9c676-210">For this data, change **DATA TYPE** for all the columns to **String**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9c676-211">String is used to highlight the capabilities of Workbench later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9c676-211">String is used to highlight the capabilities of Workbench later in this tutorial.</span></span> 

   ![Review data types](media/tutorial-bikeshare-dataprep/datatypedetection.png)

   <span data-ttu-id="9c676-213">b.</span><span class="sxs-lookup"><span data-stu-id="9c676-213">b.</span></span> <span data-ttu-id="9c676-214">To continue, select __Next__.</span><span class="sxs-lookup"><span data-stu-id="9c676-214">To continue, select __Next__.</span></span> 

1. <span data-ttu-id="9c676-215">**Sampling**: To create a sampling scheme, select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="9c676-215">**Sampling**: To create a sampling scheme, select **Edit**.</span></span> <span data-ttu-id="9c676-216">Select the new __Top 10000__ row that is added, and then select __Edit__.</span><span class="sxs-lookup"><span data-stu-id="9c676-216">Select the new __Top 10000__ row that is added, and then select __Edit__.</span></span> <span data-ttu-id="9c676-217">Set __Sample Strategy__ to **Full File**, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="9c676-217">Set __Sample Strategy__ to **Full File**, and then select **Apply**.</span></span>

   ![Add a new sampling strategy](media/tutorial-bikeshare-dataprep/weatherdatasamplingfullfile.png)

   <span data-ttu-id="9c676-219">To use the __Full File__ strategy, select the __Full File__ entry, and then select __Set as Active__.</span><span class="sxs-lookup"><span data-stu-id="9c676-219">To use the __Full File__ strategy, select the __Full File__ entry, and then select __Set as Active__.</span></span> <span data-ttu-id="9c676-220">A star appears next to __Full File__ to indicate that it's the active strategy.</span><span class="sxs-lookup"><span data-stu-id="9c676-220">A star appears next to __Full File__ to indicate that it's the active strategy.</span></span>

   ![Full File set as active strategy](media/tutorial-bikeshare-dataprep/fullfileactive.png)

   <span data-ttu-id="9c676-222">To continue, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9c676-222">To continue, select **Next**.</span></span>

1. <span data-ttu-id="9c676-223">**Path Column**: Use the __Path Column__ section to include the full file path as a column in the imported data.</span><span class="sxs-lookup"><span data-stu-id="9c676-223">**Path Column**: Use the __Path Column__ section to include the full file path as a column in the imported data.</span></span> <span data-ttu-id="9c676-224">Select __Do Not Include Path Column__.</span><span class="sxs-lookup"><span data-stu-id="9c676-224">Select __Do Not Include Path Column__.</span></span>

   > [!TIP]
   > <span data-ttu-id="9c676-225">Including the path as a column is useful if you're importing a folder of many files with different file names.</span><span class="sxs-lookup"><span data-stu-id="9c676-225">Including the path as a column is useful if you're importing a folder of many files with different file names.</span></span> <span data-ttu-id="9c676-226">It's also useful if the file names contain information that you want to extract later.</span><span class="sxs-lookup"><span data-stu-id="9c676-226">It's also useful if the file names contain information that you want to extract later.</span></span>

   ![Path Column set to do not include](media/tutorial-bikeshare-dataprep/pathcolumn.png)

1. <span data-ttu-id="9c676-228">**Finish**: To finish creating the data source, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="9c676-228">**Finish**: To finish creating the data source, select **Finish**.</span></span>

    <span data-ttu-id="9c676-229">A new data source tab named __BostonWeather__ opens.</span><span class="sxs-lookup"><span data-stu-id="9c676-229">A new data source tab named __BostonWeather__ opens.</span></span> <span data-ttu-id="9c676-230">A sample of the data is displayed in a grid view.</span><span class="sxs-lookup"><span data-stu-id="9c676-230">A sample of the data is displayed in a grid view.</span></span> <span data-ttu-id="9c676-231">The sample is based on the active sampling scheme specified previously.</span><span class="sxs-lookup"><span data-stu-id="9c676-231">The sample is based on the active sampling scheme specified previously.</span></span>

    <span data-ttu-id="9c676-232">Notice that the **Steps** pane on the right side of the screen displays the individual actions taken while creating this data source.</span><span class="sxs-lookup"><span data-stu-id="9c676-232">Notice that the **Steps** pane on the right side of the screen displays the individual actions taken while creating this data source.</span></span>

   ![Display data source, sample, and steps](media/tutorial-bikeshare-dataprep/weatherdataloaded.png)

### <a name="view-data-source-metrics"></a><span data-ttu-id="9c676-234">View data source metrics</span><span class="sxs-lookup"><span data-stu-id="9c676-234">View data source metrics</span></span>

<span data-ttu-id="9c676-235">Select __Metrics__ at the upper left of the tab's grid view.</span><span class="sxs-lookup"><span data-stu-id="9c676-235">Select __Metrics__ at the upper left of the tab's grid view.</span></span> <span data-ttu-id="9c676-236">This view displays the distribution and other aggregated statistics of the sampled data.</span><span class="sxs-lookup"><span data-stu-id="9c676-236">This view displays the distribution and other aggregated statistics of the sampled data.</span></span>

![Metrics display](media/tutorial-bikeshare-dataprep/weathermetrics.png)

> [!NOTE]
> <span data-ttu-id="9c676-238">To configure the visibility of the statistics, use the **Choose Metric** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="9c676-238">To configure the visibility of the statistics, use the **Choose Metric** drop-down list.</span></span> <span data-ttu-id="9c676-239">Select and clear metrics there to change the grid view.</span><span class="sxs-lookup"><span data-stu-id="9c676-239">Select and clear metrics there to change the grid view.</span></span>

<span data-ttu-id="9c676-240">To return to the __Data__ view, select __Data__ in the upper left of the page.</span><span class="sxs-lookup"><span data-stu-id="9c676-240">To return to the __Data__ view, select __Data__ in the upper left of the page.</span></span>

## <a name="add-a-data-source-to-the-data-preparation-package"></a><span data-ttu-id="9c676-241">Add a data source to the data preparation package</span><span class="sxs-lookup"><span data-stu-id="9c676-241">Add a data source to the data preparation package</span></span>

1. <span data-ttu-id="9c676-242">Select __Prepare__ to begin preparing the data.</span><span class="sxs-lookup"><span data-stu-id="9c676-242">Select __Prepare__ to begin preparing the data.</span></span> 

1. <span data-ttu-id="9c676-243">When prompted, enter a name for the data preparation package, such as **BikeShare Data Prep**.</span><span class="sxs-lookup"><span data-stu-id="9c676-243">When prompted, enter a name for the data preparation package, such as **BikeShare Data Prep**.</span></span> 

1. <span data-ttu-id="9c676-244">Select __OK__ to continue.</span><span class="sxs-lookup"><span data-stu-id="9c676-244">Select __OK__ to continue.</span></span>

   ![Prepare dialog box](media/tutorial-bikeshare-dataprep/dataprepdialog.png)

1. <span data-ttu-id="9c676-246">A new package named **BikeShare Data Prep** appears under the __Data Preparation__ section of the __Data__ tab.</span><span class="sxs-lookup"><span data-stu-id="9c676-246">A new package named **BikeShare Data Prep** appears under the __Data Preparation__ section of the __Data__ tab.</span></span> 

   <span data-ttu-id="9c676-247">To display the package, select this entry.</span><span class="sxs-lookup"><span data-stu-id="9c676-247">To display the package, select this entry.</span></span> 

1. <span data-ttu-id="9c676-248">Select the **>>** button to expand __Dataflows__ and display the dataflows contained in the package.</span><span class="sxs-lookup"><span data-stu-id="9c676-248">Select the **>>** button to expand __Dataflows__ and display the dataflows contained in the package.</span></span> <span data-ttu-id="9c676-249">In this example, __BostonWeather__ is the only dataflow.</span><span class="sxs-lookup"><span data-stu-id="9c676-249">In this example, __BostonWeather__ is the only dataflow.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9c676-250">A package can contain multiple dataflows.</span><span class="sxs-lookup"><span data-stu-id="9c676-250">A package can contain multiple dataflows.</span></span>

   ![Dataflows in the package](media/tutorial-bikeshare-dataprep/weatherdataloadedingrid.png)

## <a name="filter-data-by-value"></a><span data-ttu-id="9c676-252">Filter data by value</span><span class="sxs-lookup"><span data-stu-id="9c676-252">Filter data by value</span></span>
1. <span data-ttu-id="9c676-253">To filter data, right-click a cell with a certain value, and select __Filter__.</span><span class="sxs-lookup"><span data-stu-id="9c676-253">To filter data, right-click a cell with a certain value, and select __Filter__.</span></span> <span data-ttu-id="9c676-254">Then select the type of filter.</span><span class="sxs-lookup"><span data-stu-id="9c676-254">Then select the type of filter.</span></span>

1. <span data-ttu-id="9c676-255">For this tutorial, select a cell that contains the value `FM-15`.</span><span class="sxs-lookup"><span data-stu-id="9c676-255">For this tutorial, select a cell that contains the value `FM-15`.</span></span> <span data-ttu-id="9c676-256">Then set the filter to **equals**.</span><span class="sxs-lookup"><span data-stu-id="9c676-256">Then set the filter to **equals**.</span></span>  <span data-ttu-id="9c676-257">Now the data is filtered to only return rows where the __REPORTTYPE__ is `FM-15`.</span><span class="sxs-lookup"><span data-stu-id="9c676-257">Now the data is filtered to only return rows where the __REPORTTYPE__ is `FM-15`.</span></span>

   ![Filter dialog box](media/tutorial-bikeshare-dataprep/weatherfilterinfm15.png)

   > [!NOTE]
   > <span data-ttu-id="9c676-259">FM-15 is a type of Meteorological Terminal Aviation Routine (METAR) weather report.</span><span class="sxs-lookup"><span data-stu-id="9c676-259">FM-15 is a type of Meteorological Terminal Aviation Routine (METAR) weather report.</span></span> <span data-ttu-id="9c676-260">The FM-15 reports are empirically observed to be the most complete, with little missing data.</span><span class="sxs-lookup"><span data-stu-id="9c676-260">The FM-15 reports are empirically observed to be the most complete, with little missing data.</span></span>

## <a name="remove-a-column"></a><span data-ttu-id="9c676-261">Remove a column</span><span class="sxs-lookup"><span data-stu-id="9c676-261">Remove a column</span></span>

<span data-ttu-id="9c676-262">You no longer need the __REPORTTYPE__ column.</span><span class="sxs-lookup"><span data-stu-id="9c676-262">You no longer need the __REPORTTYPE__ column.</span></span> <span data-ttu-id="9c676-263">Right-click the column header, and select **Remove Column**.</span><span class="sxs-lookup"><span data-stu-id="9c676-263">Right-click the column header, and select **Remove Column**.</span></span>

   ![Remove Column option](media/tutorial-bikeshare-dataprep/weatherremovereporttype.png)

## <a name="change-datatypes-and-remove-errors"></a><span data-ttu-id="9c676-265">Change datatypes and remove errors</span><span class="sxs-lookup"><span data-stu-id="9c676-265">Change datatypes and remove errors</span></span>
1. <span data-ttu-id="9c676-266">Select Ctrl (Command ⌘ on Mac) while you select column headers to select multiple columns at the same time.</span><span class="sxs-lookup"><span data-stu-id="9c676-266">Select Ctrl (Command ⌘ on Mac) while you select column headers to select multiple columns at the same time.</span></span> <span data-ttu-id="9c676-267">Use this technique to select the following column headers:</span><span class="sxs-lookup"><span data-stu-id="9c676-267">Use this technique to select the following column headers:</span></span>

   * <span data-ttu-id="9c676-268">**HOURLYDRYBULBTEMPF**</span><span class="sxs-lookup"><span data-stu-id="9c676-268">**HOURLYDRYBULBTEMPF**</span></span>

   * <span data-ttu-id="9c676-269">**HOURLYRelativeHumidity**</span><span class="sxs-lookup"><span data-stu-id="9c676-269">**HOURLYRelativeHumidity**</span></span>

   * <span data-ttu-id="9c676-270">**HOURLYWindSpeed**</span><span class="sxs-lookup"><span data-stu-id="9c676-270">**HOURLYWindSpeed**</span></span>

1. <span data-ttu-id="9c676-271">Right-click one of the selected column headers, and select **Convert Field Type to Numeric**.</span><span class="sxs-lookup"><span data-stu-id="9c676-271">Right-click one of the selected column headers, and select **Convert Field Type to Numeric**.</span></span> <span data-ttu-id="9c676-272">This option converts the data type for the columns to numeric.</span><span class="sxs-lookup"><span data-stu-id="9c676-272">This option converts the data type for the columns to numeric.</span></span>

   ![Convert multiple columns to numeric](media/tutorial-bikeshare-dataprep/weatherconverttonumeric.png)

1. <span data-ttu-id="9c676-274">Filter out the error values.</span><span class="sxs-lookup"><span data-stu-id="9c676-274">Filter out the error values.</span></span> <span data-ttu-id="9c676-275">Some columns have data type conversion problems.</span><span class="sxs-lookup"><span data-stu-id="9c676-275">Some columns have data type conversion problems.</span></span> <span data-ttu-id="9c676-276">This problem is indicated by the red color in the __Data Quality Bar__ for the column.</span><span class="sxs-lookup"><span data-stu-id="9c676-276">This problem is indicated by the red color in the __Data Quality Bar__ for the column.</span></span>

   <span data-ttu-id="9c676-277">To remove the rows that have errors, right-click the **HOURLYDRYBULBTEMPF** column heading.</span><span class="sxs-lookup"><span data-stu-id="9c676-277">To remove the rows that have errors, right-click the **HOURLYDRYBULBTEMPF** column heading.</span></span> <span data-ttu-id="9c676-278">Select **Filter Column**.</span><span class="sxs-lookup"><span data-stu-id="9c676-278">Select **Filter Column**.</span></span> <span data-ttu-id="9c676-279">Use the default **I Want To** as **Keep Rows**.</span><span class="sxs-lookup"><span data-stu-id="9c676-279">Use the default **I Want To** as **Keep Rows**.</span></span> <span data-ttu-id="9c676-280">Change the **Conditions** drop-down list to select **is not error**.</span><span class="sxs-lookup"><span data-stu-id="9c676-280">Change the **Conditions** drop-down list to select **is not error**.</span></span> <span data-ttu-id="9c676-281">Select **OK** to apply the filter.</span><span class="sxs-lookup"><span data-stu-id="9c676-281">Select **OK** to apply the filter.</span></span>

   ![Filter error values](media/tutorial-bikeshare-dataprep/filtererrorvalues.png)

1. <span data-ttu-id="9c676-283">To eliminate the remaining error rows in the other columns, repeat this filter process for the **HOURLYRelativeHumidity** and **HOURLYWindSpeed** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-283">To eliminate the remaining error rows in the other columns, repeat this filter process for the **HOURLYRelativeHumidity** and **HOURLYWindSpeed** columns.</span></span>

## <a name="use-by-example-transformations"></a><span data-ttu-id="9c676-284">Use by example transformations</span><span class="sxs-lookup"><span data-stu-id="9c676-284">Use by example transformations</span></span>

<span data-ttu-id="9c676-285">To use the data in a prediction for two-hour time blocks, you must compute the average weather conditions for two-hour periods.</span><span class="sxs-lookup"><span data-stu-id="9c676-285">To use the data in a prediction for two-hour time blocks, you must compute the average weather conditions for two-hour periods.</span></span> <span data-ttu-id="9c676-286">Use the following actions:</span><span class="sxs-lookup"><span data-stu-id="9c676-286">Use the following actions:</span></span>

* <span data-ttu-id="9c676-287">Split the **DATE** column into separate **Date** and **Time** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-287">Split the **DATE** column into separate **Date** and **Time** columns.</span></span> <span data-ttu-id="9c676-288">See the following section for the detailed steps.</span><span class="sxs-lookup"><span data-stu-id="9c676-288">See the following section for the detailed steps.</span></span>

* <span data-ttu-id="9c676-289">Derive an **Hour_Range** column from the **Time** column.</span><span class="sxs-lookup"><span data-stu-id="9c676-289">Derive an **Hour_Range** column from the **Time** column.</span></span> <span data-ttu-id="9c676-290">See the following section for the detailed steps.</span><span class="sxs-lookup"><span data-stu-id="9c676-290">See the following section for the detailed steps.</span></span>

* <span data-ttu-id="9c676-291">Derive a **Date\_Hour\_Range** column from the **DATE** and **Hour_Range** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-291">Derive a **Date\_Hour\_Range** column from the **DATE** and **Hour_Range** columns.</span></span> <span data-ttu-id="9c676-292">See the following section for the detailed steps.</span><span class="sxs-lookup"><span data-stu-id="9c676-292">See the following section for the detailed steps.</span></span>

### <a name="split-column-by-example"></a><span data-ttu-id="9c676-293">Split column by example</span><span class="sxs-lookup"><span data-stu-id="9c676-293">Split column by example</span></span>

1. <span data-ttu-id="9c676-294">Split the **DATE** column into separate **Date** and **Time** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-294">Split the **DATE** column into separate **Date** and **Time** columns.</span></span> <span data-ttu-id="9c676-295">Right-click the **DATE** column header, and select **Split Column by Example**.</span><span class="sxs-lookup"><span data-stu-id="9c676-295">Right-click the **DATE** column header, and select **Split Column by Example**.</span></span>

   ![Split Column by Example entry](media/tutorial-bikeshare-dataprep/weathersplitcolumnbyexample.png)

1. <span data-ttu-id="9c676-297">Machine Learning Workbench automatically identifies a meaningful delimiter and creates two columns by splitting the data into date and time values.</span><span class="sxs-lookup"><span data-stu-id="9c676-297">Machine Learning Workbench automatically identifies a meaningful delimiter and creates two columns by splitting the data into date and time values.</span></span> 

1. <span data-ttu-id="9c676-298">Select __OK__ to accept the split operation results.</span><span class="sxs-lookup"><span data-stu-id="9c676-298">Select __OK__ to accept the split operation results.</span></span>

   ![Split columns DATE_1 and DATE_2](media/tutorial-bikeshare-dataprep/weatherdatesplitted.png)

### <a name="derive-column-by-example"></a><span data-ttu-id="9c676-300">Derive column by example</span><span class="sxs-lookup"><span data-stu-id="9c676-300">Derive column by example</span></span>

1. <span data-ttu-id="9c676-301">To derive a two-hour range, right-click the __DATE\_2__ column header, and select **Derive Column by Example**.</span><span class="sxs-lookup"><span data-stu-id="9c676-301">To derive a two-hour range, right-click the __DATE\_2__ column header, and select **Derive Column by Example**.</span></span>

   ![Derive Column by Example entry](media/tutorial-bikeshare-dataprep/weatherdate2range.png)

   <span data-ttu-id="9c676-303">A new empty column is added with null values.</span><span class="sxs-lookup"><span data-stu-id="9c676-303">A new empty column is added with null values.</span></span>

1. <span data-ttu-id="9c676-304">Select in the first empty cell in the new column.</span><span class="sxs-lookup"><span data-stu-id="9c676-304">Select in the first empty cell in the new column.</span></span> <span data-ttu-id="9c676-305">To provide an example of the time range desired, type **12AM-2AM** in the new column, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="9c676-305">To provide an example of the time range desired, type **12AM-2AM** in the new column, and then select Enter.</span></span>

   ![New column with value of 12AM-2AM](media/tutorial-bikeshare-dataprep/weathertimerangeexample.png)

   > [!NOTE]
   > <span data-ttu-id="9c676-307">Machine Learning Workbench synthesizes a program based on the examples provided by you and applies the same program on remaining rows.</span><span class="sxs-lookup"><span data-stu-id="9c676-307">Machine Learning Workbench synthesizes a program based on the examples provided by you and applies the same program on remaining rows.</span></span> <span data-ttu-id="9c676-308">All other rows are automatically populated based on the example you provided.</span><span class="sxs-lookup"><span data-stu-id="9c676-308">All other rows are automatically populated based on the example you provided.</span></span> <span data-ttu-id="9c676-309">Workbench also analyzes your data and tries to identify edge cases.</span><span class="sxs-lookup"><span data-stu-id="9c676-309">Workbench also analyzes your data and tries to identify edge cases.</span></span> 

   > [!IMPORTANT]
   > <span data-ttu-id="9c676-310">Identification of edge cases might not work on Mac in the current version of Workbench.</span><span class="sxs-lookup"><span data-stu-id="9c676-310">Identification of edge cases might not work on Mac in the current version of Workbench.</span></span> <span data-ttu-id="9c676-311">Skip the following step 3 and step 4 on Mac.</span><span class="sxs-lookup"><span data-stu-id="9c676-311">Skip the following step 3 and step 4 on Mac.</span></span> <span data-ttu-id="9c676-312">Instead, select __OK__ after all the rows are populated with the derived values.</span><span class="sxs-lookup"><span data-stu-id="9c676-312">Instead, select __OK__ after all the rows are populated with the derived values.</span></span>
   
1. <span data-ttu-id="9c676-313">The text **Analyzing Data** above the grid indicates that Workbench is trying to detect edge cases.</span><span class="sxs-lookup"><span data-stu-id="9c676-313">The text **Analyzing Data** above the grid indicates that Workbench is trying to detect edge cases.</span></span> <span data-ttu-id="9c676-314">When finished, the status changes to **Review next suggested row** or **No suggestions**.</span><span class="sxs-lookup"><span data-stu-id="9c676-314">When finished, the status changes to **Review next suggested row** or **No suggestions**.</span></span> <span data-ttu-id="9c676-315">In this example, **Review next suggested row** is returned.</span><span class="sxs-lookup"><span data-stu-id="9c676-315">In this example, **Review next suggested row** is returned.</span></span>

1. <span data-ttu-id="9c676-316">To review the suggested changes, select **Review next suggested row**.</span><span class="sxs-lookup"><span data-stu-id="9c676-316">To review the suggested changes, select **Review next suggested row**.</span></span> <span data-ttu-id="9c676-317">The cell that you should review and correct, if needed, is highlighted on the display.</span><span class="sxs-lookup"><span data-stu-id="9c676-317">The cell that you should review and correct, if needed, is highlighted on the display.</span></span>

   ![Review next suggested row](media/tutorial-bikeshare-dataprep/weatherreviewnextsuggested.png)

    <span data-ttu-id="9c676-319">Select __OK__ to accept the transformation.</span><span class="sxs-lookup"><span data-stu-id="9c676-319">Select __OK__ to accept the transformation.</span></span>
 
1. <span data-ttu-id="9c676-320">You are returned to the grid view of data for __BostonWeather__.</span><span class="sxs-lookup"><span data-stu-id="9c676-320">You are returned to the grid view of data for __BostonWeather__.</span></span> <span data-ttu-id="9c676-321">The grid now contains the three columns added previously.</span><span class="sxs-lookup"><span data-stu-id="9c676-321">The grid now contains the three columns added previously.</span></span>

   ![Grid view with added rows](media/tutorial-bikeshare-dataprep/timerangecomputed.png)

   > [!TIP]
   > <span data-ttu-id="9c676-323">All the changes you made are preserved in the **Steps** pane.</span><span class="sxs-lookup"><span data-stu-id="9c676-323">All the changes you made are preserved in the **Steps** pane.</span></span> <span data-ttu-id="9c676-324">Go to the step that you created in the **Steps** pane, select the down arrow, and select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="9c676-324">Go to the step that you created in the **Steps** pane, select the down arrow, and select **Edit**.</span></span> <span data-ttu-id="9c676-325">The advanced window for **Derive Column by Example** is displayed.</span><span class="sxs-lookup"><span data-stu-id="9c676-325">The advanced window for **Derive Column by Example** is displayed.</span></span> <span data-ttu-id="9c676-326">All your examples are preserved here.</span><span class="sxs-lookup"><span data-stu-id="9c676-326">All your examples are preserved here.</span></span> <span data-ttu-id="9c676-327">You also can add examples manually by double-clicking on a row in the following grid.</span><span class="sxs-lookup"><span data-stu-id="9c676-327">You also can add examples manually by double-clicking on a row in the following grid.</span></span> <span data-ttu-id="9c676-328">Select **Cancel** to return to the main grid without applying changes.</span><span class="sxs-lookup"><span data-stu-id="9c676-328">Select **Cancel** to return to the main grid without applying changes.</span></span> <span data-ttu-id="9c676-329">You also can access this view by selecting **Advanced mode** while you perform a **Derive Column by Example** transform.</span><span class="sxs-lookup"><span data-stu-id="9c676-329">You also can access this view by selecting **Advanced mode** while you perform a **Derive Column by Example** transform.</span></span>

1. <span data-ttu-id="9c676-330">To rename the column, double-click the column header, and type **Hour Range**.</span><span class="sxs-lookup"><span data-stu-id="9c676-330">To rename the column, double-click the column header, and type **Hour Range**.</span></span> <span data-ttu-id="9c676-331">Select Enter to save the change.</span><span class="sxs-lookup"><span data-stu-id="9c676-331">Select Enter to save the change.</span></span>

   ![Rename the column](media/tutorial-bikeshare-dataprep/weatherhourrangecolumnrename.png)

1. <span data-ttu-id="9c676-333">To derive the date and hour range, multi-select the **Date\_1** and **Hour Range** columns, right-click, and then select **Derive Column by Example**.</span><span class="sxs-lookup"><span data-stu-id="9c676-333">To derive the date and hour range, multi-select the **Date\_1** and **Hour Range** columns, right-click, and then select **Derive Column by Example**.</span></span>

   ![Derive Column by Example](media/tutorial-bikeshare-dataprep/weatherderivedatehourrange.png)

   <span data-ttu-id="9c676-335">Type **Jan 01, 2015 12AM-2AM** as the example against the first row, and select Enter.</span><span class="sxs-lookup"><span data-stu-id="9c676-335">Type **Jan 01, 2015 12AM-2AM** as the example against the first row, and select Enter.</span></span>

   <span data-ttu-id="9c676-336">Workbench determines the transformation based on the example you provide.</span><span class="sxs-lookup"><span data-stu-id="9c676-336">Workbench determines the transformation based on the example you provide.</span></span> <span data-ttu-id="9c676-337">In this example, the result is that the date format is changed and concatenated with the two-hour window.</span><span class="sxs-lookup"><span data-stu-id="9c676-337">In this example, the result is that the date format is changed and concatenated with the two-hour window.</span></span>

   ![The example Jan 01, 2015 12AM-2AM](media/tutorial-bikeshare-dataprep/wetherdatehourrangeexample.png)

   > [!IMPORTANT]
   > <span data-ttu-id="9c676-339">On a Mac, take the following step instead of step 8:</span><span class="sxs-lookup"><span data-stu-id="9c676-339">On a Mac, take the following step instead of step 8:</span></span>
   >
   > * <span data-ttu-id="9c676-340">Go to the first cell that contains **Feb 01, 2015 12AM-2AM**.</span><span class="sxs-lookup"><span data-stu-id="9c676-340">Go to the first cell that contains **Feb 01, 2015 12AM-2AM**.</span></span> <span data-ttu-id="9c676-341">It should be row 15.</span><span class="sxs-lookup"><span data-stu-id="9c676-341">It should be row 15.</span></span> <span data-ttu-id="9c676-342">Correct the value to **Jan 02, 2015 12AM-2AM**, and select Enter.</span><span class="sxs-lookup"><span data-stu-id="9c676-342">Correct the value to **Jan 02, 2015 12AM-2AM**, and select Enter.</span></span> 
   

1. <span data-ttu-id="9c676-343">Wait for the status to change from **Analyzing Data** to **Review next suggested row**.</span><span class="sxs-lookup"><span data-stu-id="9c676-343">Wait for the status to change from **Analyzing Data** to **Review next suggested row**.</span></span> <span data-ttu-id="9c676-344">This change might take several seconds.</span><span class="sxs-lookup"><span data-stu-id="9c676-344">This change might take several seconds.</span></span> <span data-ttu-id="9c676-345">Select the status link to go to the suggested row.</span><span class="sxs-lookup"><span data-stu-id="9c676-345">Select the status link to go to the suggested row.</span></span> 

   ![Suggested row to review](media/tutorial-bikeshare-dataprep/wetherdatehourrangedisambiguate.png)

   <span data-ttu-id="9c676-347">The row has a null value because the source date value can be for either dd/mm/yyyy or mm/dd/yyyy.</span><span class="sxs-lookup"><span data-stu-id="9c676-347">The row has a null value because the source date value can be for either dd/mm/yyyy or mm/dd/yyyy.</span></span> <span data-ttu-id="9c676-348">Type the correct value of **Jan 13, 2015 2AM-4AM**, and select Enter.</span><span class="sxs-lookup"><span data-stu-id="9c676-348">Type the correct value of **Jan 13, 2015 2AM-4AM**, and select Enter.</span></span> <span data-ttu-id="9c676-349">Workbench uses the two examples to improve the derivation for the remaining rows.</span><span class="sxs-lookup"><span data-stu-id="9c676-349">Workbench uses the two examples to improve the derivation for the remaining rows.</span></span>

   ![Correctly formatted data](media/tutorial-bikeshare-dataprep/wetherdatehourrangedisambiguated.png)

1. <span data-ttu-id="9c676-351">Select **OK** to accept the transform.</span><span class="sxs-lookup"><span data-stu-id="9c676-351">Select **OK** to accept the transform.</span></span>

   ![Completed transformation grid](media/tutorial-bikeshare-dataprep/weatherdatehourrangecomputed.png)

   > [!TIP]
   > <span data-ttu-id="9c676-353">To use the **Advanced mode** of **Derive Column by Example** for this step.</span><span class="sxs-lookup"><span data-stu-id="9c676-353">To use the **Advanced mode** of **Derive Column by Example** for this step.</span></span> <span data-ttu-id="9c676-354">select the down arrow in the **Steps** pane.</span><span class="sxs-lookup"><span data-stu-id="9c676-354">select the down arrow in the **Steps** pane.</span></span> <span data-ttu-id="9c676-355">In the data grid, there are check boxes next to the **DATE\_1** and **Hour Range** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-355">In the data grid, there are check boxes next to the **DATE\_1** and **Hour Range** columns.</span></span> <span data-ttu-id="9c676-356">Clear the check box next to the **Hour Range** column to see how the output changes.</span><span class="sxs-lookup"><span data-stu-id="9c676-356">Clear the check box next to the **Hour Range** column to see how the output changes.</span></span> <span data-ttu-id="9c676-357">In the absence of the **Hour Range** column as input, **12AM-2AM** is treated as a constant and is appended to the derived values.</span><span class="sxs-lookup"><span data-stu-id="9c676-357">In the absence of the **Hour Range** column as input, **12AM-2AM** is treated as a constant and is appended to the derived values.</span></span> <span data-ttu-id="9c676-358">Select **Cancel** to return to the main grid without applying your changes.</span><span class="sxs-lookup"><span data-stu-id="9c676-358">Select **Cancel** to return to the main grid without applying your changes.</span></span>
   <span data-ttu-id="9c676-359">![Advanced mode](media/tutorial-bikeshare-dataprep/derivedcolumnadvancededitdeselectcolumn.png)</span><span class="sxs-lookup"><span data-stu-id="9c676-359">![Advanced mode](media/tutorial-bikeshare-dataprep/derivedcolumnadvancededitdeselectcolumn.png)</span></span>

1. <span data-ttu-id="9c676-360">To rename the column, double-click the header.</span><span class="sxs-lookup"><span data-stu-id="9c676-360">To rename the column, double-click the header.</span></span> <span data-ttu-id="9c676-361">Change the name to **Date Hour Range**, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="9c676-361">Change the name to **Date Hour Range**, and then select Enter.</span></span>

1. <span data-ttu-id="9c676-362">Multi-select the **DATE**, **DATE\_1**, **DATE\_2**, and **Hour Range** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-362">Multi-select the **DATE**, **DATE\_1**, **DATE\_2**, and **Hour Range** columns.</span></span> <span data-ttu-id="9c676-363">Right-click, and then select **Remove column**.</span><span class="sxs-lookup"><span data-stu-id="9c676-363">Right-click, and then select **Remove column**.</span></span>

## <a name="summarize-data-mean"></a><span data-ttu-id="9c676-364">Summarize data (mean)</span><span class="sxs-lookup"><span data-stu-id="9c676-364">Summarize data (mean)</span></span>

<span data-ttu-id="9c676-365">The next step is to summarize the weather conditions by taking the mean of the values, grouped by hour range.</span><span class="sxs-lookup"><span data-stu-id="9c676-365">The next step is to summarize the weather conditions by taking the mean of the values, grouped by hour range.</span></span>

1. <span data-ttu-id="9c676-366">Select the **Date Hour Range** column, and then on the **Transforms** menu, select **Summarize**.</span><span class="sxs-lookup"><span data-stu-id="9c676-366">Select the **Date Hour Range** column, and then on the **Transforms** menu, select **Summarize**.</span></span>

    ![Transforms menu](media/tutorial-bikeshare-dataprep/weathersummarizemenu.png)

1. <span data-ttu-id="9c676-368">To summarize the data, drag columns from the grid at the bottom of the page to the left and right panes at the top.</span><span class="sxs-lookup"><span data-stu-id="9c676-368">To summarize the data, drag columns from the grid at the bottom of the page to the left and right panes at the top.</span></span> <span data-ttu-id="9c676-369">The left pane contains the text **Drag columns here to group data**.</span><span class="sxs-lookup"><span data-stu-id="9c676-369">The left pane contains the text **Drag columns here to group data**.</span></span> <span data-ttu-id="9c676-370">The right pane contains the text **Drag columns here to summarize data**.</span><span class="sxs-lookup"><span data-stu-id="9c676-370">The right pane contains the text **Drag columns here to summarize data**.</span></span> 

    <span data-ttu-id="9c676-371">a.</span><span class="sxs-lookup"><span data-stu-id="9c676-371">a.</span></span> <span data-ttu-id="9c676-372">Drag the **Date Hour Range** column from the grid at the bottom to the left pane.</span><span class="sxs-lookup"><span data-stu-id="9c676-372">Drag the **Date Hour Range** column from the grid at the bottom to the left pane.</span></span> <span data-ttu-id="9c676-373">Drag **HOURLYDRYBULBTEMPF**, **HOURLYRelativeHumidity**, and **HOURLYWindSpeed** to the right pane.</span><span class="sxs-lookup"><span data-stu-id="9c676-373">Drag **HOURLYDRYBULBTEMPF**, **HOURLYRelativeHumidity**, and **HOURLYWindSpeed** to the right pane.</span></span> 

    <span data-ttu-id="9c676-374">b.</span><span class="sxs-lookup"><span data-stu-id="9c676-374">b.</span></span> <span data-ttu-id="9c676-375">In the right pane, select **Mean** as the **Aggregate** measure for each column.</span><span class="sxs-lookup"><span data-stu-id="9c676-375">In the right pane, select **Mean** as the **Aggregate** measure for each column.</span></span> <span data-ttu-id="9c676-376">Select **OK** to finish the summarization.</span><span class="sxs-lookup"><span data-stu-id="9c676-376">Select **OK** to finish the summarization.</span></span>

    ![Summarized data screen](media/tutorial-bikeshare-dataprep/weathersummarize.png)

## <a name="transform-dataflow-by-using-script"></a><span data-ttu-id="9c676-378">Transform dataflow by using script</span><span class="sxs-lookup"><span data-stu-id="9c676-378">Transform dataflow by using script</span></span>

<span data-ttu-id="9c676-379">Changing the data in the numeric columns to a range of 0 to 1 allows some models to converge quickly.</span><span class="sxs-lookup"><span data-stu-id="9c676-379">Changing the data in the numeric columns to a range of 0 to 1 allows some models to converge quickly.</span></span> <span data-ttu-id="9c676-380">Currently, there is no built-in transformation to generically do this transformation.</span><span class="sxs-lookup"><span data-stu-id="9c676-380">Currently, there is no built-in transformation to generically do this transformation.</span></span> <span data-ttu-id="9c676-381">Use a Python script to perform this operation.</span><span class="sxs-lookup"><span data-stu-id="9c676-381">Use a Python script to perform this operation.</span></span>

1. <span data-ttu-id="9c676-382">On the **Transform** menu, select **Transform Dataflow (Script)**.</span><span class="sxs-lookup"><span data-stu-id="9c676-382">On the **Transform** menu, select **Transform Dataflow (Script)**.</span></span>

1. <span data-ttu-id="9c676-383">Enter the following code in the text box that appears.</span><span class="sxs-lookup"><span data-stu-id="9c676-383">Enter the following code in the text box that appears.</span></span> <span data-ttu-id="9c676-384">If you used the column names, the code should work without modification.</span><span class="sxs-lookup"><span data-stu-id="9c676-384">If you used the column names, the code should work without modification.</span></span> <span data-ttu-id="9c676-385">You are writing a simple min-max normalization logic in Python.</span><span class="sxs-lookup"><span data-stu-id="9c676-385">You are writing a simple min-max normalization logic in Python.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9c676-386">The script expects the column names used previously in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9c676-386">The script expects the column names used previously in this tutorial.</span></span> <span data-ttu-id="9c676-387">If you have different column names, you must change the names in the script.</span><span class="sxs-lookup"><span data-stu-id="9c676-387">If you have different column names, you must change the names in the script.</span></span>

   ```python
   maxVal = max(df["HOURLYDRYBULBTEMPF_Mean"])
   minVal = min(df["HOURLYDRYBULBTEMPF_Mean"])
   df["HOURLYDRYBULBTEMPF_Mean"] = (df["HOURLYDRYBULBTEMPF_Mean"]-minVal)/(maxVal-minVal)
   df.rename(columns={"HOURLYDRYBULBTEMPF_Mean":"N_DryBulbTemp"},inplace=True)

   maxVal = max(df["HOURLYRelativeHumidity_Mean"])
   minVal = min(df["HOURLYRelativeHumidity_Mean"])
   df["HOURLYRelativeHumidity_Mean"] = (df["HOURLYRelativeHumidity_Mean"]-minVal)/(maxVal-minVal)
   df.rename(columns={"HOURLYRelativeHumidity_Mean":"N_RelativeHumidity"},inplace=True)

   maxVal = max(df["HOURLYWindSpeed_Mean"])
   minVal = min(df["HOURLYWindSpeed_Mean"])
   df["HOURLYWindSpeed_Mean"] = (df["HOURLYWindSpeed_Mean"]-minVal)/(maxVal-minVal)
   df.rename(columns={"HOURLYWindSpeed_Mean":"N_WindSpeed"},inplace=True)

   df
   ```

    > [!TIP]
    > <span data-ttu-id="9c676-388">The Python script must return `df` at the end.</span><span class="sxs-lookup"><span data-stu-id="9c676-388">The Python script must return `df` at the end.</span></span> <span data-ttu-id="9c676-389">This value is used to populate the grid.</span><span class="sxs-lookup"><span data-stu-id="9c676-389">This value is used to populate the grid.</span></span>
    
   ![Transform Dataflow (Script) dialog box](media/tutorial-bikeshare-dataprep/transformdataflowscript.png)

1. <span data-ttu-id="9c676-391">Select __OK__ to use the script.</span><span class="sxs-lookup"><span data-stu-id="9c676-391">Select __OK__ to use the script.</span></span> <span data-ttu-id="9c676-392">The numeric columns in the grid now contain values in the range of 0 to 1.</span><span class="sxs-lookup"><span data-stu-id="9c676-392">The numeric columns in the grid now contain values in the range of 0 to 1.</span></span>

    ![Grid that contains values between 0 and 1](media/tutorial-bikeshare-dataprep/datagridwithdecimals.png)

<span data-ttu-id="9c676-394">You have finished preparing the weather data.</span><span class="sxs-lookup"><span data-stu-id="9c676-394">You have finished preparing the weather data.</span></span> <span data-ttu-id="9c676-395">Next, prepare the trip data.</span><span class="sxs-lookup"><span data-stu-id="9c676-395">Next, prepare the trip data.</span></span>

## <a name="load-trip-data"></a><span data-ttu-id="9c676-396">Load trip data</span><span class="sxs-lookup"><span data-stu-id="9c676-396">Load trip data</span></span>

1. <span data-ttu-id="9c676-397">To import the `201701-hubway-tripdata.csv` file, use the steps in the [Create a new data source](#newdatasource) section.</span><span class="sxs-lookup"><span data-stu-id="9c676-397">To import the `201701-hubway-tripdata.csv` file, use the steps in the [Create a new data source](#newdatasource) section.</span></span> <span data-ttu-id="9c676-398">Use the following options during the import process:</span><span class="sxs-lookup"><span data-stu-id="9c676-398">Use the following options during the import process:</span></span>

    * <span data-ttu-id="9c676-399">__File Selection__: Select **Azure Blob** when you browse to select the file.</span><span class="sxs-lookup"><span data-stu-id="9c676-399">__File Selection__: Select **Azure Blob** when you browse to select the file.</span></span>

    * <span data-ttu-id="9c676-400">__Sampling Scheme__: Select **Full File** sampling scheme, and make the sample active.</span><span class="sxs-lookup"><span data-stu-id="9c676-400">__Sampling Scheme__: Select **Full File** sampling scheme, and make the sample active.</span></span>

    * <span data-ttu-id="9c676-401">__Data Type__: Accept the defaults.</span><span class="sxs-lookup"><span data-stu-id="9c676-401">__Data Type__: Accept the defaults.</span></span>

1. <span data-ttu-id="9c676-402">After you import the data, select __Prepare__ to begin preparing the data.</span><span class="sxs-lookup"><span data-stu-id="9c676-402">After you import the data, select __Prepare__ to begin preparing the data.</span></span> <span data-ttu-id="9c676-403">Select the existing **BikeShare Data Prep.dprep** package, and then select __OK__.</span><span class="sxs-lookup"><span data-stu-id="9c676-403">Select the existing **BikeShare Data Prep.dprep** package, and then select __OK__.</span></span>

    <span data-ttu-id="9c676-404">This process adds a **Dataflow** to the existing **Data Preparation** file rather than creating a new one.</span><span class="sxs-lookup"><span data-stu-id="9c676-404">This process adds a **Dataflow** to the existing **Data Preparation** file rather than creating a new one.</span></span>

    ![Select the existing package](media/tutorial-bikeshare-dataprep/addjandatatodprep.png)

1. <span data-ttu-id="9c676-406">After the grid has loaded, expand __DATAFLOWS__.</span><span class="sxs-lookup"><span data-stu-id="9c676-406">After the grid has loaded, expand __DATAFLOWS__.</span></span> <span data-ttu-id="9c676-407">There are now two dataflows: **BostonWeather** and **201701-hubway-tripdata**.</span><span class="sxs-lookup"><span data-stu-id="9c676-407">There are now two dataflows: **BostonWeather** and **201701-hubway-tripdata**.</span></span> <span data-ttu-id="9c676-408">Select the **201701-hubway-tripdata** entry.</span><span class="sxs-lookup"><span data-stu-id="9c676-408">Select the **201701-hubway-tripdata** entry.</span></span>

    ![201701-hubway-tripdata entry](media/tutorial-bikeshare-dataprep/twodfsindprep.png)

## <a name="use-the-map-inspector"></a><span data-ttu-id="9c676-410">Use the map inspector</span><span class="sxs-lookup"><span data-stu-id="9c676-410">Use the map inspector</span></span>

<span data-ttu-id="9c676-411">For data preparation, useful visualizations called inspectors are available for string, numeric, and geographical data.</span><span class="sxs-lookup"><span data-stu-id="9c676-411">For data preparation, useful visualizations called inspectors are available for string, numeric, and geographical data.</span></span> <span data-ttu-id="9c676-412">They help you to understand the data better and identify outliers.</span><span class="sxs-lookup"><span data-stu-id="9c676-412">They help you to understand the data better and identify outliers.</span></span> <span data-ttu-id="9c676-413">Follow these steps to use the map inspector.</span><span class="sxs-lookup"><span data-stu-id="9c676-413">Follow these steps to use the map inspector.</span></span>

1. <span data-ttu-id="9c676-414">Multi-select the **start station latitude** and **start station longitude** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-414">Multi-select the **start station latitude** and **start station longitude** columns.</span></span> <span data-ttu-id="9c676-415">Right-click one of the columns, and then select **Map**.</span><span class="sxs-lookup"><span data-stu-id="9c676-415">Right-click one of the columns, and then select **Map**.</span></span>

    > [!TIP]
    > <span data-ttu-id="9c676-416">To enable multi-select, hold down the Ctrl key (Command ⌘ on Mac), and select the header for each column.</span><span class="sxs-lookup"><span data-stu-id="9c676-416">To enable multi-select, hold down the Ctrl key (Command ⌘ on Mac), and select the header for each column.</span></span>

    ![Map visualization](media/tutorial-bikeshare-dataprep/launchMapInspector.png)

1. <span data-ttu-id="9c676-418">To maximize the map visualization, select the **Maximize** icon.</span><span class="sxs-lookup"><span data-stu-id="9c676-418">To maximize the map visualization, select the **Maximize** icon.</span></span> <span data-ttu-id="9c676-419">To fit the map to the window, select the **E** icon on the upper-left side of the visualization.</span><span class="sxs-lookup"><span data-stu-id="9c676-419">To fit the map to the window, select the **E** icon on the upper-left side of the visualization.</span></span>

    ![Maximized image](media/tutorial-bikeshare-dataprep/maximizedmap.png)

1. <span data-ttu-id="9c676-421">Select the **Minimize** button to return to the grid view.</span><span class="sxs-lookup"><span data-stu-id="9c676-421">Select the **Minimize** button to return to the grid view.</span></span>

## <a name="use-the-column-statistics-inspector"></a><span data-ttu-id="9c676-422">Use the column statistics inspector</span><span class="sxs-lookup"><span data-stu-id="9c676-422">Use the column statistics inspector</span></span>

<span data-ttu-id="9c676-423">To use the column statistics inspector, right-click the __tripduration__ column, and select __Column Statistics__.</span><span class="sxs-lookup"><span data-stu-id="9c676-423">To use the column statistics inspector, right-click the __tripduration__ column, and select __Column Statistics__.</span></span>

![Column statistics entry](media/tutorial-bikeshare-dataprep/tripdurationcolstats.png)

<span data-ttu-id="9c676-425">This process adds a new visualization titled __tripduration Statistics__ in the __INSPECTORS__ pane.</span><span class="sxs-lookup"><span data-stu-id="9c676-425">This process adds a new visualization titled __tripduration Statistics__ in the __INSPECTORS__ pane.</span></span>

![The tripduration Statistics inspector](media/tutorial-bikeshare-dataprep/tripdurationcolstatsinwell.png)

> [!IMPORTANT]
> <span data-ttu-id="9c676-427">The maximum value of the trip duration is 961,814 minutes, which is about two years.</span><span class="sxs-lookup"><span data-stu-id="9c676-427">The maximum value of the trip duration is 961,814 minutes, which is about two years.</span></span> <span data-ttu-id="9c676-428">It seems there are some outliers in the dataset.</span><span class="sxs-lookup"><span data-stu-id="9c676-428">It seems there are some outliers in the dataset.</span></span>

## <a name="use-the-histogram-inspector"></a><span data-ttu-id="9c676-429">Use the histogram inspector</span><span class="sxs-lookup"><span data-stu-id="9c676-429">Use the histogram inspector</span></span>

<span data-ttu-id="9c676-430">To attempt to identify outliers, right-click the __tripduration__ column, and select __Histogram__.</span><span class="sxs-lookup"><span data-stu-id="9c676-430">To attempt to identify outliers, right-click the __tripduration__ column, and select __Histogram__.</span></span>

![Histogram inspector](media/tutorial-bikeshare-dataprep/tripdurationhistogram.png)

<span data-ttu-id="9c676-432">The histogram isn't helpful because the outliers skew the graph.</span><span class="sxs-lookup"><span data-stu-id="9c676-432">The histogram isn't helpful because the outliers skew the graph.</span></span>

## <a name="add-a-column-by-using-script"></a><span data-ttu-id="9c676-433">Add a column by using script</span><span class="sxs-lookup"><span data-stu-id="9c676-433">Add a column by using script</span></span>

1. <span data-ttu-id="9c676-434">Right-click the **tripduration** column, and select **Add Column (Script)**.</span><span class="sxs-lookup"><span data-stu-id="9c676-434">Right-click the **tripduration** column, and select **Add Column (Script)**.</span></span>

    ![Add Column (Script) menu](media/tutorial-bikeshare-dataprep/computecolscript.png)

1. <span data-ttu-id="9c676-436">In the __Add Column (Script)__ dialog box, use the following values:</span><span class="sxs-lookup"><span data-stu-id="9c676-436">In the __Add Column (Script)__ dialog box, use the following values:</span></span>

    * <span data-ttu-id="9c676-437">__New Column Name__: logtripduration</span><span class="sxs-lookup"><span data-stu-id="9c676-437">__New Column Name__: logtripduration</span></span>

    * <span data-ttu-id="9c676-438">__Insert this New Column After__: tripduration</span><span class="sxs-lookup"><span data-stu-id="9c676-438">__Insert this New Column After__: tripduration</span></span>

    * <span data-ttu-id="9c676-439">__New Column Code__: `math.log(row.tripduration)`</span><span class="sxs-lookup"><span data-stu-id="9c676-439">__New Column Code__: `math.log(row.tripduration)`</span></span>

    * <span data-ttu-id="9c676-440">__Code Block Type__: Expression</span><span class="sxs-lookup"><span data-stu-id="9c676-440">__Code Block Type__: Expression</span></span>

   ![Add Column (Script) dialog box](media/tutorial-bikeshare-dataprep/computecolscriptdialog.png)

1. <span data-ttu-id="9c676-442">Select __OK__ to add the **logtripduration** column.</span><span class="sxs-lookup"><span data-stu-id="9c676-442">Select __OK__ to add the **logtripduration** column.</span></span>

1. <span data-ttu-id="9c676-443">Right-click the column, and select **Histogram**.</span><span class="sxs-lookup"><span data-stu-id="9c676-443">Right-click the column, and select **Histogram**.</span></span>

    ![Histogram of logtripduration column](media/tutorial-bikeshare-dataprep/logtriphistogram.png)

    <span data-ttu-id="9c676-445">Visually, this histogram seems like a normal distribution with an abnormal tail.</span><span class="sxs-lookup"><span data-stu-id="9c676-445">Visually, this histogram seems like a normal distribution with an abnormal tail.</span></span>

## <a name="use-an-advanced-filter"></a><span data-ttu-id="9c676-446">Use an advanced filter</span><span class="sxs-lookup"><span data-stu-id="9c676-446">Use an advanced filter</span></span>

<span data-ttu-id="9c676-447">Using a filter on the data updates the inspectors with the new distribution.</span><span class="sxs-lookup"><span data-stu-id="9c676-447">Using a filter on the data updates the inspectors with the new distribution.</span></span> 

1. <span data-ttu-id="9c676-448">Right-click the **logtripduration** column, and select **Filter Column**.</span><span class="sxs-lookup"><span data-stu-id="9c676-448">Right-click the **logtripduration** column, and select **Filter Column**.</span></span> 

1. <span data-ttu-id="9c676-449">In the __Edit__ dialog box, use the following values:</span><span class="sxs-lookup"><span data-stu-id="9c676-449">In the __Edit__ dialog box, use the following values:</span></span>

    * <span data-ttu-id="9c676-450">__Filter this Number Column__: logtripduration</span><span class="sxs-lookup"><span data-stu-id="9c676-450">__Filter this Number Column__: logtripduration</span></span>

    * <span data-ttu-id="9c676-451">__I Want To__: Keep Rows</span><span class="sxs-lookup"><span data-stu-id="9c676-451">__I Want To__: Keep Rows</span></span>

    * <span data-ttu-id="9c676-452">__When__: Any of the Conditions below are True (logical OR)</span><span class="sxs-lookup"><span data-stu-id="9c676-452">__When__: Any of the Conditions below are True (logical OR)</span></span>

    * <span data-ttu-id="9c676-453">__If this Column__: less than</span><span class="sxs-lookup"><span data-stu-id="9c676-453">__If this Column__: less than</span></span>

    * <span data-ttu-id="9c676-454">__The Value__: 9</span><span class="sxs-lookup"><span data-stu-id="9c676-454">__The Value__: 9</span></span>

    ![Filter options](media/tutorial-bikeshare-dataprep/loftripfilter.png)

1. <span data-ttu-id="9c676-456">Select __OK__ to apply the filter.</span><span class="sxs-lookup"><span data-stu-id="9c676-456">Select __OK__ to apply the filter.</span></span>

    ![Updated histograms after filter is applied](media/tutorial-bikeshare-dataprep/loftripfilteredinspector.png)

### <a name="the-halo-effect"></a><span data-ttu-id="9c676-458">The halo effect</span><span class="sxs-lookup"><span data-stu-id="9c676-458">The halo effect</span></span>

1. <span data-ttu-id="9c676-459">Maximize the **logtripduration** histogram.</span><span class="sxs-lookup"><span data-stu-id="9c676-459">Maximize the **logtripduration** histogram.</span></span> <span data-ttu-id="9c676-460">A blue histogram is overlaid on a gray histogram.</span><span class="sxs-lookup"><span data-stu-id="9c676-460">A blue histogram is overlaid on a gray histogram.</span></span> <span data-ttu-id="9c676-461">This display is called the **Halo Effect**:</span><span class="sxs-lookup"><span data-stu-id="9c676-461">This display is called the **Halo Effect**:</span></span>

    * <span data-ttu-id="9c676-462">The gray histogram represents the distribution before the operation (in this case, the filtering operation).</span><span class="sxs-lookup"><span data-stu-id="9c676-462">The gray histogram represents the distribution before the operation (in this case, the filtering operation).</span></span>

    * <span data-ttu-id="9c676-463">The blue histogram represents the histogram after the operation.</span><span class="sxs-lookup"><span data-stu-id="9c676-463">The blue histogram represents the histogram after the operation.</span></span> 

   <span data-ttu-id="9c676-464">The halo effect helps with visualizing the effect of an operation on the data.</span><span class="sxs-lookup"><span data-stu-id="9c676-464">The halo effect helps with visualizing the effect of an operation on the data.</span></span>

   ![Halo effect](media/tutorial-bikeshare-dataprep/loftripfilteredinspectormaximized.png)

    > [!NOTE]
    > <span data-ttu-id="9c676-466">The blue histogram appears shorter compared to the previous one.</span><span class="sxs-lookup"><span data-stu-id="9c676-466">The blue histogram appears shorter compared to the previous one.</span></span> <span data-ttu-id="9c676-467">This difference is due to automatic re-bucketing of data in the new range.</span><span class="sxs-lookup"><span data-stu-id="9c676-467">This difference is due to automatic re-bucketing of data in the new range.</span></span>

1. <span data-ttu-id="9c676-468">To remove the halo, select __Edit__ and clear __Show halo__.</span><span class="sxs-lookup"><span data-stu-id="9c676-468">To remove the halo, select __Edit__ and clear __Show halo__.</span></span>

    ![Options for the histogram](media/tutorial-bikeshare-dataprep/uncheckhalo.png)

1. <span data-ttu-id="9c676-470">Select **OK** to disable the halo effect.</span><span class="sxs-lookup"><span data-stu-id="9c676-470">Select **OK** to disable the halo effect.</span></span> <span data-ttu-id="9c676-471">Then minimize the histogram.</span><span class="sxs-lookup"><span data-stu-id="9c676-471">Then minimize the histogram.</span></span>

### <a name="remove-columns"></a><span data-ttu-id="9c676-472">Remove columns</span><span class="sxs-lookup"><span data-stu-id="9c676-472">Remove columns</span></span>

<span data-ttu-id="9c676-473">In the trip data, each row represents a bike pickup event.</span><span class="sxs-lookup"><span data-stu-id="9c676-473">In the trip data, each row represents a bike pickup event.</span></span> <span data-ttu-id="9c676-474">For this tutorial, you need only the **starttime** and **start station id** columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-474">For this tutorial, you need only the **starttime** and **start station id** columns.</span></span> <span data-ttu-id="9c676-475">To remove the other columns, multi-select these two columns, right-click the column header, and then select **Keep Column**.</span><span class="sxs-lookup"><span data-stu-id="9c676-475">To remove the other columns, multi-select these two columns, right-click the column header, and then select **Keep Column**.</span></span> <span data-ttu-id="9c676-476">Other columns are removed.</span><span class="sxs-lookup"><span data-stu-id="9c676-476">Other columns are removed.</span></span>

![Keep Column option](media/tutorial-bikeshare-dataprep/tripdatakeepcolumn.png)

### <a name="summarize-data-count"></a><span data-ttu-id="9c676-478">Summarize data (count)</span><span class="sxs-lookup"><span data-stu-id="9c676-478">Summarize data (count)</span></span>

<span data-ttu-id="9c676-479">To summarize bike demand for a two-hour period, use derived columns.</span><span class="sxs-lookup"><span data-stu-id="9c676-479">To summarize bike demand for a two-hour period, use derived columns.</span></span>

1. <span data-ttu-id="9c676-480">Right-click the **starttime** column, and select **Derive Column by Example**.</span><span class="sxs-lookup"><span data-stu-id="9c676-480">Right-click the **starttime** column, and select **Derive Column by Example**.</span></span>

    ![Derive Column by Example option](media/tutorial-bikeshare-dataprep/tripdataderivebyexample.png)

1. <span data-ttu-id="9c676-482">For the example, enter a value of **Jan 01, 2017 12AM-2AM** for the first row.</span><span class="sxs-lookup"><span data-stu-id="9c676-482">For the example, enter a value of **Jan 01, 2017 12AM-2AM** for the first row.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9c676-483">In the previous example of deriving columns, you used multiple steps to derive a column that contained the date and time period.</span><span class="sxs-lookup"><span data-stu-id="9c676-483">In the previous example of deriving columns, you used multiple steps to derive a column that contained the date and time period.</span></span> <span data-ttu-id="9c676-484">In this example, you can see that this operation can be performed as a single step by providing an example of the final output.</span><span class="sxs-lookup"><span data-stu-id="9c676-484">In this example, you can see that this operation can be performed as a single step by providing an example of the final output.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9c676-485">You can give an example against any of the rows.</span><span class="sxs-lookup"><span data-stu-id="9c676-485">You can give an example against any of the rows.</span></span> <span data-ttu-id="9c676-486">For this example, the value of **Jan 01, 2017 12AM-2AM** is valid for the first row of data.</span><span class="sxs-lookup"><span data-stu-id="9c676-486">For this example, the value of **Jan 01, 2017 12AM-2AM** is valid for the first row of data.</span></span>

    ![Example data](media/tutorial-bikeshare-dataprep/tripdataderivebyexamplefirstexample.png)

   > [!IMPORTANT]
   > <span data-ttu-id="9c676-488">On a Mac, follow this step instead of step 3:</span><span class="sxs-lookup"><span data-stu-id="9c676-488">On a Mac, follow this step instead of step 3:</span></span>
   >
   > * <span data-ttu-id="9c676-489">Go to the first cell that contains **Jan 01, 2017 1AM-2AM**.</span><span class="sxs-lookup"><span data-stu-id="9c676-489">Go to the first cell that contains **Jan 01, 2017 1AM-2AM**.</span></span> <span data-ttu-id="9c676-490">It should be row 14.</span><span class="sxs-lookup"><span data-stu-id="9c676-490">It should be row 14.</span></span> <span data-ttu-id="9c676-491">Correct the value to **Jan 01, 2017 12AM-2AM**, and select Enter.</span><span class="sxs-lookup"><span data-stu-id="9c676-491">Correct the value to **Jan 01, 2017 12AM-2AM**, and select Enter.</span></span> 

1. <span data-ttu-id="9c676-492">Wait until the application computes the values against all the rows.</span><span class="sxs-lookup"><span data-stu-id="9c676-492">Wait until the application computes the values against all the rows.</span></span> <span data-ttu-id="9c676-493">The process might take several seconds.</span><span class="sxs-lookup"><span data-stu-id="9c676-493">The process might take several seconds.</span></span> <span data-ttu-id="9c676-494">After the analysis is finished, use the __Review next suggested row__ link to review data.</span><span class="sxs-lookup"><span data-stu-id="9c676-494">After the analysis is finished, use the __Review next suggested row__ link to review data.</span></span>

   ![Finished analysis with review link](media/tutorial-bikeshare-dataprep/tripdatabyexanalysiscomplete.png)

    <span data-ttu-id="9c676-496">Ensure that the computed values are correct.</span><span class="sxs-lookup"><span data-stu-id="9c676-496">Ensure that the computed values are correct.</span></span> <span data-ttu-id="9c676-497">If not, update the value with the expected value, and select Enter.</span><span class="sxs-lookup"><span data-stu-id="9c676-497">If not, update the value with the expected value, and select Enter.</span></span> <span data-ttu-id="9c676-498">Then wait for the analysis to finish.</span><span class="sxs-lookup"><span data-stu-id="9c676-498">Then wait for the analysis to finish.</span></span> <span data-ttu-id="9c676-499">Complete the **Review next suggested row** process until you see **No suggestions**.</span><span class="sxs-lookup"><span data-stu-id="9c676-499">Complete the **Review next suggested row** process until you see **No suggestions**.</span></span> <span data-ttu-id="9c676-500">**No suggestions** means the application looked at the edge cases and is satisfied with the synthesized program.</span><span class="sxs-lookup"><span data-stu-id="9c676-500">**No suggestions** means the application looked at the edge cases and is satisfied with the synthesized program.</span></span> <span data-ttu-id="9c676-501">It's a best practice to perform a visual inspection of the transformed data before you accept the transformation.</span><span class="sxs-lookup"><span data-stu-id="9c676-501">It's a best practice to perform a visual inspection of the transformed data before you accept the transformation.</span></span> 

1. <span data-ttu-id="9c676-502">Select **OK** to accept the transform.</span><span class="sxs-lookup"><span data-stu-id="9c676-502">Select **OK** to accept the transform.</span></span> <span data-ttu-id="9c676-503">Rename the newly created column to **Date Hour Range**.</span><span class="sxs-lookup"><span data-stu-id="9c676-503">Rename the newly created column to **Date Hour Range**.</span></span>

    ![Renamed column](media/tutorial-bikeshare-dataprep/tripdatasummarize.png)

1. <span data-ttu-id="9c676-505">Right-click the **starttime** column header, and select **Remove column**.</span><span class="sxs-lookup"><span data-stu-id="9c676-505">Right-click the **starttime** column header, and select **Remove column**.</span></span>

1. <span data-ttu-id="9c676-506">To summarize the data, on the __Transform__ menu, select __Summarize__.</span><span class="sxs-lookup"><span data-stu-id="9c676-506">To summarize the data, on the __Transform__ menu, select __Summarize__.</span></span> <span data-ttu-id="9c676-507">To create the transformation, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="9c676-507">To create the transformation, use the following steps:</span></span>

    * <span data-ttu-id="9c676-508">Drag __Date Hour Range__ and __start station id__ to the **Group By** pane on the left.</span><span class="sxs-lookup"><span data-stu-id="9c676-508">Drag __Date Hour Range__ and __start station id__ to the **Group By** pane on the left.</span></span>

    * <span data-ttu-id="9c676-509">Drag __start station id__ to the **summarize data** pane on the right.</span><span class="sxs-lookup"><span data-stu-id="9c676-509">Drag __start station id__ to the **summarize data** pane on the right.</span></span>

   ![Summarization options](media/tutorial-bikeshare-dataprep/tripdatacount.png)

1. <span data-ttu-id="9c676-511">Select **OK** to accept the summary result.</span><span class="sxs-lookup"><span data-stu-id="9c676-511">Select **OK** to accept the summary result.</span></span>

## <a name="join-dataflows"></a><span data-ttu-id="9c676-512">Join dataflows</span><span class="sxs-lookup"><span data-stu-id="9c676-512">Join dataflows</span></span>

<span data-ttu-id="9c676-513">To join the weather data with the trip data, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="9c676-513">To join the weather data with the trip data, use the following steps:</span></span>

1. <span data-ttu-id="9c676-514">On the __Transforms__ menu, select __Join__.</span><span class="sxs-lookup"><span data-stu-id="9c676-514">On the __Transforms__ menu, select __Join__.</span></span>

1. <span data-ttu-id="9c676-515">__Tables__: Select **BostonWeather** as the **Left** dataflow and **201701-hubway-tripdata** as the **Right** dataflow.</span><span class="sxs-lookup"><span data-stu-id="9c676-515">__Tables__: Select **BostonWeather** as the **Left** dataflow and **201701-hubway-tripdata** as the **Right** dataflow.</span></span> <span data-ttu-id="9c676-516">To continue, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9c676-516">To continue, select **Next**.</span></span>

    ![Tables selections](media/tutorial-bikeshare-dataprep/jointableselection.png)

1. <span data-ttu-id="9c676-518">__Key Columns__: Select the **Date Hour Range** column in both the tables, and then select __Next__.</span><span class="sxs-lookup"><span data-stu-id="9c676-518">__Key Columns__: Select the **Date Hour Range** column in both the tables, and then select __Next__.</span></span>

    ![Key Columns selections](media/tutorial-bikeshare-dataprep/joinkeyselection.png)

1. <span data-ttu-id="9c676-520">__Join Type__: Select __Matching rows__ as the join type, and then select __Finish__.</span><span class="sxs-lookup"><span data-stu-id="9c676-520">__Join Type__: Select __Matching rows__ as the join type, and then select __Finish__.</span></span>

    ![Matching rows join type](media/tutorial-bikeshare-dataprep/joinscreen.png)

    <span data-ttu-id="9c676-522">This process creates a new dataflow named __Join Result__.</span><span class="sxs-lookup"><span data-stu-id="9c676-522">This process creates a new dataflow named __Join Result__.</span></span>

## <a name="create-additional-features"></a><span data-ttu-id="9c676-523">Create additional features</span><span class="sxs-lookup"><span data-stu-id="9c676-523">Create additional features</span></span>

1. <span data-ttu-id="9c676-524">To create a column that contains the day of the week, right-click the **Date Hour Range** column and select **Derive Column by Example**.</span><span class="sxs-lookup"><span data-stu-id="9c676-524">To create a column that contains the day of the week, right-click the **Date Hour Range** column and select **Derive Column by Example**.</span></span> <span data-ttu-id="9c676-525">Use a value of __Sun__ for a date that occurred on a Sunday.</span><span class="sxs-lookup"><span data-stu-id="9c676-525">Use a value of __Sun__ for a date that occurred on a Sunday.</span></span> <span data-ttu-id="9c676-526">An example is **Jan 01, 2017 12AM-2AM**.</span><span class="sxs-lookup"><span data-stu-id="9c676-526">An example is **Jan 01, 2017 12AM-2AM**.</span></span> <span data-ttu-id="9c676-527">Select Enter, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c676-527">Select Enter, and then select **OK**.</span></span> <span data-ttu-id="9c676-528">Rename this column to __Weekday__.</span><span class="sxs-lookup"><span data-stu-id="9c676-528">Rename this column to __Weekday__.</span></span>

    ![Create new column for day of the week](media/tutorial-bikeshare-dataprep/featureweekday.png)

1. <span data-ttu-id="9c676-530">To create a column that contains the time period for a row, right-click the **Date Hour Range** column, and select **Derive Column by example**.</span><span class="sxs-lookup"><span data-stu-id="9c676-530">To create a column that contains the time period for a row, right-click the **Date Hour Range** column, and select **Derive Column by example**.</span></span> <span data-ttu-id="9c676-531">Use a value of **12AM-2AM** for the row that contains **Jan 01, 2017 12AM-2AM**.</span><span class="sxs-lookup"><span data-stu-id="9c676-531">Use a value of **12AM-2AM** for the row that contains **Jan 01, 2017 12AM-2AM**.</span></span> <span data-ttu-id="9c676-532">Select Enter, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c676-532">Select Enter, and then select **OK**.</span></span> <span data-ttu-id="9c676-533">Rename this column to **Period**.</span><span class="sxs-lookup"><span data-stu-id="9c676-533">Rename this column to **Period**.</span></span>

    ![Period column](media/tutorial-bikeshare-dataprep/featurehourrange.png)

1. <span data-ttu-id="9c676-535">To remove the **Date Hour Range** and **r_Date Hour Range** columns, select Ctrl (Command ⌘ on Mac), and then select each column header.</span><span class="sxs-lookup"><span data-stu-id="9c676-535">To remove the **Date Hour Range** and **r_Date Hour Range** columns, select Ctrl (Command ⌘ on Mac), and then select each column header.</span></span> <span data-ttu-id="9c676-536">Right-click, and select **Remove Column**.</span><span class="sxs-lookup"><span data-stu-id="9c676-536">Right-click, and select **Remove Column**.</span></span>

## <a name="read-data-from-python"></a><span data-ttu-id="9c676-537">Read data from Python</span><span class="sxs-lookup"><span data-stu-id="9c676-537">Read data from Python</span></span>

<span data-ttu-id="9c676-538">You can run a data preparation package from Python or PySpark and retrieve the result as a **Data Frame**.</span><span class="sxs-lookup"><span data-stu-id="9c676-538">You can run a data preparation package from Python or PySpark and retrieve the result as a **Data Frame**.</span></span>

<span data-ttu-id="9c676-539">To generate an example Python script, right-click __BikeShare Data Prep__, and select __Generate Data Access Code File__.</span><span class="sxs-lookup"><span data-stu-id="9c676-539">To generate an example Python script, right-click __BikeShare Data Prep__, and select __Generate Data Access Code File__.</span></span> <span data-ttu-id="9c676-540">The example Python file is created in your **Project Folder** and is also loaded in a tab within Workbench.</span><span class="sxs-lookup"><span data-stu-id="9c676-540">The example Python file is created in your **Project Folder** and is also loaded in a tab within Workbench.</span></span> <span data-ttu-id="9c676-541">The following Python script is an example of the code that is generated:</span><span class="sxs-lookup"><span data-stu-id="9c676-541">The following Python script is an example of the code that is generated:</span></span>

```python
# Use the Azure Machine Learning data preparation package
from azureml.dataprep import package

# Use the Azure Machine Learning data collector to log various metrics
from azureml.logging import get_azureml_logger
logger = get_azureml_logger()

# This call will load the referenced package and return a DataFrame.
# If run in a PySpark environment, this call returns a
# Spark DataFrame. If not, it will return a Pandas DataFrame.
df = package.run('BikeShare Data Prep.dprep', dataflow_idx=0)

# Remove this line and add code that uses the DataFrame
df.head(10)
```

<span data-ttu-id="9c676-542">For this tutorial, the name of the file is `BikeShare Data Prep.py`.</span><span class="sxs-lookup"><span data-stu-id="9c676-542">For this tutorial, the name of the file is `BikeShare Data Prep.py`.</span></span> <span data-ttu-id="9c676-543">This file is used later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="9c676-543">This file is used later in the tutorial.</span></span>

## <a name="save-test-data-as-a-csv-file"></a><span data-ttu-id="9c676-544">Save test data as a CSV file</span><span class="sxs-lookup"><span data-stu-id="9c676-544">Save test data as a CSV file</span></span>

<span data-ttu-id="9c676-545">To save the **Join Result** dataflow to a .csv file, you must change the `BikeShare Data Prep.py` script.</span><span class="sxs-lookup"><span data-stu-id="9c676-545">To save the **Join Result** dataflow to a .csv file, you must change the `BikeShare Data Prep.py` script.</span></span> 

1. <span data-ttu-id="9c676-546">Open the project for editing in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9c676-546">Open the project for editing in Visual Studio Code.</span></span>

    ![Open project in Visual Studio Code](media/tutorial-bikeshare-dataprep/openprojectinvscode.png)

1. <span data-ttu-id="9c676-548">Update the Python script in the `BikeShare Data Prep.py` file by using the following code:</span><span class="sxs-lookup"><span data-stu-id="9c676-548">Update the Python script in the `BikeShare Data Prep.py` file by using the following code:</span></span>

    ```python
    import pyspark

    from azureml.dataprep.package import run
    from pyspark.sql.functions import *

    # start Spark session
    spark = pyspark.sql.SparkSession.builder.appName('BikeShare').getOrCreate()

    # dataflow_idx=2 sets the dataflow to the 3rd dataflow (the index starts at 0), the Join Result.
    df = run('BikeShare Data Prep.dprep', dataflow_idx=2)
    df.show(n=10)
    row_count_first = df.count()

    # Example file name: 'wasb://data-files@bikesharestorage.blob.core.windows.net/testata'
    # 'wasb://<your container name>@<your azure storage name>.blob.core.windows.net/<csv folder name>
    blobfolder = 'Your Azure Storage blob path'

    df.write.csv(blobfolder, mode='overwrite') 

    # retrieve csv file parts into one data frame
    csvfiles = "<Your Azure Storage blob path>/*.csv"
    df = spark.read.option("header", "false").csv(csvfiles)
    row_count_result = df.count()
    print(row_count_result)
    if (row_count_first == row_count_result):
        print('counts match')
    else:
        print('counts do not match')
    print('done')
    ```

1. <span data-ttu-id="9c676-549">Replace `Your Azure Storage blob path` with the path to the output file to be created.</span><span class="sxs-lookup"><span data-stu-id="9c676-549">Replace `Your Azure Storage blob path` with the path to the output file to be created.</span></span> <span data-ttu-id="9c676-550">Replace for both the `blobfolder` and `csvfiles` variables.</span><span class="sxs-lookup"><span data-stu-id="9c676-550">Replace for both the `blobfolder` and `csvfiles` variables.</span></span>

## <a name="create-an-hdinsight-run-configuration"></a><span data-ttu-id="9c676-551">Create an HDInsight run configuration</span><span class="sxs-lookup"><span data-stu-id="9c676-551">Create an HDInsight run configuration</span></span>

1. <span data-ttu-id="9c676-552">In Machine Learning Workbench, open the command-line window, select the **File** menu, and then select **Open Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="9c676-552">In Machine Learning Workbench, open the command-line window, select the **File** menu, and then select **Open Command Prompt**.</span></span> <span data-ttu-id="9c676-553">Your command prompt starts in the project folder with the prompt `C:\Projects\BikeShare>`.</span><span class="sxs-lookup"><span data-stu-id="9c676-553">Your command prompt starts in the project folder with the prompt `C:\Projects\BikeShare>`.</span></span>

    ![Open command prompt](media/tutorial-bikeshare-dataprep/opencommandprompt.png)

   >[!IMPORTANT]
   ><span data-ttu-id="9c676-555">You must use the command-line window (opened from Workbench) to accomplish the steps that follow.</span><span class="sxs-lookup"><span data-stu-id="9c676-555">You must use the command-line window (opened from Workbench) to accomplish the steps that follow.</span></span>

1. <span data-ttu-id="9c676-556">Use the command prompt to sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="9c676-556">Use the command prompt to sign in to Azure.</span></span> 

   <span data-ttu-id="9c676-557">The Workbench app and CLI use independent credential caches when you authenticate against Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9c676-557">The Workbench app and CLI use independent credential caches when you authenticate against Azure resources.</span></span> <span data-ttu-id="9c676-558">You need to do this only once until the cached token expires.</span><span class="sxs-lookup"><span data-stu-id="9c676-558">You need to do this only once until the cached token expires.</span></span> <span data-ttu-id="9c676-559">The `az account list` command returns the list of subscriptions available to your login.</span><span class="sxs-lookup"><span data-stu-id="9c676-559">The `az account list` command returns the list of subscriptions available to your login.</span></span> <span data-ttu-id="9c676-560">If there is more than one, use the ID value from the desired subscription.</span><span class="sxs-lookup"><span data-stu-id="9c676-560">If there is more than one, use the ID value from the desired subscription.</span></span> <span data-ttu-id="9c676-561">Set that subscription as the default account to use with the `az account set -s` command, and then provide the subscription ID value.</span><span class="sxs-lookup"><span data-stu-id="9c676-561">Set that subscription as the default account to use with the `az account set -s` command, and then provide the subscription ID value.</span></span> <span data-ttu-id="9c676-562">Then confirm the setting by using the account `show` command.</span><span class="sxs-lookup"><span data-stu-id="9c676-562">Then confirm the setting by using the account `show` command.</span></span>

   ```azurecli
   REM login by using the aka.ms/devicelogin site
   az login
   
   REM lists all Azure subscriptions you have access to 
   az account list -o table
   
   REM sets the current Azure subscription to the one you want to use
   az account set -s <subscriptionId>
   
   REM verifies that your current subscription is set correctly
   az account show
   ```

1. <span data-ttu-id="9c676-563">Create the HDInsight run config. You need the name of your cluster and the `sshuser` password.</span><span class="sxs-lookup"><span data-stu-id="9c676-563">Create the HDInsight run config. You need the name of your cluster and the `sshuser` password.</span></span>

    ```azurecli
    az ml computetarget attach cluster --name hdinsight --address <yourclustername>.azurehdinsight.net --username sshuser --password <your password>
    az ml experiment prepare -c hdinsight
    ```
> [!NOTE]
> <span data-ttu-id="9c676-564">When a blank project is created, the default run configurations are **local** and **docker**.</span><span class="sxs-lookup"><span data-stu-id="9c676-564">When a blank project is created, the default run configurations are **local** and **docker**.</span></span> <span data-ttu-id="9c676-565">This step creates a new run configuration that is available in Workbench when you run your scripts.</span><span class="sxs-lookup"><span data-stu-id="9c676-565">This step creates a new run configuration that is available in Workbench when you run your scripts.</span></span> 

## <a name="run-in-an-hdinsight-cluster"></a><span data-ttu-id="9c676-566">Run in an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="9c676-566">Run in an HDInsight cluster</span></span>

<span data-ttu-id="9c676-567">Return to the Machine Learning Workbench application to run your script in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="9c676-567">Return to the Machine Learning Workbench application to run your script in the HDInsight cluster.</span></span>

1. <span data-ttu-id="9c676-568">Return to the home screen of your project by selecting the **Home** icon on the left.</span><span class="sxs-lookup"><span data-stu-id="9c676-568">Return to the home screen of your project by selecting the **Home** icon on the left.</span></span>

1. <span data-ttu-id="9c676-569">Select **hdinsight** from the drop-down list to run your script in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="9c676-569">Select **hdinsight** from the drop-down list to run your script in the HDInsight cluster.</span></span>

1. <span data-ttu-id="9c676-570">Select **Run**.</span><span class="sxs-lookup"><span data-stu-id="9c676-570">Select **Run**.</span></span> <span data-ttu-id="9c676-571">The script is submitted as a job.</span><span class="sxs-lookup"><span data-stu-id="9c676-571">The script is submitted as a job.</span></span> <span data-ttu-id="9c676-572">The job status changes to __Completed__ after the file is written to the specified location in your storage container.</span><span class="sxs-lookup"><span data-stu-id="9c676-572">The job status changes to __Completed__ after the file is written to the specified location in your storage container.</span></span>

    ![HDInsight run script](media/tutorial-bikeshare-dataprep/hdinsightrunscript.png)


## <a name="substitute-data-sources"></a><span data-ttu-id="9c676-574">Substitute data sources</span><span class="sxs-lookup"><span data-stu-id="9c676-574">Substitute data sources</span></span>

<span data-ttu-id="9c676-575">In the previous steps, you used the `201701-hubway-tripdata.csv` and `BostonWeather.csv` data sources to prepare the test data.</span><span class="sxs-lookup"><span data-stu-id="9c676-575">In the previous steps, you used the `201701-hubway-tripdata.csv` and `BostonWeather.csv` data sources to prepare the test data.</span></span> <span data-ttu-id="9c676-576">To use the package with the other trip data files, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="9c676-576">To use the package with the other trip data files, use the following steps:</span></span>

1. <span data-ttu-id="9c676-577">Create a new data source by using the steps given previously, with the following changes to the process:</span><span class="sxs-lookup"><span data-stu-id="9c676-577">Create a new data source by using the steps given previously, with the following changes to the process:</span></span>

    * <span data-ttu-id="9c676-578">__File Selection__: When you select a file, multi-select the six remaining trip tripdata .csv files.</span><span class="sxs-lookup"><span data-stu-id="9c676-578">__File Selection__: When you select a file, multi-select the six remaining trip tripdata .csv files.</span></span>

    ![Load six remaining files](media/tutorial-bikeshare-dataprep/browseazurestoragefortripdatafiles.png)

    > [!NOTE]
     > <span data-ttu-id="9c676-580">The __+5__ entry indicates that there are five additional files beyond the one that is listed.</span><span class="sxs-lookup"><span data-stu-id="9c676-580">The __+5__ entry indicates that there are five additional files beyond the one that is listed.</span></span>

    * <span data-ttu-id="9c676-581">__File Details__: Set __Promote Headers Mode__ to **All Files Have The Same Headers**.</span><span class="sxs-lookup"><span data-stu-id="9c676-581">__File Details__: Set __Promote Headers Mode__ to **All Files Have The Same Headers**.</span></span> <span data-ttu-id="9c676-582">This value indicates that each of the files contains the same header.</span><span class="sxs-lookup"><span data-stu-id="9c676-582">This value indicates that each of the files contains the same header.</span></span>

    ![File details selection](media/tutorial-bikeshare-dataprep/headerfromeachfile.png) 

   <span data-ttu-id="9c676-584">Save the name of this data source because it's used in later steps.</span><span class="sxs-lookup"><span data-stu-id="9c676-584">Save the name of this data source because it's used in later steps.</span></span>

1. <span data-ttu-id="9c676-585">Select the folder icon to view the files in your project.</span><span class="sxs-lookup"><span data-stu-id="9c676-585">Select the folder icon to view the files in your project.</span></span> <span data-ttu-id="9c676-586">Expand the __aml\_config__ directory, and then select the `hdinsight.runconfig` file.</span><span class="sxs-lookup"><span data-stu-id="9c676-586">Expand the __aml\_config__ directory, and then select the `hdinsight.runconfig` file.</span></span>

    ![Location of hdinsight.runconfig](media/tutorial-bikeshare-dataprep/hdinsightsubstitutedatasources.png) 

1. <span data-ttu-id="9c676-588">Select the **Edit** button to open the file in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9c676-588">Select the **Edit** button to open the file in Visual Studio Code.</span></span>

1. <span data-ttu-id="9c676-589">Add the following lines at the end of the `hdinsight.runconfig` file, and then select the disk icon to save the file.</span><span class="sxs-lookup"><span data-stu-id="9c676-589">Add the following lines at the end of the `hdinsight.runconfig` file, and then select the disk icon to save the file.</span></span>

    ```yaml
    DataSourceSubstitutions:
      201701-hubway-tripdata.dsource: 201501-hubway-tripdata.dsource
    ```

    <span data-ttu-id="9c676-590">This change replaces the original data source with the one that contains the six trip data files.</span><span class="sxs-lookup"><span data-stu-id="9c676-590">This change replaces the original data source with the one that contains the six trip data files.</span></span>

## <a name="save-training-data-as-a-csv-file"></a><span data-ttu-id="9c676-591">Save training data as a CSV file</span><span class="sxs-lookup"><span data-stu-id="9c676-591">Save training data as a CSV file</span></span>

1. <span data-ttu-id="9c676-592">Browse to the Python file `BikeShare Data Prep.py` that you edited previously.</span><span class="sxs-lookup"><span data-stu-id="9c676-592">Browse to the Python file `BikeShare Data Prep.py` that you edited previously.</span></span> <span data-ttu-id="9c676-593">Provide a different file path to save the training data.</span><span class="sxs-lookup"><span data-stu-id="9c676-593">Provide a different file path to save the training data.</span></span>

    ```python
    import pyspark

    from azureml.dataprep.package import run
    from pyspark.sql.functions import *

    # start Spark session
    spark = pyspark.sql.SparkSession.builder.appName('BikeShare').getOrCreate()

    # dataflow_idx=2 sets the dataflow to the 3rd dataflow (the index starts at 0), the Join Result.
    df = run('BikeShare Data Prep.dprep', dataflow_idx=2)
    df.show(n=10)
    row_count_first = df.count()

    # Example file name: 'wasb://data-files@bikesharestorage.blob.core.windows.net/traindata'
    # 'wasb://<your container name>@<your azure storage name>.blob.core.windows.net/<csv folder name>
    blobfolder = 'Your Azure Storage blob path'

    df.write.csv(blobfolder, mode='overwrite') 

    # retrieve csv file parts into one data frame
    csvfiles = "<Your Azure Storage blob path>/*.csv"
    df = spark.read.option("header", "false").csv(csvfiles)
    row_count_result = df.count()
    print(row_count_result)
    if (row_count_first == row_count_result):
        print('counts match')
    else:
        print('counts do not match')
    print('done')
    ```

1. <span data-ttu-id="9c676-594">Use the folder named `traindata` for the training data output.</span><span class="sxs-lookup"><span data-stu-id="9c676-594">Use the folder named `traindata` for the training data output.</span></span>

1. <span data-ttu-id="9c676-595">To submit a new job, select **Run**.</span><span class="sxs-lookup"><span data-stu-id="9c676-595">To submit a new job, select **Run**.</span></span> <span data-ttu-id="9c676-596">Make sure **hdinsight** is selected.</span><span class="sxs-lookup"><span data-stu-id="9c676-596">Make sure **hdinsight** is selected.</span></span> <span data-ttu-id="9c676-597">A job is submitted with the new configuration.</span><span class="sxs-lookup"><span data-stu-id="9c676-597">A job is submitted with the new configuration.</span></span> <span data-ttu-id="9c676-598">The output of this job is the training data.</span><span class="sxs-lookup"><span data-stu-id="9c676-598">The output of this job is the training data.</span></span> <span data-ttu-id="9c676-599">This data is created by using the same data preparation steps that you followed previously.</span><span class="sxs-lookup"><span data-stu-id="9c676-599">This data is created by using the same data preparation steps that you followed previously.</span></span> <span data-ttu-id="9c676-600">The job might take a few minutes to finish.</span><span class="sxs-lookup"><span data-stu-id="9c676-600">The job might take a few minutes to finish.</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="9c676-601">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9c676-601">Clean up resources</span></span>

[!INCLUDE [aml-delete-resource-group](../../../includes/aml-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="9c676-602">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c676-602">Next steps</span></span>
<span data-ttu-id="9c676-603">You have finished the bike-share data preparation tutorial.</span><span class="sxs-lookup"><span data-stu-id="9c676-603">You have finished the bike-share data preparation tutorial.</span></span> <span data-ttu-id="9c676-604">In this tutorial, you used Machine Learning (preview) to learn how to:</span><span class="sxs-lookup"><span data-stu-id="9c676-604">In this tutorial, you used Machine Learning (preview) to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9c676-605">Prepare data interactively with the Machine Learning data preparation tool.</span><span class="sxs-lookup"><span data-stu-id="9c676-605">Prepare data interactively with the Machine Learning data preparation tool.</span></span>
> * <span data-ttu-id="9c676-606">Import, transform, and create a test dataset.</span><span class="sxs-lookup"><span data-stu-id="9c676-606">Import, transform, and create a test dataset.</span></span>
> * <span data-ttu-id="9c676-607">Generate a data preparation package.</span><span class="sxs-lookup"><span data-stu-id="9c676-607">Generate a data preparation package.</span></span>
> * <span data-ttu-id="9c676-608">Run the data preparation package by using Python.</span><span class="sxs-lookup"><span data-stu-id="9c676-608">Run the data preparation package by using Python.</span></span>
> * <span data-ttu-id="9c676-609">Generate a training dataset by reusing the data preparation package for additional input files.</span><span class="sxs-lookup"><span data-stu-id="9c676-609">Generate a training dataset by reusing the data preparation package for additional input files.</span></span>

<span data-ttu-id="9c676-610">Next, learn more about data preparation:</span><span class="sxs-lookup"><span data-stu-id="9c676-610">Next, learn more about data preparation:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9c676-611">Data preparation user guide</span><span class="sxs-lookup"><span data-stu-id="9c676-611">Data preparation user guide</span></span>](data-prep-user-guide.md)
