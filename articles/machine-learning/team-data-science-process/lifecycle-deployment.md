---
title: Deployment stage of the Team Data Science Process lifecycle - Azure | Microsoft Docs
description: The goals, tasks, and deliverables for the deployment stage of your data-science projects
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
ms.openlocfilehash: 9c54e93eca181331117f2f7faad3e7d07274412d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966561"
---
# <a name="deployment"></a><span data-ttu-id="76b74-103">Deployment</span><span class="sxs-lookup"><span data-stu-id="76b74-103">Deployment</span></span>

<span data-ttu-id="76b74-104">This article outlines the goals, tasks, and deliverables associated with the deployment of the Team Data Science Process (TDSP).</span><span class="sxs-lookup"><span data-stu-id="76b74-104">This article outlines the goals, tasks, and deliverables associated with the deployment of the Team Data Science Process (TDSP).</span></span> <span data-ttu-id="76b74-105">This process provides a recommended lifecycle that you can use to structure your data-science projects.</span><span class="sxs-lookup"><span data-stu-id="76b74-105">This process provides a recommended lifecycle that you can use to structure your data-science projects.</span></span> <span data-ttu-id="76b74-106">The lifecycle outlines the major stages that projects typically execute, often iteratively:</span><span class="sxs-lookup"><span data-stu-id="76b74-106">The lifecycle outlines the major stages that projects typically execute, often iteratively:</span></span>

   1. <span data-ttu-id="76b74-107">**Business understanding**</span><span class="sxs-lookup"><span data-stu-id="76b74-107">**Business understanding**</span></span>
   2. <span data-ttu-id="76b74-108">**Data acquisition and understanding**</span><span class="sxs-lookup"><span data-stu-id="76b74-108">**Data acquisition and understanding**</span></span>
   3. <span data-ttu-id="76b74-109">**Modeling**</span><span class="sxs-lookup"><span data-stu-id="76b74-109">**Modeling**</span></span>
   4. <span data-ttu-id="76b74-110">**Deployment**</span><span class="sxs-lookup"><span data-stu-id="76b74-110">**Deployment**</span></span>
   5. <span data-ttu-id="76b74-111">**Customer acceptance**</span><span class="sxs-lookup"><span data-stu-id="76b74-111">**Customer acceptance**</span></span>

<span data-ttu-id="76b74-112">Here is a visual representation of the TDSP lifecycle:</span><span class="sxs-lookup"><span data-stu-id="76b74-112">Here is a visual representation of the TDSP lifecycle:</span></span> 

![TDSP lifecycle](./media/lifecycle/tdsp-lifecycle2.png) 


## <a name="goal"></a><span data-ttu-id="76b74-114">Goal</span><span class="sxs-lookup"><span data-stu-id="76b74-114">Goal</span></span>
<span data-ttu-id="76b74-115">Deploy models with a data pipeline to a production or production-like environment for final user acceptance.</span><span class="sxs-lookup"><span data-stu-id="76b74-115">Deploy models with a data pipeline to a production or production-like environment for final user acceptance.</span></span> 

## <a name="how-to-do-it"></a><span data-ttu-id="76b74-116">How to do it</span><span class="sxs-lookup"><span data-stu-id="76b74-116">How to do it</span></span>
<span data-ttu-id="76b74-117">The main task addressed in this stage:</span><span class="sxs-lookup"><span data-stu-id="76b74-117">The main task addressed in this stage:</span></span>

<span data-ttu-id="76b74-118">**Operationalize the model**: Deploy the model and pipeline to a production or production-like environment for application consumption.</span><span class="sxs-lookup"><span data-stu-id="76b74-118">**Operationalize the model**: Deploy the model and pipeline to a production or production-like environment for application consumption.</span></span>

### <a name="operationalize-a-model"></a><span data-ttu-id="76b74-119">Operationalize a model</span><span class="sxs-lookup"><span data-stu-id="76b74-119">Operationalize a model</span></span>
<span data-ttu-id="76b74-120">After you have a set of models that perform well, you can operationalize them for other applications to consume.</span><span class="sxs-lookup"><span data-stu-id="76b74-120">After you have a set of models that perform well, you can operationalize them for other applications to consume.</span></span> <span data-ttu-id="76b74-121">Depending on the business requirements, predictions are made either in real time or on a batch basis.</span><span class="sxs-lookup"><span data-stu-id="76b74-121">Depending on the business requirements, predictions are made either in real time or on a batch basis.</span></span> <span data-ttu-id="76b74-122">To deploy models, you expose them with an open API interface.</span><span class="sxs-lookup"><span data-stu-id="76b74-122">To deploy models, you expose them with an open API interface.</span></span> <span data-ttu-id="76b74-123">The interface enables the model to be easily consumed from various applications, such as:</span><span class="sxs-lookup"><span data-stu-id="76b74-123">The interface enables the model to be easily consumed from various applications, such as:</span></span>

   * <span data-ttu-id="76b74-124">Online websites</span><span class="sxs-lookup"><span data-stu-id="76b74-124">Online websites</span></span>
   * <span data-ttu-id="76b74-125">Spreadsheets</span><span class="sxs-lookup"><span data-stu-id="76b74-125">Spreadsheets</span></span> 
   * <span data-ttu-id="76b74-126">Dashboards</span><span class="sxs-lookup"><span data-stu-id="76b74-126">Dashboards</span></span>
   * <span data-ttu-id="76b74-127">Line-of-business applications</span><span class="sxs-lookup"><span data-stu-id="76b74-127">Line-of-business applications</span></span> 
   * <span data-ttu-id="76b74-128">Back-end applications</span><span class="sxs-lookup"><span data-stu-id="76b74-128">Back-end applications</span></span> 

<span data-ttu-id="76b74-129">For examples of model operationalization with an Azure Machine Learning web service, see [Deploy an Azure Machine Learning web service](../studio/publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="76b74-129">For examples of model operationalization with an Azure Machine Learning web service, see [Deploy an Azure Machine Learning web service](../studio/publish-a-machine-learning-web-service.md).</span></span> <span data-ttu-id="76b74-130">It is a best practice to build telemetry and monitoring into the production model and the data pipeline that you deploy.</span><span class="sxs-lookup"><span data-stu-id="76b74-130">It is a best practice to build telemetry and monitoring into the production model and the data pipeline that you deploy.</span></span> <span data-ttu-id="76b74-131">This practice helps with subsequent system status reporting and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="76b74-131">This practice helps with subsequent system status reporting and troubleshooting.</span></span>  

## <a name="artifacts"></a><span data-ttu-id="76b74-132">Artifacts</span><span class="sxs-lookup"><span data-stu-id="76b74-132">Artifacts</span></span>

* <span data-ttu-id="76b74-133">A status dashboard that displays the system health and key metrics</span><span class="sxs-lookup"><span data-stu-id="76b74-133">A status dashboard that displays the system health and key metrics</span></span>
* <span data-ttu-id="76b74-134">A final modeling report with deployment details</span><span class="sxs-lookup"><span data-stu-id="76b74-134">A final modeling report with deployment details</span></span>
* <span data-ttu-id="76b74-135">A final solution architecture document</span><span class="sxs-lookup"><span data-stu-id="76b74-135">A final solution architecture document</span></span>


## <a name="next-steps"></a><span data-ttu-id="76b74-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="76b74-136">Next steps</span></span>

<span data-ttu-id="76b74-137">Here are links to each step in the lifecycle of the TDSP:</span><span class="sxs-lookup"><span data-stu-id="76b74-137">Here are links to each step in the lifecycle of the TDSP:</span></span>

   1. [<span data-ttu-id="76b74-138">Business understanding</span><span class="sxs-lookup"><span data-stu-id="76b74-138">Business understanding</span></span>](lifecycle-business-understanding.md)
   2. [<span data-ttu-id="76b74-139">Data Acquisition and understanding</span><span class="sxs-lookup"><span data-stu-id="76b74-139">Data Acquisition and understanding</span></span>](lifecycle-data.md)
   3. [<span data-ttu-id="76b74-140">Modeling</span><span class="sxs-lookup"><span data-stu-id="76b74-140">Modeling</span></span>](lifecycle-modeling.md)
   4. [<span data-ttu-id="76b74-141">Deployment</span><span class="sxs-lookup"><span data-stu-id="76b74-141">Deployment</span></span>](lifecycle-deployment.md)
   5. [<span data-ttu-id="76b74-142">Customer acceptance</span><span class="sxs-lookup"><span data-stu-id="76b74-142">Customer acceptance</span></span>](lifecycle-acceptance.md)

<span data-ttu-id="76b74-143">We provide full end-to-end walkthroughs that demonstrate all the steps in the process for specific scenarios.</span><span class="sxs-lookup"><span data-stu-id="76b74-143">We provide full end-to-end walkthroughs that demonstrate all the steps in the process for specific scenarios.</span></span> <span data-ttu-id="76b74-144">The [Example walkthroughs](walkthroughs.md) article provides a list of the scenarios with links and thumbnail descriptions.</span><span class="sxs-lookup"><span data-stu-id="76b74-144">The [Example walkthroughs](walkthroughs.md) article provides a list of the scenarios with links and thumbnail descriptions.</span></span> <span data-ttu-id="76b74-145">The walkthroughs illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="76b74-145">The walkthroughs illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span></span> 

<span data-ttu-id="76b74-146">For examples of how to execute steps in TDSPs that use Azure Machine Learning Studio, see [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="76b74-146">For examples of how to execute steps in TDSPs that use Azure Machine Learning Studio, see [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess).</span></span>
