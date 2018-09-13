---
title: 'Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs'
description: Describes how to create hierarchies in a tabular model.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 928fe227a74c5c63ccdfb364b0e2423d7b544864
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968122"
---
# <a name="create-hierarchies"></a><span data-ttu-id="2d649-103">Create hierarchies</span><span class="sxs-lookup"><span data-stu-id="2d649-103">Create hierarchies</span></span>

<span data-ttu-id="2d649-104">In this lesson, you create hierarchies.</span><span class="sxs-lookup"><span data-stu-id="2d649-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="2d649-105">Hierarchies are groups of columns arranged in levels.</span><span class="sxs-lookup"><span data-stu-id="2d649-105">Hierarchies are groups of columns arranged in levels.</span></span> <span data-ttu-id="2d649-106">For example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span><span class="sxs-lookup"><span data-stu-id="2d649-106">For example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="2d649-107">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span><span class="sxs-lookup"><span data-stu-id="2d649-107">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="2d649-108">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="2d649-108">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="2d649-109">To create hierarchies, use the model designer in *Diagram View*.</span><span class="sxs-lookup"><span data-stu-id="2d649-109">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="2d649-110">Creating and managing hierarchies is not supported in Data View.</span><span class="sxs-lookup"><span data-stu-id="2d649-110">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="2d649-111">Estimated time to complete this lesson: **20 minutes**</span><span class="sxs-lookup"><span data-stu-id="2d649-111">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2d649-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d649-112">Prerequisites</span></span>  
<span data-ttu-id="2d649-113">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="2d649-113">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="2d649-114">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="2d649-114">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="2d649-115">Create hierarchies</span><span class="sxs-lookup"><span data-stu-id="2d649-115">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="2d649-116">To create a Category hierarchy in the DimProduct table</span><span class="sxs-lookup"><span data-stu-id="2d649-116">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="2d649-117">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span><span class="sxs-lookup"><span data-stu-id="2d649-117">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="2d649-118">A new hierarchy appears at the bottom of the table window.</span><span class="sxs-lookup"><span data-stu-id="2d649-118">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="2d649-119">Rename the hierarchy **Category**.</span><span class="sxs-lookup"><span data-stu-id="2d649-119">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="2d649-120">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span><span class="sxs-lookup"><span data-stu-id="2d649-120">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="2d649-121">In the **Category** hierarchy, right-click **ProductCategoryName** > **Rename**, and then type **Category**.</span><span class="sxs-lookup"><span data-stu-id="2d649-121">In the **Category** hierarchy, right-click **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="2d649-122">Renaming a column in a hierarchy does not rename that column in the table.</span><span class="sxs-lookup"><span data-stu-id="2d649-122">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="2d649-123">A column in a hierarchy is just a representation of the column in the table.</span><span class="sxs-lookup"><span data-stu-id="2d649-123">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="2d649-124">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span><span class="sxs-lookup"><span data-stu-id="2d649-124">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="2d649-125">Rename it **Subcategory**.</span><span class="sxs-lookup"><span data-stu-id="2d649-125">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="2d649-126">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span><span class="sxs-lookup"><span data-stu-id="2d649-126">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="2d649-127">Rename it **Model**.</span><span class="sxs-lookup"><span data-stu-id="2d649-127">Rename it **Model**.</span></span>

6.  <span data-ttu-id="2d649-128">Finally, add **EnglishProductName** to the Category hierarchy.</span><span class="sxs-lookup"><span data-stu-id="2d649-128">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="2d649-129">Rename it **Product**.</span><span class="sxs-lookup"><span data-stu-id="2d649-129">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="2d649-131">To create hierarchies in the DimDate table</span><span class="sxs-lookup"><span data-stu-id="2d649-131">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="2d649-132">In the **DimDate** table, create a hierarchy named **Calendar**.</span><span class="sxs-lookup"><span data-stu-id="2d649-132">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="2d649-133">Add the following columns in-order:</span><span class="sxs-lookup"><span data-stu-id="2d649-133">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="2d649-134">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="2d649-134">CalendarYear</span></span>
    *  <span data-ttu-id="2d649-135">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="2d649-135">CalendarSemester</span></span>
    *  <span data-ttu-id="2d649-136">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="2d649-136">CalendarQuarter</span></span>
    *  <span data-ttu-id="2d649-137">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="2d649-137">MonthCalendar</span></span>
    *  <span data-ttu-id="2d649-138">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="2d649-138">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="2d649-139">In the **DimDate** table, create a **Fiscal** hierarchy.</span><span class="sxs-lookup"><span data-stu-id="2d649-139">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="2d649-140">Include the following columns in-order:</span><span class="sxs-lookup"><span data-stu-id="2d649-140">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="2d649-141">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="2d649-141">FiscalYear</span></span>
    *  <span data-ttu-id="2d649-142">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="2d649-142">FiscalSemester</span></span>
    *  <span data-ttu-id="2d649-143">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="2d649-143">FiscalQuarter</span></span>
    *  <span data-ttu-id="2d649-144">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="2d649-144">MonthCalendar</span></span>
    *  <span data-ttu-id="2d649-145">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="2d649-145">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="2d649-146">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span><span class="sxs-lookup"><span data-stu-id="2d649-146">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="2d649-147">Include the following columns in-order:</span><span class="sxs-lookup"><span data-stu-id="2d649-147">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="2d649-148">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="2d649-148">CalendarYear</span></span>
    *  <span data-ttu-id="2d649-149">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="2d649-149">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="2d649-150">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="2d649-150">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="2d649-151">What's next?</span><span class="sxs-lookup"><span data-stu-id="2d649-151">What's next?</span></span>
<span data-ttu-id="2d649-152">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="2d649-152">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
