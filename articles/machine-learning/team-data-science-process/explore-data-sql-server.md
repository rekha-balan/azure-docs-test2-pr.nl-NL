---
title: Explore data in SQL Server Virtual Machine on Azure | Microsoft Docs
description: How to explore data that is stored in a SQL Server VM on Azure.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: deguhath
ms.openlocfilehash: d96852006377123f6e9d17c3ae5b79fe930c1e1c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857733"
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="94dc9-103">Explore data in SQL Server Virtual Machine on Azure</span><span class="sxs-lookup"><span data-stu-id="94dc9-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="94dc9-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span><span class="sxs-lookup"><span data-stu-id="94dc9-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="94dc9-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span><span class="sxs-lookup"><span data-stu-id="94dc9-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="94dc9-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span><span class="sxs-lookup"><span data-stu-id="94dc9-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="94dc9-107">This task is a step in the Cortana Analytics Process (CAP).</span><span class="sxs-lookup"><span data-stu-id="94dc9-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="94dc9-108">The sample SQL statements in this document assume that data is in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="94dc9-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="94dc9-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="94dc9-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <a name="sql-dataexploration"></a><span data-ttu-id="94dc9-110">Explore SQL data with SQL scripts</span><span class="sxs-lookup"><span data-stu-id="94dc9-110">Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="94dc9-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="94dc9-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="94dc9-112">Get the count of observations per day</span><span class="sxs-lookup"><span data-stu-id="94dc9-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="94dc9-113">Get the levels in a categorical column</span><span class="sxs-lookup"><span data-stu-id="94dc9-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="94dc9-114">Get the number of levels in combination of two categorical columns</span><span class="sxs-lookup"><span data-stu-id="94dc9-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="94dc9-115">Get the distribution for numerical columns</span><span class="sxs-lookup"><span data-stu-id="94dc9-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="94dc9-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span><span class="sxs-lookup"><span data-stu-id="94dc9-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="python"></a><span data-ttu-id="94dc9-117">Explore SQL data with Python</span><span class="sxs-lookup"><span data-stu-id="94dc9-117">Explore SQL data with Python</span></span>
<span data-ttu-id="94dc9-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="94dc9-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](data-blob.md).</span></span> <span data-ttu-id="94dc9-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span><span class="sxs-lookup"><span data-stu-id="94dc9-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="94dc9-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span><span class="sxs-lookup"><span data-stu-id="94dc9-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="94dc9-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span><span class="sxs-lookup"><span data-stu-id="94dc9-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="94dc9-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span><span class="sxs-lookup"><span data-stu-id="94dc9-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="94dc9-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span><span class="sxs-lookup"><span data-stu-id="94dc9-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="94dc9-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="94dc9-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](data-blob.md).</span></span>

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="94dc9-125">The Team Data Science Process in action example</span><span class="sxs-lookup"><span data-stu-id="94dc9-125">The Team Data Science Process in action example</span></span>
<span data-ttu-id="94dc9-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="94dc9-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](sql-walkthrough.md).</span></span>

