---
title: Data science code testing on Azure with the UCI adult income prediction dataset - Team Data Science Process and Azure DevOps Services
description: Data science code testing with UCI adult income prediction data
services: machine-learning, team-data-science-process
documentationcenter: ''
author: weig
manager: deguhath
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2018
ms.author: weig
ms.openlocfilehash: ad0a8b5b0bb9afbbe626c9481961f20ccd4797bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867958"
---
# <a name="data-science-code-testing-with-the-uci-adult-income-prediction-dataset"></a><span data-ttu-id="d8adc-103">Data science code testing with the UCI adult income prediction dataset</span><span class="sxs-lookup"><span data-stu-id="d8adc-103">Data science code testing with the UCI adult income prediction dataset</span></span>
<span data-ttu-id="d8adc-104">This article gives preliminary guidelines for testing code in a data science workflow.</span><span class="sxs-lookup"><span data-stu-id="d8adc-104">This article gives preliminary guidelines for testing code in a data science workflow.</span></span> <span data-ttu-id="d8adc-105">Such testing gives data scientists a systematic and efficient way to check the quality and expected outcome of their code.</span><span class="sxs-lookup"><span data-stu-id="d8adc-105">Such testing gives data scientists a systematic and efficient way to check the quality and expected outcome of their code.</span></span> <span data-ttu-id="d8adc-106">We use a Team Data Science Process (TDSP) [project that uses the UCI Adult Income dataset](https://github.com/Azure/MachineLearningSamples-TDSPUCIAdultIncome) that we published earlier to show how code testing can be done.</span><span class="sxs-lookup"><span data-stu-id="d8adc-106">We use a Team Data Science Process (TDSP) [project that uses the UCI Adult Income dataset](https://github.com/Azure/MachineLearningSamples-TDSPUCIAdultIncome) that we published earlier to show how code testing can be done.</span></span> 

## <a name="introduction-on-code-testing"></a><span data-ttu-id="d8adc-107">Introduction on code testing</span><span class="sxs-lookup"><span data-stu-id="d8adc-107">Introduction on code testing</span></span>
<span data-ttu-id="d8adc-108">"Unit testing" is a longstanding practice for software development.</span><span class="sxs-lookup"><span data-stu-id="d8adc-108">"Unit testing" is a longstanding practice for software development.</span></span> <span data-ttu-id="d8adc-109">But for data science, it's often not clear what that means and how you should test code for different stages of a data science lifecycle, such as:</span><span class="sxs-lookup"><span data-stu-id="d8adc-109">But for data science, it's often not clear what that means and how you should test code for different stages of a data science lifecycle, such as:</span></span>

* <span data-ttu-id="d8adc-110">Data preparation</span><span class="sxs-lookup"><span data-stu-id="d8adc-110">Data preparation</span></span>
* <span data-ttu-id="d8adc-111">Data quality examination</span><span class="sxs-lookup"><span data-stu-id="d8adc-111">Data quality examination</span></span>
* <span data-ttu-id="d8adc-112">Modeling</span><span class="sxs-lookup"><span data-stu-id="d8adc-112">Modeling</span></span>
* <span data-ttu-id="d8adc-113">Model deployment</span><span class="sxs-lookup"><span data-stu-id="d8adc-113">Model deployment</span></span> 

<span data-ttu-id="d8adc-114">This article replaces the term "unit testing" with "code testing."</span><span class="sxs-lookup"><span data-stu-id="d8adc-114">This article replaces the term "unit testing" with "code testing."</span></span> <span data-ttu-id="d8adc-115">It refers to testing as the functions that help to assess if code for a certain step of a data science lifecycle is producing results "as expected."</span><span class="sxs-lookup"><span data-stu-id="d8adc-115">It refers to testing as the functions that help to assess if code for a certain step of a data science lifecycle is producing results "as expected."</span></span> <span data-ttu-id="d8adc-116">The person who's writing the test defines what's "as expected," depending on the outcome of the function--for example, data quality check or modeling.</span><span class="sxs-lookup"><span data-stu-id="d8adc-116">The person who's writing the test defines what's "as expected," depending on the outcome of the function--for example, data quality check or modeling.</span></span>

<span data-ttu-id="d8adc-117">This article provides references as useful resources.</span><span class="sxs-lookup"><span data-stu-id="d8adc-117">This article provides references as useful resources.</span></span>

## <a name="azure-devops-for-the-testing-framework"></a><span data-ttu-id="d8adc-118">Azure DevOps for the testing framework</span><span class="sxs-lookup"><span data-stu-id="d8adc-118">Azure DevOps for the testing framework</span></span>
<span data-ttu-id="d8adc-119">This article describes how to perform and automate testing by using Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="d8adc-119">This article describes how to perform and automate testing by using Azure DevOps.</span></span> <span data-ttu-id="d8adc-120">You might decide to use alternative tools.</span><span class="sxs-lookup"><span data-stu-id="d8adc-120">You might decide to use alternative tools.</span></span> <span data-ttu-id="d8adc-121">We also show how to set up an automatic build by using Azure DevOps and build agents.</span><span class="sxs-lookup"><span data-stu-id="d8adc-121">We also show how to set up an automatic build by using Azure DevOps and build agents.</span></span> <span data-ttu-id="d8adc-122">For build agents, we use Azure Data Science Virtual Machines (DSVMs).</span><span class="sxs-lookup"><span data-stu-id="d8adc-122">For build agents, we use Azure Data Science Virtual Machines (DSVMs).</span></span>

## <a name="flow-of-code-testing"></a><span data-ttu-id="d8adc-123">Flow of code testing</span><span class="sxs-lookup"><span data-stu-id="d8adc-123">Flow of code testing</span></span>
<span data-ttu-id="d8adc-124">The overall workflow of testing code in a data science project looks like this:</span><span class="sxs-lookup"><span data-stu-id="d8adc-124">The overall workflow of testing code in a data science project looks like this:</span></span> 

![Flow chart of code testing](./media/code-test/test-flow-chart.PNG)

    
## <a name="detailed-steps"></a><span data-ttu-id="d8adc-126">Detailed steps</span><span class="sxs-lookup"><span data-stu-id="d8adc-126">Detailed steps</span></span>

<span data-ttu-id="d8adc-127">Use the following steps to set up and run code testing and an automated build by using a build agent and Azure DevOps:</span><span class="sxs-lookup"><span data-stu-id="d8adc-127">Use the following steps to set up and run code testing and an automated build by using a build agent and Azure DevOps:</span></span>

1. <span data-ttu-id="d8adc-128">Create a project in the Visual Studio desktop application:</span><span class="sxs-lookup"><span data-stu-id="d8adc-128">Create a project in the Visual Studio desktop application:</span></span>

    !["Create new project" screen in Visual Studio](./media/code-test/create_project.PNG)

   <span data-ttu-id="d8adc-130">After you create your project, you'll find it in Solution Explorer in the right pane:</span><span class="sxs-lookup"><span data-stu-id="d8adc-130">After you create your project, you'll find it in Solution Explorer in the right pane:</span></span>
    
    ![Steps for creating a project](./media/code-test/create_python_project_in_vs.PNG)

    ![Solution Explorer](./media/code-test/solution_explorer_in_vs.PNG)

1. <span data-ttu-id="d8adc-133">Feed your project code into the Azure DevOps project code repository:</span><span class="sxs-lookup"><span data-stu-id="d8adc-133">Feed your project code into the Azure DevOps project code repository:</span></span> 

    ![Project code repository](./media/code-test/create_repo.PNG)

1. <span data-ttu-id="d8adc-135">Suppose you've done some data preparation work, such as data ingestion, feature engineering, and creating label columns.</span><span class="sxs-lookup"><span data-stu-id="d8adc-135">Suppose you've done some data preparation work, such as data ingestion, feature engineering, and creating label columns.</span></span> <span data-ttu-id="d8adc-136">You want to make sure your code is generating the results that you expect.</span><span class="sxs-lookup"><span data-stu-id="d8adc-136">You want to make sure your code is generating the results that you expect.</span></span> <span data-ttu-id="d8adc-137">Here's some code that you can use to test whether the data-processing code is working properly:</span><span class="sxs-lookup"><span data-stu-id="d8adc-137">Here's some code that you can use to test whether the data-processing code is working properly:</span></span>

    * <span data-ttu-id="d8adc-138">Check that column names are right:</span><span class="sxs-lookup"><span data-stu-id="d8adc-138">Check that column names are right:</span></span>
    
      ![Code for matching column names](./media/code-test/check_column_names.PNG)

    * <span data-ttu-id="d8adc-140">Check that response levels are right:</span><span class="sxs-lookup"><span data-stu-id="d8adc-140">Check that response levels are right:</span></span>

      ![Code for matching levels](./media/code-test/check_response_levels.PNG)

    * <span data-ttu-id="d8adc-142">Check that response percentage is reasonable:</span><span class="sxs-lookup"><span data-stu-id="d8adc-142">Check that response percentage is reasonable:</span></span>

      ![Code for response percentage](./media/code-test/check_response_percentage.PNG)

    * <span data-ttu-id="d8adc-144">Check the missing rate of each column in the data:</span><span class="sxs-lookup"><span data-stu-id="d8adc-144">Check the missing rate of each column in the data:</span></span>
    
      ![Code for missing rate](./media/code-test/check_missing_rate.PNG)


1. <span data-ttu-id="d8adc-146">After you've done the data processing and feature engineering work, and you've trained a good model, make sure that the model you trained can score new datasets correctly.</span><span class="sxs-lookup"><span data-stu-id="d8adc-146">After you've done the data processing and feature engineering work, and you've trained a good model, make sure that the model you trained can score new datasets correctly.</span></span> <span data-ttu-id="d8adc-147">You can use the following two tests to check the prediction levels and distribution of label values:</span><span class="sxs-lookup"><span data-stu-id="d8adc-147">You can use the following two tests to check the prediction levels and distribution of label values:</span></span>

    * <span data-ttu-id="d8adc-148">Check prediction levels:</span><span class="sxs-lookup"><span data-stu-id="d8adc-148">Check prediction levels:</span></span>
    
      ![Code for checking prediction levels](./media/code-test/check_prediction_levels.PNG)

    * <span data-ttu-id="d8adc-150">Check the distribution of prediction values:</span><span class="sxs-lookup"><span data-stu-id="d8adc-150">Check the distribution of prediction values:</span></span>

      ![Code for checking prediction values](./media/code-test/check_prediction_values.PNG)

1. <span data-ttu-id="d8adc-152">Put all test functions together into a Python script called **test_funcs.py**:</span><span class="sxs-lookup"><span data-stu-id="d8adc-152">Put all test functions together into a Python script called **test_funcs.py**:</span></span>

    ![Python script for test functions](./media/code-test/create_file_test_func.PNG)


1. <span data-ttu-id="d8adc-154">After the test codes are prepared, you can set up the testing environment in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8adc-154">After the test codes are prepared, you can set up the testing environment in Visual Studio.</span></span>

   <span data-ttu-id="d8adc-155">Create a Python file called **test1.py**.</span><span class="sxs-lookup"><span data-stu-id="d8adc-155">Create a Python file called **test1.py**.</span></span> <span data-ttu-id="d8adc-156">In this file, create a class that includes all the tests you want to do.</span><span class="sxs-lookup"><span data-stu-id="d8adc-156">In this file, create a class that includes all the tests you want to do.</span></span> <span data-ttu-id="d8adc-157">The following example shows six tests prepared:</span><span class="sxs-lookup"><span data-stu-id="d8adc-157">The following example shows six tests prepared:</span></span>
    
    ![Python file with a list of tests in a class](./media/code-test/create_file_test1_class.PNG)

1. <span data-ttu-id="d8adc-159">Those tests can be automatically discovered if you put **codetest.testCase** after your class name.</span><span class="sxs-lookup"><span data-stu-id="d8adc-159">Those tests can be automatically discovered if you put **codetest.testCase** after your class name.</span></span> <span data-ttu-id="d8adc-160">Open Test Explorer in the right pane, and select **Run All**.</span><span class="sxs-lookup"><span data-stu-id="d8adc-160">Open Test Explorer in the right pane, and select **Run All**.</span></span> <span data-ttu-id="d8adc-161">All the tests will run sequentially and will tell you if the test is successful or not.</span><span class="sxs-lookup"><span data-stu-id="d8adc-161">All the tests will run sequentially and will tell you if the test is successful or not.</span></span>

    ![Running the tests](./media/code-test/run_tests.PNG)

1. <span data-ttu-id="d8adc-163">Check in your code to the project repository by using Git commands.</span><span class="sxs-lookup"><span data-stu-id="d8adc-163">Check in your code to the project repository by using Git commands.</span></span> <span data-ttu-id="d8adc-164">Your most recent work will be reflected shortly in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="d8adc-164">Your most recent work will be reflected shortly in Azure DevOps.</span></span>

    ![Git commands for checking in code](./media/code-test/git_check_in.PNG)

    ![Most recent work in Azure DevOps](./media/code-test/git_check_in_most_recent_work.PNG)

1. <span data-ttu-id="d8adc-167">Set up automatic build and test in Azure DevOps:</span><span class="sxs-lookup"><span data-stu-id="d8adc-167">Set up automatic build and test in Azure DevOps:</span></span>

    <span data-ttu-id="d8adc-168">a.</span><span class="sxs-lookup"><span data-stu-id="d8adc-168">a.</span></span> <span data-ttu-id="d8adc-169">In the project repository, select **Build and Release**, and then select **+New** to create a new build process.</span><span class="sxs-lookup"><span data-stu-id="d8adc-169">In the project repository, select **Build and Release**, and then select **+New** to create a new build process.</span></span>

       ![Selections for starting a new build process](./media/code-test/create_new_build.PNG)

    <span data-ttu-id="d8adc-170">b.</span><span class="sxs-lookup"><span data-stu-id="d8adc-170">b.</span></span> <span data-ttu-id="d8adc-171">Follow the prompts to select your source code location, project name, repository, and branch information.</span><span class="sxs-lookup"><span data-stu-id="d8adc-171">Follow the prompts to select your source code location, project name, repository, and branch information.</span></span>
    
       ![Source, name, repository, and branch information](./media/code-test/fill_in_build_info.PNG)

    <span data-ttu-id="d8adc-172">c.</span><span class="sxs-lookup"><span data-stu-id="d8adc-172">c.</span></span> <span data-ttu-id="d8adc-173">Select a template.</span><span class="sxs-lookup"><span data-stu-id="d8adc-173">Select a template.</span></span> <span data-ttu-id="d8adc-174">Because there's no Python project template, start by selecting **Empty process**.</span><span class="sxs-lookup"><span data-stu-id="d8adc-174">Because there's no Python project template, start by selecting **Empty process**.</span></span> 

       ![List of templates and "Empty process" button](./media/code-test/start_empty_process_template.PNG)

    <span data-ttu-id="d8adc-175">d.</span><span class="sxs-lookup"><span data-stu-id="d8adc-175">d.</span></span> <span data-ttu-id="d8adc-176">Name the build and select the agent.</span><span class="sxs-lookup"><span data-stu-id="d8adc-176">Name the build and select the agent.</span></span> <span data-ttu-id="d8adc-177">You can choose the default here if you want to use a DSVM to finish the build process.</span><span class="sxs-lookup"><span data-stu-id="d8adc-177">You can choose the default here if you want to use a DSVM to finish the build process.</span></span> <span data-ttu-id="d8adc-178">For more information about setting agents, see [Build and release agents](https://docs.microsoft.com/azure/devops/pipelines/agents/agents?view=vsts).</span><span class="sxs-lookup"><span data-stu-id="d8adc-178">For more information about setting agents, see [Build and release agents](https://docs.microsoft.com/azure/devops/pipelines/agents/agents?view=vsts).</span></span>
    
       ![Build and agent selections](./media/code-test/select_agent.PNG)

    <span data-ttu-id="d8adc-179">e.</span><span class="sxs-lookup"><span data-stu-id="d8adc-179">e.</span></span> <span data-ttu-id="d8adc-180">Select **+** in the left pane, to add a task for this build phase.</span><span class="sxs-lookup"><span data-stu-id="d8adc-180">Select **+** in the left pane, to add a task for this build phase.</span></span> <span data-ttu-id="d8adc-181">Because we're going to run the Python script **test1.py** to finish all the checks, this task is using a PowerShell command to run Python code.</span><span class="sxs-lookup"><span data-stu-id="d8adc-181">Because we're going to run the Python script **test1.py** to finish all the checks, this task is using a PowerShell command to run Python code.</span></span>
    
       !["Add tasks" pane with PowerShell selected](./media/code-test/add_task_powershell.PNG)

    <span data-ttu-id="d8adc-182">f.</span><span class="sxs-lookup"><span data-stu-id="d8adc-182">f.</span></span> <span data-ttu-id="d8adc-183">In the PowerShell details, fill in the required information, such as the name and version of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8adc-183">In the PowerShell details, fill in the required information, such as the name and version of PowerShell.</span></span> <span data-ttu-id="d8adc-184">Choose **Inline Script** as the type.</span><span class="sxs-lookup"><span data-stu-id="d8adc-184">Choose **Inline Script** as the type.</span></span> 
    
       In the box under **Inline Script**, you can type **python test1.py**. Make sure the environment variable is set up correctly for Python. If you need a different version or kernel of Python, you can explicitly specify the path as shown in the figure: 
    
       ![PowerShell details](./media/code-test/powershell_scripts.PNG)

    <span data-ttu-id="d8adc-185">g.</span><span class="sxs-lookup"><span data-stu-id="d8adc-185">g.</span></span> <span data-ttu-id="d8adc-186">Select **Save & queue** to finish the build pipeline process.</span><span class="sxs-lookup"><span data-stu-id="d8adc-186">Select **Save & queue** to finish the build pipeline process.</span></span>

       !["Save & queue" button](./media/code-test/save_and_queue_build_definition.PNG)

<span data-ttu-id="d8adc-187">Now every time a new commit is pushed to the code repository, the build process will start automatically.</span><span class="sxs-lookup"><span data-stu-id="d8adc-187">Now every time a new commit is pushed to the code repository, the build process will start automatically.</span></span> <span data-ttu-id="d8adc-188">(Here we use master as the repository, but you can define any branch.) The process runs the **test1.py** file in the agent machine to make sure that everything defined in the code runs correctly.</span><span class="sxs-lookup"><span data-stu-id="d8adc-188">(Here we use master as the repository, but you can define any branch.) The process runs the **test1.py** file in the agent machine to make sure that everything defined in the code runs correctly.</span></span> 

<span data-ttu-id="d8adc-189">If alerts are set up correctly, you'll be notified in email when the build is finished.</span><span class="sxs-lookup"><span data-stu-id="d8adc-189">If alerts are set up correctly, you'll be notified in email when the build is finished.</span></span> <span data-ttu-id="d8adc-190">You can also check the build status in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="d8adc-190">You can also check the build status in Azure DevOps.</span></span> <span data-ttu-id="d8adc-191">If it fails, you can check the details of the build and find out which piece is broken.</span><span class="sxs-lookup"><span data-stu-id="d8adc-191">If it fails, you can check the details of the build and find out which piece is broken.</span></span>

![Email notification of build success](./media/code-test/email_build_succeed.PNG)

![Azure DevOps notification of build success](./media/code-test/vs_online_build_succeed.PNG)

## <a name="next-steps"></a><span data-ttu-id="d8adc-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8adc-194">Next steps</span></span>
* <span data-ttu-id="d8adc-195">See the [UCI income prediction repository](https://github.com/Azure/MachineLearningSamples-TDSPUCIAdultIncome) for concrete examples of unit tests for data science scenarios.</span><span class="sxs-lookup"><span data-stu-id="d8adc-195">See the [UCI income prediction repository](https://github.com/Azure/MachineLearningSamples-TDSPUCIAdultIncome) for concrete examples of unit tests for data science scenarios.</span></span>
* <span data-ttu-id="d8adc-196">Follow the preceding outline and examples from the UCI income prediction scenario in your own data science projects.</span><span class="sxs-lookup"><span data-stu-id="d8adc-196">Follow the preceding outline and examples from the UCI income prediction scenario in your own data science projects.</span></span>

## <a name="references"></a><span data-ttu-id="d8adc-197">References</span><span class="sxs-lookup"><span data-stu-id="d8adc-197">References</span></span>
* [<span data-ttu-id="d8adc-198">Team Data Science Process</span><span class="sxs-lookup"><span data-stu-id="d8adc-198">Team Data Science Process</span></span>](https://aka.ms/tdsp)
* [<span data-ttu-id="d8adc-199">Visual Studio Testing Tools</span><span class="sxs-lookup"><span data-stu-id="d8adc-199">Visual Studio Testing Tools</span></span>](https://www.visualstudio.com/vs/features/testing-tools/)
* [<span data-ttu-id="d8adc-200">Azure DevOps Testing Resources</span><span class="sxs-lookup"><span data-stu-id="d8adc-200">Azure DevOps Testing Resources</span></span>](https://www.visualstudio.com/team-services/)
* [<span data-ttu-id="d8adc-201">Data Science Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="d8adc-201">Data Science Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)