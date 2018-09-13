---
title: 'Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs'
description: Describes how to create measures in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 6cf880cf132168d60ff49c2e7ea571cd8e89d36f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967706"
---
# <a name="create-measures"></a><span data-ttu-id="20799-103">Create measures</span><span class="sxs-lookup"><span data-stu-id="20799-103">Create measures</span></span>

<span data-ttu-id="20799-104">In this lesson, you create measures to be included in your model.</span><span class="sxs-lookup"><span data-stu-id="20799-104">In this lesson, you create measures to be included in your model.</span></span> <span data-ttu-id="20799-105">Similar to the calculated columns you created, a measure is a calculation created by using a DAX formula.</span><span class="sxs-lookup"><span data-stu-id="20799-105">Similar to the calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="20799-106">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span><span class="sxs-lookup"><span data-stu-id="20799-106">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="20799-107">For example, a particular column or slicer added to the Row Labels field in a PivotTable.</span><span class="sxs-lookup"><span data-stu-id="20799-107">For example, a particular column or slicer added to the Row Labels field in a PivotTable.</span></span> <span data-ttu-id="20799-108">A value for each cell in the filter is then calculated by the applied measure.</span><span class="sxs-lookup"><span data-stu-id="20799-108">A value for each cell in the filter is then calculated by the applied measure.</span></span> <span data-ttu-id="20799-109">Measures are powerful, flexible calculations that you want to include in almost all tabular models to perform dynamic calculations on numerical data.</span><span class="sxs-lookup"><span data-stu-id="20799-109">Measures are powerful, flexible calculations that you want to include in almost all tabular models to perform dynamic calculations on numerical data.</span></span> <span data-ttu-id="20799-110">To learn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="20799-110">To learn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="20799-111">To create measures, you use the *Measure Grid*.</span><span class="sxs-lookup"><span data-stu-id="20799-111">To create measures, you use the *Measure Grid*.</span></span> <span data-ttu-id="20799-112">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span><span class="sxs-lookup"><span data-stu-id="20799-112">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="20799-113">The measure grid appears below a table in the model designer when in Data View.</span><span class="sxs-lookup"><span data-stu-id="20799-113">The measure grid appears below a table in the model designer when in Data View.</span></span> <span data-ttu-id="20799-114">To hide or show the measure grid for a table, click the **Table** menu, and then click **Show Measure Grid**.</span><span class="sxs-lookup"><span data-stu-id="20799-114">To hide or show the measure grid for a table, click the **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="20799-115">You can create a measure by clicking an empty cell in the measure grid, and then typing a DAX formula in the formula bar.</span><span class="sxs-lookup"><span data-stu-id="20799-115">You can create a measure by clicking an empty cell in the measure grid, and then typing a DAX formula in the formula bar.</span></span> <span data-ttu-id="20799-116">When you click ENTER to complete the formula, the measure then appears in the cell.</span><span class="sxs-lookup"><span data-stu-id="20799-116">When you click ENTER to complete the formula, the measure then appears in the cell.</span></span> <span data-ttu-id="20799-117">You can also create measures using a standard aggregation function by clicking a column, and then clicking the AutoSum button (**∑**) on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="20799-117">You can also create measures using a standard aggregation function by clicking a column, and then clicking the AutoSum button (**∑**) on the toolbar.</span></span> <span data-ttu-id="20799-118">Measures created using the AutoSum feature appear in the measure grid cell directly beneath the column, but can be moved.</span><span class="sxs-lookup"><span data-stu-id="20799-118">Measures created using the AutoSum feature appear in the measure grid cell directly beneath the column, but can be moved.</span></span>  
  
<span data-ttu-id="20799-119">In this lesson, you create measures by both entering a DAX formula in the formula bar, and by using the AutoSum feature.</span><span class="sxs-lookup"><span data-stu-id="20799-119">In this lesson, you create measures by both entering a DAX formula in the formula bar, and by using the AutoSum feature.</span></span>  
  
<span data-ttu-id="20799-120">Estimated time to complete this lesson: **30 minutes**</span><span class="sxs-lookup"><span data-stu-id="20799-120">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="20799-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="20799-121">Prerequisites</span></span>  
<span data-ttu-id="20799-122">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="20799-122">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="20799-123">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="20799-123">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="20799-124">Create measures</span><span class="sxs-lookup"><span data-stu-id="20799-124">Create measures</span></span>  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a><span data-ttu-id="20799-125">To create a DaysCurrentQuarterToDate measure in the DimDate table</span><span class="sxs-lookup"><span data-stu-id="20799-125">To create a DaysCurrentQuarterToDate measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="20799-126">In the model designer, click the **DimDate** table.</span><span class="sxs-lookup"><span data-stu-id="20799-126">In the model designer, click the **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="20799-127">In the measure grid, click the top-left empty cell.</span><span class="sxs-lookup"><span data-stu-id="20799-127">In the measure grid, click the top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="20799-128">In the formula bar, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="20799-128">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="20799-129">Notice the top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by the result, **92**.</span><span class="sxs-lookup"><span data-stu-id="20799-129">Notice the top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by the result, **92**.</span></span> <span data-ttu-id="20799-130">The result is not relevant at this point because no user filter has been applied.</span><span class="sxs-lookup"><span data-stu-id="20799-130">The result is not relevant at this point because no user filter has been applied.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="20799-132">Unlike calculated columns, with measure formulas you can type the measure name, followed by a colon, followed by the formula expression.</span><span class="sxs-lookup"><span data-stu-id="20799-132">Unlike calculated columns, with measure formulas you can type the measure name, followed by a colon, followed by the formula expression.</span></span>

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a><span data-ttu-id="20799-133">To create a DaysInCurrentQuarter measure in the DimDate table</span><span class="sxs-lookup"><span data-stu-id="20799-133">To create a DaysInCurrentQuarter measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="20799-134">With the **DimDate** table still active in the model designer, in the measure grid, click the empty cell below the measure you created.</span><span class="sxs-lookup"><span data-stu-id="20799-134">With the **DimDate** table still active in the model designer, in the measure grid, click the empty cell below the measure you created.</span></span>  
  
2.  <span data-ttu-id="20799-135">In the formula bar, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="20799-135">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="20799-136">When creating a comparison ratio between one incomplete period and the previous period.</span><span class="sxs-lookup"><span data-stu-id="20799-136">When creating a comparison ratio between one incomplete period and the previous period.</span></span> <span data-ttu-id="20799-137">The formula must calculate the proportion of the period that has elapsed and compare it to the same proportion in the previous period.</span><span class="sxs-lookup"><span data-stu-id="20799-137">The formula must calculate the proportion of the period that has elapsed and compare it to the same proportion in the previous period.</span></span> <span data-ttu-id="20799-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives the proportion elapsed in the current period.</span><span class="sxs-lookup"><span data-stu-id="20799-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives the proportion elapsed in the current period.</span></span>  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a><span data-ttu-id="20799-139">To create an InternetDistinctCountSalesOrder measure in the FactInternetSales table</span><span class="sxs-lookup"><span data-stu-id="20799-139">To create an InternetDistinctCountSalesOrder measure in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="20799-140">Click the **FactInternetSales** table.</span><span class="sxs-lookup"><span data-stu-id="20799-140">Click the **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="20799-141">Click the **SalesOrderNumber** column heading.</span><span class="sxs-lookup"><span data-stu-id="20799-141">Click the **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="20799-142">On the toolbar, click the down-arrow next to the AutoSum (**∑**) button, and then select **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="20799-142">On the toolbar, click the down-arrow next to the AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="20799-143">The AutoSum feature automatically creates a measure for the selected column using the DistinctCount standard aggregation formula.</span><span class="sxs-lookup"><span data-stu-id="20799-143">The AutoSum feature automatically creates a measure for the selected column using the DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="20799-145">In the measure grid, click the new measure, and then in the **Properties** window, in **Measure Name**, rename the measure to **InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="20799-145">In the measure grid, click the new measure, and then in the **Properties** window, in **Measure Name**, rename the measure to **InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a><span data-ttu-id="20799-146">To create additional measures in the FactInternetSales table</span><span class="sxs-lookup"><span data-stu-id="20799-146">To create additional measures in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="20799-147">By using the AutoSum feature, create and name the following measures:</span><span class="sxs-lookup"><span data-stu-id="20799-147">By using the AutoSum feature, create and name the following measures:</span></span>  

    |<span data-ttu-id="20799-148">Column</span><span class="sxs-lookup"><span data-stu-id="20799-148">Column</span></span>|<span data-ttu-id="20799-149">Measure name</span><span class="sxs-lookup"><span data-stu-id="20799-149">Measure name</span></span>|<span data-ttu-id="20799-150">AutoSum (∑)</span><span class="sxs-lookup"><span data-stu-id="20799-150">AutoSum (∑)</span></span>|<span data-ttu-id="20799-151">Formula</span><span class="sxs-lookup"><span data-stu-id="20799-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="20799-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="20799-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="20799-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="20799-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="20799-154">Count</span><span class="sxs-lookup"><span data-stu-id="20799-154">Count</span></span>|<span data-ttu-id="20799-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="20799-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="20799-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="20799-156">OrderQuantity</span></span>|<span data-ttu-id="20799-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="20799-157">InternetTotalUnits</span></span>|<span data-ttu-id="20799-158">Sum</span><span class="sxs-lookup"><span data-stu-id="20799-158">Sum</span></span>|<span data-ttu-id="20799-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="20799-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="20799-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="20799-160">DiscountAmount</span></span>|<span data-ttu-id="20799-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="20799-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="20799-162">Sum</span><span class="sxs-lookup"><span data-stu-id="20799-162">Sum</span></span>|<span data-ttu-id="20799-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="20799-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="20799-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="20799-164">TotalProductCost</span></span>|<span data-ttu-id="20799-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="20799-165">InternetTotalProductCost</span></span>|<span data-ttu-id="20799-166">Sum</span><span class="sxs-lookup"><span data-stu-id="20799-166">Sum</span></span>|<span data-ttu-id="20799-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="20799-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="20799-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="20799-168">SalesAmount</span></span>|<span data-ttu-id="20799-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="20799-169">InternetTotalSales</span></span>|<span data-ttu-id="20799-170">Sum</span><span class="sxs-lookup"><span data-stu-id="20799-170">Sum</span></span>|<span data-ttu-id="20799-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="20799-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="20799-172">Margin</span><span class="sxs-lookup"><span data-stu-id="20799-172">Margin</span></span>|<span data-ttu-id="20799-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="20799-173">InternetTotalMargin</span></span>|<span data-ttu-id="20799-174">Sum</span><span class="sxs-lookup"><span data-stu-id="20799-174">Sum</span></span>|<span data-ttu-id="20799-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="20799-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="20799-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="20799-176">TaxAmt</span></span>|<span data-ttu-id="20799-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="20799-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="20799-178">Sum</span><span class="sxs-lookup"><span data-stu-id="20799-178">Sum</span></span>|<span data-ttu-id="20799-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="20799-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="20799-180">Freight</span><span class="sxs-lookup"><span data-stu-id="20799-180">Freight</span></span>|<span data-ttu-id="20799-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="20799-181">InternetTotalFreight</span></span>|<span data-ttu-id="20799-182">Sum</span><span class="sxs-lookup"><span data-stu-id="20799-182">Sum</span></span>|<span data-ttu-id="20799-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="20799-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="20799-184">By clicking an empty cell in the measure grid, and by using the formula bar, create,  the following custom measures in order:</span><span class="sxs-lookup"><span data-stu-id="20799-184">By clicking an empty cell in the measure grid, and by using the formula bar, create,  the following custom measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="20799-185">Measures created for the FactInternetSales table can be used to analyze critical financial data such as sales, costs, and profit margin for items defined by the user selected filter.</span><span class="sxs-lookup"><span data-stu-id="20799-185">Measures created for the FactInternetSales table can be used to analyze critical financial data such as sales, costs, and profit margin for items defined by the user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="20799-186">What's next?</span><span class="sxs-lookup"><span data-stu-id="20799-186">What's next?</span></span>
<span data-ttu-id="20799-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="20799-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
