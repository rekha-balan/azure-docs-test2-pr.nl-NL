---
title: Quickstart article for Visual Studio Code Tools for Machine Learning on Azure | Microsoft Docs
description: This article describe how to get started using Visual Studio Code Tools for Machine Learning, from creating an experiment, training a model, and operationalizing a web-service.
services: machine-learning
author: chris-lauren
ms.author: chris.lauren
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: quickstart
ms.date: 11/15/2017
ms.openlocfilehash: a215c562ad15b69dcec20c1951fe8bc3fe80c6ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857792"
---
# <a name="visual-studio-code-tools-for-ai"></a><span data-ttu-id="17208-103">Visual Studio Code Tools for AI</span><span class="sxs-lookup"><span data-stu-id="17208-103">Visual Studio Code Tools for AI</span></span>
<span data-ttu-id="17208-104">Visual Studio Code Tools for AI is a development extension to build, test, and deploy Deep Learning / AI solutions.</span><span class="sxs-lookup"><span data-stu-id="17208-104">Visual Studio Code Tools for AI is a development extension to build, test, and deploy Deep Learning / AI solutions.</span></span> <span data-ttu-id="17208-105">It features a seamless integration with Azure Machine Learning, notably a run history view, detailing the performance of previous trainings and custom metrics.</span><span class="sxs-lookup"><span data-stu-id="17208-105">It features a seamless integration with Azure Machine Learning, notably a run history view, detailing the performance of previous trainings and custom metrics.</span></span> <span data-ttu-id="17208-106">It offers a samples explorer view, allowing to browse and bootstrap new project with  [Microsoft Cognitive Toolkit (previously known as CNTK)](http://www.microsoft.com/en-us/cognitive-toolkit), [Google TensorFlow](https://www.tensorflow.org), and other deep-learning framework.</span><span class="sxs-lookup"><span data-stu-id="17208-106">It offers a samples explorer view, allowing to browse and bootstrap new project with  [Microsoft Cognitive Toolkit (previously known as CNTK)](http://www.microsoft.com/en-us/cognitive-toolkit), [Google TensorFlow](https://www.tensorflow.org), and other deep-learning framework.</span></span> <span data-ttu-id="17208-107">Finally, it provides an explorer for compute targets, which enables you to submit jobs to train models on remote environments like Azure Virtual Machines or Linux servers with GPU.</span><span class="sxs-lookup"><span data-stu-id="17208-107">Finally, it provides an explorer for compute targets, which enables you to submit jobs to train models on remote environments like Azure Virtual Machines or Linux servers with GPU.</span></span> 
 
## <a name="getting-started"></a><span data-ttu-id="17208-108">Getting started</span><span class="sxs-lookup"><span data-stu-id="17208-108">Getting started</span></span> 
<span data-ttu-id="17208-109">To get started, you first need to download and install [Visual Studio Code](https://code.visualstudio.com/Download).</span><span class="sxs-lookup"><span data-stu-id="17208-109">To get started, you first need to download and install [Visual Studio Code](https://code.visualstudio.com/Download).</span></span> <span data-ttu-id="17208-110">Once you have Visual Studio Code open, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="17208-110">Once you have Visual Studio Code open, do the following steps:</span></span>
1. <span data-ttu-id="17208-111">Click on the extension icon in the activity bar.</span><span class="sxs-lookup"><span data-stu-id="17208-111">Click on the extension icon in the activity bar.</span></span> 
2. <span data-ttu-id="17208-112">Search for "Visual Studio Code Tools for AI".</span><span class="sxs-lookup"><span data-stu-id="17208-112">Search for "Visual Studio Code Tools for AI".</span></span> 
3. <span data-ttu-id="17208-113">Click on the **Install** button.</span><span class="sxs-lookup"><span data-stu-id="17208-113">Click on the **Install** button.</span></span> 
4. <span data-ttu-id="17208-114">After installation, click on **Reload** button.</span><span class="sxs-lookup"><span data-stu-id="17208-114">After installation, click on **Reload** button.</span></span> 

<span data-ttu-id="17208-115">Once Visual Studio Code is reloaded, the extension is active.</span><span class="sxs-lookup"><span data-stu-id="17208-115">Once Visual Studio Code is reloaded, the extension is active.</span></span> <span data-ttu-id="17208-116">[Learn more about installing extensions](https://code.visualstudio.com/docs/editor/extension-gallery).</span><span class="sxs-lookup"><span data-stu-id="17208-116">[Learn more about installing extensions](https://code.visualstudio.com/docs/editor/extension-gallery).</span></span>

## <a name="exploring-project-samples"></a><span data-ttu-id="17208-117">Exploring project samples</span><span class="sxs-lookup"><span data-stu-id="17208-117">Exploring project samples</span></span>
<span data-ttu-id="17208-118">Visual Studio Code Tools for AI comes with a samples explorer.</span><span class="sxs-lookup"><span data-stu-id="17208-118">Visual Studio Code Tools for AI comes with a samples explorer.</span></span> <span data-ttu-id="17208-119">The samples explorer makes it easy to discover sample and try them with only a few clicks.</span><span class="sxs-lookup"><span data-stu-id="17208-119">The samples explorer makes it easy to discover sample and try them with only a few clicks.</span></span> <span data-ttu-id="17208-120">To open the explorer, do as follow:</span><span class="sxs-lookup"><span data-stu-id="17208-120">To open the explorer, do as follow:</span></span>   
1. <span data-ttu-id="17208-121">Open the command palette (View > **Command Palette** or **Ctrl+Shift+P**).</span><span class="sxs-lookup"><span data-stu-id="17208-121">Open the command palette (View > **Command Palette** or **Ctrl+Shift+P**).</span></span>
2. <span data-ttu-id="17208-122">Enter "AI Sample".</span><span class="sxs-lookup"><span data-stu-id="17208-122">Enter "AI Sample".</span></span> 
3. <span data-ttu-id="17208-123">You get a recommendation for "AI: Open Azure ML Sample Explorer", select it and press enter.</span><span class="sxs-lookup"><span data-stu-id="17208-123">You get a recommendation for "AI: Open Azure ML Sample Explorer", select it and press enter.</span></span> 

<span data-ttu-id="17208-124">Alternatively, you can click on the samples explorer icon.</span><span class="sxs-lookup"><span data-stu-id="17208-124">Alternatively, you can click on the samples explorer icon.</span></span>

## <a name="creating-a-new-project-from-the-sample-explorer"></a><span data-ttu-id="17208-125">Creating a new project from the sample explorer</span><span class="sxs-lookup"><span data-stu-id="17208-125">Creating a new project from the sample explorer</span></span> 
<span data-ttu-id="17208-126">You can browse different samples and get more information about them.</span><span class="sxs-lookup"><span data-stu-id="17208-126">You can browse different samples and get more information about them.</span></span> <span data-ttu-id="17208-127">Let's browse until finding the "Classifying Iris" sample.</span><span class="sxs-lookup"><span data-stu-id="17208-127">Let's browse until finding the "Classifying Iris" sample.</span></span> <span data-ttu-id="17208-128">To create a new project based on this sample do the following:</span><span class="sxs-lookup"><span data-stu-id="17208-128">To create a new project based on this sample do the following:</span></span>
1. <span data-ttu-id="17208-129">Click install button on the project sample, notice the commands being prompted, walking you through the steps of creating a new project.</span><span class="sxs-lookup"><span data-stu-id="17208-129">Click install button on the project sample, notice the commands being prompted, walking you through the steps of creating a new project.</span></span> 
2. <span data-ttu-id="17208-130">Pick a name for the project, for example "Iris".</span><span class="sxs-lookup"><span data-stu-id="17208-130">Pick a name for the project, for example "Iris".</span></span>
3. <span data-ttu-id="17208-131">Choose a folder path to create your project and press enter.</span><span class="sxs-lookup"><span data-stu-id="17208-131">Choose a folder path to create your project and press enter.</span></span> 
4. <span data-ttu-id="17208-132">Select an existing workspace and press enter.</span><span class="sxs-lookup"><span data-stu-id="17208-132">Select an existing workspace and press enter.</span></span>

<span data-ttu-id="17208-133">The project will then be created.</span><span class="sxs-lookup"><span data-stu-id="17208-133">The project will then be created.</span></span>

> [!TIP]
> <span data-ttu-id="17208-134">You will need to be logged-in to access your Azure resource.</span><span class="sxs-lookup"><span data-stu-id="17208-134">You will need to be logged-in to access your Azure resource.</span></span> <span data-ttu-id="17208-135">From the embedded terminal enter "az login" and follow the instruction.</span><span class="sxs-lookup"><span data-stu-id="17208-135">From the embedded terminal enter "az login" and follow the instruction.</span></span> 

## <a name="submitting-experiment-with-the-new-project"></a><span data-ttu-id="17208-136">Submitting experiment with the new project</span><span class="sxs-lookup"><span data-stu-id="17208-136">Submitting experiment with the new project</span></span>
<span data-ttu-id="17208-137">The new project being open in Visual Studio Code, we submit a job to our different compute target (local and VM with docker).</span><span class="sxs-lookup"><span data-stu-id="17208-137">The new project being open in Visual Studio Code, we submit a job to our different compute target (local and VM with docker).</span></span>
<span data-ttu-id="17208-138">Visual Studio Code Tools for AI provides multiple ways to submit an experiment.</span><span class="sxs-lookup"><span data-stu-id="17208-138">Visual Studio Code Tools for AI provides multiple ways to submit an experiment.</span></span> 
1. <span data-ttu-id="17208-139">Context Menu (right click) - **AI: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="17208-139">Context Menu (right click) - **AI: Submit Job**.</span></span>
2. <span data-ttu-id="17208-140">From the command palette: "AI: Submit Job".</span><span class="sxs-lookup"><span data-stu-id="17208-140">From the command palette: "AI: Submit Job".</span></span>
3. <span data-ttu-id="17208-141">Alternatively, you can run the command directly using Azure CLI, Machine Learning Commands, using the embedded terminal.</span><span class="sxs-lookup"><span data-stu-id="17208-141">Alternatively, you can run the command directly using Azure CLI, Machine Learning Commands, using the embedded terminal.</span></span>

<span data-ttu-id="17208-142">Open iris_sklearn.py, right click and select **AI: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="17208-142">Open iris_sklearn.py, right click and select **AI: Submit Job**.</span></span>
1. <span data-ttu-id="17208-143">Select your platform: "Azure Machine Learning".</span><span class="sxs-lookup"><span data-stu-id="17208-143">Select your platform: "Azure Machine Learning".</span></span>
2. <span data-ttu-id="17208-144">Select your run-configuration: "Docker-Python."</span><span class="sxs-lookup"><span data-stu-id="17208-144">Select your run-configuration: "Docker-Python."</span></span>

> [!NOTE]
> <span data-ttu-id="17208-145">If it is the first time your submit a job, you receive a message "No Machine Learning configuration found, creating...".</span><span class="sxs-lookup"><span data-stu-id="17208-145">If it is the first time your submit a job, you receive a message "No Machine Learning configuration found, creating...".</span></span> <span data-ttu-id="17208-146">A JSON file is opened, save it (**Ctrl+S**).</span><span class="sxs-lookup"><span data-stu-id="17208-146">A JSON file is opened, save it (**Ctrl+S**).</span></span>

<span data-ttu-id="17208-147">Once the job is submitted, the embedded-terminal displays the progress of the runs.</span><span class="sxs-lookup"><span data-stu-id="17208-147">Once the job is submitted, the embedded-terminal displays the progress of the runs.</span></span> 

## <a name="view-list-of-jobs"></a><span data-ttu-id="17208-148">View list of jobs</span><span class="sxs-lookup"><span data-stu-id="17208-148">View list of jobs</span></span>
<span data-ttu-id="17208-149">Once the jobs are submitted, you can list the jobs from the run history.</span><span class="sxs-lookup"><span data-stu-id="17208-149">Once the jobs are submitted, you can list the jobs from the run history.</span></span>
1. <span data-ttu-id="17208-150">Open the command palette (View > **Command Palette** or **Ctrl+Shift+P**).</span><span class="sxs-lookup"><span data-stu-id="17208-150">Open the command palette (View > **Command Palette** or **Ctrl+Shift+P**).</span></span>
2. <span data-ttu-id="17208-151">Enter "AI List."</span><span class="sxs-lookup"><span data-stu-id="17208-151">Enter "AI List."</span></span>
3. <span data-ttu-id="17208-152">You get a recommendation for "AI: List Jobs", select and press enter.</span><span class="sxs-lookup"><span data-stu-id="17208-152">You get a recommendation for "AI: List Jobs", select and press enter.</span></span>

<span data-ttu-id="17208-153">The Job List View opens and displays all the runs and some related information.</span><span class="sxs-lookup"><span data-stu-id="17208-153">The Job List View opens and displays all the runs and some related information.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="17208-154">View job details</span><span class="sxs-lookup"><span data-stu-id="17208-154">View job details</span></span>
<span data-ttu-id="17208-155">With the Job List View still open, click on the first run in the list.</span><span class="sxs-lookup"><span data-stu-id="17208-155">With the Job List View still open, click on the first run in the list.</span></span>
<span data-ttu-id="17208-156">To deep dive into the results of a job, click on the top **job ID** to see detailed information.</span><span class="sxs-lookup"><span data-stu-id="17208-156">To deep dive into the results of a job, click on the top **job ID** to see detailed information.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="17208-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="17208-157">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="17208-158">How to configure Azure Machine Learning to work with an IDE</span><span class="sxs-lookup"><span data-stu-id="17208-158">How to configure Azure Machine Learning to work with an IDE</span></span>](./how-to-configure-your-IDE.md)
