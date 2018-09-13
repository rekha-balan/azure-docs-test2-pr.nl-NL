---
title: 'Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs'
description: Describes how to create calculated columns in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: d97a365d1eae21a58e2b33b82dc2593343248e0e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867578"
---
# <a name="create-calculated-columns"></a><span data-ttu-id="82355-103">Create calculated columns</span><span class="sxs-lookup"><span data-stu-id="82355-103">Create calculated columns</span></span>

<span data-ttu-id="82355-104">In this lesson, you create data in your model by adding calculated columns.</span><span class="sxs-lookup"><span data-stu-id="82355-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="82355-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span><span class="sxs-lookup"><span data-stu-id="82355-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="82355-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="82355-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="82355-107">You create five new calculated columns in three different tables.</span><span class="sxs-lookup"><span data-stu-id="82355-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="82355-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span><span class="sxs-lookup"><span data-stu-id="82355-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="82355-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span><span class="sxs-lookup"><span data-stu-id="82355-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="82355-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span><span class="sxs-lookup"><span data-stu-id="82355-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="82355-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span><span class="sxs-lookup"><span data-stu-id="82355-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="82355-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="82355-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="82355-113">Estimated time to complete this lesson: **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="82355-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="82355-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="82355-114">Prerequisites</span></span>  
<span data-ttu-id="82355-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="82355-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="82355-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="82355-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="82355-117">Create calculated columns</span><span class="sxs-lookup"><span data-stu-id="82355-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="82355-118">Create a MonthCalendar calculated column in the DimDate table</span><span class="sxs-lookup"><span data-stu-id="82355-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="82355-119">Click the **Model** menu > **Model View** > **Data View**.</span><span class="sxs-lookup"><span data-stu-id="82355-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="82355-120">Calculated columns can only be created by using the model designer in Data View.</span><span class="sxs-lookup"><span data-stu-id="82355-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="82355-121">In the model designer, click the **DimDate** table (tab).</span><span class="sxs-lookup"><span data-stu-id="82355-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="82355-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span><span class="sxs-lookup"><span data-stu-id="82355-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="82355-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span><span class="sxs-lookup"><span data-stu-id="82355-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="82355-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span><span class="sxs-lookup"><span data-stu-id="82355-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="82355-125">Values are then populated for all the rows in the calculated column.</span><span class="sxs-lookup"><span data-stu-id="82355-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="82355-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span><span class="sxs-lookup"><span data-stu-id="82355-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="82355-127">Rename this column to **MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="82355-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="82355-129">The MonthCalendar calculated column provides a sortable name for Month.</span><span class="sxs-lookup"><span data-stu-id="82355-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="82355-130">Create a DayOfWeek calculated column in the DimDate table</span><span class="sxs-lookup"><span data-stu-id="82355-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="82355-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span><span class="sxs-lookup"><span data-stu-id="82355-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="82355-132">In the formula bar, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="82355-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="82355-133">When you've finished building the formula, press ENTER.</span><span class="sxs-lookup"><span data-stu-id="82355-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="82355-134">The new column is added to the far right of the table.</span><span class="sxs-lookup"><span data-stu-id="82355-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="82355-135">Rename the column to **DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="82355-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="82355-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span><span class="sxs-lookup"><span data-stu-id="82355-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="82355-137">Moving columns in your table makes it easier to navigate.</span><span class="sxs-lookup"><span data-stu-id="82355-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="82355-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span><span class="sxs-lookup"><span data-stu-id="82355-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="82355-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span><span class="sxs-lookup"><span data-stu-id="82355-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="82355-140">In the **DimProduct** table, scroll to the far right of the table.</span><span class="sxs-lookup"><span data-stu-id="82355-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="82355-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span><span class="sxs-lookup"><span data-stu-id="82355-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="82355-142">In the formula bar, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="82355-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="82355-143">Rename the column to **ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="82355-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="82355-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span><span class="sxs-lookup"><span data-stu-id="82355-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="82355-145">Hierarchies cannot span more than one table.</span><span class="sxs-lookup"><span data-stu-id="82355-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="82355-146">You create hierarchies later in Lesson 9.</span><span class="sxs-lookup"><span data-stu-id="82355-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="82355-147">Create a ProductCategoryName calculated column in the DimProduct table</span><span class="sxs-lookup"><span data-stu-id="82355-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="82355-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span><span class="sxs-lookup"><span data-stu-id="82355-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="82355-149">In the formula bar, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="82355-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="82355-150">Rename the column to **ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="82355-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="82355-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span><span class="sxs-lookup"><span data-stu-id="82355-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="82355-152">Hierarchies cannot span more than one table.</span><span class="sxs-lookup"><span data-stu-id="82355-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="82355-153">Create a Margin calculated column in the FactInternetSales table</span><span class="sxs-lookup"><span data-stu-id="82355-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="82355-154">In the model designer, select the **FactInternetSales** table.</span><span class="sxs-lookup"><span data-stu-id="82355-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="82355-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span><span class="sxs-lookup"><span data-stu-id="82355-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="82355-156">In the formula bar, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="82355-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="82355-157">Rename the column to **Margin**.</span><span class="sxs-lookup"><span data-stu-id="82355-157">Rename the column to **Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="82355-159">The Margin calculated column is used to analyze profit margins for each sale.</span><span class="sxs-lookup"><span data-stu-id="82355-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="82355-160">What's next?</span><span class="sxs-lookup"><span data-stu-id="82355-160">What's next?</span></span>
<span data-ttu-id="82355-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="82355-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
