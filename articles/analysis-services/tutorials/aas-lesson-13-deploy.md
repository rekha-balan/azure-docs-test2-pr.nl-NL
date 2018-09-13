---
title: 'Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs'
description: Describes how to deploy the tutorial project to Azure Analysis Services.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 84cdae1694608814167641417781cd22c12656a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869996"
---
# <a name="deploy"></a><span data-ttu-id="c3df9-103">Deploy</span><span class="sxs-lookup"><span data-stu-id="c3df9-103">Deploy</span></span>

<span data-ttu-id="c3df9-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span><span class="sxs-lookup"><span data-stu-id="c3df9-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span></span> <span data-ttu-id="c3df9-105">You then deploy the model to that instance.</span><span class="sxs-lookup"><span data-stu-id="c3df9-105">You then deploy the model to that instance.</span></span> <span data-ttu-id="c3df9-106">After your model is deployed, users can connect to it by using a reporting client application.</span><span class="sxs-lookup"><span data-stu-id="c3df9-106">After your model is deployed, users can connect to it by using a reporting client application.</span></span> <span data-ttu-id="c3df9-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="c3df9-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="c3df9-108">Estimated time to complete this lesson: **5 minutes**</span><span class="sxs-lookup"><span data-stu-id="c3df9-108">Estimated time to complete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="c3df9-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c3df9-109">Prerequisites</span></span>  
<span data-ttu-id="c3df9-110">This article is part of a tabular modeling tutorial, which should be completed in order.</span><span class="sxs-lookup"><span data-stu-id="c3df9-110">This article is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="c3df9-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="c3df9-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="c3df9-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span><span class="sxs-lookup"><span data-stu-id="c3df9-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="c3df9-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span><span class="sxs-lookup"><span data-stu-id="c3df9-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-the-model"></a><span data-ttu-id="c3df9-114">Deploy the model</span><span class="sxs-lookup"><span data-stu-id="c3df9-114">Deploy the model</span></span>  
  
#### <a name="to-configure-deployment-properties"></a><span data-ttu-id="c3df9-115">To configure deployment properties</span><span class="sxs-lookup"><span data-stu-id="c3df9-115">To configure deployment properties</span></span>  

  
1.  <span data-ttu-id="c3df9-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="c3df9-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="c3df9-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span><span class="sxs-lookup"><span data-stu-id="c3df9-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="c3df9-119">In the **Database** property, type **Adventure Works Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="c3df9-119">In the **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="c3df9-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span><span class="sxs-lookup"><span data-stu-id="c3df9-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="c3df9-121">Verify your selections and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3df9-121">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a><span data-ttu-id="c3df9-122">To deploy the Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="c3df9-122">To deploy the Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="c3df9-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span><span class="sxs-lookup"><span data-stu-id="c3df9-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="c3df9-124">Right-click the **AW Internet Sales** project > **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="c3df9-124">Right-click the **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="c3df9-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span><span class="sxs-lookup"><span data-stu-id="c3df9-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span></span> <span data-ttu-id="c3df9-126">Enter your organizational account and password, for example nancy@adventureworks.com.</span><span class="sxs-lookup"><span data-stu-id="c3df9-126">Enter your organizational account and password, for example nancy@adventureworks.com.</span></span> <span data-ttu-id="c3df9-127">This account must be in Admins on the server.</span><span class="sxs-lookup"><span data-stu-id="c3df9-127">This account must be in Admins on the server.</span></span>
  
    <span data-ttu-id="c3df9-128">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span><span class="sxs-lookup"><span data-stu-id="c3df9-128">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="c3df9-130">When deployment successfully completes, go ahead and click **Close**.</span><span class="sxs-lookup"><span data-stu-id="c3df9-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  

<span data-ttu-id="c3df9-131">This lesson describes the most common and easiest method to deploy a tabular model from SSDT.</span><span class="sxs-lookup"><span data-stu-id="c3df9-131">This lesson describes the most common and easiest method to deploy a tabular model from SSDT.</span></span> <span data-ttu-id="c3df9-132">Advanced deployment options such as the Deployment Wizard or automating with XMLA and AMO provide greater flexibility, consistency, and scheduled deployments.</span><span class="sxs-lookup"><span data-stu-id="c3df9-132">Advanced deployment options such as the Deployment Wizard or automating with XMLA and AMO provide greater flexibility, consistency, and scheduled deployments.</span></span> <span data-ttu-id="c3df9-133">To learn more, see [Tabular model solution deployment](https://docs.microsoft.com/sql/analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="c3df9-133">To learn more, see [Tabular model solution deployment](https://docs.microsoft.com/sql/analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular).</span></span>

## <a name="conclusion"></a><span data-ttu-id="c3df9-134">Conclusion</span><span class="sxs-lookup"><span data-stu-id="c3df9-134">Conclusion</span></span>  
<span data-ttu-id="c3df9-135">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="c3df9-135">Congratulations!</span></span> <span data-ttu-id="c3df9-136">You're finished authoring and deploying your first Analysis Services Tabular model.</span><span class="sxs-lookup"><span data-stu-id="c3df9-136">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="c3df9-137">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span><span class="sxs-lookup"><span data-stu-id="c3df9-137">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span></span> <span data-ttu-id="c3df9-138">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span><span class="sxs-lookup"><span data-stu-id="c3df9-138">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span></span> <span data-ttu-id="c3df9-139">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span><span class="sxs-lookup"><span data-stu-id="c3df9-139">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="c3df9-141">What's next?</span><span class="sxs-lookup"><span data-stu-id="c3df9-141">What's next?</span></span>
<span data-ttu-id="c3df9-142">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="c3df9-142">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="c3df9-143">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="c3df9-143">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="c3df9-144">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="c3df9-144">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="c3df9-145">Supplemental Lesson - Ragged hierarchies</span><span class="sxs-lookup"><span data-stu-id="c3df9-145">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
