---
title: 'Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs'
description: Describes how to fix ragged hierarchies in the Azure Analysis Services tutorial.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 9fdf332727c4d66af2d5394fb26e84f6ea9d963f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867575"
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="52e5c-103">Supplemental lesson - Ragged hierarchies</span><span class="sxs-lookup"><span data-stu-id="52e5c-103">Supplemental lesson - Ragged hierarchies</span></span>

<span data-ttu-id="52e5c-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span><span class="sxs-lookup"><span data-stu-id="52e5c-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="52e5c-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span><span class="sxs-lookup"><span data-stu-id="52e5c-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="52e5c-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span><span class="sxs-lookup"><span data-stu-id="52e5c-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="52e5c-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span><span class="sxs-lookup"><span data-stu-id="52e5c-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="52e5c-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span><span class="sxs-lookup"><span data-stu-id="52e5c-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="52e5c-110">The **Default** setting assumes there are no blank members at any level.</span><span class="sxs-lookup"><span data-stu-id="52e5c-110">The **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="52e5c-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span><span class="sxs-lookup"><span data-stu-id="52e5c-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span></span>  
  
<span data-ttu-id="52e5c-112">Estimated time to complete this lesson: **20 minutes**</span><span class="sxs-lookup"><span data-stu-id="52e5c-112">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="52e5c-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="52e5c-113">Prerequisites</span></span>  
<span data-ttu-id="52e5c-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span><span class="sxs-lookup"><span data-stu-id="52e5c-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="52e5c-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span><span class="sxs-lookup"><span data-stu-id="52e5c-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="52e5c-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span><span class="sxs-lookup"><span data-stu-id="52e5c-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="52e5c-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span><span class="sxs-lookup"><span data-stu-id="52e5c-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="52e5c-118">That part takes about 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="52e5c-118">That part takes about 15 minutes.</span></span> <span data-ttu-id="52e5c-119">Then, you get to solve it in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="52e5c-119">Then, you get to solve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="52e5c-120">Add tables and objects</span><span class="sxs-lookup"><span data-stu-id="52e5c-120">Add tables and objects</span></span>
  
### <a name="to-add-new-tables-to-your-model"></a><span data-ttu-id="52e5c-121">To add new tables to your model</span><span class="sxs-lookup"><span data-stu-id="52e5c-121">To add new tables to your model</span></span>
  
1.  <span data-ttu-id="52e5c-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span><span class="sxs-lookup"><span data-stu-id="52e5c-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="52e5c-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="52e5c-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="52e5c-124">In Query Editor, click **Import**</span><span class="sxs-lookup"><span data-stu-id="52e5c-124">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="52e5c-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="52e5c-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="52e5c-126">Table 1</span><span class="sxs-lookup"><span data-stu-id="52e5c-126">Table 1</span></span>           | <span data-ttu-id="52e5c-127">Column</span><span class="sxs-lookup"><span data-stu-id="52e5c-127">Column</span></span>       | <span data-ttu-id="52e5c-128">Filter Direction</span><span class="sxs-lookup"><span data-stu-id="52e5c-128">Filter Direction</span></span>   | <span data-ttu-id="52e5c-129">Table 2</span><span class="sxs-lookup"><span data-stu-id="52e5c-129">Table 2</span></span>     | <span data-ttu-id="52e5c-130">Column</span><span class="sxs-lookup"><span data-stu-id="52e5c-130">Column</span></span>      | <span data-ttu-id="52e5c-131">Active</span><span class="sxs-lookup"><span data-stu-id="52e5c-131">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="52e5c-132">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="52e5c-132">FactResellerSales</span></span> | <span data-ttu-id="52e5c-133">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="52e5c-133">OrderDateKey</span></span> | <span data-ttu-id="52e5c-134">Default</span><span class="sxs-lookup"><span data-stu-id="52e5c-134">Default</span></span>            | <span data-ttu-id="52e5c-135">DimDate</span><span class="sxs-lookup"><span data-stu-id="52e5c-135">DimDate</span></span>     | <span data-ttu-id="52e5c-136">Date</span><span class="sxs-lookup"><span data-stu-id="52e5c-136">Date</span></span>        | <span data-ttu-id="52e5c-137">Yes</span><span class="sxs-lookup"><span data-stu-id="52e5c-137">Yes</span></span>    |
    | <span data-ttu-id="52e5c-138">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="52e5c-138">FactResellerSales</span></span> | <span data-ttu-id="52e5c-139">DueDate</span><span class="sxs-lookup"><span data-stu-id="52e5c-139">DueDate</span></span>      | <span data-ttu-id="52e5c-140">Default</span><span class="sxs-lookup"><span data-stu-id="52e5c-140">Default</span></span>            | <span data-ttu-id="52e5c-141">DimDate</span><span class="sxs-lookup"><span data-stu-id="52e5c-141">DimDate</span></span>     | <span data-ttu-id="52e5c-142">Date</span><span class="sxs-lookup"><span data-stu-id="52e5c-142">Date</span></span>        | <span data-ttu-id="52e5c-143">No</span><span class="sxs-lookup"><span data-stu-id="52e5c-143">No</span></span>     |
    | <span data-ttu-id="52e5c-144">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="52e5c-144">FactResellerSales</span></span> | <span data-ttu-id="52e5c-145">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="52e5c-145">ShipDateKey</span></span>  | <span data-ttu-id="52e5c-146">Default</span><span class="sxs-lookup"><span data-stu-id="52e5c-146">Default</span></span>            | <span data-ttu-id="52e5c-147">DimDate</span><span class="sxs-lookup"><span data-stu-id="52e5c-147">DimDate</span></span>     | <span data-ttu-id="52e5c-148">Date</span><span class="sxs-lookup"><span data-stu-id="52e5c-148">Date</span></span>        | <span data-ttu-id="52e5c-149">No</span><span class="sxs-lookup"><span data-stu-id="52e5c-149">No</span></span>     |
    | <span data-ttu-id="52e5c-150">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="52e5c-150">FactResellerSales</span></span> | <span data-ttu-id="52e5c-151">ProductKey</span><span class="sxs-lookup"><span data-stu-id="52e5c-151">ProductKey</span></span>   | <span data-ttu-id="52e5c-152">Default</span><span class="sxs-lookup"><span data-stu-id="52e5c-152">Default</span></span>            | <span data-ttu-id="52e5c-153">DimProduct</span><span class="sxs-lookup"><span data-stu-id="52e5c-153">DimProduct</span></span>  | <span data-ttu-id="52e5c-154">ProductKey</span><span class="sxs-lookup"><span data-stu-id="52e5c-154">ProductKey</span></span>  | <span data-ttu-id="52e5c-155">Yes</span><span class="sxs-lookup"><span data-stu-id="52e5c-155">Yes</span></span>    |
    | <span data-ttu-id="52e5c-156">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="52e5c-156">FactResellerSales</span></span> | <span data-ttu-id="52e5c-157">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="52e5c-157">EmployeeKey</span></span>  | <span data-ttu-id="52e5c-158">To Both Tables</span><span class="sxs-lookup"><span data-stu-id="52e5c-158">To Both Tables</span></span> | <span data-ttu-id="52e5c-159">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="52e5c-159">DimEmployee</span></span> | <span data-ttu-id="52e5c-160">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="52e5c-160">EmployeeKey</span></span> | <span data-ttu-id="52e5c-161">Yes</span><span class="sxs-lookup"><span data-stu-id="52e5c-161">Yes</span></span>    |

5. <span data-ttu-id="52e5c-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="52e5c-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="52e5c-163">**Path**</span><span class="sxs-lookup"><span data-stu-id="52e5c-163">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="52e5c-164">**FullName**</span><span class="sxs-lookup"><span data-stu-id="52e5c-164">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="52e5c-165">**Level1**</span><span class="sxs-lookup"><span data-stu-id="52e5c-165">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="52e5c-166">**Level2**</span><span class="sxs-lookup"><span data-stu-id="52e5c-166">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    <span data-ttu-id="52e5c-167">**Level3**</span><span class="sxs-lookup"><span data-stu-id="52e5c-167">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    <span data-ttu-id="52e5c-168">**Level4**</span><span class="sxs-lookup"><span data-stu-id="52e5c-168">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    <span data-ttu-id="52e5c-169">**Level5**</span><span class="sxs-lookup"><span data-stu-id="52e5c-169">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  <span data-ttu-id="52e5c-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span><span class="sxs-lookup"><span data-stu-id="52e5c-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="52e5c-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="52e5c-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="52e5c-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="52e5c-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="52e5c-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span><span class="sxs-lookup"><span data-stu-id="52e5c-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="52e5c-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span><span class="sxs-lookup"><span data-stu-id="52e5c-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="52e5c-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span><span class="sxs-lookup"><span data-stu-id="52e5c-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="52e5c-177">There are many rows where blank members are shown.</span><span class="sxs-lookup"><span data-stu-id="52e5c-177">There are many rows where blank members are shown.</span></span>

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a><span data-ttu-id="52e5c-178">To fix the ragged hierarchy by setting the Hide members property</span><span class="sxs-lookup"><span data-stu-id="52e5c-178">To fix the ragged hierarchy by setting the Hide members property</span></span>

1.  <span data-ttu-id="52e5c-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span><span class="sxs-lookup"><span data-stu-id="52e5c-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="52e5c-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span><span class="sxs-lookup"><span data-stu-id="52e5c-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="52e5c-182">Back in Excel, refresh the PivotTable.</span><span class="sxs-lookup"><span data-stu-id="52e5c-182">Back in Excel, refresh the PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="52e5c-184">Now that looks a whole lot better!</span><span class="sxs-lookup"><span data-stu-id="52e5c-184">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="52e5c-185">See Also</span><span class="sxs-lookup"><span data-stu-id="52e5c-185">See Also</span></span>   
[<span data-ttu-id="52e5c-186">Lesson 9: Create hierarchies</span><span class="sxs-lookup"><span data-stu-id="52e5c-186">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="52e5c-187">Supplemental Lesson - Dynamic security</span><span class="sxs-lookup"><span data-stu-id="52e5c-187">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="52e5c-188">Supplemental Lesson - Detail rows</span><span class="sxs-lookup"><span data-stu-id="52e5c-188">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  
