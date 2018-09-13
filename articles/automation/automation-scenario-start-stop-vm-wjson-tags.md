---
title: Use JSON-formatted tags to schedule Azure VM state | Microsoft Docs
description: This article demonstrates how to use JSON strings on tags to automate the scheduling of VM startup and shutdown.
services: automation
documentationcenter: ''
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: 1b23264275509fee81acf7362113ca7587709089
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555731"
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="f39c1-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span><span class="sxs-lookup"><span data-stu-id="f39c1-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="f39c1-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span><span class="sxs-lookup"><span data-stu-id="f39c1-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="f39c1-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span><span class="sxs-lookup"><span data-stu-id="f39c1-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="f39c1-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span><span class="sxs-lookup"><span data-stu-id="f39c1-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="f39c1-107">We do have some out-of-the-box options.</span><span class="sxs-lookup"><span data-stu-id="f39c1-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="f39c1-108">These include:</span><span class="sxs-lookup"><span data-stu-id="f39c1-108">These include:</span></span>

* <span data-ttu-id="f39c1-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span><span class="sxs-lookup"><span data-stu-id="f39c1-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="f39c1-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span><span class="sxs-lookup"><span data-stu-id="f39c1-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="f39c1-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span><span class="sxs-lookup"><span data-stu-id="f39c1-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="f39c1-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span><span class="sxs-lookup"><span data-stu-id="f39c1-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="f39c1-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span><span class="sxs-lookup"><span data-stu-id="f39c1-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="f39c1-114">Schedule applied to a resource group</span><span class="sxs-lookup"><span data-stu-id="f39c1-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="f39c1-115">Schedule applied to a resource group and virtual machine in the resource group</span><span class="sxs-lookup"><span data-stu-id="f39c1-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="f39c1-116">Schedule applied to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="f39c1-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="f39c1-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span><span class="sxs-lookup"><span data-stu-id="f39c1-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="f39c1-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span><span class="sxs-lookup"><span data-stu-id="f39c1-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="f39c1-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span><span class="sxs-lookup"><span data-stu-id="f39c1-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="f39c1-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span><span class="sxs-lookup"><span data-stu-id="f39c1-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="f39c1-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="f39c1-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="f39c1-122">Download the runbooks for the scenario</span><span class="sxs-lookup"><span data-stu-id="f39c1-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="f39c1-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span><span class="sxs-lookup"><span data-stu-id="f39c1-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="f39c1-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="f39c1-124">Runbook</span></span> | <span data-ttu-id="f39c1-125">Description</span><span class="sxs-lookup"><span data-stu-id="f39c1-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f39c1-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="f39c1-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="f39c1-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span><span class="sxs-lookup"><span data-stu-id="f39c1-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="f39c1-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="f39c1-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="f39c1-129">Adds the Schedule tag to a VM or resource group.</span><span class="sxs-lookup"><span data-stu-id="f39c1-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="f39c1-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="f39c1-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="f39c1-131">Modifies the existing Schedule tag by replacing it with a new one.</span><span class="sxs-lookup"><span data-stu-id="f39c1-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="f39c1-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="f39c1-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="f39c1-133">Removes the Schedule tag from a VM or resource group.</span><span class="sxs-lookup"><span data-stu-id="f39c1-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="f39c1-134">Install and configure this scenario</span><span class="sxs-lookup"><span data-stu-id="f39c1-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="f39c1-135">Install and publish the runbooks</span><span class="sxs-lookup"><span data-stu-id="f39c1-135">Install and publish the runbooks</span></span>
<span data-ttu-id="f39c1-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="f39c1-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="f39c1-137">Publish each runbook after it has been successfully imported into your Automation account.</span><span class="sxs-lookup"><span data-stu-id="f39c1-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="f39c1-138">Add a schedule to the Test-ResourceSchedule runbook</span><span class="sxs-lookup"><span data-stu-id="f39c1-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="f39c1-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span><span class="sxs-lookup"><span data-stu-id="f39c1-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="f39c1-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span><span class="sxs-lookup"><span data-stu-id="f39c1-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="f39c1-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span><span class="sxs-lookup"><span data-stu-id="f39c1-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="f39c1-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span><span class="sxs-lookup"><span data-stu-id="f39c1-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="f39c1-143">On the **Schedules** blade, click **Add a schedule**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="f39c1-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="f39c1-145">Then select **Create a new schedule**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="f39c1-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="f39c1-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="f39c1-147">For the schedule **Start**, set the start time to an hour increment.</span><span class="sxs-lookup"><span data-stu-id="f39c1-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="f39c1-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="f39c1-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span><span class="sxs-lookup"><span data-stu-id="f39c1-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="f39c1-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="f39c1-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span><span class="sxs-lookup"><span data-stu-id="f39c1-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="f39c1-152">This is the only parameter that's required for the runbook.</span><span class="sxs-lookup"><span data-stu-id="f39c1-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="f39c1-153">When you're finished, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="f39c1-154">The runbook schedule should look like the following when it's completed:</span><span class="sxs-lookup"><span data-stu-id="f39c1-154">The runbook schedule should look like the following when it's completed:</span></span>

![Configured Test-ResourceSchedule runbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="f39c1-156">Format the JSON string</span><span class="sxs-lookup"><span data-stu-id="f39c1-156">Format the JSON string</span></span>
<span data-ttu-id="f39c1-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span><span class="sxs-lookup"><span data-stu-id="f39c1-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="f39c1-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f39c1-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="f39c1-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span><span class="sxs-lookup"><span data-stu-id="f39c1-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="f39c1-160">The following is an example of how the solutions should be formatted:</span><span class="sxs-lookup"><span data-stu-id="f39c1-160">The following is an example of how the solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="f39c1-161">Here is some detailed information about this structure:</span><span class="sxs-lookup"><span data-stu-id="f39c1-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="f39c1-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span><span class="sxs-lookup"><span data-stu-id="f39c1-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="f39c1-163">*TzId* represents the time zone of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f39c1-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="f39c1-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones in PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="f39c1-166">Weekdays are represented with a numeric value of zero to six.</span><span class="sxs-lookup"><span data-stu-id="f39c1-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="f39c1-167">The value zero equals Sunday.</span><span class="sxs-lookup"><span data-stu-id="f39c1-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="f39c1-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span><span class="sxs-lookup"><span data-stu-id="f39c1-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="f39c1-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span><span class="sxs-lookup"><span data-stu-id="f39c1-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="f39c1-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span><span class="sxs-lookup"><span data-stu-id="f39c1-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="f39c1-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span><span class="sxs-lookup"><span data-stu-id="f39c1-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="f39c1-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span><span class="sxs-lookup"><span data-stu-id="f39c1-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="f39c1-173">Tag resource groups or VMs</span><span class="sxs-lookup"><span data-stu-id="f39c1-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="f39c1-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span><span class="sxs-lookup"><span data-stu-id="f39c1-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="f39c1-175">Virtual machines that don't have a Schedule tag are not evaluated.</span><span class="sxs-lookup"><span data-stu-id="f39c1-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="f39c1-176">Therefore, they aren't started or shut down.</span><span class="sxs-lookup"><span data-stu-id="f39c1-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="f39c1-177">There are two ways to tag resource groups or VMs with this solution.</span><span class="sxs-lookup"><span data-stu-id="f39c1-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="f39c1-178">You can do it directly from the portal.</span><span class="sxs-lookup"><span data-stu-id="f39c1-178">You can do it directly from the portal.</span></span> <span data-ttu-id="f39c1-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span><span class="sxs-lookup"><span data-stu-id="f39c1-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="f39c1-180">Tag through the portal</span><span class="sxs-lookup"><span data-stu-id="f39c1-180">Tag through the portal</span></span>
<span data-ttu-id="f39c1-181">Follow these steps to tag a virtual machine or resource group in the portal:</span><span class="sxs-lookup"><span data-stu-id="f39c1-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="f39c1-182">Flatten the JSON string and verify that there aren't any spaces.</span><span class="sxs-lookup"><span data-stu-id="f39c1-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="f39c1-183">Your JSON string should look like this:</span><span class="sxs-lookup"><span data-stu-id="f39c1-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="f39c1-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span><span class="sxs-lookup"><span data-stu-id="f39c1-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![VM tag option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="f39c1-186">Tags are defined following a key/value pair.</span><span class="sxs-lookup"><span data-stu-id="f39c1-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="f39c1-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span><span class="sxs-lookup"><span data-stu-id="f39c1-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="f39c1-188">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f39c1-188">Click **Save**.</span></span> <span data-ttu-id="f39c1-189">Your new tag should now appear in the list of tags for your resource.</span><span class="sxs-lookup"><span data-stu-id="f39c1-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![VM schedule tag](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="f39c1-191">Tag from PowerShell</span><span class="sxs-lookup"><span data-stu-id="f39c1-191">Tag from PowerShell</span></span>
<span data-ttu-id="f39c1-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f39c1-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="f39c1-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f39c1-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="f39c1-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span><span class="sxs-lookup"><span data-stu-id="f39c1-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="f39c1-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f39c1-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f39c1-196">After you complete the setup, you can proceed with the following steps.</span><span class="sxs-lookup"><span data-stu-id="f39c1-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="f39c1-197">Create a schedule tag with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f39c1-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="f39c1-198">Open a PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="f39c1-198">Open a PowerShell session.</span></span> <span data-ttu-id="f39c1-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span><span class="sxs-lookup"><span data-stu-id="f39c1-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="f39c1-200">Define a schedule hash table.</span><span class="sxs-lookup"><span data-stu-id="f39c1-200">Define a schedule hash table.</span></span> <span data-ttu-id="f39c1-201">Here is an example of how it should be constructed:</span><span class="sxs-lookup"><span data-stu-id="f39c1-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="f39c1-202">Define the parameters that are required by the runbook.</span><span class="sxs-lookup"><span data-stu-id="f39c1-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="f39c1-203">In the following example, we are targeting a VM:</span><span class="sxs-lookup"><span data-stu-id="f39c1-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="f39c1-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span><span class="sxs-lookup"><span data-stu-id="f39c1-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="f39c1-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span><span class="sxs-lookup"><span data-stu-id="f39c1-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="f39c1-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f39c1-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="f39c1-207">Remove a schedule tag with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f39c1-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="f39c1-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span><span class="sxs-lookup"><span data-stu-id="f39c1-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="f39c1-209">Define the parameters that are required by the runbook.</span><span class="sxs-lookup"><span data-stu-id="f39c1-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="f39c1-210">In the following example, we are targeting a VM:</span><span class="sxs-lookup"><span data-stu-id="f39c1-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="f39c1-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span><span class="sxs-lookup"><span data-stu-id="f39c1-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="f39c1-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span><span class="sxs-lookup"><span data-stu-id="f39c1-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="f39c1-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f39c1-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="f39c1-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span><span class="sxs-lookup"><span data-stu-id="f39c1-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="f39c1-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span><span class="sxs-lookup"><span data-stu-id="f39c1-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="f39c1-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span><span class="sxs-lookup"><span data-stu-id="f39c1-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="f39c1-217">The **Job Summary** includes messages from the output, warning, and error streams.</span><span class="sxs-lookup"><span data-stu-id="f39c1-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="f39c1-218">Select the **Output** tile to view detailed results from the runbook execution.</span><span class="sxs-lookup"><span data-stu-id="f39c1-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Test-ResourceSchedule Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="f39c1-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="f39c1-220">Next steps</span></span>
* <span data-ttu-id="f39c1-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="f39c1-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="f39c1-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="f39c1-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="f39c1-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="f39c1-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="f39c1-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f39c1-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="f39c1-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="f39c1-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>





