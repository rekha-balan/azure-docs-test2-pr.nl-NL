---
title: Explore data in a Hadoop cluster and create models in Azure Machine Learning | Microsoft Docs
description: Using the Team Data Science Process for an end-to-end scenario employing an HDInsight Hadoop cluster to build and deploy a model using a publicly available dataset.
services: machine-learning,hdinsight
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 650fdb77b63b9e658dd206c291952ea443d23839
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552191"
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="5642e-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="5642e-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="5642e-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span><span class="sxs-lookup"><span data-stu-id="5642e-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span></span> <span data-ttu-id="5642e-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span><span class="sxs-lookup"><span data-stu-id="5642e-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="5642e-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5642e-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="5642e-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span><span class="sxs-lookup"><span data-stu-id="5642e-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span></span> <span data-ttu-id="5642e-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span><span class="sxs-lookup"><span data-stu-id="5642e-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <a name="dataset"></a><span data-ttu-id="5642e-109">NYC Taxi Trips Dataset description</span><span class="sxs-lookup"><span data-stu-id="5642e-109">NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="5642e-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span><span class="sxs-lookup"><span data-stu-id="5642e-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="5642e-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span><span class="sxs-lookup"><span data-stu-id="5642e-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="5642e-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span><span class="sxs-lookup"><span data-stu-id="5642e-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="5642e-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span><span class="sxs-lookup"><span data-stu-id="5642e-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="5642e-114">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="5642e-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="5642e-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span><span class="sxs-lookup"><span data-stu-id="5642e-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="5642e-116">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="5642e-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="5642e-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="5642e-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="5642e-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span><span class="sxs-lookup"><span data-stu-id="5642e-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="5642e-119">We describe some more details of the data when we store them into Hive tables shortly.</span><span class="sxs-lookup"><span data-stu-id="5642e-119">We describe some more details of the data when we store them into Hive tables shortly.</span></span>

## <a name="mltasks"></a><span data-ttu-id="5642e-120">Examples of prediction tasks</span><span class="sxs-lookup"><span data-stu-id="5642e-120">Examples of prediction tasks</span></span>
<span data-ttu-id="5642e-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span><span class="sxs-lookup"><span data-stu-id="5642e-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span></span>
<span data-ttu-id="5642e-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span><span class="sxs-lookup"><span data-stu-id="5642e-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span></span>

1. <span data-ttu-id="5642e-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span><span class="sxs-lookup"><span data-stu-id="5642e-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="5642e-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span><span class="sxs-lookup"><span data-stu-id="5642e-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="5642e-125">We divide the *tip\_amount* into five bins or classes:</span><span class="sxs-lookup"><span data-stu-id="5642e-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="5642e-126">**Regression task**: To predict the amount of the tip paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="5642e-126">**Regression task**: To predict the amount of the tip paid for a trip.</span></span>  

## <a name="setup"></a><span data-ttu-id="5642e-127">Set up an HDInsight Hadoop cluster for advanced analytics</span><span class="sxs-lookup"><span data-stu-id="5642e-127">Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-128">This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5642e-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span><span class="sxs-lookup"><span data-stu-id="5642e-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="5642e-130">[Create a storage account](../storage/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="5642e-130">[Create a storage account](../storage/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="5642e-131">The data used in HDInsight clusters also resides here.</span><span class="sxs-lookup"><span data-stu-id="5642e-131">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="5642e-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5642e-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="5642e-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span><span class="sxs-lookup"><span data-stu-id="5642e-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="5642e-134">There are two important steps to remember while customizing your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-134">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="5642e-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span><span class="sxs-lookup"><span data-stu-id="5642e-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="5642e-136">This storage account is used to access data that is processed within the cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-136">This storage account is used to access data that is processed within the cluster.</span></span>
   * <span data-ttu-id="5642e-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="5642e-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span><span class="sxs-lookup"><span data-stu-id="5642e-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="5642e-139">This step specifies the user credentials used for remote login.</span><span class="sxs-lookup"><span data-stu-id="5642e-139">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="5642e-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span><span class="sxs-lookup"><span data-stu-id="5642e-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span></span> <span data-ttu-id="5642e-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span></span>

## <a name="getdata"></a><span data-ttu-id="5642e-142">Get the data from a public source</span><span class="sxs-lookup"><span data-stu-id="5642e-142">Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-143">This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5642e-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span><span class="sxs-lookup"><span data-stu-id="5642e-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span></span>

<span data-ttu-id="5642e-145">Here we describe how use AzCopy to transfer the files containing data.</span><span class="sxs-lookup"><span data-stu-id="5642e-145">Here we describe how use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="5642e-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5642e-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="5642e-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span><span class="sxs-lookup"><span data-stu-id="5642e-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="5642e-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span><span class="sxs-lookup"><span data-stu-id="5642e-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span></span> <span data-ttu-id="5642e-149">Unzip the downloaded files to the same directory on your local machine.</span><span class="sxs-lookup"><span data-stu-id="5642e-149">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="5642e-150">Make a note of the folder where the uncompressed files reside.</span><span class="sxs-lookup"><span data-stu-id="5642e-150">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="5642e-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span><span class="sxs-lookup"><span data-stu-id="5642e-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <a name="upload"></a><span data-ttu-id="5642e-152">Upload the data to the default container of Azure HDInsight Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="5642e-152">Upload the data to the default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-153">This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5642e-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span><span class="sxs-lookup"><span data-stu-id="5642e-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="5642e-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span><span class="sxs-lookup"><span data-stu-id="5642e-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span></span>  
* <span data-ttu-id="5642e-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="5642e-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="5642e-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span></span> <span data-ttu-id="5642e-158">Note that the name of the default container is usually the same name as the cluster itself.</span><span class="sxs-lookup"><span data-stu-id="5642e-158">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="5642e-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span><span class="sxs-lookup"><span data-stu-id="5642e-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="5642e-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span><span class="sxs-lookup"><span data-stu-id="5642e-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span></span>

<span data-ttu-id="5642e-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span><span class="sxs-lookup"><span data-stu-id="5642e-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span></span>

<span data-ttu-id="5642e-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="5642e-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="5642e-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span></span>

## <a name="#download-hql-files"></a><span data-ttu-id="5642e-165">Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span><span class="sxs-lookup"><span data-stu-id="5642e-165">Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-166">This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5642e-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="5642e-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="5642e-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span><span class="sxs-lookup"><span data-stu-id="5642e-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="5642e-169">The Hive queries are stored in .hql files.</span><span class="sxs-lookup"><span data-stu-id="5642e-169">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="5642e-170">We then down sample this data to be used within Azure Machine Learning for building models.</span><span class="sxs-lookup"><span data-stu-id="5642e-170">We then down sample this data to be used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="5642e-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span><span class="sxs-lookup"><span data-stu-id="5642e-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="5642e-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span><span class="sxs-lookup"><span data-stu-id="5642e-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="5642e-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span><span class="sxs-lookup"><span data-stu-id="5642e-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <a name="#hive-db-tables"></a><span data-ttu-id="5642e-174">Create Hive database and tables partitioned by month</span><span class="sxs-lookup"><span data-stu-id="5642e-174">Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-175">This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5642e-176">We are now ready to create Hive tables for our NYC taxi dataset.</span><span class="sxs-lookup"><span data-stu-id="5642e-176">We are now ready to create Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="5642e-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span><span class="sxs-lookup"><span data-stu-id="5642e-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="5642e-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span><span class="sxs-lookup"><span data-stu-id="5642e-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="5642e-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span><span class="sxs-lookup"><span data-stu-id="5642e-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="5642e-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span><span class="sxs-lookup"><span data-stu-id="5642e-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="5642e-181">This Hive script creates two tables:</span><span class="sxs-lookup"><span data-stu-id="5642e-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="5642e-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span><span class="sxs-lookup"><span data-stu-id="5642e-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="5642e-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span><span class="sxs-lookup"><span data-stu-id="5642e-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="5642e-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="5642e-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <a name="#load-data"></a><span data-ttu-id="5642e-185">Load Data to Hive tables by partitions</span><span class="sxs-lookup"><span data-stu-id="5642e-185">Load Data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-186">This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5642e-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span><span class="sxs-lookup"><span data-stu-id="5642e-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="5642e-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span><span class="sxs-lookup"><span data-stu-id="5642e-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="5642e-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span><span class="sxs-lookup"><span data-stu-id="5642e-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="5642e-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span><span class="sxs-lookup"><span data-stu-id="5642e-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="5642e-191">But these queries could be run across the entire data.</span><span class="sxs-lookup"><span data-stu-id="5642e-191">But these queries could be run across the entire data.</span></span>

### <a name="#show-db"></a><span data-ttu-id="5642e-192">Show databases in the HDInsight Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="5642e-192">Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="5642e-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span><span class="sxs-lookup"><span data-stu-id="5642e-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <a name="#show-tables"></a><span data-ttu-id="5642e-194">Show the Hive tables in the nyctaxidb database</span><span class="sxs-lookup"><span data-stu-id="5642e-194">Show the Hive tables in the nyctaxidb database</span></span>
<span data-ttu-id="5642e-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span><span class="sxs-lookup"><span data-stu-id="5642e-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="5642e-196">We can confirm that the tables are partitioned by issuing the command below:</span><span class="sxs-lookup"><span data-stu-id="5642e-196">We can confirm that the tables are partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="5642e-197">The expected output is shown below:</span><span class="sxs-lookup"><span data-stu-id="5642e-197">The expected output is shown below:</span></span>

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

<span data-ttu-id="5642e-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span><span class="sxs-lookup"><span data-stu-id="5642e-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="5642e-199">The expected output is shown below:</span><span class="sxs-lookup"><span data-stu-id="5642e-199">The expected output is shown below:</span></span>

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

## <a name="#explore-hive"></a><span data-ttu-id="5642e-200">Data exploration and feature engineering in Hive</span><span class="sxs-lookup"><span data-stu-id="5642e-200">Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-201">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span><span class="sxs-lookup"><span data-stu-id="5642e-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="5642e-203">Here are examples of such tasks that we walk you through in this section:</span><span class="sxs-lookup"><span data-stu-id="5642e-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="5642e-204">View the top 10 records in both tables.</span><span class="sxs-lookup"><span data-stu-id="5642e-204">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="5642e-205">Explore data distributions of a few fields in varying time windows.</span><span class="sxs-lookup"><span data-stu-id="5642e-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="5642e-206">Investigate data quality of the longitude and latitude fields.</span><span class="sxs-lookup"><span data-stu-id="5642e-206">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="5642e-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="5642e-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="5642e-208">Generate features by computing the direct trip distances.</span><span class="sxs-lookup"><span data-stu-id="5642e-208">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="5642e-209">Exploration: View the top 10 records in table trip</span><span class="sxs-lookup"><span data-stu-id="5642e-209">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-210">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-211">To see what the data looks like, we examine 10 records from each table.</span><span class="sxs-lookup"><span data-stu-id="5642e-211">To see what the data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="5642e-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span><span class="sxs-lookup"><span data-stu-id="5642e-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span></span>

<span data-ttu-id="5642e-213">To get the top 10 records in the table "trip" from the first month:</span><span class="sxs-lookup"><span data-stu-id="5642e-213">To get the top 10 records in the table "trip" from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="5642e-214">To get the top 10 records in the table "fare" from the first month:</span><span class="sxs-lookup"><span data-stu-id="5642e-214">To get the top 10 records in the table "fare" from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="5642e-215">It is often useful to save the records to a file for convenient viewing.</span><span class="sxs-lookup"><span data-stu-id="5642e-215">It is often useful to save the records to a file for convenient viewing.</span></span> <span data-ttu-id="5642e-216">A small change to the above query accomplishes this:</span><span class="sxs-lookup"><span data-stu-id="5642e-216">A small change to the above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="5642e-217">Exploration: View the number of records in each of the 12 partitions</span><span class="sxs-lookup"><span data-stu-id="5642e-217">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-218">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-219">Of interest is the how the number of trips varies during the calendar year.</span><span class="sxs-lookup"><span data-stu-id="5642e-219">Of interest is the how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="5642e-220">Grouping by month allows us to see what this distribution of trips looks like.</span><span class="sxs-lookup"><span data-stu-id="5642e-220">Grouping by month allows us to see what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="5642e-221">This gives us the output :</span><span class="sxs-lookup"><span data-stu-id="5642e-221">This gives us the output :</span></span>

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

<span data-ttu-id="5642e-222">Here, the first column is the month and the second is the number of trips for that month.</span><span class="sxs-lookup"><span data-stu-id="5642e-222">Here, the first column is the month and the second is the number of trips for that month.</span></span>

<span data-ttu-id="5642e-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span><span class="sxs-lookup"><span data-stu-id="5642e-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="5642e-224">This yields:</span><span class="sxs-lookup"><span data-stu-id="5642e-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="5642e-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span><span class="sxs-lookup"><span data-stu-id="5642e-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="5642e-226">This gives us the output:</span><span class="sxs-lookup"><span data-stu-id="5642e-226">This gives us the output:</span></span>

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

<span data-ttu-id="5642e-227">Note that the exact same number of trips per month is returned for both data sets.</span><span class="sxs-lookup"><span data-stu-id="5642e-227">Note that the exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="5642e-228">This provides the first validation that the data has been loaded correctly.</span><span class="sxs-lookup"><span data-stu-id="5642e-228">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="5642e-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span><span class="sxs-lookup"><span data-stu-id="5642e-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="5642e-230">This yields :</span><span class="sxs-lookup"><span data-stu-id="5642e-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="5642e-231">The total number of records in both tables is also the same.</span><span class="sxs-lookup"><span data-stu-id="5642e-231">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="5642e-232">This provides a second validation that the data has been loaded correctly.</span><span class="sxs-lookup"><span data-stu-id="5642e-232">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="5642e-233">Exploration: Trip distribution by medallion</span><span class="sxs-lookup"><span data-stu-id="5642e-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-234">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span><span class="sxs-lookup"><span data-stu-id="5642e-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="5642e-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span><span class="sxs-lookup"><span data-stu-id="5642e-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="5642e-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span><span class="sxs-lookup"><span data-stu-id="5642e-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="5642e-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span><span class="sxs-lookup"><span data-stu-id="5642e-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="5642e-239">The medallion in the NYC taxi data set identifies a unique cab.</span><span class="sxs-lookup"><span data-stu-id="5642e-239">The medallion in the NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="5642e-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span><span class="sxs-lookup"><span data-stu-id="5642e-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="5642e-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="5642e-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="5642e-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span><span class="sxs-lookup"><span data-stu-id="5642e-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="5642e-243">From the Hive directory prompt, issue the command below :</span><span class="sxs-lookup"><span data-stu-id="5642e-243">From the Hive directory prompt, issue the command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="5642e-244">Exploration: Trip distribution by medallion and hack_license</span><span class="sxs-lookup"><span data-stu-id="5642e-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-245">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span><span class="sxs-lookup"><span data-stu-id="5642e-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="5642e-247">This section provide an example of how to do this for cabs and drivers.</span><span class="sxs-lookup"><span data-stu-id="5642e-247">This section provide an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="5642e-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span><span class="sxs-lookup"><span data-stu-id="5642e-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="5642e-249">Below are its contents.</span><span class="sxs-lookup"><span data-stu-id="5642e-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="5642e-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span><span class="sxs-lookup"><span data-stu-id="5642e-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="5642e-251">From the Hive directory prompt, run :</span><span class="sxs-lookup"><span data-stu-id="5642e-251">From the Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="5642e-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="5642e-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="5642e-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span><span class="sxs-lookup"><span data-stu-id="5642e-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-254">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span><span class="sxs-lookup"><span data-stu-id="5642e-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="5642e-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span><span class="sxs-lookup"><span data-stu-id="5642e-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="5642e-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span><span class="sxs-lookup"><span data-stu-id="5642e-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="5642e-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span><span class="sxs-lookup"><span data-stu-id="5642e-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="5642e-259">From the Hive directory prompt, run :</span><span class="sxs-lookup"><span data-stu-id="5642e-259">From the Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="5642e-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span><span class="sxs-lookup"><span data-stu-id="5642e-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="5642e-261">This is useful because it makes the screen print of the Hive query output more readable.</span><span class="sxs-lookup"><span data-stu-id="5642e-261">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="5642e-262">Exploration: Binary class distributions of trip tips</span><span class="sxs-lookup"><span data-stu-id="5642e-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-263">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span><span class="sxs-lookup"><span data-stu-id="5642e-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="5642e-265">This distribution of tips is binary:</span><span class="sxs-lookup"><span data-stu-id="5642e-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="5642e-266">tip given(Class 1, tip\_amount > $0)</span><span class="sxs-lookup"><span data-stu-id="5642e-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="5642e-267">no tip (Class 0, tip\_amount = $0).</span><span class="sxs-lookup"><span data-stu-id="5642e-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="5642e-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span><span class="sxs-lookup"><span data-stu-id="5642e-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="5642e-269">From the Hive directory prompt, run:</span><span class="sxs-lookup"><span data-stu-id="5642e-269">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="5642e-270">Exploration: Class distributions in the multiclass setting</span><span class="sxs-lookup"><span data-stu-id="5642e-270">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-271">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span><span class="sxs-lookup"><span data-stu-id="5642e-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span></span> <span data-ttu-id="5642e-273">We can use bins to define tip ranges in the query.</span><span class="sxs-lookup"><span data-stu-id="5642e-273">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="5642e-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span><span class="sxs-lookup"><span data-stu-id="5642e-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="5642e-275">Below are its contents.</span><span class="sxs-lookup"><span data-stu-id="5642e-275">Below are its contents.</span></span>

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

<span data-ttu-id="5642e-276">Run the following command from Hadoop Command Line console:</span><span class="sxs-lookup"><span data-stu-id="5642e-276">Run the following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="5642e-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span><span class="sxs-lookup"><span data-stu-id="5642e-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-278">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span><span class="sxs-lookup"><span data-stu-id="5642e-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span></span> <span data-ttu-id="5642e-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span><span class="sxs-lookup"><span data-stu-id="5642e-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="5642e-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span><span class="sxs-lookup"><span data-stu-id="5642e-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="5642e-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span><span class="sxs-lookup"><span data-stu-id="5642e-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="5642e-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span><span class="sxs-lookup"><span data-stu-id="5642e-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="5642e-284">In this case, we write our results to a directory called "queryoutputdir".</span><span class="sxs-lookup"><span data-stu-id="5642e-284">In this case, we write our results to a directory called "queryoutputdir".</span></span> <span data-ttu-id="5642e-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span><span class="sxs-lookup"><span data-stu-id="5642e-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="5642e-286">From the Hive directory prompt, run:</span><span class="sxs-lookup"><span data-stu-id="5642e-286">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="5642e-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="5642e-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span><span class="sxs-lookup"><span data-stu-id="5642e-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="5642e-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span><span class="sxs-lookup"><span data-stu-id="5642e-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="5642e-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span><span class="sxs-lookup"><span data-stu-id="5642e-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="5642e-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="5642e-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span></span>

## <a name="#downsample"></a><span data-ttu-id="5642e-292">Down sample data and build models in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5642e-292">Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="5642e-293">This is typically a **Data Scientist** task.</span><span class="sxs-lookup"><span data-stu-id="5642e-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5642e-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5642e-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="5642e-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5642e-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="5642e-296">Down sampling the data</span><span class="sxs-lookup"><span data-stu-id="5642e-296">Down sampling the data</span></span>
<span data-ttu-id="5642e-297">There are two steps in this procedure.</span><span class="sxs-lookup"><span data-stu-id="5642e-297">There are two steps in this procedure.</span></span> <span data-ttu-id="5642e-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span><span class="sxs-lookup"><span data-stu-id="5642e-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="5642e-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="5642e-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="5642e-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span><span class="sxs-lookup"><span data-stu-id="5642e-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span></span> <span data-ttu-id="5642e-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span><span class="sxs-lookup"><span data-stu-id="5642e-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span></span>

<span data-ttu-id="5642e-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span><span class="sxs-lookup"><span data-stu-id="5642e-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="5642e-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span><span class="sxs-lookup"><span data-stu-id="5642e-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="5642e-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5642e-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span></span> <span data-ttu-id="5642e-305">Only about 1% of the original dataset is imported into the Studio.</span><span class="sxs-lookup"><span data-stu-id="5642e-305">Only about 1% of the original dataset is imported into the Studio.</span></span>

<span data-ttu-id="5642e-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5642e-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

<span data-ttu-id="5642e-307">To run this query, from the Hive directory prompt :</span><span class="sxs-lookup"><span data-stu-id="5642e-307">To run this query, from the Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="5642e-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5642e-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="5642e-309">Furthermore, we may use this dataset for building Machine Learning models.</span><span class="sxs-lookup"><span data-stu-id="5642e-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-azure-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="5642e-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span><span class="sxs-lookup"><span data-stu-id="5642e-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span></span>
<span data-ttu-id="5642e-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span><span class="sxs-lookup"><span data-stu-id="5642e-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="5642e-312">Some details on the [Import Data][import-data] module and the parameters to input :</span><span class="sxs-lookup"><span data-stu-id="5642e-312">Some details on the [Import Data][import-data] module and the parameters to input :</span></span>

<span data-ttu-id="5642e-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="5642e-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="5642e-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span><span class="sxs-lookup"><span data-stu-id="5642e-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span></span>

<span data-ttu-id="5642e-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span><span class="sxs-lookup"><span data-stu-id="5642e-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span></span>

<span data-ttu-id="5642e-316">**Location of output data** : This is chosen to be Azure.</span><span class="sxs-lookup"><span data-stu-id="5642e-316">**Location of output data** : This is chosen to be Azure.</span></span>

<span data-ttu-id="5642e-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="5642e-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="5642e-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span><span class="sxs-lookup"><span data-stu-id="5642e-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="5642e-319">For a cluster called "abc123", this is just abc123.</span><span class="sxs-lookup"><span data-stu-id="5642e-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5642e-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span><span class="sxs-lookup"><span data-stu-id="5642e-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="5642e-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span><span class="sxs-lookup"><span data-stu-id="5642e-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="5642e-322">From the Hive directory prompt, issue the command :</span><span class="sxs-lookup"><span data-stu-id="5642e-322">From the Hive directory prompt, issue the command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="5642e-323">If the table is an internal table and it is populated, its contents must show here.</span><span class="sxs-lookup"><span data-stu-id="5642e-323">If the table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="5642e-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="5642e-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span></span> <span data-ttu-id="5642e-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span><span class="sxs-lookup"><span data-stu-id="5642e-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="5642e-326">If the table and its contents show up, this confirms that it is an internal table.</span><span class="sxs-lookup"><span data-stu-id="5642e-326">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="5642e-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span><span class="sxs-lookup"><span data-stu-id="5642e-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span></span>

![Hive query for Import Data module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="5642e-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT \* FROM nyctaxidb.nyctaxi\_downsampled\_data".</span><span class="sxs-lookup"><span data-stu-id="5642e-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT \* FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="5642e-330">The dataset may now be used as the starting point for building Machine Learning models.</span><span class="sxs-lookup"><span data-stu-id="5642e-330">The dataset may now be used as the starting point for building Machine Learning models.</span></span>

### <a name="mlmodel"></a><span data-ttu-id="5642e-331">Build models in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5642e-331">Build models in Azure Machine Learning</span></span>
<span data-ttu-id="5642e-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="5642e-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="5642e-333">The data is ready for us to use in addressing the prediction problems identified above:</span><span class="sxs-lookup"><span data-stu-id="5642e-333">The data is ready for us to use in addressing the prediction problems identified above:</span></span>

<span data-ttu-id="5642e-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="5642e-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="5642e-335">**Learner used:** Two-class logistic regression</span><span class="sxs-lookup"><span data-stu-id="5642e-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="5642e-336">a.</span><span class="sxs-lookup"><span data-stu-id="5642e-336">a.</span></span> <span data-ttu-id="5642e-337">For this problem, our target (or class) label is "tipped".</span><span class="sxs-lookup"><span data-stu-id="5642e-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="5642e-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span><span class="sxs-lookup"><span data-stu-id="5642e-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="5642e-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span><span class="sxs-lookup"><span data-stu-id="5642e-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="5642e-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="5642e-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5642e-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span><span class="sxs-lookup"><span data-stu-id="5642e-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span></span>

![Experiment snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="5642e-343">b.</span><span class="sxs-lookup"><span data-stu-id="5642e-343">b.</span></span> <span data-ttu-id="5642e-344">For this experiment, our target label distributions were roughly 1:1.</span><span class="sxs-lookup"><span data-stu-id="5642e-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="5642e-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span><span class="sxs-lookup"><span data-stu-id="5642e-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span></span>

![Distribution of tip class labels](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="5642e-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span><span class="sxs-lookup"><span data-stu-id="5642e-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span></span>

![AUC value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="5642e-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span><span class="sxs-lookup"><span data-stu-id="5642e-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span></span>

<span data-ttu-id="5642e-350">**Learner used:** Multiclass logistic regression</span><span class="sxs-lookup"><span data-stu-id="5642e-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="5642e-351">a.</span><span class="sxs-lookup"><span data-stu-id="5642e-351">a.</span></span> <span data-ttu-id="5642e-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="5642e-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="5642e-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span><span class="sxs-lookup"><span data-stu-id="5642e-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="5642e-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span><span class="sxs-lookup"><span data-stu-id="5642e-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="5642e-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="5642e-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5642e-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span><span class="sxs-lookup"><span data-stu-id="5642e-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Experiment snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="5642e-358">We now show what our actual test class distribution looks like.</span><span class="sxs-lookup"><span data-stu-id="5642e-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="5642e-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span><span class="sxs-lookup"><span data-stu-id="5642e-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span></span>

![Test class distribution](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="5642e-361">b.</span><span class="sxs-lookup"><span data-stu-id="5642e-361">b.</span></span> <span data-ttu-id="5642e-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span><span class="sxs-lookup"><span data-stu-id="5642e-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span></span> <span data-ttu-id="5642e-363">This is shown below.</span><span class="sxs-lookup"><span data-stu-id="5642e-363">This is shown below.</span></span>

![Confusion matrix](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="5642e-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span><span class="sxs-lookup"><span data-stu-id="5642e-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

<span data-ttu-id="5642e-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span><span class="sxs-lookup"><span data-stu-id="5642e-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span></span>

<span data-ttu-id="5642e-367">**Learner used:** Boosted decision tree</span><span class="sxs-lookup"><span data-stu-id="5642e-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="5642e-368">a.</span><span class="sxs-lookup"><span data-stu-id="5642e-368">a.</span></span> <span data-ttu-id="5642e-369">For this problem, our target (or class) label is "tip\_amount".</span><span class="sxs-lookup"><span data-stu-id="5642e-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="5642e-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span><span class="sxs-lookup"><span data-stu-id="5642e-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="5642e-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="5642e-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5642e-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span><span class="sxs-lookup"><span data-stu-id="5642e-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span></span>

![Experiment snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="5642e-374">b.</span><span class="sxs-lookup"><span data-stu-id="5642e-374">b.</span></span> <span data-ttu-id="5642e-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span><span class="sxs-lookup"><span data-stu-id="5642e-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span></span> <span data-ttu-id="5642e-376">We show these below.</span><span class="sxs-lookup"><span data-stu-id="5642e-376">We show these below.</span></span>

![Prediction statistics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="5642e-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span><span class="sxs-lookup"><span data-stu-id="5642e-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5642e-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="5642e-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="5642e-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="5642e-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="5642e-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5642e-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="5642e-382">License Information</span><span class="sxs-lookup"><span data-stu-id="5642e-382">License Information</span></span>
<span data-ttu-id="5642e-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span><span class="sxs-lookup"><span data-stu-id="5642e-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="5642e-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span><span class="sxs-lookup"><span data-stu-id="5642e-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="5642e-385">References</span><span class="sxs-lookup"><span data-stu-id="5642e-385">References</span></span>
<span data-ttu-id="5642e-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="5642e-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="5642e-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="5642e-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="5642e-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="5642e-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/









