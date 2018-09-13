---
title: Create features for data in an Hadoop cluster using Hive queries | Microsoft Docs
description: Examples of Hive queries that generate features in data stored in an Azure HDInsight Hadoop cluster.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/21/2017
ms.author: deguhath
ms.openlocfilehash: bca1e609570d9ea0dee9845969de8bb4b29cc1ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869618"
---
# <a name="create-features-for-data-in-a-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="0613a-103">Create features for data in a Hadoop cluster using Hive queries</span><span class="sxs-lookup"><span data-stu-id="0613a-103">Create features for data in a Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="0613a-104">This document shows how to create features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span><span class="sxs-lookup"><span data-stu-id="0613a-104">This document shows how to create features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="0613a-105">These Hive queries use embedded Hive User-Defined Functions (UDFs), the scripts for which are provided.</span><span class="sxs-lookup"><span data-stu-id="0613a-105">These Hive queries use embedded Hive User-Defined Functions (UDFs), the scripts for which are provided.</span></span>

<span data-ttu-id="0613a-106">The operations needed to create features can be memory intensive.</span><span class="sxs-lookup"><span data-stu-id="0613a-106">The operations needed to create features can be memory intensive.</span></span> <span data-ttu-id="0613a-107">The performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span><span class="sxs-lookup"><span data-stu-id="0613a-107">The performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="0613a-108">The tuning of these parameters is discussed in the final section.</span><span class="sxs-lookup"><span data-stu-id="0613a-108">The tuning of these parameters is discussed in the final section.</span></span>

<span data-ttu-id="0613a-109">Examples of the queries that are presented are specific to the [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="0613a-109">Examples of the queries that are presented are specific to the [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="0613a-110">These queries already have data schema specified and are ready to be submitted to run.</span><span class="sxs-lookup"><span data-stu-id="0613a-110">These queries already have data schema specified and are ready to be submitted to run.</span></span> <span data-ttu-id="0613a-111">In the final section, parameters that users can tune so that the performance of Hive queries can be improved are  also discussed.</span><span class="sxs-lookup"><span data-stu-id="0613a-111">In the final section, parameters that users can tune so that the performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../../includes/cap-create-features-selector.md)]

<span data-ttu-id="0613a-112">This **menu** links to topics that describe how to create features for data in various environments.</span><span class="sxs-lookup"><span data-stu-id="0613a-112">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="0613a-113">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="0613a-113">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0613a-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0613a-114">Prerequisites</span></span>
<span data-ttu-id="0613a-115">This article assumes that you have:</span><span class="sxs-lookup"><span data-stu-id="0613a-115">This article assumes that you have:</span></span>

* <span data-ttu-id="0613a-116">Created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="0613a-116">Created an Azure storage account.</span></span> <span data-ttu-id="0613a-117">If you need instructions, see [Create an Azure Storage account](../../storage/common/storage-quickstart-create-account.md)</span><span class="sxs-lookup"><span data-stu-id="0613a-117">If you need instructions, see [Create an Azure Storage account](../../storage/common/storage-quickstart-create-account.md)</span></span>
* <span data-ttu-id="0613a-118">Provisioned a customized Hadoop cluster with the HDInsight service.</span><span class="sxs-lookup"><span data-stu-id="0613a-118">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="0613a-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="0613a-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="0613a-120">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="0613a-120">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0613a-121">If it has not, follow [Create and load data to Hive tables](move-hive-tables.md) to upload data to Hive tables first.</span><span class="sxs-lookup"><span data-stu-id="0613a-121">If it has not, follow [Create and load data to Hive tables](move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="0613a-122">Enabled remote access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="0613a-122">Enabled remote access to the cluster.</span></span> <span data-ttu-id="0613a-123">If you need instructions, see [Access the Head Node of Hadoop Cluster](customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="0613a-123">If you need instructions, see [Access the Head Node of Hadoop Cluster](customize-hadoop-cluster.md).</span></span>

## <a name="hive-featureengineering"></a><span data-ttu-id="0613a-124">Feature generation</span><span class="sxs-lookup"><span data-stu-id="0613a-124">Feature generation</span></span>
<span data-ttu-id="0613a-125">In this section, several examples of the ways in which features can be generating using Hive queries are described.</span><span class="sxs-lookup"><span data-stu-id="0613a-125">In this section, several examples of the ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="0613a-126">Once you have generated additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, which can then be joined with the original table.</span><span class="sxs-lookup"><span data-stu-id="0613a-126">Once you have generated additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, which can then be joined with the original table.</span></span> <span data-ttu-id="0613a-127">Here are the examples presented:</span><span class="sxs-lookup"><span data-stu-id="0613a-127">Here are the examples presented:</span></span>

1. [<span data-ttu-id="0613a-128">Frequency-based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="0613a-128">Frequency-based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="0613a-129">Risks of Categorical Variables in Binary Classification</span><span class="sxs-lookup"><span data-stu-id="0613a-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="0613a-130">Extract features from Datetime Field</span><span class="sxs-lookup"><span data-stu-id="0613a-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="0613a-131">Extract features from Text Field</span><span class="sxs-lookup"><span data-stu-id="0613a-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="0613a-132">Calculate distance between GPS coordinates</span><span class="sxs-lookup"><span data-stu-id="0613a-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a><span data-ttu-id="0613a-133">Frequency-based feature generation</span><span class="sxs-lookup"><span data-stu-id="0613a-133">Frequency-based feature generation</span></span>
<span data-ttu-id="0613a-134">It is often useful to calculate the frequencies of the levels of a categorical variable, or the frequencies of certain combinations of levels from multiple categorical variables.</span><span class="sxs-lookup"><span data-stu-id="0613a-134">It is often useful to calculate the frequencies of the levels of a categorical variable, or the frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="0613a-135">Users can use the following script to calculate these frequencies:</span><span class="sxs-lookup"><span data-stu-id="0613a-135">Users can use the following script to calculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a><span data-ttu-id="0613a-136">Risks of categorical variables in binary classification</span><span class="sxs-lookup"><span data-stu-id="0613a-136">Risks of categorical variables in binary classification</span></span>
<span data-ttu-id="0613a-137">In binary classification, non-numeric categorical variables must be converted into numeric features when the models being used only take numeric features.</span><span class="sxs-lookup"><span data-stu-id="0613a-137">In binary classification, non-numeric categorical variables must be converted into numeric features when the models being used only take numeric features.</span></span> <span data-ttu-id="0613a-138">This conversion is done by replacing each non-numeric level with a numeric risk.</span><span class="sxs-lookup"><span data-stu-id="0613a-138">This conversion is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="0613a-139">This section shows some generic Hive queries that calculate the risk values (log odds) of a categorical variable.</span><span class="sxs-lookup"><span data-stu-id="0613a-139">This section shows some generic Hive queries that calculate the risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="0613a-140">In this example, variables `smooth_param1` and `smooth_param2` are set to smooth the risk values calculated from the data.</span><span class="sxs-lookup"><span data-stu-id="0613a-140">In this example, variables `smooth_param1` and `smooth_param2` are set to smooth the risk values calculated from the data.</span></span> <span data-ttu-id="0613a-141">Risks have a range between -Inf and Inf.</span><span class="sxs-lookup"><span data-stu-id="0613a-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="0613a-142">A risk > 0 indicates that the probability that the target is equal to 1 is greater than 0.5.</span><span class="sxs-lookup"><span data-stu-id="0613a-142">A risk > 0 indicates that the probability that the target is equal to 1 is greater than 0.5.</span></span>

<span data-ttu-id="0613a-143">After the risk table is calculated, users can assign risk values to a table by joining it with the risk table.</span><span class="sxs-lookup"><span data-stu-id="0613a-143">After the risk table is calculated, users can assign risk values to a table by joining it with the risk table.</span></span> <span data-ttu-id="0613a-144">The Hive joining query was provided in previous section.</span><span class="sxs-lookup"><span data-stu-id="0613a-144">The Hive joining query was provided in previous section.</span></span>

### <a name="hive-datefeatures"></a><span data-ttu-id="0613a-145">Extract features from datetime fields</span><span class="sxs-lookup"><span data-stu-id="0613a-145">Extract features from datetime fields</span></span>
<span data-ttu-id="0613a-146">Hive comes with a set of UDFs for processing datetime fields.</span><span class="sxs-lookup"><span data-stu-id="0613a-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="0613a-147">In Hive, the default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span><span class="sxs-lookup"><span data-stu-id="0613a-147">In Hive, the default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="0613a-148">This section shows examples that extract the day of a month, the month from a datetime field, and other examples that convert a datetime string in a format other than the default format to a datetime string in default format.</span><span class="sxs-lookup"><span data-stu-id="0613a-148">This section shows examples that extract the day of a month, the month from a datetime field, and other examples that convert a datetime string in a format other than the default format to a datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="0613a-149">This Hive query assumes that the *<datetime field>* is in the default datetime format.</span><span class="sxs-lookup"><span data-stu-id="0613a-149">This Hive query assumes that the *<datetime field>* is in the default datetime format.</span></span>

<span data-ttu-id="0613a-150">If a datetime field is not in the default format, you need to convert the datetime field into Unix time stamp first, and then convert the Unix time stamp to a datetime string that is in the default format.</span><span class="sxs-lookup"><span data-stu-id="0613a-150">If a datetime field is not in the default format, you need to convert the datetime field into Unix time stamp first, and then convert the Unix time stamp to a datetime string that is in the default format.</span></span> <span data-ttu-id="0613a-151">When the datetime is in default format, users can apply the embedded datetime UDFs to extract features.</span><span class="sxs-lookup"><span data-stu-id="0613a-151">When the datetime is in default format, users can apply the embedded datetime UDFs to extract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of the datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="0613a-152">In this query, if the *<datetime field>* has the pattern like *03/26/2015 12:04:39*, the *<pattern of the datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="0613a-152">In this query, if the *<datetime field>* has the pattern like *03/26/2015 12:04:39*, the *<pattern of the datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="0613a-153">To test it, users can run</span><span class="sxs-lookup"><span data-stu-id="0613a-153">To test it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="0613a-154">The *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when the clusters are provisioned.</span><span class="sxs-lookup"><span data-stu-id="0613a-154">The *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when the clusters are provisioned.</span></span>

### <a name="hive-textfeatures"></a><span data-ttu-id="0613a-155">Extract features from text fields</span><span class="sxs-lookup"><span data-stu-id="0613a-155">Extract features from text fields</span></span>
<span data-ttu-id="0613a-156">When the Hive table has a text field that contains a string of words that are delimited by spaces, the following query extracts the length of the string, and the number of words in the string.</span><span class="sxs-lookup"><span data-stu-id="0613a-156">When the Hive table has a text field that contains a string of words that are delimited by spaces, the following query extracts the length of the string, and the number of words in the string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a><span data-ttu-id="0613a-157">Calculate distances between sets of GPS coordinates</span><span class="sxs-lookup"><span data-stu-id="0613a-157">Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="0613a-158">The query given in this section can be directly applied to the NYC Taxi Trip Data.</span><span class="sxs-lookup"><span data-stu-id="0613a-158">The query given in this section can be directly applied to the NYC Taxi Trip Data.</span></span> <span data-ttu-id="0613a-159">The purpose of this query is to show how to apply an embedded mathematical function in Hive to generate features.</span><span class="sxs-lookup"><span data-stu-id="0613a-159">The purpose of this query is to show how to apply an embedded mathematical function in Hive to generate features.</span></span>

<span data-ttu-id="0613a-160">The fields that are used in this query are the GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span><span class="sxs-lookup"><span data-stu-id="0613a-160">The fields that are used in this query are the GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="0613a-161">The queries that calculate the direct distance between the pickup and dropoff coordinates are:</span><span class="sxs-lookup"><span data-stu-id="0613a-161">The queries that calculate the direct distance between the pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="0613a-162">The mathematical equations that calculate the distance between two GPS coordinates can be found on the <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span><span class="sxs-lookup"><span data-stu-id="0613a-162">The mathematical equations that calculate the distance between two GPS coordinates can be found on the <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="0613a-163">In this Javascript, the function `toRad()` is just *lat_or_lon*pi/180\*, which converts degrees to radians.</span><span class="sxs-lookup"><span data-stu-id="0613a-163">In this Javascript, the function `toRad()` is just *lat_or_lon*pi/180\*, which converts degrees to radians.</span></span> <span data-ttu-id="0613a-164">Here, *lat_or_lon* is the latitude or longitude.</span><span class="sxs-lookup"><span data-stu-id="0613a-164">Here, *lat_or_lon* is the latitude or longitude.</span></span> <span data-ttu-id="0613a-165">Since Hive does not provide the function `atan2`, but provides the function `atan`, the `atan2` function is implemented by `atan` function in the above Hive query using the definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span><span class="sxs-lookup"><span data-stu-id="0613a-165">Since Hive does not provide the function `atan2`, but provides the function `atan`, the `atan2` function is implemented by `atan` function in the above Hive query using the definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Create workspace](./media/create-features-hive/atan2new.png)

<span data-ttu-id="0613a-167">A full list of Hive embedded UDFs can be found in the **Built-in Functions** section on the <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span><span class="sxs-lookup"><span data-stu-id="0613a-167">A full list of Hive embedded UDFs can be found in the **Built-in Functions** section on the <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <a name="tuning"></a> <span data-ttu-id="0613a-168">Advanced topics: Tune Hive parameters to improve query speed</span><span class="sxs-lookup"><span data-stu-id="0613a-168">Advanced topics: Tune Hive parameters to improve query speed</span></span>
<span data-ttu-id="0613a-169">The default parameter settings of Hive cluster might not be suitable for the Hive queries and the data that the queries are processing.</span><span class="sxs-lookup"><span data-stu-id="0613a-169">The default parameter settings of Hive cluster might not be suitable for the Hive queries and the data that the queries are processing.</span></span> <span data-ttu-id="0613a-170">This section discusses some parameters that users can tune to improve the performance of Hive queries.</span><span class="sxs-lookup"><span data-stu-id="0613a-170">This section discusses some parameters that users can tune to improve the performance of Hive queries.</span></span> <span data-ttu-id="0613a-171">Users need to add the parameter tuning queries before the queries of processing data.</span><span class="sxs-lookup"><span data-stu-id="0613a-171">Users need to add the parameter tuning queries before the queries of processing data.</span></span>

1. <span data-ttu-id="0613a-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of the common errors.</span><span class="sxs-lookup"><span data-stu-id="0613a-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of the common errors.</span></span> <span data-ttu-id="0613a-173">This error can be avoided by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* to desired values.</span><span class="sxs-lookup"><span data-stu-id="0613a-173">This error can be avoided by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* to desired values.</span></span> <span data-ttu-id="0613a-174">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="0613a-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="0613a-175">This parameter allocates 4GB memory to Java heap space and also makes sorting more efficient by allocating more memory for it.</span><span class="sxs-lookup"><span data-stu-id="0613a-175">This parameter allocates 4GB memory to Java heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="0613a-176">It is a good idea to play with these allocations if there are any job failure errors related to heap space.</span><span class="sxs-lookup"><span data-stu-id="0613a-176">It is a good idea to play with these allocations if there are any job failure errors related to heap space.</span></span>

1. <span data-ttu-id="0613a-177">**DFS block size**: This parameter sets the smallest unit of data that the file system stores.</span><span class="sxs-lookup"><span data-stu-id="0613a-177">**DFS block size**: This parameter sets the smallest unit of data that the file system stores.</span></span> <span data-ttu-id="0613a-178">As an example, if the DFS block size is 128 MB, then any data of size less than and up to 128 MB is stored in a single block.</span><span class="sxs-lookup"><span data-stu-id="0613a-178">As an example, if the DFS block size is 128 MB, then any data of size less than and up to 128 MB is stored in a single block.</span></span> <span data-ttu-id="0613a-179">Data that is larger than 128 MB is allotted extra blocks.</span><span class="sxs-lookup"><span data-stu-id="0613a-179">Data that is larger than 128 MB is allotted extra blocks.</span></span> 
2. <span data-ttu-id="0613a-180">Choosing a small block size causes large overheads in Hadoop since the name node has to process many more requests to find the relevant block pertaining to the file.</span><span class="sxs-lookup"><span data-stu-id="0613a-180">Choosing a small block size causes large overheads in Hadoop since the name node has to process many more requests to find the relevant block pertaining to the file.</span></span> <span data-ttu-id="0613a-181">A recommended setting when dealing with gigabytes (or larger) data is:</span><span class="sxs-lookup"><span data-stu-id="0613a-181">A recommended setting when dealing with gigabytes (or larger) data is:</span></span>

        set dfs.block.size=128m;

2. <span data-ttu-id="0613a-182">**Optimizing join operation in Hive**: While join operations in the map/reduce framework typically take place in the reduce phase, sometimes, enormous gains can be achieved by scheduling joins in the map phase (also called "mapjoins").</span><span class="sxs-lookup"><span data-stu-id="0613a-182">**Optimizing join operation in Hive**: While join operations in the map/reduce framework typically take place in the reduce phase, sometimes, enormous gains can be achieved by scheduling joins in the map phase (also called "mapjoins").</span></span> <span data-ttu-id="0613a-183">To direct Hive to do this whenever possible, set:</span><span class="sxs-lookup"><span data-stu-id="0613a-183">To direct Hive to do this whenever possible, set:</span></span>
   
       set hive.auto.convert.join=true;

3. <span data-ttu-id="0613a-184">**Specifying the number of mappers to Hive**: While Hadoop allows the user to set the number of reducers, the number of mappers is typically not be set by the user.</span><span class="sxs-lookup"><span data-stu-id="0613a-184">**Specifying the number of mappers to Hive**: While Hadoop allows the user to set the number of reducers, the number of mappers is typically not be set by the user.</span></span> <span data-ttu-id="0613a-185">A trick that allows some degree of control on this number is to choose the Hadoop variables *mapred.min.split.size* and *mapred.max.split.size* as the size of each map task is determined by:</span><span class="sxs-lookup"><span data-stu-id="0613a-185">A trick that allows some degree of control on this number is to choose the Hadoop variables *mapred.min.split.size* and *mapred.max.split.size* as the size of each map task is determined by:</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="0613a-186">Typically, the default value of:</span><span class="sxs-lookup"><span data-stu-id="0613a-186">Typically, the default value of:</span></span>
    
    - <span data-ttu-id="0613a-187">*mapred.min.split.size* is 0, that of</span><span class="sxs-lookup"><span data-stu-id="0613a-187">*mapred.min.split.size* is 0, that of</span></span>
    - <span data-ttu-id="0613a-188">*mapred.max.split.size* is **Long.MAX** and that of</span><span class="sxs-lookup"><span data-stu-id="0613a-188">*mapred.max.split.size* is **Long.MAX** and that of</span></span> 
    - <span data-ttu-id="0613a-189">*dfs.block.size* is 64 MB.</span><span class="sxs-lookup"><span data-stu-id="0613a-189">*dfs.block.size* is 64 MB.</span></span>

    <span data-ttu-id="0613a-190">As we can see, given the data size, tuning these parameters by "setting" them allows us to tune the number of mappers used.</span><span class="sxs-lookup"><span data-stu-id="0613a-190">As we can see, given the data size, tuning these parameters by "setting" them allows us to tune the number of mappers used.</span></span>

4. <span data-ttu-id="0613a-191">Here are a few other more **advanced options** for optimizing Hive performance.</span><span class="sxs-lookup"><span data-stu-id="0613a-191">Here are a few other more **advanced options** for optimizing Hive performance.</span></span> <span data-ttu-id="0613a-192">These allow you to set the memory allocated to map and reduce tasks, and can be useful in tweaking performance.</span><span class="sxs-lookup"><span data-stu-id="0613a-192">These allow you to set the memory allocated to map and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="0613a-193">Keep in mind that the *mapreduce.reduce.memory.mb* cannot be greater than the physical memory size of each worker node in the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="0613a-193">Keep in mind that the *mapreduce.reduce.memory.mb* cannot be greater than the physical memory size of each worker node in the Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

