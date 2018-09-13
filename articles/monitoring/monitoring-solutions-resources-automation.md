---
title: Azure Automation resources in management solutions | Microsoft Docs
description: Management solutions will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.  This article describes how to include runbooks and their related resources in a solution.
services: monitoring
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 95d5b2499f9e260e6ed134c4191b053325ca3f42
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869687"
---
# <a name="adding-azure-automation-resources-to-a-management-solution-preview"></a><span data-ttu-id="4e189-104">Adding Azure Automation resources to a management solution (Preview)</span><span class="sxs-lookup"><span data-stu-id="4e189-104">Adding Azure Automation resources to a management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="4e189-105">This is preliminary documentation for creating management solutions which are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="4e189-105">This is preliminary documentation for creating management solutions which are currently in preview.</span></span> <span data-ttu-id="4e189-106">Any schema described below is subject to change.</span><span class="sxs-lookup"><span data-stu-id="4e189-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="4e189-107">[Management solutions]( monitoring-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span><span class="sxs-lookup"><span data-stu-id="4e189-107">[Management solutions]( monitoring-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="4e189-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span><span class="sxs-lookup"><span data-stu-id="4e189-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="4e189-109">This article describes how to include runbooks and their related resources in a solution.</span><span class="sxs-lookup"><span data-stu-id="4e189-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4e189-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Design and build a management solution in Azure ]( monitoring-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="4e189-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Design and build a management solution in Azure ]( monitoring-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="4e189-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4e189-111">Prerequisites</span></span>
<span data-ttu-id="4e189-112">This article assumes that you're already familiar with the following information.</span><span class="sxs-lookup"><span data-stu-id="4e189-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="4e189-113">How to [create a management solution]( monitoring-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="4e189-113">How to [create a management solution]( monitoring-solutions-creating.md).</span></span>
- <span data-ttu-id="4e189-114">The structure of a [solution file]( monitoring-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="4e189-114">The structure of a [solution file]( monitoring-solutions-solution-file.md).</span></span>
- <span data-ttu-id="4e189-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="4e189-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="4e189-116">Automation account</span><span class="sxs-lookup"><span data-stu-id="4e189-116">Automation account</span></span>
<span data-ttu-id="4e189-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="4e189-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="4e189-118">As described in [Log Analytics workspace and Automation account]( monitoring-solutions.md#log-analytics-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="4e189-118">As described in [Log Analytics workspace and Automation account]( monitoring-solutions.md#log-analytics-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="4e189-119">If it isn't available, then the solution install will fail.</span><span class="sxs-lookup"><span data-stu-id="4e189-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="4e189-120">The name of each Automation resource includes the name of its Automation account.</span><span class="sxs-lookup"><span data-stu-id="4e189-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="4e189-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span><span class="sxs-lookup"><span data-stu-id="4e189-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="4e189-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="4e189-122">Runbooks</span></span>
<span data-ttu-id="4e189-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="4e189-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="4e189-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span><span class="sxs-lookup"><span data-stu-id="4e189-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="4e189-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="4e189-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="4e189-127">The properties for runbooks are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="4e189-128">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-128">Property</span></span> | <span data-ttu-id="4e189-129">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="4e189-130">runbookType</span></span> |<span data-ttu-id="4e189-131">Specifies the types of the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="4e189-132">Script - PowerShell script</span><span class="sxs-lookup"><span data-stu-id="4e189-132">Script - PowerShell script</span></span> <br><span data-ttu-id="4e189-133">PowerShell - PowerShell workflow</span><span class="sxs-lookup"><span data-stu-id="4e189-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="4e189-134">GraphPowerShell - Graphical PowerShell script runbook</span><span class="sxs-lookup"><span data-stu-id="4e189-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="4e189-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span><span class="sxs-lookup"><span data-stu-id="4e189-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="4e189-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="4e189-136">logProgress</span></span> |<span data-ttu-id="4e189-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="4e189-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="4e189-138">logVerbose</span></span> |<span data-ttu-id="4e189-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="4e189-140">description</span><span class="sxs-lookup"><span data-stu-id="4e189-140">description</span></span> |<span data-ttu-id="4e189-141">Optional description for the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="4e189-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="4e189-142">publishContentLink</span></span> |<span data-ttu-id="4e189-143">Specifies the content of the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="4e189-144">uri - Uri to the content of the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="4e189-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="4e189-146">version - Version of the runbook for your own tracking.</span><span class="sxs-lookup"><span data-stu-id="4e189-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="4e189-147">Automation jobs</span><span class="sxs-lookup"><span data-stu-id="4e189-147">Automation jobs</span></span>
<span data-ttu-id="4e189-148">When you start a runbook in Azure Automation, it creates an automation job.</span><span class="sxs-lookup"><span data-stu-id="4e189-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="4e189-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span><span class="sxs-lookup"><span data-stu-id="4e189-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="4e189-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span><span class="sxs-lookup"><span data-stu-id="4e189-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="4e189-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="4e189-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="4e189-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="4e189-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="4e189-154">The properties for automation jobs are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="4e189-155">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-155">Property</span></span> | <span data-ttu-id="4e189-156">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-157">runbook</span><span class="sxs-lookup"><span data-stu-id="4e189-157">runbook</span></span> |<span data-ttu-id="4e189-158">Single name entity with the name of the runbook to start.</span><span class="sxs-lookup"><span data-stu-id="4e189-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="4e189-159">parameters</span><span class="sxs-lookup"><span data-stu-id="4e189-159">parameters</span></span> |<span data-ttu-id="4e189-160">Entity for each parameter value required by the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="4e189-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="4e189-162">The job should [depend on]( monitoring-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span><span class="sxs-lookup"><span data-stu-id="4e189-162">The job should [depend on]( monitoring-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="4e189-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span><span class="sxs-lookup"><span data-stu-id="4e189-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="4e189-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span><span class="sxs-lookup"><span data-stu-id="4e189-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="4e189-165">You can read more about GUID parameters in [Creating a management solution file in Azure]( monitoring-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="4e189-165">You can read more about GUID parameters in [Creating a management solution file in Azure]( monitoring-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="4e189-166">Certificates</span><span class="sxs-lookup"><span data-stu-id="4e189-166">Certificates</span></span>
<span data-ttu-id="4e189-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="4e189-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="4e189-169">The properties for Certificates resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="4e189-170">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-170">Property</span></span> | <span data-ttu-id="4e189-171">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="4e189-172">base64Value</span></span> |<span data-ttu-id="4e189-173">Base 64 value for the certificate.</span><span class="sxs-lookup"><span data-stu-id="4e189-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="4e189-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="4e189-174">thumbprint</span></span> |<span data-ttu-id="4e189-175">Thumbprint for the certificate.</span><span class="sxs-lookup"><span data-stu-id="4e189-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="4e189-176">Credentials</span><span class="sxs-lookup"><span data-stu-id="4e189-176">Credentials</span></span>
<span data-ttu-id="4e189-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="4e189-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="4e189-179">The properties for Credential resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="4e189-180">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-180">Property</span></span> | <span data-ttu-id="4e189-181">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-182">userName</span><span class="sxs-lookup"><span data-stu-id="4e189-182">userName</span></span> |<span data-ttu-id="4e189-183">User name for the credential.</span><span class="sxs-lookup"><span data-stu-id="4e189-183">User name for the credential.</span></span> |
| <span data-ttu-id="4e189-184">password</span><span class="sxs-lookup"><span data-stu-id="4e189-184">password</span></span> |<span data-ttu-id="4e189-185">Password for the credential.</span><span class="sxs-lookup"><span data-stu-id="4e189-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="4e189-186">Schedules</span><span class="sxs-lookup"><span data-stu-id="4e189-186">Schedules</span></span>
<span data-ttu-id="4e189-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the following structure.</span></span> <span data-ttu-id="4e189-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="4e189-189">The properties for schedule resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="4e189-190">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-190">Property</span></span> | <span data-ttu-id="4e189-191">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-192">description</span><span class="sxs-lookup"><span data-stu-id="4e189-192">description</span></span> |<span data-ttu-id="4e189-193">Optional description for the schedule.</span><span class="sxs-lookup"><span data-stu-id="4e189-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="4e189-194">startTime</span><span class="sxs-lookup"><span data-stu-id="4e189-194">startTime</span></span> |<span data-ttu-id="4e189-195">Specifies the start time of a schedule as a DateTime object.</span><span class="sxs-lookup"><span data-stu-id="4e189-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="4e189-196">A string can be provided if it can be converted to a valid DateTime.</span><span class="sxs-lookup"><span data-stu-id="4e189-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="4e189-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="4e189-197">isEnabled</span></span> |<span data-ttu-id="4e189-198">Specifies whether the schedule is enabled.</span><span class="sxs-lookup"><span data-stu-id="4e189-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="4e189-199">interval</span><span class="sxs-lookup"><span data-stu-id="4e189-199">interval</span></span> |<span data-ttu-id="4e189-200">The type of interval for the schedule.</span><span class="sxs-lookup"><span data-stu-id="4e189-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="4e189-201">day</span><span class="sxs-lookup"><span data-stu-id="4e189-201">day</span></span><br><span data-ttu-id="4e189-202">hour</span><span class="sxs-lookup"><span data-stu-id="4e189-202">hour</span></span> |
| <span data-ttu-id="4e189-203">frequency</span><span class="sxs-lookup"><span data-stu-id="4e189-203">frequency</span></span> |<span data-ttu-id="4e189-204">Frequency that the schedule should fire in number of days or hours.</span><span class="sxs-lookup"><span data-stu-id="4e189-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="4e189-205">Schedules must have a start time with a value greater than the current time.</span><span class="sxs-lookup"><span data-stu-id="4e189-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="4e189-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span><span class="sxs-lookup"><span data-stu-id="4e189-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="4e189-207">Use one of the following two strategies when using schedule resources in a solution.</span><span class="sxs-lookup"><span data-stu-id="4e189-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="4e189-208">Use a parameter for the start time of the schedule.</span><span class="sxs-lookup"><span data-stu-id="4e189-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="4e189-209">This will prompt the user to provide a value when they install the solution.</span><span class="sxs-lookup"><span data-stu-id="4e189-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="4e189-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span><span class="sxs-lookup"><span data-stu-id="4e189-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="4e189-211">Create the schedules using a runbook that starts when the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="4e189-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="4e189-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span><span class="sxs-lookup"><span data-stu-id="4e189-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="4e189-213">Job schedules</span><span class="sxs-lookup"><span data-stu-id="4e189-213">Job schedules</span></span>
<span data-ttu-id="4e189-214">Job schedule resources link a runbook with a schedule.</span><span class="sxs-lookup"><span data-stu-id="4e189-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="4e189-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the following structure.</span></span>  <span data-ttu-id="4e189-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="4e189-217">The properties for job schedules are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="4e189-218">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-218">Property</span></span> | <span data-ttu-id="4e189-219">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-220">schedule name</span><span class="sxs-lookup"><span data-stu-id="4e189-220">schedule name</span></span> |<span data-ttu-id="4e189-221">Single **name** entity with the name of the schedule.</span><span class="sxs-lookup"><span data-stu-id="4e189-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="4e189-222">runbook name</span><span class="sxs-lookup"><span data-stu-id="4e189-222">runbook name</span></span>  |<span data-ttu-id="4e189-223">Single **name** entity with the name of the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="4e189-224">Variables</span><span class="sxs-lookup"><span data-stu-id="4e189-224">Variables</span></span>
<span data-ttu-id="4e189-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="4e189-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="4e189-227">The properties for variable resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="4e189-228">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-228">Property</span></span> | <span data-ttu-id="4e189-229">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-230">description</span><span class="sxs-lookup"><span data-stu-id="4e189-230">description</span></span> | <span data-ttu-id="4e189-231">Optional description for the variable.</span><span class="sxs-lookup"><span data-stu-id="4e189-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="4e189-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="4e189-232">isEncrypted</span></span> | <span data-ttu-id="4e189-233">Specifies whether the variable should be encrypted.</span><span class="sxs-lookup"><span data-stu-id="4e189-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="4e189-234">type</span><span class="sxs-lookup"><span data-stu-id="4e189-234">type</span></span> | <span data-ttu-id="4e189-235">This property currently has no effect.</span><span class="sxs-lookup"><span data-stu-id="4e189-235">This property currently has no effect.</span></span>  <span data-ttu-id="4e189-236">The data type of the variable will be determined by the initial value.</span><span class="sxs-lookup"><span data-stu-id="4e189-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="4e189-237">value</span><span class="sxs-lookup"><span data-stu-id="4e189-237">value</span></span> | <span data-ttu-id="4e189-238">Value for the variable.</span><span class="sxs-lookup"><span data-stu-id="4e189-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="4e189-239">The **type** property currently has no effect on the variable being created.</span><span class="sxs-lookup"><span data-stu-id="4e189-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="4e189-240">The data type for the variable will be determined by the value.</span><span class="sxs-lookup"><span data-stu-id="4e189-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="4e189-241">If you set the initial value for the variable, it must be configured as the correct data type.</span><span class="sxs-lookup"><span data-stu-id="4e189-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="4e189-242">The following table provides the different data types allowable and their syntax.</span><span class="sxs-lookup"><span data-stu-id="4e189-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="4e189-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span><span class="sxs-lookup"><span data-stu-id="4e189-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="4e189-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span><span class="sxs-lookup"><span data-stu-id="4e189-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="4e189-245">Data type</span><span class="sxs-lookup"><span data-stu-id="4e189-245">Data type</span></span> | <span data-ttu-id="4e189-246">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-246">Description</span></span> | <span data-ttu-id="4e189-247">Example</span><span class="sxs-lookup"><span data-stu-id="4e189-247">Example</span></span> | <span data-ttu-id="4e189-248">Resolves to</span><span class="sxs-lookup"><span data-stu-id="4e189-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="4e189-249">string</span><span class="sxs-lookup"><span data-stu-id="4e189-249">string</span></span>   | <span data-ttu-id="4e189-250">Enclose value in double quotes.</span><span class="sxs-lookup"><span data-stu-id="4e189-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="4e189-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="4e189-251">"\"Hello world\""</span></span> | <span data-ttu-id="4e189-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="4e189-252">"Hello world"</span></span> |
| <span data-ttu-id="4e189-253">numeric</span><span class="sxs-lookup"><span data-stu-id="4e189-253">numeric</span></span>  | <span data-ttu-id="4e189-254">Numeric value with single quotes.</span><span class="sxs-lookup"><span data-stu-id="4e189-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="4e189-255">"64"</span><span class="sxs-lookup"><span data-stu-id="4e189-255">"64"</span></span> | <span data-ttu-id="4e189-256">64</span><span class="sxs-lookup"><span data-stu-id="4e189-256">64</span></span> |
| <span data-ttu-id="4e189-257">boolean</span><span class="sxs-lookup"><span data-stu-id="4e189-257">boolean</span></span>  | <span data-ttu-id="4e189-258">**true** or **false** in quotes.</span><span class="sxs-lookup"><span data-stu-id="4e189-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="4e189-259">Note that this value must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="4e189-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="4e189-260">"true"</span><span class="sxs-lookup"><span data-stu-id="4e189-260">"true"</span></span> | <span data-ttu-id="4e189-261">true</span><span class="sxs-lookup"><span data-stu-id="4e189-261">true</span></span> |
| <span data-ttu-id="4e189-262">datetime</span><span class="sxs-lookup"><span data-stu-id="4e189-262">datetime</span></span> | <span data-ttu-id="4e189-263">Serialized date value.</span><span class="sxs-lookup"><span data-stu-id="4e189-263">Serialized date value.</span></span><br><span data-ttu-id="4e189-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span><span class="sxs-lookup"><span data-stu-id="4e189-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="4e189-265">Example: get-date "5/24/2017 13:14:57" \| ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="4e189-265">Example: get-date "5/24/2017 13:14:57" \| ConvertTo-Json</span></span> | <span data-ttu-id="4e189-266">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="4e189-266">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="4e189-267">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="4e189-267">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="4e189-268">Modules</span><span class="sxs-lookup"><span data-stu-id="4e189-268">Modules</span></span>
<span data-ttu-id="4e189-269">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="4e189-269">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="4e189-270">You do need to include a resource for any other module used by your runbooks.</span><span class="sxs-lookup"><span data-stu-id="4e189-270">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="4e189-271">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="4e189-271">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="4e189-272">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="4e189-272">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="4e189-273">The properties for module resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4e189-273">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="4e189-274">Property</span><span class="sxs-lookup"><span data-stu-id="4e189-274">Property</span></span> | <span data-ttu-id="4e189-275">Description</span><span class="sxs-lookup"><span data-stu-id="4e189-275">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e189-276">contentLink</span><span class="sxs-lookup"><span data-stu-id="4e189-276">contentLink</span></span> |<span data-ttu-id="4e189-277">Specifies the content of the module.</span><span class="sxs-lookup"><span data-stu-id="4e189-277">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="4e189-278">uri - Uri to the content of the module.</span><span class="sxs-lookup"><span data-stu-id="4e189-278">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="4e189-279">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-279">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="4e189-280">version - Version of the module for your own tracking.</span><span class="sxs-lookup"><span data-stu-id="4e189-280">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="4e189-281">The runbook should depend on the module resource to ensure that it's created before the runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-281">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="4e189-282">Updating modules</span><span class="sxs-lookup"><span data-stu-id="4e189-282">Updating modules</span></span>
<span data-ttu-id="4e189-283">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span><span class="sxs-lookup"><span data-stu-id="4e189-283">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="4e189-284">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span><span class="sxs-lookup"><span data-stu-id="4e189-284">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="4e189-285">This will ensure that any modules are updated as required before the runbooks are loaded.</span><span class="sxs-lookup"><span data-stu-id="4e189-285">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="4e189-286">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span><span class="sxs-lookup"><span data-stu-id="4e189-286">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="4e189-287">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span><span class="sxs-lookup"><span data-stu-id="4e189-287">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="4e189-288">Sample</span><span class="sxs-lookup"><span data-stu-id="4e189-288">Sample</span></span>
<span data-ttu-id="4e189-289">Following is a sample of a solution that include that includes the following resources:</span><span class="sxs-lookup"><span data-stu-id="4e189-289">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="4e189-290">Runbook.</span><span class="sxs-lookup"><span data-stu-id="4e189-290">Runbook.</span></span>  <span data-ttu-id="4e189-291">This is a sample runbook stored in a public GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="4e189-291">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="4e189-292">Automation job that starts the runbook when the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="4e189-292">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="4e189-293">Schedule and job schedule to start the runbook at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="4e189-293">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="4e189-294">Certificate.</span><span class="sxs-lookup"><span data-stu-id="4e189-294">Certificate.</span></span>
- <span data-ttu-id="4e189-295">Credential.</span><span class="sxs-lookup"><span data-stu-id="4e189-295">Credential.</span></span>
- <span data-ttu-id="4e189-296">Variable.</span><span class="sxs-lookup"><span data-stu-id="4e189-296">Variable.</span></span>
- <span data-ttu-id="4e189-297">Module.</span><span class="sxs-lookup"><span data-stu-id="4e189-297">Module.</span></span>  <span data-ttu-id="4e189-298">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4e189-298">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="4e189-299">The sample uses [standard solution parameters]( monitoring-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span><span class="sxs-lookup"><span data-stu-id="4e189-299">The sample uses [standard solution parameters]( monitoring-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="4e189-300">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e189-300">Next steps</span></span>
* <span data-ttu-id="4e189-301">[Add a view to your solution]( monitoring-solutions-resources-views.md) to visualize collected data.</span><span class="sxs-lookup"><span data-stu-id="4e189-301">[Add a view to your solution]( monitoring-solutions-resources-views.md) to visualize collected data.</span></span>
