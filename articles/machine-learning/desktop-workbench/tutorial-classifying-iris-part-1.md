---
title: Prepare data for classifying Iris tutorial in Azure Machine Learning services (preview) | Microsoft Docs
description: This full-length tutorial shows how to use Azure Machine Learning services (preview) end to end. This is part one and discusses data preparation.
services: machine-learning
author: hning86
ms.author: haining
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs, gcampanella
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: tutorial
ms.date: 3/7/2018
ms.openlocfilehash: 066c3c973f67a0ba272224a9c5843824f5ed492d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867335"
---
# <a name="tutorial-1-classify-iris---preparing-the-data"></a><span data-ttu-id="03b94-104">Tutorial 1: Classify Iris - Preparing the data</span><span class="sxs-lookup"><span data-stu-id="03b94-104">Tutorial 1: Classify Iris - Preparing the data</span></span>

<span data-ttu-id="03b94-105">Azure Machine Learning service (preview) is an integrated, end-to-end data science and advanced analytics solution for professional data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="03b94-105">Azure Machine Learning service (preview) is an integrated, end-to-end data science and advanced analytics solution for professional data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span></span>

<span data-ttu-id="03b94-106">This tutorial is **part one of a three-part series**.</span><span class="sxs-lookup"><span data-stu-id="03b94-106">This tutorial is **part one of a three-part series**.</span></span> <span data-ttu-id="03b94-107">In this tutorial, you walk through the basics of Azure Machine Learning services (preview) and learn how to:</span><span class="sxs-lookup"><span data-stu-id="03b94-107">In this tutorial, you walk through the basics of Azure Machine Learning services (preview) and learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="03b94-108">Create a project in Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="03b94-108">Create a project in Azure Machine Learning Workbench</span></span>
> * <span data-ttu-id="03b94-109">Create a data preparation package</span><span class="sxs-lookup"><span data-stu-id="03b94-109">Create a data preparation package</span></span>
> * <span data-ttu-id="03b94-110">Generate Python/PySpark code to invoke a data preparation package</span><span class="sxs-lookup"><span data-stu-id="03b94-110">Generate Python/PySpark code to invoke a data preparation package</span></span>

<span data-ttu-id="03b94-111">This tutorial uses the timeless [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span><span class="sxs-lookup"><span data-stu-id="03b94-111">This tutorial uses the timeless [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="03b94-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="03b94-112">Prerequisites</span></span>

<span data-ttu-id="03b94-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="03b94-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="03b94-114">To complete this tutorial, you must have:</span><span class="sxs-lookup"><span data-stu-id="03b94-114">To complete this tutorial, you must have:</span></span>
- <span data-ttu-id="03b94-115">An Azure Machine Learning Experimentation account</span><span class="sxs-lookup"><span data-stu-id="03b94-115">An Azure Machine Learning Experimentation account</span></span>
- <span data-ttu-id="03b94-116">Azure Machine Learning Workbench installed</span><span class="sxs-lookup"><span data-stu-id="03b94-116">Azure Machine Learning Workbench installed</span></span>

<span data-ttu-id="03b94-117">If you don't have these prerequisites already, follow the steps in the [Quickstart: Install and start](../service/quickstart-installation.md) article to set up your accounts and install the Azure Machine Learning Workbench application.</span><span class="sxs-lookup"><span data-stu-id="03b94-117">If you don't have these prerequisites already, follow the steps in the [Quickstart: Install and start](../service/quickstart-installation.md) article to set up your accounts and install the Azure Machine Learning Workbench application.</span></span> 

## <a name="create-a-new-project-in-workbench"></a><span data-ttu-id="03b94-118">Create a new project in Workbench</span><span class="sxs-lookup"><span data-stu-id="03b94-118">Create a new project in Workbench</span></span>

<span data-ttu-id="03b94-119">If you followed the steps in the [Quickstart: Install and start](../service/quickstart-installation.md) article you should already have this project and can skip to the next section.</span><span class="sxs-lookup"><span data-stu-id="03b94-119">If you followed the steps in the [Quickstart: Install and start](../service/quickstart-installation.md) article you should already have this project and can skip to the next section.</span></span>

1. <span data-ttu-id="03b94-120">Open the Azure Machine Learning Workbench app, and log in if needed.</span><span class="sxs-lookup"><span data-stu-id="03b94-120">Open the Azure Machine Learning Workbench app, and log in if needed.</span></span> 
   
   + <span data-ttu-id="03b94-121">On Windows, launch it using the **Machine Learning Workbench** desktop shortcut.</span><span class="sxs-lookup"><span data-stu-id="03b94-121">On Windows, launch it using the **Machine Learning Workbench** desktop shortcut.</span></span> 
   + <span data-ttu-id="03b94-122">On macOS, select **Azure ML Workbench** in Launchpad.</span><span class="sxs-lookup"><span data-stu-id="03b94-122">On macOS, select **Azure ML Workbench** in Launchpad.</span></span>

1. <span data-ttu-id="03b94-123">Select the plus sign (+) in the **PROJECTS** pane and choose **New Project**.</span><span class="sxs-lookup"><span data-stu-id="03b94-123">Select the plus sign (+) in the **PROJECTS** pane and choose **New Project**.</span></span>  

   ![New workspace](./media/tutorial-classifying-iris/new_ws.png)

1. <span data-ttu-id="03b94-125">Fill out of the form fields and select the **Create** button to create a new project in the Workbench.</span><span class="sxs-lookup"><span data-stu-id="03b94-125">Fill out of the form fields and select the **Create** button to create a new project in the Workbench.</span></span>

   <span data-ttu-id="03b94-126">Field</span><span class="sxs-lookup"><span data-stu-id="03b94-126">Field</span></span>|<span data-ttu-id="03b94-127">Suggested value for tutorial</span><span class="sxs-lookup"><span data-stu-id="03b94-127">Suggested value for tutorial</span></span>|<span data-ttu-id="03b94-128">Description</span><span class="sxs-lookup"><span data-stu-id="03b94-128">Description</span></span>
   ---|---|---
   <span data-ttu-id="03b94-129">Project name</span><span class="sxs-lookup"><span data-stu-id="03b94-129">Project name</span></span> | <span data-ttu-id="03b94-130">myIris</span><span class="sxs-lookup"><span data-stu-id="03b94-130">myIris</span></span> |<span data-ttu-id="03b94-131">Enter a unique name that identifies your account.</span><span class="sxs-lookup"><span data-stu-id="03b94-131">Enter a unique name that identifies your account.</span></span> <span data-ttu-id="03b94-132">You can use your own name, or a departmental or project name that best identifies the experiment.</span><span class="sxs-lookup"><span data-stu-id="03b94-132">You can use your own name, or a departmental or project name that best identifies the experiment.</span></span> <span data-ttu-id="03b94-133">The name should be 2 to 32 characters.</span><span class="sxs-lookup"><span data-stu-id="03b94-133">The name should be 2 to 32 characters.</span></span> <span data-ttu-id="03b94-134">It should include only alphanumeric characters and the dash (-) character.</span><span class="sxs-lookup"><span data-stu-id="03b94-134">It should include only alphanumeric characters and the dash (-) character.</span></span> 
   <span data-ttu-id="03b94-135">Project directory</span><span class="sxs-lookup"><span data-stu-id="03b94-135">Project directory</span></span> | <span data-ttu-id="03b94-136">c:\Temp\\</span><span class="sxs-lookup"><span data-stu-id="03b94-136">c:\Temp\\</span></span> | <span data-ttu-id="03b94-137">Specify the directory in which the project is created.</span><span class="sxs-lookup"><span data-stu-id="03b94-137">Specify the directory in which the project is created.</span></span>
   <span data-ttu-id="03b94-138">Project description</span><span class="sxs-lookup"><span data-stu-id="03b94-138">Project description</span></span> | <span data-ttu-id="03b94-139">_leave blank_</span><span class="sxs-lookup"><span data-stu-id="03b94-139">_leave blank_</span></span> | <span data-ttu-id="03b94-140">Optional field useful for describing the projects.</span><span class="sxs-lookup"><span data-stu-id="03b94-140">Optional field useful for describing the projects.</span></span>
   <span data-ttu-id="03b94-141">Visualstudio.com GIT Repository URL</span><span class="sxs-lookup"><span data-stu-id="03b94-141">Visualstudio.com GIT Repository URL</span></span> |<span data-ttu-id="03b94-142">_leave blank_</span><span class="sxs-lookup"><span data-stu-id="03b94-142">_leave blank_</span></span> | <span data-ttu-id="03b94-143">Optional field.</span><span class="sxs-lookup"><span data-stu-id="03b94-143">Optional field.</span></span> <span data-ttu-id="03b94-144">You can associate a project with a Git repository on Azure DevOps for source control and collaboration.</span><span class="sxs-lookup"><span data-stu-id="03b94-144">You can associate a project with a Git repository on Azure DevOps for source control and collaboration.</span></span> <span data-ttu-id="03b94-145">[Learn how to set that up](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/using-git-ml-project#step-3-set-up-a-machine-learning-project-and-git-repo).</span><span class="sxs-lookup"><span data-stu-id="03b94-145">[Learn how to set that up](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/using-git-ml-project#step-3-set-up-a-machine-learning-project-and-git-repo).</span></span> 
   <span data-ttu-id="03b94-146">Selected workspace</span><span class="sxs-lookup"><span data-stu-id="03b94-146">Selected workspace</span></span> | <span data-ttu-id="03b94-147">IrisGarden (if it exists)</span><span class="sxs-lookup"><span data-stu-id="03b94-147">IrisGarden (if it exists)</span></span> | <span data-ttu-id="03b94-148">Choose a workspace that you have created for your Experimentation account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="03b94-148">Choose a workspace that you have created for your Experimentation account in the Azure portal.</span></span> <br/><span data-ttu-id="03b94-149">If you followed the Quickstart, you should have a workspace by the name IrisGarden.</span><span class="sxs-lookup"><span data-stu-id="03b94-149">If you followed the Quickstart, you should have a workspace by the name IrisGarden.</span></span> <span data-ttu-id="03b94-150">If not, select the one you created when you created your Experimentation account or any other you want to use.</span><span class="sxs-lookup"><span data-stu-id="03b94-150">If not, select the one you created when you created your Experimentation account or any other you want to use.</span></span>
   <span data-ttu-id="03b94-151">Project template</span><span class="sxs-lookup"><span data-stu-id="03b94-151">Project template</span></span> | <span data-ttu-id="03b94-152">Classifying Iris</span><span class="sxs-lookup"><span data-stu-id="03b94-152">Classifying Iris</span></span> | <span data-ttu-id="03b94-153">Templates contain scripts and data you can use to explore the product.</span><span class="sxs-lookup"><span data-stu-id="03b94-153">Templates contain scripts and data you can use to explore the product.</span></span> <span data-ttu-id="03b94-154">This template contains the scripts and data you need for this quickstart and other tutorials in this documentation site.</span><span class="sxs-lookup"><span data-stu-id="03b94-154">This template contains the scripts and data you need for this quickstart and other tutorials in this documentation site.</span></span> 

   ![New project](media/tutorial-classifying-iris/new_project.png)
 
 <span data-ttu-id="03b94-156">A new project is created and the project dashboard opens with that project.</span><span class="sxs-lookup"><span data-stu-id="03b94-156">A new project is created and the project dashboard opens with that project.</span></span> <span data-ttu-id="03b94-157">At this point, you can explore the project home page, data sources, notebooks, and source code files.</span><span class="sxs-lookup"><span data-stu-id="03b94-157">At this point, you can explore the project home page, data sources, notebooks, and source code files.</span></span> 

   ![Open project](media/tutorial-classifying-iris/project-open.png)
 

## <a name="create-a-data-preparation-package"></a><span data-ttu-id="03b94-159">Create a data preparation package</span><span class="sxs-lookup"><span data-stu-id="03b94-159">Create a data preparation package</span></span>

<span data-ttu-id="03b94-160">Next, you can explore and start preparing the data in Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="03b94-160">Next, you can explore and start preparing the data in Azure Machine Learning Workbench.</span></span> <span data-ttu-id="03b94-161">Each transformation you perform in Workbench is stored in a JSON format in a local data preparation package (\*.dprep file).</span><span class="sxs-lookup"><span data-stu-id="03b94-161">Each transformation you perform in Workbench is stored in a JSON format in a local data preparation package (\*.dprep file).</span></span> <span data-ttu-id="03b94-162">This data preparation package is the primary container for your data preparation work in Workbench.</span><span class="sxs-lookup"><span data-stu-id="03b94-162">This data preparation package is the primary container for your data preparation work in Workbench.</span></span>

<span data-ttu-id="03b94-163">This data preparation package can be handed off later to a runtime, such as local-C#/CoreCLR, Scala/Spark, or Scala/HDI.</span><span class="sxs-lookup"><span data-stu-id="03b94-163">This data preparation package can be handed off later to a runtime, such as local-C#/CoreCLR, Scala/Spark, or Scala/HDI.</span></span> 

1. <span data-ttu-id="03b94-164">Select the folder icon to open the Files view, then select **iris.csv** to open that file.</span><span class="sxs-lookup"><span data-stu-id="03b94-164">Select the folder icon to open the Files view, then select **iris.csv** to open that file.</span></span>

   <span data-ttu-id="03b94-165">This file contains a table with 5 columns and 50 rows.</span><span class="sxs-lookup"><span data-stu-id="03b94-165">This file contains a table with 5 columns and 50 rows.</span></span> <span data-ttu-id="03b94-166">Four columns are numerical feature columns.</span><span class="sxs-lookup"><span data-stu-id="03b94-166">Four columns are numerical feature columns.</span></span> <span data-ttu-id="03b94-167">The fifth column is a string target column.</span><span class="sxs-lookup"><span data-stu-id="03b94-167">The fifth column is a string target column.</span></span> <span data-ttu-id="03b94-168">None of the columns have header names.</span><span class="sxs-lookup"><span data-stu-id="03b94-168">None of the columns have header names.</span></span>

   ![iris.csv](media/tutorial-classifying-iris/show_iris_csv.png)

   >[!NOTE]
   > <span data-ttu-id="03b94-170">Do not include data files in your project folder, particularly when the file size is large.</span><span class="sxs-lookup"><span data-stu-id="03b94-170">Do not include data files in your project folder, particularly when the file size is large.</span></span> <span data-ttu-id="03b94-171">Because the **iris.csv** data file is tiny, it was included in this template for demonstration purposes.</span><span class="sxs-lookup"><span data-stu-id="03b94-171">Because the **iris.csv** data file is tiny, it was included in this template for demonstration purposes.</span></span> <span data-ttu-id="03b94-172">For more information, see [How to read and write large data files](how-to-read-write-files.md).</span><span class="sxs-lookup"><span data-stu-id="03b94-172">For more information, see [How to read and write large data files](how-to-read-write-files.md).</span></span>

2. <span data-ttu-id="03b94-173">In the **Data view**, select the plus sign (**+**) to add a new data source.</span><span class="sxs-lookup"><span data-stu-id="03b94-173">In the **Data view**, select the plus sign (**+**) to add a new data source.</span></span> <span data-ttu-id="03b94-174">The **Add Data Source** page opens.</span><span class="sxs-lookup"><span data-stu-id="03b94-174">The **Add Data Source** page opens.</span></span> 

   ![Data view in Azure Machine Learning Workbench](media/tutorial-classifying-iris/data_view.png)

3. <span data-ttu-id="03b94-176">Select **Text Files(\*.csv, \*.json, \*.txt., ...)** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="03b94-176">Select **Text Files(\*.csv, \*.json, \*.txt., ...)** and click **Next**.</span></span>
   <span data-ttu-id="03b94-177">![Data Source in Azure Machine Learning Workbench](media/tutorial-classifying-iris/data-source.png)</span><span class="sxs-lookup"><span data-stu-id="03b94-177">![Data Source in Azure Machine Learning Workbench](media/tutorial-classifying-iris/data-source.png)</span></span>

4. <span data-ttu-id="03b94-178">Browse to the file **iris.csv**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="03b94-178">Browse to the file **iris.csv**, and click **Finish**.</span></span> <span data-ttu-id="03b94-179">This will use default values for parameters such as the separator and data types.</span><span class="sxs-lookup"><span data-stu-id="03b94-179">This will use default values for parameters such as the separator and data types.</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="03b94-180">Make sure you select the **iris.csv** file from within the current project directory for this exercise.</span><span class="sxs-lookup"><span data-stu-id="03b94-180">Make sure you select the **iris.csv** file from within the current project directory for this exercise.</span></span> <span data-ttu-id="03b94-181">Otherwise, later steps might fail.</span><span class="sxs-lookup"><span data-stu-id="03b94-181">Otherwise, later steps might fail.</span></span>
 
   ![Select iris](media/tutorial-classifying-iris/select_iris_csv.png)
   
5. <span data-ttu-id="03b94-183">A new file named **iris-1.dsource** is created.</span><span class="sxs-lookup"><span data-stu-id="03b94-183">A new file named **iris-1.dsource** is created.</span></span> <span data-ttu-id="03b94-184">The file is named uniquely with  "-1" because the sample project already comes with an unnumbered **iris.dsource** file.</span><span class="sxs-lookup"><span data-stu-id="03b94-184">The file is named uniquely with  "-1" because the sample project already comes with an unnumbered **iris.dsource** file.</span></span>  

   <span data-ttu-id="03b94-185">The file opens, and the data is shown.</span><span class="sxs-lookup"><span data-stu-id="03b94-185">The file opens, and the data is shown.</span></span> <span data-ttu-id="03b94-186">A series of column headers, from **Column1** to **Column5**, is automatically added to this data set.</span><span class="sxs-lookup"><span data-stu-id="03b94-186">A series of column headers, from **Column1** to **Column5**, is automatically added to this data set.</span></span> <span data-ttu-id="03b94-187">Scroll to the bottom and notice that the last row of the data set is empty.</span><span class="sxs-lookup"><span data-stu-id="03b94-187">Scroll to the bottom and notice that the last row of the data set is empty.</span></span> <span data-ttu-id="03b94-188">The row is empty because there is an extra line break in the CSV file.</span><span class="sxs-lookup"><span data-stu-id="03b94-188">The row is empty because there is an extra line break in the CSV file.</span></span>

   ![Iris data view](media/tutorial-classifying-iris/iris_data_view.png)

1. <span data-ttu-id="03b94-190">Select the **Metrics** button.</span><span class="sxs-lookup"><span data-stu-id="03b94-190">Select the **Metrics** button.</span></span> <span data-ttu-id="03b94-191">Histograms are generated and displayed.</span><span class="sxs-lookup"><span data-stu-id="03b94-191">Histograms are generated and displayed.</span></span>

   <span data-ttu-id="03b94-192">You can switch back to the data view by selecting the **Data** button.</span><span class="sxs-lookup"><span data-stu-id="03b94-192">You can switch back to the data view by selecting the **Data** button.</span></span>
   
   ![Iris data view](media/tutorial-classifying-iris/iris_data_view_metrics.png)

1. <span data-ttu-id="03b94-194">Observe the histograms.</span><span class="sxs-lookup"><span data-stu-id="03b94-194">Observe the histograms.</span></span> <span data-ttu-id="03b94-195">A complete set of statistics has been calculated for each column.</span><span class="sxs-lookup"><span data-stu-id="03b94-195">A complete set of statistics has been calculated for each column.</span></span> 

   ![Iris data view](media/tutorial-classifying-iris/iris_metrics_view.png)

8. <span data-ttu-id="03b94-197">Begin creating a data preparation package by selecting the **Prepare** button.</span><span class="sxs-lookup"><span data-stu-id="03b94-197">Begin creating a data preparation package by selecting the **Prepare** button.</span></span> <span data-ttu-id="03b94-198">The **Prepare** dialog box opens.</span><span class="sxs-lookup"><span data-stu-id="03b94-198">The **Prepare** dialog box opens.</span></span> 

   <span data-ttu-id="03b94-199">The sample project contains a **iris.dprep** data preparation file that is selected by default.</span><span class="sxs-lookup"><span data-stu-id="03b94-199">The sample project contains a **iris.dprep** data preparation file that is selected by default.</span></span> 

   ![Iris data view](media/tutorial-classifying-iris/prepare.png)

1. <span data-ttu-id="03b94-201">Create a new data preparation package by selecting **+ New Data Preparation Package** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="03b94-201">Create a new data preparation package by selecting **+ New Data Preparation Package** from the drop-down menu.</span></span>

   ![Iris data view](media/tutorial-classifying-iris/prepare_new.png)

1. <span data-ttu-id="03b94-203">Enter a new value for the package name (use **iris-1**) and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="03b94-203">Enter a new value for the package name (use **iris-1**) and then select **OK**.</span></span>

   <span data-ttu-id="03b94-204">A new data preparation package named **iris-1.dprep** is created and opened in the data preparation editor.</span><span class="sxs-lookup"><span data-stu-id="03b94-204">A new data preparation package named **iris-1.dprep** is created and opened in the data preparation editor.</span></span>

   ![Iris data view](media/tutorial-classifying-iris/prepare_iris-1.png)

   <span data-ttu-id="03b94-206">Now, let's do some basic data preparation.</span><span class="sxs-lookup"><span data-stu-id="03b94-206">Now, let's do some basic data preparation.</span></span> 

1. <span data-ttu-id="03b94-207">Select each column header to make the header text editable.</span><span class="sxs-lookup"><span data-stu-id="03b94-207">Select each column header to make the header text editable.</span></span> <span data-ttu-id="03b94-208">Then, rename each column as follows:</span><span class="sxs-lookup"><span data-stu-id="03b94-208">Then, rename each column as follows:</span></span> 

   <span data-ttu-id="03b94-209">In order, enter **Sepal Length**, **Sepal Width**, **Petal Length**, **Petal Width**, and **Species** for the five columns respectively.</span><span class="sxs-lookup"><span data-stu-id="03b94-209">In order, enter **Sepal Length**, **Sepal Width**, **Petal Length**, **Petal Width**, and **Species** for the five columns respectively.</span></span>

   ![Rename the columns](media/tutorial-classifying-iris/rename_column.png)

1. <span data-ttu-id="03b94-211">Count distinct values:</span><span class="sxs-lookup"><span data-stu-id="03b94-211">Count distinct values:</span></span>
   1. <span data-ttu-id="03b94-212">Select the **Species** column</span><span class="sxs-lookup"><span data-stu-id="03b94-212">Select the **Species** column</span></span>
   1. <span data-ttu-id="03b94-213">Right-click to select it.</span><span class="sxs-lookup"><span data-stu-id="03b94-213">Right-click to select it.</span></span> 
   1. <span data-ttu-id="03b94-214">Select **Value Counts** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="03b94-214">Select **Value Counts** from the drop-down menu.</span></span> 

   <span data-ttu-id="03b94-215">The **Inspectors** pane opens below the data.</span><span class="sxs-lookup"><span data-stu-id="03b94-215">The **Inspectors** pane opens below the data.</span></span> <span data-ttu-id="03b94-216">A histogram with four bars appears.</span><span class="sxs-lookup"><span data-stu-id="03b94-216">A histogram with four bars appears.</span></span> <span data-ttu-id="03b94-217">The target column has four distinct values: **Iris-virginica**, **Iris-versicolor**, **Iris-setosa**, and a **(null)** value.</span><span class="sxs-lookup"><span data-stu-id="03b94-217">The target column has four distinct values: **Iris-virginica**, **Iris-versicolor**, **Iris-setosa**, and a **(null)** value.</span></span>

   ![Select Value Counts](media/tutorial-classifying-iris/value_count.png)

   ![Value count histogram](media/tutorial-classifying-iris/filter_out.png)

1. <span data-ttu-id="03b94-220">To filter out the null values, select the "(null)" bar and then select the minus sign (**-**).</span><span class="sxs-lookup"><span data-stu-id="03b94-220">To filter out the null values, select the "(null)" bar and then select the minus sign (**-**).</span></span> 

   <span data-ttu-id="03b94-221">Then, the (null) row turns gray to indicate that it was filtered out.</span><span class="sxs-lookup"><span data-stu-id="03b94-221">Then, the (null) row turns gray to indicate that it was filtered out.</span></span> 

   ![Filter out nulls](media/tutorial-classifying-iris/filter_out2.png)

1. <span data-ttu-id="03b94-223">Take notice of the individual data preparation steps that are detailed in the **STEPS** pane.</span><span class="sxs-lookup"><span data-stu-id="03b94-223">Take notice of the individual data preparation steps that are detailed in the **STEPS** pane.</span></span> <span data-ttu-id="03b94-224">As you renamed the columns and filtered the null value rows, each action was recorded as a data preparation step.</span><span class="sxs-lookup"><span data-stu-id="03b94-224">As you renamed the columns and filtered the null value rows, each action was recorded as a data preparation step.</span></span> <span data-ttu-id="03b94-225">You can edit individual steps to adjust their settings, reorder the steps, and remove steps.</span><span class="sxs-lookup"><span data-stu-id="03b94-225">You can edit individual steps to adjust their settings, reorder the steps, and remove steps.</span></span>

   ![Steps](media/tutorial-classifying-iris/steps.png)

1. <span data-ttu-id="03b94-227">Close the data preparation editor.</span><span class="sxs-lookup"><span data-stu-id="03b94-227">Close the data preparation editor.</span></span> <span data-ttu-id="03b94-228">Select the **x** icon on the **iris-1** tab with the graph icon to close the tab. Your work is automatically saved into the **iris-1.dprep** file shown under the **Data Preparations** heading.</span><span class="sxs-lookup"><span data-stu-id="03b94-228">Select the **x** icon on the **iris-1** tab with the graph icon to close the tab. Your work is automatically saved into the **iris-1.dprep** file shown under the **Data Preparations** heading.</span></span>

   ![Close](media/tutorial-classifying-iris/close.png)

## <a name="generate-pythonpyspark-code-to-invoke-a-data-preparation-package"></a><span data-ttu-id="03b94-230">Generate Python/PySpark code to invoke a data preparation package</span><span class="sxs-lookup"><span data-stu-id="03b94-230">Generate Python/PySpark code to invoke a data preparation package</span></span>

 <span data-ttu-id="03b94-231">The output of a data preparation package can be explored directly in Python or in a Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="03b94-231">The output of a data preparation package can be explored directly in Python or in a Jupyter Notebook.</span></span> <span data-ttu-id="03b94-232">The packages can be executed across multiple runtimes including local Python, Spark (including in Docker), and HDInsight.</span><span class="sxs-lookup"><span data-stu-id="03b94-232">The packages can be executed across multiple runtimes including local Python, Spark (including in Docker), and HDInsight.</span></span> 

1. <span data-ttu-id="03b94-233">Find the **iris-1.dprep** file under the Data Preparations tab.</span><span class="sxs-lookup"><span data-stu-id="03b94-233">Find the **iris-1.dprep** file under the Data Preparations tab.</span></span>

1. <span data-ttu-id="03b94-234">Right-click the **iris-1.dprep** file, and select **Generate Data Access Code File** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="03b94-234">Right-click the **iris-1.dprep** file, and select **Generate Data Access Code File** from the context menu.</span></span> 

   ![Generate code](media/tutorial-classifying-iris/generate_code.png)

   <span data-ttu-id="03b94-236">A new file named **iris-1.py** opens with the following lines of code to invoke the logic you created as a data preparation package:</span><span class="sxs-lookup"><span data-stu-id="03b94-236">A new file named **iris-1.py** opens with the following lines of code to invoke the logic you created as a data preparation package:</span></span>

   ```python
   # Use the Azure Machine Learning data preparation package
   from azureml.dataprep import package

   # Use the Azure Machine Learning data collector to log various metrics
   from azureml.logging import get_azureml_logger
   logger = get_azureml_logger()

   # This call will load the referenced package and return a DataFrame.
   # If run in a PySpark environment, this call returns a
   # Spark DataFrame. If not, it will return a Pandas DataFrame.
   df = package.run('iris-1.dprep', dataflow_idx=0)

   # Remove this line and add code that uses the DataFrame
   df.head(10)
   ```

   <span data-ttu-id="03b94-237">Depending on the context in which this code is run, `df` represents a different kind of DataFrame:</span><span class="sxs-lookup"><span data-stu-id="03b94-237">Depending on the context in which this code is run, `df` represents a different kind of DataFrame:</span></span>
   + <span data-ttu-id="03b94-238">When executing on a Python runtime, a [pandas DataFrame](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html) is used.</span><span class="sxs-lookup"><span data-stu-id="03b94-238">When executing on a Python runtime, a [pandas DataFrame](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html) is used.</span></span>
   + <span data-ttu-id="03b94-239">When executing in a Spark context, a [Spark DataFrame](https://spark.apache.org/docs/latest/sql-programming-guide.html) is used.</span><span class="sxs-lookup"><span data-stu-id="03b94-239">When executing in a Spark context, a [Spark DataFrame](https://spark.apache.org/docs/latest/sql-programming-guide.html) is used.</span></span> 
   
   <span data-ttu-id="03b94-240">To learn more about how to prepare data in Azure Machine Learning Workbench, see the [Get started with data preparation](data-prep-getting-started.md) guide.</span><span class="sxs-lookup"><span data-stu-id="03b94-240">To learn more about how to prepare data in Azure Machine Learning Workbench, see the [Get started with data preparation](data-prep-getting-started.md) guide.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="03b94-241">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="03b94-241">Clean up resources</span></span>

[!INCLUDE [aml-delete-resource-group](../../../includes/aml-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="03b94-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="03b94-242">Next steps</span></span>

<span data-ttu-id="03b94-243">In this tutorial, you used Azure Machine Learning Workbench to:</span><span class="sxs-lookup"><span data-stu-id="03b94-243">In this tutorial, you used Azure Machine Learning Workbench to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="03b94-244">Create a new project</span><span class="sxs-lookup"><span data-stu-id="03b94-244">Create a new project</span></span>
> * <span data-ttu-id="03b94-245">Create a data preparation package</span><span class="sxs-lookup"><span data-stu-id="03b94-245">Create a data preparation package</span></span>
> * <span data-ttu-id="03b94-246">Generate Python/PySpark code to invoke a data preparation package</span><span class="sxs-lookup"><span data-stu-id="03b94-246">Generate Python/PySpark code to invoke a data preparation package</span></span>

<span data-ttu-id="03b94-247">You are ready to move on to the next part in the tutorial series, where you learn how to build an Azure Machine Learning model:</span><span class="sxs-lookup"><span data-stu-id="03b94-247">You are ready to move on to the next part in the tutorial series, where you learn how to build an Azure Machine Learning model:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="03b94-248">Tutorial 2 - Build models</span><span class="sxs-lookup"><span data-stu-id="03b94-248">Tutorial 2 - Build models</span></span>](tutorial-classifying-iris-part-2.md)
