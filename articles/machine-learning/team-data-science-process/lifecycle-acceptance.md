---
title: Customer acceptance stage of the Team Data Science Process lifecycle - Azure | Microsoft Docs
description: The goals, tasks, and deliverables for the customer acceptance stage of your data-science projects
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: 82819ab59d9bab6f256cd01a376f62ac8dac26b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969430"
---
# <a name="customer-acceptance"></a><span data-ttu-id="62c03-103">Customer acceptance</span><span class="sxs-lookup"><span data-stu-id="62c03-103">Customer acceptance</span></span>

<span data-ttu-id="62c03-104">This article outlines the goals, tasks, and deliverables associated with the customer acceptance stage of the Team Data Science Process (TDSP).</span><span class="sxs-lookup"><span data-stu-id="62c03-104">This article outlines the goals, tasks, and deliverables associated with the customer acceptance stage of the Team Data Science Process (TDSP).</span></span> <span data-ttu-id="62c03-105">This process provides a recommended lifecycle that you can use to structure your data-science projects.</span><span class="sxs-lookup"><span data-stu-id="62c03-105">This process provides a recommended lifecycle that you can use to structure your data-science projects.</span></span> <span data-ttu-id="62c03-106">The lifecycle outlines the major stages that projects typically execute, often iteratively:</span><span class="sxs-lookup"><span data-stu-id="62c03-106">The lifecycle outlines the major stages that projects typically execute, often iteratively:</span></span>

   1. <span data-ttu-id="62c03-107">**Business understanding**</span><span class="sxs-lookup"><span data-stu-id="62c03-107">**Business understanding**</span></span>
   2. <span data-ttu-id="62c03-108">**Data acquisition and understanding**</span><span class="sxs-lookup"><span data-stu-id="62c03-108">**Data acquisition and understanding**</span></span>
   3. <span data-ttu-id="62c03-109">**Modeling**</span><span class="sxs-lookup"><span data-stu-id="62c03-109">**Modeling**</span></span>
   4. <span data-ttu-id="62c03-110">**Deployment**</span><span class="sxs-lookup"><span data-stu-id="62c03-110">**Deployment**</span></span>
   5. <span data-ttu-id="62c03-111">**Customer acceptance**</span><span class="sxs-lookup"><span data-stu-id="62c03-111">**Customer acceptance**</span></span>

<span data-ttu-id="62c03-112">Here is a visual representation of the TDSP lifecycle:</span><span class="sxs-lookup"><span data-stu-id="62c03-112">Here is a visual representation of the TDSP lifecycle:</span></span> 

![TDSP lifecycle](./media/lifecycle/tdsp-lifecycle2.png) 


## <a name="goal"></a><span data-ttu-id="62c03-114">Goal</span><span class="sxs-lookup"><span data-stu-id="62c03-114">Goal</span></span>
<span data-ttu-id="62c03-115">**Finalize the project deliverables**: Confirm that the pipeline, the model, and their deployment in a production environment satisfy the customer's objectives.</span><span class="sxs-lookup"><span data-stu-id="62c03-115">**Finalize the project deliverables**: Confirm that the pipeline, the model, and their deployment in a production environment satisfy the customer's objectives.</span></span>

## <a name="how-to-do-it"></a><span data-ttu-id="62c03-116">How to do it</span><span class="sxs-lookup"><span data-stu-id="62c03-116">How to do it</span></span>
<span data-ttu-id="62c03-117">There are two main tasks addressed in this stage:</span><span class="sxs-lookup"><span data-stu-id="62c03-117">There are two main tasks addressed in this stage:</span></span>

   * <span data-ttu-id="62c03-118">**System validation**: Confirm that the deployed model and pipeline meet the customer's needs.</span><span class="sxs-lookup"><span data-stu-id="62c03-118">**System validation**: Confirm that the deployed model and pipeline meet the customer's needs.</span></span>
   * <span data-ttu-id="62c03-119">**Project hand-off**: Hand the project off to the entity that's going to run the system in production.</span><span class="sxs-lookup"><span data-stu-id="62c03-119">**Project hand-off**: Hand the project off to the entity that's going to run the system in production.</span></span>

<span data-ttu-id="62c03-120">The customer should validate that the system meets their business needs and that it answers the questions with acceptable accuracy to deploy the system to production for use by their client's application.</span><span class="sxs-lookup"><span data-stu-id="62c03-120">The customer should validate that the system meets their business needs and that it answers the questions with acceptable accuracy to deploy the system to production for use by their client's application.</span></span> <span data-ttu-id="62c03-121">All the documentation is finalized and reviewed.</span><span class="sxs-lookup"><span data-stu-id="62c03-121">All the documentation is finalized and reviewed.</span></span> <span data-ttu-id="62c03-122">The project is handed-off to the entity responsible for operations.</span><span class="sxs-lookup"><span data-stu-id="62c03-122">The project is handed-off to the entity responsible for operations.</span></span> <span data-ttu-id="62c03-123">This entity might be, for example, an IT or customer data-science team or an agent of the customer that's responsible for running the system in production.</span><span class="sxs-lookup"><span data-stu-id="62c03-123">This entity might be, for example, an IT or customer data-science team or an agent of the customer that's responsible for running the system in production.</span></span> 

## <a name="artifacts"></a><span data-ttu-id="62c03-124">Artifacts</span><span class="sxs-lookup"><span data-stu-id="62c03-124">Artifacts</span></span>
<span data-ttu-id="62c03-125">The main artifact produced in this final stage is the **Exit report of the project for the customer**.</span><span class="sxs-lookup"><span data-stu-id="62c03-125">The main artifact produced in this final stage is the **Exit report of the project for the customer**.</span></span> <span data-ttu-id="62c03-126">This technical report contains all the details of the project that are useful for learning about how to operate the system.</span><span class="sxs-lookup"><span data-stu-id="62c03-126">This technical report contains all the details of the project that are useful for learning about how to operate the system.</span></span> <span data-ttu-id="62c03-127">TDSP provides an [Exit report](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) template.</span><span class="sxs-lookup"><span data-stu-id="62c03-127">TDSP provides an [Exit report](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) template.</span></span> <span data-ttu-id="62c03-128">You can use the template as is, or you can customize it for specific client needs.</span><span class="sxs-lookup"><span data-stu-id="62c03-128">You can use the template as is, or you can customize it for specific client needs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="62c03-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="62c03-129">Next steps</span></span>

<span data-ttu-id="62c03-130">Here are links to each step in the lifecycle of the TDSP:</span><span class="sxs-lookup"><span data-stu-id="62c03-130">Here are links to each step in the lifecycle of the TDSP:</span></span>

   1. [<span data-ttu-id="62c03-131">Business understanding</span><span class="sxs-lookup"><span data-stu-id="62c03-131">Business understanding</span></span>](lifecycle-business-understanding.md)
   2. [<span data-ttu-id="62c03-132">Data acquisition and understanding</span><span class="sxs-lookup"><span data-stu-id="62c03-132">Data acquisition and understanding</span></span>](lifecycle-data.md)
   3. [<span data-ttu-id="62c03-133">Modeling</span><span class="sxs-lookup"><span data-stu-id="62c03-133">Modeling</span></span>](lifecycle-modeling.md)
   4. [<span data-ttu-id="62c03-134">Deployment</span><span class="sxs-lookup"><span data-stu-id="62c03-134">Deployment</span></span>](lifecycle-deployment.md)
   5. [<span data-ttu-id="62c03-135">Customer acceptance</span><span class="sxs-lookup"><span data-stu-id="62c03-135">Customer acceptance</span></span>](lifecycle-acceptance.md)

<span data-ttu-id="62c03-136">We provide full end-to-end walkthroughs that demonstrate all the steps in the process for specific scenarios.</span><span class="sxs-lookup"><span data-stu-id="62c03-136">We provide full end-to-end walkthroughs that demonstrate all the steps in the process for specific scenarios.</span></span> <span data-ttu-id="62c03-137">The [Example walkthroughs](walkthroughs.md) article provides a list of the scenarios with links and thumbnail descriptions.</span><span class="sxs-lookup"><span data-stu-id="62c03-137">The [Example walkthroughs](walkthroughs.md) article provides a list of the scenarios with links and thumbnail descriptions.</span></span> <span data-ttu-id="62c03-138">The walkthroughs illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="62c03-138">The walkthroughs illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span></span> 

<span data-ttu-id="62c03-139">For examples of how to execute steps in TDSPs that use Azure Machine Learning Studio, see [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="62c03-139">For examples of how to execute steps in TDSPs that use Azure Machine Learning Studio, see [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess).</span></span>
