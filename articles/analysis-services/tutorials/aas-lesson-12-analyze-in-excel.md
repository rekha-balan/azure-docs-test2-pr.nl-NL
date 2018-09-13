---
title: 'Azure Analysis Services tutorial lesson 12: Analyze in Excel | Microsoft Docs'
description: Describes how to use Analyze in Excel in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 1e487f6778c45e554f95489e62ac2dedd01ee3f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857524"
---
# <a name="analyze-in-excel"></a><span data-ttu-id="ee378-103">Analyze in Excel</span><span class="sxs-lookup"><span data-stu-id="ee378-103">Analyze in Excel</span></span>

<span data-ttu-id="ee378-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span><span class="sxs-lookup"><span data-stu-id="ee378-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span></span> <span data-ttu-id="ee378-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span><span class="sxs-lookup"><span data-stu-id="ee378-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span></span> <span data-ttu-id="ee378-106">You do not perform any data analysis in this lesson.</span><span class="sxs-lookup"><span data-stu-id="ee378-106">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="ee378-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span><span class="sxs-lookup"><span data-stu-id="ee378-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span></span>   
  
<span data-ttu-id="ee378-108">To complete this lesson, Excel must be installed on the same computer as Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee378-108">To complete this lesson, Excel must be installed on the same computer as Visual Studio.</span></span>
  
<span data-ttu-id="ee378-109">Estimated time to complete this lesson: **Five minutes**</span><span class="sxs-lookup"><span data-stu-id="ee378-109">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ee378-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee378-110">Prerequisites</span></span>  
<span data-ttu-id="ee378-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="ee378-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ee378-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ee378-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a><span data-ttu-id="ee378-113">Browse using the Default and Internet Sales perspectives</span><span class="sxs-lookup"><span data-stu-id="ee378-113">Browse using the Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="ee378-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span><span class="sxs-lookup"><span data-stu-id="ee378-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span></span> <span data-ttu-id="ee378-115">The Internet Sales perspective excludes the Customer table object.</span><span class="sxs-lookup"><span data-stu-id="ee378-115">The Internet Sales perspective excludes the Customer table object.</span></span>  
  
#### <a name="to-browse-by-using-the-default-perspective"></a><span data-ttu-id="ee378-116">To browse by using the Default perspective</span><span class="sxs-lookup"><span data-stu-id="ee378-116">To browse by using the Default perspective</span></span>  
  
1.  <span data-ttu-id="ee378-117">Click the **Model** menu > **Analyze in Excel**.</span><span class="sxs-lookup"><span data-stu-id="ee378-117">Click the **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="ee378-118">In the **Analyze in Excel** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee378-118">In the **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="ee378-119">Excel opens with a new workbook.</span><span class="sxs-lookup"><span data-stu-id="ee378-119">Excel opens with a new workbook.</span></span> <span data-ttu-id="ee378-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span><span class="sxs-lookup"><span data-stu-id="ee378-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span></span> <span data-ttu-id="ee378-121">A PivotTable is automatically added to the worksheet.</span><span class="sxs-lookup"><span data-stu-id="ee378-121">A PivotTable is automatically added to the worksheet.</span></span>  
  
3.  <span data-ttu-id="ee378-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span><span class="sxs-lookup"><span data-stu-id="ee378-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="ee378-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span><span class="sxs-lookup"><span data-stu-id="ee378-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="ee378-124">Close Excel without saving the workbook.</span><span class="sxs-lookup"><span data-stu-id="ee378-124">Close Excel without saving the workbook.</span></span>  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a><span data-ttu-id="ee378-125">To browse by using the Internet Sales perspective</span><span class="sxs-lookup"><span data-stu-id="ee378-125">To browse by using the Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="ee378-126">Click the **Model** menu, and then click **Analyze in Excel**.</span><span class="sxs-lookup"><span data-stu-id="ee378-126">Click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="ee378-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee378-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="ee378-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span><span class="sxs-lookup"><span data-stu-id="ee378-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span></span>  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="ee378-131">Close Excel without saving the workbook.</span><span class="sxs-lookup"><span data-stu-id="ee378-131">Close Excel without saving the workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="ee378-132">Browse by using roles</span><span class="sxs-lookup"><span data-stu-id="ee378-132">Browse by using roles</span></span>  
<span data-ttu-id="ee378-133">Roles are an important part of any tabular model.</span><span class="sxs-lookup"><span data-stu-id="ee378-133">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="ee378-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span><span class="sxs-lookup"><span data-stu-id="ee378-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="ee378-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span><span class="sxs-lookup"><span data-stu-id="ee378-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span></span>  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a><span data-ttu-id="ee378-136">To browse by using the Sales Manager user role</span><span class="sxs-lookup"><span data-stu-id="ee378-136">To browse by using the Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="ee378-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span><span class="sxs-lookup"><span data-stu-id="ee378-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="ee378-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee378-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="ee378-139">Excel opens with a new workbook.</span><span class="sxs-lookup"><span data-stu-id="ee378-139">Excel opens with a new workbook.</span></span> <span data-ttu-id="ee378-140">A PivotTable is automatically created.</span><span class="sxs-lookup"><span data-stu-id="ee378-140">A PivotTable is automatically created.</span></span> <span data-ttu-id="ee378-141">The Pivot Table Field List includes all the data fields available in your new model.</span><span class="sxs-lookup"><span data-stu-id="ee378-141">The Pivot Table Field List includes all the data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="ee378-142">Close Excel without saving the workbook.</span><span class="sxs-lookup"><span data-stu-id="ee378-142">Close Excel without saving the workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="ee378-143">What's next?</span><span class="sxs-lookup"><span data-stu-id="ee378-143">What's next?</span></span>
<span data-ttu-id="ee378-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ee378-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
