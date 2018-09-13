---
title: Azure Analysis Services tutorial lesson 8 Create perspectives | Microsoft Docs
description: Describes how to create perspectives in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: f72c1048a4bf2cb0a2f42db99bb35cf66563ae0f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967817"
---
# <a name="create-perspectives"></a><span data-ttu-id="213b9-103">Create perspectives</span><span class="sxs-lookup"><span data-stu-id="213b9-103">Create perspectives</span></span>

<span data-ttu-id="213b9-104">In this lesson, you create an Internet Sales perspective.</span><span class="sxs-lookup"><span data-stu-id="213b9-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="213b9-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span><span class="sxs-lookup"><span data-stu-id="213b9-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="213b9-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span><span class="sxs-lookup"><span data-stu-id="213b9-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="213b9-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="213b9-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="213b9-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span><span class="sxs-lookup"><span data-stu-id="213b9-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="213b9-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span><span class="sxs-lookup"><span data-stu-id="213b9-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="213b9-110">However, it is not visible in a reporting client field list.</span><span class="sxs-lookup"><span data-stu-id="213b9-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="213b9-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span><span class="sxs-lookup"><span data-stu-id="213b9-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="213b9-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span><span class="sxs-lookup"><span data-stu-id="213b9-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="213b9-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span><span class="sxs-lookup"><span data-stu-id="213b9-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="213b9-114">Estimated time to complete this lesson: **Five minutes**</span><span class="sxs-lookup"><span data-stu-id="213b9-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="213b9-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="213b9-115">Prerequisites</span></span>  
<span data-ttu-id="213b9-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="213b9-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="213b9-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="213b9-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="213b9-118">Create perspectives</span><span class="sxs-lookup"><span data-stu-id="213b9-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="213b9-119">To create an Internet Sales perspective</span><span class="sxs-lookup"><span data-stu-id="213b9-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="213b9-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span><span class="sxs-lookup"><span data-stu-id="213b9-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="213b9-121">In the **Perspectives** dialog box, click **New Perspective**.</span><span class="sxs-lookup"><span data-stu-id="213b9-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="213b9-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="213b9-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="213b9-123">Select the all the tables *except* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="213b9-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="213b9-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span><span class="sxs-lookup"><span data-stu-id="213b9-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="213b9-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span><span class="sxs-lookup"><span data-stu-id="213b9-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="213b9-127">What's next?</span><span class="sxs-lookup"><span data-stu-id="213b9-127">What's next?</span></span>
<span data-ttu-id="213b9-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="213b9-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
