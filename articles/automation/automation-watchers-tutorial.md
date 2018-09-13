---
title: Create a watcher task in the Azure Automation account
description: Learn how to create a watcher task in the Azure Automation account to watch for new files created in a folder.
services: automation
ms.service: automation
ms.component: process-automation
author: eamonoreilly
ms.author: eamono
ms.topic: conceptual
ms.date: 03/19/2017
ms.openlocfilehash: 0cc215d6643c86460a1d5471aa1eed8fdf18e028
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870597"
---
# <a name="create-an-azure-automation-watcher-tasks-to-track-file-changes-on-a-local-machine"></a><span data-ttu-id="473de-103">Create an Azure Automation watcher tasks to track file changes on a local machine</span><span class="sxs-lookup"><span data-stu-id="473de-103">Create an Azure Automation watcher tasks to track file changes on a local machine</span></span>

<span data-ttu-id="473de-104">Azure Automation uses watcher tasks to watch for events and trigger actions.</span><span class="sxs-lookup"><span data-stu-id="473de-104">Azure Automation uses watcher tasks to watch for events and trigger actions.</span></span> <span data-ttu-id="473de-105">This tutorial walks you through creating a watcher task to monitor when a new file is added to a directory.</span><span class="sxs-lookup"><span data-stu-id="473de-105">This tutorial walks you through creating a watcher task to monitor when a new file is added to a directory.</span></span>

<span data-ttu-id="473de-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="473de-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="473de-107">Import a watcher runbook</span><span class="sxs-lookup"><span data-stu-id="473de-107">Import a watcher runbook</span></span>
> * <span data-ttu-id="473de-108">Create an Automation variable</span><span class="sxs-lookup"><span data-stu-id="473de-108">Create an Automation variable</span></span>
> * <span data-ttu-id="473de-109">Create an action runbook</span><span class="sxs-lookup"><span data-stu-id="473de-109">Create an action runbook</span></span>
> * <span data-ttu-id="473de-110">Create a watcher task</span><span class="sxs-lookup"><span data-stu-id="473de-110">Create a watcher task</span></span>
> * <span data-ttu-id="473de-111">Trigger a watcher</span><span class="sxs-lookup"><span data-stu-id="473de-111">Trigger a watcher</span></span>
> * <span data-ttu-id="473de-112">Inspect the output</span><span class="sxs-lookup"><span data-stu-id="473de-112">Inspect the output</span></span>

## <a name="prerequisites"></a><span data-ttu-id="473de-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="473de-113">Prerequisites</span></span>

<span data-ttu-id="473de-114">To complete this tutorial, the following are required:</span><span class="sxs-lookup"><span data-stu-id="473de-114">To complete this tutorial, the following are required:</span></span>

* <span data-ttu-id="473de-115">Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="473de-115">Azure subscription.</span></span> <span data-ttu-id="473de-116">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="473de-116">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="473de-117">[Automation account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span><span class="sxs-lookup"><span data-stu-id="473de-117">[Automation account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span></span>
* <span data-ttu-id="473de-118">A [hybrid runbook worker](automation-hybrid-runbook-worker.md) where the watcher task runs.</span><span class="sxs-lookup"><span data-stu-id="473de-118">A [hybrid runbook worker](automation-hybrid-runbook-worker.md) where the watcher task runs.</span></span>

## <a name="import-a-watcher-runbook"></a><span data-ttu-id="473de-119">Import a watcher runbook</span><span class="sxs-lookup"><span data-stu-id="473de-119">Import a watcher runbook</span></span>

<span data-ttu-id="473de-120">This tutorial uses a watcher runbook called **Watch-NewFile** to look for new files in a directory.</span><span class="sxs-lookup"><span data-stu-id="473de-120">This tutorial uses a watcher runbook called **Watch-NewFile** to look for new files in a directory.</span></span> <span data-ttu-id="473de-121">The watcher runbook retrieves the last known write time to the files in a folder and looks at any files newer than that watermark.</span><span class="sxs-lookup"><span data-stu-id="473de-121">The watcher runbook retrieves the last known write time to the files in a folder and looks at any files newer than that watermark.</span></span> <span data-ttu-id="473de-122">In this step, you import this runbook into your automation account.</span><span class="sxs-lookup"><span data-stu-id="473de-122">In this step, you import this runbook into your automation account.</span></span>

1. <span data-ttu-id="473de-123">Open your Automation account, and click on the **Runbooks** page.</span><span class="sxs-lookup"><span data-stu-id="473de-123">Open your Automation account, and click on the **Runbooks** page.</span></span>
1. <span data-ttu-id="473de-124">Click on the **Browse gallery** button.</span><span class="sxs-lookup"><span data-stu-id="473de-124">Click on the **Browse gallery** button.</span></span>
1. <span data-ttu-id="473de-125">Search for "Watcher runbook", select **Watcher runbook that looks for new files in a directory** and select **Import**.</span><span class="sxs-lookup"><span data-stu-id="473de-125">Search for "Watcher runbook", select **Watcher runbook that looks for new files in a directory** and select **Import**.</span></span>
  <span data-ttu-id="473de-126">![Import automation runbook from UI](media/automation-watchers-tutorial/importsourcewatcher.png)</span><span class="sxs-lookup"><span data-stu-id="473de-126">![Import automation runbook from UI](media/automation-watchers-tutorial/importsourcewatcher.png)</span></span>
1. <span data-ttu-id="473de-127">Give the runbook a name and description and select **OK** to import the runbook into your Automation account.</span><span class="sxs-lookup"><span data-stu-id="473de-127">Give the runbook a name and description and select **OK** to import the runbook into your Automation account.</span></span>
1. <span data-ttu-id="473de-128">Select **Edit** and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="473de-128">Select **Edit** and then click **Publish**.</span></span> <span data-ttu-id="473de-129">When prompted select **Yes** to publish the runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-129">When prompted select **Yes** to publish the runbook.</span></span>

## <a name="create-an-automation-variable"></a><span data-ttu-id="473de-130">Create an Automation variable</span><span class="sxs-lookup"><span data-stu-id="473de-130">Create an Automation variable</span></span>

<span data-ttu-id="473de-131">An [automation variable](automation-variables.md) is used to store the timestamps that the preceding runbook reads and stores from each file.</span><span class="sxs-lookup"><span data-stu-id="473de-131">An [automation variable](automation-variables.md) is used to store the timestamps that the preceding runbook reads and stores from each file.</span></span> 

1. <span data-ttu-id="473de-132">Select **Variables** under **SHARED RESOURCES** and select **+ Add a variable**.</span><span class="sxs-lookup"><span data-stu-id="473de-132">Select **Variables** under **SHARED RESOURCES** and select **+ Add a variable**.</span></span>
1. <span data-ttu-id="473de-133">Enter "Watch-NewFileTimestamp" for the name</span><span class="sxs-lookup"><span data-stu-id="473de-133">Enter "Watch-NewFileTimestamp" for the name</span></span>
1. <span data-ttu-id="473de-134">Select DateTime for Type.</span><span class="sxs-lookup"><span data-stu-id="473de-134">Select DateTime for Type.</span></span>
1. <span data-ttu-id="473de-135">Click on the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="473de-135">Click on the **Create** button.</span></span> <span data-ttu-id="473de-136">This creates the automation variable.</span><span class="sxs-lookup"><span data-stu-id="473de-136">This creates the automation variable.</span></span>

## <a name="create-an-action-runbook"></a><span data-ttu-id="473de-137">Create an action runbook</span><span class="sxs-lookup"><span data-stu-id="473de-137">Create an action runbook</span></span>

<span data-ttu-id="473de-138">An action runbook is used in a watcher task to act on the data passed to it from a watcher runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-138">An action runbook is used in a watcher task to act on the data passed to it from a watcher runbook.</span></span> <span data-ttu-id="473de-139">In this step, you update import a pre-defined action runbook called "Process-NewFile".</span><span class="sxs-lookup"><span data-stu-id="473de-139">In this step, you update import a pre-defined action runbook called "Process-NewFile".</span></span>

1. <span data-ttu-id="473de-140">Navigate to your automation account and select **Runbooks** under the **PROCESS AUTOMATION** category.</span><span class="sxs-lookup"><span data-stu-id="473de-140">Navigate to your automation account and select **Runbooks** under the **PROCESS AUTOMATION** category.</span></span>
1. <span data-ttu-id="473de-141">Click on the **Browse gallery** button.</span><span class="sxs-lookup"><span data-stu-id="473de-141">Click on the **Browse gallery** button.</span></span>
1. <span data-ttu-id="473de-142">Search for "Watcher action" and select **Watcher action that processes events triggered by a watcher runbook** and select **Import**.</span><span class="sxs-lookup"><span data-stu-id="473de-142">Search for "Watcher action" and select **Watcher action that processes events triggered by a watcher runbook** and select **Import**.</span></span>
  <span data-ttu-id="473de-143">![Import action runbook from UI](media/automation-watchers-tutorial/importsourceaction.png)</span><span class="sxs-lookup"><span data-stu-id="473de-143">![Import action runbook from UI](media/automation-watchers-tutorial/importsourceaction.png)</span></span>
1. <span data-ttu-id="473de-144">Give the runbook a name and description and select **OK** to import the runbook into your Automation account.</span><span class="sxs-lookup"><span data-stu-id="473de-144">Give the runbook a name and description and select **OK** to import the runbook into your Automation account.</span></span>
1. <span data-ttu-id="473de-145">Select **Edit** and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="473de-145">Select **Edit** and then click **Publish**.</span></span> <span data-ttu-id="473de-146">When prompted select **Yes** to publish the runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-146">When prompted select **Yes** to publish the runbook.</span></span>

## <a name="create-a-watcher-task"></a><span data-ttu-id="473de-147">Create a watcher task</span><span class="sxs-lookup"><span data-stu-id="473de-147">Create a watcher task</span></span>

<span data-ttu-id="473de-148">The watcher task contains two parts.</span><span class="sxs-lookup"><span data-stu-id="473de-148">The watcher task contains two parts.</span></span> <span data-ttu-id="473de-149">The watcher and the action.</span><span class="sxs-lookup"><span data-stu-id="473de-149">The watcher and the action.</span></span> <span data-ttu-id="473de-150">The watcher runs at an interval defined in the watcher task.</span><span class="sxs-lookup"><span data-stu-id="473de-150">The watcher runs at an interval defined in the watcher task.</span></span> <span data-ttu-id="473de-151">Data from the watcher runbook is passed onto the action runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-151">Data from the watcher runbook is passed onto the action runbook.</span></span> <span data-ttu-id="473de-152">In this step, you configure the watcher task referencing the watcher and action runbooks defined in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="473de-152">In this step, you configure the watcher task referencing the watcher and action runbooks defined in the preceding steps.</span></span>

1. <span data-ttu-id="473de-153">Navigate to your automation account and select **Watcher tasks** under the **PROCESS AUTOMATION** category.</span><span class="sxs-lookup"><span data-stu-id="473de-153">Navigate to your automation account and select **Watcher tasks** under the **PROCESS AUTOMATION** category.</span></span>
1. <span data-ttu-id="473de-154">Select the Watcher tasks page and click on **+ Add a watcher task** button.</span><span class="sxs-lookup"><span data-stu-id="473de-154">Select the Watcher tasks page and click on **+ Add a watcher task** button.</span></span>
1. <span data-ttu-id="473de-155">Enter "WatchMyFolder" as the name.</span><span class="sxs-lookup"><span data-stu-id="473de-155">Enter "WatchMyFolder" as the name.</span></span>

1. <span data-ttu-id="473de-156">Select **Configure watcher** and select the **Watch-NewFile** runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-156">Select **Configure watcher** and select the **Watch-NewFile** runbook.</span></span>

1. <span data-ttu-id="473de-157">Enter the following values for the parameters:</span><span class="sxs-lookup"><span data-stu-id="473de-157">Enter the following values for the parameters:</span></span>

   * <span data-ttu-id="473de-158">**FOLDERPATH** - A folder on the hybrid worker where new files get created.</span><span class="sxs-lookup"><span data-stu-id="473de-158">**FOLDERPATH** - A folder on the hybrid worker where new files get created.</span></span> <span data-ttu-id="473de-159">d:\examplefiles</span><span class="sxs-lookup"><span data-stu-id="473de-159">d:\examplefiles</span></span>
   * <span data-ttu-id="473de-160">**EXTENSION** - Leave blank to process all file extensions.</span><span class="sxs-lookup"><span data-stu-id="473de-160">**EXTENSION** - Leave blank to process all file extensions.</span></span>
   * <span data-ttu-id="473de-161">**RECURSE** - Leave this value as the default.</span><span class="sxs-lookup"><span data-stu-id="473de-161">**RECURSE** - Leave this value as the default.</span></span>
   * <span data-ttu-id="473de-162">**RUN SETTINGS** - Pick the hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="473de-162">**RUN SETTINGS** - Pick the hybrid worker.</span></span>

1. <span data-ttu-id="473de-163">Click OK, and then Select to return to the watcher page.</span><span class="sxs-lookup"><span data-stu-id="473de-163">Click OK, and then Select to return to the watcher page.</span></span>
1. <span data-ttu-id="473de-164">Select **Configure action** and select "Process-NewFile" runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-164">Select **Configure action** and select "Process-NewFile" runbook.</span></span>
1. <span data-ttu-id="473de-165">Enter the following values for parameters:</span><span class="sxs-lookup"><span data-stu-id="473de-165">Enter the following values for parameters:</span></span>

   *    <span data-ttu-id="473de-166">**EVENTDATA** - Leave blank.</span><span class="sxs-lookup"><span data-stu-id="473de-166">**EVENTDATA** - Leave blank.</span></span> <span data-ttu-id="473de-167">Data is passed in from the watcher runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-167">Data is passed in from the watcher runbook.</span></span>  
   *    <span data-ttu-id="473de-168">**Run Settings** - Leave as Azure as this runbook runs in the Automation service.</span><span class="sxs-lookup"><span data-stu-id="473de-168">**Run Settings** - Leave as Azure as this runbook runs in the Automation service.</span></span>

1. <span data-ttu-id="473de-169">Click **OK**, and then Select to return to the watcher page.</span><span class="sxs-lookup"><span data-stu-id="473de-169">Click **OK**, and then Select to return to the watcher page.</span></span>
1. <span data-ttu-id="473de-170">Click **OK** to create the watcher task.</span><span class="sxs-lookup"><span data-stu-id="473de-170">Click **OK** to create the watcher task.</span></span>

![Configure watcher action from UI](media/automation-watchers-tutorial/watchertaskcreation.png)

## <a name="trigger-a-watcher"></a><span data-ttu-id="473de-172">Trigger a watcher</span><span class="sxs-lookup"><span data-stu-id="473de-172">Trigger a watcher</span></span>

<span data-ttu-id="473de-173">To test the watcher is working as expected, you need to create a test file.</span><span class="sxs-lookup"><span data-stu-id="473de-173">To test the watcher is working as expected, you need to create a test file.</span></span>

<span data-ttu-id="473de-174">Remote into the hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="473de-174">Remote into the hybrid worker.</span></span> <span data-ttu-id="473de-175">Open **PowerShell** and create a test file in the folder.</span><span class="sxs-lookup"><span data-stu-id="473de-175">Open **PowerShell** and create a test file in the folder.</span></span>
  
   ```PowerShell-interactive
   New-Item -Name ExampleFile1.txt
   ```

<span data-ttu-id="473de-176">The following example shows the expected output.</span><span class="sxs-lookup"><span data-stu-id="473de-176">The following example shows the expected output.</span></span>

```
    Directory: D:\examplefiles


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       12/11/2017   9:05 PM              0 ExampleFile1.txt
```

## <a name="inspect-the-output"></a><span data-ttu-id="473de-177">Inspect the output</span><span class="sxs-lookup"><span data-stu-id="473de-177">Inspect the output</span></span>

1. <span data-ttu-id="473de-178">Navigate to your automation account and select **Watcher tasks** under the **PROCESS AUTOMATION** category.</span><span class="sxs-lookup"><span data-stu-id="473de-178">Navigate to your automation account and select **Watcher tasks** under the **PROCESS AUTOMATION** category.</span></span>
1. <span data-ttu-id="473de-179">Select the watcher task "WatchMyFolder".</span><span class="sxs-lookup"><span data-stu-id="473de-179">Select the watcher task "WatchMyFolder".</span></span>
1. <span data-ttu-id="473de-180">Click on **View watcher streams** under **Streams** to see that the watcher found the new file and started the action runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-180">Click on **View watcher streams** under **Streams** to see that the watcher found the new file and started the action runbook.</span></span>
1. <span data-ttu-id="473de-181">To see the action runbook jobs, click on the **View watcher action jobs**.</span><span class="sxs-lookup"><span data-stu-id="473de-181">To see the action runbook jobs, click on the **View watcher action jobs**.</span></span> <span data-ttu-id="473de-182">Each job can be selected the view the details of the job.</span><span class="sxs-lookup"><span data-stu-id="473de-182">Each job can be selected the view the details of the job.</span></span>

   ![Watcher action jobs from UI](media/automation-watchers-tutorial/WatcherActionJobs.png)

<span data-ttu-id="473de-184">The expected output when the new file is found can be seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="473de-184">The expected output when the new file is found can be seen in the following example:</span></span>

```
Message is Process new file...



Passed in data is @{FileName=D:\examplefiles\ExampleFile1.txt; Length=0}
```

## <a name="next-steps"></a><span data-ttu-id="473de-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="473de-185">Next steps</span></span>

<span data-ttu-id="473de-186">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="473de-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="473de-187">Import a watcher runbook</span><span class="sxs-lookup"><span data-stu-id="473de-187">Import a watcher runbook</span></span>
> * <span data-ttu-id="473de-188">Create an Automation variable</span><span class="sxs-lookup"><span data-stu-id="473de-188">Create an Automation variable</span></span>
> * <span data-ttu-id="473de-189">Create an action runbook</span><span class="sxs-lookup"><span data-stu-id="473de-189">Create an action runbook</span></span>
> * <span data-ttu-id="473de-190">Create a watcher task</span><span class="sxs-lookup"><span data-stu-id="473de-190">Create a watcher task</span></span>
> * <span data-ttu-id="473de-191">Trigger a watcher</span><span class="sxs-lookup"><span data-stu-id="473de-191">Trigger a watcher</span></span>
> * <span data-ttu-id="473de-192">Inspect the output</span><span class="sxs-lookup"><span data-stu-id="473de-192">Inspect the output</span></span>

<span data-ttu-id="473de-193">Follow this link to learn more about authoring your own runbook.</span><span class="sxs-lookup"><span data-stu-id="473de-193">Follow this link to learn more about authoring your own runbook.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="473de-194">[My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="473de-194">[My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
