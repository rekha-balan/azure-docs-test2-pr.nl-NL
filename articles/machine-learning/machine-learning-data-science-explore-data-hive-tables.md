---
title: Explore data in Hive tables with Hive queries | Microsoft Docs
description: Explore data in Hive tables using Hive queries.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fe86e3be0f5ec6c02aebe35f139a0bb759fa034c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552175"
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="829b8-103">Explore data in Hive tables with Hive queries</span><span class="sxs-lookup"><span data-stu-id="829b8-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="829b8-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="829b8-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="829b8-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span><span class="sxs-lookup"><span data-stu-id="829b8-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="829b8-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="829b8-106">Prerequisites</span></span>
<span data-ttu-id="829b8-107">This article assumes that you have:</span><span class="sxs-lookup"><span data-stu-id="829b8-107">This article assumes that you have:</span></span>

* <span data-ttu-id="829b8-108">Created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="829b8-108">Created an Azure storage account.</span></span> <span data-ttu-id="829b8-109">If you need instructions, see [Create an Azure Storage account](../storage/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="829b8-109">If you need instructions, see [Create an Azure Storage account](../storage/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="829b8-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span><span class="sxs-lookup"><span data-stu-id="829b8-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="829b8-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="829b8-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="829b8-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="829b8-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="829b8-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span><span class="sxs-lookup"><span data-stu-id="829b8-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="829b8-114">Enabled remote access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="829b8-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="829b8-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="829b8-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="829b8-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="829b8-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="829b8-117">Example Hive query scripts for data exploration</span><span class="sxs-lookup"><span data-stu-id="829b8-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="829b8-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="829b8-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="829b8-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="829b8-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="829b8-120">Get the levels in a categorical column</span><span class="sxs-lookup"><span data-stu-id="829b8-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="829b8-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="829b8-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="829b8-122">Get the distribution for numerical columns</span><span class="sxs-lookup"><span data-stu-id="829b8-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="829b8-123">Extract records from joining two tables</span><span class="sxs-lookup"><span data-stu-id="829b8-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="829b8-124">Additional query scripts for taxi trip data scenarios</span><span class="sxs-lookup"><span data-stu-id="829b8-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="829b8-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="829b8-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="829b8-126">These queries already have data schema specified and are ready to be submitted to run.</span><span class="sxs-lookup"><span data-stu-id="829b8-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

