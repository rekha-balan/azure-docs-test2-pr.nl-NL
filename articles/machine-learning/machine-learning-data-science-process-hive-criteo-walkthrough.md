---
title: The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset | Microsoft Docs
description: Using the Team Data Science Process for an end-to-end scenario employing an HDInsight Hadoop cluster to build and deploy a model using a large (1 TB) publicly available dataset
services: machine-learning,hdinsight
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: f1380363b77e1b00311dd131cd2e2d2b01369415
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556040"
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="11dc8-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span><span class="sxs-lookup"><span data-stu-id="11dc8-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="11dc8-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span><span class="sxs-lookup"><span data-stu-id="11dc8-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="11dc8-105">We use Azure Machine Learning to build a binary classification model on this data.</span><span class="sxs-lookup"><span data-stu-id="11dc8-105">We use Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="11dc8-106">We also show how to publish one of these models as a Web service.</span><span class="sxs-lookup"><span data-stu-id="11dc8-106">We also show how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="11dc8-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="11dc8-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="11dc8-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span><span class="sxs-lookup"><span data-stu-id="11dc8-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <a name="dataset"></a><span data-ttu-id="11dc8-109">Criteo Dataset Description</span><span class="sxs-lookup"><span data-stu-id="11dc8-109">Criteo Dataset Description</span></span>
<span data-ttu-id="11dc8-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span><span class="sxs-lookup"><span data-stu-id="11dc8-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="11dc8-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="11dc8-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="11dc8-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span><span class="sxs-lookup"><span data-stu-id="11dc8-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span></span>

<span data-ttu-id="11dc8-113">Each record in this dataset contains 40 columns:</span><span class="sxs-lookup"><span data-stu-id="11dc8-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="11dc8-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span><span class="sxs-lookup"><span data-stu-id="11dc8-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="11dc8-115">next 13 columns are numeric, and</span><span class="sxs-lookup"><span data-stu-id="11dc8-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="11dc8-116">last 26 are categorical columns</span><span class="sxs-lookup"><span data-stu-id="11dc8-116">last 26 are categorical columns</span></span>

<span data-ttu-id="11dc8-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span><span class="sxs-lookup"><span data-stu-id="11dc8-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="11dc8-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span><span class="sxs-lookup"><span data-stu-id="11dc8-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="11dc8-119">There are missing values in both the numeric and categorical columns in this dataset.</span><span class="sxs-lookup"><span data-stu-id="11dc8-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="11dc8-120">We describe a simple method for handling the missing values.</span><span class="sxs-lookup"><span data-stu-id="11dc8-120">We describe a simple method for handling the missing values.</span></span> <span data-ttu-id="11dc8-121">Additional details of the data are explored when we store them into Hive tables.</span><span class="sxs-lookup"><span data-stu-id="11dc8-121">Additional details of the data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="11dc8-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span><span class="sxs-lookup"><span data-stu-id="11dc8-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="11dc8-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span><span class="sxs-lookup"><span data-stu-id="11dc8-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <a name="mltasks"></a><span data-ttu-id="11dc8-124">Examples of prediction tasks</span><span class="sxs-lookup"><span data-stu-id="11dc8-124">Examples of prediction tasks</span></span>
<span data-ttu-id="11dc8-125">Two sample prediction problems are addressed in this walkthrough:</span><span class="sxs-lookup"><span data-stu-id="11dc8-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="11dc8-126">**Binary classification**: Predicts whether a user clicked an add:</span><span class="sxs-lookup"><span data-stu-id="11dc8-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="11dc8-127">Class 0: No Click</span><span class="sxs-lookup"><span data-stu-id="11dc8-127">Class 0: No Click</span></span>
   * <span data-ttu-id="11dc8-128">Class 1: Click</span><span class="sxs-lookup"><span data-stu-id="11dc8-128">Class 1: Click</span></span>
2. <span data-ttu-id="11dc8-129">**Regression**: Predicts the probability of an ad click from user features.</span><span class="sxs-lookup"><span data-stu-id="11dc8-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <a name="setup"></a><span data-ttu-id="11dc8-130">Set Up an HDInsight Hadoop cluster for data science</span><span class="sxs-lookup"><span data-stu-id="11dc8-130">Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="11dc8-131">**Note:** This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="11dc8-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="11dc8-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span><span class="sxs-lookup"><span data-stu-id="11dc8-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="11dc8-133">[Create a storage account](../storage/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="11dc8-133">[Create a storage account](../storage/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="11dc8-134">The data used in HDInsight clusters is stored here.</span><span class="sxs-lookup"><span data-stu-id="11dc8-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="11dc8-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span><span class="sxs-lookup"><span data-stu-id="11dc8-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="11dc8-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="11dc8-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span><span class="sxs-lookup"><span data-stu-id="11dc8-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="11dc8-138">This storage account is used for accessing data that can be processed within the cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="11dc8-139">You must enable Remote Access to the head node of the cluster after it is created.</span><span class="sxs-lookup"><span data-stu-id="11dc8-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="11dc8-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span><span class="sxs-lookup"><span data-stu-id="11dc8-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="11dc8-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <a name="getdata"></a><span data-ttu-id="11dc8-142">Get and consume data from a public source</span><span class="sxs-lookup"><span data-stu-id="11dc8-142">Get and consume data from a public source</span></span>
<span data-ttu-id="11dc8-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span><span class="sxs-lookup"><span data-stu-id="11dc8-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="11dc8-144">A snapshot of what this looks like is shown here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-144">A snapshot of what this looks like is shown here:</span></span>

![Accept Criteo terms](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="11dc8-146">Click **Continue to Download** to read more about the dataset and its availability.</span><span class="sxs-lookup"><span data-stu-id="11dc8-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="11dc8-147">The data resides in a public [Azure blob storage](../storage/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="11dc8-147">The data resides in a public [Azure blob storage](../storage/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="11dc8-148">The "wasb" refers to Azure Blob Storage location.</span><span class="sxs-lookup"><span data-stu-id="11dc8-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="11dc8-149">The data in this public blob storage consists of three subfolders of unzipped data.</span><span class="sxs-lookup"><span data-stu-id="11dc8-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="11dc8-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span><span class="sxs-lookup"><span data-stu-id="11dc8-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="11dc8-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span><span class="sxs-lookup"><span data-stu-id="11dc8-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="11dc8-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span><span class="sxs-lookup"><span data-stu-id="11dc8-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="11dc8-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span><span class="sxs-lookup"><span data-stu-id="11dc8-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="11dc8-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span><span class="sxs-lookup"><span data-stu-id="11dc8-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <a name="login"></a><span data-ttu-id="11dc8-155">Log in to the cluster headnode</span><span class="sxs-lookup"><span data-stu-id="11dc8-155">Log in to the cluster headnode</span></span>
<span data-ttu-id="11dc8-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="11dc8-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="11dc8-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="11dc8-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="11dc8-159">This takes you to the headnode of the cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="11dc8-160">Here is what a typical first log in to the cluster headnode looks like:</span><span class="sxs-lookup"><span data-stu-id="11dc8-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![Log in to cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="11dc8-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span><span class="sxs-lookup"><span data-stu-id="11dc8-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="11dc8-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span><span class="sxs-lookup"><span data-stu-id="11dc8-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="11dc8-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="11dc8-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="11dc8-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="11dc8-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <a name="hive-db-tables"></a> <span data-ttu-id="11dc8-166">Create Hive database and tables</span><span class="sxs-lookup"><span data-stu-id="11dc8-166">Create Hive database and tables</span></span>
<span data-ttu-id="11dc8-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span><span class="sxs-lookup"><span data-stu-id="11dc8-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="11dc8-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span><span class="sxs-lookup"><span data-stu-id="11dc8-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="11dc8-169">This takes care of any path issues automatically.</span><span class="sxs-lookup"><span data-stu-id="11dc8-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="11dc8-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span><span class="sxs-lookup"><span data-stu-id="11dc8-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="11dc8-171">To execute any Hive query, one can always use the following commands:</span><span class="sxs-lookup"><span data-stu-id="11dc8-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="11dc8-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span><span class="sxs-lookup"><span data-stu-id="11dc8-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="11dc8-173">The following code creates a database "criteo" and then generates 4 tables:</span><span class="sxs-lookup"><span data-stu-id="11dc8-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="11dc8-174">a *table for generating counts* built on days day\_00 to day\_20,</span><span class="sxs-lookup"><span data-stu-id="11dc8-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="11dc8-175">a *table for use as the train dataset* built on day\_21, and</span><span class="sxs-lookup"><span data-stu-id="11dc8-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="11dc8-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span><span class="sxs-lookup"><span data-stu-id="11dc8-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="11dc8-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span><span class="sxs-lookup"><span data-stu-id="11dc8-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span></span>

<span data-ttu-id="11dc8-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span><span class="sxs-lookup"><span data-stu-id="11dc8-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="11dc8-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span><span class="sxs-lookup"><span data-stu-id="11dc8-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="11dc8-180">**There are two ways to execute ANY Hive query that we now mention.**</span><span class="sxs-lookup"><span data-stu-id="11dc8-180">**There are two ways to execute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="11dc8-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span><span class="sxs-lookup"><span data-stu-id="11dc8-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="11dc8-182">To do this, do:</span><span class="sxs-lookup"><span data-stu-id="11dc8-182">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="11dc8-183">Now at the REPL command-line, cutting and pasting the query executes it.</span><span class="sxs-lookup"><span data-stu-id="11dc8-183">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="11dc8-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span><span class="sxs-lookup"><span data-stu-id="11dc8-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="11dc8-185">Confirm database and table creation</span><span class="sxs-lookup"><span data-stu-id="11dc8-185">Confirm database and table creation</span></span>
<span data-ttu-id="11dc8-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span><span class="sxs-lookup"><span data-stu-id="11dc8-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="11dc8-187">This gives:</span><span class="sxs-lookup"><span data-stu-id="11dc8-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="11dc8-188">This confirms the creation of the new database, "criteo".</span><span class="sxs-lookup"><span data-stu-id="11dc8-188">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="11dc8-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span><span class="sxs-lookup"><span data-stu-id="11dc8-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="11dc8-190">We then see the following output:</span><span class="sxs-lookup"><span data-stu-id="11dc8-190">We then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> <span data-ttu-id="11dc8-191">Data exploration in Hive</span><span class="sxs-lookup"><span data-stu-id="11dc8-191">Data exploration in Hive</span></span>
<span data-ttu-id="11dc8-192">Now we are ready to do some basic data exploration in Hive.</span><span class="sxs-lookup"><span data-stu-id="11dc8-192">Now we are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="11dc8-193">We begin by counting the number of examples in the train and test data tables.</span><span class="sxs-lookup"><span data-stu-id="11dc8-193">We begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="11dc8-194">Number of train examples</span><span class="sxs-lookup"><span data-stu-id="11dc8-194">Number of train examples</span></span>
<span data-ttu-id="11dc8-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="11dc8-196">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="11dc8-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span><span class="sxs-lookup"><span data-stu-id="11dc8-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="11dc8-198">Number of test examples in the two test datasets</span><span class="sxs-lookup"><span data-stu-id="11dc8-198">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="11dc8-199">We now count the number of examples in the two test datasets.</span><span class="sxs-lookup"><span data-stu-id="11dc8-199">We now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="11dc8-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="11dc8-201">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="11dc8-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span><span class="sxs-lookup"><span data-stu-id="11dc8-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="11dc8-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span><span class="sxs-lookup"><span data-stu-id="11dc8-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="11dc8-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="11dc8-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="11dc8-205">This gives:</span><span class="sxs-lookup"><span data-stu-id="11dc8-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="11dc8-206">Label distribution in the train dataset</span><span class="sxs-lookup"><span data-stu-id="11dc8-206">Label distribution in the train dataset</span></span>
<span data-ttu-id="11dc8-207">The label distribution in the train dataset is of interest.</span><span class="sxs-lookup"><span data-stu-id="11dc8-207">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="11dc8-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="11dc8-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="11dc8-209">This yields the label distribution:</span><span class="sxs-lookup"><span data-stu-id="11dc8-209">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="11dc8-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span><span class="sxs-lookup"><span data-stu-id="11dc8-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="11dc8-211">Histogram distributions of some numeric variables in the train dataset</span><span class="sxs-lookup"><span data-stu-id="11dc8-211">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="11dc8-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span><span class="sxs-lookup"><span data-stu-id="11dc8-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="11dc8-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="11dc8-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="11dc8-214">This yields the following:</span><span class="sxs-lookup"><span data-stu-id="11dc8-214">This yields the following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="11dc8-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span><span class="sxs-lookup"><span data-stu-id="11dc8-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="11dc8-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span><span class="sxs-lookup"><span data-stu-id="11dc8-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="11dc8-217">Approximate percentiles of some numeric variables in the train dataset</span><span class="sxs-lookup"><span data-stu-id="11dc8-217">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="11dc8-218">Also of interest with numeric variables is the computation of approximate percentiles.</span><span class="sxs-lookup"><span data-stu-id="11dc8-218">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="11dc8-219">Hive's native "percentile\_approx" does this for us.</span><span class="sxs-lookup"><span data-stu-id="11dc8-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="11dc8-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span><span class="sxs-lookup"><span data-stu-id="11dc8-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="11dc8-221">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="11dc8-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span><span class="sxs-lookup"><span data-stu-id="11dc8-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="11dc8-223">Find number of unique values for some categorical columns in the train dataset</span><span class="sxs-lookup"><span data-stu-id="11dc8-223">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="11dc8-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span><span class="sxs-lookup"><span data-stu-id="11dc8-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="11dc8-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="11dc8-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="11dc8-226">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="11dc8-227">We note that Col15 has 19M unique values!</span><span class="sxs-lookup"><span data-stu-id="11dc8-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="11dc8-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span><span class="sxs-lookup"><span data-stu-id="11dc8-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="11dc8-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span><span class="sxs-lookup"><span data-stu-id="11dc8-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="11dc8-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span><span class="sxs-lookup"><span data-stu-id="11dc8-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="11dc8-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span><span class="sxs-lookup"><span data-stu-id="11dc8-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="11dc8-232">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="11dc8-233">Again we see that except for Col20, all the other columns have many unique values.</span><span class="sxs-lookup"><span data-stu-id="11dc8-233">Again we see that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="11dc8-234">Co-occurence counts of pairs of categorical variables in the train dataset</span><span class="sxs-lookup"><span data-stu-id="11dc8-234">Co-occurence counts of pairs of categorical variables in the train dataset</span></span>
<span data-ttu-id="11dc8-235">The co-occurence counts of pairs of categorical variables is also of interest.</span><span class="sxs-lookup"><span data-stu-id="11dc8-235">The co-occurence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="11dc8-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="11dc8-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="11dc8-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span><span class="sxs-lookup"><span data-stu-id="11dc8-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="11dc8-238">This gives us:</span><span class="sxs-lookup"><span data-stu-id="11dc8-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a> <span data-ttu-id="11dc8-239">Down sample the datasets for Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="11dc8-239">Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="11dc8-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="11dc8-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="11dc8-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span><span class="sxs-lookup"><span data-stu-id="11dc8-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="11dc8-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span><span class="sxs-lookup"><span data-stu-id="11dc8-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="11dc8-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span><span class="sxs-lookup"><span data-stu-id="11dc8-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="11dc8-244">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="11dc8-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span><span class="sxs-lookup"><span data-stu-id="11dc8-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="11dc8-246">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="11dc8-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span><span class="sxs-lookup"><span data-stu-id="11dc8-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="11dc8-248">This yields:</span><span class="sxs-lookup"><span data-stu-id="11dc8-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="11dc8-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="11dc8-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="11dc8-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span><span class="sxs-lookup"><span data-stu-id="11dc8-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span></span> <span data-ttu-id="11dc8-251">In the next sub-section, we discuss this in some detail.</span><span class="sxs-lookup"><span data-stu-id="11dc8-251">In the next sub-section, we discuss this in some detail.</span></span>

## <a name="count"></a> <span data-ttu-id="11dc8-252">A brief discussion on the count table</span><span class="sxs-lookup"><span data-stu-id="11dc8-252">A brief discussion on the count table</span></span>
<span data-ttu-id="11dc8-253">As we saw, several categorical variables have a very high dimensionality.</span><span class="sxs-lookup"><span data-stu-id="11dc8-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="11dc8-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span><span class="sxs-lookup"><span data-stu-id="11dc8-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="11dc8-255">More information on this technique is in the link provided.</span><span class="sxs-lookup"><span data-stu-id="11dc8-255">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="11dc8-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span><span class="sxs-lookup"><span data-stu-id="11dc8-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="11dc8-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="11dc8-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="11dc8-258">To build count tables on the count data, we use the data in the folder raw/count.</span><span class="sxs-lookup"><span data-stu-id="11dc8-258">To build count tables on the count data, we use the data in the folder raw/count.</span></span> <span data-ttu-id="11dc8-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span><span class="sxs-lookup"><span data-stu-id="11dc8-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="11dc8-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span><span class="sxs-lookup"><span data-stu-id="11dc8-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span></span> <span data-ttu-id="11dc8-261">Detailed instructions on how to access these tables are provided in the next section.</span><span class="sxs-lookup"><span data-stu-id="11dc8-261">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <a name="aml"></a> <span data-ttu-id="11dc8-262">Build a model with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="11dc8-262">Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="11dc8-263">Our model building process in Azure Machine Learning follows these steps:</span><span class="sxs-lookup"><span data-stu-id="11dc8-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="11dc8-264">Get the data from Hive tables into Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="11dc8-264">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="11dc8-265">Create the experiment: clean the data and featurize with count tables</span><span class="sxs-lookup"><span data-stu-id="11dc8-265">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="11dc8-266">Build, train, and score the model</span><span class="sxs-lookup"><span data-stu-id="11dc8-266">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="11dc8-267">Evaluate the model</span><span class="sxs-lookup"><span data-stu-id="11dc8-267">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="11dc8-268">Publish the model as a web-service</span><span class="sxs-lookup"><span data-stu-id="11dc8-268">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="11dc8-269">Now we are ready to build models in Azure Machine Learning studio.</span><span class="sxs-lookup"><span data-stu-id="11dc8-269">Now we are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="11dc8-270">Our down sampled data is saved as Hive tables in the cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-270">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="11dc8-271">We use the Azure Machine Learning **Import Data** module to read this data.</span><span class="sxs-lookup"><span data-stu-id="11dc8-271">We use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="11dc8-272">The credentials to access the storage account of this cluster are provided in what follows.</span><span class="sxs-lookup"><span data-stu-id="11dc8-272">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <a name="step1"></a> <span data-ttu-id="11dc8-273">Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span><span class="sxs-lookup"><span data-stu-id="11dc8-273">Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="11dc8-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span><span class="sxs-lookup"><span data-stu-id="11dc8-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="11dc8-275">Then, from the **Search** box on the top left, search for "Import Data".</span><span class="sxs-lookup"><span data-stu-id="11dc8-275">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="11dc8-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span><span class="sxs-lookup"><span data-stu-id="11dc8-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="11dc8-277">This is what the **Import Data** looks like while getting data from the Hive table:</span><span class="sxs-lookup"><span data-stu-id="11dc8-277">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![Import Data gets data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="11dc8-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span><span class="sxs-lookup"><span data-stu-id="11dc8-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="11dc8-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span><span class="sxs-lookup"><span data-stu-id="11dc8-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="11dc8-281">Choose "Hive query" for **Data Source**</span><span class="sxs-lookup"><span data-stu-id="11dc8-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="11dc8-282">In the **Hive database query** box, a simple SELECT \* FROM <your\_database\_name.your\_table\_name> - is enough.</span><span class="sxs-lookup"><span data-stu-id="11dc8-282">In the **Hive database query** box, a simple SELECT \* FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="11dc8-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="11dc8-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="11dc8-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="11dc8-285">(NOT the Remote Access user name!)</span><span class="sxs-lookup"><span data-stu-id="11dc8-285">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="11dc8-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="11dc8-287">(NOT the Remote Access password!)</span><span class="sxs-lookup"><span data-stu-id="11dc8-287">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="11dc8-288">**Location of output data**: Choose "Azure"</span><span class="sxs-lookup"><span data-stu-id="11dc8-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="11dc8-289">**Azure storage account name**: The storage account associated with the cluster</span><span class="sxs-lookup"><span data-stu-id="11dc8-289">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="11dc8-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="11dc8-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="11dc8-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span><span class="sxs-lookup"><span data-stu-id="11dc8-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="11dc8-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span><span class="sxs-lookup"><span data-stu-id="11dc8-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="11dc8-293">What this looks like:</span><span class="sxs-lookup"><span data-stu-id="11dc8-293">What this looks like:</span></span>

![Import Data save data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="11dc8-295">Right-click the output port of the **Import Data** module.</span><span class="sxs-lookup"><span data-stu-id="11dc8-295">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="11dc8-296">This reveals a **Save as dataset** option and a **Visualize** option.</span><span class="sxs-lookup"><span data-stu-id="11dc8-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="11dc8-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span><span class="sxs-lookup"><span data-stu-id="11dc8-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="11dc8-298">To save data, simply select **Save as dataset** and follow instructions.</span><span class="sxs-lookup"><span data-stu-id="11dc8-298">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="11dc8-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="11dc8-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="11dc8-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span><span class="sxs-lookup"><span data-stu-id="11dc8-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="11dc8-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span><span class="sxs-lookup"><span data-stu-id="11dc8-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![Drage dataset onto the main panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="11dc8-303">Do this for both the train and the test datasets.</span><span class="sxs-lookup"><span data-stu-id="11dc8-303">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="11dc8-304">Also, remember to use the database name and table names that you gave for this purpose.</span><span class="sxs-lookup"><span data-stu-id="11dc8-304">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="11dc8-305">The values used in the figure are solely for illustration purposes.\*\*</span><span class="sxs-lookup"><span data-stu-id="11dc8-305">The values used in the figure are solely for illustration purposes.\*\*</span></span>
> 
> 

### <a name="step2"></a> <span data-ttu-id="11dc8-306">Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span><span class="sxs-lookup"><span data-stu-id="11dc8-306">Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="11dc8-307">Our Azure ML experiment looks like this:</span><span class="sxs-lookup"><span data-stu-id="11dc8-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="11dc8-309">We now examine the key components of this experiment.</span><span class="sxs-lookup"><span data-stu-id="11dc8-309">We now examine the key components of this experiment.</span></span> <span data-ttu-id="11dc8-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span><span class="sxs-lookup"><span data-stu-id="11dc8-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="11dc8-311">Clean Missing Data</span><span class="sxs-lookup"><span data-stu-id="11dc8-311">Clean Missing Data</span></span>
<span data-ttu-id="11dc8-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span><span class="sxs-lookup"><span data-stu-id="11dc8-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="11dc8-313">Looking into this module, we see this:</span><span class="sxs-lookup"><span data-stu-id="11dc8-313">Looking into this module, we see this:</span></span>

![Clean missing data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="11dc8-315">Here, we chose to replace all missing values with a 0.</span><span class="sxs-lookup"><span data-stu-id="11dc8-315">Here, we chose to replace all missing values with a 0.</span></span> <span data-ttu-id="11dc8-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span><span class="sxs-lookup"><span data-stu-id="11dc8-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="11dc8-317">Feature engineering on the data</span><span class="sxs-lookup"><span data-stu-id="11dc8-317">Feature engineering on the data</span></span>
<span data-ttu-id="11dc8-318">There can be millions of unique values for some categorical features of large datasets.</span><span class="sxs-lookup"><span data-stu-id="11dc8-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="11dc8-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span><span class="sxs-lookup"><span data-stu-id="11dc8-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="11dc8-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span><span class="sxs-lookup"><span data-stu-id="11dc8-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="11dc8-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span><span class="sxs-lookup"><span data-stu-id="11dc8-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="11dc8-322">Building counting transforms</span><span class="sxs-lookup"><span data-stu-id="11dc8-322">Building counting transforms</span></span>
<span data-ttu-id="11dc8-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="11dc8-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="11dc8-324">The module looks like this:</span><span class="sxs-lookup"><span data-stu-id="11dc8-324">The module looks like this:</span></span>

<span data-ttu-id="11dc8-325">![Build Counting Transform module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="11dc8-325">![Build Counting Transform module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="11dc8-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span><span class="sxs-lookup"><span data-stu-id="11dc8-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span></span> <span data-ttu-id="11dc8-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span><span class="sxs-lookup"><span data-stu-id="11dc8-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="11dc8-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span><span class="sxs-lookup"><span data-stu-id="11dc8-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="11dc8-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span><span class="sxs-lookup"><span data-stu-id="11dc8-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="11dc8-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span><span class="sxs-lookup"><span data-stu-id="11dc8-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="11dc8-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span><span class="sxs-lookup"><span data-stu-id="11dc8-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![Module parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="11dc8-333">In the figure above, we show how to enter the input blob location.</span><span class="sxs-lookup"><span data-stu-id="11dc8-333">In the figure above, we show how to enter the input blob location.</span></span> <span data-ttu-id="11dc8-334">This location has the data reserved for building count tables on.</span><span class="sxs-lookup"><span data-stu-id="11dc8-334">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="11dc8-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span><span class="sxs-lookup"><span data-stu-id="11dc8-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

!["Save as Transform" option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="11dc8-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span><span class="sxs-lookup"><span data-stu-id="11dc8-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="11dc8-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span><span class="sxs-lookup"><span data-stu-id="11dc8-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="11dc8-339">Choosing what count features to include as part of the train and test datasets</span><span class="sxs-lookup"><span data-stu-id="11dc8-339">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="11dc8-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span><span class="sxs-lookup"><span data-stu-id="11dc8-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="11dc8-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span><span class="sxs-lookup"><span data-stu-id="11dc8-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modify Count Table parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="11dc8-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span><span class="sxs-lookup"><span data-stu-id="11dc8-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span></span> <span data-ttu-id="11dc8-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span><span class="sxs-lookup"><span data-stu-id="11dc8-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="11dc8-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span><span class="sxs-lookup"><span data-stu-id="11dc8-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="11dc8-346">Data transformation before generating the count features</span><span class="sxs-lookup"><span data-stu-id="11dc8-346">Data transformation before generating the count features</span></span>
<span data-ttu-id="11dc8-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span><span class="sxs-lookup"><span data-stu-id="11dc8-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="11dc8-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span><span class="sxs-lookup"><span data-stu-id="11dc8-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span></span>

![Execute R Script modules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="11dc8-350">Here is the first R script:</span><span class="sxs-lookup"><span data-stu-id="11dc8-350">Here is the first R script:</span></span>

![First R script](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="11dc8-352">In this R script, we rename our columns to names "Col1" to "Col40".</span><span class="sxs-lookup"><span data-stu-id="11dc8-352">In this R script, we rename our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="11dc8-353">This is because the count transform expects names of this format.</span><span class="sxs-lookup"><span data-stu-id="11dc8-353">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="11dc8-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span><span class="sxs-lookup"><span data-stu-id="11dc8-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span></span> <span data-ttu-id="11dc8-355">The R script here shows how to do this:</span><span class="sxs-lookup"><span data-stu-id="11dc8-355">The R script here shows how to do this:</span></span>

![Second R script](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="11dc8-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span><span class="sxs-lookup"><span data-stu-id="11dc8-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="11dc8-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span><span class="sxs-lookup"><span data-stu-id="11dc8-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="11dc8-359">Applying the count transformation on our data</span><span class="sxs-lookup"><span data-stu-id="11dc8-359">Applying the count transformation on our data</span></span>
<span data-ttu-id="11dc8-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span><span class="sxs-lookup"><span data-stu-id="11dc8-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="11dc8-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span><span class="sxs-lookup"><span data-stu-id="11dc8-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="11dc8-362">It is shown here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-362">It is shown here:</span></span>

![Apply Transformation module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="11dc8-364">An excerpt of what the count features look like</span><span class="sxs-lookup"><span data-stu-id="11dc8-364">An excerpt of what the count features look like</span></span>
<span data-ttu-id="11dc8-365">It is instructive to see what the count features look like in our case.</span><span class="sxs-lookup"><span data-stu-id="11dc8-365">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="11dc8-366">Here we show an excerpt of this:</span><span class="sxs-lookup"><span data-stu-id="11dc8-366">Here we show an excerpt of this:</span></span>

![Count features](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="11dc8-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span><span class="sxs-lookup"><span data-stu-id="11dc8-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="11dc8-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span><span class="sxs-lookup"><span data-stu-id="11dc8-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="11dc8-370">In the next section, we show how this can be done.</span><span class="sxs-lookup"><span data-stu-id="11dc8-370">In the next section, we show how this can be done.</span></span>

### <a name="step3"></a> <span data-ttu-id="11dc8-371">Step 3: Build, train, and score the model</span><span class="sxs-lookup"><span data-stu-id="11dc8-371">Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="11dc8-372">Choice of learner</span><span class="sxs-lookup"><span data-stu-id="11dc8-372">Choice of learner</span></span>
<span data-ttu-id="11dc8-373">First, we need to choose a learner.</span><span class="sxs-lookup"><span data-stu-id="11dc8-373">First, we need to choose a learner.</span></span> <span data-ttu-id="11dc8-374">We are going to use a two class boosted decision tree as our learner.</span><span class="sxs-lookup"><span data-stu-id="11dc8-374">We are going to use a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="11dc8-375">Here are the default options for this learner:</span><span class="sxs-lookup"><span data-stu-id="11dc8-375">Here are the default options for this learner:</span></span>

![Two-Class Boosted Decision Tree parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="11dc8-377">For our experiment, we are going to choose the default values.</span><span class="sxs-lookup"><span data-stu-id="11dc8-377">For our experiment, we are going to choose the default values.</span></span> <span data-ttu-id="11dc8-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span><span class="sxs-lookup"><span data-stu-id="11dc8-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="11dc8-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span><span class="sxs-lookup"><span data-stu-id="11dc8-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="11dc8-380">Train the model</span><span class="sxs-lookup"><span data-stu-id="11dc8-380">Train the model</span></span>
<span data-ttu-id="11dc8-381">For training, we simply invoke a **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="11dc8-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="11dc8-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span><span class="sxs-lookup"><span data-stu-id="11dc8-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="11dc8-383">This is shown here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-383">This is shown here:</span></span>

![Train Model module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="11dc8-385">Score the model</span><span class="sxs-lookup"><span data-stu-id="11dc8-385">Score the model</span></span>
<span data-ttu-id="11dc8-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span><span class="sxs-lookup"><span data-stu-id="11dc8-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="11dc8-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span><span class="sxs-lookup"><span data-stu-id="11dc8-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![Score Model module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a> <span data-ttu-id="11dc8-389">Step 4: Evaluate the model</span><span class="sxs-lookup"><span data-stu-id="11dc8-389">Step 4: Evaluate the model</span></span>
<span data-ttu-id="11dc8-390">Finally, we would like to analyze model performance.</span><span class="sxs-lookup"><span data-stu-id="11dc8-390">Finally, we would like to analyze model performance.</span></span> <span data-ttu-id="11dc8-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span><span class="sxs-lookup"><span data-stu-id="11dc8-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="11dc8-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span><span class="sxs-lookup"><span data-stu-id="11dc8-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="11dc8-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span><span class="sxs-lookup"><span data-stu-id="11dc8-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![Evaluate module BDT model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="11dc8-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span><span class="sxs-lookup"><span data-stu-id="11dc8-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="11dc8-396">In what follows, we show our results using this model on our test dataset.</span><span class="sxs-lookup"><span data-stu-id="11dc8-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="11dc8-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="11dc8-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![Visualize Evaluate Model module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a> <span data-ttu-id="11dc8-399">Step 5: Publish the model as a Web service</span><span class="sxs-lookup"><span data-stu-id="11dc8-399">Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="11dc8-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span><span class="sxs-lookup"><span data-stu-id="11dc8-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="11dc8-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span><span class="sxs-lookup"><span data-stu-id="11dc8-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="11dc8-402">To do this, we first save our trained model as a Trained Model object.</span><span class="sxs-lookup"><span data-stu-id="11dc8-402">To do this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="11dc8-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span><span class="sxs-lookup"><span data-stu-id="11dc8-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="11dc8-404">Next, we need to create input and output ports for our web service:</span><span class="sxs-lookup"><span data-stu-id="11dc8-404">Next, we need to create input and output ports for our web service:</span></span>

* <span data-ttu-id="11dc8-405">an input port takes data in the same form as the data that we need predictions for</span><span class="sxs-lookup"><span data-stu-id="11dc8-405">an input port takes data in the same form as the data that we need predictions for</span></span>
* <span data-ttu-id="11dc8-406">an output port returns the Scored Labels and the associated probabilities.</span><span class="sxs-lookup"><span data-stu-id="11dc8-406">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="11dc8-407">Select a few rows of data for the input port</span><span class="sxs-lookup"><span data-stu-id="11dc8-407">Select a few rows of data for the input port</span></span>
<span data-ttu-id="11dc8-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span><span class="sxs-lookup"><span data-stu-id="11dc8-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="11dc8-409">Select just these rows of data for our input port using the SQL query shown here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-409">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![Input port data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="11dc8-411">Web service</span><span class="sxs-lookup"><span data-stu-id="11dc8-411">Web service</span></span>
<span data-ttu-id="11dc8-412">Now we are ready to run a small experiment that can be used to publish our web service.</span><span class="sxs-lookup"><span data-stu-id="11dc8-412">Now we are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="11dc8-413">Generate input data for webservice</span><span class="sxs-lookup"><span data-stu-id="11dc8-413">Generate input data for webservice</span></span>
<span data-ttu-id="11dc8-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span><span class="sxs-lookup"><span data-stu-id="11dc8-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="11dc8-415">This can serve as the input data format for our webservice.</span><span class="sxs-lookup"><span data-stu-id="11dc8-415">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="11dc8-416">This is shown here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-416">This is shown here:</span></span>

![Create BDT input data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="11dc8-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="11dc8-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="11dc8-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span><span class="sxs-lookup"><span data-stu-id="11dc8-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="11dc8-420">This Dataset is used for the input data in the webservice.</span><span class="sxs-lookup"><span data-stu-id="11dc8-420">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="11dc8-421">Scoring experiment for publishing webservice</span><span class="sxs-lookup"><span data-stu-id="11dc8-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="11dc8-422">First, we show what this looks like.</span><span class="sxs-lookup"><span data-stu-id="11dc8-422">First, we show what this looks like.</span></span> <span data-ttu-id="11dc8-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="11dc8-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="11dc8-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span><span class="sxs-lookup"><span data-stu-id="11dc8-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![Select Columns in Dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="11dc8-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span><span class="sxs-lookup"><span data-stu-id="11dc8-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="11dc8-427">We show the contents here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-427">We show the contents here:</span></span>

![Filtering with the Select Columns in Dataset module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="11dc8-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span><span class="sxs-lookup"><span data-stu-id="11dc8-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="11dc8-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span><span class="sxs-lookup"><span data-stu-id="11dc8-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![Publish Web service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="11dc8-432">Once the webservice is published, we get redirected to a page that looks thus:</span><span class="sxs-lookup"><span data-stu-id="11dc8-432">Once the webservice is published, we get redirected to a page that looks thus:</span></span>

![Web service dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="11dc8-434">We see two links for webservices on the left side:</span><span class="sxs-lookup"><span data-stu-id="11dc8-434">We see two links for webservices on the left side:</span></span>

* <span data-ttu-id="11dc8-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span><span class="sxs-lookup"><span data-stu-id="11dc8-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="11dc8-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="11dc8-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="11dc8-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span><span class="sxs-lookup"><span data-stu-id="11dc8-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="11dc8-438">Note that the API key on this page needs to be used for authentication.</span><span class="sxs-lookup"><span data-stu-id="11dc8-438">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="11dc8-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span><span class="sxs-lookup"><span data-stu-id="11dc8-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="11dc8-440">Here we show a segment of python code with the correct API key.</span><span class="sxs-lookup"><span data-stu-id="11dc8-440">Here we show a segment of python code with the correct API key.</span></span>

![Python code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="11dc8-442">Note that we replaced the default API key with our webservices's API key.</span><span class="sxs-lookup"><span data-stu-id="11dc8-442">Note that we replaced the default API key with our webservices's API key.</span></span> <span data-ttu-id="11dc8-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span><span class="sxs-lookup"><span data-stu-id="11dc8-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![IPython response](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="11dc8-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span><span class="sxs-lookup"><span data-stu-id="11dc8-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="11dc8-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span><span class="sxs-lookup"><span data-stu-id="11dc8-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="11dc8-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="11dc8-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="11dc8-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span><span class="sxs-lookup"><span data-stu-id="11dc8-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span></span>































