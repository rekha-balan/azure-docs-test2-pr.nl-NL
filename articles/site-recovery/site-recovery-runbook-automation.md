---
title: Add Azure automation runbooks to recovery plans in Site Recovery | Microsoft Docs
description: This article describes how Azure Site Recovery now enables you to extend recovery plans using Azure Automation to complete complex tasks during recovery to Azure
services: site-recovery
documentationcenter: ''
author: ruturaj
manager: gauravd
editor: ''
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: required
ms.date: 02/22/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 858e0c987bbd2f864b8ddf96feed9d296038edf9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556012"
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="27501-103">Add Azure automation runbooks to recovery plans</span><span class="sxs-lookup"><span data-stu-id="27501-103">Add Azure automation runbooks to recovery plans</span></span>
<span data-ttu-id="27501-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span><span class="sxs-lookup"><span data-stu-id="27501-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="27501-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span><span class="sxs-lookup"><span data-stu-id="27501-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="27501-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span><span class="sxs-lookup"><span data-stu-id="27501-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="27501-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span><span class="sxs-lookup"><span data-stu-id="27501-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="27501-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="27501-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="27501-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="27501-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="27501-110">In this tutorial, we look at how you can integrate Azure Automation runbooks into recovery plans.</span><span class="sxs-lookup"><span data-stu-id="27501-110">In this tutorial, we look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="27501-111">We automate simple tasks that earlier required manual intervention and see how to convert a multi-step recovery into a single-click recovery action.</span><span class="sxs-lookup"><span data-stu-id="27501-111">We automate simple tasks that earlier required manual intervention and see how to convert a multi-step recovery into a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="27501-112">Customize the recovery plan</span><span class="sxs-lookup"><span data-stu-id="27501-112">Customize the recovery plan</span></span>
1. <span data-ttu-id="27501-113">Let us begin by operning the resource blade of the recovery plan.</span><span class="sxs-lookup"><span data-stu-id="27501-113">Let us begin by operning the resource blade of the recovery plan.</span></span> <span data-ttu-id="27501-114">You can see the recovery plan has two virtual machines added to it for recovery.</span><span class="sxs-lookup"><span data-stu-id="27501-114">You can see the recovery plan has two virtual machines added to it for recovery.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/essentials-rp.PNG)
- - -
1. <span data-ttu-id="27501-115">Click the customize button to begin adding a runbook.</span><span class="sxs-lookup"><span data-stu-id="27501-115">Click the customize button to begin adding a runbook.</span></span> 

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/customize-rp.PNG)


1. <span data-ttu-id="27501-116">Right-click on the start group 1 and select to add a 'Add post action'.</span><span class="sxs-lookup"><span data-stu-id="27501-116">Right-click on the start group 1 and select to add a 'Add post action'.</span></span>
2. <span data-ttu-id="27501-117">Select to choose a script in the new blade.</span><span class="sxs-lookup"><span data-stu-id="27501-117">Select to choose a script in the new blade.</span></span>
3. <span data-ttu-id="27501-118">Name the script 'Hello World'.</span><span class="sxs-lookup"><span data-stu-id="27501-118">Name the script 'Hello World'.</span></span>
4. <span data-ttu-id="27501-119">Choose an Automation Account name.</span><span class="sxs-lookup"><span data-stu-id="27501-119">Choose an Automation Account name.</span></span> 
    >[!NOTE]
    > <span data-ttu-id="27501-120">Automation account can be in any Azure geography but has to be in the same subscription as the Site Recovery vault.</span><span class="sxs-lookup"><span data-stu-id="27501-120">Automation account can be in any Azure geography but has to be in the same subscription as the Site Recovery vault.</span></span>
    
5. <span data-ttu-id="27501-121">Select a runbook from the Automation Account.</span><span class="sxs-lookup"><span data-stu-id="27501-121">Select a runbook from the Automation Account.</span></span> <span data-ttu-id="27501-122">This runbook is the script that will run during the execution of the recovery plan after the recovery of first group.</span><span class="sxs-lookup"><span data-stu-id="27501-122">This runbook is the script that will run during the execution of the recovery plan after the recovery of first group.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/update-rp.PNG)
6. <span data-ttu-id="27501-123">Select OK to save the script.</span><span class="sxs-lookup"><span data-stu-id="27501-123">Select OK to save the script.</span></span> <span data-ttu-id="27501-124">Script is added to the post action group of Group 1: Start.</span><span class="sxs-lookup"><span data-stu-id="27501-124">Script is added to the post action group of Group 1: Start.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="salient-points-of-adding-a-script"></a><span data-ttu-id="27501-125">Salient points of adding a script</span><span class="sxs-lookup"><span data-stu-id="27501-125">Salient points of adding a script</span></span>
1. <span data-ttu-id="27501-126">You can right click the script and choose to 'delete step' or 'update script'.</span><span class="sxs-lookup"><span data-stu-id="27501-126">You can right click the script and choose to 'delete step' or 'update script'.</span></span>
2. <span data-ttu-id="27501-127">A script can run on the Azure while failover from On-premises to Azure, and can run on Azure as a primary side script before shutdown, during failback from Azure to on-premises.</span><span class="sxs-lookup"><span data-stu-id="27501-127">A script can run on the Azure while failover from On-premises to Azure, and can run on Azure as a primary side script before shutdown, during failback from Azure to on-premises.</span></span>
3. <span data-ttu-id="27501-128">When a script runs, it injects a recovery plan context.</span><span class="sxs-lookup"><span data-stu-id="27501-128">When a script runs, it injects a recovery plan context.</span></span>

<span data-ttu-id="27501-129">Following is an example of how the context variable looks.</span><span class="sxs-lookup"><span data-stu-id="27501-129">Following is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",
                
                "ResourceGroupName":"ContosoRG",
                
                "CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test",
                
                "RecoveryPointId":"TimeStamp"}

                }

        }


<span data-ttu-id="27501-130">The following table contains name and description for each variable in the context.</span><span class="sxs-lookup"><span data-stu-id="27501-130">The following table contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="27501-131">**Variable name**</span><span class="sxs-lookup"><span data-stu-id="27501-131">**Variable name**</span></span> | <span data-ttu-id="27501-132">**Description**</span><span class="sxs-lookup"><span data-stu-id="27501-132">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="27501-133">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="27501-133">RecoveryPlanName</span></span> |<span data-ttu-id="27501-134">Name of plan being run.</span><span class="sxs-lookup"><span data-stu-id="27501-134">Name of plan being run.</span></span> <span data-ttu-id="27501-135">This variable helps you to take different actions based on name and by reusing the script</span><span class="sxs-lookup"><span data-stu-id="27501-135">This variable helps you to take different actions based on name and by reusing the script</span></span> |
| <span data-ttu-id="27501-136">FailoverType</span><span class="sxs-lookup"><span data-stu-id="27501-136">FailoverType</span></span> |<span data-ttu-id="27501-137">Specifies whether the failover is test, planned, or unplanned.</span><span class="sxs-lookup"><span data-stu-id="27501-137">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="27501-138">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="27501-138">FailoverDirection</span></span> |<span data-ttu-id="27501-139">Specify whether recovery is to primary or secondary</span><span class="sxs-lookup"><span data-stu-id="27501-139">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="27501-140">GroupID</span><span class="sxs-lookup"><span data-stu-id="27501-140">GroupID</span></span> |<span data-ttu-id="27501-141">Identify the group number within the recovery plan when the plan is running</span><span class="sxs-lookup"><span data-stu-id="27501-141">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="27501-142">VmMap</span><span class="sxs-lookup"><span data-stu-id="27501-142">VmMap</span></span> |<span data-ttu-id="27501-143">Array of all the virtual machines in the group</span><span class="sxs-lookup"><span data-stu-id="27501-143">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="27501-144">VMMap key</span><span class="sxs-lookup"><span data-stu-id="27501-144">VMMap key</span></span> |<span data-ttu-id="27501-145">Unique key (GUID) for each VM.</span><span class="sxs-lookup"><span data-stu-id="27501-145">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="27501-146">It's the same as the VMM ID of the virtual machine where applicable.</span><span class="sxs-lookup"><span data-stu-id="27501-146">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="27501-147">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="27501-147">SubscriptionId</span></span> |<span data-ttu-id="27501-148">Azure Subscription ID in which the VM is created.</span><span class="sxs-lookup"><span data-stu-id="27501-148">Azure Subscription ID in which the VM is created.</span></span> |
| <span data-ttu-id="27501-149">RoleName</span><span class="sxs-lookup"><span data-stu-id="27501-149">RoleName</span></span> |<span data-ttu-id="27501-150">Name of the Azure VM that's being recovered</span><span class="sxs-lookup"><span data-stu-id="27501-150">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="27501-151">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="27501-151">CloudServiceName</span></span> |<span data-ttu-id="27501-152">Azure Cloud Service name under which the virtual machine is created.</span><span class="sxs-lookup"><span data-stu-id="27501-152">Azure Cloud Service name under which the virtual machine is created.</span></span> |
| <span data-ttu-id="27501-153">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="27501-153">ResourceGroupName</span></span>|<span data-ttu-id="27501-154">Azure Resource Group name under which the virtual machine is created.</span><span class="sxs-lookup"><span data-stu-id="27501-154">Azure Resource Group name under which the virtual machine is created.</span></span> |
| <span data-ttu-id="27501-155">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="27501-155">RecoveryPointId</span></span>|<span data-ttu-id="27501-156">Timestamp to which the VM is recovered.</span><span class="sxs-lookup"><span data-stu-id="27501-156">Timestamp to which the VM is recovered.</span></span> |

<span data-ttu-id="27501-157">You also need to ensure that the Automation Account has the following modules added.</span><span class="sxs-lookup"><span data-stu-id="27501-157">You also need to ensure that the Automation Account has the following modules added.</span></span> <span data-ttu-id="27501-158">All the modules should be of compatible versions.</span><span class="sxs-lookup"><span data-stu-id="27501-158">All the modules should be of compatible versions.</span></span> <span data-ttu-id="27501-159">An easy way is to make sure all modules are at the latest version available.</span><span class="sxs-lookup"><span data-stu-id="27501-159">An easy way is to make sure all modules are at the latest version available.</span></span>
* <span data-ttu-id="27501-160">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="27501-160">AzureRM.profile</span></span>
* <span data-ttu-id="27501-161">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="27501-161">AzureRM.Resources</span></span>
* <span data-ttu-id="27501-162">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="27501-162">AzureRM.Automation</span></span>
* <span data-ttu-id="27501-163">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="27501-163">AzureRM.Network</span></span>
* <span data-ttu-id="27501-164">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="27501-164">AzureRM.Compute</span></span>


### <a name="accessing-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="27501-165">Accessing all VMs of the VmMap in a loop</span><span class="sxs-lookup"><span data-stu-id="27501-165">Accessing all VMs of the VmMap in a loop</span></span>
<span data-ttu-id="27501-166">Use the following snippet to loop across all VMs of the VmMap.</span><span class="sxs-lookup"><span data-stu-id="27501-166">Use the following snippet to loop across all VMs of the VmMap.</span></span>

```
    $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
    $vmMap = $RecoveryPlanContext.VmMap
     foreach($VMID in $VMinfo)
     {
         $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
             #this check is to ensure that we skip when some data is not available else it will fail
         Write-output "Resource group name ", $VM.ResourceGroupName
         Write-output "Rolename " = $VM.RoleName
         }
     }

```

> [!NOTE]
> <span data-ttu-id="27501-167">The Resource Group name and the Role name values are empty when the script is a pre-action to a boot group.</span><span class="sxs-lookup"><span data-stu-id="27501-167">The Resource Group name and the Role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="27501-168">The values are populated only if the VM of that group succeeds in failover and the script is a post-action of the boot group.</span><span class="sxs-lookup"><span data-stu-id="27501-168">The values are populated only if the VM of that group succeeds in failover and the script is a post-action of the boot group.</span></span>

## <a name="using-the-same-automation-runbook-with-multiple-recovery-plans"></a><span data-ttu-id="27501-169">Using the same Automation runbook with multiple recovery plans</span><span class="sxs-lookup"><span data-stu-id="27501-169">Using the same Automation runbook with multiple recovery plans</span></span>

<span data-ttu-id="27501-170">A single script can be used across multiple recovery plans by using external variables.</span><span class="sxs-lookup"><span data-stu-id="27501-170">A single script can be used across multiple recovery plans by using external variables.</span></span> <span data-ttu-id="27501-171">You can use the [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span><span class="sxs-lookup"><span data-stu-id="27501-171">You can use the [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="27501-172">By pre-fixing the variable with the name of the recovery plan, you can create individual variables for every recovery plan and use them as a parameter.</span><span class="sxs-lookup"><span data-stu-id="27501-172">By pre-fixing the variable with the name of the recovery plan, you can create individual variables for every recovery plan and use them as a parameter.</span></span> <span data-ttu-id="27501-173">You can change the parameter without changing the script and make the script work differently.</span><span class="sxs-lookup"><span data-stu-id="27501-173">You can change the parameter without changing the script and make the script work differently.</span></span>

### <a name="using-simple-string-variables-in-runbook-script"></a><span data-ttu-id="27501-174">Using simple string variables in runbook script</span><span class="sxs-lookup"><span data-stu-id="27501-174">Using simple string variables in runbook script</span></span>

<span data-ttu-id="27501-175">Consider script that takes the input of an NSG and applies it to the VMs of a recovery plan.</span><span class="sxs-lookup"><span data-stu-id="27501-175">Consider script that takes the input of an NSG and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="27501-176">For the script to understand which recovery plan is executing, you can use the Recovery Plan Context.</span><span class="sxs-lookup"><span data-stu-id="27501-176">For the script to understand which recovery plan is executing, you can use the Recovery Plan Context.</span></span>

```
    workflow AddPublicIPAndNSG {
        param (
              [parameter(Mandatory=$false)]
              [Object]$RecoveryPlanContext
        )

        $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="27501-177">To apply an existing NSG, you need the NSG name and the NSG resource group.</span><span class="sxs-lookup"><span data-stu-id="27501-177">To apply an existing NSG, you need the NSG name and the NSG resource group.</span></span> <span data-ttu-id="27501-178">We provide these variables as an input for the recovery plan scripts.</span><span class="sxs-lookup"><span data-stu-id="27501-178">We provide these variables as an input for the recovery plan scripts.</span></span> <span data-ttu-id="27501-179">To do this, create two variables in the Automation accounts assets and prefix it with the name of the recovery plan for which you are creating the parameters.</span><span class="sxs-lookup"><span data-stu-id="27501-179">To do this, create two variables in the Automation accounts assets and prefix it with the name of the recovery plan for which you are creating the parameters.</span></span>

1. <span data-ttu-id="27501-180">Create a variable to store the NSG name.</span><span class="sxs-lookup"><span data-stu-id="27501-180">Create a variable to store the NSG name.</span></span> <span data-ttu-id="27501-181">Prefix it with the name of the recovery plan.</span><span class="sxs-lookup"><span data-stu-id="27501-181">Prefix it with the name of the recovery plan.</span></span>
    <span data-ttu-id="27501-182">![Create NSG name variable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/var1.png)</span><span class="sxs-lookup"><span data-stu-id="27501-182">![Create NSG name variable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/var1.png)</span></span>

2. <span data-ttu-id="27501-183">Create a variable to store the NSG's RG name.</span><span class="sxs-lookup"><span data-stu-id="27501-183">Create a variable to store the NSG's RG name.</span></span> <span data-ttu-id="27501-184">Prefix it with the name of the recovery plan.</span><span class="sxs-lookup"><span data-stu-id="27501-184">Prefix it with the name of the recovery plan.</span></span>
    <span data-ttu-id="27501-185">![Create NSG RG name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/var2.png)</span><span class="sxs-lookup"><span data-stu-id="27501-185">![Create NSG RG name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/var2.png)</span></span>


<span data-ttu-id="27501-186">In the script, acquire the variables' values by using the following reference code:</span><span class="sxs-lookup"><span data-stu-id="27501-186">In the script, acquire the variables' values by using the following reference code:</span></span>

```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue 
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
```

<span data-ttu-id="27501-187">Next you can use the variables in the runbook and apply the NSG to the Network Interface of the failed over virtual machine.</span><span class="sxs-lookup"><span data-stu-id="27501-187">Next you can use the variables in the runbook and apply the NSG to the Network Interface of the failed over virtual machine.</span></span>

```
     InlineScript { 
        if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
```

<span data-ttu-id="27501-188">For each recovery plan, create independent variables so that you can reuse the script and prefix it wih the recovery plan name.</span><span class="sxs-lookup"><span data-stu-id="27501-188">For each recovery plan, create independent variables so that you can reuse the script and prefix it wih the recovery plan name.</span></span> <span data-ttu-id="27501-189">A complete end to end script for this example is [given here](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="27501-189">A complete end to end script for this example is [given here](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="using-complex-variable-to-store-more-information"></a><span data-ttu-id="27501-190">Using complex variable to store more information</span><span class="sxs-lookup"><span data-stu-id="27501-190">Using complex variable to store more information</span></span>

<span data-ttu-id="27501-191">Consider a scenario where you want just one script to turn on a public IP on specific VMs Another example would be to apply different NSGs on different virtual machines (not all).</span><span class="sxs-lookup"><span data-stu-id="27501-191">Consider a scenario where you want just one script to turn on a public IP on specific VMs Another example would be to apply different NSGs on different virtual machines (not all).</span></span> <span data-ttu-id="27501-192">This script should be reusable for any other recovery plan.</span><span class="sxs-lookup"><span data-stu-id="27501-192">This script should be reusable for any other recovery plan.</span></span> <span data-ttu-id="27501-193">Each recovery plan can have variable number of virtual machines (example, a sharepoint recovery has two front ends, a simple LOB application has only one front end).</span><span class="sxs-lookup"><span data-stu-id="27501-193">Each recovery plan can have variable number of virtual machines (example, a sharepoint recovery has two front ends, a simple LOB application has only one front end).</span></span> <span data-ttu-id="27501-194">To achieve this result, it is impossible to create separate variables per recovery plan.</span><span class="sxs-lookup"><span data-stu-id="27501-194">To achieve this result, it is impossible to create separate variables per recovery plan.</span></span> <span data-ttu-id="27501-195">Here we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets, by specifying multiple values.</span><span class="sxs-lookup"><span data-stu-id="27501-195">Here we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets, by specifying multiple values.</span></span> <span data-ttu-id="27501-196">You need the Azure powershell to execute the following steps.</span><span class="sxs-lookup"><span data-stu-id="27501-196">You need the Azure powershell to execute the following steps.</span></span>

1. <span data-ttu-id="27501-197">On the Azure powershell login to your subscription.</span><span class="sxs-lookup"><span data-stu-id="27501-197">On the Azure powershell login to your subscription.</span></span>

    ```
        login-azurermaccount
        $sub = Get-AzureRmSubscription -Name <SubscriptionName>
        $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="27501-198">To store the parameters, create the complex variable with the same name as the recovery plan.</span><span class="sxs-lookup"><span data-stu-id="27501-198">To store the parameters, create the complex variable with the same name as the recovery plan.</span></span>

    ```
        $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

    <span data-ttu-id="27501-199">In this complex variable, \**VMDetails* is the VM ID for the protected virtual machine.</span><span class="sxs-lookup"><span data-stu-id="27501-199">In this complex variable, \**VMDetails* is the VM ID for the protected virtual machine.</span></span> <span data-ttu-id="27501-200">You can find this in the properties of the virtual machine on the portal.</span><span class="sxs-lookup"><span data-stu-id="27501-200">You can find this in the properties of the virtual machine on the portal.</span></span> <span data-ttu-id="27501-201">Here we have created a variable to store the details of two virtual machines.</span><span class="sxs-lookup"><span data-stu-id="27501-201">Here we have created a variable to store the details of two virtual machines.</span></span>

    ![VM's ID to be used as GUID](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-runbook-automation-new/vmguid.png)

3. <span data-ttu-id="27501-203">Use this variable in your runbook and apply the NSG on the virtual machine if any of the given VMGUID is found in the recovery plan context.</span><span class="sxs-lookup"><span data-stu-id="27501-203">Use this variable in your runbook and apply the NSG on the virtual machine if any of the given VMGUID is found in the recovery plan context.</span></span>

    ```
        $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName 
    ```

4. <span data-ttu-id="27501-204">In your runbook, loop through the VMs of the recovery plan context and check if the VM also exists in **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="27501-204">In your runbook, loop through the VMs of the recovery plan context and check if the VM also exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="27501-205">If it exists, apply the NSG by accessing the properties of the variable.</span><span class="sxs-lookup"><span data-stu-id="27501-205">If it exists, apply the NSG by accessing the properties of the variable.</span></span>
    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap
           
        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID
            
            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="27501-206">You can use the same script with different recovery plans and provide different parameters by storing the value corresponding to different recovery plans in different variable.</span><span class="sxs-lookup"><span data-stu-id="27501-206">You can use the same script with different recovery plans and provide different parameters by storing the value corresponding to different recovery plans in different variable.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="27501-207">Sample scripts</span><span class="sxs-lookup"><span data-stu-id="27501-207">Sample scripts</span></span>
<span data-ttu-id="27501-208">Deploy sample scripts into your Automation account using the Deploy to Azure button below.</span><span class="sxs-lookup"><span data-stu-id="27501-208">Deploy sample scripts into your Automation account using the Deploy to Azure button below.</span></span>

<span data-ttu-id="27501-209">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="27501-209">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="27501-210">Also view a quick video about recovering a two tier WordPress application to Azure.</span><span class="sxs-lookup"><span data-stu-id="27501-210">Also view a quick video about recovering a two tier WordPress application to Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="27501-211">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="27501-211">Additional Resources</span></span>
[<span data-ttu-id="27501-212">Azure Automation Service Run as Account</span><span class="sxs-lookup"><span data-stu-id="27501-212">Azure Automation Service Run as Account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

[<span data-ttu-id="27501-213">Azure Automation Overview</span><span class="sxs-lookup"><span data-stu-id="27501-213">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Automation Overview")

[<span data-ttu-id="27501-214">Sample Azure Automation Scripts</span><span class="sxs-lookup"><span data-stu-id="27501-214">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Sample Azure Automation Scripts")







