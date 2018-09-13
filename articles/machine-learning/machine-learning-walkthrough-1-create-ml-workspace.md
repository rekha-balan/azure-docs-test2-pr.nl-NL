---
title: 'Step 1: Create a Machine Learning workspace | Microsoft Docs'
description: 'Step 1 of the Develop a predictive solution walkthrough: Learn how to set up a new Azure Machine Learning Studio workspace.'
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: ae6811202ab453880a24a218fceb50fef81b352e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556516"
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="21f60-103">Walkthrough Step 1: Create a Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="21f60-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="21f60-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="21f60-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="21f60-105">**Create a Machine Learning workspace**</span><span class="sxs-lookup"><span data-stu-id="21f60-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="21f60-106">Upload existing data</span><span class="sxs-lookup"><span data-stu-id="21f60-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="21f60-107">Create a new experiment</span><span class="sxs-lookup"><span data-stu-id="21f60-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="21f60-108">Train and evaluate the models</span><span class="sxs-lookup"><span data-stu-id="21f60-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="21f60-109">Deploy the Web service</span><span class="sxs-lookup"><span data-stu-id="21f60-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="21f60-110">Access the Web service</span><span class="sxs-lookup"><span data-stu-id="21f60-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="21f60-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="21f60-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="21f60-112">This workspace contains the tools you need to create, manage, and publish experiments.</span><span class="sxs-lookup"><span data-stu-id="21f60-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="21f60-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span><span class="sxs-lookup"><span data-stu-id="21f60-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="21f60-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="21f60-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="21f60-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="21f60-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="21f60-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span><span class="sxs-lookup"><span data-stu-id="21f60-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Select workspace in Studio][2]

> [!TIP]
> <span data-ttu-id="21f60-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span><span class="sxs-lookup"><span data-stu-id="21f60-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="21f60-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span><span class="sxs-lookup"><span data-stu-id="21f60-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="21f60-120">You just need the Microsoft account or organizational account for each user.</span><span class="sxs-lookup"><span data-stu-id="21f60-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="21f60-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="21f60-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="21f60-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="21f60-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png

