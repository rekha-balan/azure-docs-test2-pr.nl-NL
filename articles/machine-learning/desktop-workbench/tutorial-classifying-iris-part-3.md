---
title: Deploy a model tutorial for Azure Machine Learning services
description: This full-length tutorial shows how to use Azure Machine Learning services end to end. This is part three and discusses the deploying model.
services: machine-learning
author: aashishb
ms.author: aashishb
manager: mwinkle
ms.reviewer: jmartens, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: tutorial
ms.date: 3/13/2018
ms.openlocfilehash: de0c93ef5b907b56e6ad66a04bb728b5b9aabb9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857769"
---
# <a name="tutorial-3-classify-iris-deploy-a-model"></a><span data-ttu-id="a9cbd-104">Tutorial 3: Classify Iris: Deploy a model</span><span class="sxs-lookup"><span data-stu-id="a9cbd-104">Tutorial 3: Classify Iris: Deploy a model</span></span>
<span data-ttu-id="a9cbd-105">Azure Machine Learning (preview) is an integrated, end-to-end data science and advanced analytics solution for professional data scientists.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-105">Azure Machine Learning (preview) is an integrated, end-to-end data science and advanced analytics solution for professional data scientists.</span></span> <span data-ttu-id="a9cbd-106">Data scientists can use it to prepare data, develop experiments, and deploy models at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-106">Data scientists can use it to prepare data, develop experiments, and deploy models at cloud scale.</span></span>

<span data-ttu-id="a9cbd-107">This tutorial is **part three of a three-part series**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-107">This tutorial is **part three of a three-part series**.</span></span> <span data-ttu-id="a9cbd-108">In this part of the tutorial, you use Machine Learning (preview) to:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-108">In this part of the tutorial, you use Machine Learning (preview) to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9cbd-109">Locate the model file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-109">Locate the model file.</span></span>
> * <span data-ttu-id="a9cbd-110">Generate a scoring script and schema file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-110">Generate a scoring script and schema file.</span></span>
> * <span data-ttu-id="a9cbd-111">Prepare the environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-111">Prepare the environment.</span></span>
> * <span data-ttu-id="a9cbd-112">Create a real-time web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-112">Create a real-time web service.</span></span>
> * <span data-ttu-id="a9cbd-113">Run the real-time web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-113">Run the real-time web service.</span></span>
> * <span data-ttu-id="a9cbd-114">Examine the output blob data.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-114">Examine the output blob data.</span></span> 

<span data-ttu-id="a9cbd-115">This tutorial uses the timeless [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span><span class="sxs-lookup"><span data-stu-id="a9cbd-115">This tutorial uses the timeless [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a9cbd-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9cbd-116">Prerequisites</span></span>

<span data-ttu-id="a9cbd-117">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-117">To complete this tutorial, you need:</span></span>
- <span data-ttu-id="a9cbd-118">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-118">An Azure subscription.</span></span> <span data-ttu-id="a9cbd-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 
- <span data-ttu-id="a9cbd-120">An experimentation account and Azure Machine Learning Workbench installed as described in this [quickstart](../service/quickstart-installation.md)</span><span class="sxs-lookup"><span data-stu-id="a9cbd-120">An experimentation account and Azure Machine Learning Workbench installed as described in this [quickstart](../service/quickstart-installation.md)</span></span>
- <span data-ttu-id="a9cbd-121">The classification model from [Tutorial part 2](tutorial-classifying-iris-part-2.md)</span><span class="sxs-lookup"><span data-stu-id="a9cbd-121">The classification model from [Tutorial part 2](tutorial-classifying-iris-part-2.md)</span></span>
- <span data-ttu-id="a9cbd-122">A Docker engine installed and running locally</span><span class="sxs-lookup"><span data-stu-id="a9cbd-122">A Docker engine installed and running locally</span></span>

## <a name="download-the-model-pickle-file"></a><span data-ttu-id="a9cbd-123">Download the model pickle file</span><span class="sxs-lookup"><span data-stu-id="a9cbd-123">Download the model pickle file</span></span>
<span data-ttu-id="a9cbd-124">In the previous part of the tutorial, the **iris_sklearn.py** script was run in the Machine Learning Workbench locally.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-124">In the previous part of the tutorial, the **iris_sklearn.py** script was run in the Machine Learning Workbench locally.</span></span> <span data-ttu-id="a9cbd-125">This action serialized the logistic regression model by using the popular Python object-serialization package [pickle](https://docs.python.org/3/library/pickle.html).</span><span class="sxs-lookup"><span data-stu-id="a9cbd-125">This action serialized the logistic regression model by using the popular Python object-serialization package [pickle](https://docs.python.org/3/library/pickle.html).</span></span> 

1. <span data-ttu-id="a9cbd-126">Open the Machine Learning Workbench application.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-126">Open the Machine Learning Workbench application.</span></span> <span data-ttu-id="a9cbd-127">Then open the **myIris** project you created in the previous parts of the tutorial series.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-127">Then open the **myIris** project you created in the previous parts of the tutorial series.</span></span>

1. <span data-ttu-id="a9cbd-128">After the project is open, select the **Files** button (folder icon) on the left pane to open the file list in your project folder.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-128">After the project is open, select the **Files** button (folder icon) on the left pane to open the file list in your project folder.</span></span>

1. <span data-ttu-id="a9cbd-129">Select the **iris_sklearn.py** file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-129">Select the **iris_sklearn.py** file.</span></span> <span data-ttu-id="a9cbd-130">The Python code opens in a new text editor tab inside the workbench.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-130">The Python code opens in a new text editor tab inside the workbench.</span></span>

1. <span data-ttu-id="a9cbd-131">Review the **iris_sklearn.py** file to see where the pickle file was generated.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-131">Review the **iris_sklearn.py** file to see where the pickle file was generated.</span></span> <span data-ttu-id="a9cbd-132">Select Ctrl+F to open the **Find** dialog box, and then find the word **pickle** in the Python code.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-132">Select Ctrl+F to open the **Find** dialog box, and then find the word **pickle** in the Python code.</span></span>

   <span data-ttu-id="a9cbd-133">This code snippet shows how the pickle output file was generated.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-133">This code snippet shows how the pickle output file was generated.</span></span> <span data-ttu-id="a9cbd-134">The output pickle file is named **model.pkl** on the disk.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-134">The output pickle file is named **model.pkl** on the disk.</span></span> 

   ```python
   print("Export the model to model.pkl")
   f = open('./outputs/model.pkl', 'wb')
   pickle.dump(clf1, f)
   f.close()
   ```

1. <span data-ttu-id="a9cbd-135">Locate the model pickle file in the output files of a previous run.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-135">Locate the model pickle file in the output files of a previous run.</span></span>
   
   <span data-ttu-id="a9cbd-136">When you ran the **iris_sklearn.py** script, the model file was written to the **outputs** folder with the name **model.pkl**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-136">When you ran the **iris_sklearn.py** script, the model file was written to the **outputs** folder with the name **model.pkl**.</span></span> <span data-ttu-id="a9cbd-137">This folder lives in the execution environment that you choose to run the script, and not in your local project folder.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-137">This folder lives in the execution environment that you choose to run the script, and not in your local project folder.</span></span> 
   
   <span data-ttu-id="a9cbd-138">a.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-138">a.</span></span> <span data-ttu-id="a9cbd-139">To locate the file, select the **Runs** button (clock icon) on the left pane to open the list of **All Runs**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-139">To locate the file, select the **Runs** button (clock icon) on the left pane to open the list of **All Runs**.</span></span> 

   <span data-ttu-id="a9cbd-140">b.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-140">b.</span></span> <span data-ttu-id="a9cbd-141">The **All Runs** tab opens.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-141">The **All Runs** tab opens.</span></span> <span data-ttu-id="a9cbd-142">In the table of runs, select one of the recent runs where the target was **local** and the script name was **iris_sklearn.py**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-142">In the table of runs, select one of the recent runs where the target was **local** and the script name was **iris_sklearn.py**.</span></span> 

   <span data-ttu-id="a9cbd-143">c.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-143">c.</span></span> <span data-ttu-id="a9cbd-144">The **Run Properties** pane opens.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-144">The **Run Properties** pane opens.</span></span> <span data-ttu-id="a9cbd-145">In the upper-right section of the pane, notice the **Outputs** section.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-145">In the upper-right section of the pane, notice the **Outputs** section.</span></span>

   <span data-ttu-id="a9cbd-146">d.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-146">d.</span></span> <span data-ttu-id="a9cbd-147">To download the pickle file, select the check box next to the **model.pkl** file, and then select **Download**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-147">To download the pickle file, select the check box next to the **model.pkl** file, and then select **Download**.</span></span> <span data-ttu-id="a9cbd-148">Save the file to the root of your project folder.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-148">Save the file to the root of your project folder.</span></span> <span data-ttu-id="a9cbd-149">The file is needed in the upcoming steps.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-149">The file is needed in the upcoming steps.</span></span>

   ![Download the pickle file](media/tutorial-classifying-iris/download_model.png)

   <span data-ttu-id="a9cbd-151">Read more about the `outputs` folder in [How to read and write large data files](how-to-read-write-files.md).</span><span class="sxs-lookup"><span data-stu-id="a9cbd-151">Read more about the `outputs` folder in [How to read and write large data files](how-to-read-write-files.md).</span></span>

## <a name="get-the-scoring-script-and-schema-files"></a><span data-ttu-id="a9cbd-152">Get the scoring script and schema files</span><span class="sxs-lookup"><span data-stu-id="a9cbd-152">Get the scoring script and schema files</span></span>
<span data-ttu-id="a9cbd-153">To deploy the web service along with the model file, you also need a scoring script.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-153">To deploy the web service along with the model file, you also need a scoring script.</span></span> <span data-ttu-id="a9cbd-154">Optionally, you need a schema for the web service input data.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-154">Optionally, you need a schema for the web service input data.</span></span> <span data-ttu-id="a9cbd-155">The scoring script loads the **model.pkl** file from the current folder and uses it to produce new predictions.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-155">The scoring script loads the **model.pkl** file from the current folder and uses it to produce new predictions.</span></span>

1. <span data-ttu-id="a9cbd-156">Open the Machine Learning Workbench application.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-156">Open the Machine Learning Workbench application.</span></span> <span data-ttu-id="a9cbd-157">Then open the **myIris** project you created in the previous part of the tutorial series.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-157">Then open the **myIris** project you created in the previous part of the tutorial series.</span></span>

1. <span data-ttu-id="a9cbd-158">After the project is open, select the **Files** button (folder icon) on the left pane to open the file list in your project folder.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-158">After the project is open, select the **Files** button (folder icon) on the left pane to open the file list in your project folder.</span></span>

1. <span data-ttu-id="a9cbd-159">Select the **score_iris.py** file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-159">Select the **score_iris.py** file.</span></span> <span data-ttu-id="a9cbd-160">The Python script opens.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-160">The Python script opens.</span></span> <span data-ttu-id="a9cbd-161">This file is used as the scoring file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-161">This file is used as the scoring file.</span></span>

   ![Scoring file](media/tutorial-classifying-iris/model_data_collection.png)

1. <span data-ttu-id="a9cbd-163">To get the schema file, run the script.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-163">To get the schema file, run the script.</span></span> <span data-ttu-id="a9cbd-164">Select the **local** environment and the **score_iris.py** script in the command bar, and then select **Run**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-164">Select the **local** environment and the **score_iris.py** script in the command bar, and then select **Run**.</span></span> 

   <span data-ttu-id="a9cbd-165">This script creates a JSON file in the **Outputs** section, which captures the input data schema required by the model.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-165">This script creates a JSON file in the **Outputs** section, which captures the input data schema required by the model.</span></span>

1. <span data-ttu-id="a9cbd-166">Note the **Jobs** pane on the right side of the **Project Dashboard** pane.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-166">Note the **Jobs** pane on the right side of the **Project Dashboard** pane.</span></span> <span data-ttu-id="a9cbd-167">Wait for the latest **score_iris.py** job to display the green **Completed** status.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-167">Wait for the latest **score_iris.py** job to display the green **Completed** status.</span></span> <span data-ttu-id="a9cbd-168">Then select the hyperlink **score_iris.py** for the latest job run to see the run details.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-168">Then select the hyperlink **score_iris.py** for the latest job run to see the run details.</span></span> 

1. <span data-ttu-id="a9cbd-169">On the **Run Properties** pane, in the **Outputs** section, select the newly created **service_schema.json** file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-169">On the **Run Properties** pane, in the **Outputs** section, select the newly created **service_schema.json** file.</span></span> <span data-ttu-id="a9cbd-170">Select the check box next to the file name, and then select **Download**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-170">Select the check box next to the file name, and then select **Download**.</span></span> <span data-ttu-id="a9cbd-171">Save the file into your project root folder.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-171">Save the file into your project root folder.</span></span>

1. <span data-ttu-id="a9cbd-172">Return to the previous tab where you opened the **score_iris.py** script.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-172">Return to the previous tab where you opened the **score_iris.py** script.</span></span> <span data-ttu-id="a9cbd-173">By using data collection, you can capture model inputs and predictions from the web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-173">By using data collection, you can capture model inputs and predictions from the web service.</span></span> <span data-ttu-id="a9cbd-174">The following steps are of particular interest for data collection.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-174">The following steps are of particular interest for data collection.</span></span>

1. <span data-ttu-id="a9cbd-175">Review the code at the top of the file, which imports class **ModelDataCollector**, because it contains the model data collection functionality:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-175">Review the code at the top of the file, which imports class **ModelDataCollector**, because it contains the model data collection functionality:</span></span>

   ```python
   from azureml.datacollector import ModelDataCollector
   ```

1. <span data-ttu-id="a9cbd-176">Review the following lines of code in the **init()** function that instantiates **ModelDataCollector**:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-176">Review the following lines of code in the **init()** function that instantiates **ModelDataCollector**:</span></span>

    ```python
    global inputs_dc, prediction_dc
    inputs_dc = ModelDataCollector('model.pkl',identifier="inputs")
    prediction_dc = ModelDataCollector('model.pkl', identifier="prediction")`
    ```

1. <span data-ttu-id="a9cbd-177">Review the following lines of code in the **run(input_df)** function as it collects the input and prediction data:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-177">Review the following lines of code in the **run(input_df)** function as it collects the input and prediction data:</span></span>

    ```python
    inputs_dc.collect(input_df)
    prediction_dc.collect(pred)
    ```

<span data-ttu-id="a9cbd-178">Now you're ready to prepare your environment to operationalize the model.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-178">Now you're ready to prepare your environment to operationalize the model.</span></span>

## <a name="prepare-to-operationalize-locally-for-development-and-testing-your-service"></a><span data-ttu-id="a9cbd-179">Prepare to operationalize locally [For development and testing your service]</span><span class="sxs-lookup"><span data-stu-id="a9cbd-179">Prepare to operationalize locally [For development and testing your service]</span></span>
<span data-ttu-id="a9cbd-180">Use _local mode_ deployment to run in Docker containers on your local computer.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-180">Use _local mode_ deployment to run in Docker containers on your local computer.</span></span>

<span data-ttu-id="a9cbd-181">You can use _local mode_ for development and testing.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-181">You can use _local mode_ for development and testing.</span></span> <span data-ttu-id="a9cbd-182">The Docker engine must be running locally to complete the following steps to operationalize the model.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-182">The Docker engine must be running locally to complete the following steps to operationalize the model.</span></span> <span data-ttu-id="a9cbd-183">You can use the `-h` flag at the end of each command to show the corresponding help message.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-183">You can use the `-h` flag at the end of each command to show the corresponding help message.</span></span>

>[!NOTE]
><span data-ttu-id="a9cbd-184">If you don't have the Docker engine locally, you can still proceed by creating a cluster in Azure for deployment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-184">If you don't have the Docker engine locally, you can still proceed by creating a cluster in Azure for deployment.</span></span> <span data-ttu-id="a9cbd-185">You can keep the cluster for re-use, or delete it after the tutorial so you don't incur ongoing charges.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-185">You can keep the cluster for re-use, or delete it after the tutorial so you don't incur ongoing charges.</span></span>

>[!NOTE]
><span data-ttu-id="a9cbd-186">Web services deployed locally do not show up in Azure Portal's list of services.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-186">Web services deployed locally do not show up in Azure Portal's list of services.</span></span> <span data-ttu-id="a9cbd-187">They will be running in Docker on the local machine.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-187">They will be running in Docker on the local machine.</span></span>

1. <span data-ttu-id="a9cbd-188">Open the command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="a9cbd-188">Open the command-line interface (CLI).</span></span>
   <span data-ttu-id="a9cbd-189">In the Machine Learning Workbench application, on the **File** menu, select **Open Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-189">In the Machine Learning Workbench application, on the **File** menu, select **Open Command Prompt**.</span></span>

   <span data-ttu-id="a9cbd-190">The command-line prompt opens in your current project folder location **c:\temp\myIris>**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-190">The command-line prompt opens in your current project folder location **c:\temp\myIris>**.</span></span>


1. <span data-ttu-id="a9cbd-191">Make sure the Azure resource provider **Microsoft.ContainerRegistry** is registered in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-191">Make sure the Azure resource provider **Microsoft.ContainerRegistry** is registered in your subscription.</span></span> <span data-ttu-id="a9cbd-192">You must register this resource provider before you can create      an environment in step 3.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-192">You must register this resource provider before you can create      an environment in step 3.</span></span> <span data-ttu-id="a9cbd-193">You can check to see if it's already registered by using the following command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-193">You can check to see if it's already registered by using the following command:</span></span>
   ``` 
   az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table 
   ``` 

   <span data-ttu-id="a9cbd-194">You should see output like this:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-194">You should see output like this:</span></span> 
   ```
   Provider                                  Status 
   --------                                  ------
   Microsoft.Authorization                   Registered 
   Microsoft.ContainerRegistry               Registered 
   microsoft.insights                        Registered 
   Microsoft.MachineLearningExperimentation  Registered 
   ... 
   ```
   
   <span data-ttu-id="a9cbd-195">If **Microsoft.ContainerRegistry** is not registered, you can register it by using the following command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-195">If **Microsoft.ContainerRegistry** is not registered, you can register it by using the following command:</span></span>
   ``` 
   az provider register --namespace Microsoft.ContainerRegistry 
   ```
   <span data-ttu-id="a9cbd-196">Registration can take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-196">Registration can take a few minutes.</span></span> <span data-ttu-id="a9cbd-197">You can check on its status by using the previous **az provider list** command or the following command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-197">You can check on its status by using the previous **az provider list** command or the following command:</span></span>
   ``` 
   az provider show -n Microsoft.ContainerRegistry 
   ``` 

   <span data-ttu-id="a9cbd-198">The third line of the output displays **"registrationState": "Registering"**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-198">The third line of the output displays **"registrationState": "Registering"**.</span></span> <span data-ttu-id="a9cbd-199">Wait a few moments and repeat the **show** command until the output displays **"registrationState": "Registered"**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-199">Wait a few moments and repeat the **show** command until the output displays **"registrationState": "Registered"**.</span></span>

   >[!NOTE] 
   <span data-ttu-id="a9cbd-200">If you are deploying to an ACS cluster, you need register the **Microsoft.ContainerService** resource provider as well using the exact same approach.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-200">If you are deploying to an ACS cluster, you need register the **Microsoft.ContainerService** resource provider as well using the exact same approach.</span></span>

1. <span data-ttu-id="a9cbd-201">Create the environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-201">Create the environment.</span></span> <span data-ttu-id="a9cbd-202">You must run this step once per environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-202">You must run this step once per environment.</span></span> <span data-ttu-id="a9cbd-203">For example, run it once for development environment, and once for production.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-203">For example, run it once for development environment, and once for production.</span></span> <span data-ttu-id="a9cbd-204">Use _local mode_ for this first environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-204">Use _local mode_ for this first environment.</span></span> <span data-ttu-id="a9cbd-205">You can try the `-c` or `--cluster` switch in the following command to set up an environment in _cluster mode_ later.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-205">You can try the `-c` or `--cluster` switch in the following command to set up an environment in _cluster mode_ later.</span></span>

   <span data-ttu-id="a9cbd-206">The following setup command requires you to have Contributor access to the subscription.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-206">The following setup command requires you to have Contributor access to the subscription.</span></span> <span data-ttu-id="a9cbd-207">If you don't have that, you need at least Contributor access to the resource group that you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-207">If you don't have that, you need at least Contributor access to the resource group that you are deploying to.</span></span> <span data-ttu-id="a9cbd-208">In the latter case, you need to specify the resource group name as part of the setup command by using the `-g` flag.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-208">In the latter case, you need to specify the resource group name as part of the setup command by using the `-g` flag.</span></span> 

   ```azurecli
   az ml env setup -n <new deployment environment name> --location <e.g. eastus2>
   ```
   
   <span data-ttu-id="a9cbd-209">Follow the on-screen instructions to provision a storage account for storing Docker images, an Azure container registry that lists the Docker images, and an Azure Application Insights account that gathers telemetry.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-209">Follow the on-screen instructions to provision a storage account for storing Docker images, an Azure container registry that lists the Docker images, and an Azure Application Insights account that gathers telemetry.</span></span> <span data-ttu-id="a9cbd-210">If you use the `-c` switch, the command will additionally create a Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-210">If you use the `-c` switch, the command will additionally create a Container Service cluster.</span></span>
   
   <span data-ttu-id="a9cbd-211">The cluster name is a way for you to identify the environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-211">The cluster name is a way for you to identify the environment.</span></span> <span data-ttu-id="a9cbd-212">The location should be the same as the location of the Model Management account you created from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-212">The location should be the same as the location of the Model Management account you created from the Azure portal.</span></span>

   <span data-ttu-id="a9cbd-213">To make sure that the environment is set up successfully, use the following command to check the status:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-213">To make sure that the environment is set up successfully, use the following command to check the status:</span></span>

   ```azurecli
   az ml env show -n <deployment environment name> -g <existing resource group name>
   ```

   <span data-ttu-id="a9cbd-214">Make sure that "Provisioning State" has the value "Succeeded", as shown, before you set the environment in step 5:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-214">Make sure that "Provisioning State" has the value "Succeeded", as shown, before you set the environment in step 5:</span></span>

   ![Provisioning State](media/tutorial-classifying-iris/provisioning_state.png)
 
1. <span data-ttu-id="a9cbd-216">If you didn't create a Model Management account in previous parts of this tutorial, do so now.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-216">If you didn't create a Model Management account in previous parts of this tutorial, do so now.</span></span> <span data-ttu-id="a9cbd-217">This is a one-time setup.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-217">This is a one-time setup.</span></span>
   ```azurecli
   az ml account modelmanagement create --location <e.g. eastus2> -n <new model management account name> -g <existing resource group name> --sku-name S1
   ```
   
1. <span data-ttu-id="a9cbd-218">Set the Model Management account.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-218">Set the Model Management account.</span></span>
   ```azurecli
   az ml account modelmanagement set -n <youracctname> -g <yourresourcegroupname>
   ```

1. <span data-ttu-id="a9cbd-219">Set the environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-219">Set the environment.</span></span>

   <span data-ttu-id="a9cbd-220">After the setup finishes, use the following command to set the environment variables required to operationalize the environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-220">After the setup finishes, use the following command to set the environment variables required to operationalize the environment.</span></span> <span data-ttu-id="a9cbd-221">Use the same environment name that you used previously in step 3.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-221">Use the same environment name that you used previously in step 3.</span></span> <span data-ttu-id="a9cbd-222">Use the same resource group name that was output in the command window when the setup process finished.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-222">Use the same resource group name that was output in the command window when the setup process finished.</span></span>

   ```azurecli
   az ml env set -n <deployment environment name> -g <existing resource group name>
   ```

1. <span data-ttu-id="a9cbd-223">To verify that you have properly configured your operationalized environment for local web service deployment, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-223">To verify that you have properly configured your operationalized environment for local web service deployment, enter the following command:</span></span>

   ```azurecli
   az ml env show
   ```

<span data-ttu-id="a9cbd-224">Now you're ready to create the real-time web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-224">Now you're ready to create the real-time web service.</span></span>

>[!NOTE]
><span data-ttu-id="a9cbd-225">You can reuse your Model Management account and environment for subsequent web service deployments.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-225">You can reuse your Model Management account and environment for subsequent web service deployments.</span></span> <span data-ttu-id="a9cbd-226">You don't need to create them for each web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-226">You don't need to create them for each web service.</span></span> <span data-ttu-id="a9cbd-227">An account or an environment can have multiple web services associated with it.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-227">An account or an environment can have multiple web services associated with it.</span></span>

## <a name="create-a-real-time-web-service-in-one-command"></a><span data-ttu-id="a9cbd-228">Create a real-time web service in one command</span><span class="sxs-lookup"><span data-stu-id="a9cbd-228">Create a real-time web service in one command</span></span>
1. <span data-ttu-id="a9cbd-229">To create a real-time web service, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-229">To create a real-time web service, use the following command:</span></span>

   ```azurecli
   az ml service create realtime -f score_iris.py --model-file model.pkl -s service_schema.json -n irisapp -r python --collect-model-data true -c aml_config\conda_dependencies.yml
   ```
   <span data-ttu-id="a9cbd-230">This command generates a web service ID you can use later.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-230">This command generates a web service ID you can use later.</span></span>

   <span data-ttu-id="a9cbd-231">The following switches are used with the **az ml service create realtime** command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-231">The following switches are used with the **az ml service create realtime** command:</span></span>

   * <span data-ttu-id="a9cbd-232">`-f`: The scoring script file name.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-232">`-f`: The scoring script file name.</span></span>

   * <span data-ttu-id="a9cbd-233">`--model-file`: The model file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-233">`--model-file`: The model file.</span></span> <span data-ttu-id="a9cbd-234">In this case, it's the pickled model.pkl file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-234">In this case, it's the pickled model.pkl file.</span></span>

   * <span data-ttu-id="a9cbd-235">`-s`: The service schema.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-235">`-s`: The service schema.</span></span> <span data-ttu-id="a9cbd-236">This was generated in a previous step by running the **score_iris.py** script locally.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-236">This was generated in a previous step by running the **score_iris.py** script locally.</span></span>

   * <span data-ttu-id="a9cbd-237">`-n`: The app name, which must be all lowercase.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-237">`-n`: The app name, which must be all lowercase.</span></span>

   * <span data-ttu-id="a9cbd-238">`-r`: The runtime of the model.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-238">`-r`: The runtime of the model.</span></span> <span data-ttu-id="a9cbd-239">In this case, it's a Python model.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-239">In this case, it's a Python model.</span></span> <span data-ttu-id="a9cbd-240">Valid runtimes are `python` and `spark-py`.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-240">Valid runtimes are `python` and `spark-py`.</span></span>

   * <span data-ttu-id="a9cbd-241">`--collect-model-data true`: This switch enables data collection.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-241">`--collect-model-data true`: This switch enables data collection.</span></span>

   * <span data-ttu-id="a9cbd-242">`-c`: Path to the conda dependencies file where additional packages are specified.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-242">`-c`: Path to the conda dependencies file where additional packages are specified.</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="a9cbd-243">The service name, which is also the new Docker image name, must be all lowercase.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-243">The service name, which is also the new Docker image name, must be all lowercase.</span></span> <span data-ttu-id="a9cbd-244">Otherwise, you get an error.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-244">Otherwise, you get an error.</span></span> 

1. <span data-ttu-id="a9cbd-245">When you run the command, the model and the scoring files are uploaded to the storage account you created as part of the environment setup.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-245">When you run the command, the model and the scoring files are uploaded to the storage account you created as part of the environment setup.</span></span> <span data-ttu-id="a9cbd-246">The deployment process builds a Docker image with your model, schema, and scoring file in it, and then pushes it to the Azure container registry: **\<ACR_name\>.azurecr.io/\<imagename\>:\<version\>**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-246">The deployment process builds a Docker image with your model, schema, and scoring file in it, and then pushes it to the Azure container registry: **\<ACR_name\>.azurecr.io/\<imagename\>:\<version\>**.</span></span> 

   <span data-ttu-id="a9cbd-247">The command pulls down the image locally to your computer and then starts a Docker container based on that image.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-247">The command pulls down the image locally to your computer and then starts a Docker container based on that image.</span></span> <span data-ttu-id="a9cbd-248">If your environment is configured in cluster mode, the Docker container is deployed into the Azure Cloud Services Kubernetes cluster instead.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-248">If your environment is configured in cluster mode, the Docker container is deployed into the Azure Cloud Services Kubernetes cluster instead.</span></span>

   <span data-ttu-id="a9cbd-249">As part of the deployment, an HTTP REST endpoint for the web service is created on your local machine.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-249">As part of the deployment, an HTTP REST endpoint for the web service is created on your local machine.</span></span> <span data-ttu-id="a9cbd-250">After a few minutes, the command should finish with a success message.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-250">After a few minutes, the command should finish with a success message.</span></span> <span data-ttu-id="a9cbd-251">Your web service is ready for action!</span><span class="sxs-lookup"><span data-stu-id="a9cbd-251">Your web service is ready for action!</span></span>

1. <span data-ttu-id="a9cbd-252">To see the running Docker container, use the **docker ps** command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-252">To see the running Docker container, use the **docker ps** command:</span></span>

   ```azurecli
   docker ps
   ```

## <a name="optional-alternative-create-a-real-time-web-service-by-using-separate-commands"></a><span data-ttu-id="a9cbd-253">[Optional alternative] Create a real-time web service by using separate commands</span><span class="sxs-lookup"><span data-stu-id="a9cbd-253">[Optional alternative] Create a real-time web service by using separate commands</span></span>
<span data-ttu-id="a9cbd-254">As an alternative to the **az ml service create realtime** command shown previously, you also can perform the steps separately.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-254">As an alternative to the **az ml service create realtime** command shown previously, you also can perform the steps separately.</span></span> 

<span data-ttu-id="a9cbd-255">First, register the model.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-255">First, register the model.</span></span> <span data-ttu-id="a9cbd-256">Then generate the manifest, build the Docker image, and create the web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-256">Then generate the manifest, build the Docker image, and create the web service.</span></span> <span data-ttu-id="a9cbd-257">This step-by-step approach gives you more flexibility at each step.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-257">This step-by-step approach gives you more flexibility at each step.</span></span> <span data-ttu-id="a9cbd-258">Additionally, you can reuse the entities generated in previous steps and rebuild the entities only when needed.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-258">Additionally, you can reuse the entities generated in previous steps and rebuild the entities only when needed.</span></span>

1. <span data-ttu-id="a9cbd-259">Register the model by providing the pickle file name.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-259">Register the model by providing the pickle file name.</span></span>

   ```azurecli
   az ml model register --model model.pkl --name model.pkl
   ```
   <span data-ttu-id="a9cbd-260">This command generates a model ID.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-260">This command generates a model ID.</span></span>

1. <span data-ttu-id="a9cbd-261">Create a manifest.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-261">Create a manifest.</span></span>

   <span data-ttu-id="a9cbd-262">To create a manifest, use the following command and provide the model ID output from the previous step:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-262">To create a manifest, use the following command and provide the model ID output from the previous step:</span></span>

   ```azurecli
   az ml manifest create --manifest-name <new manifest name> -f score_iris.py -r python -i <model ID> -s service_schema.json -c aml_config\conda_dependencies.yml
   ```
   <span data-ttu-id="a9cbd-263">This command generates a manifest ID.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-263">This command generates a manifest ID.</span></span>

1. <span data-ttu-id="a9cbd-264">Create a Docker image.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-264">Create a Docker image.</span></span>

   <span data-ttu-id="a9cbd-265">To create a Docker image, use the following command and provide the manifest ID value output from the previous step.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-265">To create a Docker image, use the following command and provide the manifest ID value output from the previous step.</span></span> <span data-ttu-id="a9cbd-266">You also can optionally include the conda dependencies by using the `-c` switch.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-266">You also can optionally include the conda dependencies by using the `-c` switch.</span></span>

   ```azurecli
   az ml image create -n irisimage --manifest-id <manifest ID> 
   ```
   <span data-ttu-id="a9cbd-267">This command generates a Docker image ID.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-267">This command generates a Docker image ID.</span></span>
   
1. <span data-ttu-id="a9cbd-268">Create the service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-268">Create the service.</span></span>

   <span data-ttu-id="a9cbd-269">To create a service, use the following command and provide the image ID output from the previous step:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-269">To create a service, use the following command and provide the image ID output from the previous step:</span></span>

   ```azurecli
   az ml service create realtime --image-id <image ID> -n irisapp --collect-model-data true
   ```
   <span data-ttu-id="a9cbd-270">This command generates a web service ID.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-270">This command generates a web service ID.</span></span>

<span data-ttu-id="a9cbd-271">You are now ready to run the web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-271">You are now ready to run the web service.</span></span>

## <a name="run-the-real-time-web-service"></a><span data-ttu-id="a9cbd-272">Run the real-time web service</span><span class="sxs-lookup"><span data-stu-id="a9cbd-272">Run the real-time web service</span></span>

<span data-ttu-id="a9cbd-273">To test the **irisapp** web service that's running, use a JSON-encoded record containing an array of four random numbers.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-273">To test the **irisapp** web service that's running, use a JSON-encoded record containing an array of four random numbers.</span></span>

1. <span data-ttu-id="a9cbd-274">The web service includes sample data.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-274">The web service includes sample data.</span></span> <span data-ttu-id="a9cbd-275">When running in local mode, you can call the **az ml service usage realtime** command.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-275">When running in local mode, you can call the **az ml service usage realtime** command.</span></span> <span data-ttu-id="a9cbd-276">That call retrieves a sample run command that you can use to test the service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-276">That call retrieves a sample run command that you can use to test the service.</span></span> <span data-ttu-id="a9cbd-277">The call also retrieves the scoring URL that you can use to incorporate the service into your own custom app.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-277">The call also retrieves the scoring URL that you can use to incorporate the service into your own custom app.</span></span>

   ```azurecli
   az ml service usage realtime -i <web service ID>
   ```

1. <span data-ttu-id="a9cbd-278">To test the service, execute the returned service run command:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-278">To test the service, execute the returned service run command:</span></span>
    
   ```azurecli
   az ml service run realtime -i <web service ID> -d '{\"input_df\": [{\"petal width\": 0.25, \"sepal length\": 3.0, \"sepal width\": 3.6, \"petal length\": 1.3}]}'
   ```

   <span data-ttu-id="a9cbd-279">The output is **"Iris-setosa"**, which is the predicted class.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-279">The output is **"Iris-setosa"**, which is the predicted class.</span></span> <span data-ttu-id="a9cbd-280">(Your result might be different.)</span><span class="sxs-lookup"><span data-stu-id="a9cbd-280">(Your result might be different.)</span></span> 

## <a name="view-the-collected-data-in-azure-blob-storage"></a><span data-ttu-id="a9cbd-281">View the collected data in Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="a9cbd-281">View the collected data in Azure Blob storage</span></span>

1. <span data-ttu-id="a9cbd-282">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9cbd-282">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="a9cbd-283">Locate your storage accounts.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-283">Locate your storage accounts.</span></span> <span data-ttu-id="a9cbd-284">To do so, select **All Services**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-284">To do so, select **All Services**.</span></span>

1. <span data-ttu-id="a9cbd-285">In the search box, enter **Storage accounts**, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-285">In the search box, enter **Storage accounts**, and then select Enter.</span></span>

1. <span data-ttu-id="a9cbd-286">From the **Storage accounts** search box, select the **Storage account** resource matching your environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-286">From the **Storage accounts** search box, select the **Storage account** resource matching your environment.</span></span> 

   > [!TIP]
   > <span data-ttu-id="a9cbd-287">To determine which storage account is in use:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-287">To determine which storage account is in use:</span></span>
   > 1. <span data-ttu-id="a9cbd-288">Open Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-288">Open Machine Learning Workbench.</span></span>
   > 1. <span data-ttu-id="a9cbd-289">Select the project you're working on.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-289">Select the project you're working on.</span></span>
   > 1. <span data-ttu-id="a9cbd-290">Open a command line prompt from the **File** menu.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-290">Open a command line prompt from the **File** menu.</span></span>
   > 1. <span data-ttu-id="a9cbd-291">At the command line prompt, enter `az ml env show -v`, and check the *storage_account* value.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-291">At the command line prompt, enter `az ml env show -v`, and check the *storage_account* value.</span></span> <span data-ttu-id="a9cbd-292">This is the name of your storage account.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-292">This is the name of your storage account.</span></span>

1. <span data-ttu-id="a9cbd-293">After the **Storage account** pane opens, select **Blobs** from the **Services** section.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-293">After the **Storage account** pane opens, select **Blobs** from the **Services** section.</span></span> <span data-ttu-id="a9cbd-294">Locate the container named **modeldata**.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-294">Locate the container named **modeldata**.</span></span> 
 
   <span data-ttu-id="a9cbd-295">If you don't see any data, you might need to wait up to 10 minutes after the first web-service request to see the data propagate to the storage account.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-295">If you don't see any data, you might need to wait up to 10 minutes after the first web-service request to see the data propagate to the storage account.</span></span>

   <span data-ttu-id="a9cbd-296">Data flows into blobs with the following container path:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-296">Data flows into blobs with the following container path:</span></span>

   ```
   /modeldata/<subscription_id>/<resource_group_name>/<model_management_account_name>/<webservice_name>/<model_id>-<model_name>-<model_version>/<identifier>/<year>/<month>/<day>/data.csv
   ```

1. <span data-ttu-id="a9cbd-297">You can consume this data from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-297">You can consume this data from Azure Blob storage.</span></span> <span data-ttu-id="a9cbd-298">There are a variety of tools that use both Microsoft software and open-source tools, such as:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-298">There are a variety of tools that use both Microsoft software and open-source tools, such as:</span></span>

   * <span data-ttu-id="a9cbd-299">Machine Learning: Open the CSV file by adding the CSV file as a data source.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-299">Machine Learning: Open the CSV file by adding the CSV file as a data source.</span></span>

   * <span data-ttu-id="a9cbd-300">Excel: Open the daily CSV files as a spreadsheet.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-300">Excel: Open the daily CSV files as a spreadsheet.</span></span>

   * <span data-ttu-id="a9cbd-301">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/): Create charts with data pulled from the CSV data in blobs.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-301">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/): Create charts with data pulled from the CSV data in blobs.</span></span>

   * <span data-ttu-id="a9cbd-302">[Hive](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-tutorial-get-started): Load the CSV data into a Hive table, and perform SQL queries directly against the blobs.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-302">[Hive](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-tutorial-get-started): Load the CSV data into a Hive table, and perform SQL queries directly against the blobs.</span></span>

   * <span data-ttu-id="a9cbd-303">[Spark](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-overview): Create a DataFrame with a large portion of CSV data.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-303">[Spark](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-overview): Create a DataFrame with a large portion of CSV data.</span></span>

      ```python
      var df = spark.read.format("com.databricks.spark.csv").option("inferSchema","true").option("header","true").load("wasb://modeldata@<storageaccount>.blob.core.windows.net/<subscription_id>/<resource_group_name>/<model_management_account_name>/<webservice_name>/<model_id>-<model_name>-<model_version>/<identifier>/<year>/<month>/<date>/*")
      ```

## <a name="clean-up-resources"></a><span data-ttu-id="a9cbd-304">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a9cbd-304">Clean up resources</span></span>

[!INCLUDE [aml-delete-resource-group](../../../includes/aml-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="a9cbd-305">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9cbd-305">Next steps</span></span>
<span data-ttu-id="a9cbd-306">In this third part of the three-part tutorial series, you have learned how to use Machine Learning to:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-306">In this third part of the three-part tutorial series, you have learned how to use Machine Learning to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a9cbd-307">Locate the model file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-307">Locate the model file.</span></span>
> * <span data-ttu-id="a9cbd-308">Generate a scoring script and schema file.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-308">Generate a scoring script and schema file.</span></span>
> * <span data-ttu-id="a9cbd-309">Prepare the environment.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-309">Prepare the environment.</span></span>
> * <span data-ttu-id="a9cbd-310">Create a real-time web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-310">Create a real-time web service.</span></span>
> * <span data-ttu-id="a9cbd-311">Run the real-time web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-311">Run the real-time web service.</span></span>
> * <span data-ttu-id="a9cbd-312">Examine the output blob data.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-312">Examine the output blob data.</span></span> 

<span data-ttu-id="a9cbd-313">You have successfully run a training script in various compute environments.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-313">You have successfully run a training script in various compute environments.</span></span> <span data-ttu-id="a9cbd-314">You have also created, serialized, and operationalized a model through a Docker-based web service.</span><span class="sxs-lookup"><span data-stu-id="a9cbd-314">You have also created, serialized, and operationalized a model through a Docker-based web service.</span></span> 

<span data-ttu-id="a9cbd-315">You are now ready to do advanced data preparation:</span><span class="sxs-lookup"><span data-stu-id="a9cbd-315">You are now ready to do advanced data preparation:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a9cbd-316">Tutorial 4 - Advanced data preparation</span><span class="sxs-lookup"><span data-stu-id="a9cbd-316">Tutorial 4 - Advanced data preparation</span></span>](tutorial-bikeshare-dataprep.md)
