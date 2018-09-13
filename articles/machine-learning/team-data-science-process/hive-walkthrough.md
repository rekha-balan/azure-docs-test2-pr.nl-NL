---
title: Explore data in a Hadoop cluster and create models in Azure Machine Learning | Microsoft Docs
description: Using the Team Data Science Process for an end-to-end scenario, employing an HDInsight Hadoop cluster to build and deploy a model.
services: machine-learning,hdinsight
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: deguhath
ms.openlocfilehash: ff4daf350783e02141a6afea815165ccecfe0116
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864748"
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="bfa42-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="bfa42-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="bfa42-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](overview.md) in an end-to-end scenario.</span><span class="sxs-lookup"><span data-stu-id="bfa42-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](overview.md) in an end-to-end scenario.</span></span> <span data-ttu-id="bfa42-105">We use an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, and feature-engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down-sample the data.</span><span class="sxs-lookup"><span data-stu-id="bfa42-105">We use an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, and feature-engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down-sample the data.</span></span> <span data-ttu-id="bfa42-106">To handle binary and multiclass classification and regression predictive tasks, we build models of the data with Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfa42-106">To handle binary and multiclass classification and regression predictive tasks, we build models of the data with Azure Machine Learning.</span></span> 

<span data-ttu-id="bfa42-107">For a walkthrough that shows how to handle a larger dataset, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="bfa42-107">For a walkthrough that shows how to handle a larger dataset, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="bfa42-108">You can also use an IPython notebook to accomplish the tasks presented in the walkthrough that uses the 1 TB dataset.</span><span class="sxs-lookup"><span data-stu-id="bfa42-108">You can also use an IPython notebook to accomplish the tasks presented in the walkthrough that uses the 1 TB dataset.</span></span> <span data-ttu-id="bfa42-109">For more information, see [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb).</span><span class="sxs-lookup"><span data-stu-id="bfa42-109">For more information, see [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb).</span></span>

## <a name="dataset"></a><span data-ttu-id="bfa42-110">NYC Taxi Trips dataset description</span><span class="sxs-lookup"><span data-stu-id="bfa42-110">NYC Taxi Trips dataset description</span></span>
<span data-ttu-id="bfa42-111">The NYC Taxi Trip data is about 20 GB of compressed comma-separated values (CSV) files (~48 GB uncompressed).</span><span class="sxs-lookup"><span data-stu-id="bfa42-111">The NYC Taxi Trip data is about 20 GB of compressed comma-separated values (CSV) files (~48 GB uncompressed).</span></span> <span data-ttu-id="bfa42-112">It has more than 173 million individual trips, and includes the fares paid for each trip.</span><span class="sxs-lookup"><span data-stu-id="bfa42-112">It has more than 173 million individual trips, and includes the fares paid for each trip.</span></span> <span data-ttu-id="bfa42-113">Each trip record includes the pick-up and drop-off location and time, anonymized hack (driver's) license number, and medallion number (the taxi’s unique ID).</span><span class="sxs-lookup"><span data-stu-id="bfa42-113">Each trip record includes the pick-up and drop-off location and time, anonymized hack (driver's) license number, and medallion number (the taxi’s unique ID).</span></span> <span data-ttu-id="bfa42-114">The data covers all trips in the year 2013, and is provided in the following two datasets for each month:</span><span class="sxs-lookup"><span data-stu-id="bfa42-114">The data covers all trips in the year 2013, and is provided in the following two datasets for each month:</span></span>

- <span data-ttu-id="bfa42-115">The trip_data CSV files contain trip details.</span><span class="sxs-lookup"><span data-stu-id="bfa42-115">The trip_data CSV files contain trip details.</span></span> <span data-ttu-id="bfa42-116">This includes the number of passengers, pick-up and drop-off points, trip duration, and trip length.</span><span class="sxs-lookup"><span data-stu-id="bfa42-116">This includes the number of passengers, pick-up and drop-off points, trip duration, and trip length.</span></span> <span data-ttu-id="bfa42-117">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="bfa42-117">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
- <span data-ttu-id="bfa42-118">The trip_fare CSV files contain details of the fare paid for each trip.</span><span class="sxs-lookup"><span data-stu-id="bfa42-118">The trip_fare CSV files contain details of the fare paid for each trip.</span></span> <span data-ttu-id="bfa42-119">This includes payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span><span class="sxs-lookup"><span data-stu-id="bfa42-119">This includes payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="bfa42-120">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="bfa42-120">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="bfa42-121">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_license, and pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="bfa42-121">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_license, and pickup\_datetime.</span></span> <span data-ttu-id="bfa42-122">To get all of the details relevant to a particular trip, it is sufficient to join with these three keys.</span><span class="sxs-lookup"><span data-stu-id="bfa42-122">To get all of the details relevant to a particular trip, it is sufficient to join with these three keys.</span></span>

## <a name="mltasks"></a><span data-ttu-id="bfa42-123">Examples of prediction tasks</span><span class="sxs-lookup"><span data-stu-id="bfa42-123">Examples of prediction tasks</span></span>
<span data-ttu-id="bfa42-124">Determine the kind of predictions you want to make based on data analysis.</span><span class="sxs-lookup"><span data-stu-id="bfa42-124">Determine the kind of predictions you want to make based on data analysis.</span></span> <span data-ttu-id="bfa42-125">This helps clarify the tasks you need to include in your process.</span><span class="sxs-lookup"><span data-stu-id="bfa42-125">This helps clarify the tasks you need to include in your process.</span></span> <span data-ttu-id="bfa42-126">Here are three examples of prediction problems that we address in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="bfa42-126">Here are three examples of prediction problems that we address in this walkthrough.</span></span> <span data-ttu-id="bfa42-127">These are based on the *tip\_amount*:</span><span class="sxs-lookup"><span data-stu-id="bfa42-127">These are based on the *tip\_amount*:</span></span>

- <span data-ttu-id="bfa42-128">**Binary classification**: Predict whether or not a tip was paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="bfa42-128">**Binary classification**: Predict whether or not a tip was paid for a trip.</span></span> <span data-ttu-id="bfa42-129">That is, a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span><span class="sxs-lookup"><span data-stu-id="bfa42-129">That is, a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0: tip_amount = $0
        Class 1: tip_amount > $0
- <span data-ttu-id="bfa42-130">**Multiclass classification**: Predict the range of tip amounts paid for the trip.</span><span class="sxs-lookup"><span data-stu-id="bfa42-130">**Multiclass classification**: Predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="bfa42-131">We divide the *tip\_amount* into five classes:</span><span class="sxs-lookup"><span data-stu-id="bfa42-131">We divide the *tip\_amount* into five classes:</span></span>
   
        Class 0: tip_amount = $0
        Class 1: tip_amount > $0 and tip_amount <= $5
        Class 2: tip_amount > $5 and tip_amount <= $10
        Class 3: tip_amount > $10 and tip_amount <= $20
        Class 4: tip_amount > $20
- <span data-ttu-id="bfa42-132">**Regression task**: Predict the amount of the tip paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="bfa42-132">**Regression task**: Predict the amount of the tip paid for a trip.</span></span>  

## <a name="setup"></a><span data-ttu-id="bfa42-133">Set up an HDInsight Hadoop cluster for advanced analytics</span><span class="sxs-lookup"><span data-stu-id="bfa42-133">Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-134">This is typically an admin task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-134">This is typically an admin task.</span></span>
> 
> 

<span data-ttu-id="bfa42-135">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span><span class="sxs-lookup"><span data-stu-id="bfa42-135">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="bfa42-136">[Create a storage account](../../storage/common/storage-quickstart-create-account.md): This storage account is used for storing data in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="bfa42-136">[Create a storage account](../../storage/common/storage-quickstart-create-account.md): This storage account is used for storing data in Azure Blob storage.</span></span> <span data-ttu-id="bfa42-137">The data used in HDInsight clusters also resides here.</span><span class="sxs-lookup"><span data-stu-id="bfa42-137">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="bfa42-138">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="bfa42-138">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](customize-hadoop-cluster.md).</span></span> <span data-ttu-id="bfa42-139">This step creates an HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span><span class="sxs-lookup"><span data-stu-id="bfa42-139">This step creates an HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="bfa42-140">There are two important steps to remember while customizing your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-140">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="bfa42-141">Remember to link the storage account created in step 1 with your HDInsight cluster when you are creating it.</span><span class="sxs-lookup"><span data-stu-id="bfa42-141">Remember to link the storage account created in step 1 with your HDInsight cluster when you are creating it.</span></span> <span data-ttu-id="bfa42-142">This storage account accesses data that is processed within the cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-142">This storage account accesses data that is processed within the cluster.</span></span>
   * <span data-ttu-id="bfa42-143">After you create the cluster, enable Remote Access to the head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-143">After you create the cluster, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="bfa42-144">Browse to the **Configuration** tab, and select **Enable Remote**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-144">Browse to the **Configuration** tab, and select **Enable Remote**.</span></span> <span data-ttu-id="bfa42-145">This step specifies the user credentials used for remote login.</span><span class="sxs-lookup"><span data-stu-id="bfa42-145">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="bfa42-146">[Create an Azure Machine Learning workspace](../studio/create-workspace.md): You use this workspace to build machine learning models.</span><span class="sxs-lookup"><span data-stu-id="bfa42-146">[Create an Azure Machine Learning workspace](../studio/create-workspace.md): You use this workspace to build machine learning models.</span></span> <span data-ttu-id="bfa42-147">This task is addressed after completing an initial data exploration and down-sampling, by using the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-147">This task is addressed after completing an initial data exploration and down-sampling, by using the HDInsight cluster.</span></span>

## <a name="getdata"></a><span data-ttu-id="bfa42-148">Get the data from a public source</span><span class="sxs-lookup"><span data-stu-id="bfa42-148">Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-149">This is typically an admin task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-149">This is typically an admin task.</span></span>
> 
> 

<span data-ttu-id="bfa42-150">To copy the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset to your machine from its public location, use any of the methods described in [Move data to and from Azure Blob storage](move-azure-blob.md).</span><span class="sxs-lookup"><span data-stu-id="bfa42-150">To copy the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset to your machine from its public location, use any of the methods described in [Move data to and from Azure Blob storage](move-azure-blob.md).</span></span>

<span data-ttu-id="bfa42-151">Here, we describe how to use AzCopy to transfer the files containing data.</span><span class="sxs-lookup"><span data-stu-id="bfa42-151">Here, we describe how to use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="bfa42-152">To download and install AzCopy, follow the instructions at [Getting started with the AzCopy command-line utility](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="bfa42-152">To download and install AzCopy, follow the instructions at [Getting started with the AzCopy command-line utility](../../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="bfa42-153">From a command prompt window, run the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span><span class="sxs-lookup"><span data-stu-id="bfa42-153">From a command prompt window, run the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="bfa42-154">When the copy completes, you will see a total of 24 zipped files in the data folder chosen.</span><span class="sxs-lookup"><span data-stu-id="bfa42-154">When the copy completes, you will see a total of 24 zipped files in the data folder chosen.</span></span> <span data-ttu-id="bfa42-155">Unzip the downloaded files to the same directory on your local machine.</span><span class="sxs-lookup"><span data-stu-id="bfa42-155">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="bfa42-156">Make a note of the folder where the uncompressed files reside.</span><span class="sxs-lookup"><span data-stu-id="bfa42-156">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="bfa42-157">This folder is referred to as the *<path\_to\_unzipped_data\_files\>* in what follows.</span><span class="sxs-lookup"><span data-stu-id="bfa42-157">This folder is referred to as the *<path\_to\_unzipped_data\_files\>* in what follows.</span></span>

## <a name="upload"></a><span data-ttu-id="bfa42-158">Upload the data to the default container of the HDInsight Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="bfa42-158">Upload the data to the default container of the HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-159">This is typically an admin task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-159">This is typically an admin task.</span></span>
> 
> 

<span data-ttu-id="bfa42-160">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span><span class="sxs-lookup"><span data-stu-id="bfa42-160">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="bfa42-161">***<path_to_data_folder>*** The directory (along with the path) on your machine that contains the unzipped data files.</span><span class="sxs-lookup"><span data-stu-id="bfa42-161">***<path_to_data_folder>*** The directory (along with the path) on your machine that contains the unzipped data files.</span></span>  
* <span data-ttu-id="bfa42-162">***<storage account name of Hadoop cluster>*** The storage account associated with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-162">***<storage account name of Hadoop cluster>*** The storage account associated with your HDInsight cluster.</span></span>
* <span data-ttu-id="bfa42-163">***<default container of Hadoop cluster>*** The default container used by your cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-163">***<default container of Hadoop cluster>*** The default container used by your cluster.</span></span> <span data-ttu-id="bfa42-164">Note that the name of the default container is usually the same name as the cluster itself.</span><span class="sxs-lookup"><span data-stu-id="bfa42-164">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="bfa42-165">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span><span class="sxs-lookup"><span data-stu-id="bfa42-165">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="bfa42-166">***<storage account key>*** The key for the storage account used by your cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-166">***<storage account key>*** The key for the storage account used by your cluster.</span></span>

<span data-ttu-id="bfa42-167">From a command prompt or a Windows PowerShell window, run the following two AzCopy commands.</span><span class="sxs-lookup"><span data-stu-id="bfa42-167">From a command prompt or a Windows PowerShell window, run the following two AzCopy commands.</span></span>

<span data-ttu-id="bfa42-168">This command uploads the trip data to the ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-168">This command uploads the trip data to the ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="bfa42-169">This command uploads the fare data to the ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-169">This command uploads the fare data to the ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="bfa42-170">The data should now be in Blob storage, and ready to be consumed within the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-170">The data should now be in Blob storage, and ready to be consumed within the HDInsight cluster.</span></span>

## <a name="#download-hql-files"></a><span data-ttu-id="bfa42-171">Sign in to the head node of Hadoop cluster and prepare for exploratory data analysis</span><span class="sxs-lookup"><span data-stu-id="bfa42-171">Sign in to the head node of Hadoop cluster and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-172">This is typically an admin task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-172">This is typically an admin task.</span></span>
> 
> 

<span data-ttu-id="bfa42-173">To access the head node of the cluster for exploratory data analysis and down-sampling of the data, follow the procedure outlined in [Access the head node of Hadoop Cluster](customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="bfa42-173">To access the head node of the cluster for exploratory data analysis and down-sampling of the data, follow the procedure outlined in [Access the head node of Hadoop Cluster](customize-hadoop-cluster.md).</span></span>

<span data-ttu-id="bfa42-174">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span><span class="sxs-lookup"><span data-stu-id="bfa42-174">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="bfa42-175">The Hive queries are stored in .hql files.</span><span class="sxs-lookup"><span data-stu-id="bfa42-175">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="bfa42-176">We then down-sample this data to be used within Machine Learning for building models.</span><span class="sxs-lookup"><span data-stu-id="bfa42-176">We then down-sample this data to be used within Machine Learning for building models.</span></span>

<span data-ttu-id="bfa42-177">To prepare the cluster for exploratory data analysis, download the .hql files containing the relevant Hive scripts from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span><span class="sxs-lookup"><span data-stu-id="bfa42-177">To prepare the cluster for exploratory data analysis, download the .hql files containing the relevant Hive scripts from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="bfa42-178">To do this, open the command prompt from within the head node of the cluster, and run the following two commands:</span><span class="sxs-lookup"><span data-stu-id="bfa42-178">To do this, open the command prompt from within the head node of the cluster, and run the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="bfa42-179">These two commands download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span><span class="sxs-lookup"><span data-stu-id="bfa42-179">These two commands download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <a name="#hive-db-tables"></a><span data-ttu-id="bfa42-180">Create Hive database and tables partitioned by month</span><span class="sxs-lookup"><span data-stu-id="bfa42-180">Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-181">This is typically an admin task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-181">This is typically an admin task.</span></span>
> 
> 

<span data-ttu-id="bfa42-182">You are now ready to create Hive tables for the NYC taxi dataset.</span><span class="sxs-lookup"><span data-stu-id="bfa42-182">You are now ready to create Hive tables for the NYC taxi dataset.</span></span>
<span data-ttu-id="bfa42-183">In the head node of the Hadoop cluster, open the Hadoop command line on the desktop of the head node.</span><span class="sxs-lookup"><span data-stu-id="bfa42-183">In the head node of the Hadoop cluster, open the Hadoop command line on the desktop of the head node.</span></span> <span data-ttu-id="bfa42-184">Enter the Hive directory by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bfa42-184">Enter the Hive directory by running the following command:</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="bfa42-185">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span><span class="sxs-lookup"><span data-stu-id="bfa42-185">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="bfa42-186">This handles any path issues automatically.</span><span class="sxs-lookup"><span data-stu-id="bfa42-186">This handles any path issues automatically.</span></span> <span data-ttu-id="bfa42-187">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop command line" interchangeably in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="bfa42-187">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop command line" interchangeably in this walkthrough.</span></span>
> 
> 

<span data-ttu-id="bfa42-188">From the Hive directory prompt, run the following command in the Hadoop command line of the head node.</span><span class="sxs-lookup"><span data-stu-id="bfa42-188">From the Hive directory prompt, run the following command in the Hadoop command line of the head node.</span></span> <span data-ttu-id="bfa42-189">This submits the Hive query to create the Hive database and tables:</span><span class="sxs-lookup"><span data-stu-id="bfa42-189">This submits the Hive query to create the Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="bfa42-190">Here is the content of the **C:\temp\sample\_hive\_create\_db\_and\_tables.hql** file.</span><span class="sxs-lookup"><span data-stu-id="bfa42-190">Here is the content of the **C:\temp\sample\_hive\_create\_db\_and\_tables.hql** file.</span></span> <span data-ttu-id="bfa42-191">This creates the Hive database **nyctaxidb**, and the tables **trip** and **fare**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-191">This creates the Hive database **nyctaxidb**, and the tables **trip** and **fare**.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="bfa42-192">This Hive script creates two tables:</span><span class="sxs-lookup"><span data-stu-id="bfa42-192">This Hive script creates two tables:</span></span>

* <span data-ttu-id="bfa42-193">The **trip** table contains trip details of each ride (driver details, pick-up time, trip distance, and times).</span><span class="sxs-lookup"><span data-stu-id="bfa42-193">The **trip** table contains trip details of each ride (driver details, pick-up time, trip distance, and times).</span></span>
* <span data-ttu-id="bfa42-194">The **fare** table contains fare details (fare amount, tip amount, tolls, and surcharges).</span><span class="sxs-lookup"><span data-stu-id="bfa42-194">The **fare** table contains fare details (fare amount, tip amount, tolls, and surcharges).</span></span>

<span data-ttu-id="bfa42-195">If you need any additional assistance with these procedures, or you want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop command line](move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="bfa42-195">If you need any additional assistance with these procedures, or you want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop command line](move-hive-tables.md#submit).</span></span>

## <a name="#load-data"></a><span data-ttu-id="bfa42-196">Load data to Hive tables by partitions</span><span class="sxs-lookup"><span data-stu-id="bfa42-196">Load data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-197">This is typically an admin task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-197">This is typically an admin task.</span></span>
> 
> 

<span data-ttu-id="bfa42-198">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span><span class="sxs-lookup"><span data-stu-id="bfa42-198">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="bfa42-199">The following PowerShell commands (issued from the Hive directory by using the Hadoop command line) load data to the trip and fare Hive tables, partitioned by month.</span><span class="sxs-lookup"><span data-stu-id="bfa42-199">The following PowerShell commands (issued from the Hive directory by using the Hadoop command line) load data to the trip and fare Hive tables, partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="bfa42-200">The **sample\_hive\_load\_data\_by\_partitions.hql** file contains the following **LOAD** commands:</span><span class="sxs-lookup"><span data-stu-id="bfa42-200">The **sample\_hive\_load\_data\_by\_partitions.hql** file contains the following **LOAD** commands:</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="bfa42-201">Note that a number of the Hive queries used here in the exploration process involve looking at only one or two partitions.</span><span class="sxs-lookup"><span data-stu-id="bfa42-201">Note that a number of the Hive queries used here in the exploration process involve looking at only one or two partitions.</span></span> <span data-ttu-id="bfa42-202">But these queries can be run across the entire dataset.</span><span class="sxs-lookup"><span data-stu-id="bfa42-202">But these queries can be run across the entire dataset.</span></span>

### <a name="#show-db"></a><span data-ttu-id="bfa42-203">Show databases in the HDInsight Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="bfa42-203">Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="bfa42-204">To show the databases created in HDInsight Hadoop cluster inside the Hadoop command-line window, run the following command in the Hadoop command line:</span><span class="sxs-lookup"><span data-stu-id="bfa42-204">To show the databases created in HDInsight Hadoop cluster inside the Hadoop command-line window, run the following command in the Hadoop command line:</span></span>

    hive -e "show databases;"

### <a name="#show-tables"></a><span data-ttu-id="bfa42-205">Show the Hive tables in the **nyctaxidb** database</span><span class="sxs-lookup"><span data-stu-id="bfa42-205">Show the Hive tables in the **nyctaxidb** database</span></span>
<span data-ttu-id="bfa42-206">To show the tables in the **nyctaxidb** database, run the following command in the Hadoop command line:</span><span class="sxs-lookup"><span data-stu-id="bfa42-206">To show the tables in the **nyctaxidb** database, run the following command in the Hadoop command line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="bfa42-207">We can confirm that the tables are partitioned by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bfa42-207">We can confirm that the tables are partitioned by running the following command:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="bfa42-208">Here is the expected output:</span><span class="sxs-lookup"><span data-stu-id="bfa42-208">Here is the expected output:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="bfa42-209">Similarly, we can ensure that the fare table is partitioned by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bfa42-209">Similarly, we can ensure that the fare table is partitioned by running the following command:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="bfa42-210">Here is the expected output:</span><span class="sxs-lookup"><span data-stu-id="bfa42-210">Here is the expected output:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a><span data-ttu-id="bfa42-211">Data exploration and feature engineering in Hive</span><span class="sxs-lookup"><span data-stu-id="bfa42-211">Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-212">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-212">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-213">You  can use Hive queries to accomplish data exploration and feature engineering tasks for the data loaded into the Hive tables.</span><span class="sxs-lookup"><span data-stu-id="bfa42-213">You  can use Hive queries to accomplish data exploration and feature engineering tasks for the data loaded into the Hive tables.</span></span> <span data-ttu-id="bfa42-214">Here are examples of such tasks:</span><span class="sxs-lookup"><span data-stu-id="bfa42-214">Here are examples of such tasks:</span></span>

* <span data-ttu-id="bfa42-215">View the top 10 records in both tables.</span><span class="sxs-lookup"><span data-stu-id="bfa42-215">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="bfa42-216">Explore data distributions of a few fields in varying time windows.</span><span class="sxs-lookup"><span data-stu-id="bfa42-216">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="bfa42-217">Investigate data quality of the longitude and latitude fields.</span><span class="sxs-lookup"><span data-stu-id="bfa42-217">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="bfa42-218">Generate binary and multiclass classification labels based on the tip amount.</span><span class="sxs-lookup"><span data-stu-id="bfa42-218">Generate binary and multiclass classification labels based on the tip amount.</span></span>
* <span data-ttu-id="bfa42-219">Generate features by computing the direct trip distances.</span><span class="sxs-lookup"><span data-stu-id="bfa42-219">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="bfa42-220">Exploration: View the top 10 records in table trip</span><span class="sxs-lookup"><span data-stu-id="bfa42-220">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-221">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-221">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-222">To see what the data looks like, examine 10 records from each table.</span><span class="sxs-lookup"><span data-stu-id="bfa42-222">To see what the data looks like, examine 10 records from each table.</span></span> <span data-ttu-id="bfa42-223">To inspect the records, run the following two queries separately from the Hive directory prompt in the Hadoop command-line console.</span><span class="sxs-lookup"><span data-stu-id="bfa42-223">To inspect the records, run the following two queries separately from the Hive directory prompt in the Hadoop command-line console.</span></span>

<span data-ttu-id="bfa42-224">To get the top 10 records in the trip table from the first month:</span><span class="sxs-lookup"><span data-stu-id="bfa42-224">To get the top 10 records in the trip table from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="bfa42-225">To get the top 10 records in the fare table from the first month:</span><span class="sxs-lookup"><span data-stu-id="bfa42-225">To get the top 10 records in the fare table from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="bfa42-226">You can save the records to a file for convenient viewing.</span><span class="sxs-lookup"><span data-stu-id="bfa42-226">You can save the records to a file for convenient viewing.</span></span> <span data-ttu-id="bfa42-227">A small change to the preceding query accomplishes this:</span><span class="sxs-lookup"><span data-stu-id="bfa42-227">A small change to the preceding query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="bfa42-228">Exploration: View the number of records in each of the 12 partitions</span><span class="sxs-lookup"><span data-stu-id="bfa42-228">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-229">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-229">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-230">Of interest is how the number of trips varies during the calendar year.</span><span class="sxs-lookup"><span data-stu-id="bfa42-230">Of interest is how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="bfa42-231">Grouping by month shows the distribution of trips.</span><span class="sxs-lookup"><span data-stu-id="bfa42-231">Grouping by month shows the distribution of trips.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="bfa42-232">This gives us the following output:</span><span class="sxs-lookup"><span data-stu-id="bfa42-232">This gives us the following output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="bfa42-233">Here, the first column is the month, and the second is the number of trips for that month.</span><span class="sxs-lookup"><span data-stu-id="bfa42-233">Here, the first column is the month, and the second is the number of trips for that month.</span></span>

<span data-ttu-id="bfa42-234">We can also count the total number of records in our trip dataset by running the following command at the Hive directory prompt:</span><span class="sxs-lookup"><span data-stu-id="bfa42-234">We can also count the total number of records in our trip dataset by running the following command at the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="bfa42-235">This yields:</span><span class="sxs-lookup"><span data-stu-id="bfa42-235">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="bfa42-236">Using commands similar to those shown for the trip dataset, we can issue Hive queries from the Hive directory prompt for the fare dataset to validate the number of records.</span><span class="sxs-lookup"><span data-stu-id="bfa42-236">Using commands similar to those shown for the trip dataset, we can issue Hive queries from the Hive directory prompt for the fare dataset to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="bfa42-237">This gives us the following output:</span><span class="sxs-lookup"><span data-stu-id="bfa42-237">This gives us the following output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="bfa42-238">Note that the exact same number of trips per month is returned for both datasets.</span><span class="sxs-lookup"><span data-stu-id="bfa42-238">Note that the exact same number of trips per month is returned for both datasets.</span></span> <span data-ttu-id="bfa42-239">This provides the first validation that the data has been loaded correctly.</span><span class="sxs-lookup"><span data-stu-id="bfa42-239">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="bfa42-240">You can count the total number of records in the fare dataset by using the following command from the Hive directory prompt:</span><span class="sxs-lookup"><span data-stu-id="bfa42-240">You can count the total number of records in the fare dataset by using the following command from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="bfa42-241">This yields:</span><span class="sxs-lookup"><span data-stu-id="bfa42-241">This yields:</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="bfa42-242">The total number of records in both tables is also the same.</span><span class="sxs-lookup"><span data-stu-id="bfa42-242">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="bfa42-243">This provides a second validation that the data has been loaded correctly.</span><span class="sxs-lookup"><span data-stu-id="bfa42-243">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="bfa42-244">Exploration: Trip distribution by medallion</span><span class="sxs-lookup"><span data-stu-id="bfa42-244">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-245">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-245">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-246">This example identifies the medallions (taxi numbers) with greater than 100 trips within a given time period.</span><span class="sxs-lookup"><span data-stu-id="bfa42-246">This example identifies the medallions (taxi numbers) with greater than 100 trips within a given time period.</span></span> <span data-ttu-id="bfa42-247">The query benefits from the partitioned table access, because it is conditioned by the partition variable **month**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-247">The query benefits from the partitioned table access, because it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="bfa42-248">The query results are written to a local file, **queryoutput.tsv**, in `C:\temp` on the head node.</span><span class="sxs-lookup"><span data-stu-id="bfa42-248">The query results are written to a local file, **queryoutput.tsv**, in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="bfa42-249">Here is the content of the **sample\_hive\_trip\_count\_by\_medallion.hql** file for inspection.</span><span class="sxs-lookup"><span data-stu-id="bfa42-249">Here is the content of the **sample\_hive\_trip\_count\_by\_medallion.hql** file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="bfa42-250">The medallion in the NYC taxi dataset identifies a unique cab.</span><span class="sxs-lookup"><span data-stu-id="bfa42-250">The medallion in the NYC taxi dataset identifies a unique cab.</span></span> <span data-ttu-id="bfa42-251">You can identify which cabs are comparatively busy by asking which ones made more than a certain number of trips in a particular time period.</span><span class="sxs-lookup"><span data-stu-id="bfa42-251">You can identify which cabs are comparatively busy by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="bfa42-252">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, **C:\temp\queryoutput.tsv**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-252">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, **C:\temp\queryoutput.tsv**.</span></span>

<span data-ttu-id="bfa42-253">Here is the content of the **sample\_hive\_trip\_count\_by\_medallion.hql** file for inspection.</span><span class="sxs-lookup"><span data-stu-id="bfa42-253">Here is the content of the **sample\_hive\_trip\_count\_by\_medallion.hql** file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="bfa42-254">From the Hive directory prompt, run the following command:</span><span class="sxs-lookup"><span data-stu-id="bfa42-254">From the Hive directory prompt, run the following command:</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="bfa42-255">Exploration: Trip distribution by medallion and hack license</span><span class="sxs-lookup"><span data-stu-id="bfa42-255">Exploration: Trip distribution by medallion and hack license</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-256">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-256">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-257">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span><span class="sxs-lookup"><span data-stu-id="bfa42-257">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="bfa42-258">This section provides an example of how to do this for cabs and drivers.</span><span class="sxs-lookup"><span data-stu-id="bfa42-258">This section provides an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="bfa42-259">The **sample\_hive\_trip\_count\_by\_medallion\_license.hql** file groups the fare dataset on **medallion** and **hack_license**, and returns counts of each combination.</span><span class="sxs-lookup"><span data-stu-id="bfa42-259">The **sample\_hive\_trip\_count\_by\_medallion\_license.hql** file groups the fare dataset on **medallion** and **hack_license**, and returns counts of each combination.</span></span> <span data-ttu-id="bfa42-260">Here are its contents:</span><span class="sxs-lookup"><span data-stu-id="bfa42-260">Here are its contents:</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="bfa42-261">This query returns cab and driver combinations, ordered by descending number of trips.</span><span class="sxs-lookup"><span data-stu-id="bfa42-261">This query returns cab and driver combinations, ordered by descending number of trips.</span></span>

<span data-ttu-id="bfa42-262">From the Hive directory prompt, run:</span><span class="sxs-lookup"><span data-stu-id="bfa42-262">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="bfa42-263">The query results are written to a local file, **C:\temp\queryoutput.tsv**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-263">The query results are written to a local file, **C:\temp\queryoutput.tsv**.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitude-or-latitude-records"></a><span data-ttu-id="bfa42-264">Exploration: Assessing data quality by checking for invalid longitude or latitude records</span><span class="sxs-lookup"><span data-stu-id="bfa42-264">Exploration: Assessing data quality by checking for invalid longitude or latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-265">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-265">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-266">A common objective of exploratory data analysis is to weed out invalid or bad records.</span><span class="sxs-lookup"><span data-stu-id="bfa42-266">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="bfa42-267">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span><span class="sxs-lookup"><span data-stu-id="bfa42-267">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="bfa42-268">Since it is likely that such records have an erroneous longitude-latitude value, we want to eliminate them from any data that is to be used for modeling.</span><span class="sxs-lookup"><span data-stu-id="bfa42-268">Since it is likely that such records have an erroneous longitude-latitude value, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="bfa42-269">Here is the content of **sample\_hive\_quality\_assessment.hql** file for inspection.</span><span class="sxs-lookup"><span data-stu-id="bfa42-269">Here is the content of **sample\_hive\_quality\_assessment.hql** file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="bfa42-270">From the Hive directory prompt, run:</span><span class="sxs-lookup"><span data-stu-id="bfa42-270">From the Hive directory prompt, run:</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="bfa42-271">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span><span class="sxs-lookup"><span data-stu-id="bfa42-271">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="bfa42-272">This is useful because it makes the screen print of the Hive query output more readable.</span><span class="sxs-lookup"><span data-stu-id="bfa42-272">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="bfa42-273">Exploration: Binary class distributions of trip tips</span><span class="sxs-lookup"><span data-stu-id="bfa42-273">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-274">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-274">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-275">For the binary classification problem outlined in the [Examples of prediction tasks](hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span><span class="sxs-lookup"><span data-stu-id="bfa42-275">For the binary classification problem outlined in the [Examples of prediction tasks](hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="bfa42-276">This distribution of tips is binary:</span><span class="sxs-lookup"><span data-stu-id="bfa42-276">This distribution of tips is binary:</span></span>

* <span data-ttu-id="bfa42-277">tip given (Class 1, tip\_amount > $0)</span><span class="sxs-lookup"><span data-stu-id="bfa42-277">tip given (Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="bfa42-278">no tip (Class 0, tip\_amount = $0)</span><span class="sxs-lookup"><span data-stu-id="bfa42-278">no tip (Class 0, tip\_amount = $0)</span></span>

<span data-ttu-id="bfa42-279">The following **sample\_hive\_tipped\_frequencies.hql** file does this:</span><span class="sxs-lookup"><span data-stu-id="bfa42-279">The following **sample\_hive\_tipped\_frequencies.hql** file does this:</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="bfa42-280">From the Hive directory prompt, run:</span><span class="sxs-lookup"><span data-stu-id="bfa42-280">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="bfa42-281">Exploration: Class distributions in the multiclass setting</span><span class="sxs-lookup"><span data-stu-id="bfa42-281">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-282">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-282">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-283">For the multiclass classification problem outlined in the [Examples of prediction tasks](hive-walkthrough.md#mltasks) section, this dataset also lends itself to a natural classification to predict the amount of the tips given.</span><span class="sxs-lookup"><span data-stu-id="bfa42-283">For the multiclass classification problem outlined in the [Examples of prediction tasks](hive-walkthrough.md#mltasks) section, this dataset also lends itself to a natural classification to predict the amount of the tips given.</span></span> <span data-ttu-id="bfa42-284">We can use bins to define tip ranges in the query.</span><span class="sxs-lookup"><span data-stu-id="bfa42-284">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="bfa42-285">To get the class distributions for the various tip ranges, use the **sample\_hive\_tip\_range\_frequencies.hql** file.</span><span class="sxs-lookup"><span data-stu-id="bfa42-285">To get the class distributions for the various tip ranges, use the **sample\_hive\_tip\_range\_frequencies.hql** file.</span></span> <span data-ttu-id="bfa42-286">Here are its contents.</span><span class="sxs-lookup"><span data-stu-id="bfa42-286">Here are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="bfa42-287">Run the following command from the Hadoop command-line console:</span><span class="sxs-lookup"><span data-stu-id="bfa42-287">Run the following command from the Hadoop command-line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-the-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="bfa42-288">Exploration: Compute the direct distance between two longitude-latitude locations</span><span class="sxs-lookup"><span data-stu-id="bfa42-288">Exploration: Compute the direct distance between two longitude-latitude locations</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-289">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-289">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-290">You might want to know if there is a difference between the direct distance between two locations, and the actual trip distance of the taxi.</span><span class="sxs-lookup"><span data-stu-id="bfa42-290">You might want to know if there is a difference between the direct distance between two locations, and the actual trip distance of the taxi.</span></span> <span data-ttu-id="bfa42-291">A passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a longer route.</span><span class="sxs-lookup"><span data-stu-id="bfa42-291">A passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a longer route.</span></span>

<span data-ttu-id="bfa42-292">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), you can use the trigonometric functions available within Hive:</span><span class="sxs-lookup"><span data-stu-id="bfa42-292">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), you can use the trigonometric functions available within Hive:</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="bfa42-293">In the preceding query, R is the radius of the Earth in miles, and pi is converted to radians.</span><span class="sxs-lookup"><span data-stu-id="bfa42-293">In the preceding query, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="bfa42-294">Note that the longitude-latitude points are filtered to remove values that are far from the NYC area.</span><span class="sxs-lookup"><span data-stu-id="bfa42-294">Note that the longitude-latitude points are filtered to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="bfa42-295">In this case, we write the results to a directory called **queryoutputdir**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-295">In this case, we write the results to a directory called **queryoutputdir**.</span></span> <span data-ttu-id="bfa42-296">The sequence of the following commands first creates this output directory, and then runs the Hive command.</span><span class="sxs-lookup"><span data-stu-id="bfa42-296">The sequence of the following commands first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="bfa42-297">From the Hive directory prompt, run:</span><span class="sxs-lookup"><span data-stu-id="bfa42-297">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="bfa42-298">The query results are written to nine Azure blobs (**queryoutputdir/000000\_0** to  **queryoutputdir/000008\_0**), under the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-298">The query results are written to nine Azure blobs (**queryoutputdir/000000\_0** to  **queryoutputdir/000008\_0**), under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="bfa42-299">To see the size of the individual blobs, run the following command from the Hive directory prompt:</span><span class="sxs-lookup"><span data-stu-id="bfa42-299">To see the size of the individual blobs, run the following command from the Hive directory prompt:</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="bfa42-300">To see the contents of a given file, say **000000\_0**, use Hadoop's `copyToLocal` command.</span><span class="sxs-lookup"><span data-stu-id="bfa42-300">To see the contents of a given file, say **000000\_0**, use Hadoop's `copyToLocal` command.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="bfa42-301">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span><span class="sxs-lookup"><span data-stu-id="bfa42-301">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="bfa42-302">A key advantage of having this data reside in an Azure blob is that we can explore the data within Machine Learning, by using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="bfa42-302">A key advantage of having this data reside in an Azure blob is that we can explore the data within Machine Learning, by using the [Import Data][import-data] module.</span></span>

## <a name="#downsample"></a><span data-ttu-id="bfa42-303">Down-sample data and build models in Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bfa42-303">Down-sample data and build models in Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="bfa42-304">This is typically a data scientist task.</span><span class="sxs-lookup"><span data-stu-id="bfa42-304">This is typically a data scientist task.</span></span>
> 
> 

<span data-ttu-id="bfa42-305">After the exploratory data analysis phase, we are now ready to down-sample the data for building models in Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfa42-305">After the exploratory data analysis phase, we are now ready to down-sample the data for building models in Machine Learning.</span></span> <span data-ttu-id="bfa42-306">In this section, we show how to use a Hive query to down-sample the data.</span><span class="sxs-lookup"><span data-stu-id="bfa42-306">In this section, we show how to use a Hive query to down-sample the data.</span></span> <span data-ttu-id="bfa42-307">Machine Learning then accesses it from the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="bfa42-307">Machine Learning then accesses it from the [Import Data][import-data] module.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="bfa42-308">Down-sampling the data</span><span class="sxs-lookup"><span data-stu-id="bfa42-308">Down-sampling the data</span></span>
<span data-ttu-id="bfa42-309">There are two steps in this procedure.</span><span class="sxs-lookup"><span data-stu-id="bfa42-309">There are two steps in this procedure.</span></span> <span data-ttu-id="bfa42-310">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records: **medallion**, **hack\_license**, and **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-310">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records: **medallion**, **hack\_license**, and **pickup\_datetime**.</span></span> <span data-ttu-id="bfa42-311">We then generate a binary classification label, **tipped**, and a multiclass classification label, **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-311">We then generate a binary classification label, **tipped**, and a multiclass classification label, **tip\_class**.</span></span>

<span data-ttu-id="bfa42-312">To be able to use the down-sampled data directly from the [Import Data][import-data] module in Machine Learning, you should store the results of the preceding query to an internal Hive table.</span><span class="sxs-lookup"><span data-stu-id="bfa42-312">To be able to use the down-sampled data directly from the [Import Data][import-data] module in Machine Learning, you should store the results of the preceding query to an internal Hive table.</span></span> <span data-ttu-id="bfa42-313">In what follows, we create an internal Hive table and populate its contents with the joined and down-sampled data.</span><span class="sxs-lookup"><span data-stu-id="bfa42-313">In what follows, we create an internal Hive table and populate its contents with the joined and down-sampled data.</span></span>

<span data-ttu-id="bfa42-314">The query applies standard Hive functions directly to generate the following from the **pickup\_datetime** field:</span><span class="sxs-lookup"><span data-stu-id="bfa42-314">The query applies standard Hive functions directly to generate the following from the **pickup\_datetime** field:</span></span>
- <span data-ttu-id="bfa42-315">hour of day</span><span class="sxs-lookup"><span data-stu-id="bfa42-315">hour of day</span></span>
- <span data-ttu-id="bfa42-316">week of year</span><span class="sxs-lookup"><span data-stu-id="bfa42-316">week of year</span></span>
- <span data-ttu-id="bfa42-317">weekday (1 stands for Monday, and 7 stands for Sunday)</span><span class="sxs-lookup"><span data-stu-id="bfa42-317">weekday (1 stands for Monday, and 7 stands for Sunday)</span></span>

<span data-ttu-id="bfa42-318">The query also generates the direct distance between the pick-up and drop-off locations.</span><span class="sxs-lookup"><span data-stu-id="bfa42-318">The query also generates the direct distance between the pick-up and drop-off locations.</span></span> <span data-ttu-id="bfa42-319">For a complete list of such functions, see [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF).</span><span class="sxs-lookup"><span data-stu-id="bfa42-319">For a complete list of such functions, see [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF).</span></span>

<span data-ttu-id="bfa42-320">The query then down-samples the data so that the query results can fit into Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="bfa42-320">The query then down-samples the data so that the query results can fit into Azure Machine Learning Studio.</span></span> <span data-ttu-id="bfa42-321">Only about 1 percent of the original dataset is imported into the studio.</span><span class="sxs-lookup"><span data-stu-id="bfa42-321">Only about 1 percent of the original dataset is imported into the studio.</span></span>

<span data-ttu-id="bfa42-322">Here are the contents of **sample\_hive\_prepare\_for\_aml\_full.hql** file that prepares data for model building in Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="bfa42-322">Here are the contents of **sample\_hive\_prepare\_for\_aml\_full.hql** file that prepares data for model building in Machine Learning:</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of the join into the above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="bfa42-323">To run this query from the Hive directory prompt:</span><span class="sxs-lookup"><span data-stu-id="bfa42-323">To run this query from the Hive directory prompt:</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="bfa42-324">We now have an internal table, **nyctaxidb.nyctaxi_downsampled_dataset**, which can be accessed by using the [Import Data][import-data] module from Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfa42-324">We now have an internal table, **nyctaxidb.nyctaxi_downsampled_dataset**, which can be accessed by using the [Import Data][import-data] module from Machine Learning.</span></span> <span data-ttu-id="bfa42-325">Furthermore, we can use this dataset for building Machine Learning models.</span><span class="sxs-lookup"><span data-stu-id="bfa42-325">Furthermore, we can use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="bfa42-326">Use the Import Data module in Machine Learning to access the down-sampled data</span><span class="sxs-lookup"><span data-stu-id="bfa42-326">Use the Import Data module in Machine Learning to access the down-sampled data</span></span>
<span data-ttu-id="bfa42-327">To issue Hive queries in the [Import Data][import-data] module of Machine Learning, you need access to a Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="bfa42-327">To issue Hive queries in the [Import Data][import-data] module of Machine Learning, you need access to a Machine Learning workspace.</span></span> <span data-ttu-id="bfa42-328">You also need access to the credentials of the cluster and its associated storage account.</span><span class="sxs-lookup"><span data-stu-id="bfa42-328">You also need access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="bfa42-329">Here are some details about the [Import Data][import-data] module and the parameters to input:</span><span class="sxs-lookup"><span data-stu-id="bfa42-329">Here are some details about the [Import Data][import-data] module and the parameters to input:</span></span>

<span data-ttu-id="bfa42-330">**HCatalog server URI**: If the cluster name is **abc123**, this is simply: https://abc123.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="bfa42-330">**HCatalog server URI**: If the cluster name is **abc123**, this is simply: https://abc123.azurehdinsight.net.</span></span>

<span data-ttu-id="bfa42-331">**Hadoop user account name**: The user name chosen for the cluster (not the remote access user name).</span><span class="sxs-lookup"><span data-stu-id="bfa42-331">**Hadoop user account name**: The user name chosen for the cluster (not the remote access user name).</span></span>

<span data-ttu-id="bfa42-332">**Hadoop ser account password**: The password chosen for the cluster (not the remote access password).</span><span class="sxs-lookup"><span data-stu-id="bfa42-332">**Hadoop ser account password**: The password chosen for the cluster (not the remote access password).</span></span>

<span data-ttu-id="bfa42-333">**Location of output data**: This is chosen to be Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa42-333">**Location of output data**: This is chosen to be Azure.</span></span>

<span data-ttu-id="bfa42-334">**Azure storage account name**: Name of the default storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa42-334">**Azure storage account name**: Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="bfa42-335">**Azure container name**: This is the default container name for the cluster, and is typically the same as the cluster name.</span><span class="sxs-lookup"><span data-stu-id="bfa42-335">**Azure container name**: This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="bfa42-336">For a cluster called **abc123**, this is abc123.</span><span class="sxs-lookup"><span data-stu-id="bfa42-336">For a cluster called **abc123**, this is abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfa42-337">Any table we wish to query by using the [Import Data][import-data] module in Machine Learning must be an internal table.</span><span class="sxs-lookup"><span data-stu-id="bfa42-337">Any table we wish to query by using the [Import Data][import-data] module in Machine Learning must be an internal table.</span></span>
> 
> 

<span data-ttu-id="bfa42-338">Here is how to determine if a table **T** in a database **D.db** is an internal table.</span><span class="sxs-lookup"><span data-stu-id="bfa42-338">Here is how to determine if a table **T** in a database **D.db** is an internal table.</span></span> <span data-ttu-id="bfa42-339">From the Hive directory prompt, run the following command:</span><span class="sxs-lookup"><span data-stu-id="bfa42-339">From the Hive directory prompt, run the following command:</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="bfa42-340">If the table is an internal table and it is populated, its contents must show here.</span><span class="sxs-lookup"><span data-stu-id="bfa42-340">If the table is an internal table and it is populated, its contents must show here.</span></span>

<span data-ttu-id="bfa42-341">Another way to determine whether a table is an internal table is to use Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="bfa42-341">Another way to determine whether a table is an internal table is to use Azure Storage Explorer.</span></span> <span data-ttu-id="bfa42-342">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span><span class="sxs-lookup"><span data-stu-id="bfa42-342">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="bfa42-343">If the table and its contents show up, this confirms that it is an internal table.</span><span class="sxs-lookup"><span data-stu-id="bfa42-343">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="bfa42-344">Here is a screenshot of the Hive query and the [Import Data][import-data] module:</span><span class="sxs-lookup"><span data-stu-id="bfa42-344">Here is a screenshot of the Hive query and the [Import Data][import-data] module:</span></span>

![Screenshot of Hive query for Import Data module](./media/hive-walkthrough/1eTYf52.png)

<span data-ttu-id="bfa42-346">Because our down-sampled data resides in the default container, the resulting Hive query from Machine Learning is very simple.</span><span class="sxs-lookup"><span data-stu-id="bfa42-346">Because our down-sampled data resides in the default container, the resulting Hive query from Machine Learning is very simple.</span></span> <span data-ttu-id="bfa42-347">It is just a **SELECT \* FROM nyctaxidb.nyctaxi\_downsampled\_data**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-347">It is just a **SELECT \* FROM nyctaxidb.nyctaxi\_downsampled\_data**.</span></span>

<span data-ttu-id="bfa42-348">The dataset can now be used as the starting point for building Machine Learning models.</span><span class="sxs-lookup"><span data-stu-id="bfa42-348">The dataset can now be used as the starting point for building Machine Learning models.</span></span>

### <a name="mlmodel"></a><span data-ttu-id="bfa42-349">Build models in Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bfa42-349">Build models in Machine Learning</span></span>
<span data-ttu-id="bfa42-350">You can now proceed to model building and model deployment in [Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="bfa42-350">You can now proceed to model building and model deployment in [Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="bfa42-351">The data is ready for us to use in addressing the prediction problems identified earlier:</span><span class="sxs-lookup"><span data-stu-id="bfa42-351">The data is ready for us to use in addressing the prediction problems identified earlier:</span></span>

- <span data-ttu-id="bfa42-352">**Binary classification**: To predict whether or not a tip was paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="bfa42-352">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

  <span data-ttu-id="bfa42-353">**Learner used:** Two-class logistic regression</span><span class="sxs-lookup"><span data-stu-id="bfa42-353">**Learner used:** Two-class logistic regression</span></span>

  <span data-ttu-id="bfa42-354">a.</span><span class="sxs-lookup"><span data-stu-id="bfa42-354">a.</span></span> <span data-ttu-id="bfa42-355">For this problem, the target (or class) label is **tipped**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-355">For this problem, the target (or class) label is **tipped**.</span></span> <span data-ttu-id="bfa42-356">The original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span><span class="sxs-lookup"><span data-stu-id="bfa42-356">The original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="bfa42-357">In particular, **tip\_class**, **tip\_amount**, and **total\_amount** reveal information about the target label that is not available at testing time.</span><span class="sxs-lookup"><span data-stu-id="bfa42-357">In particular, **tip\_class**, **tip\_amount**, and **total\_amount** reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="bfa42-358">We remove these columns from consideration by using the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="bfa42-358">We remove these columns from consideration by using the [Select Columns in Dataset][select-columns] module.</span></span>

  <span data-ttu-id="bfa42-359">The following diagram shows our experiment to predict whether or not a tip was paid for a given trip:</span><span class="sxs-lookup"><span data-stu-id="bfa42-359">The following diagram shows our experiment to predict whether or not a tip was paid for a given trip:</span></span>

  ![Diagram of experiment](./media/hive-walkthrough/QGxRz5A.png)

  <span data-ttu-id="bfa42-361">b.</span><span class="sxs-lookup"><span data-stu-id="bfa42-361">b.</span></span> <span data-ttu-id="bfa42-362">For this experiment, our target label distributions were roughly 1:1.</span><span class="sxs-lookup"><span data-stu-id="bfa42-362">For this experiment, our target label distributions were roughly 1:1.</span></span>

   <span data-ttu-id="bfa42-363">The following chart shows the distribution of tip class labels for the binary classification problem:</span><span class="sxs-lookup"><span data-stu-id="bfa42-363">The following chart shows the distribution of tip class labels for the binary classification problem:</span></span>

  ![Chart of distribution of tip class labels](./media/hive-walkthrough/9mM4jlD.png)

    <span data-ttu-id="bfa42-365">As a result, we obtain an area under the curve (AUC) of 0.987, as shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="bfa42-365">As a result, we obtain an area under the curve (AUC) of 0.987, as shown in the following figure:</span></span>

  ![Chart of AUC value](./media/hive-walkthrough/8JDT0F8.png)

- <span data-ttu-id="bfa42-367">**Multiclass classification**: To predict the range of tip amounts paid for the trip, by using the previously defined classes.</span><span class="sxs-lookup"><span data-stu-id="bfa42-367">**Multiclass classification**: To predict the range of tip amounts paid for the trip, by using the previously defined classes.</span></span>

  <span data-ttu-id="bfa42-368">**Learner used:** Multiclass logistic regression</span><span class="sxs-lookup"><span data-stu-id="bfa42-368">**Learner used:** Multiclass logistic regression</span></span>

  <span data-ttu-id="bfa42-369">a.</span><span class="sxs-lookup"><span data-stu-id="bfa42-369">a.</span></span> <span data-ttu-id="bfa42-370">For this problem, our target (or class) label is **tip\_class**, which can take one of five values (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="bfa42-370">For this problem, our target (or class) label is **tip\_class**, which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="bfa42-371">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span><span class="sxs-lookup"><span data-stu-id="bfa42-371">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="bfa42-372">In particular, **tipped**, **tip\_amount**, and **total\_amount** reveal information about the target label that is not available at testing time.</span><span class="sxs-lookup"><span data-stu-id="bfa42-372">In particular, **tipped**, **tip\_amount**, and **total\_amount** reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="bfa42-373">We remove these columns by using the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="bfa42-373">We remove these columns by using the [Select Columns in Dataset][select-columns] module.</span></span>

  <span data-ttu-id="bfa42-374">The following diagram shows the experiment to predict in which bin a tip is likely to fall.</span><span class="sxs-lookup"><span data-stu-id="bfa42-374">The following diagram shows the experiment to predict in which bin a tip is likely to fall.</span></span> <span data-ttu-id="bfa42-375">The bins are: Class 0: tip = $0, Class 1: tip > $0 and tip <= $5, Class 2: tip > $5 and tip <= $10, Class 3: tip > $10 and tip <= $20, and Class 4: tip > $20.</span><span class="sxs-lookup"><span data-stu-id="bfa42-375">The bins are: Class 0: tip = $0, Class 1: tip > $0 and tip <= $5, Class 2: tip > $5 and tip <= $10, Class 3: tip > $10 and tip <= $20, and Class 4: tip > $20.</span></span>

  ![Diagram of experiment](./media/hive-walkthrough/5ztv0n0.png)

  <span data-ttu-id="bfa42-377">We now show what the actual test class distribution looks like.</span><span class="sxs-lookup"><span data-stu-id="bfa42-377">We now show what the actual test class distribution looks like.</span></span> <span data-ttu-id="bfa42-378">Class 0 and Class 1 are prevalent, and the other classes are rare.</span><span class="sxs-lookup"><span data-stu-id="bfa42-378">Class 0 and Class 1 are prevalent, and the other classes are rare.</span></span>

  ![Chart of test class distribution](./media/hive-walkthrough/Vy1FUKa.png)

  <span data-ttu-id="bfa42-380">b.</span><span class="sxs-lookup"><span data-stu-id="bfa42-380">b.</span></span> <span data-ttu-id="bfa42-381">For this experiment, we use a confusion matrix to look at the prediction accuracies.</span><span class="sxs-lookup"><span data-stu-id="bfa42-381">For this experiment, we use a confusion matrix to look at the prediction accuracies.</span></span> <span data-ttu-id="bfa42-382">This is shown here:</span><span class="sxs-lookup"><span data-stu-id="bfa42-382">This is shown here:</span></span>

  ![Confusion matrix](./media/hive-walkthrough/cxFmErM.png)

  <span data-ttu-id="bfa42-384">Note that while the class accuracies on the prevalent classes are quite good, the model does not do a good job of "learning" on the rarer classes.</span><span class="sxs-lookup"><span data-stu-id="bfa42-384">Note that while the class accuracies on the prevalent classes are quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

- <span data-ttu-id="bfa42-385">**Regression task**: To predict the amount of tip paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="bfa42-385">**Regression task**: To predict the amount of tip paid for a trip.</span></span>

  <span data-ttu-id="bfa42-386">**Learner used:** Boosted decision tree</span><span class="sxs-lookup"><span data-stu-id="bfa42-386">**Learner used:** Boosted decision tree</span></span>

  <span data-ttu-id="bfa42-387">a.</span><span class="sxs-lookup"><span data-stu-id="bfa42-387">a.</span></span> <span data-ttu-id="bfa42-388">For this problem, the target (or class) label is **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-388">For this problem, the target (or class) label is **tip\_amount**.</span></span> <span data-ttu-id="bfa42-389">The target leaks in this case are: **tipped**, **tip\_class**, and **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="bfa42-389">The target leaks in this case are: **tipped**, **tip\_class**, and **total\_amount**.</span></span> <span data-ttu-id="bfa42-390">All these variables reveal information about the tip amount that is typically unavailable at testing time.</span><span class="sxs-lookup"><span data-stu-id="bfa42-390">All these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="bfa42-391">We remove these columns by using the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="bfa42-391">We remove these columns by using the [Select Columns in Dataset][select-columns] module.</span></span>

  <span data-ttu-id="bfa42-392">The following diagram shows the experiment to predict the amount of the given tip:</span><span class="sxs-lookup"><span data-stu-id="bfa42-392">The following diagram shows the experiment to predict the amount of the given tip:</span></span>

  ![Diagram of experiment](./media/hive-walkthrough/11TZWgV.png)

  <span data-ttu-id="bfa42-394">b.</span><span class="sxs-lookup"><span data-stu-id="bfa42-394">b.</span></span> <span data-ttu-id="bfa42-395">For regression problems, we measure the accuracies of the prediction by looking at the squared error in the predictions, and the coefficient of determination:</span><span class="sxs-lookup"><span data-stu-id="bfa42-395">For regression problems, we measure the accuracies of the prediction by looking at the squared error in the predictions, and the coefficient of determination:</span></span>

  ![Screenshot of prediction statistics](./media/hive-walkthrough/Jat9mrz.png)

  <span data-ttu-id="bfa42-397">Here, the coefficient of determination is 0.709, implying that about 71 percent of the variance is explained by the model coefficients.</span><span class="sxs-lookup"><span data-stu-id="bfa42-397">Here, the coefficient of determination is 0.709, implying that about 71 percent of the variance is explained by the model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfa42-398">To learn more about Machine Learning and how to access and use it, see [What's Machine Learning](../studio/what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="bfa42-398">To learn more about Machine Learning and how to access and use it, see [What's Machine Learning](../studio/what-is-machine-learning.md).</span></span> <span data-ttu-id="bfa42-399">In addition, the [Azure AI Gallery](https://gallery.cortanaintelligence.com/) covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfa42-399">In addition, the [Azure AI Gallery](https://gallery.cortanaintelligence.com/) covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="bfa42-400">License information</span><span class="sxs-lookup"><span data-stu-id="bfa42-400">License information</span></span>
<span data-ttu-id="bfa42-401">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span><span class="sxs-lookup"><span data-stu-id="bfa42-401">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="bfa42-402">For more details, see the **LICENSE.txt** file in the directory of the sample code on GitHub.</span><span class="sxs-lookup"><span data-stu-id="bfa42-402">For more details, see the **LICENSE.txt** file in the directory of the sample code on GitHub.</span></span>

## <a name="references"></a><span data-ttu-id="bfa42-403">References</span><span class="sxs-lookup"><span data-stu-id="bfa42-403">References</span></span>
<span data-ttu-id="bfa42-404">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="bfa42-404">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="bfa42-405">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="bfa42-405">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="bfa42-406">•    [NYC Taxi and Limousine Commission Research and Statistics](http://www.nyc.gov/html/tlc/html/technology/aggregated_data.shtml)</span><span class="sxs-lookup"><span data-stu-id="bfa42-406">•    [NYC Taxi and Limousine Commission Research and Statistics](http://www.nyc.gov/html/tlc/html/technology/aggregated_data.shtml)</span></span>

[2]: ./media/hive-walkthrough/output-hive-results-3.png
[11]: ./media/hive-walkthrough/hive-reader-properties.png
[12]: ./media/hive-walkthrough/binary-classification-training.png
[13]: ./media/hive-walkthrough/create-scoring-experiment.png
[14]: ./media/hive-walkthrough/binary-classification-scoring.png
[15]: ./media/hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/



