---
title: 'Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough | Microsoft Docs'
description: How to use Azure Data Lake to do data exploration and binary classification tasks on a dataset.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 62ca89ffe7507c2dc0a0f1a86750fb2bb996a5bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868829"
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="e983a-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span><span class="sxs-lookup"><span data-stu-id="e983a-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="e983a-104">This walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi trip and fare dataset to predict whether or not a tip is paid by a fare.</span><span class="sxs-lookup"><span data-stu-id="e983a-104">This walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi trip and fare dataset to predict whether or not a tip is paid by a fare.</span></span> <span data-ttu-id="e983a-105">It walks you through the steps of the [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition to model training, and then to the deployment of a web service that publishes the model.</span><span class="sxs-lookup"><span data-stu-id="e983a-105">It walks you through the steps of the [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition to model training, and then to the deployment of a web service that publishes the model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="e983a-106">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e983a-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="e983a-107">The [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all the capabilities required to make it easy for data scientists to store data of any size, shape and speed, and to conduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span><span class="sxs-lookup"><span data-stu-id="e983a-107">The [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all the capabilities required to make it easy for data scientists to store data of any size, shape and speed, and to conduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="e983a-108">You pay on a per-job basis, only when data is actually being processed.</span><span class="sxs-lookup"><span data-stu-id="e983a-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="e983a-109">Azure Data Lake Analytics includes U-SQL, a language that blends the declarative nature of SQL with the expressive power of C# to provide scalable distributed query capability.</span><span class="sxs-lookup"><span data-stu-id="e983a-109">Azure Data Lake Analytics includes U-SQL, a language that blends the declarative nature of SQL with the expressive power of C# to provide scalable distributed query capability.</span></span> <span data-ttu-id="e983a-110">It enables you to process unstructured data by applying schema on read, insert custom logic and user-defined functions (UDFs), and includes extensibility to enable fine grained control over how to execute at scale.</span><span class="sxs-lookup"><span data-stu-id="e983a-110">It enables you to process unstructured data by applying schema on read, insert custom logic and user-defined functions (UDFs), and includes extensibility to enable fine grained control over how to execute at scale.</span></span> <span data-ttu-id="e983a-111">To learn more about the design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="e983a-111">To learn more about the design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="e983a-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e983a-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="e983a-113">This gives you a complete cloud big data and advanced analytics platform.</span><span class="sxs-lookup"><span data-stu-id="e983a-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="e983a-114">This walkthrough begins by describing how to install the prerequisites and resources that are needed to complete data science process tasks.</span><span class="sxs-lookup"><span data-stu-id="e983a-114">This walkthrough begins by describing how to install the prerequisites and resources that are needed to complete data science process tasks.</span></span> <span data-ttu-id="e983a-115">Then it outlines the data processing steps using U-SQL and concludes by showing how to use Python and Hive with Azure Machine Learning Studio to build and deploy the predictive models.</span><span class="sxs-lookup"><span data-stu-id="e983a-115">Then it outlines the data processing steps using U-SQL and concludes by showing how to use Python and Hive with Azure Machine Learning Studio to build and deploy the predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="e983a-116">U-SQL and Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e983a-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="e983a-117">This walkthrough recommends using Visual Studio to edit U-SQL scripts to process the dataset.</span><span class="sxs-lookup"><span data-stu-id="e983a-117">This walkthrough recommends using Visual Studio to edit U-SQL scripts to process the dataset.</span></span> <span data-ttu-id="e983a-118">The U-SQL scripts are described here and provided in a separate file.</span><span class="sxs-lookup"><span data-stu-id="e983a-118">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="e983a-119">The process includes ingesting, exploring, and sampling the data.</span><span class="sxs-lookup"><span data-stu-id="e983a-119">The process includes ingesting, exploring, and sampling the data.</span></span> <span data-ttu-id="e983a-120">It also shows how to run a U-SQL scripted job from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e983a-120">It also shows how to run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="e983a-121">Hive tables are created for the data in an associated HDInsight cluster to facilitate the building and deployment of a binary classification model in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e983a-121">Hive tables are created for the data in an associated HDInsight cluster to facilitate the building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="e983a-122">Python</span><span class="sxs-lookup"><span data-stu-id="e983a-122">Python</span></span>
<span data-ttu-id="e983a-123">This walkthrough also contains a section that shows how to build and deploy a predictive model using Python with Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e983a-123">This walkthrough also contains a section that shows how to build and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span> <span data-ttu-id="e983a-124">It provides a Jupyter notebook with the Python scripts for the steps in this process.</span><span class="sxs-lookup"><span data-stu-id="e983a-124">It provides a Jupyter notebook with the Python scripts for the steps in this process.</span></span> <span data-ttu-id="e983a-125">The notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition to the binary classification model outlined here.</span><span class="sxs-lookup"><span data-stu-id="e983a-125">The notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition to the binary classification model outlined here.</span></span> <span data-ttu-id="e983a-126">The regression task is to predict the amount of the tip based on other tip features.</span><span class="sxs-lookup"><span data-stu-id="e983a-126">The regression task is to predict the amount of the tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="e983a-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e983a-127">Azure Machine Learning</span></span>
<span data-ttu-id="e983a-128">Azure Machine Learning Studio is used to build and deploy the predictive models.</span><span class="sxs-lookup"><span data-stu-id="e983a-128">Azure Machine Learning Studio is used to build and deploy the predictive models.</span></span> <span data-ttu-id="e983a-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span><span class="sxs-lookup"><span data-stu-id="e983a-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="e983a-130">Scripts</span><span class="sxs-lookup"><span data-stu-id="e983a-130">Scripts</span></span>
<span data-ttu-id="e983a-131">Only the principal steps are outlined in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="e983a-131">Only the principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="e983a-132">You can download the full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="e983a-132">You can download the full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e983a-133">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e983a-133">Prerequisites</span></span>
<span data-ttu-id="e983a-134">Before you begin these topics, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="e983a-134">Before you begin these topics, you must have the following:</span></span>

* <span data-ttu-id="e983a-135">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e983a-135">An Azure subscription.</span></span> <span data-ttu-id="e983a-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e983a-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e983a-137">[Recommended] Visual Studio 2013 or later.</span><span class="sxs-lookup"><span data-stu-id="e983a-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="e983a-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="e983a-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="e983a-139">Instead of Visual Studio, you can also use the Azure portal to submit Azure Data Lake queries.</span><span class="sxs-lookup"><span data-stu-id="e983a-139">Instead of Visual Studio, you can also use the Azure portal to submit Azure Data Lake queries.</span></span> <span data-ttu-id="e983a-140">Instructions are provided on how to do so both with Visual Studio and on the portal in the section titled **Process data with U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="e983a-140">Instructions are provided on how to do so both with Visual Studio and on the portal in the section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="e983a-141">Prepare data science environment for Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e983a-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="e983a-142">To prepare the data science environment for this walkthrough, create the following resources:</span><span class="sxs-lookup"><span data-stu-id="e983a-142">To prepare the data science environment for this walkthrough, create the following resources:</span></span>

* <span data-ttu-id="e983a-143">Azure Data Lake Store (ADLS)</span><span class="sxs-lookup"><span data-stu-id="e983a-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="e983a-144">Azure Data Lake Analytics (ADLA)</span><span class="sxs-lookup"><span data-stu-id="e983a-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="e983a-145">Azure Blob storage account</span><span class="sxs-lookup"><span data-stu-id="e983a-145">Azure Blob storage account</span></span>
* <span data-ttu-id="e983a-146">Azure Machine Learning Studio account</span><span class="sxs-lookup"><span data-stu-id="e983a-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="e983a-147">Azure Data Lake Tools for Visual Studio (Recommended)</span><span class="sxs-lookup"><span data-stu-id="e983a-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="e983a-148">This section provides instructions on how to create each of these resources.</span><span class="sxs-lookup"><span data-stu-id="e983a-148">This section provides instructions on how to create each of these resources.</span></span> <span data-ttu-id="e983a-149">If you choose to use Hive tables with Azure Machine Learning, instead of Python, to build a model, you also need to provision an HDInsight (Hadoop) cluster.</span><span class="sxs-lookup"><span data-stu-id="e983a-149">If you choose to use Hive tables with Azure Machine Learning, instead of Python, to build a model, you also need to provision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="e983a-150">This alternative procedure in described in the Option 2 section.</span><span class="sxs-lookup"><span data-stu-id="e983a-150">This alternative procedure in described in the Option 2 section.</span></span>


> [!NOTE]
> <span data-ttu-id="e983a-151">The **Azure Data Lake Store** can be created either separately or when you create the **Azure Data Lake Analytics** as the default storage.</span><span class="sxs-lookup"><span data-stu-id="e983a-151">The **Azure Data Lake Store** can be created either separately or when you create the **Azure Data Lake Analytics** as the default storage.</span></span> <span data-ttu-id="e983a-152">Instructions are referenced for creating each of these resources separately, but the Data Lake storage account need not be created separately.</span><span class="sxs-lookup"><span data-stu-id="e983a-152">Instructions are referenced for creating each of these resources separately, but the Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="e983a-153">Create an Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e983a-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="e983a-154">Create an ADLS from the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e983a-154">Create an ADLS from the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="e983a-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e983a-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="e983a-156">Be sure to set up the Cluster AAD Identity in the **DataSource** blade of the **Optional Configuration** blade described there.</span><span class="sxs-lookup"><span data-stu-id="e983a-156">Be sure to set up the Cluster AAD Identity in the **DataSource** blade of the **Optional Configuration** blade described there.</span></span> 

 ![3](./media/data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="e983a-158">Create an Azure Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="e983a-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="e983a-159">Create an ADLA account from the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e983a-159">Create an ADLA account from the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="e983a-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure portal](../../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e983a-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure portal](../../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="e983a-162">Create an Azure Blob storage account</span><span class="sxs-lookup"><span data-stu-id="e983a-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="e983a-163">Create an Azure Blob storage account from the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e983a-163">Create an Azure Blob storage account from the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="e983a-164">For details, see the Create a storage account section in [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e983a-164">For details, see the Create a storage account section in [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="e983a-166">Set up an Azure Machine Learning Studio account</span><span class="sxs-lookup"><span data-stu-id="e983a-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="e983a-167">Sign up/into Azure Machine Learning Studio from the [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span><span class="sxs-lookup"><span data-stu-id="e983a-167">Sign up/into Azure Machine Learning Studio from the [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="e983a-168">Click on the **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span><span class="sxs-lookup"><span data-stu-id="e983a-168">Click on the **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="e983a-169">Now your are ready to create experiments in Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="e983a-169">Now your are ready to create experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="e983a-170">Install Azure Data Lake Tools [Recommended]</span><span class="sxs-lookup"><span data-stu-id="e983a-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="e983a-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="e983a-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="e983a-173">After the installation finishes successfully, open up Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e983a-173">After the installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="e983a-174">You should see the Data Lake tab the menu at the top.</span><span class="sxs-lookup"><span data-stu-id="e983a-174">You should see the Data Lake tab the menu at the top.</span></span> <span data-ttu-id="e983a-175">Your Azure resources should appear in the left panel when you sign into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="e983a-175">Your Azure resources should appear in the left panel when you sign into your Azure account.</span></span>

 ![7](./media/data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="the-nyc-taxi-trips-dataset"></a><span data-ttu-id="e983a-177">The NYC Taxi Trips dataset</span><span class="sxs-lookup"><span data-stu-id="e983a-177">The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="e983a-178">The data set used here is a publicly available dataset -- the [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="e983a-178">The data set used here is a publicly available dataset -- the [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="e983a-179">The NYC Taxi Trip data consists of about 20 GB of compressed CSV files (~48 GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span><span class="sxs-lookup"><span data-stu-id="e983a-179">The NYC Taxi Trip data consists of about 20 GB of compressed CSV files (~48 GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="e983a-180">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique ID) number.</span><span class="sxs-lookup"><span data-stu-id="e983a-180">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique ID) number.</span></span> <span data-ttu-id="e983a-181">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span><span class="sxs-lookup"><span data-stu-id="e983a-181">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

<span data-ttu-id="e983a-182">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span><span class="sxs-lookup"><span data-stu-id="e983a-182">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e983a-183">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="e983a-183">Here are a few sample records:</span></span>

       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868



<span data-ttu-id="e983a-184">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span><span class="sxs-lookup"><span data-stu-id="e983a-184">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="e983a-185">Here are a few sample records:</span><span class="sxs-lookup"><span data-stu-id="e983a-185">Here are a few sample records:</span></span>

       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e983a-186">The unique key to join trip\_data and trip\_fare is composed of the following three fields: medallion, hack\_license and pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="e983a-186">The unique key to join trip\_data and trip\_fare is composed of the following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="e983a-187">The raw CSV files can be accessed from a public Azure storage blob.</span><span class="sxs-lookup"><span data-stu-id="e983a-187">The raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="e983a-188">The U-SQL script for this join is in the [Join trip and fare tables](#join) section.</span><span class="sxs-lookup"><span data-stu-id="e983a-188">The U-SQL script for this join is in the [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="e983a-189">Process data with U-SQL</span><span class="sxs-lookup"><span data-stu-id="e983a-189">Process data with U-SQL</span></span>
<span data-ttu-id="e983a-190">The data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling the data.</span><span class="sxs-lookup"><span data-stu-id="e983a-190">The data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling the data.</span></span> <span data-ttu-id="e983a-191">How to join trip and fare tables is also shown.</span><span class="sxs-lookup"><span data-stu-id="e983a-191">How to join trip and fare tables is also shown.</span></span> <span data-ttu-id="e983a-192">The final section shows run a U-SQL scripted job from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e983a-192">The final section shows run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="e983a-193">Here are links to each subsection:</span><span class="sxs-lookup"><span data-stu-id="e983a-193">Here are links to each subsection:</span></span>

* [<span data-ttu-id="e983a-194">Data ingestion: read in data from public blob</span><span class="sxs-lookup"><span data-stu-id="e983a-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="e983a-195">Data quality checks</span><span class="sxs-lookup"><span data-stu-id="e983a-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="e983a-196">Data exploration</span><span class="sxs-lookup"><span data-stu-id="e983a-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="e983a-197">Join trip and fare tables</span><span class="sxs-lookup"><span data-stu-id="e983a-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="e983a-198">Data sampling</span><span class="sxs-lookup"><span data-stu-id="e983a-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="e983a-199">Run U-SQL jobs</span><span class="sxs-lookup"><span data-stu-id="e983a-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="e983a-200">The U-SQL scripts are described here and provided in a separate file.</span><span class="sxs-lookup"><span data-stu-id="e983a-200">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="e983a-201">You can download the full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="e983a-201">You can download the full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="e983a-202">To execute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it to a folder.</span><span class="sxs-lookup"><span data-stu-id="e983a-202">To execute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it to a folder.</span></span>

![8](./media/data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="e983a-204">It is possible to use the Azure Portal to execute U-SQL instead of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e983a-204">It is possible to use the Azure Portal to execute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="e983a-205">You can navigate to the Azure Data Lake Analytics resource on the portal and submit queries directly as illustrated in the following figure:</span><span class="sxs-lookup"><span data-stu-id="e983a-205">You can navigate to the Azure Data Lake Analytics resource on the portal and submit queries directly as illustrated in the following figure:</span></span>
> 
> 

![9](./media/data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a><span data-ttu-id="e983a-207">Data Ingestion: Read in data from public blob</span><span class="sxs-lookup"><span data-stu-id="e983a-207">Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="e983a-208">The location of the data in the Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="e983a-208">The location of the data in the Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="e983a-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in the wasb address.</span><span class="sxs-lookup"><span data-stu-id="e983a-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in the wasb address.</span></span> <span data-ttu-id="e983a-210">Since the file names are in same format, it is possible to use **trip\_data_{\*\}.csv** to read in all 12 trip files.</span><span class="sxs-lookup"><span data-stu-id="e983a-210">Since the file names are in same format, it is possible to use **trip\_data_{\*\}.csv** to read in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="e983a-211">Since there are headers in the first row, you need to remove the headers and change column types into appropriate ones.</span><span class="sxs-lookup"><span data-stu-id="e983a-211">Since there are headers in the first row, you need to remove the headers and change column types into appropriate ones.</span></span> <span data-ttu-id="e983a-212">You can either save the processed data to Azure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or to Azure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span><span class="sxs-lookup"><span data-stu-id="e983a-212">You can either save the processed data to Azure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or to Azure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data to ADL
    OUTPUT @trip   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data to blob
    OUTPUT @trip   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="e983a-213">Similarly you can read in the fare data sets.</span><span class="sxs-lookup"><span data-stu-id="e983a-213">Similarly you can read in the fare data sets.</span></span> <span data-ttu-id="e983a-214">Right-click Azure Data Lake Store, you can choose to look at your data in **Azure portal --> Data Explorer** or **File Explorer** within Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e983a-214">Right-click Azure Data Lake Store, you can choose to look at your data in **Azure portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a><span data-ttu-id="e983a-217">Data quality checks</span><span class="sxs-lookup"><span data-stu-id="e983a-217">Data quality checks</span></span>
<span data-ttu-id="e983a-218">After trip and fare tables have been read in, data quality checks can be done in the following way.</span><span class="sxs-lookup"><span data-stu-id="e983a-218">After trip and fare tables have been read in, data quality checks can be done in the following way.</span></span> <span data-ttu-id="e983a-219">The resulting CSV files can be output to Azure Blob storage or Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e983a-219">The resulting CSV files can be output to Azure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="e983a-220">Find the number of medallions and unique number of medallions:</span><span class="sxs-lookup"><span data-stu-id="e983a-220">Find the number of medallions and unique number of medallions:</span></span>

    ///check the number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e983a-221">Find those medallions that had more than 100 trips:</span><span class="sxs-lookup"><span data-stu-id="e983a-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e983a-222">Find those invalid records in terms of pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="e983a-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e983a-223">Find missing values for some variables:</span><span class="sxs-lookup"><span data-stu-id="e983a-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a><span data-ttu-id="e983a-224">Data exploration</span><span class="sxs-lookup"><span data-stu-id="e983a-224">Data exploration</span></span>
<span data-ttu-id="e983a-225">Do some data exploration with the following scripts to get a better understanding of the data.</span><span class="sxs-lookup"><span data-stu-id="e983a-225">Do some data exploration with the following scripts to get a better understanding of the data.</span></span>

<span data-ttu-id="e983a-226">Find the distribution of tipped and non-tipped trips:</span><span class="sxs-lookup"><span data-stu-id="e983a-226">Find the distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e983a-227">Find the distribution of tip amount with cut-off values: 0, 5, 10, and 20 dollars.</span><span class="sxs-lookup"><span data-stu-id="e983a-227">Find the distribution of tip amount with cut-off values: 0, 5, 10, and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e983a-228">Find basic statistics of trip distance:</span><span class="sxs-lookup"><span data-stu-id="e983a-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="e983a-229">Find the percentiles of trip distance:</span><span class="sxs-lookup"><span data-stu-id="e983a-229">Find the percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a><span data-ttu-id="e983a-230">Join trip and fare tables</span><span class="sxs-lookup"><span data-stu-id="e983a-230">Join trip and fare tables</span></span>
<span data-ttu-id="e983a-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span><span class="sxs-lookup"><span data-stu-id="e983a-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output to blob
    OUTPUT @model_data_full   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data to ADL
    OUTPUT @model_data_full   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="e983a-232">For each level of passenger count, calculate the number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span><span class="sxs-lookup"><span data-stu-id="e983a-232">For each level of passenger count, calculate the number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a><span data-ttu-id="e983a-233">Data sampling</span><span class="sxs-lookup"><span data-stu-id="e983a-233">Data sampling</span></span>
<span data-ttu-id="e983a-234">First, randomly select 0.1% of the data from the joined table:</span><span class="sxs-lookup"><span data-stu-id="e983a-234">First, randomly select 0.1% of the data from the joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e983a-235">Then do stratified sampling by binary variable tip_class:</span><span class="sxs-lookup"><span data-stu-id="e983a-235">Then do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output to blob
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data to ADL
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a><span data-ttu-id="e983a-236">Run U-SQL jobs</span><span class="sxs-lookup"><span data-stu-id="e983a-236">Run U-SQL jobs</span></span>
<span data-ttu-id="e983a-237">When you finish editing U-SQL scripts, you can submit them to the server using your Azure Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="e983a-237">When you finish editing U-SQL scripts, you can submit them to the server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="e983a-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span><span class="sxs-lookup"><span data-stu-id="e983a-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="e983a-240">When the job is complied successfully, the status of your job is displayed in Visual Studio for monitoring.</span><span class="sxs-lookup"><span data-stu-id="e983a-240">When the job is complied successfully, the status of your job is displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="e983a-241">After the job finishes running, you can even replay the job execution process and find out the bottleneck steps to improve your job efficiency.</span><span class="sxs-lookup"><span data-stu-id="e983a-241">After the job finishes running, you can even replay the job execution process and find out the bottleneck steps to improve your job efficiency.</span></span> <span data-ttu-id="e983a-242">You can also go to Azure portal to check the status of your U-SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="e983a-242">You can also go to Azure portal to check the status of your U-SQL jobs.</span></span>

 ![13](./media/data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="e983a-245">Now you can check the output files in either Azure Blob storage or Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e983a-245">Now you can check the output files in either Azure Blob storage or Azure portal.</span></span> <span data-ttu-id="e983a-246">Use the stratified sample data for our modeling in the next step.</span><span class="sxs-lookup"><span data-stu-id="e983a-246">Use the stratified sample data for our modeling in the next step.</span></span>

 ![15](./media/data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="e983a-249">Build and deploy models in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e983a-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="e983a-250">Two options are available for you to pull data into Azure Machine Learning to build and</span><span class="sxs-lookup"><span data-stu-id="e983a-250">Two options are available for you to pull data into Azure Machine Learning to build and</span></span> 

* <span data-ttu-id="e983a-251">In the first option, you use the sampled data that has been written to an Azure Blob (in the **Data sampling** step above) and use Python to build and deploy models from Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e983a-251">In the first option, you use the sampled data that has been written to an Azure Blob (in the **Data sampling** step above) and use Python to build and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="e983a-252">In the second option, you query the data in Azure Data Lake directly using a Hive query.</span><span class="sxs-lookup"><span data-stu-id="e983a-252">In the second option, you query the data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="e983a-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where the Hive tables point to the NY Taxi data in Azure Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="e983a-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where the Hive tables point to the NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="e983a-254">Both these options are discussed in the following sections.</span><span class="sxs-lookup"><span data-stu-id="e983a-254">Both these options are discussed in the following sections.</span></span> 

## <a name="option-1-use-python-to-build-and-deploy-machine-learning-models"></a><span data-ttu-id="e983a-255">Option 1: Use Python to build and deploy machine learning models</span><span class="sxs-lookup"><span data-stu-id="e983a-255">Option 1: Use Python to build and deploy machine learning models</span></span>
<span data-ttu-id="e983a-256">To build and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e983a-256">To build and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="e983a-257">The Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains the full code to explore, visualize data, feature engineering, modeling and deployment.</span><span class="sxs-lookup"><span data-stu-id="e983a-257">The Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains the full code to explore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="e983a-258">In this article, just the modeling and deployment are covered.</span><span class="sxs-lookup"><span data-stu-id="e983a-258">In this article, just the modeling and deployment are covered.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="e983a-259">Import Python libraries</span><span class="sxs-lookup"><span data-stu-id="e983a-259">Import Python libraries</span></span>
<span data-ttu-id="e983a-260">In order to run the sample Jupyter Notebook or the Python script file, the following Python packages are needed.</span><span class="sxs-lookup"><span data-stu-id="e983a-260">In order to run the sample Jupyter Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="e983a-261">If you are using the AzureML Notebook service, these packages have been pre-installed.</span><span class="sxs-lookup"><span data-stu-id="e983a-261">If you are using the AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-the-data-from-blob"></a><span data-ttu-id="e983a-262">Read in the data from blob</span><span class="sxs-lookup"><span data-stu-id="e983a-262">Read in the data from blob</span></span>
* <span data-ttu-id="e983a-263">Connection String</span><span class="sxs-lookup"><span data-stu-id="e983a-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="e983a-264">Read in as text</span><span class="sxs-lookup"><span data-stu-id="e983a-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds to read in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="e983a-266">Add column names and separate columns</span><span class="sxs-lookup"><span data-stu-id="e983a-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="e983a-267">Change some columns to numeric</span><span class="sxs-lookup"><span data-stu-id="e983a-267">Change some columns to numeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="e983a-268">Build machine learning models</span><span class="sxs-lookup"><span data-stu-id="e983a-268">Build machine learning models</span></span>
<span data-ttu-id="e983a-269">Here you build a binary classification model to predict whether a trip is tipped or not.</span><span class="sxs-lookup"><span data-stu-id="e983a-269">Here you build a binary classification model to predict whether a trip is tipped or not.</span></span> <span data-ttu-id="e983a-270">In the Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span><span class="sxs-lookup"><span data-stu-id="e983a-270">In the Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="e983a-271">First you need to create dummy variables that can be used in scikit-learn models</span><span class="sxs-lookup"><span data-stu-id="e983a-271">First you need to create dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="e983a-272">Create data frame for the modeling</span><span class="sxs-lookup"><span data-stu-id="e983a-272">Create data frame for the modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="e983a-273">Training and testing 60-40 split</span><span class="sxs-lookup"><span data-stu-id="e983a-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="e983a-274">Logistic Regression in training set</span><span class="sxs-lookup"><span data-stu-id="e983a-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="e983a-275">Score testing data set</span><span class="sxs-lookup"><span data-stu-id="e983a-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="e983a-276">Calculate Evaluation metrics</span><span class="sxs-lookup"><span data-stu-id="e983a-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="e983a-277">Build Web Service API and consume it in Python</span><span class="sxs-lookup"><span data-stu-id="e983a-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="e983a-278">You want to operationalize the machine learning model after it has been built.</span><span class="sxs-lookup"><span data-stu-id="e983a-278">You want to operationalize the machine learning model after it has been built.</span></span> <span data-ttu-id="e983a-279">The binary logistic model is used here as an example.</span><span class="sxs-lookup"><span data-stu-id="e983a-279">The binary logistic model is used here as an example.</span></span> <span data-ttu-id="e983a-280">Make sure the scikit-learn version in your local machine is 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="e983a-280">Make sure the scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="e983a-281">You don't have to worry about this if you use Azure ML studio service.</span><span class="sxs-lookup"><span data-stu-id="e983a-281">You don't have to worry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="e983a-282">Find your workspace credentials from Azure ML studio settings.</span><span class="sxs-lookup"><span data-stu-id="e983a-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="e983a-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span><span class="sxs-lookup"><span data-stu-id="e983a-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="e983a-285">Create Web Service</span><span class="sxs-lookup"><span data-stu-id="e983a-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="e983a-286">Get web service credentials</span><span class="sxs-lookup"><span data-stu-id="e983a-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="e983a-287">Call Web service API.</span><span class="sxs-lookup"><span data-stu-id="e983a-287">Call Web service API.</span></span> <span data-ttu-id="e983a-288">You have to wait 5-10 seconds after the previous step.</span><span class="sxs-lookup"><span data-stu-id="e983a-288">You have to wait 5-10 seconds after the previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="e983a-289">Option 2: Create and deploy models directly in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e983a-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="e983a-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used to create and deploy models.</span><span class="sxs-lookup"><span data-stu-id="e983a-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used to create and deploy models.</span></span> <span data-ttu-id="e983a-291">This approach uses a Hive table that points at the Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e983a-291">This approach uses a Hive table that points at the Azure Data Lake Store.</span></span> <span data-ttu-id="e983a-292">This requires that a separate Azure HDInsight cluster be provisioned, on which the Hive table is created.</span><span class="sxs-lookup"><span data-stu-id="e983a-292">This requires that a separate Azure HDInsight cluster be provisioned, on which the Hive table is created.</span></span> <span data-ttu-id="e983a-293">The following sections show how to do this.</span><span class="sxs-lookup"><span data-stu-id="e983a-293">The following sections show how to do this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="e983a-294">Create an HDInsight Linux Cluster</span><span class="sxs-lookup"><span data-stu-id="e983a-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="e983a-295">Create an HDInsight Cluster (Linux) from the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e983a-295">Create an HDInsight Cluster (Linux) from the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="e983a-296">For details, see the **Create an HDInsight cluster with access to Azure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure portal](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e983a-296">For details, see the **Create an HDInsight cluster with access to Azure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure portal](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="e983a-298">Create Hive table in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e983a-298">Create Hive table in HDInsight</span></span>
<span data-ttu-id="e983a-299">Now you create Hive tables to be used in Azure Machine Learning Studio in the HDInsight cluster using the data stored in Azure Data Lake Store in the previous step.</span><span class="sxs-lookup"><span data-stu-id="e983a-299">Now you create Hive tables to be used in Azure Machine Learning Studio in the HDInsight cluster using the data stored in Azure Data Lake Store in the previous step.</span></span> <span data-ttu-id="e983a-300">Go to the HDInsight cluster created.</span><span class="sxs-lookup"><span data-stu-id="e983a-300">Go to the HDInsight cluster created.</span></span> <span data-ttu-id="e983a-301">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in the list with read, write and execute rights.</span><span class="sxs-lookup"><span data-stu-id="e983a-301">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in the list with read, write and execute rights.</span></span> 

 ![19](./media/data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="e983a-303">Then click **Dashboard** next to the **Settings** button and a window pops up.</span><span class="sxs-lookup"><span data-stu-id="e983a-303">Then click **Dashboard** next to the **Settings** button and a window pops up.</span></span> <span data-ttu-id="e983a-304">Click **Hive View** in the upper right corner of the page and you should see the **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="e983a-304">Click **Hive View** in the upper right corner of the page and you should see the **Query Editor**.</span></span>

 ![20](./media/data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="e983a-307">Paste in the following Hive scripts to create a table.</span><span class="sxs-lookup"><span data-stu-id="e983a-307">Paste in the following Hive scripts to create a table.</span></span> <span data-ttu-id="e983a-308">The location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span><span class="sxs-lookup"><span data-stu-id="e983a-308">The location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="e983a-309">When the query finishes running, you should see the results like this:</span><span class="sxs-lookup"><span data-stu-id="e983a-309">When the query finishes running, you should see the results like this:</span></span>

 ![22](./media/data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="e983a-311">Build and deploy models in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e983a-311">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="e983a-312">You are now ready to build and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e983a-312">You are now ready to build and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="e983a-313">The stratified sample data is ready to be used in this binary classification (tip or not) problem.</span><span class="sxs-lookup"><span data-stu-id="e983a-313">The stratified sample data is ready to be used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="e983a-314">The predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here it is only shown how to handle the case using the binary classification model.</span><span class="sxs-lookup"><span data-stu-id="e983a-314">The predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here it is only shown how to handle the case using the binary classification model.</span></span>

1. <span data-ttu-id="e983a-315">Get the data into Azure ML using the **Import Data** module, available in the **Data Input and Output** section.</span><span class="sxs-lookup"><span data-stu-id="e983a-315">Get the data into Azure ML using the **Import Data** module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="e983a-316">For more information, see the [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span><span class="sxs-lookup"><span data-stu-id="e983a-316">For more information, see the [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="e983a-317">Select **Hive Query** as the **Data source** in the **Properties** panel.</span><span class="sxs-lookup"><span data-stu-id="e983a-317">Select **Hive Query** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="e983a-318">Paste the following Hive script in the **Hive database query** editor</span><span class="sxs-lookup"><span data-stu-id="e983a-318">Paste the following Hive script in the **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="e983a-319">Enter the URI of HDInsight cluster (this can be found in Azure portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span><span class="sxs-lookup"><span data-stu-id="e983a-319">Enter the URI of HDInsight cluster (this can be found in Azure portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="e983a-321">An example of a binary classification experiment reading data from Hive table is shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="e983a-321">An example of a binary classification experiment reading data from Hive table is shown in the following figure:</span></span>

 ![24](./media/data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="e983a-323">After the experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span><span class="sxs-lookup"><span data-stu-id="e983a-323">After the experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="e983a-325">Run the automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span><span class="sxs-lookup"><span data-stu-id="e983a-325">Run the automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="e983a-327">The web service dashboard displays shortly:</span><span class="sxs-lookup"><span data-stu-id="e983a-327">The web service dashboard displays shortly:</span></span>

 ![27](./media/data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="e983a-329">Summary</span><span class="sxs-lookup"><span data-stu-id="e983a-329">Summary</span></span>
<span data-ttu-id="e983a-330">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e983a-330">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="e983a-331">This environment was used to analyze a large public dataset, taking it through the canonical steps of the Data Science Process, from data acquisition through model training, and then to the deployment of the model as a web service.</span><span class="sxs-lookup"><span data-stu-id="e983a-331">This environment was used to analyze a large public dataset, taking it through the canonical steps of the Data Science Process, from data acquisition through model training, and then to the deployment of the model as a web service.</span></span> <span data-ttu-id="e983a-332">U-SQL was used to process, explore and sample the data.</span><span class="sxs-lookup"><span data-stu-id="e983a-332">U-SQL was used to process, explore and sample the data.</span></span> <span data-ttu-id="e983a-333">Python and Hive were used with Azure Machine Learning Studio to build and deploy predictive models.</span><span class="sxs-lookup"><span data-stu-id="e983a-333">Python and Hive were used with Azure Machine Learning Studio to build and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="e983a-334">What's next?</span><span class="sxs-lookup"><span data-stu-id="e983a-334">What's next?</span></span>
<span data-ttu-id="e983a-335">The learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links to topics describing each step in the advanced analytics process.</span><span class="sxs-lookup"><span data-stu-id="e983a-335">The learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links to topics describing each step in the advanced analytics process.</span></span> <span data-ttu-id="e983a-336">There are a series of walkthroughs itemized on the [Team Data Science Process walkthroughs](walkthroughs.md) page that showcase how to use resources and services in various predictive analytics scenarios:</span><span class="sxs-lookup"><span data-stu-id="e983a-336">There are a series of walkthroughs itemized on the [Team Data Science Process walkthroughs](walkthroughs.md) page that showcase how to use resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="e983a-337">The Team Data Science Process in action: using SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e983a-337">The Team Data Science Process in action: using SQL Data Warehouse</span></span>](sqldw-walkthrough.md)
* [<span data-ttu-id="e983a-338">The Team Data Science Process in action: using HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="e983a-338">The Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](hive-walkthrough.md)
* [<span data-ttu-id="e983a-339">The Team Data Science Process: using SQL Server</span><span class="sxs-lookup"><span data-stu-id="e983a-339">The Team Data Science Process: using SQL Server</span></span>](sql-walkthrough.md)
* [<span data-ttu-id="e983a-340">Overview of the Data Science Process using Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e983a-340">Overview of the Data Science Process using Spark on Azure HDInsight</span></span>](spark-overview.md)
