---
title: Load data from SQL Server into Azure SQL Data Warehouse (SSIS) | Microsoft Docs
description: Shows you how to create a SQL Server Integration Services (SSIS) package to move data from a wide variety of data sources to SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: douglaslms
manager: jhubbard
editor: ''
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: douglasl;barbkess
ms.openlocfilehash: e2fcce705349ae2595a707f1168934d90921f868
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554365"
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="ca49b-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span><span class="sxs-lookup"><span data-stu-id="ca49b-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="ca49b-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ca49b-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span><span class="sxs-lookup"><span data-stu-id="ca49b-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span></span>

<span data-ttu-id="ca49b-109">In this tutorial, you will:</span><span class="sxs-lookup"><span data-stu-id="ca49b-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="ca49b-110">Create a new Integration Services project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca49b-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="ca49b-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span><span class="sxs-lookup"><span data-stu-id="ca49b-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="ca49b-112">Design an SSIS package that loads data from the source into the destination.</span><span class="sxs-lookup"><span data-stu-id="ca49b-112">Design an SSIS package that loads data from the source into the destination.</span></span>
* <span data-ttu-id="ca49b-113">Run the SSIS package to load the data.</span><span class="sxs-lookup"><span data-stu-id="ca49b-113">Run the SSIS package to load the data.</span></span>

<span data-ttu-id="ca49b-114">This tutorial uses SQL Server as the data source.</span><span class="sxs-lookup"><span data-stu-id="ca49b-114">This tutorial uses SQL Server as the data source.</span></span> <span data-ttu-id="ca49b-115">SQL Server could be running on premises or in an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ca49b-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="ca49b-116">Basic concepts</span><span class="sxs-lookup"><span data-stu-id="ca49b-116">Basic concepts</span></span>
<span data-ttu-id="ca49b-117">The package is the unit of work in SSIS.</span><span class="sxs-lookup"><span data-stu-id="ca49b-117">The package is the unit of work in SSIS.</span></span> <span data-ttu-id="ca49b-118">Related packages are grouped in projects.</span><span class="sxs-lookup"><span data-stu-id="ca49b-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="ca49b-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="ca49b-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="ca49b-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span><span class="sxs-lookup"><span data-stu-id="ca49b-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span></span> <span data-ttu-id="ca49b-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span><span class="sxs-lookup"><span data-stu-id="ca49b-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="ca49b-122">Options for loading data with SSIS</span><span class="sxs-lookup"><span data-stu-id="ca49b-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="ca49b-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="ca49b-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="ca49b-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span><span class="sxs-lookup"><span data-stu-id="ca49b-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span></span>
2. <span data-ttu-id="ca49b-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="ca49b-127">This option may provide slightly better performance than the ADO NET Destination.</span><span class="sxs-lookup"><span data-stu-id="ca49b-127">This option may provide slightly better performance than the ADO NET Destination.</span></span>
3. <span data-ttu-id="ca49b-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ca49b-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span></span> <span data-ttu-id="ca49b-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="ca49b-130">This option provides the best performance of the three options listed here.</span><span class="sxs-lookup"><span data-stu-id="ca49b-130">This option provides the best performance of the three options listed here.</span></span> <span data-ttu-id="ca49b-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span><span class="sxs-lookup"><span data-stu-id="ca49b-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="ca49b-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span><span class="sxs-lookup"><span data-stu-id="ca49b-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ca49b-133">Before you start</span><span class="sxs-lookup"><span data-stu-id="ca49b-133">Before you start</span></span>
<span data-ttu-id="ca49b-134">To step through this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="ca49b-134">To step through this tutorial, you need:</span></span>

1. <span data-ttu-id="ca49b-135">**SQL Server Integration Services (SSIS)**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="ca49b-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ca49b-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="ca49b-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span><span class="sxs-lookup"><span data-stu-id="ca49b-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="ca49b-138">**Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-138">**Visual Studio**.</span></span> <span data-ttu-id="ca49b-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span><span class="sxs-lookup"><span data-stu-id="ca49b-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="ca49b-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="ca49b-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span><span class="sxs-lookup"><span data-stu-id="ca49b-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="ca49b-142">**Sample data**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-142">**Sample data**.</span></span> <span data-ttu-id="ca49b-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="ca49b-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span><span class="sxs-lookup"><span data-stu-id="ca49b-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="ca49b-145">**A SQL Data Warehouse database and permissions**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="ca49b-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span><span class="sxs-lookup"><span data-stu-id="ca49b-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="ca49b-147">You have to have permissions to create a table and to load data.</span><span class="sxs-lookup"><span data-stu-id="ca49b-147">You have to have permissions to create a table and to load data.</span></span>
6. <span data-ttu-id="ca49b-148">**A firewall rule**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-148">**A firewall rule**.</span></span> <span data-ttu-id="ca49b-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="ca49b-150">Step 1: Create a new Integration Services project</span><span class="sxs-lookup"><span data-stu-id="ca49b-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="ca49b-151">Launch Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca49b-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="ca49b-152">On the **File** menu, select **New | Project**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-152">On the **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="ca49b-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span><span class="sxs-lookup"><span data-stu-id="ca49b-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="ca49b-154">Select **Integration Services Project**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="ca49b-155">Provide values for **Name** and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="ca49b-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span><span class="sxs-lookup"><span data-stu-id="ca49b-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="ca49b-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span><span class="sxs-lookup"><span data-stu-id="ca49b-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span></span> <span data-ttu-id="ca49b-158">You see the following screen areas:</span><span class="sxs-lookup"><span data-stu-id="ca49b-158">You see the following screen areas:</span></span>

* <span data-ttu-id="ca49b-159">On the left, the **Toolbox** of SSIS components.</span><span class="sxs-lookup"><span data-stu-id="ca49b-159">On the left, the **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="ca49b-160">In the middle, the design surface, with multiple tabs.</span><span class="sxs-lookup"><span data-stu-id="ca49b-160">In the middle, the design surface, with multiple tabs.</span></span> <span data-ttu-id="ca49b-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span><span class="sxs-lookup"><span data-stu-id="ca49b-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span></span>
* <span data-ttu-id="ca49b-162">On the right, the **Solution Explorer** and the **Properties** panes.</span><span class="sxs-lookup"><span data-stu-id="ca49b-162">On the right, the **Solution Explorer** and the **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a><span data-ttu-id="ca49b-163">Step 2: Create the basic data flow</span><span class="sxs-lookup"><span data-stu-id="ca49b-163">Step 2: Create the basic data flow</span></span>
1. <span data-ttu-id="ca49b-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span><span class="sxs-lookup"><span data-stu-id="ca49b-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="ca49b-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span><span class="sxs-lookup"><span data-stu-id="ca49b-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span></span>
3. <span data-ttu-id="ca49b-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span><span class="sxs-lookup"><span data-stu-id="ca49b-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span></span> <span data-ttu-id="ca49b-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span><span class="sxs-lookup"><span data-stu-id="ca49b-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span></span>
4. <span data-ttu-id="ca49b-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span><span class="sxs-lookup"><span data-stu-id="ca49b-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span></span> <span data-ttu-id="ca49b-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span><span class="sxs-lookup"><span data-stu-id="ca49b-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a><span data-ttu-id="ca49b-170">Step 3: Configure the source adapter</span><span class="sxs-lookup"><span data-stu-id="ca49b-170">Step 3: Configure the source adapter</span></span>
1. <span data-ttu-id="ca49b-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="ca49b-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span><span class="sxs-lookup"><span data-stu-id="ca49b-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="ca49b-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span><span class="sxs-lookup"><span data-stu-id="ca49b-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="ca49b-174">In the **Connection Manager** dialog box, do the following things.</span><span class="sxs-lookup"><span data-stu-id="ca49b-174">In the **Connection Manager** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="ca49b-175">For **Provider**, select the SqlClient Data Provider.</span><span class="sxs-lookup"><span data-stu-id="ca49b-175">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="ca49b-176">For **Server name**, enter the SQL Server name.</span><span class="sxs-lookup"><span data-stu-id="ca49b-176">For **Server name**, enter the SQL Server name.</span></span>
   3. <span data-ttu-id="ca49b-177">In the **Log on to the server** section, select or enter authentication information.</span><span class="sxs-lookup"><span data-stu-id="ca49b-177">In the **Log on to the server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="ca49b-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span><span class="sxs-lookup"><span data-stu-id="ca49b-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="ca49b-179">Click **Test Connection**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="ca49b-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ca49b-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="ca49b-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ca49b-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="ca49b-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="ca49b-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span><span class="sxs-lookup"><span data-stu-id="ca49b-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="ca49b-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ca49b-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="ca49b-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="ca49b-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span><span class="sxs-lookup"><span data-stu-id="ca49b-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span></span>

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a><span data-ttu-id="ca49b-187">Step 4: Connect the source adapter to the destination adapter</span><span class="sxs-lookup"><span data-stu-id="ca49b-187">Step 4: Connect the source adapter to the destination adapter</span></span>
1. <span data-ttu-id="ca49b-188">Select the source adapter on the design surface.</span><span class="sxs-lookup"><span data-stu-id="ca49b-188">Select the source adapter on the design surface.</span></span>
2. <span data-ttu-id="ca49b-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span><span class="sxs-lookup"><span data-stu-id="ca49b-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="ca49b-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span><span class="sxs-lookup"><span data-stu-id="ca49b-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span></span> <span data-ttu-id="ca49b-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span><span class="sxs-lookup"><span data-stu-id="ca49b-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span></span>

## <a name="step-5-configure-the-destination-adapter"></a><span data-ttu-id="ca49b-192">Step 5: Configure the destination adapter</span><span class="sxs-lookup"><span data-stu-id="ca49b-192">Step 5: Configure the destination adapter</span></span>
1. <span data-ttu-id="ca49b-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="ca49b-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span><span class="sxs-lookup"><span data-stu-id="ca49b-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="ca49b-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span><span class="sxs-lookup"><span data-stu-id="ca49b-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="ca49b-196">In the **Connection Manager** dialog box, do the following things.</span><span class="sxs-lookup"><span data-stu-id="ca49b-196">In the **Connection Manager** dialog box, do the following things.</span></span>
   1. <span data-ttu-id="ca49b-197">For **Provider**, select the SqlClient Data Provider.</span><span class="sxs-lookup"><span data-stu-id="ca49b-197">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="ca49b-198">For **Server name**, enter the SQL Data Warehouse name.</span><span class="sxs-lookup"><span data-stu-id="ca49b-198">For **Server name**, enter the SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="ca49b-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span><span class="sxs-lookup"><span data-stu-id="ca49b-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="ca49b-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="ca49b-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="ca49b-201">Click **Test Connection**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="ca49b-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ca49b-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="ca49b-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ca49b-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="ca49b-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="ca49b-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span><span class="sxs-lookup"><span data-stu-id="ca49b-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="ca49b-206">In the **Create Table** dialog box, do the following things.</span><span class="sxs-lookup"><span data-stu-id="ca49b-206">In the **Create Table** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="ca49b-207">Change the name of the destination table to **SalesOrderDetail**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-207">Change the name of the destination table to **SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="ca49b-208">Remove the **rowguid** column.</span><span class="sxs-lookup"><span data-stu-id="ca49b-208">Remove the **rowguid** column.</span></span> <span data-ttu-id="ca49b-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="ca49b-210">Change the data type of the **LineTotal** column to **money**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-210">Change the data type of the **LineTotal** column to **money**.</span></span> <span data-ttu-id="ca49b-211">The **decimal** data type is not supported in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-211">The **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="ca49b-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="ca49b-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="ca49b-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span><span class="sxs-lookup"><span data-stu-id="ca49b-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="ca49b-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span><span class="sxs-lookup"><span data-stu-id="ca49b-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="ca49b-215">Click **OK** to finish configuring the data source.</span><span class="sxs-lookup"><span data-stu-id="ca49b-215">Click **OK** to finish configuring the data source.</span></span>

## <a name="step-6-run-the-package-to-load-the-data"></a><span data-ttu-id="ca49b-216">Step 6: Run the package to load the data</span><span class="sxs-lookup"><span data-stu-id="ca49b-216">Step 6: Run the package to load the data</span></span>
<span data-ttu-id="ca49b-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="ca49b-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span></span>

<span data-ttu-id="ca49b-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span><span class="sxs-lookup"><span data-stu-id="ca49b-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="ca49b-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span><span class="sxs-lookup"><span data-stu-id="ca49b-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span></span>

![][15]

<span data-ttu-id="ca49b-220">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="ca49b-220">Congratulations!</span></span> <span data-ttu-id="ca49b-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ca49b-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca49b-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="ca49b-222">Next steps</span></span>
* <span data-ttu-id="ca49b-223">Learn more about the SSIS data flow.</span><span class="sxs-lookup"><span data-stu-id="ca49b-223">Learn more about the SSIS data flow.</span></span> <span data-ttu-id="ca49b-224">Start here: [Data Flow][Data Flow].</span><span class="sxs-lookup"><span data-stu-id="ca49b-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="ca49b-225">Learn how to debug and troubleshoot your packages right in the design environment.</span><span class="sxs-lookup"><span data-stu-id="ca49b-225">Learn how to debug and troubleshoot your packages right in the design environment.</span></span> <span data-ttu-id="ca49b-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span><span class="sxs-lookup"><span data-stu-id="ca49b-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="ca49b-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span><span class="sxs-lookup"><span data-stu-id="ca49b-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span></span> <span data-ttu-id="ca49b-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span><span class="sxs-lookup"><span data-stu-id="ca49b-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
















