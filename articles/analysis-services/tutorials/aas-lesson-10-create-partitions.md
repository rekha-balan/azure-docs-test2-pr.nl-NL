---
title: 'Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs'
description: Describes how to create partitions in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 7a445cd0e5c737371fa56f1e4dffa49d1915b15a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857404"
---
# <a name="create-partitions"></a><span data-ttu-id="1c349-103">Create partitions</span><span class="sxs-lookup"><span data-stu-id="1c349-103">Create partitions</span></span>

<span data-ttu-id="1c349-104">In this lesson, you create partitions to divide the FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span><span class="sxs-lookup"><span data-stu-id="1c349-104">In this lesson, you create partitions to divide the FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="1c349-105">By default, every table you include in your model has one partition, which includes all the table’s columns and rows.</span><span class="sxs-lookup"><span data-stu-id="1c349-105">By default, every table you include in your model has one partition, which includes all the table’s columns and rows.</span></span> <span data-ttu-id="1c349-106">For the FactInternetSales table, we want to divide the data by year; one partition for each of the table’s five years.</span><span class="sxs-lookup"><span data-stu-id="1c349-106">For the FactInternetSales table, we want to divide the data by year; one partition for each of the table’s five years.</span></span> <span data-ttu-id="1c349-107">Each partition can then be processed independently.</span><span class="sxs-lookup"><span data-stu-id="1c349-107">Each partition can then be processed independently.</span></span> <span data-ttu-id="1c349-108">To learn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="1c349-108">To learn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="1c349-109">Estimated time to complete this lesson: **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="1c349-109">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="1c349-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1c349-110">Prerequisites</span></span>  
<span data-ttu-id="1c349-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="1c349-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="1c349-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="1c349-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="1c349-113">Create partitions</span><span class="sxs-lookup"><span data-stu-id="1c349-113">Create partitions</span></span>  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a><span data-ttu-id="1c349-114">To create partitions in the FactInternetSales table</span><span class="sxs-lookup"><span data-stu-id="1c349-114">To create partitions in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="1c349-115">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span><span class="sxs-lookup"><span data-stu-id="1c349-115">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="1c349-116">In Partition Manager, click **Copy**, and then change the name to **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="1c349-116">In Partition Manager, click **Copy**, and then change the name to **FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="1c349-117">Because you want the partition to include only those rows within a certain period, for the year 2010, you must modify the query expression.</span><span class="sxs-lookup"><span data-stu-id="1c349-117">Because you want the partition to include only those rows within a certain period, for the year 2010, you must modify the query expression.</span></span>
  
4.  <span data-ttu-id="1c349-118">Click **Design** to open Query Editor, and then click the **FactInternetSales2010** query.</span><span class="sxs-lookup"><span data-stu-id="1c349-118">Click **Design** to open Query Editor, and then click the **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="1c349-119">In preview, click the down arrow in the **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span><span class="sxs-lookup"><span data-stu-id="1c349-119">In preview, click the down arrow in the **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="1c349-121">In the Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in the date field, enter **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="1c349-121">In the Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in the date field, enter **1/1/2010**.</span></span> <span data-ttu-id="1c349-122">Leave the **And** operator selected, then select **is before**, then in the date field, enter **1/1/2011**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c349-122">Leave the **And** operator selected, then select **is before**, then in the date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="1c349-124">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span><span class="sxs-lookup"><span data-stu-id="1c349-124">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="1c349-125">This filter is to select only order dates from 2010.</span><span class="sxs-lookup"><span data-stu-id="1c349-125">This filter is to select only order dates from 2010.</span></span>

8.  <span data-ttu-id="1c349-126">Click **Import**.</span><span class="sxs-lookup"><span data-stu-id="1c349-126">Click **Import**.</span></span>

    <span data-ttu-id="1c349-127">In Partition Manager, notice the query expression now has an additional Filtered Rows clause.</span><span class="sxs-lookup"><span data-stu-id="1c349-127">In Partition Manager, notice the query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="1c349-129">This statement specifies this partition should include only the data in those rows where the OrderDate is in the 2010 calendar year as specified in the filtered rows clause.</span><span class="sxs-lookup"><span data-stu-id="1c349-129">This statement specifies this partition should include only the data in those rows where the OrderDate is in the 2010 calendar year as specified in the filtered rows clause.</span></span>  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a><span data-ttu-id="1c349-130">To create a partition for the 2011 year</span><span class="sxs-lookup"><span data-stu-id="1c349-130">To create a partition for the 2011 year</span></span>  
  
1.  <span data-ttu-id="1c349-131">In the partitions list, click the **FactInternetSales2010** partition you created, and then click **Copy**.</span><span class="sxs-lookup"><span data-stu-id="1c349-131">In the partitions list, click the **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="1c349-132">Change the partition name to **FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="1c349-132">Change the partition name to **FactInternetSales2011**.</span></span> 

    <span data-ttu-id="1c349-133">You do not need to use Query Editor to create a new filtered rows clause.</span><span class="sxs-lookup"><span data-stu-id="1c349-133">You do not need to use Query Editor to create a new filtered rows clause.</span></span> <span data-ttu-id="1c349-134">Because you created a copy of the query for 2010, all you need to do is make a slight change in the query for 2011.</span><span class="sxs-lookup"><span data-stu-id="1c349-134">Because you created a copy of the query for 2010, all you need to do is make a slight change in the query for 2011.</span></span>
  
2.  <span data-ttu-id="1c349-135">In **Query Expression**, in-order for this partition to include only those rows for the 2011 year, replace the years in the Filtered Rows clause with **2011** and **2012**, respectively, like:</span><span class="sxs-lookup"><span data-stu-id="1c349-135">In **Query Expression**, in-order for this partition to include only those rows for the 2011 year, replace the years in the Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="1c349-136">To create partitions for 2012, 2013, and 2014.</span><span class="sxs-lookup"><span data-stu-id="1c349-136">To create partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="1c349-137">Follow the previous steps, creating partitions for 2012, 2013, and 2014, changing the years in the Filtered Rows clause to include only rows for that year.</span><span class="sxs-lookup"><span data-stu-id="1c349-137">Follow the previous steps, creating partitions for 2012, 2013, and 2014, changing the years in the Filtered Rows clause to include only rows for that year.</span></span> 
  

## <a name="delete-the-factinternetsales-partition"></a><span data-ttu-id="1c349-138">Delete the FactInternetSales partition</span><span class="sxs-lookup"><span data-stu-id="1c349-138">Delete the FactInternetSales partition</span></span>
<span data-ttu-id="1c349-139">Now that you have partitions for each year, you can delete the FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span><span class="sxs-lookup"><span data-stu-id="1c349-139">Now that you have partitions for each year, you can delete the FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="to-delete-the-factinternetsales-partition"></a><span data-ttu-id="1c349-140">To delete the FactInternetSales partition</span><span class="sxs-lookup"><span data-stu-id="1c349-140">To delete the FactInternetSales partition</span></span>
-  <span data-ttu-id="1c349-141">Click the FactInternetSales partition, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1c349-141">Click the FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="1c349-142">Process partitions</span><span class="sxs-lookup"><span data-stu-id="1c349-142">Process partitions</span></span>  
<span data-ttu-id="1c349-143">In Partition Manager, notice the **Last Processed** column for each of the new partitions you created shows these partitions have never been processed.</span><span class="sxs-lookup"><span data-stu-id="1c349-143">In Partition Manager, notice the **Last Processed** column for each of the new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="1c349-144">When you create partitions, you should run a Process Partitions or Process Table operation to refresh the data in those partitions.</span><span class="sxs-lookup"><span data-stu-id="1c349-144">When you create partitions, you should run a Process Partitions or Process Table operation to refresh the data in those partitions.</span></span>  
  
#### <a name="to-process-the-factinternetsales-partitions"></a><span data-ttu-id="1c349-145">To process the FactInternetSales partitions</span><span class="sxs-lookup"><span data-stu-id="1c349-145">To process the FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="1c349-146">Click **OK** to close Partition Manager.</span><span class="sxs-lookup"><span data-stu-id="1c349-146">Click **OK** to close Partition Manager.</span></span>  
  
2.  <span data-ttu-id="1c349-147">Click the **FactInternetSales** table, then click the **Model** menu > **Process** > **Process Partitions**.</span><span class="sxs-lookup"><span data-stu-id="1c349-147">Click the **FactInternetSales** table, then click the **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="1c349-148">In the Process Partitions dialog box, verify **Mode** is set to **Process Default**.</span><span class="sxs-lookup"><span data-stu-id="1c349-148">In the Process Partitions dialog box, verify **Mode** is set to **Process Default**.</span></span>  
  
4.  <span data-ttu-id="1c349-149">Select the checkbox in the **Process** column for each of the five partitions you created, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c349-149">Select the checkbox in the **Process** column for each of the five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="1c349-151">If you're prompted for Impersonation credentials, enter the Windows user name and password you specified in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="1c349-151">If you're prompted for Impersonation credentials, enter the Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="1c349-152">The **Data Processing** dialog box appears and displays process details for each partition.</span><span class="sxs-lookup"><span data-stu-id="1c349-152">The **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="1c349-153">Notice that a different number of rows for each partition are transferred.</span><span class="sxs-lookup"><span data-stu-id="1c349-153">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="1c349-154">Each partition includes only those rows for the year specified in the WHERE clause in the SQL Statement.</span><span class="sxs-lookup"><span data-stu-id="1c349-154">Each partition includes only those rows for the year specified in the WHERE clause in the SQL Statement.</span></span> <span data-ttu-id="1c349-155">When processing is finished, go ahead and close the Data Processing dialog box.</span><span class="sxs-lookup"><span data-stu-id="1c349-155">When processing is finished, go ahead and close the Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="1c349-157">What's next?</span><span class="sxs-lookup"><span data-stu-id="1c349-157">What's next?</span></span>
<span data-ttu-id="1c349-158">Go to the next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1c349-158">Go to the next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
