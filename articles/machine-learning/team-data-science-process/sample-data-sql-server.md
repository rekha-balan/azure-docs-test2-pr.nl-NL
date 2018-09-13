---
title: Sample Data in SQL Server on Azure | Microsoft Docs
description: Sample Data in SQL Server on Azure
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgeonlun
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 74dcef9e927fc537cba56b03fcbfb9528c952ad0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856806"
---
# <a name="heading"></a><span data-ttu-id="59fcf-103">Sample data in SQL Server on Azure</span><span class="sxs-lookup"><span data-stu-id="59fcf-103">Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="59fcf-104">This article shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span><span class="sxs-lookup"><span data-stu-id="59fcf-104">This article shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="59fcf-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="59fcf-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="59fcf-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span><span class="sxs-lookup"><span data-stu-id="59fcf-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="59fcf-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span><span class="sxs-lookup"><span data-stu-id="59fcf-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="59fcf-108">If it is not, refer to [Move data to SQL Server on Azure](move-sql-server-virtual-machine.md) article for instructions on how to move your data to SQL Server on Azure.</span><span class="sxs-lookup"><span data-stu-id="59fcf-108">If it is not, refer to [Move data to SQL Server on Azure](move-sql-server-virtual-machine.md) article for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="59fcf-109">The following **menu** links to articles that describe how to sample data from various storage environments.</span><span class="sxs-lookup"><span data-stu-id="59fcf-109">The following **menu** links to articles that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="59fcf-110">**Why sample your data?**</span><span class="sxs-lookup"><span data-stu-id="59fcf-110">**Why sample your data?**</span></span>
<span data-ttu-id="59fcf-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span><span class="sxs-lookup"><span data-stu-id="59fcf-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="59fcf-112">This facilitates data understanding, exploration, and feature engineering.</span><span class="sxs-lookup"><span data-stu-id="59fcf-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="59fcf-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span><span class="sxs-lookup"><span data-stu-id="59fcf-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="59fcf-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="59fcf-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="SQL"></a><span data-ttu-id="59fcf-115">Using SQL</span><span class="sxs-lookup"><span data-stu-id="59fcf-115">Using SQL</span></span>
<span data-ttu-id="59fcf-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span><span class="sxs-lookup"><span data-stu-id="59fcf-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="59fcf-117">Choose a method based on your data size and its distribution.</span><span class="sxs-lookup"><span data-stu-id="59fcf-117">Choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="59fcf-118">The following two items show how to use `newid` in SQL Server to perform the sampling.</span><span class="sxs-lookup"><span data-stu-id="59fcf-118">The following two items show how to use `newid` in SQL Server to perform the sampling.</span></span> <span data-ttu-id="59fcf-119">The method you choose depends on how random you want the sample to be (pk_id in the following sample code is assumed to be an auto-generated primary key).</span><span class="sxs-lookup"><span data-stu-id="59fcf-119">The method you choose depends on how random you want the sample to be (pk_id in the following sample code is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="59fcf-120">Less strict random sample</span><span class="sxs-lookup"><span data-stu-id="59fcf-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="59fcf-121">More random sample</span><span class="sxs-lookup"><span data-stu-id="59fcf-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="59fcf-122">Tablesample can be used for sampling the data as well.</span><span class="sxs-lookup"><span data-stu-id="59fcf-122">Tablesample can be used for sampling the data as well.</span></span> <span data-ttu-id="59fcf-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span><span class="sxs-lookup"><span data-stu-id="59fcf-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="59fcf-124">You can explore and generate features from this sampled data by storing it in a new table</span><span class="sxs-lookup"><span data-stu-id="59fcf-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <a name="sql-aml"></a><span data-ttu-id="59fcf-125">Connecting to Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59fcf-125">Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="59fcf-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span><span class="sxs-lookup"><span data-stu-id="59fcf-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="59fcf-127">A screen shot of using the reader module to read the sampled data is shown here:</span><span class="sxs-lookup"><span data-stu-id="59fcf-127">A screen shot of using the reader module to read the sampled data is shown here:</span></span>

![reader sql][1]

## <a name="python"></a><span data-ttu-id="59fcf-129">Using the Python programming language</span><span class="sxs-lookup"><span data-stu-id="59fcf-129">Using the Python programming language</span></span>
<span data-ttu-id="59fcf-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span><span class="sxs-lookup"><span data-stu-id="59fcf-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="59fcf-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span><span class="sxs-lookup"><span data-stu-id="59fcf-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="59fcf-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span><span class="sxs-lookup"><span data-stu-id="59fcf-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="59fcf-133">The  following code reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data:</span><span class="sxs-lookup"><span data-stu-id="59fcf-133">The  following code reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data:</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="59fcf-134">You can now work with the sampled data in the Pandas data frame.</span><span class="sxs-lookup"><span data-stu-id="59fcf-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <a name="python-aml"></a><span data-ttu-id="59fcf-135">Connecting to Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59fcf-135">Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="59fcf-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="59fcf-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="59fcf-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="59fcf-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="59fcf-138">The steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="59fcf-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="59fcf-139">Write the pandas data frame to a local file</span><span class="sxs-lookup"><span data-stu-id="59fcf-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="59fcf-140">Upload local file to Azure blob</span><span class="sxs-lookup"><span data-stu-id="59fcf-140">Upload local file to Azure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="59fcf-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the following screen grab:</span><span class="sxs-lookup"><span data-stu-id="59fcf-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the following screen grab:</span></span>

![reader blob][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="59fcf-143">The Team Data Science Process in Action example</span><span class="sxs-lookup"><span data-stu-id="59fcf-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="59fcf-144">To walkthrough an example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Server](sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="59fcf-144">To walkthrough an example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Server](sql-walkthrough.md).</span></span>

[1]: ./media/sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/