---
title: Sample data in Azure HDInsight Hive tables | Microsoft Docs
description: Down sampling data in Azure HDInsight  (Hadopop) Hive Tables
services: machine-learning,hdinsight
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 558f7d684453c8b5040f586820bd2a8a9ac0f9c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871522"
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="33b02-103">Sample data in Azure HDInsight Hive tables</span><span class="sxs-lookup"><span data-stu-id="33b02-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="33b02-104">This article describes how to down-sample data stored in Azure HDInsight Hive tables using Hive queries to reduce it to a size more manageable for analysis.</span><span class="sxs-lookup"><span data-stu-id="33b02-104">This article describes how to down-sample data stored in Azure HDInsight Hive tables using Hive queries to reduce it to a size more manageable for analysis.</span></span> <span data-ttu-id="33b02-105">It cover three popularly used sampling methods:</span><span class="sxs-lookup"><span data-stu-id="33b02-105">It cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="33b02-106">Uniform random sampling</span><span class="sxs-lookup"><span data-stu-id="33b02-106">Uniform random sampling</span></span>
* <span data-ttu-id="33b02-107">Random sampling by groups</span><span class="sxs-lookup"><span data-stu-id="33b02-107">Random sampling by groups</span></span>
* <span data-ttu-id="33b02-108">Stratified sampling</span><span class="sxs-lookup"><span data-stu-id="33b02-108">Stratified sampling</span></span>

<span data-ttu-id="33b02-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span><span class="sxs-lookup"><span data-stu-id="33b02-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="33b02-110">**Why sample your data?**</span><span class="sxs-lookup"><span data-stu-id="33b02-110">**Why sample your data?**</span></span>
<span data-ttu-id="33b02-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span><span class="sxs-lookup"><span data-stu-id="33b02-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="33b02-112">Down-sampling facilitates data understanding, exploration, and feature engineering.</span><span class="sxs-lookup"><span data-stu-id="33b02-112">Down-sampling facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="33b02-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span><span class="sxs-lookup"><span data-stu-id="33b02-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="33b02-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="33b02-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-to-submit-hive-queries"></a><span data-ttu-id="33b02-115">How to submit Hive queries</span><span class="sxs-lookup"><span data-stu-id="33b02-115">How to submit Hive queries</span></span>
<span data-ttu-id="33b02-116">Hive queries can be submitted from the Hadoop Command-Line console on the head node of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="33b02-116">Hive queries can be submitted from the Hadoop Command-Line console on the head node of the Hadoop cluster.</span></span> <span data-ttu-id="33b02-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command-Line console, and submit the Hive queries from there.</span><span class="sxs-lookup"><span data-stu-id="33b02-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command-Line console, and submit the Hive queries from there.</span></span> <span data-ttu-id="33b02-118">For instructions on submitting Hive queries in the Hadoop Command-Line console, see [How to Submit Hive Queries](move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="33b02-118">For instructions on submitting Hive queries in the Hadoop Command-Line console, see [How to Submit Hive Queries](move-hive-tables.md#submit).</span></span>

## <a name="uniform"></a> <span data-ttu-id="33b02-119">Uniform random sampling</span><span class="sxs-lookup"><span data-stu-id="33b02-119">Uniform random sampling</span></span>
<span data-ttu-id="33b02-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span><span class="sxs-lookup"><span data-stu-id="33b02-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span></span> <span data-ttu-id="33b02-121">It can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span><span class="sxs-lookup"><span data-stu-id="33b02-121">It can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="33b02-122">Here is an example query:</span><span class="sxs-lookup"><span data-stu-id="33b02-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="33b02-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span><span class="sxs-lookup"><span data-stu-id="33b02-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span></span>

## <a name="group"></a> <span data-ttu-id="33b02-124">Random sampling by groups</span><span class="sxs-lookup"><span data-stu-id="33b02-124">Random sampling by groups</span></span>
<span data-ttu-id="33b02-125">When sampling categorical data, you may want to either include or exclude all of the instances for some value of the categorical variable.</span><span class="sxs-lookup"><span data-stu-id="33b02-125">When sampling categorical data, you may want to either include or exclude all of the instances for some value of the categorical variable.</span></span> <span data-ttu-id="33b02-126">This sort of sampling is called "sampling by group".</span><span class="sxs-lookup"><span data-stu-id="33b02-126">This sort of sampling is called "sampling by group".</span></span> <span data-ttu-id="33b02-127">For example, if you have a categorical variable "*State*", which has values such as NY, MA, CA, NJ, and PA, you want records from each state to be together, whether they are sampled or not.</span><span class="sxs-lookup"><span data-stu-id="33b02-127">For example, if you have a categorical variable "*State*", which has values such as NY, MA, CA, NJ, and PA, you want records from each state to be together, whether they are sampled or not.</span></span>

<span data-ttu-id="33b02-128">Here is an example query that samples by group:</span><span class="sxs-lookup"><span data-stu-id="33b02-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a><span data-ttu-id="33b02-129">Stratified sampling</span><span class="sxs-lookup"><span data-stu-id="33b02-129">Stratified sampling</span></span>
<span data-ttu-id="33b02-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have categorical values that are present in the same ratio as they were in the parent population.</span><span class="sxs-lookup"><span data-stu-id="33b02-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have categorical values that are present in the same ratio as they were in the parent population.</span></span> <span data-ttu-id="33b02-131">Using the same example as above, suppose your data has the following observations by states: NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span><span class="sxs-lookup"><span data-stu-id="33b02-131">Using the same example as above, suppose your data has the following observations by states: NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="33b02-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span><span class="sxs-lookup"><span data-stu-id="33b02-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="33b02-133">Here is an example query:</span><span class="sxs-lookup"><span data-stu-id="33b02-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="33b02-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="33b02-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

