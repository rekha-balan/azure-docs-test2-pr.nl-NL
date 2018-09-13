---
title: Azure Automation resources in OMS solutions | Microsoft Docs
description: Solutions in OMS will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.  This article describes how to include runbooks and their related resources in a solution.
services: operations-management-suite
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/17/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a86a20e1e83f412a06f54bb195180b9d2af98ca6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661958"
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="26e44-104">Adding Azure Automation resources to an OMS management solution (Preview)</span><span class="sxs-lookup"><span data-stu-id="26e44-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="26e44-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="26e44-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="26e44-106">Any schema described below is subject to change.</span><span class="sxs-lookup"><span data-stu-id="26e44-106">Any schema described below is subject to change.</span></span>   
> 
> 

<span data-ttu-id="26e44-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span><span class="sxs-lookup"><span data-stu-id="26e44-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="26e44-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span><span class="sxs-lookup"><span data-stu-id="26e44-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="26e44-109">This article describes how to include runbooks and their related resources in a solution.</span><span class="sxs-lookup"><span data-stu-id="26e44-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="26e44-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="26e44-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="26e44-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26e44-111">Prerequisites</span></span>
<span data-ttu-id="26e44-112">This article assumes that you're already familiar with the following information.</span><span class="sxs-lookup"><span data-stu-id="26e44-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="26e44-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="26e44-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="26e44-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="26e44-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="26e44-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="26e44-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="26e44-116">Automation account</span><span class="sxs-lookup"><span data-stu-id="26e44-116">Automation account</span></span>
<span data-ttu-id="26e44-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="26e44-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="26e44-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="26e44-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="26e44-119">If it isn't available, then the solution install will fail.</span><span class="sxs-lookup"><span data-stu-id="26e44-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="26e44-120">The name of each Automation resource includes the name of its Automation account.</span><span class="sxs-lookup"><span data-stu-id="26e44-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="26e44-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span><span class="sxs-lookup"><span data-stu-id="26e44-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="26e44-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="26e44-122">Runbooks</span></span>
<span data-ttu-id="26e44-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="26e44-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="26e44-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span><span class="sxs-lookup"><span data-stu-id="26e44-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="26e44-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="26e44-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="26e44-127">The properties for runbooks are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="26e44-128">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-128">Property</span></span> | <span data-ttu-id="26e44-129">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="26e44-130">runbookType</span></span> |<span data-ttu-id="26e44-131">Specifies the types of the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="26e44-132">Script - PowerShell script</span><span class="sxs-lookup"><span data-stu-id="26e44-132">Script - PowerShell script</span></span> <br><span data-ttu-id="26e44-133">PowerShell - PowerShell workflow</span><span class="sxs-lookup"><span data-stu-id="26e44-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="26e44-134">GraphPowerShell - Graphical PowerShell script runbook</span><span class="sxs-lookup"><span data-stu-id="26e44-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="26e44-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span><span class="sxs-lookup"><span data-stu-id="26e44-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="26e44-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="26e44-136">logProgress</span></span> |<span data-ttu-id="26e44-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="26e44-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="26e44-138">logVerbose</span></span> |<span data-ttu-id="26e44-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="26e44-140">description</span><span class="sxs-lookup"><span data-stu-id="26e44-140">description</span></span> |<span data-ttu-id="26e44-141">Optional description for the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="26e44-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="26e44-142">publishContentLink</span></span> |<span data-ttu-id="26e44-143">Specifies the content of the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="26e44-144">uri - Uri to the content of the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="26e44-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="26e44-146">version - Version of the runbook for your own tracking.</span><span class="sxs-lookup"><span data-stu-id="26e44-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="26e44-147">Automation jobs</span><span class="sxs-lookup"><span data-stu-id="26e44-147">Automation jobs</span></span>
<span data-ttu-id="26e44-148">When you start a runbook in Azure Automation, it creates an automation job.</span><span class="sxs-lookup"><span data-stu-id="26e44-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="26e44-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span><span class="sxs-lookup"><span data-stu-id="26e44-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="26e44-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span><span class="sxs-lookup"><span data-stu-id="26e44-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="26e44-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="26e44-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="26e44-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="26e44-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="26e44-154">The properties for automation jobs are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="26e44-155">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-155">Property</span></span> | <span data-ttu-id="26e44-156">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-157">runbook</span><span class="sxs-lookup"><span data-stu-id="26e44-157">runbook</span></span> |<span data-ttu-id="26e44-158">Single name entity with the name of the runbook to start.</span><span class="sxs-lookup"><span data-stu-id="26e44-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="26e44-159">parameters</span><span class="sxs-lookup"><span data-stu-id="26e44-159">parameters</span></span> |<span data-ttu-id="26e44-160">Entity for each parameter value required by the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="26e44-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="26e44-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span><span class="sxs-lookup"><span data-stu-id="26e44-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="26e44-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span><span class="sxs-lookup"><span data-stu-id="26e44-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="26e44-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span><span class="sxs-lookup"><span data-stu-id="26e44-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="26e44-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="26e44-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="26e44-166">Certificates</span><span class="sxs-lookup"><span data-stu-id="26e44-166">Certificates</span></span>
<span data-ttu-id="26e44-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="26e44-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="26e44-169">The properties for Certificates resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="26e44-170">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-170">Property</span></span> | <span data-ttu-id="26e44-171">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="26e44-172">base64Value</span></span> |<span data-ttu-id="26e44-173">Base 64 value for the certificate.</span><span class="sxs-lookup"><span data-stu-id="26e44-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="26e44-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="26e44-174">thumbprint</span></span> |<span data-ttu-id="26e44-175">Thumbprint for the certificate.</span><span class="sxs-lookup"><span data-stu-id="26e44-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="26e44-176">Credentials</span><span class="sxs-lookup"><span data-stu-id="26e44-176">Credentials</span></span>
<span data-ttu-id="26e44-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="26e44-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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

<span data-ttu-id="26e44-179">The properties for Credential resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="26e44-180">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-180">Property</span></span> | <span data-ttu-id="26e44-181">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-182">userName</span><span class="sxs-lookup"><span data-stu-id="26e44-182">userName</span></span> |<span data-ttu-id="26e44-183">User name for the credential.</span><span class="sxs-lookup"><span data-stu-id="26e44-183">User name for the credential.</span></span> |
| <span data-ttu-id="26e44-184">password</span><span class="sxs-lookup"><span data-stu-id="26e44-184">password</span></span> |<span data-ttu-id="26e44-185">Password for the credential.</span><span class="sxs-lookup"><span data-stu-id="26e44-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="26e44-186">Schedules</span><span class="sxs-lookup"><span data-stu-id="26e44-186">Schedules</span></span>
<span data-ttu-id="26e44-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="26e44-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="26e44-189">The properties for schedule resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="26e44-190">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-190">Property</span></span> | <span data-ttu-id="26e44-191">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-192">description</span><span class="sxs-lookup"><span data-stu-id="26e44-192">description</span></span> |<span data-ttu-id="26e44-193">Optional description for the schedule.</span><span class="sxs-lookup"><span data-stu-id="26e44-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="26e44-194">startTime</span><span class="sxs-lookup"><span data-stu-id="26e44-194">startTime</span></span> |<span data-ttu-id="26e44-195">Specifies the start time of a schedule as a DateTime object.</span><span class="sxs-lookup"><span data-stu-id="26e44-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="26e44-196">A string can be provided if it can be converted to a valid DateTime.</span><span class="sxs-lookup"><span data-stu-id="26e44-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="26e44-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="26e44-197">isEnabled</span></span> |<span data-ttu-id="26e44-198">Specifies whether the schedule is enabled.</span><span class="sxs-lookup"><span data-stu-id="26e44-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="26e44-199">interval</span><span class="sxs-lookup"><span data-stu-id="26e44-199">interval</span></span> |<span data-ttu-id="26e44-200">The type of interval for the schedule.</span><span class="sxs-lookup"><span data-stu-id="26e44-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="26e44-201">day</span><span class="sxs-lookup"><span data-stu-id="26e44-201">day</span></span><br><span data-ttu-id="26e44-202">hour</span><span class="sxs-lookup"><span data-stu-id="26e44-202">hour</span></span> |
| <span data-ttu-id="26e44-203">frequency</span><span class="sxs-lookup"><span data-stu-id="26e44-203">frequency</span></span> |<span data-ttu-id="26e44-204">Frequency that the schedule should fire in number of days or hours.</span><span class="sxs-lookup"><span data-stu-id="26e44-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="26e44-205">Schedules must have a start time with a value greater than the current time.</span><span class="sxs-lookup"><span data-stu-id="26e44-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="26e44-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span><span class="sxs-lookup"><span data-stu-id="26e44-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="26e44-207">Use one of the following two strategies when using schedule resources in a solution.</span><span class="sxs-lookup"><span data-stu-id="26e44-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="26e44-208">Use a parameter for the start time of the schedule.</span><span class="sxs-lookup"><span data-stu-id="26e44-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="26e44-209">This will prompt the user to provide a value when they install the solution.</span><span class="sxs-lookup"><span data-stu-id="26e44-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="26e44-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span><span class="sxs-lookup"><span data-stu-id="26e44-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="26e44-211">Create the schedules using a runbook that starts when the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="26e44-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="26e44-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span><span class="sxs-lookup"><span data-stu-id="26e44-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="26e44-213">Job schedules</span><span class="sxs-lookup"><span data-stu-id="26e44-213">Job schedules</span></span>
<span data-ttu-id="26e44-214">Job schedule resources link a runbook with a schedule.</span><span class="sxs-lookup"><span data-stu-id="26e44-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="26e44-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="26e44-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="26e44-217">The properties for job schedules are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="26e44-218">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-218">Property</span></span> | <span data-ttu-id="26e44-219">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-220">schedule name</span><span class="sxs-lookup"><span data-stu-id="26e44-220">schedule name</span></span> |<span data-ttu-id="26e44-221">Single **name** entity with the name of the schedule.</span><span class="sxs-lookup"><span data-stu-id="26e44-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="26e44-222">runbook name</span><span class="sxs-lookup"><span data-stu-id="26e44-222">runbook name</span></span>  |<span data-ttu-id="26e44-223">Single **name** entity with the name of the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="26e44-224">Variables</span><span class="sxs-lookup"><span data-stu-id="26e44-224">Variables</span></span>
<span data-ttu-id="26e44-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="26e44-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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

<span data-ttu-id="26e44-227">The properties for variable resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="26e44-228">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-228">Property</span></span> | <span data-ttu-id="26e44-229">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-230">description</span><span class="sxs-lookup"><span data-stu-id="26e44-230">description</span></span> | <span data-ttu-id="26e44-231">Optional description for the variable.</span><span class="sxs-lookup"><span data-stu-id="26e44-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="26e44-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="26e44-232">isEncrypted</span></span> | <span data-ttu-id="26e44-233">Specifies whether the variable should be encrypted.</span><span class="sxs-lookup"><span data-stu-id="26e44-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="26e44-234">type</span><span class="sxs-lookup"><span data-stu-id="26e44-234">type</span></span> | <span data-ttu-id="26e44-235">Data type for the variable.</span><span class="sxs-lookup"><span data-stu-id="26e44-235">Data type for the variable.</span></span> |
| <span data-ttu-id="26e44-236">value</span><span class="sxs-lookup"><span data-stu-id="26e44-236">value</span></span> | <span data-ttu-id="26e44-237">Value for the variable.</span><span class="sxs-lookup"><span data-stu-id="26e44-237">Value for the variable.</span></span> |

## <a name="modules"></a><span data-ttu-id="26e44-238">Modules</span><span class="sxs-lookup"><span data-stu-id="26e44-238">Modules</span></span>
<span data-ttu-id="26e44-239">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="26e44-239">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="26e44-240">You do need to include a resource for any other module used by your runbooks.</span><span class="sxs-lookup"><span data-stu-id="26e44-240">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="26e44-241">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="26e44-241">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="26e44-242">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="26e44-242">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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


<span data-ttu-id="26e44-243">The properties for module resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="26e44-243">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="26e44-244">Property</span><span class="sxs-lookup"><span data-stu-id="26e44-244">Property</span></span> | <span data-ttu-id="26e44-245">Description</span><span class="sxs-lookup"><span data-stu-id="26e44-245">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26e44-246">contentLink</span><span class="sxs-lookup"><span data-stu-id="26e44-246">contentLink</span></span> |<span data-ttu-id="26e44-247">Specifies the content of the module.</span><span class="sxs-lookup"><span data-stu-id="26e44-247">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="26e44-248">uri - Uri to the content of the module.</span><span class="sxs-lookup"><span data-stu-id="26e44-248">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="26e44-249">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-249">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="26e44-250">version - Version of the module for your own tracking.</span><span class="sxs-lookup"><span data-stu-id="26e44-250">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="26e44-251">The runbook should depend on the module resource to ensure that it's created before the runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-251">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="26e44-252">Updating modules</span><span class="sxs-lookup"><span data-stu-id="26e44-252">Updating modules</span></span>
<span data-ttu-id="26e44-253">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span><span class="sxs-lookup"><span data-stu-id="26e44-253">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="26e44-254">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span><span class="sxs-lookup"><span data-stu-id="26e44-254">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="26e44-255">This will ensure that any modules are updated as required before the runbooks are loaded.</span><span class="sxs-lookup"><span data-stu-id="26e44-255">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="26e44-256">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span><span class="sxs-lookup"><span data-stu-id="26e44-256">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="26e44-257">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span><span class="sxs-lookup"><span data-stu-id="26e44-257">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="26e44-258">Sample</span><span class="sxs-lookup"><span data-stu-id="26e44-258">Sample</span></span>
<span data-ttu-id="26e44-259">Following is a sample of a solution that include that includes the following resources:</span><span class="sxs-lookup"><span data-stu-id="26e44-259">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="26e44-260">Runbook.</span><span class="sxs-lookup"><span data-stu-id="26e44-260">Runbook.</span></span>  <span data-ttu-id="26e44-261">This is a sample runbook stored in a public GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="26e44-261">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="26e44-262">Automation job that starts the runbook when the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="26e44-262">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="26e44-263">Schedule and job schedule to start the runbook at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="26e44-263">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="26e44-264">Certificate.</span><span class="sxs-lookup"><span data-stu-id="26e44-264">Certificate.</span></span>
- <span data-ttu-id="26e44-265">Credential.</span><span class="sxs-lookup"><span data-stu-id="26e44-265">Credential.</span></span>
- <span data-ttu-id="26e44-266">Variable.</span><span class="sxs-lookup"><span data-stu-id="26e44-266">Variable.</span></span>
- <span data-ttu-id="26e44-267">Module.</span><span class="sxs-lookup"><span data-stu-id="26e44-267">Module.</span></span>  <span data-ttu-id="26e44-268">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="26e44-268">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="26e44-269">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span><span class="sxs-lookup"><span data-stu-id="26e44-269">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


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




## <a name="next-steps"></a><span data-ttu-id="26e44-270">Next steps</span><span class="sxs-lookup"><span data-stu-id="26e44-270">Next steps</span></span>
* <span data-ttu-id="26e44-271">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span><span class="sxs-lookup"><span data-stu-id="26e44-271">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
