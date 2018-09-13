---
title: Create features for data in SQL Server using SQL and Python | Microsoft Docs
description: Process Data from SQL Azure
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: ''
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/21/2017
ms.author: deguhath
ms.openlocfilehash: eb81d6726b083d864a58b6c11eed67f95aeda350
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871032"
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="a7666-103">Create features for data in SQL Server using SQL and Python</span><span class="sxs-lookup"><span data-stu-id="a7666-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="a7666-104">This document shows how to generate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from the data.</span><span class="sxs-lookup"><span data-stu-id="a7666-104">This document shows how to generate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from the data.</span></span> <span data-ttu-id="a7666-105">You can use SQL or a programming language like Python to accomplish this task.</span><span class="sxs-lookup"><span data-stu-id="a7666-105">You can use SQL or a programming language like Python to accomplish this task.</span></span> <span data-ttu-id="a7666-106">Both approaches are demonstrated here.</span><span class="sxs-lookup"><span data-stu-id="a7666-106">Both approaches are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../../includes/cap-create-features-selector.md)]

<span data-ttu-id="a7666-107">This **menu** links to topics that describe how to create features for data in various environments.</span><span class="sxs-lookup"><span data-stu-id="a7666-107">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="a7666-108">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="a7666-108">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="a7666-109">For a practical example, you can consult the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span><span class="sxs-lookup"><span data-stu-id="a7666-109">For a practical example, you can consult the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a7666-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7666-110">Prerequisites</span></span>
<span data-ttu-id="a7666-111">This article assumes that you have:</span><span class="sxs-lookup"><span data-stu-id="a7666-111">This article assumes that you have:</span></span>

* <span data-ttu-id="a7666-112">Created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a7666-112">Created an Azure storage account.</span></span> <span data-ttu-id="a7666-113">If you need instructions, see [Create an Azure Storage account](../../storage/common/storage-quickstart-create-account.md)</span><span class="sxs-lookup"><span data-stu-id="a7666-113">If you need instructions, see [Create an Azure Storage account](../../storage/common/storage-quickstart-create-account.md)</span></span>
* <span data-ttu-id="a7666-114">Stored your data in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a7666-114">Stored your data in SQL Server.</span></span> <span data-ttu-id="a7666-115">If you have not, see [Move data to an Azure SQL Database for Azure Machine Learning](move-sql-azure.md) for instructions on how to move the data there.</span><span class="sxs-lookup"><span data-stu-id="a7666-115">If you have not, see [Move data to an Azure SQL Database for Azure Machine Learning](move-sql-azure.md) for instructions on how to move the data there.</span></span>

## <a name="sql-featuregen"></a><span data-ttu-id="a7666-116">Feature generation with SQL</span><span class="sxs-lookup"><span data-stu-id="a7666-116">Feature generation with SQL</span></span>
<span data-ttu-id="a7666-117">In this section, we describe ways of generating features using SQL:</span><span class="sxs-lookup"><span data-stu-id="a7666-117">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="a7666-118">Count based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="a7666-118">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="a7666-119">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="a7666-119">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="a7666-120">Rolling out the features from a single column</span><span class="sxs-lookup"><span data-stu-id="a7666-120">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="a7666-121">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span><span class="sxs-lookup"><span data-stu-id="a7666-121">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span>
> 
> 

### <a name="sql-countfeature"></a><span data-ttu-id="a7666-122">Count based feature generation</span><span class="sxs-lookup"><span data-stu-id="a7666-122">Count based feature generation</span></span>
<span data-ttu-id="a7666-123">This document demonstrates two ways of generating count features.</span><span class="sxs-lookup"><span data-stu-id="a7666-123">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="a7666-124">The first method uses conditional sum and the second method uses the 'where\` clause.</span><span class="sxs-lookup"><span data-stu-id="a7666-124">The first method uses conditional sum and the second method uses the 'where\` clause.</span></span> <span data-ttu-id="a7666-125">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span><span class="sxs-lookup"><span data-stu-id="a7666-125">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a><span data-ttu-id="a7666-126">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="a7666-126">Binning Feature Generation</span></span>
<span data-ttu-id="a7666-127">The following example shows how to generate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span><span class="sxs-lookup"><span data-stu-id="a7666-127">The following example shows how to generate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a><span data-ttu-id="a7666-128">Rolling out the features from a single column</span><span class="sxs-lookup"><span data-stu-id="a7666-128">Rolling out the features from a single column</span></span>
<span data-ttu-id="a7666-129">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span><span class="sxs-lookup"><span data-stu-id="a7666-129">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="a7666-130">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span><span class="sxs-lookup"><span data-stu-id="a7666-130">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="a7666-131">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="a7666-131">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="a7666-132">Here are some useful things to understand about location data before creating features from the field:</span><span class="sxs-lookup"><span data-stu-id="a7666-132">Here are some useful things to understand about location data before creating features from the field:</span></span>

* <span data-ttu-id="a7666-133">The sign indicates whether we are north or south, east or west on the globe.</span><span class="sxs-lookup"><span data-stu-id="a7666-133">The sign indicates whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="a7666-134">A nonzero hundreds digit indicates longitude, not latitude is being used.</span><span class="sxs-lookup"><span data-stu-id="a7666-134">A nonzero hundreds digit indicates longitude, not latitude is being used.</span></span>
* <span data-ttu-id="a7666-135">The tens digit gives a position to about 1,000 kilometers.</span><span class="sxs-lookup"><span data-stu-id="a7666-135">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="a7666-136">It gives useful information about what continent or ocean we are on.</span><span class="sxs-lookup"><span data-stu-id="a7666-136">It gives useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="a7666-137">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span><span class="sxs-lookup"><span data-stu-id="a7666-137">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="a7666-138">It indicates, roughly, what large state or country we are in.</span><span class="sxs-lookup"><span data-stu-id="a7666-138">It indicates, roughly, what large state or country we are in.</span></span>
* <span data-ttu-id="a7666-139">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span><span class="sxs-lookup"><span data-stu-id="a7666-139">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="a7666-140">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span><span class="sxs-lookup"><span data-stu-id="a7666-140">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="a7666-141">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span><span class="sxs-lookup"><span data-stu-id="a7666-141">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="a7666-142">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span><span class="sxs-lookup"><span data-stu-id="a7666-142">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="a7666-143">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span><span class="sxs-lookup"><span data-stu-id="a7666-143">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="a7666-144">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span><span class="sxs-lookup"><span data-stu-id="a7666-144">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="a7666-145">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span><span class="sxs-lookup"><span data-stu-id="a7666-145">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="a7666-146">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span><span class="sxs-lookup"><span data-stu-id="a7666-146">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="a7666-147">It should be more than good enough for tracking movements of glaciers and rivers.</span><span class="sxs-lookup"><span data-stu-id="a7666-147">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="a7666-148">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span><span class="sxs-lookup"><span data-stu-id="a7666-148">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="a7666-149">The location information can be featurized by separating out region, location, and city information.</span><span class="sxs-lookup"><span data-stu-id="a7666-149">The location information can be featurized by separating out region, location, and city information.</span></span> <span data-ttu-id="a7666-150">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` to get the region/district information.</span><span class="sxs-lookup"><span data-stu-id="a7666-150">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` to get the region/district information.</span></span>

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

<span data-ttu-id="a7666-151">These location based features can be further used to generate additional count features as described earlier.</span><span class="sxs-lookup"><span data-stu-id="a7666-151">These location based features can be further used to generate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="a7666-152">You can programmatically insert the records using your language of choice.</span><span class="sxs-lookup"><span data-stu-id="a7666-152">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="a7666-153">You may need to insert the data in chunks to improve write efficiency.</span><span class="sxs-lookup"><span data-stu-id="a7666-153">You may need to insert the data in chunks to improve write efficiency.</span></span> <span data-ttu-id="a7666-154">[Here is an example of how to do this using pyodbc](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="a7666-154">[Here is an example of how to do this using pyodbc](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="a7666-155">Another alternative is to insert data in the database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="a7666-155">Another alternative is to insert data in the database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <a name="sql-aml"></a><span data-ttu-id="a7666-156">Connecting to Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a7666-156">Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="a7666-157">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span><span class="sxs-lookup"><span data-stu-id="a7666-157">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="a7666-158">Features can be generated or accessed if already created, using the [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span><span class="sxs-lookup"><span data-stu-id="a7666-158">Features can be generated or accessed if already created, using the [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![Azure ML readers](./media/sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a><span data-ttu-id="a7666-160">Using a programming language like Python</span><span class="sxs-lookup"><span data-stu-id="a7666-160">Using a programming language like Python</span></span>
<span data-ttu-id="a7666-161">Using Python to generate features when the data is in SQL Server is similar to processing data in Azure blob using Python.</span><span class="sxs-lookup"><span data-stu-id="a7666-161">Using Python to generate features when the data is in SQL Server is similar to processing data in Azure blob using Python.</span></span> <span data-ttu-id="a7666-162">For comparison, see [Process Azure Blob data in your data science environment](data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a7666-162">For comparison, see [Process Azure Blob data in your data science environment](data-blob.md).</span></span> <span data-ttu-id="a7666-163">Load the data from the database into a pandas data frame to process it further.</span><span class="sxs-lookup"><span data-stu-id="a7666-163">Load the data from the database into a pandas data frame to process it further.</span></span> <span data-ttu-id="a7666-164">The process of connecting to the database and loading the data into the data frame is documented in this section.</span><span class="sxs-lookup"><span data-stu-id="a7666-164">The process of connecting to the database and loading the data into the data frame is documented in this section.</span></span>

<span data-ttu-id="a7666-165">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span><span class="sxs-lookup"><span data-stu-id="a7666-165">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="a7666-166">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span><span class="sxs-lookup"><span data-stu-id="a7666-166">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="a7666-167">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span><span class="sxs-lookup"><span data-stu-id="a7666-167">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="a7666-168">Now you can work with the Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a7666-168">Now you can work with the Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](create-features-blob.md).</span></span>

