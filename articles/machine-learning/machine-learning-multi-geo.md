---
title: Multi-Geo Help documentation | Microsoft Docs
description: Learn how to create a workspace and publish a web service in an Azure region different from the South Central United States (SCUS) Azure region.
services: machine-learning
documentationcenter: ''
author: tedway
manager: jhubbard
editor: rmca14
tags: ''
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: edeff8d59ee0a4bf4b5b34a9b143b14822d04a97
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556549"
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="f562e-103">Multi-Geo Help documentation</span><span class="sxs-lookup"><span data-stu-id="f562e-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="f562e-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span><span class="sxs-lookup"><span data-stu-id="f562e-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="f562e-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span><span class="sxs-lookup"><span data-stu-id="f562e-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="f562e-106">Create a workspace</span><span class="sxs-lookup"><span data-stu-id="f562e-106">Create a workspace</span></span>
1. <span data-ttu-id="f562e-107">Sign in to the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="f562e-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="f562e-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span><span class="sxs-lookup"><span data-stu-id="f562e-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="f562e-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span><span class="sxs-lookup"><span data-stu-id="f562e-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="f562e-110">![Multi-Geo Help image 1][1]</span><span class="sxs-lookup"><span data-stu-id="f562e-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="f562e-111">Select the workspace, and then click **Sign-in to ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="f562e-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="f562e-112">![Multi-Geo Help image 2][2]</span><span class="sxs-lookup"><span data-stu-id="f562e-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="f562e-113">You now have a workspace in another region that you may use just like any other workspace.</span><span class="sxs-lookup"><span data-stu-id="f562e-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="f562e-114">To switch among your workspaces, look to the upper right of your screen.</span><span class="sxs-lookup"><span data-stu-id="f562e-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="f562e-115">Click the dropdown, select the region, and then select the workspace.</span><span class="sxs-lookup"><span data-stu-id="f562e-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="f562e-116">Everything is local to the workspace region.</span><span class="sxs-lookup"><span data-stu-id="f562e-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="f562e-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span><span class="sxs-lookup"><span data-stu-id="f562e-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="f562e-118">![Multi-Geo Help image 3][3]</span><span class="sxs-lookup"><span data-stu-id="f562e-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="f562e-119">Open an experiment from Gallery</span><span class="sxs-lookup"><span data-stu-id="f562e-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="f562e-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span><span class="sxs-lookup"><span data-stu-id="f562e-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Multi-Geo Help image 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="f562e-122">Web service management</span><span class="sxs-lookup"><span data-stu-id="f562e-122">Web service management</span></span>
<span data-ttu-id="f562e-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span><span class="sxs-lookup"><span data-stu-id="f562e-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-to-note"></a><span data-ttu-id="f562e-124">Things to note</span><span class="sxs-lookup"><span data-stu-id="f562e-124">Things to note</span></span>
1. <span data-ttu-id="f562e-125">You can only copy experiments between workspaces that belong to the same region this way.</span><span class="sxs-lookup"><span data-stu-id="f562e-125">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="f562e-126">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span><span class="sxs-lookup"><span data-stu-id="f562e-126">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="f562e-127">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span><span class="sxs-lookup"><span data-stu-id="f562e-127">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="f562e-128">The region selector will only show workspaces for one region at a time.</span><span class="sxs-lookup"><span data-stu-id="f562e-128">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="f562e-129">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span><span class="sxs-lookup"><span data-stu-id="f562e-129">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="f562e-130">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span><span class="sxs-lookup"><span data-stu-id="f562e-130">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="f562e-131">More information</span><span class="sxs-lookup"><span data-stu-id="f562e-131">More information</span></span>
<span data-ttu-id="f562e-132">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="f562e-132">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-multi-geo/multi-geo_1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-multi-geo/multi-geo_2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-multi-geo/multi-geo_3.png
[4a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-multi-geo/multi-geo_4a.png




