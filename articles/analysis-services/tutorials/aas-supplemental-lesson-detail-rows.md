---
title: 'Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs'
description: Describes how to create a Detail Rows Expression in the Azure Analysis Services tutorial.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 626258488afec4b3c3f025ae85bd3b5866aa0cf3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864928"
---
# <a name="supplemental-lesson---detail-rows"></a>Supplemental lesson - Detail Rows

In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression. A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure. 
  
Estimated time to complete this lesson: **10 minutes**  
  
## <a name="prerequisites"></a>Prerequisites  
This supplemental lesson is part of a tabular modeling tutorial. Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.  
  
## <a name="whats-the-issue"></a>What's the issue?
Let's look at the details of the InternetTotalSales measure, before adding a Detail Rows Expression.

1.  In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.
  
2.  In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**. The PivotTable now gives an aggregated results from the InternetTotalSales measure by regions and year. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. In the PivotTable, double-click an aggregated value for a year and a region name. The value for Australia and the year 2014. A new sheet opens containing data, but not useful data.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
The goal here is a table containing columns and rows of data that contribute to the aggregated result of the InternetTotalSales measure. To do that, add a Detail Rows Expression as a property of the measure.

## <a name="add-a-detail-rows-expression"></a>Add a Detail Rows Expression

#### <a name="to-create-a-detail-rows-expression"></a>To create a Detail Rows Expression 
  
1. In the FactInternetSales table's measure grid, click the **InternetTotalSales** measure. 

2. In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. In DAX Editor, enter the following expression:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.

4. Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value. This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Redeploy your model.

  
## <a name="see-also"></a>See also  

[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Supplemental lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Supplemental lesson - Ragged hierarchies](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
 