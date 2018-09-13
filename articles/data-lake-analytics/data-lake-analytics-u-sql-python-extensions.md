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
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Tutorial: Get started with extending U-SQL with Python

Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code. The following example illustrates the basic steps:

* Use the REFERENCE ASSEMBLY statement to enable Python extensions for the U-SQL Script
* Using the REDUCE operation to partition the input data on a key
* The Python extensions for U-SQL include a built-in reducer (Extension.Python.Reducer) that runs Python code on each vertex assigned to the reducer
* The U-SQL script contains the embedded Python code that has a function called usqlml_main that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.

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

## <a name="how-python-integrates-with-u-sql"></a>How Python Integrates with U-SQL

### <a name="datatypes"></a>Datatypes

* String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL
* U-SQL Nulls are converted to and from Pandas "NA" values

### <a name="schemas"></a>Schemas

* Index vectors in Pandas are not supported in U-SQL. All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1. 
* U-SQL datasets cannot have duplicate column names
* U-SQL datasets column names that are not strings. 

### <a name="python-versions"></a>Python Versions
Only Python 3.5.1 (compiled for Windows) is supported. 

### <a name="standard-python-modules"></a>Standard Python modules
All the standard Python modules are included.

### <a name="additional-python-modules"></a>Additional Python modules
Besides the standard Python libraries, several commonly used python libraries are included:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Exception Messages
Currently, an exception in Python code shows up as generic vertex failure. In the future, the U-SQL Job error messages will display the Python exception message.

### <a name="input-and-output-size-limitations"></a>Input and Output size limitations
Every vertex has a limited amount of memory assigned to it. Currently, that limit is 6 GB for an AU. Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.

## <a name="see-also"></a>See also
* [Overview of Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Using U-SQL window functions for Azure Data Lake Analytics jobs](data-lake-analytics-use-window-functions.md)

