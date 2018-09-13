---
title: Extend U-SQL scripts with Python in Azure Data Lake Analytics | Microsoft Docs
description: Learn how to run Python code in U-SQL Scripts
services: data-lake-analytics
documentationcenter: ''
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: b3a9434df566d391e50e7755f9ab7fa880fe1d53
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555214"
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="f715f-103">Tutorial: Get started with extending U-SQL with Python</span><span class="sxs-lookup"><span data-stu-id="f715f-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="f715f-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span><span class="sxs-lookup"><span data-stu-id="f715f-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span></span> <span data-ttu-id="f715f-105">The following example illustrates the basic steps:</span><span class="sxs-lookup"><span data-stu-id="f715f-105">The following example illustrates the basic steps:</span></span>

* <span data-ttu-id="f715f-106">Use the REFERENCE ASSEMBLY statement to enable Python extensions for the U-SQL Script</span><span class="sxs-lookup"><span data-stu-id="f715f-106">Use the REFERENCE ASSEMBLY statement to enable Python extensions for the U-SQL Script</span></span>
* <span data-ttu-id="f715f-107">Using the REDUCE operation to partition the input data on a key</span><span class="sxs-lookup"><span data-stu-id="f715f-107">Using the REDUCE operation to partition the input data on a key</span></span>
* <span data-ttu-id="f715f-108">The Python extensions for U-SQL include a built-in reducer (Extension.Python.Reducer) that runs Python code on each vertex assigned to the reducer</span><span class="sxs-lookup"><span data-stu-id="f715f-108">The Python extensions for U-SQL include a built-in reducer (Extension.Python.Reducer) that runs Python code on each vertex assigned to the reducer</span></span>
* <span data-ttu-id="f715f-109">The U-SQL script contains the embedded Python code that has a function called usqlml_main that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span><span class="sxs-lookup"><span data-stu-id="f715f-109">The U-SQL script contains the embedded Python code that has a function called usqlml_main that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="f715f-110">How Python Integrates with U-SQL</span><span class="sxs-lookup"><span data-stu-id="f715f-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="f715f-111">Datatypes</span><span class="sxs-lookup"><span data-stu-id="f715f-111">Datatypes</span></span>

* <span data-ttu-id="f715f-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span><span class="sxs-lookup"><span data-stu-id="f715f-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="f715f-113">U-SQL Nulls are converted to and from Pandas "NA" values</span><span class="sxs-lookup"><span data-stu-id="f715f-113">U-SQL Nulls are converted to and from Pandas "NA" values</span></span>

### <a name="schemas"></a><span data-ttu-id="f715f-114">Schemas</span><span class="sxs-lookup"><span data-stu-id="f715f-114">Schemas</span></span>

* <span data-ttu-id="f715f-115">Index vectors in Pandas are not supported in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f715f-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="f715f-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span><span class="sxs-lookup"><span data-stu-id="f715f-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span></span> 
* <span data-ttu-id="f715f-117">U-SQL datasets cannot have duplicate column names</span><span class="sxs-lookup"><span data-stu-id="f715f-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="f715f-118">U-SQL datasets column names that are not strings.</span><span class="sxs-lookup"><span data-stu-id="f715f-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="f715f-119">Python Versions</span><span class="sxs-lookup"><span data-stu-id="f715f-119">Python Versions</span></span>
<span data-ttu-id="f715f-120">Only Python 3.5.1 (compiled for Windows) is supported.</span><span class="sxs-lookup"><span data-stu-id="f715f-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="f715f-121">Standard Python modules</span><span class="sxs-lookup"><span data-stu-id="f715f-121">Standard Python modules</span></span>
<span data-ttu-id="f715f-122">All the standard Python modules are included.</span><span class="sxs-lookup"><span data-stu-id="f715f-122">All the standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="f715f-123">Additional Python modules</span><span class="sxs-lookup"><span data-stu-id="f715f-123">Additional Python modules</span></span>
<span data-ttu-id="f715f-124">Besides the standard Python libraries, several commonly used python libraries are included:</span><span class="sxs-lookup"><span data-stu-id="f715f-124">Besides the standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="f715f-125">Exception Messages</span><span class="sxs-lookup"><span data-stu-id="f715f-125">Exception Messages</span></span>
<span data-ttu-id="f715f-126">Currently, an exception in Python code shows up as generic vertex failure.</span><span class="sxs-lookup"><span data-stu-id="f715f-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="f715f-127">In the future, the U-SQL Job error messages will display the Python exception message.</span><span class="sxs-lookup"><span data-stu-id="f715f-127">In the future, the U-SQL Job error messages will display the Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="f715f-128">Input and Output size limitations</span><span class="sxs-lookup"><span data-stu-id="f715f-128">Input and Output size limitations</span></span>
<span data-ttu-id="f715f-129">Every vertex has a limited amount of memory assigned to it.</span><span class="sxs-lookup"><span data-stu-id="f715f-129">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="f715f-130">Currently, that limit is 6 GB for an AU.</span><span class="sxs-lookup"><span data-stu-id="f715f-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="f715f-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span><span class="sxs-lookup"><span data-stu-id="f715f-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="f715f-132">See also</span><span class="sxs-lookup"><span data-stu-id="f715f-132">See also</span></span>
* [<span data-ttu-id="f715f-133">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f715f-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f715f-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f715f-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="f715f-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="f715f-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

