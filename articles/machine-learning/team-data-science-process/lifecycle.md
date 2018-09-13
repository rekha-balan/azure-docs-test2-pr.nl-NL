---
title: The Team Data Science Process lifecycle - Azure | Microsoft Docs
description: The steps needed to execute your data-science projects
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: dca71a13db33f44fed551e4791625c5667cfdc21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856603"
---
# <a name="the-team-data-science-process-lifecycle"></a><span data-ttu-id="ae667-103">The Team Data Science Process lifecycle</span><span class="sxs-lookup"><span data-stu-id="ae667-103">The Team Data Science Process lifecycle</span></span>

<span data-ttu-id="ae667-104">The Team Data Science Process (TDSP) provides a recommended lifecycle that you can use to structure your data-science projects.</span><span class="sxs-lookup"><span data-stu-id="ae667-104">The Team Data Science Process (TDSP) provides a recommended lifecycle that you can use to structure your data-science projects.</span></span> <span data-ttu-id="ae667-105">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span><span class="sxs-lookup"><span data-stu-id="ae667-105">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> <span data-ttu-id="ae667-106">If you use another data-science lifecycle, such as the Cross Industry Standard Process for Data Mining [(CRISP-DM)](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), Knowledge Discovery in Databases [(KDD)](https://wikipedia.org/wiki/Data_mining#Process), or your organization's own custom process, you can still use the task-based TDSP.</span><span class="sxs-lookup"><span data-stu-id="ae667-106">If you use another data-science lifecycle, such as the Cross Industry Standard Process for Data Mining [(CRISP-DM)](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), Knowledge Discovery in Databases [(KDD)](https://wikipedia.org/wiki/Data_mining#Process), or your organization's own custom process, you can still use the task-based TDSP.</span></span> 

<span data-ttu-id="ae667-107">This lifecycle is designed for data-science projects that are intended to ship as part of intelligent applications.</span><span class="sxs-lookup"><span data-stu-id="ae667-107">This lifecycle is designed for data-science projects that are intended to ship as part of intelligent applications.</span></span> <span data-ttu-id="ae667-108">These applications deploy machine learning or artificial intelligence models for predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="ae667-108">These applications deploy machine learning or artificial intelligence models for predictive analytics.</span></span> <span data-ttu-id="ae667-109">Exploratory data-science projects and ad hoc analytics projects can also benefit from the use of this process.</span><span class="sxs-lookup"><span data-stu-id="ae667-109">Exploratory data-science projects and ad hoc analytics projects can also benefit from the use of this process.</span></span> <span data-ttu-id="ae667-110">But for those projects, some of the steps described here might not be needed.</span><span class="sxs-lookup"><span data-stu-id="ae667-110">But for those projects, some of the steps described here might not be needed.</span></span> 

<span data-ttu-id="ae667-111">The TDSP lifecycle is composed of five major stages that are executed iteratively.</span><span class="sxs-lookup"><span data-stu-id="ae667-111">The TDSP lifecycle is composed of five major stages that are executed iteratively.</span></span> <span data-ttu-id="ae667-112">These stages include:</span><span class="sxs-lookup"><span data-stu-id="ae667-112">These stages include:</span></span>

   1. [<span data-ttu-id="ae667-113">Business understanding</span><span class="sxs-lookup"><span data-stu-id="ae667-113">Business understanding</span></span>](lifecycle-business-understanding.md)
   2. [<span data-ttu-id="ae667-114">Data acquisition and understanding</span><span class="sxs-lookup"><span data-stu-id="ae667-114">Data acquisition and understanding</span></span>](lifecycle-data.md)
   3. [<span data-ttu-id="ae667-115">Modeling</span><span class="sxs-lookup"><span data-stu-id="ae667-115">Modeling</span></span>](lifecycle-modeling.md)
   4. [<span data-ttu-id="ae667-116">Deployment</span><span class="sxs-lookup"><span data-stu-id="ae667-116">Deployment</span></span>](lifecycle-deployment.md)
   5. [<span data-ttu-id="ae667-117">Customer acceptance</span><span class="sxs-lookup"><span data-stu-id="ae667-117">Customer acceptance</span></span>](lifecycle-acceptance.md)

<span data-ttu-id="ae667-118">Here is a visual representation of the TDSP lifecycle:</span><span class="sxs-lookup"><span data-stu-id="ae667-118">Here is a visual representation of the TDSP lifecycle:</span></span> 

![TDSP lifecycle](./media/lifecycle/tdsp-lifecycle2.png) 


<span data-ttu-id="ae667-120">The TDSP lifecycle is modeled as a sequence of iterated steps that provide guidance on the tasks needed to use predictive models.</span><span class="sxs-lookup"><span data-stu-id="ae667-120">The TDSP lifecycle is modeled as a sequence of iterated steps that provide guidance on the tasks needed to use predictive models.</span></span> <span data-ttu-id="ae667-121">You deploy the predictive models in the production environment that you plan to use to build the intelligent applications.</span><span class="sxs-lookup"><span data-stu-id="ae667-121">You deploy the predictive models in the production environment that you plan to use to build the intelligent applications.</span></span> <span data-ttu-id="ae667-122">The goal of this process lifecycle is to continue to move a data-science project toward a clear engagement end point.</span><span class="sxs-lookup"><span data-stu-id="ae667-122">The goal of this process lifecycle is to continue to move a data-science project toward a clear engagement end point.</span></span> <span data-ttu-id="ae667-123">Data science is an exercise in research and discovery.</span><span class="sxs-lookup"><span data-stu-id="ae667-123">Data science is an exercise in research and discovery.</span></span> <span data-ttu-id="ae667-124">The ability to communicate tasks to your team and your customers by using a well-defined set of artifacts that employ standardized templates helps to avoid misunderstandings.</span><span class="sxs-lookup"><span data-stu-id="ae667-124">The ability to communicate tasks to your team and your customers by using a well-defined set of artifacts that employ standardized templates helps to avoid misunderstandings.</span></span> <span data-ttu-id="ae667-125">Using these templates also increases the chance of the successful completion of a complex data-science project.</span><span class="sxs-lookup"><span data-stu-id="ae667-125">Using these templates also increases the chance of the successful completion of a complex data-science project.</span></span>

<span data-ttu-id="ae667-126">For each stage, we provide the following information:</span><span class="sxs-lookup"><span data-stu-id="ae667-126">For each stage, we provide the following information:</span></span>

   * <span data-ttu-id="ae667-127">**Goals**: The specific objectives.</span><span class="sxs-lookup"><span data-stu-id="ae667-127">**Goals**: The specific objectives.</span></span>
   * <span data-ttu-id="ae667-128">**How to do it**: An outline of the specific tasks and guidance on how to complete them.</span><span class="sxs-lookup"><span data-stu-id="ae667-128">**How to do it**: An outline of the specific tasks and guidance on how to complete them.</span></span>
   * <span data-ttu-id="ae667-129">**Artifacts**: The deliverables and the support to produce them.</span><span class="sxs-lookup"><span data-stu-id="ae667-129">**Artifacts**: The deliverables and the support to produce them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae667-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae667-130">Next steps</span></span>

<span data-ttu-id="ae667-131">We provide full end-to-end walkthroughs that demonstrate all the steps in the process for specific scenarios.</span><span class="sxs-lookup"><span data-stu-id="ae667-131">We provide full end-to-end walkthroughs that demonstrate all the steps in the process for specific scenarios.</span></span> <span data-ttu-id="ae667-132">The [Example walkthroughs](walkthroughs.md) article provides a list of the scenarios with links and thumbnail descriptions.</span><span class="sxs-lookup"><span data-stu-id="ae667-132">The [Example walkthroughs](walkthroughs.md) article provides a list of the scenarios with links and thumbnail descriptions.</span></span> <span data-ttu-id="ae667-133">The walkthroughs illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="ae667-133">The walkthroughs illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span></span> 

<span data-ttu-id="ae667-134">For examples of how to execute steps in TDSPs that use Azure Machine Learning Studio, see [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="ae667-134">For examples of how to execute steps in TDSPs that use Azure Machine Learning Studio, see [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess).</span></span>
