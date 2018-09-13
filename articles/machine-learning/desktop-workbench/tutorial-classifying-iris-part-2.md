---
title: Build a model tutorial for Azure Machine Learning services (preview) | Microsoft Docs
description: This full-length tutorial shows how to use Azure Machine Learning services (preview) end to end. This is part two and discusses experimentation.
services: machine-learning
author: hning86
ms.author: haining
manager: mwinkle
ms.reviewer: jmartens
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: tutorial
ms.date: 3/15/2018
ms.openlocfilehash: 4f9b14762332bd11fd69a855d8fabdb206e34919
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867986"
---
# <a name="tutorial-2-classify-iris---build-a-model"></a><span data-ttu-id="0fde8-104">Tutorial 2: Classify Iris - Build a model</span><span class="sxs-lookup"><span data-stu-id="0fde8-104">Tutorial 2: Classify Iris - Build a model</span></span>
<span data-ttu-id="0fde8-105">Azure Machine Learning services (preview) are an integrated, data science and advanced analytics solution for professional data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="0fde8-105">Azure Machine Learning services (preview) are an integrated, data science and advanced analytics solution for professional data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span></span>

<span data-ttu-id="0fde8-106">This tutorial is **part two of a three-part series**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-106">This tutorial is **part two of a three-part series**.</span></span> <span data-ttu-id="0fde8-107">In this part of the tutorial, you use Azure Machine Learning services to:</span><span class="sxs-lookup"><span data-stu-id="0fde8-107">In this part of the tutorial, you use Azure Machine Learning services to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0fde8-108">Open scripts and review code</span><span class="sxs-lookup"><span data-stu-id="0fde8-108">Open scripts and review code</span></span>
> * <span data-ttu-id="0fde8-109">Execute scripts in a local environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-109">Execute scripts in a local environment</span></span>
> * <span data-ttu-id="0fde8-110">Review run histories</span><span class="sxs-lookup"><span data-stu-id="0fde8-110">Review run histories</span></span>
> * <span data-ttu-id="0fde8-111">Execute scripts in a local Azure CLI window</span><span class="sxs-lookup"><span data-stu-id="0fde8-111">Execute scripts in a local Azure CLI window</span></span>
> * <span data-ttu-id="0fde8-112">Execute scripts in a local Docker environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-112">Execute scripts in a local Docker environment</span></span>
> * <span data-ttu-id="0fde8-113">Execute scripts in a remote Docker environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-113">Execute scripts in a remote Docker environment</span></span>
> * <span data-ttu-id="0fde8-114">Execute scripts in a cloud Azure HDInsight environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-114">Execute scripts in a cloud Azure HDInsight environment</span></span>

<span data-ttu-id="0fde8-115">This tutorial uses the timeless [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span><span class="sxs-lookup"><span data-stu-id="0fde8-115">This tutorial uses the timeless [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0fde8-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0fde8-116">Prerequisites</span></span>

<span data-ttu-id="0fde8-117">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="0fde8-117">To complete this tutorial, you need:</span></span>
- <span data-ttu-id="0fde8-118">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0fde8-118">An Azure subscription.</span></span> <span data-ttu-id="0fde8-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="0fde8-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 
- <span data-ttu-id="0fde8-120">An experimentation account and Azure Machine Learning Workbench installed as described in this [quickstart](../service/quickstart-installation.md)</span><span class="sxs-lookup"><span data-stu-id="0fde8-120">An experimentation account and Azure Machine Learning Workbench installed as described in this [quickstart](../service/quickstart-installation.md)</span></span>
- <span data-ttu-id="0fde8-121">The project and prepared Iris data from [Tutorial part 1](tutorial-classifying-iris-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="0fde8-121">The project and prepared Iris data from [Tutorial part 1](tutorial-classifying-iris-part-1.md)</span></span>
- <span data-ttu-id="0fde8-122">A Docker engine installed and running locally.</span><span class="sxs-lookup"><span data-stu-id="0fde8-122">A Docker engine installed and running locally.</span></span> <span data-ttu-id="0fde8-123">Docker's Community Edition is sufficient.</span><span class="sxs-lookup"><span data-stu-id="0fde8-123">Docker's Community Edition is sufficient.</span></span> <span data-ttu-id="0fde8-124">Learn how to install Docker here: https://docs.docker.com/engine/installation/.</span><span class="sxs-lookup"><span data-stu-id="0fde8-124">Learn how to install Docker here: https://docs.docker.com/engine/installation/.</span></span>

## <a name="review-irissklearnpy-and-the-configuration-files"></a><span data-ttu-id="0fde8-125">Review iris_sklearn.py and the configuration files</span><span class="sxs-lookup"><span data-stu-id="0fde8-125">Review iris_sklearn.py and the configuration files</span></span>

1. <span data-ttu-id="0fde8-126">Launch the Azure Machine Learning Workbench application.</span><span class="sxs-lookup"><span data-stu-id="0fde8-126">Launch the Azure Machine Learning Workbench application.</span></span>

1. <span data-ttu-id="0fde8-127">Open the **myIris** project you created in [Part 1 of the tutorial series](tutorial-classifying-iris-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="0fde8-127">Open the **myIris** project you created in [Part 1 of the tutorial series](tutorial-classifying-iris-part-1.md).</span></span>

2. <span data-ttu-id="0fde8-128">In the open project, select the **Files** button (the folder icon) on the far-left pane to open the file list in your project folder.</span><span class="sxs-lookup"><span data-stu-id="0fde8-128">In the open project, select the **Files** button (the folder icon) on the far-left pane to open the file list in your project folder.</span></span>

   ![Open the Azure Machine Learning Workbench project](media/tutorial-classifying-iris/2-project-open.png)

3. <span data-ttu-id="0fde8-130">Select the **iris_sklearn.py** Python script file.</span><span class="sxs-lookup"><span data-stu-id="0fde8-130">Select the **iris_sklearn.py** Python script file.</span></span> 

   ![Choose a script](media/tutorial-classifying-iris/2-choose-iris_sklearn.png)

   <span data-ttu-id="0fde8-132">The code opens in a new text editor tab inside the Workbench.</span><span class="sxs-lookup"><span data-stu-id="0fde8-132">The code opens in a new text editor tab inside the Workbench.</span></span> <span data-ttu-id="0fde8-133">This is the script you use throughout this part of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fde8-133">This is the script you use throughout this part of the tutorial.</span></span> 

   >[!NOTE]
   ><span data-ttu-id="0fde8-134">The code you see might not be exactly the same as the preceding code, because this sample project is updated frequently.</span><span class="sxs-lookup"><span data-stu-id="0fde8-134">The code you see might not be exactly the same as the preceding code, because this sample project is updated frequently.</span></span>
   
   ![Open a file](media/tutorial-classifying-iris/open_iris_sklearn.png)

4. <span data-ttu-id="0fde8-136">Inspect the Python script code to become familiar with the coding style.</span><span class="sxs-lookup"><span data-stu-id="0fde8-136">Inspect the Python script code to become familiar with the coding style.</span></span> 

   <span data-ttu-id="0fde8-137">The script **iris_sklearn.py** performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="0fde8-137">The script **iris_sklearn.py** performs the following tasks:</span></span>

   * <span data-ttu-id="0fde8-138">Loads the default data preparation package called **iris.dprep** to create a [pandas DataFrame](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html).</span><span class="sxs-lookup"><span data-stu-id="0fde8-138">Loads the default data preparation package called **iris.dprep** to create a [pandas DataFrame](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html).</span></span> 

   * <span data-ttu-id="0fde8-139">Adds random features to make the problem more difficult to solve.</span><span class="sxs-lookup"><span data-stu-id="0fde8-139">Adds random features to make the problem more difficult to solve.</span></span> <span data-ttu-id="0fde8-140">Randomness is necessary because Iris is a small data set that is easily classified with nearly 100% accuracy.</span><span class="sxs-lookup"><span data-stu-id="0fde8-140">Randomness is necessary because Iris is a small data set that is easily classified with nearly 100% accuracy.</span></span>

   * <span data-ttu-id="0fde8-141">Uses the [scikit-learn](http://scikit-learn.org/stable/index.html) machine learning library to build a logistic regression model.</span><span class="sxs-lookup"><span data-stu-id="0fde8-141">Uses the [scikit-learn](http://scikit-learn.org/stable/index.html) machine learning library to build a logistic regression model.</span></span>  <span data-ttu-id="0fde8-142">This library comes with Azure Machine Learning Workbench by default.</span><span class="sxs-lookup"><span data-stu-id="0fde8-142">This library comes with Azure Machine Learning Workbench by default.</span></span>

   * <span data-ttu-id="0fde8-143">Serializes the model using the [pickle](https://docs.python.org/3/library/pickle.html) library into a file in the `outputs` folder.</span><span class="sxs-lookup"><span data-stu-id="0fde8-143">Serializes the model using the [pickle](https://docs.python.org/3/library/pickle.html) library into a file in the `outputs` folder.</span></span> 
   
   * <span data-ttu-id="0fde8-144">Loads the serialized model, and then deserializes it back into memory.</span><span class="sxs-lookup"><span data-stu-id="0fde8-144">Loads the serialized model, and then deserializes it back into memory.</span></span>

   * <span data-ttu-id="0fde8-145">Uses the deserialized model to make a prediction on a new record.</span><span class="sxs-lookup"><span data-stu-id="0fde8-145">Uses the deserialized model to make a prediction on a new record.</span></span> 

   * <span data-ttu-id="0fde8-146">Plots two graphs, a confusion matrix and a multi-class receiver operating characteristic (ROC) curve, using the [matplotlib](https://matplotlib.org/) library, and then saves them in the `outputs` folder.</span><span class="sxs-lookup"><span data-stu-id="0fde8-146">Plots two graphs, a confusion matrix and a multi-class receiver operating characteristic (ROC) curve, using the [matplotlib](https://matplotlib.org/) library, and then saves them in the `outputs` folder.</span></span> <span data-ttu-id="0fde8-147">You can install this library in your environment if it isn't there already.</span><span class="sxs-lookup"><span data-stu-id="0fde8-147">You can install this library in your environment if it isn't there already.</span></span>

   * <span data-ttu-id="0fde8-148">Plots the regulatization rate and model accuracy in the run history automatically.</span><span class="sxs-lookup"><span data-stu-id="0fde8-148">Plots the regulatization rate and model accuracy in the run history automatically.</span></span> <span data-ttu-id="0fde8-149">The `run_logger` object is used throughout to record the regularization rate and the model accuracy into the logs.</span><span class="sxs-lookup"><span data-stu-id="0fde8-149">The `run_logger` object is used throughout to record the regularization rate and the model accuracy into the logs.</span></span> 


## <a name="run-irissklearnpy-in-your-local-environment"></a><span data-ttu-id="0fde8-150">Run iris_sklearn.py in your local environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-150">Run iris_sklearn.py in your local environment</span></span>

1. <span data-ttu-id="0fde8-151">Start the Azure Machine Learning command-line interface (CLI):</span><span class="sxs-lookup"><span data-stu-id="0fde8-151">Start the Azure Machine Learning command-line interface (CLI):</span></span>
   1. <span data-ttu-id="0fde8-152">Launch the Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="0fde8-152">Launch the Azure Machine Learning Workbench.</span></span>

   1. <span data-ttu-id="0fde8-153">From the Workbench menu, select **File** > **Open Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-153">From the Workbench menu, select **File** > **Open Command Prompt**.</span></span> 
   
   <span data-ttu-id="0fde8-154">The Azure Machine Learning command-line interface (CLI) window starts in the project folder  `C:\Temp\myIris\>` on Windows.</span><span class="sxs-lookup"><span data-stu-id="0fde8-154">The Azure Machine Learning command-line interface (CLI) window starts in the project folder  `C:\Temp\myIris\>` on Windows.</span></span> <span data-ttu-id="0fde8-155">This project is the same as the one you created in Part 1 of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fde8-155">This project is the same as the one you created in Part 1 of the tutorial.</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="0fde8-156">You must use this CLI window to accomplish the next steps.</span><span class="sxs-lookup"><span data-stu-id="0fde8-156">You must use this CLI window to accomplish the next steps.</span></span>

1. <span data-ttu-id="0fde8-157">In the CLI window, install the Python plotting library, **matplotlib**, if you do not already have the library.</span><span class="sxs-lookup"><span data-stu-id="0fde8-157">In the CLI window, install the Python plotting library, **matplotlib**, if you do not already have the library.</span></span>

   <span data-ttu-id="0fde8-158">The **iris_sklearn.py** script has dependencies on two Python packages: **scikit-learn** and **matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-158">The **iris_sklearn.py** script has dependencies on two Python packages: **scikit-learn** and **matplotlib**.</span></span>  <span data-ttu-id="0fde8-159">The **scikit-learn** package is installed by Azure Machine Learning Workbench for your convenience.</span><span class="sxs-lookup"><span data-stu-id="0fde8-159">The **scikit-learn** package is installed by Azure Machine Learning Workbench for your convenience.</span></span> <span data-ttu-id="0fde8-160">But, you need to install **matplotlib** if you don't have it installed yet.</span><span class="sxs-lookup"><span data-stu-id="0fde8-160">But, you need to install **matplotlib** if you don't have it installed yet.</span></span>

   <span data-ttu-id="0fde8-161">If you move on without installing **matplotlib**, the code in this tutorial can still run successfully.</span><span class="sxs-lookup"><span data-stu-id="0fde8-161">If you move on without installing **matplotlib**, the code in this tutorial can still run successfully.</span></span> <span data-ttu-id="0fde8-162">However, the code will not be able to produce the confusion matrix output and the multi-class ROC curve plots shown in the history visualizations.</span><span class="sxs-lookup"><span data-stu-id="0fde8-162">However, the code will not be able to produce the confusion matrix output and the multi-class ROC curve plots shown in the history visualizations.</span></span>

   ```azurecli
   pip install matplotlib
   ```

   <span data-ttu-id="0fde8-163">This install takes about a minute.</span><span class="sxs-lookup"><span data-stu-id="0fde8-163">This install takes about a minute.</span></span>

1. <span data-ttu-id="0fde8-164">Return to the Workbench application.</span><span class="sxs-lookup"><span data-stu-id="0fde8-164">Return to the Workbench application.</span></span> 

1. <span data-ttu-id="0fde8-165">Find the tab called **iris_sklearn.py**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-165">Find the tab called **iris_sklearn.py**.</span></span> 

   ![Find tab with script](media/tutorial-classifying-iris/2-iris_sklearn-tab.png)

1. <span data-ttu-id="0fde8-167">In the toolbar of that tab, select **local** as the execution environment, and `iris_sklearn.py` as the script to run.</span><span class="sxs-lookup"><span data-stu-id="0fde8-167">In the toolbar of that tab, select **local** as the execution environment, and `iris_sklearn.py` as the script to run.</span></span> <span data-ttu-id="0fde8-168">These may already be selected.</span><span class="sxs-lookup"><span data-stu-id="0fde8-168">These may already be selected.</span></span>

   ![Local and script choice](media/tutorial-classifying-iris/2-local-script.png)

1. <span data-ttu-id="0fde8-170">Move to the right side of the toolbar and enter `0.01` in the **Arguments** field.</span><span class="sxs-lookup"><span data-stu-id="0fde8-170">Move to the right side of the toolbar and enter `0.01` in the **Arguments** field.</span></span> 

   <span data-ttu-id="0fde8-171">This value corresponds to the regularization rate of the logistic regression model.</span><span class="sxs-lookup"><span data-stu-id="0fde8-171">This value corresponds to the regularization rate of the logistic regression model.</span></span>

   ![Local and script choice](media/tutorial-classifying-iris/2-local-script-arguments.png)

1. <span data-ttu-id="0fde8-173">Select the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="0fde8-173">Select the **Run** button.</span></span> <span data-ttu-id="0fde8-174">A job is immediately scheduled.</span><span class="sxs-lookup"><span data-stu-id="0fde8-174">A job is immediately scheduled.</span></span> <span data-ttu-id="0fde8-175">The job is listed in the **Jobs** pane on the right side of the workbench window.</span><span class="sxs-lookup"><span data-stu-id="0fde8-175">The job is listed in the **Jobs** pane on the right side of the workbench window.</span></span> 

   ![Local and script choice](media/tutorial-classifying-iris/2-local-script-arguments-run.png)

   <span data-ttu-id="0fde8-177">After a few moments, the status of the job transitions from **Submitting**, to **Running**, and finally to **Completed**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-177">After a few moments, the status of the job transitions from **Submitting**, to **Running**, and finally to **Completed**.</span></span>

1. <span data-ttu-id="0fde8-178">Select **Completed** in the job status text in the **Jobs** pane.</span><span class="sxs-lookup"><span data-stu-id="0fde8-178">Select **Completed** in the job status text in the **Jobs** pane.</span></span> 

   ![Run sklearn](media/tutorial-classifying-iris/2-completed.png)

   <span data-ttu-id="0fde8-180">A pop-up window opens and displays the standard output (stdout) text for the run.</span><span class="sxs-lookup"><span data-stu-id="0fde8-180">A pop-up window opens and displays the standard output (stdout) text for the run.</span></span> <span data-ttu-id="0fde8-181">To close the stdout text, select the **Close** (**x**) button on the upper right of the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="0fde8-181">To close the stdout text, select the **Close** (**x**) button on the upper right of the pop-up window.</span></span>

   ![Standard output](media/tutorial-classifying-iris/2-standard-output.png)

9. <span data-ttu-id="0fde8-183">In the same job status in the **Jobs** pane, select the blue text **iris_sklearn.py [n]** (_n_ is the run number) just above the **Completed** status and the start time.</span><span class="sxs-lookup"><span data-stu-id="0fde8-183">In the same job status in the **Jobs** pane, select the blue text **iris_sklearn.py [n]** (_n_ is the run number) just above the **Completed** status and the start time.</span></span> <span data-ttu-id="0fde8-184">The **Run Properties** window opens and shows the following information for that particular run:</span><span class="sxs-lookup"><span data-stu-id="0fde8-184">The **Run Properties** window opens and shows the following information for that particular run:</span></span>
   - <span data-ttu-id="0fde8-185">**Run Properties** information</span><span class="sxs-lookup"><span data-stu-id="0fde8-185">**Run Properties** information</span></span>
   - <span data-ttu-id="0fde8-186">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="0fde8-186">**Outputs**</span></span>
   - <span data-ttu-id="0fde8-187">**Metrics**</span><span class="sxs-lookup"><span data-stu-id="0fde8-187">**Metrics**</span></span>
   - <span data-ttu-id="0fde8-188">**Visualizations**, if any</span><span class="sxs-lookup"><span data-stu-id="0fde8-188">**Visualizations**, if any</span></span>
   - <span data-ttu-id="0fde8-189">**Logs**</span><span class="sxs-lookup"><span data-stu-id="0fde8-189">**Logs**</span></span> 

   <span data-ttu-id="0fde8-190">When the run is finished, the pop-up window shows the following results:</span><span class="sxs-lookup"><span data-stu-id="0fde8-190">When the run is finished, the pop-up window shows the following results:</span></span>

   >[!NOTE]
   ><span data-ttu-id="0fde8-191">Because the tutorial introduced some randomization into the training set earlier, your exact results might vary from the results shown here.</span><span class="sxs-lookup"><span data-stu-id="0fde8-191">Because the tutorial introduced some randomization into the training set earlier, your exact results might vary from the results shown here.</span></span>

   ```text
   Python version: 3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
   
   Iris dataset shape: (150, 5)
   Regularization rate is 0.01
   LogisticRegression(C=100.0, class_weight=None, dual=False, fit_intercept=True,
          intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,
          penalty='l2', random_state=None, solver='liblinear', tol=0.0001,
          verbose=0, warm_start=False)
   Accuracy is 0.6792452830188679
   
   ==========================================
   Serialize and deserialize using the outputs folder.
   
   Export the model to model.pkl
   Import the model from model.pkl
   New sample: [[3.0, 3.6, 1.3, 0.25]]
   Predicted class is ['Iris-setosa']
   Plotting confusion matrix...
   Confusion matrix in text:
   [[50  0  0]
    [ 1 37 12]
    [ 0  4 46]]
   Confusion matrix plotted.
   Plotting ROC curve....
   ROC curve plotted.
   Confusion matrix and ROC curve plotted. See them in Run History details pane.
   ```
    
10. <span data-ttu-id="0fde8-192">Close the **Run Properties** tab, and then return to the **iris_sklearn.py** tab.</span><span class="sxs-lookup"><span data-stu-id="0fde8-192">Close the **Run Properties** tab, and then return to the **iris_sklearn.py** tab.</span></span> 

11. <span data-ttu-id="0fde8-193">Repeat for additional runs.</span><span class="sxs-lookup"><span data-stu-id="0fde8-193">Repeat for additional runs.</span></span> 

    <span data-ttu-id="0fde8-194">Enter a series of values in the **Arguments** field ranging from `0.001` to `10`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-194">Enter a series of values in the **Arguments** field ranging from `0.001` to `10`.</span></span> <span data-ttu-id="0fde8-195">Select **Run** to execute the code a few more times.</span><span class="sxs-lookup"><span data-stu-id="0fde8-195">Select **Run** to execute the code a few more times.</span></span> <span data-ttu-id="0fde8-196">The argument value you change each time is fed to the logistic regression model in the code, resulting in different findings each time.</span><span class="sxs-lookup"><span data-stu-id="0fde8-196">The argument value you change each time is fed to the logistic regression model in the code, resulting in different findings each time.</span></span>

## <a name="review-the-run-history-in-detail"></a><span data-ttu-id="0fde8-197">Review the run history in detail</span><span class="sxs-lookup"><span data-stu-id="0fde8-197">Review the run history in detail</span></span>
<span data-ttu-id="0fde8-198">In Azure Machine Learning Workbench, every script execution is captured as a run history record.</span><span class="sxs-lookup"><span data-stu-id="0fde8-198">In Azure Machine Learning Workbench, every script execution is captured as a run history record.</span></span> <span data-ttu-id="0fde8-199">If you open the **Runs** view, you can view the run history of a particular script.</span><span class="sxs-lookup"><span data-stu-id="0fde8-199">If you open the **Runs** view, you can view the run history of a particular script.</span></span>

1. <span data-ttu-id="0fde8-200">To open the list of **Runs**, select the **Runs** button (clock icon) on the left toolbar.</span><span class="sxs-lookup"><span data-stu-id="0fde8-200">To open the list of **Runs**, select the **Runs** button (clock icon) on the left toolbar.</span></span> <span data-ttu-id="0fde8-201">Then select **iris_sklearn.py** to show the **Run Dashboard** of `iris_sklearn.py`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-201">Then select **iris_sklearn.py** to show the **Run Dashboard** of `iris_sklearn.py`.</span></span>

   ![Run view](media/tutorial-classifying-iris/run_view.png)

1. <span data-ttu-id="0fde8-203">The **Run Dashboard** tab opens.</span><span class="sxs-lookup"><span data-stu-id="0fde8-203">The **Run Dashboard** tab opens.</span></span> 

   <span data-ttu-id="0fde8-204">Review the statistics captured across the multiple runs.</span><span class="sxs-lookup"><span data-stu-id="0fde8-204">Review the statistics captured across the multiple runs.</span></span> <span data-ttu-id="0fde8-205">Graphs render in the top of the tab. Each run has a consecutive number, and the run details are listed in the table at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="0fde8-205">Graphs render in the top of the tab. Each run has a consecutive number, and the run details are listed in the table at the bottom of the screen.</span></span>

   ![Run dashboard](media/tutorial-classifying-iris/run_dashboard.png)

1. <span data-ttu-id="0fde8-207">Filter the table, and then select any of the graphs to view the status, duration, accuracy, and regularization rate of each run.</span><span class="sxs-lookup"><span data-stu-id="0fde8-207">Filter the table, and then select any of the graphs to view the status, duration, accuracy, and regularization rate of each run.</span></span> 

1. <span data-ttu-id="0fde8-208">Select the checkboxes next to two or more runs in the **Runs** table.</span><span class="sxs-lookup"><span data-stu-id="0fde8-208">Select the checkboxes next to two or more runs in the **Runs** table.</span></span> <span data-ttu-id="0fde8-209">Select the **Compare** button to open a detailed comparison pane.</span><span class="sxs-lookup"><span data-stu-id="0fde8-209">Select the **Compare** button to open a detailed comparison pane.</span></span> <span data-ttu-id="0fde8-210">Review the side-by-side comparison.</span><span class="sxs-lookup"><span data-stu-id="0fde8-210">Review the side-by-side comparison.</span></span> 

1. <span data-ttu-id="0fde8-211">To return to the **Run Dashboard**, select the **Run List** back button on the upper left of the **Comparison** pane.</span><span class="sxs-lookup"><span data-stu-id="0fde8-211">To return to the **Run Dashboard**, select the **Run List** back button on the upper left of the **Comparison** pane.</span></span>

   ![Return to Run list](media/tutorial-classifying-iris/2-compare-back.png)

1. <span data-ttu-id="0fde8-213">Select an individual run to see the run detail view.</span><span class="sxs-lookup"><span data-stu-id="0fde8-213">Select an individual run to see the run detail view.</span></span> <span data-ttu-id="0fde8-214">Notice that the statistics for the selected run are listed in the **Run Properties** section.</span><span class="sxs-lookup"><span data-stu-id="0fde8-214">Notice that the statistics for the selected run are listed in the **Run Properties** section.</span></span> <span data-ttu-id="0fde8-215">The files written into the output folder are listed in the **Outputs** section, and you can download the files from there.</span><span class="sxs-lookup"><span data-stu-id="0fde8-215">The files written into the output folder are listed in the **Outputs** section, and you can download the files from there.</span></span>

   ![Run details](media/tutorial-classifying-iris/run_details.png)

   <span data-ttu-id="0fde8-217">The two plots, the confusion matrix and the multi-class ROC curve, are rendered in the **Visualizations** section.</span><span class="sxs-lookup"><span data-stu-id="0fde8-217">The two plots, the confusion matrix and the multi-class ROC curve, are rendered in the **Visualizations** section.</span></span> <span data-ttu-id="0fde8-218">All the log files can also be found in the **Logs** section.</span><span class="sxs-lookup"><span data-stu-id="0fde8-218">All the log files can also be found in the **Logs** section.</span></span>


## <a name="run-scripts-in-local-docker-environments"></a><span data-ttu-id="0fde8-219">Run scripts in local Docker environments</span><span class="sxs-lookup"><span data-stu-id="0fde8-219">Run scripts in local Docker environments</span></span>

<span data-ttu-id="0fde8-220">Optionally, you can experiment with running scripts against a local Docker container.</span><span class="sxs-lookup"><span data-stu-id="0fde8-220">Optionally, you can experiment with running scripts against a local Docker container.</span></span> <span data-ttu-id="0fde8-221">You can configure additional execution environments, such as Docker, and run your script in those environments.</span><span class="sxs-lookup"><span data-stu-id="0fde8-221">You can configure additional execution environments, such as Docker, and run your script in those environments.</span></span> 

>[!NOTE]
><span data-ttu-id="0fde8-222">To experiment with dispatching scripts to run in a Docker container in a remote Azure VM or an Azure HDInsight Spark cluster, you can follow the [instructions to create an Ubuntu-based Azure Data Science Virtual Machine or HDInsight cluster](how-to-create-dsvm-hdi.md).</span><span class="sxs-lookup"><span data-stu-id="0fde8-222">To experiment with dispatching scripts to run in a Docker container in a remote Azure VM or an Azure HDInsight Spark cluster, you can follow the [instructions to create an Ubuntu-based Azure Data Science Virtual Machine or HDInsight cluster](how-to-create-dsvm-hdi.md).</span></span>

1. <span data-ttu-id="0fde8-223">If you have not yet done so, install and start Docker locally on your Windows or MacOS machine.</span><span class="sxs-lookup"><span data-stu-id="0fde8-223">If you have not yet done so, install and start Docker locally on your Windows or MacOS machine.</span></span> <span data-ttu-id="0fde8-224">For more information, see the Docker installation instructions at https://docs.docker.com/install/.</span><span class="sxs-lookup"><span data-stu-id="0fde8-224">For more information, see the Docker installation instructions at https://docs.docker.com/install/.</span></span> <span data-ttu-id="0fde8-225">Community edition is sufficient.</span><span class="sxs-lookup"><span data-stu-id="0fde8-225">Community edition is sufficient.</span></span>

1. <span data-ttu-id="0fde8-226">On the left pane, select the **Folder** icon to open the **Files** list for your project.</span><span class="sxs-lookup"><span data-stu-id="0fde8-226">On the left pane, select the **Folder** icon to open the **Files** list for your project.</span></span> <span data-ttu-id="0fde8-227">Expand the `aml_config` folder.</span><span class="sxs-lookup"><span data-stu-id="0fde8-227">Expand the `aml_config` folder.</span></span> 

2. <span data-ttu-id="0fde8-228">There are several environments that are preconfigured: **docker-python**, **docker-spark**, and **local**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-228">There are several environments that are preconfigured: **docker-python**, **docker-spark**, and **local**.</span></span> 

   <span data-ttu-id="0fde8-229">Each environment has two files, such as `docker.compute` (for both **docker-python** and **docker-spark**) and `docker-python.runconfig`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-229">Each environment has two files, such as `docker.compute` (for both **docker-python** and **docker-spark**) and `docker-python.runconfig`.</span></span> <span data-ttu-id="0fde8-230">Open each file to see that certain options are configurable in the text editor.</span><span class="sxs-lookup"><span data-stu-id="0fde8-230">Open each file to see that certain options are configurable in the text editor.</span></span>  

   <span data-ttu-id="0fde8-231">To clean up, select **Close** (**x**) on the tabs for any open text editors.</span><span class="sxs-lookup"><span data-stu-id="0fde8-231">To clean up, select **Close** (**x**) on the tabs for any open text editors.</span></span>

3. <span data-ttu-id="0fde8-232">Run the **iris_sklearn.py** script by using the **docker-python** environment:</span><span class="sxs-lookup"><span data-stu-id="0fde8-232">Run the **iris_sklearn.py** script by using the **docker-python** environment:</span></span> 

   - <span data-ttu-id="0fde8-233">On the left toolbar, select the **Clock** icon to open the **Runs** pane.</span><span class="sxs-lookup"><span data-stu-id="0fde8-233">On the left toolbar, select the **Clock** icon to open the **Runs** pane.</span></span> <span data-ttu-id="0fde8-234">Select **All Runs**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-234">Select **All Runs**.</span></span> 

   - <span data-ttu-id="0fde8-235">On the top of the **All Runs** tab, select **docker-python** as the targeted environment instead of the default **local**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-235">On the top of the **All Runs** tab, select **docker-python** as the targeted environment instead of the default **local**.</span></span> 

   - <span data-ttu-id="0fde8-236">Next, move to the right side and select **iris_sklearn.py** as the script to run.</span><span class="sxs-lookup"><span data-stu-id="0fde8-236">Next, move to the right side and select **iris_sklearn.py** as the script to run.</span></span> 

   - <span data-ttu-id="0fde8-237">Leave the **Arguments** field blank because the script specifies a default value.</span><span class="sxs-lookup"><span data-stu-id="0fde8-237">Leave the **Arguments** field blank because the script specifies a default value.</span></span> 

   - <span data-ttu-id="0fde8-238">Select the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="0fde8-238">Select the **Run** button.</span></span>

4. <span data-ttu-id="0fde8-239">Observe that a new job starts.</span><span class="sxs-lookup"><span data-stu-id="0fde8-239">Observe that a new job starts.</span></span> <span data-ttu-id="0fde8-240">It appears in the **Jobs** pane on the right side of the workbench window.</span><span class="sxs-lookup"><span data-stu-id="0fde8-240">It appears in the **Jobs** pane on the right side of the workbench window.</span></span>

   <span data-ttu-id="0fde8-241">When you run against Docker for the first time, the job takes a few extra minutes to finish.</span><span class="sxs-lookup"><span data-stu-id="0fde8-241">When you run against Docker for the first time, the job takes a few extra minutes to finish.</span></span> 

   <span data-ttu-id="0fde8-242">Behind the scenes, Azure Machine Learning Workbench builds a new Docker file.</span><span class="sxs-lookup"><span data-stu-id="0fde8-242">Behind the scenes, Azure Machine Learning Workbench builds a new Docker file.</span></span> 
   <span data-ttu-id="0fde8-243">The new file references the base Docker image specified in the `docker.compute` file and the dependency Python packages specified in the `conda_dependencies.yml` file.</span><span class="sxs-lookup"><span data-stu-id="0fde8-243">The new file references the base Docker image specified in the `docker.compute` file and the dependency Python packages specified in the `conda_dependencies.yml` file.</span></span> 
   
   <span data-ttu-id="0fde8-244">The Docker engine performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="0fde8-244">The Docker engine performs the following tasks:</span></span>

    - <span data-ttu-id="0fde8-245">Downloads the base image from Azure.</span><span class="sxs-lookup"><span data-stu-id="0fde8-245">Downloads the base image from Azure.</span></span>
    - <span data-ttu-id="0fde8-246">Installs the Python packages specified in the `conda_dependencies.yml` file.</span><span class="sxs-lookup"><span data-stu-id="0fde8-246">Installs the Python packages specified in the `conda_dependencies.yml` file.</span></span>
    - <span data-ttu-id="0fde8-247">Starts a Docker container.</span><span class="sxs-lookup"><span data-stu-id="0fde8-247">Starts a Docker container.</span></span>
    - <span data-ttu-id="0fde8-248">Copies or references, depending on the run configuration, the local copy of the project folder.</span><span class="sxs-lookup"><span data-stu-id="0fde8-248">Copies or references, depending on the run configuration, the local copy of the project folder.</span></span>      
    - <span data-ttu-id="0fde8-249">Executes the `iris_sklearn.py` script.</span><span class="sxs-lookup"><span data-stu-id="0fde8-249">Executes the `iris_sklearn.py` script.</span></span>

   <span data-ttu-id="0fde8-250">In the end, you should see the exact same results as you do when you target **local**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-250">In the end, you should see the exact same results as you do when you target **local**.</span></span>

5. <span data-ttu-id="0fde8-251">Now, let's try Spark.</span><span class="sxs-lookup"><span data-stu-id="0fde8-251">Now, let's try Spark.</span></span> <span data-ttu-id="0fde8-252">The Docker base image contains a preinstalled and configured Spark instance that you can use to execute a PySpark script.</span><span class="sxs-lookup"><span data-stu-id="0fde8-252">The Docker base image contains a preinstalled and configured Spark instance that you can use to execute a PySpark script.</span></span> <span data-ttu-id="0fde8-253">Using this base image is an easy way to develop and test your Spark program, without having to spend time installing and configuring Spark yourself.</span><span class="sxs-lookup"><span data-stu-id="0fde8-253">Using this base image is an easy way to develop and test your Spark program, without having to spend time installing and configuring Spark yourself.</span></span> 

   <span data-ttu-id="0fde8-254">Open the `iris_spark.py` file.</span><span class="sxs-lookup"><span data-stu-id="0fde8-254">Open the `iris_spark.py` file.</span></span> <span data-ttu-id="0fde8-255">This script loads the `iris.csv` data file, and uses the logistic regression algorithm from the Spark Machine Learning library to classify the Iris data set.</span><span class="sxs-lookup"><span data-stu-id="0fde8-255">This script loads the `iris.csv` data file, and uses the logistic regression algorithm from the Spark Machine Learning library to classify the Iris data set.</span></span> <span data-ttu-id="0fde8-256">Now change the run environment to **docker-spark** and the script to **iris_spark.py**, and then run it again.</span><span class="sxs-lookup"><span data-stu-id="0fde8-256">Now change the run environment to **docker-spark** and the script to **iris_spark.py**, and then run it again.</span></span> <span data-ttu-id="0fde8-257">This process takes a little longer because a Spark session has to be created and started inside the Docker container.</span><span class="sxs-lookup"><span data-stu-id="0fde8-257">This process takes a little longer because a Spark session has to be created and started inside the Docker container.</span></span> <span data-ttu-id="0fde8-258">You can also see the stdout is different than the stdout of `iris_spark.py`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-258">You can also see the stdout is different than the stdout of `iris_spark.py`.</span></span>

6. <span data-ttu-id="0fde8-259">Start a few more runs and play with different arguments.</span><span class="sxs-lookup"><span data-stu-id="0fde8-259">Start a few more runs and play with different arguments.</span></span> 

7. <span data-ttu-id="0fde8-260">Open the `iris_spark.py` file to see the logistic regression model built using the Spark Machine Learning library.</span><span class="sxs-lookup"><span data-stu-id="0fde8-260">Open the `iris_spark.py` file to see the logistic regression model built using the Spark Machine Learning library.</span></span> 

8. <span data-ttu-id="0fde8-261">Interact with the **Jobs** pane, run a history list view, and run a details view of your runs across different execution environments.</span><span class="sxs-lookup"><span data-stu-id="0fde8-261">Interact with the **Jobs** pane, run a history list view, and run a details view of your runs across different execution environments.</span></span>

## <a name="run-scripts-in-the-cli-window"></a><span data-ttu-id="0fde8-262">Run scripts in the CLI window</span><span class="sxs-lookup"><span data-stu-id="0fde8-262">Run scripts in the CLI window</span></span>

1. <span data-ttu-id="0fde8-263">Start the Azure Machine Learning command-line interface (CLI):</span><span class="sxs-lookup"><span data-stu-id="0fde8-263">Start the Azure Machine Learning command-line interface (CLI):</span></span>
   1. <span data-ttu-id="0fde8-264">Launch the Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="0fde8-264">Launch the Azure Machine Learning Workbench.</span></span>

   1. <span data-ttu-id="0fde8-265">From the Workbench menu, select **File** > **Open Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-265">From the Workbench menu, select **File** > **Open Command Prompt**.</span></span> 
   
   <span data-ttu-id="0fde8-266">The CLI prompt starts in the project folder  `C:\Temp\myIris\>` on Windows.</span><span class="sxs-lookup"><span data-stu-id="0fde8-266">The CLI prompt starts in the project folder  `C:\Temp\myIris\>` on Windows.</span></span> <span data-ttu-id="0fde8-267">This is the project you created in Part 1 of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fde8-267">This is the project you created in Part 1 of the tutorial.</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="0fde8-268">You must use this CLI window to accomplish the next steps.</span><span class="sxs-lookup"><span data-stu-id="0fde8-268">You must use this CLI window to accomplish the next steps.</span></span>

1. <span data-ttu-id="0fde8-269">In the CLI window, log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="0fde8-269">In the CLI window, log in to Azure.</span></span> <span data-ttu-id="0fde8-270">[Learn more about az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="0fde8-270">[Learn more about az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).</span></span>

   <span data-ttu-id="0fde8-271">You may already be logged in.</span><span class="sxs-lookup"><span data-stu-id="0fde8-271">You may already be logged in.</span></span> <span data-ttu-id="0fde8-272">In that case, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="0fde8-272">In that case, you can skip this step.</span></span>

   1. <span data-ttu-id="0fde8-273">At the command prompt, enter:</span><span class="sxs-lookup"><span data-stu-id="0fde8-273">At the command prompt, enter:</span></span>
      ```azurecli
      az login
      ```

      <span data-ttu-id="0fde8-274">This command returns a code to use in your browser at https://aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="0fde8-274">This command returns a code to use in your browser at https://aka.ms/devicelogin.</span></span>

   1. <span data-ttu-id="0fde8-275">Go to https://aka.ms/devicelogin in your browser.</span><span class="sxs-lookup"><span data-stu-id="0fde8-275">Go to https://aka.ms/devicelogin in your browser.</span></span>

   1. <span data-ttu-id="0fde8-276">When prompted, enter the code, which you received in the CLI, into your browser.</span><span class="sxs-lookup"><span data-stu-id="0fde8-276">When prompted, enter the code, which you received in the CLI, into your browser.</span></span>

   <span data-ttu-id="0fde8-277">The Workbench app and CLI use independent credential caches when authenticating against Azure resources.</span><span class="sxs-lookup"><span data-stu-id="0fde8-277">The Workbench app and CLI use independent credential caches when authenticating against Azure resources.</span></span> <span data-ttu-id="0fde8-278">After you log in, you won't need to authenticated again until the cached token expires.</span><span class="sxs-lookup"><span data-stu-id="0fde8-278">After you log in, you won't need to authenticated again until the cached token expires.</span></span> 

1. <span data-ttu-id="0fde8-279">If your organization has multiple Azure subscriptions (enterprise environment), you must set the subscription to be used.</span><span class="sxs-lookup"><span data-stu-id="0fde8-279">If your organization has multiple Azure subscriptions (enterprise environment), you must set the subscription to be used.</span></span> <span data-ttu-id="0fde8-280">Find your subscription, set it using the subscription ID, and then test it.</span><span class="sxs-lookup"><span data-stu-id="0fde8-280">Find your subscription, set it using the subscription ID, and then test it.</span></span>

   1. <span data-ttu-id="0fde8-281">List every Azure subscription to which you have access using this command:</span><span class="sxs-lookup"><span data-stu-id="0fde8-281">List every Azure subscription to which you have access using this command:</span></span>
   
      ```azurecli
      az account list -o table
      ```

      <span data-ttu-id="0fde8-282">The **az account list** command returns the list of subscriptions available to your login.</span><span class="sxs-lookup"><span data-stu-id="0fde8-282">The **az account list** command returns the list of subscriptions available to your login.</span></span> 
      <span data-ttu-id="0fde8-283">If there is more than one, identify the subscription ID value for the subscription you want to use.</span><span class="sxs-lookup"><span data-stu-id="0fde8-283">If there is more than one, identify the subscription ID value for the subscription you want to use.</span></span>

   1. <span data-ttu-id="0fde8-284">Set the Azure subscription you want to use as the default account:</span><span class="sxs-lookup"><span data-stu-id="0fde8-284">Set the Azure subscription you want to use as the default account:</span></span>
   
      ```azurecli
      az account set -s <your-subscription-id>
      ```
      <span data-ttu-id="0fde8-285">where \<your-subscription-id\> is ID value for the subscription you want to use.</span><span class="sxs-lookup"><span data-stu-id="0fde8-285">where \<your-subscription-id\> is ID value for the subscription you want to use.</span></span> <span data-ttu-id="0fde8-286">Do not include the brackets.</span><span class="sxs-lookup"><span data-stu-id="0fde8-286">Do not include the brackets.</span></span>

   1. <span data-ttu-id="0fde8-287">Confirm the new subscription setting by requesting the details for the current subscription.</span><span class="sxs-lookup"><span data-stu-id="0fde8-287">Confirm the new subscription setting by requesting the details for the current subscription.</span></span> 

      ```azurecli
      az account show
      ```    

1. <span data-ttu-id="0fde8-288">In the CLI window, install the Python plotting library, **matplotlib**, if you do not already have the library.</span><span class="sxs-lookup"><span data-stu-id="0fde8-288">In the CLI window, install the Python plotting library, **matplotlib**, if you do not already have the library.</span></span>

   ```azurecli
   pip install matplotlib
   ```

1. <span data-ttu-id="0fde8-289">In the CLI window, submit the **iris_sklearn.py** script as an experiment.</span><span class="sxs-lookup"><span data-stu-id="0fde8-289">In the CLI window, submit the **iris_sklearn.py** script as an experiment.</span></span>

   <span data-ttu-id="0fde8-290">The execution of iris_sklearn.py is run against the local compute context.</span><span class="sxs-lookup"><span data-stu-id="0fde8-290">The execution of iris_sklearn.py is run against the local compute context.</span></span>

   + <span data-ttu-id="0fde8-291">On Windows:</span><span class="sxs-lookup"><span data-stu-id="0fde8-291">On Windows:</span></span>
     ```azurecli
     az ml experiment submit -c local .\iris_sklearn.py
     ```

   + <span data-ttu-id="0fde8-292">On MacOS:</span><span class="sxs-lookup"><span data-stu-id="0fde8-292">On MacOS:</span></span>
     ```azurecli
     az ml experiment submit -c local iris_sklearn.py
     ```
   
   <span data-ttu-id="0fde8-293">Your output should be similar to:</span><span class="sxs-lookup"><span data-stu-id="0fde8-293">Your output should be similar to:</span></span>
    ```text
    RunId: myIris_1521077190506
    
    Executing user inputs .....
    ===========================
    
    Python version: 3.5.2 |Continuum Analytics, Inc.| (default, Jul  2 2016, 17:52:12) 
    [GCC 4.2.1 Compatible Apple LLVM 4.2 (clang-425.0.28)]
    
    Iris dataset shape: (150, 5)
    Regularization rate is 0.01
    LogisticRegression(C=100.0, class_weight=None, dual=False, fit_intercept=True,
              intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,
              penalty='l2', random_state=None, solver='liblinear', tol=0.0001,
              verbose=0, warm_start=False)
    Accuracy is 0.6792452830188679
        
    ==========================================
    Serialize and deserialize using the outputs folder.
    
    Export the model to model.pkl
    Import the model from model.pkl
    New sample: [[3.0, 3.6, 1.3, 0.25]]
    Predicted class is ['Iris-setosa']
    Plotting confusion matrix...
    Confusion matrix in text:
    [[50  0  0]
     [ 1 37 12]
     [ 0  4 46]]
    Confusion matrix plotted.
    Plotting ROC curve....
    ROC curve plotted.
    Confusion matrix and ROC curve plotted. See them in Run History details page.
    
    Execution Details
    =================
    RunId: myIris_1521077190506
    ```

1. <span data-ttu-id="0fde8-294">Review the output.</span><span class="sxs-lookup"><span data-stu-id="0fde8-294">Review the output.</span></span> <span data-ttu-id="0fde8-295">You have the same output and results that you had when you used the Workbench to run the script.</span><span class="sxs-lookup"><span data-stu-id="0fde8-295">You have the same output and results that you had when you used the Workbench to run the script.</span></span> 

1. <span data-ttu-id="0fde8-296">In the CLI window, run the Python script, **iris_sklearn.py**, again using a Docker execution environment (if you have Docker installed on your machine).</span><span class="sxs-lookup"><span data-stu-id="0fde8-296">In the CLI window, run the Python script, **iris_sklearn.py**, again using a Docker execution environment (if you have Docker installed on your machine).</span></span>

   + <span data-ttu-id="0fde8-297">If your container is on Windows:</span><span class="sxs-lookup"><span data-stu-id="0fde8-297">If your container is on Windows:</span></span> 
     |<span data-ttu-id="0fde8-298">Execution</span><span class="sxs-lookup"><span data-stu-id="0fde8-298">Execution</span></span><br/><span data-ttu-id="0fde8-299">environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-299">environment</span></span>|<span data-ttu-id="0fde8-300">Command on Windows</span><span class="sxs-lookup"><span data-stu-id="0fde8-300">Command on Windows</span></span>|
     |---------------------|------------------|
     |<span data-ttu-id="0fde8-301">Python</span><span class="sxs-lookup"><span data-stu-id="0fde8-301">Python</span></span>|`az ml experiment submit -c docker-python .\iris_sklearn.py 0.01`|
     |<span data-ttu-id="0fde8-302">Spark</span><span class="sxs-lookup"><span data-stu-id="0fde8-302">Spark</span></span>|`az ml experiment submit -c docker-spark .\iris_spark.py 0.1`|

   + <span data-ttu-id="0fde8-303">If your container is on MacOS:</span><span class="sxs-lookup"><span data-stu-id="0fde8-303">If your container is on MacOS:</span></span> 
     |<span data-ttu-id="0fde8-304">Execution</span><span class="sxs-lookup"><span data-stu-id="0fde8-304">Execution</span></span><br/><span data-ttu-id="0fde8-305">environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-305">environment</span></span>|<span data-ttu-id="0fde8-306">Command on Windows</span><span class="sxs-lookup"><span data-stu-id="0fde8-306">Command on Windows</span></span>|
     |---------------------|------------------|
     |<span data-ttu-id="0fde8-307">Python</span><span class="sxs-lookup"><span data-stu-id="0fde8-307">Python</span></span>|`az ml experiment submit -c docker-python iris_sklearn.py 0.01`|
     |<span data-ttu-id="0fde8-308">Spark</span><span class="sxs-lookup"><span data-stu-id="0fde8-308">Spark</span></span>|`az ml experiment submit -c docker-spark iris_spark.py 0.1`|

1. <span data-ttu-id="0fde8-309">Go back to the Workbench, and:</span><span class="sxs-lookup"><span data-stu-id="0fde8-309">Go back to the Workbench, and:</span></span>
   1. <span data-ttu-id="0fde8-310">Select the folder icon on the left pane to list the project files.</span><span class="sxs-lookup"><span data-stu-id="0fde8-310">Select the folder icon on the left pane to list the project files.</span></span>
   
   1. <span data-ttu-id="0fde8-311">Open the Python script named **run.py**.</span><span class="sxs-lookup"><span data-stu-id="0fde8-311">Open the Python script named **run.py**.</span></span> <span data-ttu-id="0fde8-312">This script is useful to loop over various regularization rates.</span><span class="sxs-lookup"><span data-stu-id="0fde8-312">This script is useful to loop over various regularization rates.</span></span> 

   ![Return to Run list](media/tutorial-classifying-iris/2-runpy.png)

1. <span data-ttu-id="0fde8-314">Run the experiment multiple times with those rates.</span><span class="sxs-lookup"><span data-stu-id="0fde8-314">Run the experiment multiple times with those rates.</span></span> 

   <span data-ttu-id="0fde8-315">This script starts an `iris_sklearn.py` job with a regularization rate of `10.0` (a ridiculously large number).</span><span class="sxs-lookup"><span data-stu-id="0fde8-315">This script starts an `iris_sklearn.py` job with a regularization rate of `10.0` (a ridiculously large number).</span></span> <span data-ttu-id="0fde8-316">The script then cuts the rate to half in the following run, and so on, until the rate is no smaller than `0.005`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-316">The script then cuts the rate to half in the following run, and so on, until the rate is no smaller than `0.005`.</span></span> 

   <span data-ttu-id="0fde8-317">The script contains the following code:</span><span class="sxs-lookup"><span data-stu-id="0fde8-317">The script contains the following code:</span></span>

   ![Return to Run list](media/tutorial-classifying-iris/2-runpy-code.png)

1. <span data-ttu-id="0fde8-319">Run the **run.py** script from the command line as follows:</span><span class="sxs-lookup"><span data-stu-id="0fde8-319">Run the **run.py** script from the command line as follows:</span></span>

   ```cmd
   python run.py
   ```

   <span data-ttu-id="0fde8-320">This command submits iris_sklearn.py multiple times with different regularization rates</span><span class="sxs-lookup"><span data-stu-id="0fde8-320">This command submits iris_sklearn.py multiple times with different regularization rates</span></span>

   <span data-ttu-id="0fde8-321">When `run.py` finishes, you can see graphs of different metrics in your run history list view in the workbench.</span><span class="sxs-lookup"><span data-stu-id="0fde8-321">When `run.py` finishes, you can see graphs of different metrics in your run history list view in the workbench.</span></span>

## <a name="run-scripts-in-a-remote-docker-container"></a><span data-ttu-id="0fde8-322">Run scripts in a remote Docker container</span><span class="sxs-lookup"><span data-stu-id="0fde8-322">Run scripts in a remote Docker container</span></span>
<span data-ttu-id="0fde8-323">To execute your script in a Docker container on a remote Linux machine, you need to have SSH access (username and password) to that remote machine.</span><span class="sxs-lookup"><span data-stu-id="0fde8-323">To execute your script in a Docker container on a remote Linux machine, you need to have SSH access (username and password) to that remote machine.</span></span> <span data-ttu-id="0fde8-324">In addition, the machine must have a Docker engine installed and running.</span><span class="sxs-lookup"><span data-stu-id="0fde8-324">In addition, the machine must have a Docker engine installed and running.</span></span> <span data-ttu-id="0fde8-325">The easiest way to obtain such a Linux machine is to create an Ubuntu-based Data Science Virtual Machine (DSVM) on Azure.</span><span class="sxs-lookup"><span data-stu-id="0fde8-325">The easiest way to obtain such a Linux machine is to create an Ubuntu-based Data Science Virtual Machine (DSVM) on Azure.</span></span> <span data-ttu-id="0fde8-326">Learn [how to create an Ubuntu DSVM to use in Azure ML Workbench](how-to-create-dsvm-hdi.md#create-an-ubuntu-dsvm-in-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0fde8-326">Learn [how to create an Ubuntu DSVM to use in Azure ML Workbench](how-to-create-dsvm-hdi.md#create-an-ubuntu-dsvm-in-azure-portal).</span></span>

>[!NOTE] 
><span data-ttu-id="0fde8-327">The CentOS-based DSVM is *not* supported.</span><span class="sxs-lookup"><span data-stu-id="0fde8-327">The CentOS-based DSVM is *not* supported.</span></span>

1. <span data-ttu-id="0fde8-328">After the VM is created, you can attach the VM as an execution environment by generating a pair of `.runconfig` and `.compute` files.</span><span class="sxs-lookup"><span data-stu-id="0fde8-328">After the VM is created, you can attach the VM as an execution environment by generating a pair of `.runconfig` and `.compute` files.</span></span> <span data-ttu-id="0fde8-329">Use the following command to generate the files.</span><span class="sxs-lookup"><span data-stu-id="0fde8-329">Use the following command to generate the files.</span></span> 

 <span data-ttu-id="0fde8-330">Let's name the new compute target `myvm`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-330">Let's name the new compute target `myvm`.</span></span>
 
   ```azurecli
   az ml computetarget attach remotedocker --name myvm --address <your-IP> --username <your-username> --password <your-password>
   ```
   
   >[!NOTE]
   ><span data-ttu-id="0fde8-331">The IP address can also be a publicly addressable fully-qualified domain name (FQDN) such as `vm-name.southcentralus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-331">The IP address can also be a publicly addressable fully-qualified domain name (FQDN) such as `vm-name.southcentralus.cloudapp.azure.com`.</span></span> <span data-ttu-id="0fde8-332">It is a good practice to add an FQDN to your DSVM and use it instead of an IP address.</span><span class="sxs-lookup"><span data-stu-id="0fde8-332">It is a good practice to add an FQDN to your DSVM and use it instead of an IP address.</span></span> <span data-ttu-id="0fde8-333">This practice is a good idea because you might turn off the VM at some point to save on cost.</span><span class="sxs-lookup"><span data-stu-id="0fde8-333">This practice is a good idea because you might turn off the VM at some point to save on cost.</span></span> <span data-ttu-id="0fde8-334">Additionally, the next time you start the VM, the IP address might have changed.</span><span class="sxs-lookup"><span data-stu-id="0fde8-334">Additionally, the next time you start the VM, the IP address might have changed.</span></span>

   >[!NOTE]
   ><span data-ttu-id="0fde8-335">In addition to username and password authentication, you can specify a private key and the corresponding passphrase (if any) using the `--private-key-file` and (optionally) the `--private-key-passphrase` options.</span><span class="sxs-lookup"><span data-stu-id="0fde8-335">In addition to username and password authentication, you can specify a private key and the corresponding passphrase (if any) using the `--private-key-file` and (optionally) the `--private-key-passphrase` options.</span></span> <span data-ttu-id="0fde8-336">If you want to use the private key that you used when created DSVM, you should specify the `--use-azureml-ssh-key` option.</span><span class="sxs-lookup"><span data-stu-id="0fde8-336">If you want to use the private key that you used when created DSVM, you should specify the `--use-azureml-ssh-key` option.</span></span>

   <span data-ttu-id="0fde8-337">Next, prepare the **myvm** compute target by running this command.</span><span class="sxs-lookup"><span data-stu-id="0fde8-337">Next, prepare the **myvm** compute target by running this command.</span></span>
   
   ```azurecli
   az ml experiment prepare -c myvm
   ```
   
   <span data-ttu-id="0fde8-338">The preceding command constructs the Docker image in the VM to get it ready to run the scripts.</span><span class="sxs-lookup"><span data-stu-id="0fde8-338">The preceding command constructs the Docker image in the VM to get it ready to run the scripts.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="0fde8-339">You can also change the value of `PrepareEnvironment` in `myvm.runconfig` from the default value `false` to `true`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-339">You can also change the value of `PrepareEnvironment` in `myvm.runconfig` from the default value `false` to `true`.</span></span> <span data-ttu-id="0fde8-340">This change automatically prepares the Docker container as part of the first run.</span><span class="sxs-lookup"><span data-stu-id="0fde8-340">This change automatically prepares the Docker container as part of the first run.</span></span>

2. <span data-ttu-id="0fde8-341">Edit the generated `myvm.runconfig` file under `aml_config` and change the framework from the default value `PySpark` to `Python`:</span><span class="sxs-lookup"><span data-stu-id="0fde8-341">Edit the generated `myvm.runconfig` file under `aml_config` and change the framework from the default value `PySpark` to `Python`:</span></span>

   ```yaml
   Framework: Python
   ```
   >[!NOTE]
   ><span data-ttu-id="0fde8-342">While PySpark should also work, using Python is more efficient if you don't actually need a Spark session to run your Python script.</span><span class="sxs-lookup"><span data-stu-id="0fde8-342">While PySpark should also work, using Python is more efficient if you don't actually need a Spark session to run your Python script.</span></span>

3. <span data-ttu-id="0fde8-343">Issue the same command as you did before in the CLI window, using target _myvm_ this time to execute iris_sklearn.py in a remote Docker container:</span><span class="sxs-lookup"><span data-stu-id="0fde8-343">Issue the same command as you did before in the CLI window, using target _myvm_ this time to execute iris_sklearn.py in a remote Docker container:</span></span>
   ```azurecli
   az ml experiment submit -c myvm iris_sklearn.py
   ```
   <span data-ttu-id="0fde8-344">The command executes as if you're in a `docker-python` environment, except that the execution happens on the remote Linux VM.</span><span class="sxs-lookup"><span data-stu-id="0fde8-344">The command executes as if you're in a `docker-python` environment, except that the execution happens on the remote Linux VM.</span></span> <span data-ttu-id="0fde8-345">The CLI window displays the same output information.</span><span class="sxs-lookup"><span data-stu-id="0fde8-345">The CLI window displays the same output information.</span></span>

4. <span data-ttu-id="0fde8-346">Let's try using Spark in the container.</span><span class="sxs-lookup"><span data-stu-id="0fde8-346">Let's try using Spark in the container.</span></span> <span data-ttu-id="0fde8-347">Open File Explorer.</span><span class="sxs-lookup"><span data-stu-id="0fde8-347">Open File Explorer.</span></span> <span data-ttu-id="0fde8-348">Make a copy of the `myvm.runconfig` file and name it `myvm-spark.runconfig`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-348">Make a copy of the `myvm.runconfig` file and name it `myvm-spark.runconfig`.</span></span> <span data-ttu-id="0fde8-349">Edit the new file to change the `Framework` setting from `Python` to `PySpark`:</span><span class="sxs-lookup"><span data-stu-id="0fde8-349">Edit the new file to change the `Framework` setting from `Python` to `PySpark`:</span></span>
   ```yaml
   Framework: PySpark
   ```
   <span data-ttu-id="0fde8-350">Don't make any changes to the `myvm.compute` file.</span><span class="sxs-lookup"><span data-stu-id="0fde8-350">Don't make any changes to the `myvm.compute` file.</span></span> <span data-ttu-id="0fde8-351">The same Docker image on the same VM gets used for the Spark execution.</span><span class="sxs-lookup"><span data-stu-id="0fde8-351">The same Docker image on the same VM gets used for the Spark execution.</span></span> <span data-ttu-id="0fde8-352">In the new `myvm-spark.runconfig`, the `Target` field points to the same `myvm.compute` file via its name `myvm`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-352">In the new `myvm-spark.runconfig`, the `Target` field points to the same `myvm.compute` file via its name `myvm`.</span></span>

5. <span data-ttu-id="0fde8-353">Type the following command to run the **iris_spark.py** script in the Spark instance running inside the remote Docker container:</span><span class="sxs-lookup"><span data-stu-id="0fde8-353">Type the following command to run the **iris_spark.py** script in the Spark instance running inside the remote Docker container:</span></span>
   ```azureli
   az ml experiment submit -c myvm-spark .\iris_spark.py
   ```

## <a name="run-scripts-in-hdinsight-clusters"></a><span data-ttu-id="0fde8-354">Run scripts in HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="0fde8-354">Run scripts in HDInsight clusters</span></span>
<span data-ttu-id="0fde8-355">You can also run this script in an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="0fde8-355">You can also run this script in an HDInsight Spark cluster.</span></span> <span data-ttu-id="0fde8-356">Learn [how to create an HDInsight Spark Cluster to use in Azure ML Workbench](how-to-create-dsvm-hdi.md#create-an-apache-spark-for-azure-hdinsight-cluster-in-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0fde8-356">Learn [how to create an HDInsight Spark Cluster to use in Azure ML Workbench](how-to-create-dsvm-hdi.md#create-an-apache-spark-for-azure-hdinsight-cluster-in-azure-portal).</span></span>

>[!NOTE] 
><span data-ttu-id="0fde8-357">The HDInsight cluster must use Azure Blob as the primary storage.</span><span class="sxs-lookup"><span data-stu-id="0fde8-357">The HDInsight cluster must use Azure Blob as the primary storage.</span></span> <span data-ttu-id="0fde8-358">Using Azure Data Lake storage is not supported yet.</span><span class="sxs-lookup"><span data-stu-id="0fde8-358">Using Azure Data Lake storage is not supported yet.</span></span>

1. <span data-ttu-id="0fde8-359">If you have access to a Spark for Azure HDInsight cluster, generate an HDInsight run configuration command as shown here.</span><span class="sxs-lookup"><span data-stu-id="0fde8-359">If you have access to a Spark for Azure HDInsight cluster, generate an HDInsight run configuration command as shown here.</span></span> <span data-ttu-id="0fde8-360">Provide the HDInsight cluster name and your HDInsight username and password as the parameters.</span><span class="sxs-lookup"><span data-stu-id="0fde8-360">Provide the HDInsight cluster name and your HDInsight username and password as the parameters.</span></span> 

   <span data-ttu-id="0fde8-361">Use the following command to create a compute target that points to a HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="0fde8-361">Use the following command to create a compute target that points to a HDInsight cluster:</span></span>

   ```azurecli
   az ml computetarget attach cluster --name myhdi --address <cluster head node FQDN> --username <your-username> --password <your-password>
   ```

   <span data-ttu-id="0fde8-362">To prepare the HDInsight cluster, run this command:</span><span class="sxs-lookup"><span data-stu-id="0fde8-362">To prepare the HDInsight cluster, run this command:</span></span>

   ```
   az ml experiment prepare -c myhdi
   ```

   <span data-ttu-id="0fde8-363">The cluster head node FQDN is typically `<your_cluster_name>-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-363">The cluster head node FQDN is typically `<your_cluster_name>-ssh.azurehdinsight.net`.</span></span>

   >[!NOTE]
   ><span data-ttu-id="0fde8-364">The `username` is the cluster SSH username defined during HDInsight setup.</span><span class="sxs-lookup"><span data-stu-id="0fde8-364">The `username` is the cluster SSH username defined during HDInsight setup.</span></span> <span data-ttu-id="0fde8-365">By default, the value is `sshuser`.</span><span class="sxs-lookup"><span data-stu-id="0fde8-365">By default, the value is `sshuser`.</span></span> <span data-ttu-id="0fde8-366">The value is not `admin`, which is the other user created during setup to enable access to the cluster's admin website.</span><span class="sxs-lookup"><span data-stu-id="0fde8-366">The value is not `admin`, which is the other user created during setup to enable access to the cluster's admin website.</span></span> 

2. <span data-ttu-id="0fde8-367">Run the **iris_spark.py** script in the HDInsight cluster with this command:</span><span class="sxs-lookup"><span data-stu-id="0fde8-367">Run the **iris_spark.py** script in the HDInsight cluster with this command:</span></span>

   ```azurecli
   az ml experiment submit -c myhdi .\iris_spark.py
   ```

   >[!NOTE]
   ><span data-ttu-id="0fde8-368">When you execute against a remote HDInsight cluster, you can also view the Yet Another Resource Negotiator (YARN) job execution details at `https://<your_cluster_name>.azurehdinsight.net/yarnui` by using the `admin` user account.</span><span class="sxs-lookup"><span data-stu-id="0fde8-368">When you execute against a remote HDInsight cluster, you can also view the Yet Another Resource Negotiator (YARN) job execution details at `https://<your_cluster_name>.azurehdinsight.net/yarnui` by using the `admin` user account.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="0fde8-369">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0fde8-369">Clean up resources</span></span>

[!INCLUDE [aml-delete-resource-group](../../../includes/aml-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="0fde8-370">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fde8-370">Next steps</span></span>
<span data-ttu-id="0fde8-371">In this second part of the three-part tutorial series, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="0fde8-371">In this second part of the three-part tutorial series, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="0fde8-372">Open scripts and review the code in Workbench</span><span class="sxs-lookup"><span data-stu-id="0fde8-372">Open scripts and review the code in Workbench</span></span>
> * <span data-ttu-id="0fde8-373">Execute scripts in a local environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-373">Execute scripts in a local environment</span></span>
> * <span data-ttu-id="0fde8-374">Review the run history</span><span class="sxs-lookup"><span data-stu-id="0fde8-374">Review the run history</span></span>
> * <span data-ttu-id="0fde8-375">Execute scripts in a local Docker environment</span><span class="sxs-lookup"><span data-stu-id="0fde8-375">Execute scripts in a local Docker environment</span></span>

<span data-ttu-id="0fde8-376">Now, you can try out the third part of this tutorial series in which you can deploy the logistic regression model you created as a real-time web service.</span><span class="sxs-lookup"><span data-stu-id="0fde8-376">Now, you can try out the third part of this tutorial series in which you can deploy the logistic regression model you created as a real-time web service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0fde8-377">Tutorial 3 - Deploy models</span><span class="sxs-lookup"><span data-stu-id="0fde8-377">Tutorial 3 - Deploy models</span></span>](tutorial-classifying-iris-part-3.md)
