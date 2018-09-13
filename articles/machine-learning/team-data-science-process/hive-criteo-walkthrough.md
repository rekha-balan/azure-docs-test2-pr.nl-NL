---
title: The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset | Microsoft Docs
description: Using the Team Data Science Process for an end-to-end scenario employing an HDInsight Hadoop cluster to build and deploy a model using a large (1 TB) publicly available dataset
services: machine-learning,hdinsight
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: deguhath
ms.openlocfilehash: b368bf76516b0b6f87ad8ff57ca886a44b71926c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966536"
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="94670-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span><span class="sxs-lookup"><span data-stu-id="94670-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="94670-104">This walkthrough demonstrates how to use the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span><span class="sxs-lookup"><span data-stu-id="94670-104">This walkthrough demonstrates how to use the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="94670-105">It uses Azure Machine Learning to build a binary classification model on this data.</span><span class="sxs-lookup"><span data-stu-id="94670-105">It uses Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="94670-106">It also shows how to publish one of these models as a Web service.</span><span class="sxs-lookup"><span data-stu-id="94670-106">It also shows how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="94670-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="94670-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="94670-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span><span class="sxs-lookup"><span data-stu-id="94670-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <a name="dataset"></a><span data-ttu-id="94670-109">Criteo Dataset Description</span><span class="sxs-lookup"><span data-stu-id="94670-109">Criteo Dataset Description</span></span>
<span data-ttu-id="94670-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span><span class="sxs-lookup"><span data-stu-id="94670-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="94670-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="94670-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="94670-112">For the convenience of data scientists, the data available to us to experiment with has been unzipped.</span><span class="sxs-lookup"><span data-stu-id="94670-112">For the convenience of data scientists, the data available to us to experiment with has been unzipped.</span></span>

<span data-ttu-id="94670-113">Each record in this dataset contains 40 columns:</span><span class="sxs-lookup"><span data-stu-id="94670-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="94670-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span><span class="sxs-lookup"><span data-stu-id="94670-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="94670-115">next 13 columns are numeric, and</span><span class="sxs-lookup"><span data-stu-id="94670-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="94670-116">last 26 are categorical columns</span><span class="sxs-lookup"><span data-stu-id="94670-116">last 26 are categorical columns</span></span>

<span data-ttu-id="94670-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span><span class="sxs-lookup"><span data-stu-id="94670-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="94670-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span><span class="sxs-lookup"><span data-stu-id="94670-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="94670-119">There are missing values in both the numeric and categorical columns in this dataset.</span><span class="sxs-lookup"><span data-stu-id="94670-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="94670-120">A simple method for handling the missing values is described.</span><span class="sxs-lookup"><span data-stu-id="94670-120">A simple method for handling the missing values is described.</span></span> <span data-ttu-id="94670-121">Additional details of the data are explored when storing them into Hive tables.</span><span class="sxs-lookup"><span data-stu-id="94670-121">Additional details of the data are explored when storing them into Hive tables.</span></span>

<span data-ttu-id="94670-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span><span class="sxs-lookup"><span data-stu-id="94670-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="94670-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span><span class="sxs-lookup"><span data-stu-id="94670-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <a name="mltasks"></a><span data-ttu-id="94670-124">Examples of prediction tasks</span><span class="sxs-lookup"><span data-stu-id="94670-124">Examples of prediction tasks</span></span>
<span data-ttu-id="94670-125">Two sample prediction problems are addressed in this walkthrough:</span><span class="sxs-lookup"><span data-stu-id="94670-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="94670-126">**Binary classification**: Predicts whether a user clicked an add:</span><span class="sxs-lookup"><span data-stu-id="94670-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="94670-127">Class 0: No Click</span><span class="sxs-lookup"><span data-stu-id="94670-127">Class 0: No Click</span></span>
   * <span data-ttu-id="94670-128">Class 1: Click</span><span class="sxs-lookup"><span data-stu-id="94670-128">Class 1: Click</span></span>
2. <span data-ttu-id="94670-129">**Regression**: Predicts the probability of an ad click from user features.</span><span class="sxs-lookup"><span data-stu-id="94670-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <a name="setup"></a><span data-ttu-id="94670-130">Set Up an HDInsight Hadoop cluster for data science</span><span class="sxs-lookup"><span data-stu-id="94670-130">Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="94670-131">**Note:** This is typically an **Admin** task.</span><span class="sxs-lookup"><span data-stu-id="94670-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="94670-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span><span class="sxs-lookup"><span data-stu-id="94670-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="94670-133">[Create a storage account](../../storage/common/storage-quickstart-create-account.md): This storage account is used to store data in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="94670-133">[Create a storage account](../../storage/common/storage-quickstart-create-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="94670-134">The data used in HDInsight clusters is stored here.</span><span class="sxs-lookup"><span data-stu-id="94670-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="94670-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span><span class="sxs-lookup"><span data-stu-id="94670-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="94670-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="94670-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span><span class="sxs-lookup"><span data-stu-id="94670-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="94670-138">This storage account is used for accessing data that can be processed within the cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="94670-139">You must enable Remote Access to the head node of the cluster after it is created.</span><span class="sxs-lookup"><span data-stu-id="94670-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="94670-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span><span class="sxs-lookup"><span data-stu-id="94670-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="94670-141">[Create an Azure ML workspace](../studio/create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-141">[Create an Azure ML workspace](../studio/create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <a name="getdata"></a><span data-ttu-id="94670-142">Get and consume data from a public source</span><span class="sxs-lookup"><span data-stu-id="94670-142">Get and consume data from a public source</span></span>
<span data-ttu-id="94670-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span><span class="sxs-lookup"><span data-stu-id="94670-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="94670-144">A snapshot of what this looks like is shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-144">A snapshot of what this looks like is shown here:</span></span>

![Accept Criteo terms](./media/hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="94670-146">Click **Continue to Download** to read more about the dataset and its availability.</span><span class="sxs-lookup"><span data-stu-id="94670-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="94670-147">The data resides in a public [Azure blob storage](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="94670-147">The data resides in a public [Azure blob storage](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="94670-148">The "wasb" refers to Azure Blob Storage location.</span><span class="sxs-lookup"><span data-stu-id="94670-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="94670-149">The data in this public blob storage consists of three subfolders of unzipped data.</span><span class="sxs-lookup"><span data-stu-id="94670-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="94670-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span><span class="sxs-lookup"><span data-stu-id="94670-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="94670-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span><span class="sxs-lookup"><span data-stu-id="94670-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="94670-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span><span class="sxs-lookup"><span data-stu-id="94670-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="94670-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span><span class="sxs-lookup"><span data-stu-id="94670-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="94670-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span><span class="sxs-lookup"><span data-stu-id="94670-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <a name="login"></a><span data-ttu-id="94670-155">Log in to the cluster headnode</span><span class="sxs-lookup"><span data-stu-id="94670-155">Log in to the cluster headnode</span></span>
<span data-ttu-id="94670-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="94670-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="94670-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="94670-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="94670-159">This takes you to the headnode of the cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="94670-160">Here is what a typical first log in to the cluster headnode looks like:</span><span class="sxs-lookup"><span data-stu-id="94670-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![Log in to cluster](./media/hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="94670-162">On the left is the "Hadoop Command Line", which is our workhorse for the data exploration.</span><span class="sxs-lookup"><span data-stu-id="94670-162">On the left is the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="94670-163">Notice two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span><span class="sxs-lookup"><span data-stu-id="94670-163">Notice two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="94670-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="94670-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="94670-165">Now you are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="94670-165">Now you are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <a name="hive-db-tables"></a> <span data-ttu-id="94670-166">Create Hive database and tables</span><span class="sxs-lookup"><span data-stu-id="94670-166">Create Hive database and tables</span></span>
<span data-ttu-id="94670-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span><span class="sxs-lookup"><span data-stu-id="94670-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="94670-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span><span class="sxs-lookup"><span data-stu-id="94670-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="94670-169">This takes care of any path issues automatically.</span><span class="sxs-lookup"><span data-stu-id="94670-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="94670-170">You can use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span><span class="sxs-lookup"><span data-stu-id="94670-170">You can use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="94670-171">To execute any Hive query, one can always use the following commands:</span><span class="sxs-lookup"><span data-stu-id="94670-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="94670-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span><span class="sxs-lookup"><span data-stu-id="94670-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="94670-173">The following code creates a database "criteo" and then generates 4 tables:</span><span class="sxs-lookup"><span data-stu-id="94670-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="94670-174">a *table for generating counts* built on days day\_00 to day\_20,</span><span class="sxs-lookup"><span data-stu-id="94670-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="94670-175">a *table for use as the train dataset* built on day\_21, and</span><span class="sxs-lookup"><span data-stu-id="94670-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="94670-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span><span class="sxs-lookup"><span data-stu-id="94670-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="94670-177">Split the test dataset into two different tables because one of the days is a holiday.</span><span class="sxs-lookup"><span data-stu-id="94670-177">Split the test dataset into two different tables because one of the days is a holiday.</span></span> <span data-ttu-id="94670-178">The objective is to determine if the model can detect differences between a holiday and non-holiday from the click-through rate.</span><span class="sxs-lookup"><span data-stu-id="94670-178">The objective is to determine if the model can detect differences between a holiday and non-holiday from the click-through rate.</span></span>

<span data-ttu-id="94670-179">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span><span class="sxs-lookup"><span data-stu-id="94670-179">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

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

<span data-ttu-id="94670-180">All these tables are external so you can simply point to their Azure Blob Storage (wasb) locations.</span><span class="sxs-lookup"><span data-stu-id="94670-180">All these tables are external so you can simply point to their Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="94670-181">**There are two ways to execute ANY Hive query:**</span><span class="sxs-lookup"><span data-stu-id="94670-181">**There are two ways to execute ANY Hive query:**</span></span>

1. <span data-ttu-id="94670-182">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span><span class="sxs-lookup"><span data-stu-id="94670-182">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="94670-183">To do this, do:</span><span class="sxs-lookup"><span data-stu-id="94670-183">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="94670-184">Now at the REPL command-line, cutting and pasting the query executes it.</span><span class="sxs-lookup"><span data-stu-id="94670-184">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="94670-185">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span><span class="sxs-lookup"><span data-stu-id="94670-185">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="94670-186">Confirm database and table creation</span><span class="sxs-lookup"><span data-stu-id="94670-186">Confirm database and table creation</span></span>
<span data-ttu-id="94670-187">Next, confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span><span class="sxs-lookup"><span data-stu-id="94670-187">Next, confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="94670-188">This gives:</span><span class="sxs-lookup"><span data-stu-id="94670-188">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="94670-189">This confirms the creation of the new database, "criteo".</span><span class="sxs-lookup"><span data-stu-id="94670-189">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="94670-190">To see what tables were created, simply issue the command here from the Hive bin/ directory prompt:</span><span class="sxs-lookup"><span data-stu-id="94670-190">To see what tables were created, simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="94670-191">You should then see the following output:</span><span class="sxs-lookup"><span data-stu-id="94670-191">You should then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> <span data-ttu-id="94670-192">Data exploration in Hive</span><span class="sxs-lookup"><span data-stu-id="94670-192">Data exploration in Hive</span></span>
<span data-ttu-id="94670-193">Now you are ready to do some basic data exploration in Hive.</span><span class="sxs-lookup"><span data-stu-id="94670-193">Now you are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="94670-194">You begin by counting the number of examples in the train and test data tables.</span><span class="sxs-lookup"><span data-stu-id="94670-194">You begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="94670-195">Number of train examples</span><span class="sxs-lookup"><span data-stu-id="94670-195">Number of train examples</span></span>
<span data-ttu-id="94670-196">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-196">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="94670-197">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-197">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="94670-198">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span><span class="sxs-lookup"><span data-stu-id="94670-198">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="94670-199">Number of test examples in the two test datasets</span><span class="sxs-lookup"><span data-stu-id="94670-199">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="94670-200">Now count the number of examples in the two test datasets.</span><span class="sxs-lookup"><span data-stu-id="94670-200">Now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="94670-201">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span><span class="sxs-lookup"><span data-stu-id="94670-201">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="94670-202">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-202">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="94670-203">As usual, you may also call the script from the Hive bin/ directory prompt by issuing the command:</span><span class="sxs-lookup"><span data-stu-id="94670-203">As usual, you may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="94670-204">Finally, you examine the number of test examples in the test dataset based on day\_23.</span><span class="sxs-lookup"><span data-stu-id="94670-204">Finally, you examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="94670-205">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="94670-205">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="94670-206">This gives:</span><span class="sxs-lookup"><span data-stu-id="94670-206">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="94670-207">Label distribution in the train dataset</span><span class="sxs-lookup"><span data-stu-id="94670-207">Label distribution in the train dataset</span></span>
<span data-ttu-id="94670-208">The label distribution in the train dataset is of interest.</span><span class="sxs-lookup"><span data-stu-id="94670-208">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="94670-209">To see this, show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="94670-209">To see this, show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="94670-210">This yields the label distribution:</span><span class="sxs-lookup"><span data-stu-id="94670-210">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="94670-211">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span><span class="sxs-lookup"><span data-stu-id="94670-211">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="94670-212">Histogram distributions of some numeric variables in the train dataset</span><span class="sxs-lookup"><span data-stu-id="94670-212">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="94670-213">You can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span><span class="sxs-lookup"><span data-stu-id="94670-213">You can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="94670-214">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="94670-214">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="94670-215">This yields the following:</span><span class="sxs-lookup"><span data-stu-id="94670-215">This yields the following:</span></span>

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

<span data-ttu-id="94670-216">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span><span class="sxs-lookup"><span data-stu-id="94670-216">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="94670-217">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span><span class="sxs-lookup"><span data-stu-id="94670-217">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="94670-218">Approximate percentiles of some numeric variables in the train dataset</span><span class="sxs-lookup"><span data-stu-id="94670-218">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="94670-219">Also of interest with numeric variables is the computation of approximate percentiles.</span><span class="sxs-lookup"><span data-stu-id="94670-219">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="94670-220">Hive's native "percentile\_approx" does this for us.</span><span class="sxs-lookup"><span data-stu-id="94670-220">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="94670-221">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span><span class="sxs-lookup"><span data-stu-id="94670-221">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="94670-222">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-222">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="94670-223">The distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span><span class="sxs-lookup"><span data-stu-id="94670-223">The distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="94670-224">Find number of unique values for some categorical columns in the train dataset</span><span class="sxs-lookup"><span data-stu-id="94670-224">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="94670-225">Continuing the data exploration, find, for some categorical columns, the number of unique values they take.</span><span class="sxs-lookup"><span data-stu-id="94670-225">Continuing the data exploration, find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="94670-226">To do this, show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="94670-226">To do this, show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="94670-227">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-227">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="94670-228">Note that Col15 has 19M unique values!</span><span class="sxs-lookup"><span data-stu-id="94670-228">Note that Col15 has 19M unique values!</span></span> <span data-ttu-id="94670-229">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is not feasible.</span><span class="sxs-lookup"><span data-stu-id="94670-229">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is not feasible.</span></span> <span data-ttu-id="94670-230">In particular, a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently is explained and demonstrated.</span><span class="sxs-lookup"><span data-stu-id="94670-230">In particular, a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently is explained and demonstrated.</span></span>

<span data-ttu-id="94670-231">Finally look at the number of unique values for some other categorical columns as well.</span><span class="sxs-lookup"><span data-stu-id="94670-231">Finally look at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="94670-232">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span><span class="sxs-lookup"><span data-stu-id="94670-232">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="94670-233">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-233">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="94670-234">Again, note that except for Col20, all the other columns have many unique values.</span><span class="sxs-lookup"><span data-stu-id="94670-234">Again, note that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="94670-235">Co-occurrence counts of pairs of categorical variables in the train dataset</span><span class="sxs-lookup"><span data-stu-id="94670-235">Co-occurrence counts of pairs of categorical variables in the train dataset</span></span>

<span data-ttu-id="94670-236">The co-occurrence counts of pairs of categorical variables is also of interest.</span><span class="sxs-lookup"><span data-stu-id="94670-236">The co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="94670-237">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="94670-237">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="94670-238">Reverse order the counts by their occurrence and look at the top 15 in this case.</span><span class="sxs-lookup"><span data-stu-id="94670-238">Reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="94670-239">This gives us:</span><span class="sxs-lookup"><span data-stu-id="94670-239">This gives us:</span></span>

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

## <a name="downsample"></a> <span data-ttu-id="94670-240">Down sample the datasets for Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="94670-240">Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="94670-241">Having explored the datasets and demonstrated how to do this type of exploration for any variables (including combinations), down sample the data sets so that models in Azure Machine Learning can be built.</span><span class="sxs-lookup"><span data-stu-id="94670-241">Having explored the datasets and demonstrated how to do this type of exploration for any variables (including combinations), down sample the data sets so that models in Azure Machine Learning can be built.</span></span> <span data-ttu-id="94670-242">Recall that the focus of the problem is: given a set of example attributes (feature values from Col2 - Col40), predict if Col1 is a 0 (no click) or a 1 (click).</span><span class="sxs-lookup"><span data-stu-id="94670-242">Recall that the focus of the problem is: given a set of example attributes (feature values from Col2 - Col40), predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="94670-243">To down sample the train and test datasets to 1% of the original size, use Hive's native RAND() function.</span><span class="sxs-lookup"><span data-stu-id="94670-243">To down sample the train and test datasets to 1% of the original size, use Hive's native RAND() function.</span></span> <span data-ttu-id="94670-244">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span><span class="sxs-lookup"><span data-stu-id="94670-244">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="94670-245">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-245">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="94670-246">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span><span class="sxs-lookup"><span data-stu-id="94670-246">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="94670-247">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-247">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="94670-248">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span><span class="sxs-lookup"><span data-stu-id="94670-248">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="94670-249">This yields:</span><span class="sxs-lookup"><span data-stu-id="94670-249">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="94670-250">With this, you are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="94670-250">With this, you are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="94670-251">There is a final important component before moving on to Azure Machine Learning, which concerns the count table.</span><span class="sxs-lookup"><span data-stu-id="94670-251">There is a final important component before moving on to Azure Machine Learning, which concerns the count table.</span></span> <span data-ttu-id="94670-252">In the next sub-section, the count table is discussed in some detail.</span><span class="sxs-lookup"><span data-stu-id="94670-252">In the next sub-section, the count table is discussed in some detail.</span></span>

## <a name="count"></a> <span data-ttu-id="94670-253">A brief discussion on the count table</span><span class="sxs-lookup"><span data-stu-id="94670-253">A brief discussion on the count table</span></span>
<span data-ttu-id="94670-254">As you saw, several categorical variables have a very high dimensionality.</span><span class="sxs-lookup"><span data-stu-id="94670-254">As you saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="94670-255">In the walkthrough, a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner is presented.</span><span class="sxs-lookup"><span data-stu-id="94670-255">In the walkthrough, a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner is presented.</span></span> <span data-ttu-id="94670-256">More information on this technique is in the link provided.</span><span class="sxs-lookup"><span data-stu-id="94670-256">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="94670-257">In this walkthrough, the focus is on using count tables to produce compact representations of high-dimensional categorical features.</span><span class="sxs-lookup"><span data-stu-id="94670-257">In this walkthrough, the focus is on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="94670-258">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="94670-258">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="94670-259">To build count tables on the count data, use the data in the folder raw/count.</span><span class="sxs-lookup"><span data-stu-id="94670-259">To build count tables on the count data, use the data in the folder raw/count.</span></span> <span data-ttu-id="94670-260">In the modeling section, users are shown how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span><span class="sxs-lookup"><span data-stu-id="94670-260">In the modeling section, users are shown how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="94670-261">In what follows, when "pre-built count tables" are referred to, we mean using the count tables that have been provided.</span><span class="sxs-lookup"><span data-stu-id="94670-261">In what follows, when "pre-built count tables" are referred to, we mean using the count tables that have been provided.</span></span> <span data-ttu-id="94670-262">Detailed instructions on how to access these tables are provided in the next section.</span><span class="sxs-lookup"><span data-stu-id="94670-262">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <a name="aml"></a> <span data-ttu-id="94670-263">Build a model with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="94670-263">Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="94670-264">Our model building process in Azure Machine Learning follows these steps:</span><span class="sxs-lookup"><span data-stu-id="94670-264">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="94670-265">Get the data from Hive tables into Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="94670-265">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="94670-266">Create the experiment: clean the data and featurize with count tables</span><span class="sxs-lookup"><span data-stu-id="94670-266">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="94670-267">Build, train, and score the model</span><span class="sxs-lookup"><span data-stu-id="94670-267">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="94670-268">Evaluate the model</span><span class="sxs-lookup"><span data-stu-id="94670-268">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="94670-269">Publish the model as a web-service</span><span class="sxs-lookup"><span data-stu-id="94670-269">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="94670-270">Now you are ready to build models in Azure Machine Learning studio.</span><span class="sxs-lookup"><span data-stu-id="94670-270">Now you are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="94670-271">Our down sampled data is saved as Hive tables in the cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-271">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="94670-272">Use the Azure Machine Learning **Import Data** module to read this data.</span><span class="sxs-lookup"><span data-stu-id="94670-272">Use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="94670-273">The credentials to access the storage account of this cluster are provided in what follows.</span><span class="sxs-lookup"><span data-stu-id="94670-273">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <a name="step1"></a> <span data-ttu-id="94670-274">Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span><span class="sxs-lookup"><span data-stu-id="94670-274">Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="94670-275">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span><span class="sxs-lookup"><span data-stu-id="94670-275">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="94670-276">Then, from the **Search** box on the top left, search for "Import Data".</span><span class="sxs-lookup"><span data-stu-id="94670-276">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="94670-277">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span><span class="sxs-lookup"><span data-stu-id="94670-277">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="94670-278">This is what the **Import Data** looks like while getting data from the Hive table:</span><span class="sxs-lookup"><span data-stu-id="94670-278">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![Import Data gets data](./media/hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="94670-280">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span><span class="sxs-lookup"><span data-stu-id="94670-280">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="94670-281">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span><span class="sxs-lookup"><span data-stu-id="94670-281">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="94670-282">Choose "Hive query" for **Data Source**</span><span class="sxs-lookup"><span data-stu-id="94670-282">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="94670-283">In the **Hive database query** box, a simple SELECT \* FROM <your\_database\_name.your\_table\_name> - is enough.</span><span class="sxs-lookup"><span data-stu-id="94670-283">In the **Hive database query** box, a simple SELECT \* FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="94670-284">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="94670-284">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="94670-285">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-285">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="94670-286">(NOT the Remote Access user name!)</span><span class="sxs-lookup"><span data-stu-id="94670-286">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="94670-287">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-287">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="94670-288">(NOT the Remote Access password!)</span><span class="sxs-lookup"><span data-stu-id="94670-288">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="94670-289">**Location of output data**: Choose "Azure"</span><span class="sxs-lookup"><span data-stu-id="94670-289">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="94670-290">**Azure storage account name**: The storage account associated with the cluster</span><span class="sxs-lookup"><span data-stu-id="94670-290">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="94670-291">**Azure storage account key**: The key of the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="94670-291">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="94670-292">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span><span class="sxs-lookup"><span data-stu-id="94670-292">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="94670-293">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span><span class="sxs-lookup"><span data-stu-id="94670-293">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="94670-294">What this looks like:</span><span class="sxs-lookup"><span data-stu-id="94670-294">What this looks like:</span></span>

![Import Data save data](./media/hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="94670-296">Right-click the output port of the **Import Data** module.</span><span class="sxs-lookup"><span data-stu-id="94670-296">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="94670-297">This reveals a **Save as dataset** option and a **Visualize** option.</span><span class="sxs-lookup"><span data-stu-id="94670-297">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="94670-298">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span><span class="sxs-lookup"><span data-stu-id="94670-298">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="94670-299">To save data, simply select **Save as dataset** and follow instructions.</span><span class="sxs-lookup"><span data-stu-id="94670-299">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="94670-300">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="94670-300">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="94670-301">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span><span class="sxs-lookup"><span data-stu-id="94670-301">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="94670-302">Dropping it onto the main panel selects it for use in machine learning modeling.</span><span class="sxs-lookup"><span data-stu-id="94670-302">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![Drage dataset onto the main panel](./media/hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="94670-304">Do this for both the train and the test datasets.</span><span class="sxs-lookup"><span data-stu-id="94670-304">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="94670-305">Also, remember to use the database name and table names that you gave for this purpose.</span><span class="sxs-lookup"><span data-stu-id="94670-305">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="94670-306">The values used in the figure are solely for illustration purposes.\*\*</span><span class="sxs-lookup"><span data-stu-id="94670-306">The values used in the figure are solely for illustration purposes.\*\*</span></span>
> 
> 

### <a name="step2"></a> <span data-ttu-id="94670-307">Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span><span class="sxs-lookup"><span data-stu-id="94670-307">Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="94670-308">Our Azure ML experiment looks like this:</span><span class="sxs-lookup"><span data-stu-id="94670-308">Our Azure ML experiment looks like this:</span></span>

![Machine Learning experiment](./media/hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="94670-310">Now examine the key components of this experiment.</span><span class="sxs-lookup"><span data-stu-id="94670-310">Now examine the key components of this experiment.</span></span> <span data-ttu-id="94670-311">Drag our saved train and test datasets on to our experiment canvas first.</span><span class="sxs-lookup"><span data-stu-id="94670-311">Drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="94670-312">Clean Missing Data</span><span class="sxs-lookup"><span data-stu-id="94670-312">Clean Missing Data</span></span>
<span data-ttu-id="94670-313">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span><span class="sxs-lookup"><span data-stu-id="94670-313">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="94670-314">Look into this module to see this:</span><span class="sxs-lookup"><span data-stu-id="94670-314">Look into this module to see this:</span></span>

![Clean missing data](./media/hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="94670-316">Here, chose to replace all missing values with a 0.</span><span class="sxs-lookup"><span data-stu-id="94670-316">Here, chose to replace all missing values with a 0.</span></span> <span data-ttu-id="94670-317">There are other options as well, which can be seen by looking at the dropdowns in the module.</span><span class="sxs-lookup"><span data-stu-id="94670-317">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="94670-318">Feature engineering on the data</span><span class="sxs-lookup"><span data-stu-id="94670-318">Feature engineering on the data</span></span>
<span data-ttu-id="94670-319">There can be millions of unique values for some categorical features of large datasets.</span><span class="sxs-lookup"><span data-stu-id="94670-319">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="94670-320">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span><span class="sxs-lookup"><span data-stu-id="94670-320">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="94670-321">This walkthrough demonstrates how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span><span class="sxs-lookup"><span data-stu-id="94670-321">This walkthrough demonstrates how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="94670-322">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span><span class="sxs-lookup"><span data-stu-id="94670-322">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="94670-323">Building counting transforms</span><span class="sxs-lookup"><span data-stu-id="94670-323">Building counting transforms</span></span>
<span data-ttu-id="94670-324">To build count features, use the **Build Counting Transform** module that is available in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="94670-324">To build count features, use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="94670-325">The module looks like this:</span><span class="sxs-lookup"><span data-stu-id="94670-325">The module looks like this:</span></span>

<span data-ttu-id="94670-326">![Build Counting Transform module](./media/hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="94670-326">![Build Counting Transform module](./media/hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="94670-327">In the **Count columns** box, enter those columns that you wish to perform counts on.</span><span class="sxs-lookup"><span data-stu-id="94670-327">In the **Count columns** box, enter those columns that you wish to perform counts on.</span></span> <span data-ttu-id="94670-328">Typically, these are (as mentioned) high-dimensional categorical columns.</span><span class="sxs-lookup"><span data-stu-id="94670-328">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="94670-329">Remember that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span><span class="sxs-lookup"><span data-stu-id="94670-329">Remember that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="94670-330">Here, count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span><span class="sxs-lookup"><span data-stu-id="94670-330">Here, count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="94670-331">To use the module in the MapReduce mode (appropriate for large datasets), you need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span><span class="sxs-lookup"><span data-stu-id="94670-331">To use the module in the MapReduce mode (appropriate for large datasets), you need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="94670-332">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span><span class="sxs-lookup"><span data-stu-id="94670-332">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![Module parameters](./media/hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="94670-334">The preceding figure shows how to enter the input blob location.</span><span class="sxs-lookup"><span data-stu-id="94670-334">The preceding figure shows how to enter the input blob location.</span></span> <span data-ttu-id="94670-335">This location has the data reserved for building count tables on.</span><span class="sxs-lookup"><span data-stu-id="94670-335">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="94670-336">When this module finishes running, save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span><span class="sxs-lookup"><span data-stu-id="94670-336">When this module finishes running, save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

!["Save as Transform" option](./media/hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="94670-338">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span><span class="sxs-lookup"><span data-stu-id="94670-338">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="94670-339">For the remainder of this experiment, it is assumed that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span><span class="sxs-lookup"><span data-stu-id="94670-339">For the remainder of this experiment, it is assumed that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="94670-340">Choosing what count features to include as part of the train and test datasets</span><span class="sxs-lookup"><span data-stu-id="94670-340">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="94670-341">Once a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span><span class="sxs-lookup"><span data-stu-id="94670-341">Once a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="94670-342">For completeness, this module is shown here.</span><span class="sxs-lookup"><span data-stu-id="94670-342">For completeness, this module is shown here.</span></span> <span data-ttu-id="94670-343">But in interests of simplicity do not actually use it in our experiment.</span><span class="sxs-lookup"><span data-stu-id="94670-343">But in interests of simplicity do not actually use it in our experiment.</span></span>

![Modify Count Table parameters](./media/hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="94670-345">In this case, as can be seen, the log-odds are to be used and the back off column is ignored.</span><span class="sxs-lookup"><span data-stu-id="94670-345">In this case, as can be seen, the log-odds are to be used and the back off column is ignored.</span></span> <span data-ttu-id="94670-346">You can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span><span class="sxs-lookup"><span data-stu-id="94670-346">You can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="94670-347">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span><span class="sxs-lookup"><span data-stu-id="94670-347">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="94670-348">Data transformation before generating the count features</span><span class="sxs-lookup"><span data-stu-id="94670-348">Data transformation before generating the count features</span></span>
<span data-ttu-id="94670-349">Now the focus is on an important point about transforming our train and test data prior to actually generating count features.</span><span class="sxs-lookup"><span data-stu-id="94670-349">Now the focus is on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="94670-350">Note that there are two **Execute R Script** modules used before the count transform is applied to our data.</span><span class="sxs-lookup"><span data-stu-id="94670-350">Note that there are two **Execute R Script** modules used before the count transform is applied to our data.</span></span>

![Execute R Script modules](./media/hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="94670-352">Here is the first R script:</span><span class="sxs-lookup"><span data-stu-id="94670-352">Here is the first R script:</span></span>

![First R script](./media/hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="94670-354">This R script renames our columns to names "Col1" to "Col40".</span><span class="sxs-lookup"><span data-stu-id="94670-354">This R script renames our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="94670-355">This is because the count transform expects names of this format.</span><span class="sxs-lookup"><span data-stu-id="94670-355">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="94670-356">The second R script balances the distribution between positive and negative classes (classes 1 and 0 respectively) by down-sampling the negative class.</span><span class="sxs-lookup"><span data-stu-id="94670-356">The second R script balances the distribution between positive and negative classes (classes 1 and 0 respectively) by down-sampling the negative class.</span></span> <span data-ttu-id="94670-357">The R script here shows how to do this:</span><span class="sxs-lookup"><span data-stu-id="94670-357">The R script here shows how to do this:</span></span>

![Second R script](./media/hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="94670-359">In this simple R script, the "pos\_neg\_ratio" is used to set the amount of balance between the positive and the negative classes.</span><span class="sxs-lookup"><span data-stu-id="94670-359">In this simple R script, the "pos\_neg\_ratio" is used to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="94670-360">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in this case, you have 3.3% positive class and 96.7% negative class).</span><span class="sxs-lookup"><span data-stu-id="94670-360">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in this case, you have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="94670-361">Applying the count transformation on our data</span><span class="sxs-lookup"><span data-stu-id="94670-361">Applying the count transformation on our data</span></span>
<span data-ttu-id="94670-362">Finally, you can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span><span class="sxs-lookup"><span data-stu-id="94670-362">Finally, you can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="94670-363">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span><span class="sxs-lookup"><span data-stu-id="94670-363">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="94670-364">It is shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-364">It is shown here:</span></span>

![Apply Transformation module](./media/hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="94670-366">An excerpt of what the count features look like</span><span class="sxs-lookup"><span data-stu-id="94670-366">An excerpt of what the count features look like</span></span>
<span data-ttu-id="94670-367">It is instructive to see what the count features look like in our case.</span><span class="sxs-lookup"><span data-stu-id="94670-367">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="94670-368">Here is an excerpt of this:</span><span class="sxs-lookup"><span data-stu-id="94670-368">Here is an excerpt of this:</span></span>

![Count features](./media/hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="94670-370">This excerpt shows that for the columns counted on, you get the counts and log odds in addition to any relevant backoffs.</span><span class="sxs-lookup"><span data-stu-id="94670-370">This excerpt shows that for the columns counted on, you get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="94670-371">You are now ready to build an Azure Machine Learning model using these transformed datasets.</span><span class="sxs-lookup"><span data-stu-id="94670-371">You are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="94670-372">In the next section shows how this can be done.</span><span class="sxs-lookup"><span data-stu-id="94670-372">In the next section shows how this can be done.</span></span>

### <a name="step3"></a> <span data-ttu-id="94670-373">Step 3: Build, train, and score the model</span><span class="sxs-lookup"><span data-stu-id="94670-373">Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="94670-374">Choice of learner</span><span class="sxs-lookup"><span data-stu-id="94670-374">Choice of learner</span></span>
<span data-ttu-id="94670-375">First, you need to choose a learner.</span><span class="sxs-lookup"><span data-stu-id="94670-375">First, you need to choose a learner.</span></span> <span data-ttu-id="94670-376">Use a two-class boosted decision tree as our learner.</span><span class="sxs-lookup"><span data-stu-id="94670-376">Use a two-class boosted decision tree as our learner.</span></span> <span data-ttu-id="94670-377">Here are the default options for this learner:</span><span class="sxs-lookup"><span data-stu-id="94670-377">Here are the default options for this learner:</span></span>

![Two-Class Boosted Decision Tree parameters](./media/hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="94670-379">For the experiment, choose the default values.</span><span class="sxs-lookup"><span data-stu-id="94670-379">For the experiment, choose the default values.</span></span> <span data-ttu-id="94670-380">Note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span><span class="sxs-lookup"><span data-stu-id="94670-380">Note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="94670-381">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span><span class="sxs-lookup"><span data-stu-id="94670-381">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="94670-382">Train the model</span><span class="sxs-lookup"><span data-stu-id="94670-382">Train the model</span></span>
<span data-ttu-id="94670-383">For training, simply invoke a **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="94670-383">For training, simply invoke a **Train Model** module.</span></span> <span data-ttu-id="94670-384">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span><span class="sxs-lookup"><span data-stu-id="94670-384">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="94670-385">This is shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-385">This is shown here:</span></span>

![Train Model module](./media/hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="94670-387">Score the model</span><span class="sxs-lookup"><span data-stu-id="94670-387">Score the model</span></span>
<span data-ttu-id="94670-388">Once you have a trained model, you are ready to score on the test dataset and to evaluate its performance.</span><span class="sxs-lookup"><span data-stu-id="94670-388">Once you have a trained model, you are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="94670-389">Do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span><span class="sxs-lookup"><span data-stu-id="94670-389">Do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![Score Model module](./media/hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a> <span data-ttu-id="94670-391">Step 4: Evaluate the model</span><span class="sxs-lookup"><span data-stu-id="94670-391">Step 4: Evaluate the model</span></span>
<span data-ttu-id="94670-392">Finally, you should analyze model performance.</span><span class="sxs-lookup"><span data-stu-id="94670-392">Finally, you should analyze model performance.</span></span> <span data-ttu-id="94670-393">Usually, for two class (binary) classification problems, a good measure is the AUC.</span><span class="sxs-lookup"><span data-stu-id="94670-393">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="94670-394">To visualize this, hook up the **Score Model** module to an **Evaluate Model** module for this.</span><span class="sxs-lookup"><span data-stu-id="94670-394">To visualize this, hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="94670-395">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span><span class="sxs-lookup"><span data-stu-id="94670-395">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![Evaluate module BDT model](./media/hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="94670-397">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span><span class="sxs-lookup"><span data-stu-id="94670-397">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="94670-398">The following section shows our results using this model on our test dataset.</span><span class="sxs-lookup"><span data-stu-id="94670-398">The following section shows our results using this model on our test dataset.</span></span> <span data-ttu-id="94670-399">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="94670-399">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![Visualize Evaluate Model module](./media/hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a> <span data-ttu-id="94670-401">Step 5: Publish the model as a Web service</span><span class="sxs-lookup"><span data-stu-id="94670-401">Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="94670-402">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span><span class="sxs-lookup"><span data-stu-id="94670-402">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="94670-403">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span><span class="sxs-lookup"><span data-stu-id="94670-403">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="94670-404">To do this, first save our trained model as a Trained Model object.</span><span class="sxs-lookup"><span data-stu-id="94670-404">To do this, first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="94670-405">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span><span class="sxs-lookup"><span data-stu-id="94670-405">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="94670-406">Next, create input and output ports for our web service:</span><span class="sxs-lookup"><span data-stu-id="94670-406">Next, create input and output ports for our web service:</span></span>

* <span data-ttu-id="94670-407">an input port takes data in the same form as the data that you need predictions for</span><span class="sxs-lookup"><span data-stu-id="94670-407">an input port takes data in the same form as the data that you need predictions for</span></span>
* <span data-ttu-id="94670-408">an output port returns the Scored Labels and the associated probabilities.</span><span class="sxs-lookup"><span data-stu-id="94670-408">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="94670-409">Select a few rows of data for the input port</span><span class="sxs-lookup"><span data-stu-id="94670-409">Select a few rows of data for the input port</span></span>
<span data-ttu-id="94670-410">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span><span class="sxs-lookup"><span data-stu-id="94670-410">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="94670-411">Select just these rows of data for our input port using the SQL query shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-411">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![Input port data](./media/hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="94670-413">Web service</span><span class="sxs-lookup"><span data-stu-id="94670-413">Web service</span></span>
<span data-ttu-id="94670-414">Now you are ready to run a small experiment that can be used to publish our web service.</span><span class="sxs-lookup"><span data-stu-id="94670-414">Now you are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="94670-415">Generate input data for webservice</span><span class="sxs-lookup"><span data-stu-id="94670-415">Generate input data for webservice</span></span>
<span data-ttu-id="94670-416">As a zeroth step, since the count table is large, take a few lines of test data and generate output data from it with count features.</span><span class="sxs-lookup"><span data-stu-id="94670-416">As a zeroth step, since the count table is large, take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="94670-417">This can serve as the input data format for our webservice.</span><span class="sxs-lookup"><span data-stu-id="94670-417">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="94670-418">This is shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-418">This is shown here:</span></span>

![Create BDT input data](./media/hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="94670-420">For the input data format, use the OUTPUT of the **Count Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="94670-420">For the input data format, use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="94670-421">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span><span class="sxs-lookup"><span data-stu-id="94670-421">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="94670-422">This Dataset is used for the input data in the webservice.</span><span class="sxs-lookup"><span data-stu-id="94670-422">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="94670-423">Scoring experiment for publishing webservice</span><span class="sxs-lookup"><span data-stu-id="94670-423">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="94670-424">First, it is shown what this looks like.</span><span class="sxs-lookup"><span data-stu-id="94670-424">First, it is shown what this looks like.</span></span> <span data-ttu-id="94670-425">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that were generated in the previous steps using the **Count Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="94670-425">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that were generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="94670-426">Use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span><span class="sxs-lookup"><span data-stu-id="94670-426">Use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![Select Columns in Dataset](./media/hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="94670-428">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span><span class="sxs-lookup"><span data-stu-id="94670-428">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="94670-429">The contents are shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-429">The contents are shown here:</span></span>

![Filtering with the Select Columns in Dataset module](./media/hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="94670-431">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span><span class="sxs-lookup"><span data-stu-id="94670-431">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="94670-432">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span><span class="sxs-lookup"><span data-stu-id="94670-432">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![Publish Web service](./media/hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="94670-434">Once the webservice is published, get redirected to a page that looks thus:</span><span class="sxs-lookup"><span data-stu-id="94670-434">Once the webservice is published, get redirected to a page that looks thus:</span></span>

![Web service dashboard](./media/hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="94670-436">Notice the two links for webservices on the left side:</span><span class="sxs-lookup"><span data-stu-id="94670-436">Notice the two links for webservices on the left side:</span></span>

* <span data-ttu-id="94670-437">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what has been utilized in this workshop.</span><span class="sxs-lookup"><span data-stu-id="94670-437">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what has been utilized in this workshop.</span></span>
* <span data-ttu-id="94670-438">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="94670-438">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="94670-439">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span><span class="sxs-lookup"><span data-stu-id="94670-439">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="94670-440">Note that the API key on this page needs to be used for authentication.</span><span class="sxs-lookup"><span data-stu-id="94670-440">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="94670-441">It is convenient to copy this python code over to a new cell in the IPython notebook.</span><span class="sxs-lookup"><span data-stu-id="94670-441">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="94670-442">Here is a segment of python code with the correct API key.</span><span class="sxs-lookup"><span data-stu-id="94670-442">Here is a segment of python code with the correct API key.</span></span>

![Python code](./media/hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="94670-444">Note that the default API key has been replaced with our webservices's API key.</span><span class="sxs-lookup"><span data-stu-id="94670-444">Note that the default API key has been replaced with our webservices's API key.</span></span> <span data-ttu-id="94670-445">Clicking **Run** on this cell in an IPython notebook yields the following response:</span><span class="sxs-lookup"><span data-stu-id="94670-445">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![IPython response](./media/hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="94670-447">For the two test examples asked about (in the JSON framework of the python script), you get back answers in the form "Scored Labels, Scored Probabilities".</span><span class="sxs-lookup"><span data-stu-id="94670-447">For the two test examples asked about (in the JSON framework of the python script), you get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="94670-448">In this case, the default values have been chosen that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span><span class="sxs-lookup"><span data-stu-id="94670-448">In this case, the default values have been chosen that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="94670-449">This concludes our walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="94670-449">This concludes our walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="94670-450">You started with a terabyte of data, constructed a prediction model, and deployed it as a web service in the cloud.</span><span class="sxs-lookup"><span data-stu-id="94670-450">You started with a terabyte of data, constructed a prediction model, and deployed it as a web service in the cloud.</span></span>

