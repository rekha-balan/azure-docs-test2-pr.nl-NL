---
title: Deploy models in production - Azure Machine Learning | Microsoft Docs
description: How to deploy models to production enabling them to play an active role in making business decisions.
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
ms.date: 11/30/2017
ms.author: deguhath
ms.openlocfilehash: 0505d58261ec32015f8847b710791249f87f049b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966328"
---
# <a name="deploy-models-in-production"></a><span data-ttu-id="3d1f0-103">Deploy models in production</span><span class="sxs-lookup"><span data-stu-id="3d1f0-103">Deploy models in production</span></span>

<span data-ttu-id="3d1f0-104">Production deployment enables a model to play an active role in a business.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-104">Production deployment enables a model to play an active role in a business.</span></span> <span data-ttu-id="3d1f0-105">Predictions from a deployed model can be used for business decisions.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-105">Predictions from a deployed model can be used for business decisions.</span></span>

## <a name="production-platforms"></a><span data-ttu-id="3d1f0-106">Production platforms</span><span class="sxs-lookup"><span data-stu-id="3d1f0-106">Production platforms</span></span>
<span data-ttu-id="3d1f0-107">There are various approaches and platforms to put models into production.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-107">There are various approaches and platforms to put models into production.</span></span> <span data-ttu-id="3d1f0-108">Here are a few options:</span><span class="sxs-lookup"><span data-stu-id="3d1f0-108">Here are a few options:</span></span>


- [<span data-ttu-id="3d1f0-109">Model deployment in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3d1f0-109">Model deployment in Azure Machine Learning</span></span>](../desktop-workbench/model-management-overview.md)
- [<span data-ttu-id="3d1f0-110">Deployment of a model in SQL-server</span><span class="sxs-lookup"><span data-stu-id="3d1f0-110">Deployment of a model in SQL-server</span></span>](https://docs.microsoft.com/sql/advanced-analytics/tutorials/sqldev-py6-operationalize-the-model)
- [<span data-ttu-id="3d1f0-111">Microsoft Machine Learning Server</span><span class="sxs-lookup"><span data-stu-id="3d1f0-111">Microsoft Machine Learning Server</span></span>](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone)


>[!NOTE]
><span data-ttu-id="3d1f0-112">Prior to deployment, one has to insure the latency of model scoring is low enough to use in production.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-112">Prior to deployment, one has to insure the latency of model scoring is low enough to use in production.</span></span>
>


>[!NOTE]
><span data-ttu-id="3d1f0-113">For deployment using Azure Machine Learning Studio, see [Deploy an Azure Machine Learning web service](../studio/publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="3d1f0-113">For deployment using Azure Machine Learning Studio, see [Deploy an Azure Machine Learning web service](../studio/publish-a-machine-learning-web-service.md).</span></span>
>

## <a name="ab-testing"></a><span data-ttu-id="3d1f0-114">A/B testing</span><span class="sxs-lookup"><span data-stu-id="3d1f0-114">A/B testing</span></span>
<span data-ttu-id="3d1f0-115">When multiple models are in production, it can be useful to perform [A/B testing](https://en.wikipedia.org/wiki/A/B_testing) to compare performance of the models.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-115">When multiple models are in production, it can be useful to perform [A/B testing](https://en.wikipedia.org/wiki/A/B_testing) to compare performance of the models.</span></span> 

 
## <a name="next-steps"></a><span data-ttu-id="3d1f0-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d1f0-116">Next steps</span></span>

<span data-ttu-id="3d1f0-117">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-117">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span></span> <span data-ttu-id="3d1f0-118">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-118">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span></span> <span data-ttu-id="3d1f0-119">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="3d1f0-119">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span></span> 
 


