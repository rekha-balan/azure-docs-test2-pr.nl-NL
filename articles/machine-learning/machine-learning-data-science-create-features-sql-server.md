---
title: Create features for data in SQL Server using SQL and Python | Microsoft Docs
description: Process Data from SQL Azure
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: ''
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 75b0f01d941c8a0a4f698d1416e1bd322b14db8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555058"
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="3414a-103">Create features for data in SQL Server using SQL and Python</span><span class="sxs-lookup"><span data-stu-id="3414a-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="3414a-104">This document shows how to generate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from the data.</span><span class="sxs-lookup"><span data-stu-id="3414a-104">This document shows how to generate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from the data.</span></span> <span data-ttu-id="3414a-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span><span class="sxs-lookup"><span data-stu-id="3414a-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="3414a-106">This **menu** links to topics that describe how to create features for data in various environments.</span><span class="sxs-lookup"><span data-stu-id="3414a-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="3414a-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="3414a-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="3414a-108">For a practical example, you can consult the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span><span class="sxs-lookup"><span data-stu-id="3414a-108">For a practical example, you can consult the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3414a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3414a-109">Prerequisites</span></span>
<span data-ttu-id="3414a-110">This article assumes that you have:</span><span class="sxs-lookup"><span data-stu-id="3414a-110">This article assumes that you have:</span></span>

* <span data-ttu-id="3414a-111">Created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="3414a-111">Created an Azure storage account.</span></span> <span data-ttu-id="3414a-112">If you need instructions, see [Create an Azure Storage account](../storage/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="3414a-112">If you need instructions, see [Create an Azure Storage account](../storage/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="3414a-113">Stored your data in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3414a-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="3414a-114">If you have not, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how to move the data there.</span><span class="sxs-lookup"><span data-stu-id="3414a-114">If you have not, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how to move the data there.</span></span>

## <a name="sql-featuregen"></a><span data-ttu-id="3414a-115">Feature Generation with SQL</span><span class="sxs-lookup"><span data-stu-id="3414a-115">Feature Generation with SQL</span></span>
<span data-ttu-id="3414a-116">In this section, we describe ways of generating features using SQL:</span><span class="sxs-lookup"><span data-stu-id="3414a-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="3414a-117">Count based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="3414a-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="3414a-118">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="3414a-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="3414a-119">Rolling out the features from a single column</span><span class="sxs-lookup"><span data-stu-id="3414a-119">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="3414a-120">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span><span class="sxs-lookup"><span data-stu-id="3414a-120">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span>
> 
> 

### <a name="sql-countfeature"></a><span data-ttu-id="3414a-121">Count based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="3414a-121">Count based Feature Generation</span></span>
<span data-ttu-id="3414a-122">This document demonstrates two ways of generating count features.</span><span class="sxs-lookup"><span data-stu-id="3414a-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="3414a-123">The first method uses conditional sum and the second method uses the 'where\` clause.</span><span class="sxs-lookup"><span data-stu-id="3414a-123">The first method uses conditional sum and the second method uses the 'where\` clause.</span></span> <span data-ttu-id="3414a-124">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span><span class="sxs-lookup"><span data-stu-id="3414a-124">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a><span data-ttu-id="3414a-125">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="3414a-125">Binning Feature Generation</span></span>
<span data-ttu-id="3414a-126">The following example shows how to generate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span><span class="sxs-lookup"><span data-stu-id="3414a-126">The following example shows how to generate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a><span data-ttu-id="3414a-127">Rolling out the features from a single column</span><span class="sxs-lookup"><span data-stu-id="3414a-127">Rolling out the features from a single column</span></span>
<span data-ttu-id="3414a-128">In this section, we demonstrate how to roll-out a single column in a table to generate additional features.</span><span class="sxs-lookup"><span data-stu-id="3414a-128">In this section, we demonstrate how to roll-out a single column in a table to generate additional features.</span></span> <span data-ttu-id="3414a-129">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span><span class="sxs-lookup"><span data-stu-id="3414a-129">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="3414a-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="3414a-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="3414a-131">This is useful to understand before featurizing the location field:</span><span class="sxs-lookup"><span data-stu-id="3414a-131">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="3414a-132">The sign tells us whether we are north or south, east or west on the globe.</span><span class="sxs-lookup"><span data-stu-id="3414a-132">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="3414a-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span><span class="sxs-lookup"><span data-stu-id="3414a-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="3414a-134">The tens digit gives a position to about 1,000 kilometers.</span><span class="sxs-lookup"><span data-stu-id="3414a-134">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="3414a-135">It gives us useful information about what continent or ocean we are on.</span><span class="sxs-lookup"><span data-stu-id="3414a-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="3414a-136">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span><span class="sxs-lookup"><span data-stu-id="3414a-136">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="3414a-137">It can tell us roughly what large state or country we are in.</span><span class="sxs-lookup"><span data-stu-id="3414a-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="3414a-138">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span><span class="sxs-lookup"><span data-stu-id="3414a-138">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="3414a-139">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span><span class="sxs-lookup"><span data-stu-id="3414a-139">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="3414a-140">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span><span class="sxs-lookup"><span data-stu-id="3414a-140">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="3414a-141">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span><span class="sxs-lookup"><span data-stu-id="3414a-141">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="3414a-142">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span><span class="sxs-lookup"><span data-stu-id="3414a-142">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="3414a-143">The fifth decimal place is worth up to 1.1 m: it distinguish trees from each other.</span><span class="sxs-lookup"><span data-stu-id="3414a-143">The fifth decimal place is worth up to 1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="3414a-144">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span><span class="sxs-lookup"><span data-stu-id="3414a-144">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="3414a-145">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span><span class="sxs-lookup"><span data-stu-id="3414a-145">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="3414a-146">It should be more than good enough for tracking movements of glaciers and rivers.</span><span class="sxs-lookup"><span data-stu-id="3414a-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="3414a-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span><span class="sxs-lookup"><span data-stu-id="3414a-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="3414a-148">The location information can can be featurized as follows, separating out region, location and city information.</span><span class="sxs-lookup"><span data-stu-id="3414a-148">The location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="3414a-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` to get the region/district information.</span><span class="sxs-lookup"><span data-stu-id="3414a-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` to get the region/district information.</span></span>

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

<span data-ttu-id="3414a-150">The above location based features can be further used to generate additional count features as described earlier.</span><span class="sxs-lookup"><span data-stu-id="3414a-150">The above location based features can be further used to generate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="3414a-151">You can programmatically insert the records using your language of choice.</span><span class="sxs-lookup"><span data-stu-id="3414a-151">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="3414a-152">You may need to insert the data in chunks to improve write efficiency [Check out the example of how to do this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="3414a-152">You may need to insert the data in chunks to improve write efficiency [Check out the example of how to do this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="3414a-153">Another alternative is to insert data in the database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="3414a-153">Another alternative is to insert data in the database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <a name="sql-aml"></a><span data-ttu-id="3414a-154">Connecting to Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3414a-154">Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="3414a-155">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span><span class="sxs-lookup"><span data-stu-id="3414a-155">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="3414a-156">Features can be generated or accessed if already created, using the [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span><span class="sxs-lookup"><span data-stu-id="3414a-156">Features can be generated or accessed if already created, using the [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![azureml readers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a><span data-ttu-id="3414a-158">Using a programming language like Python</span><span class="sxs-lookup"><span data-stu-id="3414a-158">Using a programming language like Python</span></span>
<span data-ttu-id="3414a-159">Using Python to generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="3414a-159">Using Python to generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="3414a-160">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span><span class="sxs-lookup"><span data-stu-id="3414a-160">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="3414a-161">We document the process of connecting to the database and loading the data into the data frame in this section.</span><span class="sxs-lookup"><span data-stu-id="3414a-161">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="3414a-162">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span><span class="sxs-lookup"><span data-stu-id="3414a-162">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="3414a-163">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span><span class="sxs-lookup"><span data-stu-id="3414a-163">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="3414a-164">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span><span class="sxs-lookup"><span data-stu-id="3414a-164">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="3414a-165">Now you can work with the Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="3414a-165">Now you can work with the Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>


