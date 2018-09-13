---
title: Visualize SQL Data Warehouse data with Power BI Microsoft Azure
description: Visualize SQL Data Warehouse data with Power BI
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: b683bb94a6a33c4d5de629284243af1dbe1cd072
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555397"
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="e09a6-103">Visualize data with Power BI</span><span class="sxs-lookup"><span data-stu-id="e09a6-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="e09a6-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span><span class="sxs-lookup"><span data-stu-id="e09a6-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e09a6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e09a6-110">Prerequisites</span></span>
<span data-ttu-id="e09a6-111">To step through this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="e09a6-111">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="e09a6-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span><span class="sxs-lookup"><span data-stu-id="e09a6-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span></span> <span data-ttu-id="e09a6-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span><span class="sxs-lookup"><span data-stu-id="e09a6-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="e09a6-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="e09a6-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-to-your-database"></a><span data-ttu-id="e09a6-115">1. Connect to your database</span><span class="sxs-lookup"><span data-stu-id="e09a6-115">1. Connect to your database</span></span>
<span data-ttu-id="e09a6-116">To open Power BI and connect to your AdventureWorksDW database:</span><span class="sxs-lookup"><span data-stu-id="e09a6-116">To open Power BI and connect to your AdventureWorksDW database:</span></span>

1. <span data-ttu-id="e09a6-117">Sign into the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e09a6-117">Sign into the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="e09a6-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="e09a6-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Find your database][1]
3. <span data-ttu-id="e09a6-120">Click the 'Open in Power BI' button.</span><span class="sxs-lookup"><span data-stu-id="e09a6-120">Click the 'Open in Power BI' button.</span></span>
   
    ![Power BI button][2]
4. <span data-ttu-id="e09a6-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span><span class="sxs-lookup"><span data-stu-id="e09a6-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="e09a6-123">Click next.</span><span class="sxs-lookup"><span data-stu-id="e09a6-123">Click next.</span></span>
   
    ![Power BI connection][3]
5. <span data-ttu-id="e09a6-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="e09a6-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span></span>
   
    ![Power BI sign in][4]
6. <span data-ttu-id="e09a6-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span><span class="sxs-lookup"><span data-stu-id="e09a6-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span></span> <span data-ttu-id="e09a6-128">This will open the database.</span><span class="sxs-lookup"><span data-stu-id="e09a6-128">This will open the database.</span></span>
   
    ![Power BI open AdventureWorksDW][5]

## <a name="2-create-a-report"></a><span data-ttu-id="e09a6-130">2. Create a report</span><span class="sxs-lookup"><span data-stu-id="e09a6-130">2. Create a report</span></span>
<span data-ttu-id="e09a6-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span><span class="sxs-lookup"><span data-stu-id="e09a6-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="e09a6-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="e09a6-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="e09a6-133">This view contains a few of the key metrics for analyzing the sales of the company.</span><span class="sxs-lookup"><span data-stu-id="e09a6-133">This view contains a few of the key metrics for analyzing the sales of the company.</span></span>

1. <span data-ttu-id="e09a6-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span><span class="sxs-lookup"><span data-stu-id="e09a6-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span></span> <span data-ttu-id="e09a6-135">Click the PostalCode and SalesAmount columns to select them.</span><span class="sxs-lookup"><span data-stu-id="e09a6-135">Click the PostalCode and SalesAmount columns to select them.</span></span>
   
    ![Power BI select AggregateSales][6]
   
    <span data-ttu-id="e09a6-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span><span class="sxs-lookup"><span data-stu-id="e09a6-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI map][7]
2. <span data-ttu-id="e09a6-139">This step creates a bar graph that shows amount of sales per customer income.</span><span class="sxs-lookup"><span data-stu-id="e09a6-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="e09a6-140">To create this go to the expanded AggregateSales view.</span><span class="sxs-lookup"><span data-stu-id="e09a6-140">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="e09a6-141">Click the SalesAmount field.</span><span class="sxs-lookup"><span data-stu-id="e09a6-141">Click the SalesAmount field.</span></span> <span data-ttu-id="e09a6-142">Drag the Customer Income field to the left and drop it into Axis.</span><span class="sxs-lookup"><span data-stu-id="e09a6-142">Drag the Customer Income field to the left and drop it into Axis.</span></span>
   
    ![Power BI select axis][8]
   
    <span data-ttu-id="e09a6-144">We moved the bar chart over the left.</span><span class="sxs-lookup"><span data-stu-id="e09a6-144">We moved the bar chart over the left.</span></span>
   
    ![Power BI bar][9]
3. <span data-ttu-id="e09a6-146">This step creates a line chart that shows sales amount per order date.</span><span class="sxs-lookup"><span data-stu-id="e09a6-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="e09a6-147">To create this go to the expanded AggregateSales view.</span><span class="sxs-lookup"><span data-stu-id="e09a6-147">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="e09a6-148">Click SalesAmount and OrderDate.</span><span class="sxs-lookup"><span data-stu-id="e09a6-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="e09a6-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span><span class="sxs-lookup"><span data-stu-id="e09a6-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span></span>
   
    ![Power BI select line chart][10]
   
    <span data-ttu-id="e09a6-151">You now have a report that shows three different visualizations of the data.</span><span class="sxs-lookup"><span data-stu-id="e09a6-151">You now have a report that shows three different visualizations of the data.</span></span>
   
    ![Power BI line][11]

<span data-ttu-id="e09a6-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span><span class="sxs-lookup"><span data-stu-id="e09a6-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e09a6-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="e09a6-154">Next steps</span></span>
<span data-ttu-id="e09a6-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span><span class="sxs-lookup"><span data-stu-id="e09a6-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="e09a6-156">Or take a look at the [Power BI website][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="e09a6-156">Or take a look at the [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting to SQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/












