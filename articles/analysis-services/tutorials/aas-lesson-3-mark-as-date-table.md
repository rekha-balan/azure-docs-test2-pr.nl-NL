---
title: 'Azure Analysis Services tutorial lesson 3: Mark as Date Table | Microsoft Docs'
description: Describes how to mark a date table in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 6627cf74154e66a84f34d5d5bc1d78ed3e0c38a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857567"
---
# <a name="mark-as-date-table"></a><span data-ttu-id="d3d51-103">Mark as Date Table</span><span class="sxs-lookup"><span data-stu-id="d3d51-103">Mark as Date Table</span></span>

<span data-ttu-id="d3d51-104">In Lesson 2: Get data, you imported a dimension table named DimDate.</span><span class="sxs-lookup"><span data-stu-id="d3d51-104">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="d3d51-105">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span><span class="sxs-lookup"><span data-stu-id="d3d51-105">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="d3d51-106">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span><span class="sxs-lookup"><span data-stu-id="d3d51-106">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="d3d51-107">In this lesson, you mark the DimDate table as the *Date table* and the Date column (in the Date table) as the *Date column* (unique identifier).</span><span class="sxs-lookup"><span data-stu-id="d3d51-107">In this lesson, you mark the DimDate table as the *Date table* and the Date column (in the Date table) as the *Date column* (unique identifier).</span></span>  

<span data-ttu-id="d3d51-108">Before you mark the date table and date column, it's a good time to do a little housekeeping to make your model easier to understand.</span><span class="sxs-lookup"><span data-stu-id="d3d51-108">Before you mark the date table and date column, it's a good time to do a little housekeeping to make your model easier to understand.</span></span> <span data-ttu-id="d3d51-109">Notice in the DimDate table a column named **FullDateAlternateKey**.</span><span class="sxs-lookup"><span data-stu-id="d3d51-109">Notice in the DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="d3d51-110">This column contains one row for every day in each calendar year included in the table.</span><span class="sxs-lookup"><span data-stu-id="d3d51-110">This column contains one row for every day in each calendar year included in the table.</span></span> <span data-ttu-id="d3d51-111">You use this column a lot in measure formulas and in reports.</span><span class="sxs-lookup"><span data-stu-id="d3d51-111">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="d3d51-112">But, FullDateAlternateKey isn't really a good identifier for this column.</span><span class="sxs-lookup"><span data-stu-id="d3d51-112">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="d3d51-113">You rename it to **Date**, making it easier to identify and include in formulas.</span><span class="sxs-lookup"><span data-stu-id="d3d51-113">You rename it to **Date**, making it easier to identify and include in formulas.</span></span> <span data-ttu-id="d3d51-114">Whenever possible, it's a good idea to rename objects like tables and columns to make them easier to identify in SSDT and client reporting applications like Power BI and Excel.</span><span class="sxs-lookup"><span data-stu-id="d3d51-114">Whenever possible, it's a good idea to rename objects like tables and columns to make them easier to identify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="d3d51-115">Estimated time to complete this lesson: **Three minutes**</span><span class="sxs-lookup"><span data-stu-id="d3d51-115">Estimated time to complete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d3d51-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3d51-116">Prerequisites</span></span>  
<span data-ttu-id="d3d51-117">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="d3d51-117">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d3d51-118">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span><span class="sxs-lookup"><span data-stu-id="d3d51-118">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="to-rename-the-fulldatealternatekey-column"></a><span data-ttu-id="d3d51-119">To rename the FullDateAlternateKey column</span><span class="sxs-lookup"><span data-stu-id="d3d51-119">To rename the FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="d3d51-120">In the model designer, click the **DimDate** table.</span><span class="sxs-lookup"><span data-stu-id="d3d51-120">In the model designer, click the **DimDate** table.</span></span>

2.  <span data-ttu-id="d3d51-121">Double-click the header for the **FullDateAlternateKey** column, and then rename it to **Date**.</span><span class="sxs-lookup"><span data-stu-id="d3d51-121">Double-click the header for the **FullDateAlternateKey** column, and then rename it to **Date**.</span></span>

  
### <a name="to-set-mark-as-date-table"></a><span data-ttu-id="d3d51-122">To set Mark as Date Table</span><span class="sxs-lookup"><span data-stu-id="d3d51-122">To set Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="d3d51-123">Select the **Date** column, and then in the **Properties** window, under **Data Type**, make sure  **Date** is selected.</span><span class="sxs-lookup"><span data-stu-id="d3d51-123">Select the **Date** column, and then in the **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="d3d51-124">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span><span class="sxs-lookup"><span data-stu-id="d3d51-124">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="d3d51-125">In the **Mark as Date Table** dialog box, in the **Date** listbox, select the **Date** column as the unique identifier.</span><span class="sxs-lookup"><span data-stu-id="d3d51-125">In the **Mark as Date Table** dialog box, in the **Date** listbox, select the **Date** column as the unique identifier.</span></span> <span data-ttu-id="d3d51-126">It's usually selected by default.</span><span class="sxs-lookup"><span data-stu-id="d3d51-126">It's usually selected by default.</span></span> <span data-ttu-id="d3d51-127">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3d51-127">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="d3d51-129">What's next?</span><span class="sxs-lookup"><span data-stu-id="d3d51-129">What's next?</span></span>
<span data-ttu-id="d3d51-130">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="d3d51-130">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
