---
title: Run U-SQL and debug locally in Azure Data Lake Tools for Visual Studio Code
description: Learn how to use Azure Data Lake Tools for Visual Studio Code to run and debug U-SQL jobs locally.
services: data-lake-analytics
ms.service: data-lake-analytics
author: jejiang
ms.author: jejiang
ms.reviewer: jasonwhowell
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.topic: conceptual
ms.date: 07/14/2017
ms.openlocfilehash: bf98562224c2da770541f731ba93ec2e5dc1718d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870649"
---
# <a name="run-u-sql-and-debug-locally-in-visual-studio-code"></a><span data-ttu-id="ec6ee-103">Run U-SQL and debug locally in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ec6ee-103">Run U-SQL and debug locally in Visual Studio Code</span></span>
<span data-ttu-id="ec6ee-104">This article describes how to run U-SQL jobs on a local development machine to speed up early coding phases or to debug code locally in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-104">This article describes how to run U-SQL jobs on a local development machine to speed up early coding phases or to debug code locally in Visual Studio Code.</span></span> <span data-ttu-id="ec6ee-105">For instructions on Azure Data Lake Tool for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="ec6ee-105">For instructions on Azure Data Lake Tool for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span> 

## <a name="set-up-the-u-sql-local-run-environment"></a><span data-ttu-id="ec6ee-106">Set up the U-SQL local run environment</span><span class="sxs-lookup"><span data-stu-id="ec6ee-106">Set up the U-SQL local run environment</span></span>

1. <span data-ttu-id="ec6ee-107">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download Local Run Package** to download the packages.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-107">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download Local Run Package** to download the packages.</span></span>  

   ![Download the ADL LocalRun Dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/downloadtheadllocalrunpackage.png)

2. <span data-ttu-id="ec6ee-109">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-109">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="ec6ee-110">Here is an example path:</span><span class="sxs-lookup"><span data-stu-id="ec6ee-110">Here is an example path:</span></span>  
`C:\Users\xxx\AppData\Roaming\LocalRunDependency` 

   ![Locate the dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   <span data-ttu-id="ec6ee-112">2.1 To install **BuildTools**, click visualcppbuildtools_full.exe in the LocalRunDependency folder, then follow the wizard instructions.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-112">2.1 To install **BuildTools**, click visualcppbuildtools_full.exe in the LocalRunDependency folder, then follow the wizard instructions.</span></span>   

    ![Install BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="ec6ee-114">2.2 To install **Win10SDK 10240**, click sdksetup.exe in the LocalRunDependency/Win10SDK_10.0.10240_2 folder, then follow the wizard instructions.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-114">2.2 To install **Win10SDK 10240**, click sdksetup.exe in the LocalRunDependency/Win10SDK_10.0.10240_2 folder, then follow the wizard instructions.</span></span>  

    ![Install Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="ec6ee-116">Set up the environment variable.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-116">Set up the environment variable.</span></span> <span data-ttu-id="ec6ee-117">Set the **SCOPE_CPP_SDK** environment variable to:</span><span class="sxs-lookup"><span data-stu-id="ec6ee-117">Set the **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\XXX\AppData\Roaming\LocalRunDependency\CppSDK_3rdparty`  


## <a name="start-the-local-run-service-and-submit-the-u-sql-job-to-a-local-account"></a><span data-ttu-id="ec6ee-118">Start the local run service and submit the U-SQL job to a local account</span><span class="sxs-lookup"><span data-stu-id="ec6ee-118">Start the local run service and submit the U-SQL job to a local account</span></span> 
<span data-ttu-id="ec6ee-119">For the first-time user, use **ADL: Download Local Run Package** to download local run packages, if you have not [set up U-SQL local run environment](#set-up-the-u-sql-local-run-environment).</span><span class="sxs-lookup"><span data-stu-id="ec6ee-119">For the first-time user, use **ADL: Download Local Run Package** to download local run packages, if you have not [set up U-SQL local run environment](#set-up-the-u-sql-local-run-environment).</span></span>

1. <span data-ttu-id="ec6ee-120">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-120">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span>   
2. <span data-ttu-id="ec6ee-121">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-121">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span></span> 

   ![Accept the Microsoft Software License Terms](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="ec6ee-123">The cmd console opens.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-123">The cmd console opens.</span></span> <span data-ttu-id="ec6ee-124">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-124">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span></span> <span data-ttu-id="ec6ee-125">For other options, you can use the default values.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-125">For other options, you can use the default values.</span></span> 

   ![Data Lake Tools for Visual Studio Code local run cmd](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="ec6ee-127">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-127">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span></span>

   ![Data Lake Tools for Visual Studio Code select local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="ec6ee-129">After you submit the job, you can view the submission details.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-129">After you submit the job, you can view the submission details.</span></span> <span data-ttu-id="ec6ee-130">To view the submission details, select **jobUrl** in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-130">To view the submission details, select **jobUrl** in the **Output** window.</span></span> <span data-ttu-id="ec6ee-131">You can also view the job submission status from the cmd console.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-131">You can also view the job submission status from the cmd console.</span></span> <span data-ttu-id="ec6ee-132">Enter **7** in the cmd console if you want to know more job details.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-132">Enter **7** in the cmd console if you want to know more job details.</span></span>

   <span data-ttu-id="ec6ee-133">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="ec6ee-133">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-the-u-sql-job"></a><span data-ttu-id="ec6ee-134">Start a local debug for the U-SQL job</span><span class="sxs-lookup"><span data-stu-id="ec6ee-134">Start a local debug for the U-SQL job</span></span>  
<span data-ttu-id="ec6ee-135">For the first-time user:</span><span class="sxs-lookup"><span data-stu-id="ec6ee-135">For the first-time user:</span></span>

1. <span data-ttu-id="ec6ee-136">Use **ADL: Download Local Run Package** to download local run packages, if you have not [set up U-SQL local run environment](#set-up-the-u-sql-local-run-environment).</span><span class="sxs-lookup"><span data-stu-id="ec6ee-136">Use **ADL: Download Local Run Package** to download local run packages, if you have not [set up U-SQL local run environment](#set-up-the-u-sql-local-run-environment).</span></span>
2. <span data-ttu-id="ec6ee-137">Install .NET Core SDK 2.0 as suggested in the message box, if not installed.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-137">Install .NET Core SDK 2.0 as suggested in the message box, if not installed.</span></span>
 
  ![reminder installs Dotnet](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/remind-install-dotnet.png)
3. <span data-ttu-id="ec6ee-139">Install C# for Visual Studio Code as suggested in the message box if not installed.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-139">Install C# for Visual Studio Code as suggested in the message box if not installed.</span></span> <span data-ttu-id="ec6ee-140">Click **Install** to continue, and then restart VSCode.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-140">Click **Install** to continue, and then restart VSCode.</span></span>

    ![Reminder to install C#](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/install-csharp.png)

<span data-ttu-id="ec6ee-142">Follow steps below to perform local debug:</span><span class="sxs-lookup"><span data-stu-id="ec6ee-142">Follow steps below to perform local debug:</span></span>
  
1. <span data-ttu-id="ec6ee-143">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-143">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="ec6ee-144">The cmd console opens.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-144">The cmd console opens.</span></span> <span data-ttu-id="ec6ee-145">Make sure that the **DataRoot** is set.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-145">Make sure that the **DataRoot** is set.</span></span>
2. <span data-ttu-id="ec6ee-146">Set a breakpoint in your C# code-behind.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-146">Set a breakpoint in your C# code-behind.</span></span>
3. <span data-ttu-id="ec6ee-147">Back to script editor, right-click and select **ADL: Local Debug**.</span><span class="sxs-lookup"><span data-stu-id="ec6ee-147">Back to script editor, right-click and select **ADL: Local Debug**.</span></span>
    
   ![Data Lake Tools for Visual Studio Code local debug result](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="ec6ee-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec6ee-149">Next steps</span></span>
* [<span data-ttu-id="ec6ee-150">Use the Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ec6ee-150">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
* [<span data-ttu-id="ec6ee-151">Develop U-SQL with Python, R, and CSharp for Azure Data Lake Analytics in VSCode</span><span class="sxs-lookup"><span data-stu-id="ec6ee-151">Develop U-SQL with Python, R, and CSharp for Azure Data Lake Analytics in VSCode</span></span>](data-lake-analytics-u-sql-develop-with-python-r-csharp-in-vscode.md)
* [<span data-ttu-id="ec6ee-152">Get started with Data Lake Analytics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec6ee-152">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="ec6ee-153">Get started with Data Lake Analytics using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ec6ee-153">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ec6ee-154">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span><span class="sxs-lookup"><span data-stu-id="ec6ee-154">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="ec6ee-155">Use Data Lake Analytics(U-SQL) catalog</span><span class="sxs-lookup"><span data-stu-id="ec6ee-155">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
