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
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="688b3-103">Supplemental lesson - Detail Rows</span><span class="sxs-lookup"><span data-stu-id="688b3-103">Supplemental lesson - Detail Rows</span></span>

<span data-ttu-id="688b3-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span><span class="sxs-lookup"><span data-stu-id="688b3-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="688b3-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span><span class="sxs-lookup"><span data-stu-id="688b3-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="688b3-106">Estimated time to complete this lesson: **10 minutes**</span><span class="sxs-lookup"><span data-stu-id="688b3-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="688b3-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="688b3-107">Prerequisites</span></span>  
<span data-ttu-id="688b3-108">This supplemental lesson is part of a tabular modeling tutorial.</span><span class="sxs-lookup"><span data-stu-id="688b3-108">This supplemental lesson is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="688b3-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span><span class="sxs-lookup"><span data-stu-id="688b3-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="whats-the-issue"></a><span data-ttu-id="688b3-110">What's the issue?</span><span class="sxs-lookup"><span data-stu-id="688b3-110">What's the issue?</span></span>
<span data-ttu-id="688b3-111">Let's look at the details of the InternetTotalSales measure, before adding a Detail Rows Expression.</span><span class="sxs-lookup"><span data-stu-id="688b3-111">Let's look at the details of the InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="688b3-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span><span class="sxs-lookup"><span data-stu-id="688b3-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="688b3-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span><span class="sxs-lookup"><span data-stu-id="688b3-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="688b3-114">The PivotTable now gives an aggregated results from the InternetTotalSales measure by regions and year.</span><span class="sxs-lookup"><span data-stu-id="688b3-114">The PivotTable now gives an aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="688b3-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span><span class="sxs-lookup"><span data-stu-id="688b3-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="688b3-117">The value for Australia and the year 2014.</span><span class="sxs-lookup"><span data-stu-id="688b3-117">The value for Australia and the year 2014.</span></span> <span data-ttu-id="688b3-118">A new sheet opens containing data, but not useful data.</span><span class="sxs-lookup"><span data-stu-id="688b3-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="688b3-120">The goal here is a table containing columns and rows of data that contribute to the aggregated result of the InternetTotalSales measure.</span><span class="sxs-lookup"><span data-stu-id="688b3-120">The goal here is a table containing columns and rows of data that contribute to the aggregated result of the InternetTotalSales measure.</span></span> <span data-ttu-id="688b3-121">To do that, add a Detail Rows Expression as a property of the measure.</span><span class="sxs-lookup"><span data-stu-id="688b3-121">To do that, add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="688b3-122">Add a Detail Rows Expression</span><span class="sxs-lookup"><span data-stu-id="688b3-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="688b3-123">To create a Detail Rows Expression</span><span class="sxs-lookup"><span data-stu-id="688b3-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="688b3-124">In the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span><span class="sxs-lookup"><span data-stu-id="688b3-124">In the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="688b3-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span><span class="sxs-lookup"><span data-stu-id="688b3-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="688b3-127">In DAX Editor, enter the following expression:</span><span class="sxs-lookup"><span data-stu-id="688b3-127">In DAX Editor, enter the following expression:</span></span>

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

    <span data-ttu-id="688b3-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span><span class="sxs-lookup"><span data-stu-id="688b3-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="688b3-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span><span class="sxs-lookup"><span data-stu-id="688b3-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="688b3-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span><span class="sxs-lookup"><span data-stu-id="688b3-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="688b3-132">Redeploy your model.</span><span class="sxs-lookup"><span data-stu-id="688b3-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="688b3-133">See also</span><span class="sxs-lookup"><span data-stu-id="688b3-133">See also</span></span>  

<span data-ttu-id="688b3-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="688b3-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
<span data-ttu-id="688b3-135">[Supplemental lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="688b3-135">[Supplemental lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
[<span data-ttu-id="688b3-136">Supplemental lesson - Ragged hierarchies</span><span class="sxs-lookup"><span data-stu-id="688b3-136">Supplemental lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
 