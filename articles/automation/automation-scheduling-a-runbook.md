---
title: Scheduling a runbook in Azure Automation | Microsoft Docs
description: Describes how to create a schedule in Azure Automation so that you can automatically start a runbook at a particular time or on a recurring schedule.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552832"
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="4169b-103">Scheduling a runbook in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4169b-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="4169b-104">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span><span class="sxs-lookup"><span data-stu-id="4169b-104">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="4169b-105">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can additionally schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span><span class="sxs-lookup"><span data-stu-id="4169b-105">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can additionally schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="4169b-106">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span><span class="sxs-lookup"><span data-stu-id="4169b-106">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="4169b-107">Creating a schedule</span><span class="sxs-lookup"><span data-stu-id="4169b-107">Creating a schedule</span></span>
<span data-ttu-id="4169b-108">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4169b-108">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="4169b-109">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4169b-109">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4169b-110">When you associate a schedule with a runbook, Automation stores the current versions of the modules in your account and links them to that schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-110">When you associate a schedule with a runbook, Automation stores the current versions of the modules in your account and links them to that schedule.</span></span>  <span data-ttu-id="4169b-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update the module to version 2.0, the schedule will continue to use 1.0.</span><span class="sxs-lookup"><span data-stu-id="4169b-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update the module to version 2.0, the schedule will continue to use 1.0.</span></span>  <span data-ttu-id="4169b-112">In order to use the updated module version, you must create a new schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-112">In order to use the updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="4169b-113">To create a new schedule in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4169b-113">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="4169b-114">In the Azure classic portal, select Automation and then then select the name of an automation account.</span><span class="sxs-lookup"><span data-stu-id="4169b-114">In the Azure classic portal, select Automation and then then select the name of an automation account.</span></span>
2. <span data-ttu-id="4169b-115">Select the **Assets** tab.</span><span class="sxs-lookup"><span data-stu-id="4169b-115">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="4169b-116">At the bottom of the window, click **Add Setting**.</span><span class="sxs-lookup"><span data-stu-id="4169b-116">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="4169b-117">Click **Add Schedule**.</span><span class="sxs-lookup"><span data-stu-id="4169b-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="4169b-118">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span><span class="sxs-lookup"><span data-stu-id="4169b-118">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="4169b-119">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span><span class="sxs-lookup"><span data-stu-id="4169b-119">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="4169b-120">To create a new schedule in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4169b-120">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="4169b-121">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span><span class="sxs-lookup"><span data-stu-id="4169b-121">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="4169b-122">Click the **Schedules** tile to open the **Schedules** blade.</span><span class="sxs-lookup"><span data-stu-id="4169b-122">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="4169b-123">Click **Add a schedule** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="4169b-123">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="4169b-124">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-124">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="4169b-125">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span><span class="sxs-lookup"><span data-stu-id="4169b-125">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="4169b-126">If you select **Once** specify a **Start time** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4169b-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="4169b-127">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span><span class="sxs-lookup"><span data-stu-id="4169b-127">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="4169b-128">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span><span class="sxs-lookup"><span data-stu-id="4169b-128">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="4169b-129">If you selected **month**, you can choose by **week days** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4169b-129">If you selected **month**, you can choose by **week days** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="4169b-130">To create a new schedule with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4169b-130">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="4169b-131">You can use the [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4169b-131">You can use the [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="4169b-132">You must specify the start time for the schedule and the frequency it should run.</span><span class="sxs-lookup"><span data-stu-id="4169b-132">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="4169b-133">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4169b-133">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="4169b-134">The following sample commands shows how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4169b-134">The following sample commands shows how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="4169b-135">Linking a schedule to a runbook</span><span class="sxs-lookup"><span data-stu-id="4169b-135">Linking a schedule to a runbook</span></span>
<span data-ttu-id="4169b-136">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span><span class="sxs-lookup"><span data-stu-id="4169b-136">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="4169b-137">If a runbook has parameters, then you can provide values for them.</span><span class="sxs-lookup"><span data-stu-id="4169b-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="4169b-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span><span class="sxs-lookup"><span data-stu-id="4169b-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="4169b-139">These values will be used each time the runbook is started by this schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-139">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="4169b-140">You can attach the same runbook to another schedule and specify different parameter values.</span><span class="sxs-lookup"><span data-stu-id="4169b-140">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="4169b-141">To link a schedule to a runbook with the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4169b-141">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="4169b-142">In the Azure classic portal, select **Automation** and then then click the name of an automation account.</span><span class="sxs-lookup"><span data-stu-id="4169b-142">In the Azure classic portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="4169b-143">Select the **Runbooks** tab.</span><span class="sxs-lookup"><span data-stu-id="4169b-143">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="4169b-144">Click on the name of the runbook to schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-144">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="4169b-145">Click the **Schedule** tab.</span><span class="sxs-lookup"><span data-stu-id="4169b-145">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="4169b-146">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span><span class="sxs-lookup"><span data-stu-id="4169b-146">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="4169b-147">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span><span class="sxs-lookup"><span data-stu-id="4169b-147">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="4169b-148">If the runbook has parameters, you will be prompted for their values.</span><span class="sxs-lookup"><span data-stu-id="4169b-148">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="4169b-149">To link a schedule to a runbook with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4169b-149">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="4169b-150">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span><span class="sxs-lookup"><span data-stu-id="4169b-150">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="4169b-151">Click on the name of the runbook to schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-151">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="4169b-152">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-152">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="4169b-153">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span><span class="sxs-lookup"><span data-stu-id="4169b-153">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="4169b-154">To link a schedule to a runbook with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4169b-154">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="4169b-155">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4169b-155">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="4169b-156">You can specify values for the runbook’s parameters with the Parameters parameter.</span><span class="sxs-lookup"><span data-stu-id="4169b-156">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="4169b-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span><span class="sxs-lookup"><span data-stu-id="4169b-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="4169b-158">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span><span class="sxs-lookup"><span data-stu-id="4169b-158">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="4169b-159">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span><span class="sxs-lookup"><span data-stu-id="4169b-159">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="4169b-160">Disabling a schedule</span><span class="sxs-lookup"><span data-stu-id="4169b-160">Disabling a schedule</span></span>
<span data-ttu-id="4169b-161">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-161">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="4169b-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span><span class="sxs-lookup"><span data-stu-id="4169b-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="4169b-163">When the expiration time is reached, the schedule will be disabled.</span><span class="sxs-lookup"><span data-stu-id="4169b-163">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="4169b-164">To disable a schedule from the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4169b-164">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="4169b-165">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span><span class="sxs-lookup"><span data-stu-id="4169b-165">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="4169b-166">In the Azure classic portal, select Automation and then then click the name of an automation account.</span><span class="sxs-lookup"><span data-stu-id="4169b-166">In the Azure classic portal, select Automation and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="4169b-167">Select the Assets tab.</span><span class="sxs-lookup"><span data-stu-id="4169b-167">Select the Assets tab.</span></span>
3. <span data-ttu-id="4169b-168">Click the name of a schedule to open its detail page.</span><span class="sxs-lookup"><span data-stu-id="4169b-168">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="4169b-169">Change **Enabled** to **No**.</span><span class="sxs-lookup"><span data-stu-id="4169b-169">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="4169b-170">To disable a schedule from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4169b-170">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="4169b-171">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span><span class="sxs-lookup"><span data-stu-id="4169b-171">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="4169b-172">Click the **Schedules** tile to open the **Schedules** blade.</span><span class="sxs-lookup"><span data-stu-id="4169b-172">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="4169b-173">Click the name of a schedule to open the details blade.</span><span class="sxs-lookup"><span data-stu-id="4169b-173">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="4169b-174">Change **Enabled** to **No**.</span><span class="sxs-lookup"><span data-stu-id="4169b-174">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="4169b-175">To disable a schedule with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4169b-175">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="4169b-176">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4169b-176">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="4169b-177">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span><span class="sxs-lookup"><span data-stu-id="4169b-177">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="4169b-178">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4169b-178">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="4169b-179">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4169b-179">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="4169b-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="4169b-180">Next steps</span></span>
* <span data-ttu-id="4169b-181">To learn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="4169b-181">To learn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="4169b-182">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="4169b-182">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

