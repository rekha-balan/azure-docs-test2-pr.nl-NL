---
title: Quickstart article for Visual Studio Tools for Machine Learning on Azure | Microsoft Docs
description: This article describe how to get started using Visual Studio Tools for Machine Learning, from creating an experiment, training a model, and operationalizing a web-service.
services: machine-learning
ms.workload: data-services
author: chris-lauren
ms.author: chris.lauren
ms.service: machine-learning
ms.component: core
ms.custom: mvc, vs-azure
ms.topic: quickstart
ms.date: 11/15/2017
ms.openlocfilehash: 94bca4d7670b1ec6fba5057b8295f7a3caac2968
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865758"
---
# <a name="visual-studio-tools-for-ai"></a><span data-ttu-id="9dc7c-103">Visual Studio Tools for AI</span><span class="sxs-lookup"><span data-stu-id="9dc7c-103">Visual Studio Tools for AI</span></span>
<span data-ttu-id="9dc7c-104">Visual Studio Tools for AI is a development extension to build, test, and deploy Deep Learning / AI solutions.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-104">Visual Studio Tools for AI is a development extension to build, test, and deploy Deep Learning / AI solutions.</span></span> <span data-ttu-id="9dc7c-105">It features a seamless integration with Azure Machine Learning, notably a run history view, detailing the performance of previous trainings and custom metrics.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-105">It features a seamless integration with Azure Machine Learning, notably a run history view, detailing the performance of previous trainings and custom metrics.</span></span> <span data-ttu-id="9dc7c-106">It offers a samples explorer view, allowing to browse and bootstrap new project with  [Microsoft Cognitive Toolkit (previously known as CNTK)](http://www.microsoft.com/en-us/cognitive-toolkit), [Google TensorFlow](https://www.tensorflow.org), and other deep-learning framework.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-106">It offers a samples explorer view, allowing to browse and bootstrap new project with  [Microsoft Cognitive Toolkit (previously known as CNTK)](http://www.microsoft.com/en-us/cognitive-toolkit), [Google TensorFlow](https://www.tensorflow.org), and other deep-learning framework.</span></span> <span data-ttu-id="9dc7c-107">Finally, it provides an explorer for compute targets, which enables you to submit jobs to train models on remote environments like Azure Virtual Machines or Linux servers with GPU.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-107">Finally, it provides an explorer for compute targets, which enables you to submit jobs to train models on remote environments like Azure Virtual Machines or Linux servers with GPU.</span></span> <span data-ttu-id="9dc7c-108">It also provides a facilitated access to [Azure Batch AI (Preview)](https://docs.microsoft.com/azure/batch-ai/).</span><span class="sxs-lookup"><span data-stu-id="9dc7c-108">It also provides a facilitated access to [Azure Batch AI (Preview)](https://docs.microsoft.com/azure/batch-ai/).</span></span>
 
## <a name="getting-started"></a><span data-ttu-id="9dc7c-109">Getting started</span><span class="sxs-lookup"><span data-stu-id="9dc7c-109">Getting started</span></span> 
<span data-ttu-id="9dc7c-110">To get started, you first need to download and install [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9dc7c-110">To get started, you first need to download and install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="9dc7c-111">Once you have Visual Studio open, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="9dc7c-111">Once you have Visual Studio open, do the following steps:</span></span>
1. <span data-ttu-id="9dc7c-112">Click "Tools" on the menu bar in Visual Studio and select "Extensions and Updates..."</span><span class="sxs-lookup"><span data-stu-id="9dc7c-112">Click "Tools" on the menu bar in Visual Studio and select "Extensions and Updates..."</span></span>
2. <span data-ttu-id="9dc7c-113">Click on "Online" tab and select "Search Visual Studio Marketplace."</span><span class="sxs-lookup"><span data-stu-id="9dc7c-113">Click on "Online" tab and select "Search Visual Studio Marketplace."</span></span>
3. <span data-ttu-id="9dc7c-114">Search for "Visual Studio for AI."</span><span class="sxs-lookup"><span data-stu-id="9dc7c-114">Search for "Visual Studio for AI."</span></span> 
3. <span data-ttu-id="9dc7c-115">Click on the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-115">Click on the **Download** button.</span></span> 
4. <span data-ttu-id="9dc7c-116">After installation, restart Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-116">After installation, restart Visual Studio.</span></span> 

<span data-ttu-id="9dc7c-117">Once Visual Studio is reloaded, the extension is active.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-117">Once Visual Studio is reloaded, the extension is active.</span></span> <span data-ttu-id="9dc7c-118">[Learn more about finding extensions](hhttps://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions).</span><span class="sxs-lookup"><span data-stu-id="9dc7c-118">[Learn more about finding extensions](hhttps://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions).</span></span>

> [!NOTE]
> <span data-ttu-id="9dc7c-119">Visual Studio Tools for AI needs Visual Studio 2015 or 2017, professional or enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-119">Visual Studio Tools for AI needs Visual Studio 2015 or 2017, professional or enterprise edition.</span></span> <span data-ttu-id="9dc7c-120">It does not support Apple OSX version.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-120">It does not support Apple OSX version.</span></span> 


## <a name="exploring-project-samples"></a><span data-ttu-id="9dc7c-121">Exploring project samples</span><span class="sxs-lookup"><span data-stu-id="9dc7c-121">Exploring project samples</span></span>
<span data-ttu-id="9dc7c-122">Visual Studio Tools for AI comes with a samples explorer.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-122">Visual Studio Tools for AI comes with a samples explorer.</span></span> <span data-ttu-id="9dc7c-123">The samples explorer makes it easy to discover sample and try them with only a few clicks.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-123">The samples explorer makes it easy to discover sample and try them with only a few clicks.</span></span> <span data-ttu-id="9dc7c-124">To open the explorer, do as follows:</span><span class="sxs-lookup"><span data-stu-id="9dc7c-124">To open the explorer, do as follows:</span></span>   
1. <span data-ttu-id="9dc7c-125">In the menu bar, click on **AI Tools**.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-125">In the menu bar, click on **AI Tools**.</span></span>
2. <span data-ttu-id="9dc7c-126">Click on "Azure Machine Learning Gallery."</span><span class="sxs-lookup"><span data-stu-id="9dc7c-126">Click on "Azure Machine Learning Gallery."</span></span>

<span data-ttu-id="9dc7c-127">A tab with all the Azure ML Samples opens.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-127">A tab with all the Azure ML Samples opens.</span></span>

## <a name="creating-a-new-project-from-the-sample-explorer"></a><span data-ttu-id="9dc7c-128">Creating a new project from the sample explorer</span><span class="sxs-lookup"><span data-stu-id="9dc7c-128">Creating a new project from the sample explorer</span></span> 
<span data-ttu-id="9dc7c-129">You can browse different samples and get more information about them.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-129">You can browse different samples and get more information about them.</span></span> <span data-ttu-id="9dc7c-130">Let's browse until finding the "Classifying Iris" sample.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-130">Let's browse until finding the "Classifying Iris" sample.</span></span> <span data-ttu-id="9dc7c-131">To create a new project based on this sample do as follows:</span><span class="sxs-lookup"><span data-stu-id="9dc7c-131">To create a new project based on this sample do as follows:</span></span>
1. <span data-ttu-id="9dc7c-132">Click on **install** button on the project sample, this will open a new dialogue.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-132">Click on **install** button on the project sample, this will open a new dialogue.</span></span> 
2. <span data-ttu-id="9dc7c-133">Select a resource group, an account, and a workspace.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-133">Select a resource group, an account, and a workspace.</span></span>
3. <span data-ttu-id="9dc7c-134">You can leave project type as General.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-134">You can leave project type as General.</span></span>
4. <span data-ttu-id="9dc7c-135">Enter a project path and a project name, then press enter.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-135">Enter a project path and a project name, then press enter.</span></span> 
5. <span data-ttu-id="9dc7c-136">A dialogue opens prompting to save a solution, click save.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-136">A dialogue opens prompting to save a solution, click save.</span></span> 

<span data-ttu-id="9dc7c-137">Once complete, a new project opens in a new instance of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-137">Once complete, a new project opens in a new instance of Visual Studio.</span></span> 

> [!TIP]
> <span data-ttu-id="9dc7c-138">You need to be logged-in to access your Azure resource.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-138">You need to be logged-in to access your Azure resource.</span></span> <span data-ttu-id="9dc7c-139">From the embedded terminal enter "az login" and follow the instruction.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-139">From the embedded terminal enter "az login" and follow the instruction.</span></span> 

## <a name="submitting-experiment-with-the-new-project"></a><span data-ttu-id="9dc7c-140">Submitting experiment with the new project</span><span class="sxs-lookup"><span data-stu-id="9dc7c-140">Submitting experiment with the new project</span></span>
<span data-ttu-id="9dc7c-141">The new project being open in Visual Studio, submit a job to a compute target (local or VM with docker).</span><span class="sxs-lookup"><span data-stu-id="9dc7c-141">The new project being open in Visual Studio, submit a job to a compute target (local or VM with docker).</span></span>
<span data-ttu-id="9dc7c-142">To submit the job, do as follow:</span><span class="sxs-lookup"><span data-stu-id="9dc7c-142">To submit the job, do as follow:</span></span> 
1. <span data-ttu-id="9dc7c-143">From the solution explorer, right-click on the file you want to submit, and select **Set as Startup File**.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-143">From the solution explorer, right-click on the file you want to submit, and select **Set as Startup File**.</span></span>
2. <span data-ttu-id="9dc7c-144">Select the project name, right-click and select **Submit Job...**</span><span class="sxs-lookup"><span data-stu-id="9dc7c-144">Select the project name, right-click and select **Submit Job...**</span></span>
3. <span data-ttu-id="9dc7c-145">A new dialogue will open, letting you choose the cluster (or compute target) to execute your script.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-145">A new dialogue will open, letting you choose the cluster (or compute target) to execute your script.</span></span>
4. <span data-ttu-id="9dc7c-146">Click on **Submit**</span><span class="sxs-lookup"><span data-stu-id="9dc7c-146">Click on **Submit**</span></span>

<span data-ttu-id="9dc7c-147">Once the job is submitted, the embedded-terminal displays the progress of the runs.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-147">Once the job is submitted, the embedded-terminal displays the progress of the runs.</span></span>

## <a name="view-list-of-jobs"></a><span data-ttu-id="9dc7c-148">View list of jobs</span><span class="sxs-lookup"><span data-stu-id="9dc7c-148">View list of jobs</span></span>
<span data-ttu-id="9dc7c-149">Once the job is submitted, you can list the jobs from the run history.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-149">Once the job is submitted, you can list the jobs from the run history.</span></span>
1. <span data-ttu-id="9dc7c-150">In **Server Explorer**, click on **AI Tools**.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-150">In **Server Explorer**, click on **AI Tools**.</span></span>
2. <span data-ttu-id="9dc7c-151">Then select **Azure Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="9dc7c-151">Then select **Azure Machine Learning**</span></span>
3. <span data-ttu-id="9dc7c-152">Click on the **Jobs** menu.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-152">Click on the **Jobs** menu.</span></span>

<span data-ttu-id="9dc7c-153">The Job explorer list all the submitted experiment for this project.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-153">The Job explorer list all the submitted experiment for this project.</span></span> 

## <a name="view-job-details"></a><span data-ttu-id="9dc7c-154">View job details</span><span class="sxs-lookup"><span data-stu-id="9dc7c-154">View job details</span></span>
<span data-ttu-id="9dc7c-155">With the Job explorer view open, click on the first run in the list.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-155">With the Job explorer view open, click on the first run in the list.</span></span>
<span data-ttu-id="9dc7c-156">This will load the Job Summary panel, and the Logs and Outputs panel.</span><span class="sxs-lookup"><span data-stu-id="9dc7c-156">This will load the Job Summary panel, and the Logs and Outputs panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dc7c-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="9dc7c-157">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9dc7c-158">How to configure Azure Machine Learning to work with an IDE</span><span class="sxs-lookup"><span data-stu-id="9dc7c-158">How to configure Azure Machine Learning to work with an IDE</span></span>](./how-to-configure-your-IDE.md)
