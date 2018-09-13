---
title: Connect Excel to SQL Database | Microsoft Docs
description: Learn how to connect Microsoft Excel to Azure SQL database in the cloud. Import data into Excel for reporting and data exploration.
services: sql-database
keywords: connect excel to sql, import data to excel
documentationcenter: ''
author: joseidz
manager: jhubbard
editor: ''
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: development
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 8cf3ae37a89d9fecb37d44f70684639916d18aa0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661967"
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="79b70-105">Connect Excel to an Azure SQL database and create a report</span><span class="sxs-lookup"><span data-stu-id="79b70-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="79b70-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span><span class="sxs-lookup"><span data-stu-id="79b70-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="79b70-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span><span class="sxs-lookup"><span data-stu-id="79b70-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="79b70-108">You'll need a SQL database in Azure before you get started.</span><span class="sxs-lookup"><span data-stu-id="79b70-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="79b70-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span><span class="sxs-lookup"><span data-stu-id="79b70-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="79b70-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span><span class="sxs-lookup"><span data-stu-id="79b70-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="79b70-111">You'll also need a copy of Excel.</span><span class="sxs-lookup"><span data-stu-id="79b70-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="79b70-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="79b70-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="79b70-113">Connect Excel to a SQL database and create an odc file</span><span class="sxs-lookup"><span data-stu-id="79b70-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="79b70-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="79b70-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="79b70-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="79b70-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Select data source: Connect Excel to SQL database.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="79b70-117">The Data Connection Wizard opens.</span><span class="sxs-lookup"><span data-stu-id="79b70-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="79b70-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="79b70-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="79b70-119">For example, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="79b70-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="79b70-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79b70-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Type the server name and login credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="79b70-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span><span class="sxs-lookup"><span data-stu-id="79b70-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="79b70-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span><span class="sxs-lookup"><span data-stu-id="79b70-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="79b70-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span><span class="sxs-lookup"><span data-stu-id="79b70-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="79b70-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79b70-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Select a database and table.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="79b70-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (\*.odc) file that Excel uses.</span><span class="sxs-lookup"><span data-stu-id="79b70-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (\*.odc) file that Excel uses.</span></span> <span data-ttu-id="79b70-128">You can leave the defaults or customize your selections.</span><span class="sxs-lookup"><span data-stu-id="79b70-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="79b70-129">You can leave the defaults, but note the **File Name** in particular.</span><span class="sxs-lookup"><span data-stu-id="79b70-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="79b70-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span><span class="sxs-lookup"><span data-stu-id="79b70-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="79b70-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="79b70-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![Saving an odc file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="79b70-133">The **Import data** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="79b70-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="79b70-134">Import the data into Excel and create a pivot chart</span><span class="sxs-lookup"><span data-stu-id="79b70-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="79b70-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span><span class="sxs-lookup"><span data-stu-id="79b70-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="79b70-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="79b70-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="79b70-137">We chose **PivotChart**.</span><span class="sxs-lookup"><span data-stu-id="79b70-137">We chose **PivotChart**.</span></span> <span data-ttu-id="79b70-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span><span class="sxs-lookup"><span data-stu-id="79b70-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="79b70-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="79b70-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="79b70-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span><span class="sxs-lookup"><span data-stu-id="79b70-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![Choosing the format for data in Excel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="79b70-142">The worksheet now has an empty pivot table and chart.</span><span class="sxs-lookup"><span data-stu-id="79b70-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="79b70-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span><span class="sxs-lookup"><span data-stu-id="79b70-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![Configure database report.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="79b70-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="79b70-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="79b70-146">![Open a connection from another workbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="79b70-146">![Open a connection from another workbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="79b70-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="79b70-147">Next steps</span></span>
* <span data-ttu-id="79b70-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span><span class="sxs-lookup"><span data-stu-id="79b70-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="79b70-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="79b70-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="79b70-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="79b70-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>








