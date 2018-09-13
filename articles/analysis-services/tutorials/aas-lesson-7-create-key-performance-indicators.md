---
title: 'Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs'
description: Describes how to create Key Performance Indicators in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 1f7d54129ef9f85bb4141d26b9be8d4a0652bff8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857722"
---
# <a name="create-key-performance-indicators"></a><span data-ttu-id="4d808-103">Create Key Performance Indicators</span><span class="sxs-lookup"><span data-stu-id="4d808-103">Create Key Performance Indicators</span></span>

<span data-ttu-id="4d808-104">In this lesson, you create Key Performance Indicators (KPIs).</span><span class="sxs-lookup"><span data-stu-id="4d808-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="4d808-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span><span class="sxs-lookup"><span data-stu-id="4d808-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="4d808-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span><span class="sxs-lookup"><span data-stu-id="4d808-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="4d808-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="4d808-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="4d808-108">Estimated time to complete this lesson: **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="4d808-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4d808-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4d808-109">Prerequisites</span></span>  
<span data-ttu-id="4d808-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="4d808-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="4d808-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="4d808-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="4d808-112">Create Key Performance Indicators</span><span class="sxs-lookup"><span data-stu-id="4d808-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="4d808-113">To create an InternetCurrentQuarterSalesPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="4d808-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="4d808-114">In the model designer, click the **FactInternetSales** table.</span><span class="sxs-lookup"><span data-stu-id="4d808-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="4d808-115">In the measure grid, click an empty cell.</span><span class="sxs-lookup"><span data-stu-id="4d808-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="4d808-116">In the formula bar, above the table, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="4d808-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="4d808-117">This measure serves as the Base measure for the KPI.</span><span class="sxs-lookup"><span data-stu-id="4d808-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="4d808-118">In the measure grid, right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span><span class="sxs-lookup"><span data-stu-id="4d808-118">In the measure grid, right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="4d808-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span><span class="sxs-lookup"><span data-stu-id="4d808-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="4d808-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span><span class="sxs-lookup"><span data-stu-id="4d808-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="4d808-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span><span class="sxs-lookup"><span data-stu-id="4d808-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="4d808-123">Notice the expandable **Descriptions** label below the available icon styles.</span><span class="sxs-lookup"><span data-stu-id="4d808-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="4d808-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span><span class="sxs-lookup"><span data-stu-id="4d808-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="4d808-125">Click **OK** to complete the KPI.</span><span class="sxs-lookup"><span data-stu-id="4d808-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="4d808-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span><span class="sxs-lookup"><span data-stu-id="4d808-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="4d808-127">This icon indicates that this measure serves as a Base value for a KPI.</span><span class="sxs-lookup"><span data-stu-id="4d808-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="4d808-128">To create an InternetCurrentQuarterMarginPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="4d808-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="4d808-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span><span class="sxs-lookup"><span data-stu-id="4d808-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="4d808-130">In the formula bar, above the table, type the following formula:</span><span class="sxs-lookup"><span data-stu-id="4d808-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="4d808-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span><span class="sxs-lookup"><span data-stu-id="4d808-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="4d808-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span><span class="sxs-lookup"><span data-stu-id="4d808-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="4d808-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span><span class="sxs-lookup"><span data-stu-id="4d808-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="4d808-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d808-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="4d808-135">What's next?</span><span class="sxs-lookup"><span data-stu-id="4d808-135">What's next?</span></span>
<span data-ttu-id="4d808-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="4d808-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
