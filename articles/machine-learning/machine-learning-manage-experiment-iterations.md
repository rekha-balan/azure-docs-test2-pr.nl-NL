---
title: Manage experiment iterations in Machine Learning Studio | Microsoft Docs
description: How to manage experiment iterations in Azure Machine Learning Studio
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: f9e531209a5e77e114d597df25d4d012eb0df655
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553560"
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="24535-103">Manage experiment iterations in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="24535-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="24535-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span><span class="sxs-lookup"><span data-stu-id="24535-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="24535-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span><span class="sxs-lookup"><span data-stu-id="24535-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="24535-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span><span class="sxs-lookup"><span data-stu-id="24535-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="24535-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span><span class="sxs-lookup"><span data-stu-id="24535-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="24535-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span><span class="sxs-lookup"><span data-stu-id="24535-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="24535-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span><span class="sxs-lookup"><span data-stu-id="24535-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="24535-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span><span class="sxs-lookup"><span data-stu-id="24535-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="24535-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span><span class="sxs-lookup"><span data-stu-id="24535-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span></span> <span data-ttu-id="24535-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span><span class="sxs-lookup"><span data-stu-id="24535-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span></span> <span data-ttu-id="24535-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span><span class="sxs-lookup"><span data-stu-id="24535-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span></span> <span data-ttu-id="24535-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span><span class="sxs-lookup"><span data-stu-id="24535-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-the-prior-run"></a><span data-ttu-id="24535-115">Viewing the Prior Run</span><span class="sxs-lookup"><span data-stu-id="24535-115">Viewing the Prior Run</span></span>
<span data-ttu-id="24535-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span><span class="sxs-lookup"><span data-stu-id="24535-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span></span>

<span data-ttu-id="24535-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span><span class="sxs-lookup"><span data-stu-id="24535-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="24535-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span><span class="sxs-lookup"><span data-stu-id="24535-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span></span>

## <a name="viewing-the-run-history"></a><span data-ttu-id="24535-119">Viewing the Run History</span><span class="sxs-lookup"><span data-stu-id="24535-119">Viewing the Run History</span></span>
<span data-ttu-id="24535-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span><span class="sxs-lookup"><span data-stu-id="24535-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="24535-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span><span class="sxs-lookup"><span data-stu-id="24535-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="24535-122">You run the experiment multiple times with different values for this parameter, as follows:</span><span class="sxs-lookup"><span data-stu-id="24535-122">You run the experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="24535-123">Learning Rate value</span><span class="sxs-lookup"><span data-stu-id="24535-123">Learning Rate value</span></span> | <span data-ttu-id="24535-124">Run start time</span><span class="sxs-lookup"><span data-stu-id="24535-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="24535-125">0.1</span><span class="sxs-lookup"><span data-stu-id="24535-125">0.1</span></span> |<span data-ttu-id="24535-126">9/11/2014 4:18:58 pm</span><span class="sxs-lookup"><span data-stu-id="24535-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="24535-127">0.2</span><span class="sxs-lookup"><span data-stu-id="24535-127">0.2</span></span> |<span data-ttu-id="24535-128">9/11/2014 4:24:33 pm</span><span class="sxs-lookup"><span data-stu-id="24535-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="24535-129">0.4</span><span class="sxs-lookup"><span data-stu-id="24535-129">0.4</span></span> |<span data-ttu-id="24535-130">9/11/2014 4:28:36 pm</span><span class="sxs-lookup"><span data-stu-id="24535-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="24535-131">0.5</span><span class="sxs-lookup"><span data-stu-id="24535-131">0.5</span></span> |<span data-ttu-id="24535-132">9/11/2014 4:33:31 pm</span><span class="sxs-lookup"><span data-stu-id="24535-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="24535-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span><span class="sxs-lookup"><span data-stu-id="24535-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![Example run history][runhistory]

<span data-ttu-id="24535-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span><span class="sxs-lookup"><span data-stu-id="24535-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span></span> <span data-ttu-id="24535-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span><span class="sxs-lookup"><span data-stu-id="24535-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="24535-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span><span class="sxs-lookup"><span data-stu-id="24535-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span></span> <span data-ttu-id="24535-138">The title, summary, and module comments are saved with each run of the experiment.</span><span class="sxs-lookup"><span data-stu-id="24535-138">The title, summary, and module comments are saved with each run of the experiment.</span></span>
> 
> 

<span data-ttu-id="24535-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span><span class="sxs-lookup"><span data-stu-id="24535-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span></span> <span data-ttu-id="24535-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span><span class="sxs-lookup"><span data-stu-id="24535-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="24535-141">Iterating on a Previous Run</span><span class="sxs-lookup"><span data-stu-id="24535-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="24535-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span><span class="sxs-lookup"><span data-stu-id="24535-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="24535-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="24535-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span></span> <span data-ttu-id="24535-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span><span class="sxs-lookup"><span data-stu-id="24535-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span></span> <span data-ttu-id="24535-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span><span class="sxs-lookup"><span data-stu-id="24535-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="24535-146">For example, suppose you have the experiment run history shown in the previous section.</span><span class="sxs-lookup"><span data-stu-id="24535-146">For example, suppose you have the experiment run history shown in the previous section.</span></span> <span data-ttu-id="24535-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span><span class="sxs-lookup"><span data-stu-id="24535-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="24535-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span><span class="sxs-lookup"><span data-stu-id="24535-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span></span>
2. <span data-ttu-id="24535-149">Click **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="24535-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="24535-150">Enter a new title and click the **OK** checkmark.</span><span class="sxs-lookup"><span data-stu-id="24535-150">Enter a new title and click the **OK** checkmark.</span></span> <span data-ttu-id="24535-151">A new copy of the experiment is created.</span><span class="sxs-lookup"><span data-stu-id="24535-151">A new copy of the experiment is created.</span></span>
4. <span data-ttu-id="24535-152">Modify the **Number of training epochs** parameter.</span><span class="sxs-lookup"><span data-stu-id="24535-152">Modify the **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="24535-153">Click **RUN**.</span><span class="sxs-lookup"><span data-stu-id="24535-153">Click **RUN**.</span></span>

<span data-ttu-id="24535-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span><span class="sxs-lookup"><span data-stu-id="24535-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span></span>

<!-- Images -->
[runhistory]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/

