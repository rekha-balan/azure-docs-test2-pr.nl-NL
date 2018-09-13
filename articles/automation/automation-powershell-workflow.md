---
title: Learning PowerShell Workflow for Azure Automation | Microsoft Docs
description: This article is intended as a quick lesson for authors familiar with PowerShell to understand the specific differences between PowerShell and PowerShell Workflow and concepts applicable to Automation runbooks.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 50966ed518b79f2033680790432e29b0c9e7b289
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552827"
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="86532-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span><span class="sxs-lookup"><span data-stu-id="86532-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="86532-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span><span class="sxs-lookup"><span data-stu-id="86532-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="86532-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span><span class="sxs-lookup"><span data-stu-id="86532-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="86532-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span><span class="sxs-lookup"><span data-stu-id="86532-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="86532-107">There are a number of syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span><span class="sxs-lookup"><span data-stu-id="86532-107">There are a number of syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="86532-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span><span class="sxs-lookup"><span data-stu-id="86532-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="86532-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span><span class="sxs-lookup"><span data-stu-id="86532-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="86532-110">A Windows PowerShell Workflow is a Windows PowerShell script that leverages Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="86532-110">A Windows PowerShell Workflow is a Windows PowerShell script that leverages Windows Workflow Foundation.</span></span> <span data-ttu-id="86532-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="86532-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="86532-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="86532-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="86532-113">Basic structure of a workflow</span><span class="sxs-lookup"><span data-stu-id="86532-113">Basic structure of a workflow</span></span>
<span data-ttu-id="86532-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span><span class="sxs-lookup"><span data-stu-id="86532-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="86532-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span><span class="sxs-lookup"><span data-stu-id="86532-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="86532-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax.</span><span class="sxs-lookup"><span data-stu-id="86532-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax.</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="86532-117">The name of the workflow must match the name of the Automation runbook.</span><span class="sxs-lookup"><span data-stu-id="86532-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="86532-118">If the runbook is being imported, then the filename must match the workflow name and must end in .ps1.</span><span class="sxs-lookup"><span data-stu-id="86532-118">If the runbook is being imported, then the filename must match the workflow name and must end in .ps1.</span></span>

<span data-ttu-id="86532-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span><span class="sxs-lookup"><span data-stu-id="86532-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="86532-120">Code changes</span><span class="sxs-lookup"><span data-stu-id="86532-120">Code changes</span></span>
<span data-ttu-id="86532-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span><span class="sxs-lookup"><span data-stu-id="86532-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="86532-122">The following sections describe changes that you will need to make to a PowerShell script for it to run in a workflow.</span><span class="sxs-lookup"><span data-stu-id="86532-122">The following sections describe changes that you will need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="86532-123">Activities</span><span class="sxs-lookup"><span data-stu-id="86532-123">Activities</span></span>
<span data-ttu-id="86532-124">An activity is a specific task in a workflow.</span><span class="sxs-lookup"><span data-stu-id="86532-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="86532-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span><span class="sxs-lookup"><span data-stu-id="86532-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="86532-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span><span class="sxs-lookup"><span data-stu-id="86532-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="86532-127">When you specify one of these cmdlets in your runbook, the corresponding activity is actually run by Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="86532-127">When you specify one of these cmdlets in your runbook, the corresponding activity is actually run by Windows Workflow Foundation.</span></span> <span data-ttu-id="86532-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span><span class="sxs-lookup"><span data-stu-id="86532-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="86532-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span><span class="sxs-lookup"><span data-stu-id="86532-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="86532-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="86532-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="86532-131">Workflow activities share a set of common parameters to configure their operation.</span><span class="sxs-lookup"><span data-stu-id="86532-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="86532-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="86532-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="86532-133">Positional parameters</span><span class="sxs-lookup"><span data-stu-id="86532-133">Positional parameters</span></span>
<span data-ttu-id="86532-134">You can't use positional parameters with activities and cmdlets in a workflow.</span><span class="sxs-lookup"><span data-stu-id="86532-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="86532-135">All this means is that you must use parameter names.</span><span class="sxs-lookup"><span data-stu-id="86532-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="86532-136">For example, consider the following code that gets all running services.</span><span class="sxs-lookup"><span data-stu-id="86532-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="86532-137">If you try to run this same code in a workflow, you'll get a message like "Parameter set cannot be resolved using the specified named parameters."</span><span class="sxs-lookup"><span data-stu-id="86532-137">If you try to run this same code in a workflow, you'll get a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="86532-138">To correct this, simply provide the parameter name as in the following.</span><span class="sxs-lookup"><span data-stu-id="86532-138">To correct this, simply provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="86532-139">Deserialized objects</span><span class="sxs-lookup"><span data-stu-id="86532-139">Deserialized objects</span></span>
<span data-ttu-id="86532-140">Objects in workflows are deserialized.</span><span class="sxs-lookup"><span data-stu-id="86532-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="86532-141">This means that their properties are still available, but not their methods.</span><span class="sxs-lookup"><span data-stu-id="86532-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="86532-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span><span class="sxs-lookup"><span data-stu-id="86532-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="86532-143">If you try to run this in a workflow, you'll get an error saying "Method invocation is not supported in a Windows PowerShell Workflow".</span><span class="sxs-lookup"><span data-stu-id="86532-143">If you try to run this in a workflow, you'll get an error saying "Method invocation is not supported in a Windows PowerShell Workflow".</span></span>  

<span data-ttu-id="86532-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span><span class="sxs-lookup"><span data-stu-id="86532-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="86532-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span><span class="sxs-lookup"><span data-stu-id="86532-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="86532-146">In the case of our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span><span class="sxs-lookup"><span data-stu-id="86532-146">In the case of our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="86532-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="86532-147">InlineScript</span></span>
<span data-ttu-id="86532-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span><span class="sxs-lookup"><span data-stu-id="86532-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="86532-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86532-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="86532-150">InlineScript uses the syntax shown below.</span><span class="sxs-lookup"><span data-stu-id="86532-150">InlineScript uses the syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="86532-151">You can return output from an InlineScript by assigning the output to a variable.</span><span class="sxs-lookup"><span data-stu-id="86532-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="86532-152">The following example stops a service and then outputs the service name.</span><span class="sxs-lookup"><span data-stu-id="86532-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="86532-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span><span class="sxs-lookup"><span data-stu-id="86532-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="86532-154">The following example is identical to the previous example except that the service name is provided by a variable.</span><span class="sxs-lookup"><span data-stu-id="86532-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="86532-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="86532-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="86532-156">You cannot use [checkpoints](#checkpoints) inside of an InlineScript block.</span><span class="sxs-lookup"><span data-stu-id="86532-156">You cannot use [checkpoints](#checkpoints) inside of an InlineScript block.</span></span> <span data-ttu-id="86532-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span><span class="sxs-lookup"><span data-stu-id="86532-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="86532-158">You cannot use [parallel execution](#parallel-processing) inside of an InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="86532-158">You cannot use [parallel execution](#parallel-processing) inside of an InlineScriptBlock.</span></span>
* <span data-ttu-id="86532-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span><span class="sxs-lookup"><span data-stu-id="86532-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="86532-160">For further details on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="86532-160">For further details on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="86532-161">Parallel processing</span><span class="sxs-lookup"><span data-stu-id="86532-161">Parallel processing</span></span>
<span data-ttu-id="86532-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span><span class="sxs-lookup"><span data-stu-id="86532-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="86532-163">You can use the **Parallel** keyword to create a script block with multiple commands that will run concurrently.</span><span class="sxs-lookup"><span data-stu-id="86532-163">You can use the **Parallel** keyword to create a script block with multiple commands that will run concurrently.</span></span> <span data-ttu-id="86532-164">This uses the syntax shown below.</span><span class="sxs-lookup"><span data-stu-id="86532-164">This uses the syntax shown below.</span></span> <span data-ttu-id="86532-165">In this case, Activity1 and Activity2 will start at the same time.</span><span class="sxs-lookup"><span data-stu-id="86532-165">In this case, Activity1 and Activity2 will start at the same time.</span></span> <span data-ttu-id="86532-166">Activity3 will start only after both Activity1 and Activity2 have completed.</span><span class="sxs-lookup"><span data-stu-id="86532-166">Activity3 will start only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="86532-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span><span class="sxs-lookup"><span data-stu-id="86532-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="86532-168">These commands are run sequentially so that one file must finish copying before the next is started.</span><span class="sxs-lookup"><span data-stu-id="86532-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    $Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    $Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    $Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="86532-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span><span class="sxs-lookup"><span data-stu-id="86532-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="86532-170">Only after they are all completely copied is the completion message displayed.</span><span class="sxs-lookup"><span data-stu-id="86532-170">Only after they are all completely copied is the completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            $Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            $Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            $Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="86532-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span><span class="sxs-lookup"><span data-stu-id="86532-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="86532-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span><span class="sxs-lookup"><span data-stu-id="86532-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="86532-173">This uses the syntax shown below.</span><span class="sxs-lookup"><span data-stu-id="86532-173">This uses the syntax shown below.</span></span> <span data-ttu-id="86532-174">In this case, Activity1 will start at the same time for all items in the collection.</span><span class="sxs-lookup"><span data-stu-id="86532-174">In this case, Activity1 will start at the same time for all items in the collection.</span></span> <span data-ttu-id="86532-175">For each item, Activity2 will start after Activity1 is complete.</span><span class="sxs-lookup"><span data-stu-id="86532-175">For each item, Activity2 will start after Activity1 is complete.</span></span> <span data-ttu-id="86532-176">Activity3 will start only after both Activity1 and Activity2 have completed for all items.</span><span class="sxs-lookup"><span data-stu-id="86532-176">Activity3 will start only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="86532-177">The following example is similar to the previous example copying files in parallel.</span><span class="sxs-lookup"><span data-stu-id="86532-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="86532-178">In this case, a message is displayed for each file after it copies.</span><span class="sxs-lookup"><span data-stu-id="86532-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="86532-179">Only after they are all completely copied is the final completion message displayed.</span><span class="sxs-lookup"><span data-stu-id="86532-179">Only after they are all completely copied is the final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            $Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="86532-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span><span class="sxs-lookup"><span data-stu-id="86532-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="86532-181">The output from the child runbook sometimes will not show up, and settings in one child runbook can affect the other parallel child runbooks</span><span class="sxs-lookup"><span data-stu-id="86532-181">The output from the child runbook sometimes will not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="86532-182">Checkpoints</span><span class="sxs-lookup"><span data-stu-id="86532-182">Checkpoints</span></span>
<span data-ttu-id="86532-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span><span class="sxs-lookup"><span data-stu-id="86532-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="86532-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span><span class="sxs-lookup"><span data-stu-id="86532-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="86532-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span><span class="sxs-lookup"><span data-stu-id="86532-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="86532-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span><span class="sxs-lookup"><span data-stu-id="86532-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="86532-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span><span class="sxs-lookup"><span data-stu-id="86532-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="86532-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span><span class="sxs-lookup"><span data-stu-id="86532-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="86532-189">For example, your workflow may create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="86532-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="86532-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="86532-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="86532-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span><span class="sxs-lookup"><span data-stu-id="86532-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="86532-192">If the the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span><span class="sxs-lookup"><span data-stu-id="86532-192">If the the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="86532-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span><span class="sxs-lookup"><span data-stu-id="86532-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="86532-194">If the network location is lost, then the workflow will end in error.</span><span class="sxs-lookup"><span data-stu-id="86532-194">If the network location is lost, then the workflow will end in error.</span></span>  <span data-ttu-id="86532-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied will be skipped.</span><span class="sxs-lookup"><span data-stu-id="86532-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied will be skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            $Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="86532-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span><span class="sxs-lookup"><span data-stu-id="86532-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="86532-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span><span class="sxs-lookup"><span data-stu-id="86532-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="86532-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span><span class="sxs-lookup"><span data-stu-id="86532-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="86532-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span><span class="sxs-lookup"><span data-stu-id="86532-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="86532-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="86532-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86532-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="86532-201">Next steps</span></span>
* <span data-ttu-id="86532-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="86532-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
