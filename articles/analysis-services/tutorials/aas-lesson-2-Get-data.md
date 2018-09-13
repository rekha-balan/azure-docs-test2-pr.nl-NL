---
title: 'Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs'
description: Describes how to get and import data in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 5803bf2c71b2cf3fe7bb145b4d3d664c60642294
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855774"
---
# <a name="get-data"></a><span data-ttu-id="3b247-103">Get data</span><span class="sxs-lookup"><span data-stu-id="3b247-103">Get data</span></span>

<span data-ttu-id="3b247-104">In this lesson, you use Get Data in SSDT to connect to the Adventure Works  sample database, select data, preview and filter, and then import into your model workspace.</span><span class="sxs-lookup"><span data-stu-id="3b247-104">In this lesson, you use Get Data in SSDT to connect to the Adventure Works  sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="3b247-105">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span><span class="sxs-lookup"><span data-stu-id="3b247-105">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="3b247-106">Data can also be queried using a Power Query M formula expression.</span><span class="sxs-lookup"><span data-stu-id="3b247-106">Data can also be queried using a Power Query M formula expression.</span></span>

> [!NOTE]
> <span data-ttu-id="3b247-107">Tasks and images in this tutorial show connecting to an AdventureWorksDW2014 database on an on-premises server.</span><span class="sxs-lookup"><span data-stu-id="3b247-107">Tasks and images in this tutorial show connecting to an AdventureWorksDW2014 database on an on-premises server.</span></span> <span data-ttu-id="3b247-108">In some cases, an Adventure Works database on Azure may be different.</span><span class="sxs-lookup"><span data-stu-id="3b247-108">In some cases, an Adventure Works database on Azure may be different.</span></span>
  
<span data-ttu-id="3b247-109">Estimated time to complete this lesson: **10 minutes**</span><span class="sxs-lookup"><span data-stu-id="3b247-109">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3b247-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b247-110">Prerequisites</span></span>  
<span data-ttu-id="3b247-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="3b247-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="3b247-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="3b247-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="3b247-113">Create a connection</span><span class="sxs-lookup"><span data-stu-id="3b247-113">Create a connection</span></span>  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw2014-database"></a><span data-ttu-id="3b247-114">To create a connection to the AdventureWorksDW2014 database</span><span class="sxs-lookup"><span data-stu-id="3b247-114">To create a connection to the AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="3b247-115">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span><span class="sxs-lookup"><span data-stu-id="3b247-115">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="3b247-116">This launches Get Data, which guides you through connecting to a data source.</span><span class="sxs-lookup"><span data-stu-id="3b247-116">This launches Get Data, which guides you through connecting to a data source.</span></span> <span data-ttu-id="3b247-117">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** to open the model in the designer.</span><span class="sxs-lookup"><span data-stu-id="3b247-117">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** to open the model in the designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="3b247-119">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span><span class="sxs-lookup"><span data-stu-id="3b247-119">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="3b247-120">In the **SQL Server Database** dialog, in **Server**, type the name of the server where you installed the AdventureWorksDW2014 database, and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="3b247-120">In the **SQL Server Database** dialog, in **Server**, type the name of the server where you installed the AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="3b247-121">When prompted to enter credentials, you need to specify the credentials Analysis Services uses to connect to the data source when importing and processing data.</span><span class="sxs-lookup"><span data-stu-id="3b247-121">When prompted to enter credentials, you need to specify the credentials Analysis Services uses to connect to the data source when importing and processing data.</span></span> <span data-ttu-id="3b247-122">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="3b247-122">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="3b247-123">It's recommended you use an account where the password doesn't expire.</span><span class="sxs-lookup"><span data-stu-id="3b247-123">It's recommended you use an account where the password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="3b247-125">Using a Windows user account and password provides the most secure method of connecting to a data source.</span><span class="sxs-lookup"><span data-stu-id="3b247-125">Using a Windows user account and password provides the most secure method of connecting to a data source.</span></span>
  
5.  <span data-ttu-id="3b247-126">In Navigator, select the **AdventureWorksDW2014** database, and then click **OK**.This creates the connection to the database.</span><span class="sxs-lookup"><span data-stu-id="3b247-126">In Navigator, select the **AdventureWorksDW2014** database, and then click **OK**.This creates the connection to the database.</span></span> 
  
6.  <span data-ttu-id="3b247-127">In Navigator, select the check box for the following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="3b247-127">In Navigator, select the check box for the following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**, and then click **Edit**.</span></span>

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
    <span data-ttu-id="3b247-129">The Query Editor opens.</span><span class="sxs-lookup"><span data-stu-id="3b247-129">The Query Editor opens.</span></span> <span data-ttu-id="3b247-130">In the next section, you select only the data you want to import.</span><span class="sxs-lookup"><span data-stu-id="3b247-130">In the next section, you select only the data you want to import.</span></span>

  
## <a name="filter-the-table-data"></a><span data-ttu-id="3b247-131">Filter the table data</span><span class="sxs-lookup"><span data-stu-id="3b247-131">Filter the table data</span></span>  
<span data-ttu-id="3b247-132">Tables in the AdventureWorksDW2014 sample database have data that isn't necessary to include in your model.</span><span class="sxs-lookup"><span data-stu-id="3b247-132">Tables in the AdventureWorksDW2014 sample database have data that isn't necessary to include in your model.</span></span> <span data-ttu-id="3b247-133">When possible, you want to filter out unnecessary data to save in-memory space used by the model.</span><span class="sxs-lookup"><span data-stu-id="3b247-133">When possible, you want to filter out unnecessary data to save in-memory space used by the model.</span></span> <span data-ttu-id="3b247-134">You filter out some of the columns from tables so they're not imported into the workspace database, or the model database after it has been deployed.</span><span class="sxs-lookup"><span data-stu-id="3b247-134">You filter out some of the columns from tables so they're not imported into the workspace database, or the model database after it has been deployed.</span></span> 
  
#### <a name="to-filter-the-table-data-before-importing"></a><span data-ttu-id="3b247-135">To filter the table data before importing</span><span class="sxs-lookup"><span data-stu-id="3b247-135">To filter the table data before importing</span></span>  
  
1.  <span data-ttu-id="3b247-136">In Query Editor, select the **DimCustomer** table.</span><span class="sxs-lookup"><span data-stu-id="3b247-136">In Query Editor, select the **DimCustomer** table.</span></span> <span data-ttu-id="3b247-137">A view of the DimCustomer table at the datasource (your AdventureWorksDW2014 sample database) appears.</span><span class="sxs-lookup"><span data-stu-id="3b247-137">A view of the DimCustomer table at the datasource (your AdventureWorksDW2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="3b247-138">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span><span class="sxs-lookup"><span data-stu-id="3b247-138">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="3b247-140">Since the values for these columns are not relevant to Internet sales analysis, there is no need to import these columns.</span><span class="sxs-lookup"><span data-stu-id="3b247-140">Since the values for these columns are not relevant to Internet sales analysis, there is no need to import these columns.</span></span> <span data-ttu-id="3b247-141">Eliminating unnecessary columns makes your model smaller and more efficient.</span><span class="sxs-lookup"><span data-stu-id="3b247-141">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  

    > [!TIP]
    > <span data-ttu-id="3b247-142">If you make a mistake, you can backup by deleting a step in **APPLIED STEPS**.</span><span class="sxs-lookup"><span data-stu-id="3b247-142">If you make a mistake, you can backup by deleting a step in **APPLIED STEPS**.</span></span>   
    
    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-step.png)

  
4.  <span data-ttu-id="3b247-144">Filter the remaining tables by removing the following columns in each table:</span><span class="sxs-lookup"><span data-stu-id="3b247-144">Filter the remaining tables by removing the following columns in each table:</span></span>  
    
    <span data-ttu-id="3b247-145">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="3b247-145">**DimDate**</span></span>
    
      |<span data-ttu-id="3b247-146">Column</span><span class="sxs-lookup"><span data-stu-id="3b247-146">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="3b247-147">**DateKey**</span><span class="sxs-lookup"><span data-stu-id="3b247-147">**DateKey**</span></span>|  
      |<span data-ttu-id="3b247-148">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="3b247-148">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="3b247-149">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="3b247-149">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="3b247-150">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="3b247-150">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="3b247-151">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="3b247-151">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="3b247-152">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="3b247-152">**DimGeography**</span></span>
  
      |<span data-ttu-id="3b247-153">Column</span><span class="sxs-lookup"><span data-stu-id="3b247-153">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="3b247-154">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="3b247-154">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="3b247-155">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="3b247-155">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="3b247-156">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="3b247-156">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="3b247-157">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="3b247-157">**DimProduct**</span></span>
  
      |<span data-ttu-id="3b247-158">Column</span><span class="sxs-lookup"><span data-stu-id="3b247-158">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="3b247-159">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="3b247-159">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="3b247-160">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="3b247-160">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="3b247-161">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-161">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="3b247-162">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-162">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="3b247-163">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-163">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="3b247-164">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-164">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="3b247-165">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-165">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="3b247-166">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-166">**GermanDescription**</span></span>|  
      |<span data-ttu-id="3b247-167">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-167">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="3b247-168">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="3b247-168">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="3b247-169">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="3b247-169">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="3b247-170">Column</span><span class="sxs-lookup"><span data-stu-id="3b247-170">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="3b247-171">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="3b247-171">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="3b247-172">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="3b247-172">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="3b247-173">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="3b247-173">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="3b247-174">Column</span><span class="sxs-lookup"><span data-stu-id="3b247-174">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="3b247-175">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="3b247-175">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="3b247-176">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="3b247-176">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="3b247-177">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="3b247-177">**FactInternetSales**</span></span>
  
      <span data-ttu-id="3b247-178">No columns removed.</span><span class="sxs-lookup"><span data-stu-id="3b247-178">No columns removed.</span></span>
  
## <a name="Import"></a><span data-ttu-id="3b247-179">Import the selected tables and column data</span><span class="sxs-lookup"><span data-stu-id="3b247-179">Import the selected tables and column data</span></span>  
<span data-ttu-id="3b247-180">Now that you've previewed and filtered out unnecessary data, you can import the rest of the data you do want.</span><span class="sxs-lookup"><span data-stu-id="3b247-180">Now that you've previewed and filtered out unnecessary data, you can import the rest of the data you do want.</span></span> <span data-ttu-id="3b247-181">The wizard imports the table data along with any relationships between tables.</span><span class="sxs-lookup"><span data-stu-id="3b247-181">The wizard imports the table data along with any relationships between tables.</span></span> <span data-ttu-id="3b247-182">New tables and columns are created in the model and data that you filtered out is not be imported.</span><span class="sxs-lookup"><span data-stu-id="3b247-182">New tables and columns are created in the model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a><span data-ttu-id="3b247-183">To import the selected tables and column data</span><span class="sxs-lookup"><span data-stu-id="3b247-183">To import the selected tables and column data</span></span>  
  
1.  <span data-ttu-id="3b247-184">Review your selections.</span><span class="sxs-lookup"><span data-stu-id="3b247-184">Review your selections.</span></span> <span data-ttu-id="3b247-185">If everything looks okay, click **Import**.</span><span class="sxs-lookup"><span data-stu-id="3b247-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="3b247-186">The Data Processing dialog shows the status of data being imported from your datasource into your workspace database.</span><span class="sxs-lookup"><span data-stu-id="3b247-186">The Data Processing dialog shows the status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="3b247-188">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="3b247-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="3b247-189">Save your model project</span><span class="sxs-lookup"><span data-stu-id="3b247-189">Save your model project</span></span>  
<span data-ttu-id="3b247-190">It's important to frequently save your model project.</span><span class="sxs-lookup"><span data-stu-id="3b247-190">It's important to frequently save your model project.</span></span>  
  
#### <a name="to-save-the-model-project"></a><span data-ttu-id="3b247-191">To save the model project</span><span class="sxs-lookup"><span data-stu-id="3b247-191">To save the model project</span></span>  
  
-   <span data-ttu-id="3b247-192">Click **File** > **Save All**.</span><span class="sxs-lookup"><span data-stu-id="3b247-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="3b247-193">What's next?</span><span class="sxs-lookup"><span data-stu-id="3b247-193">What's next?</span></span>
<span data-ttu-id="3b247-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="3b247-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
