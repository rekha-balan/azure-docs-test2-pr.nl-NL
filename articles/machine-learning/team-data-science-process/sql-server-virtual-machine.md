---
title: Explore data in a SQL Server virtual machine on Azure | Microsoft Docs
description: Explore data and generate features in a SQL Server virtual machine on Azure
services: machine-learning
documentationcenter: ''
author: deguhath
manager: jhubbard
editor: ''
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: deguhath
ms.openlocfilehash: 39bdbce4ada225c0fa7df8559f68b591ccfc68b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864916"
---
# <a name="heading"></a><span data-ttu-id="98025-103">Process Data in SQL Server Virtual Machine on Azure</span><span class="sxs-lookup"><span data-stu-id="98025-103">Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="98025-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span><span class="sxs-lookup"><span data-stu-id="98025-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="98025-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span><span class="sxs-lookup"><span data-stu-id="98025-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="98025-106">The sample SQL statements in this document assume that data is in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98025-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="98025-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98025-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <a name="SQL"></a><span data-ttu-id="98025-108">Using SQL</span><span class="sxs-lookup"><span data-stu-id="98025-108">Using SQL</span></span>
<span data-ttu-id="98025-109">We describe the following data wrangling tasks in this section using SQL:</span><span class="sxs-lookup"><span data-stu-id="98025-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="98025-110">Data Exploration</span><span class="sxs-lookup"><span data-stu-id="98025-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="98025-111">Feature Generation</span><span class="sxs-lookup"><span data-stu-id="98025-111">Feature Generation</span></span>](#sql-featuregen)

### <a name="sql-dataexploration"></a><span data-ttu-id="98025-112">Data Exploration</span><span class="sxs-lookup"><span data-stu-id="98025-112">Data Exploration</span></span>
<span data-ttu-id="98025-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98025-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="98025-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span><span class="sxs-lookup"><span data-stu-id="98025-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="98025-115">Get the count of observations per day</span><span class="sxs-lookup"><span data-stu-id="98025-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="98025-116">Get the levels in a categorical column</span><span class="sxs-lookup"><span data-stu-id="98025-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="98025-117">Get the number of levels in combination of two categorical columns</span><span class="sxs-lookup"><span data-stu-id="98025-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="98025-118">Get the distribution for numerical columns</span><span class="sxs-lookup"><span data-stu-id="98025-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a><span data-ttu-id="98025-119">Feature Generation</span><span class="sxs-lookup"><span data-stu-id="98025-119">Feature Generation</span></span>
<span data-ttu-id="98025-120">In this section, we describe ways of generating features using SQL:</span><span class="sxs-lookup"><span data-stu-id="98025-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="98025-121">Count based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="98025-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="98025-122">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="98025-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="98025-123">Rolling out the features from a single column</span><span class="sxs-lookup"><span data-stu-id="98025-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="98025-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span><span class="sxs-lookup"><span data-stu-id="98025-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <a name="sql-countfeature"></a><span data-ttu-id="98025-125">Count based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="98025-125">Count based Feature Generation</span></span>
<span data-ttu-id="98025-126">The following examples demonstrate two ways of generating count features.</span><span class="sxs-lookup"><span data-stu-id="98025-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="98025-127">The first method uses conditional sum and the second method uses the 'where' clause.</span><span class="sxs-lookup"><span data-stu-id="98025-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="98025-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span><span class="sxs-lookup"><span data-stu-id="98025-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a><span data-ttu-id="98025-129">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="98025-129">Binning Feature Generation</span></span>
<span data-ttu-id="98025-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span><span class="sxs-lookup"><span data-stu-id="98025-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a><span data-ttu-id="98025-131">Rolling out the features from a single column</span><span class="sxs-lookup"><span data-stu-id="98025-131">Rolling out the features from a single column</span></span>
<span data-ttu-id="98025-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span><span class="sxs-lookup"><span data-stu-id="98025-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="98025-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span><span class="sxs-lookup"><span data-stu-id="98025-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="98025-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="98025-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="98025-135">This is useful to understand before featurizing the location field:</span><span class="sxs-lookup"><span data-stu-id="98025-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="98025-136">The sign tells us whether we are north or south, east or west on the globe.</span><span class="sxs-lookup"><span data-stu-id="98025-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="98025-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span><span class="sxs-lookup"><span data-stu-id="98025-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="98025-138">The tens digit gives a position to about 1,000 kilometers.</span><span class="sxs-lookup"><span data-stu-id="98025-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="98025-139">It gives us useful information about what continent or ocean we are on.</span><span class="sxs-lookup"><span data-stu-id="98025-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="98025-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span><span class="sxs-lookup"><span data-stu-id="98025-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="98025-141">It can tell us roughly what large state or country we are in.</span><span class="sxs-lookup"><span data-stu-id="98025-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="98025-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span><span class="sxs-lookup"><span data-stu-id="98025-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="98025-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span><span class="sxs-lookup"><span data-stu-id="98025-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="98025-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span><span class="sxs-lookup"><span data-stu-id="98025-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="98025-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span><span class="sxs-lookup"><span data-stu-id="98025-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="98025-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span><span class="sxs-lookup"><span data-stu-id="98025-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="98025-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span><span class="sxs-lookup"><span data-stu-id="98025-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="98025-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span><span class="sxs-lookup"><span data-stu-id="98025-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="98025-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span><span class="sxs-lookup"><span data-stu-id="98025-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="98025-150">It should be more than good enough for tracking movements of glaciers and rivers.</span><span class="sxs-lookup"><span data-stu-id="98025-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="98025-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span><span class="sxs-lookup"><span data-stu-id="98025-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="98025-152">The location information can be featurized as follows, separating out region, location, and city information.</span><span class="sxs-lookup"><span data-stu-id="98025-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="98025-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span><span class="sxs-lookup"><span data-stu-id="98025-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="98025-154">These location-based features can be further used to generate additional count features as described earlier.</span><span class="sxs-lookup"><span data-stu-id="98025-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="98025-155">You can programmatically insert the records using your language of choice.</span><span class="sxs-lookup"><span data-stu-id="98025-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="98025-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="98025-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="98025-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="98025-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <a name="sql-aml"></a><span data-ttu-id="98025-158">Connecting to Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="98025-158">Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="98025-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span><span class="sxs-lookup"><span data-stu-id="98025-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="98025-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span><span class="sxs-lookup"><span data-stu-id="98025-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml readers][1] 

## <a name="python"></a><span data-ttu-id="98025-162">Using a programming language like Python</span><span class="sxs-lookup"><span data-stu-id="98025-162">Using a programming language like Python</span></span>
<span data-ttu-id="98025-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="98025-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](data-blob.md).</span></span> <span data-ttu-id="98025-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span><span class="sxs-lookup"><span data-stu-id="98025-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="98025-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span><span class="sxs-lookup"><span data-stu-id="98025-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="98025-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span><span class="sxs-lookup"><span data-stu-id="98025-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="98025-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span><span class="sxs-lookup"><span data-stu-id="98025-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="98025-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span><span class="sxs-lookup"><span data-stu-id="98025-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="98025-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="98025-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="98025-170">Azure Data Science in Action Example</span><span class="sxs-lookup"><span data-stu-id="98025-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="98025-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="98025-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](sql-walkthrough.md).</span></span>

[1]: ./media/sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

