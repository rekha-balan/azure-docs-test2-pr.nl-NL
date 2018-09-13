---
title: Creating a management solution file in Azure | Microsoft Docs
description: Management solutions provide packaged management scenarios that customers can add to their Azure environment.  This article provides details on how you can create management solutions to be used in your own environment or made available to your customers.
services: monitoring
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/09/2018
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 46e6ea791752045b0f1afbf1e83e43f498415e54
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867167"
---
# <a name="creating-a-management-solution-file-in-azure-preview"></a><span data-ttu-id="29675-104">Creating a management solution file in Azure (Preview)</span><span class="sxs-lookup"><span data-stu-id="29675-104">Creating a management solution file in Azure (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="29675-105">This is preliminary documentation for creating management solutions in Azure which are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="29675-105">This is preliminary documentation for creating management solutions in Azure which are currently in preview.</span></span> <span data-ttu-id="29675-106">Any schema described below is subject to change.</span><span class="sxs-lookup"><span data-stu-id="29675-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="29675-107">Management solutions in Azure are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="29675-107">Management solutions in Azure are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="29675-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="29675-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="29675-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span><span class="sxs-lookup"><span data-stu-id="29675-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="29675-110">Tools</span><span class="sxs-lookup"><span data-stu-id="29675-110">Tools</span></span>

<span data-ttu-id="29675-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span><span class="sxs-lookup"><span data-stu-id="29675-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="29675-112">Creating and deploying Azure resource groups through Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29675-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="29675-113">Working with Azure Resource Manager Templates in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="29675-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="29675-114">Structure</span><span class="sxs-lookup"><span data-stu-id="29675-114">Structure</span></span>
<span data-ttu-id="29675-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format), which is as follows.</span><span class="sxs-lookup"><span data-stu-id="29675-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format), which is as follows.</span></span>  <span data-ttu-id="29675-116">Each of the sections below describes the top-level elements and their contents in a solution.</span><span class="sxs-lookup"><span data-stu-id="29675-116">Each of the sections below describes the top-level elements and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="29675-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="29675-117">Parameters</span></span>
<span data-ttu-id="29675-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span><span class="sxs-lookup"><span data-stu-id="29675-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="29675-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span><span class="sxs-lookup"><span data-stu-id="29675-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="29675-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span><span class="sxs-lookup"><span data-stu-id="29675-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="29675-121">When a user [installs your management solution](monitoring-solutions.md#install-a-management-solution) through the Azure Marketplace or Azure QuickStart templates they are prompted to select a [Log Analytics workspace and Automation account](monitoring-solutions.md#log-analytics-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="29675-121">When a user [installs your management solution](monitoring-solutions.md#install-a-management-solution) through the Azure Marketplace or Azure QuickStart templates they are prompted to select a [Log Analytics workspace and Automation account](monitoring-solutions.md#log-analytics-workspace-and-automation-account).</span></span>  <span data-ttu-id="29675-122">These are used to populate the values of each of the standard parameters.</span><span class="sxs-lookup"><span data-stu-id="29675-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="29675-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span><span class="sxs-lookup"><span data-stu-id="29675-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>


<span data-ttu-id="29675-124">A sample parameter is shown below.</span><span class="sxs-lookup"><span data-stu-id="29675-124">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="29675-125">The following table describes the attributes of a parameter.</span><span class="sxs-lookup"><span data-stu-id="29675-125">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="29675-126">Attribute</span><span class="sxs-lookup"><span data-stu-id="29675-126">Attribute</span></span> | <span data-ttu-id="29675-127">Description</span><span class="sxs-lookup"><span data-stu-id="29675-127">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="29675-128">type</span><span class="sxs-lookup"><span data-stu-id="29675-128">type</span></span> |<span data-ttu-id="29675-129">Data type for the parameter.</span><span class="sxs-lookup"><span data-stu-id="29675-129">Data type for the parameter.</span></span> <span data-ttu-id="29675-130">The input control displayed for the user depends on the data type.</span><span class="sxs-lookup"><span data-stu-id="29675-130">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="29675-131">bool - Drop down box</span><span class="sxs-lookup"><span data-stu-id="29675-131">bool - Drop down box</span></span><br><span data-ttu-id="29675-132">string - Text box</span><span class="sxs-lookup"><span data-stu-id="29675-132">string - Text box</span></span><br><span data-ttu-id="29675-133">int - Text box</span><span class="sxs-lookup"><span data-stu-id="29675-133">int - Text box</span></span><br><span data-ttu-id="29675-134">securestring - Password field</span><span class="sxs-lookup"><span data-stu-id="29675-134">securestring - Password field</span></span><br> |
| <span data-ttu-id="29675-135">category</span><span class="sxs-lookup"><span data-stu-id="29675-135">category</span></span> |<span data-ttu-id="29675-136">Optional category for the parameter.</span><span class="sxs-lookup"><span data-stu-id="29675-136">Optional category for the parameter.</span></span>  <span data-ttu-id="29675-137">Parameters in the same category are grouped together.</span><span class="sxs-lookup"><span data-stu-id="29675-137">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="29675-138">control</span><span class="sxs-lookup"><span data-stu-id="29675-138">control</span></span> |<span data-ttu-id="29675-139">Additional functionality for string parameters.</span><span class="sxs-lookup"><span data-stu-id="29675-139">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="29675-140">datetime - Datetime control is displayed.</span><span class="sxs-lookup"><span data-stu-id="29675-140">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="29675-141">guid - Guid value is automatically generated, and the parameter is not displayed.</span><span class="sxs-lookup"><span data-stu-id="29675-141">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="29675-142">description</span><span class="sxs-lookup"><span data-stu-id="29675-142">description</span></span> |<span data-ttu-id="29675-143">Optional description for the parameter.</span><span class="sxs-lookup"><span data-stu-id="29675-143">Optional description for the parameter.</span></span>  <span data-ttu-id="29675-144">Displayed in an information balloon next to the parameter.</span><span class="sxs-lookup"><span data-stu-id="29675-144">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="29675-145">Standard parameters</span><span class="sxs-lookup"><span data-stu-id="29675-145">Standard parameters</span></span>
<span data-ttu-id="29675-146">The following table lists the standard parameters for all management solutions.</span><span class="sxs-lookup"><span data-stu-id="29675-146">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="29675-147">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span><span class="sxs-lookup"><span data-stu-id="29675-147">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="29675-148">The user must provide values for them if the solution is installed with another method.</span><span class="sxs-lookup"><span data-stu-id="29675-148">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="29675-149">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span><span class="sxs-lookup"><span data-stu-id="29675-149">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="29675-150">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span><span class="sxs-lookup"><span data-stu-id="29675-150">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="29675-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="29675-151">Parameter</span></span> | <span data-ttu-id="29675-152">Type</span><span class="sxs-lookup"><span data-stu-id="29675-152">Type</span></span> | <span data-ttu-id="29675-153">Description</span><span class="sxs-lookup"><span data-stu-id="29675-153">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="29675-154">accountName</span><span class="sxs-lookup"><span data-stu-id="29675-154">accountName</span></span> |<span data-ttu-id="29675-155">string</span><span class="sxs-lookup"><span data-stu-id="29675-155">string</span></span> |<span data-ttu-id="29675-156">Azure Automation account name.</span><span class="sxs-lookup"><span data-stu-id="29675-156">Azure Automation account name.</span></span> |
| <span data-ttu-id="29675-157">pricingTier</span><span class="sxs-lookup"><span data-stu-id="29675-157">pricingTier</span></span> |<span data-ttu-id="29675-158">string</span><span class="sxs-lookup"><span data-stu-id="29675-158">string</span></span> |<span data-ttu-id="29675-159">Pricing tier of both Log Analytics workspace and Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="29675-159">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="29675-160">regionId</span><span class="sxs-lookup"><span data-stu-id="29675-160">regionId</span></span> |<span data-ttu-id="29675-161">string</span><span class="sxs-lookup"><span data-stu-id="29675-161">string</span></span> |<span data-ttu-id="29675-162">Region of the Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="29675-162">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="29675-163">solutionName</span><span class="sxs-lookup"><span data-stu-id="29675-163">solutionName</span></span> |<span data-ttu-id="29675-164">string</span><span class="sxs-lookup"><span data-stu-id="29675-164">string</span></span> |<span data-ttu-id="29675-165">Name of the solution.</span><span class="sxs-lookup"><span data-stu-id="29675-165">Name of the solution.</span></span>  <span data-ttu-id="29675-166">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span><span class="sxs-lookup"><span data-stu-id="29675-166">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="29675-167">workspaceName</span><span class="sxs-lookup"><span data-stu-id="29675-167">workspaceName</span></span> |<span data-ttu-id="29675-168">string</span><span class="sxs-lookup"><span data-stu-id="29675-168">string</span></span> |<span data-ttu-id="29675-169">Log Analytics workspace name.</span><span class="sxs-lookup"><span data-stu-id="29675-169">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="29675-170">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="29675-170">workspaceRegionId</span></span> |<span data-ttu-id="29675-171">string</span><span class="sxs-lookup"><span data-stu-id="29675-171">string</span></span> |<span data-ttu-id="29675-172">Region of the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="29675-172">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="29675-173">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span><span class="sxs-lookup"><span data-stu-id="29675-173">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="29675-174">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span><span class="sxs-lookup"><span data-stu-id="29675-174">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="29675-175">For example, to access the workspace name, you would use **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="29675-175">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="29675-176">Variables</span><span class="sxs-lookup"><span data-stu-id="29675-176">Variables</span></span>
<span data-ttu-id="29675-177">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span><span class="sxs-lookup"><span data-stu-id="29675-177">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="29675-178">These values are not exposed to the user installing the solution.</span><span class="sxs-lookup"><span data-stu-id="29675-178">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="29675-179">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span><span class="sxs-lookup"><span data-stu-id="29675-179">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="29675-180">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span><span class="sxs-lookup"><span data-stu-id="29675-180">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="29675-181">This makes the code more readable and allows you to easily change these values in later versions.</span><span class="sxs-lookup"><span data-stu-id="29675-181">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="29675-182">Following is an example of a **variables** element with typical parameters used in solutions.</span><span class="sxs-lookup"><span data-stu-id="29675-182">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="29675-183">You refer to variable values through the solution with the syntax **variables('variable name')**.</span><span class="sxs-lookup"><span data-stu-id="29675-183">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="29675-184">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="29675-184">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="29675-185">You can also define complex variables that multiple sets of values.</span><span class="sxs-lookup"><span data-stu-id="29675-185">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="29675-186">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span><span class="sxs-lookup"><span data-stu-id="29675-186">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="29675-187">For example, you could restructure the solution variables shown above to the following.</span><span class="sxs-lookup"><span data-stu-id="29675-187">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="29675-188">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="29675-188">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="29675-189">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span><span class="sxs-lookup"><span data-stu-id="29675-189">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="29675-190">Resources</span><span class="sxs-lookup"><span data-stu-id="29675-190">Resources</span></span>
<span data-ttu-id="29675-191">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span><span class="sxs-lookup"><span data-stu-id="29675-191">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="29675-192">This will be the largest and most complex portion of the template.</span><span class="sxs-lookup"><span data-stu-id="29675-192">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="29675-193">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="29675-193">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="29675-194">Different resources that you will typically define are detailed in other articles in this documentation.</span><span class="sxs-lookup"><span data-stu-id="29675-194">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="29675-195">Dependencies</span><span class="sxs-lookup"><span data-stu-id="29675-195">Dependencies</span></span>
<span data-ttu-id="29675-196">The **dependsOn** element specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span><span class="sxs-lookup"><span data-stu-id="29675-196">The **dependsOn** element specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="29675-197">When the solution is installed, a resource is not created until all of its dependencies have been created.</span><span class="sxs-lookup"><span data-stu-id="29675-197">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="29675-198">For example, your solution might [start a runbook](monitoring-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](monitoring-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="29675-198">For example, your solution might [start a runbook](monitoring-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](monitoring-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="29675-199">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span><span class="sxs-lookup"><span data-stu-id="29675-199">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="log-analytics-workspace-and-automation-account"></a><span data-ttu-id="29675-200">Log Analytics workspace and Automation account</span><span class="sxs-lookup"><span data-stu-id="29675-200">Log Analytics workspace and Automation account</span></span>
<span data-ttu-id="29675-201">Management solutions require a [Log Analytics workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span><span class="sxs-lookup"><span data-stu-id="29675-201">Management solutions require a [Log Analytics workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="29675-202">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span><span class="sxs-lookup"><span data-stu-id="29675-202">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="29675-203">The user will [specify a workspace and account](monitoring-solutions.md#log-analytics-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span><span class="sxs-lookup"><span data-stu-id="29675-203">The user will [specify a workspace and account](monitoring-solutions.md#log-analytics-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>


## <a name="solution-resource"></a><span data-ttu-id="29675-204">Solution resource</span><span class="sxs-lookup"><span data-stu-id="29675-204">Solution resource</span></span>
<span data-ttu-id="29675-205">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span><span class="sxs-lookup"><span data-stu-id="29675-205">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="29675-206">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="29675-206">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="29675-207">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span><span class="sxs-lookup"><span data-stu-id="29675-207">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="29675-208">Dependencies</span><span class="sxs-lookup"><span data-stu-id="29675-208">Dependencies</span></span>
<span data-ttu-id="29675-209">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span><span class="sxs-lookup"><span data-stu-id="29675-209">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="29675-210">You do this by adding an entry for each resource in the **dependsOn** element.</span><span class="sxs-lookup"><span data-stu-id="29675-210">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="29675-211">Properties</span><span class="sxs-lookup"><span data-stu-id="29675-211">Properties</span></span>
<span data-ttu-id="29675-212">The solution resource has the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="29675-212">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="29675-213">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="29675-213">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="29675-214">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span><span class="sxs-lookup"><span data-stu-id="29675-214">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="29675-215">Property</span><span class="sxs-lookup"><span data-stu-id="29675-215">Property</span></span> | <span data-ttu-id="29675-216">Description</span><span class="sxs-lookup"><span data-stu-id="29675-216">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="29675-217">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="29675-217">workspaceResourceId</span></span> |<span data-ttu-id="29675-218">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span><span class="sxs-lookup"><span data-stu-id="29675-218">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="29675-219">referencedResources</span><span class="sxs-lookup"><span data-stu-id="29675-219">referencedResources</span></span> |<span data-ttu-id="29675-220">List of resources in the solution that should not be removed when the solution is removed.</span><span class="sxs-lookup"><span data-stu-id="29675-220">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="29675-221">containedResources</span><span class="sxs-lookup"><span data-stu-id="29675-221">containedResources</span></span> |<span data-ttu-id="29675-222">List of resources in the solution that should be removed when the solution is removed.</span><span class="sxs-lookup"><span data-stu-id="29675-222">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="29675-223">The example  above is for a solution with a runbook, a schedule, and view.</span><span class="sxs-lookup"><span data-stu-id="29675-223">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="29675-224">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span><span class="sxs-lookup"><span data-stu-id="29675-224">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="29675-225">The view is *contained* so it is removed when the solution is removed.</span><span class="sxs-lookup"><span data-stu-id="29675-225">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="29675-226">Plan</span><span class="sxs-lookup"><span data-stu-id="29675-226">Plan</span></span>
<span data-ttu-id="29675-227">The **plan** entity of the solution resource has the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="29675-227">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="29675-228">Property</span><span class="sxs-lookup"><span data-stu-id="29675-228">Property</span></span> | <span data-ttu-id="29675-229">Description</span><span class="sxs-lookup"><span data-stu-id="29675-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="29675-230">name</span><span class="sxs-lookup"><span data-stu-id="29675-230">name</span></span> |<span data-ttu-id="29675-231">Name of the solution.</span><span class="sxs-lookup"><span data-stu-id="29675-231">Name of the solution.</span></span> |
| <span data-ttu-id="29675-232">version</span><span class="sxs-lookup"><span data-stu-id="29675-232">version</span></span> |<span data-ttu-id="29675-233">Version of the solution as determined by the author.</span><span class="sxs-lookup"><span data-stu-id="29675-233">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="29675-234">product</span><span class="sxs-lookup"><span data-stu-id="29675-234">product</span></span> |<span data-ttu-id="29675-235">Unique string to identify the solution.</span><span class="sxs-lookup"><span data-stu-id="29675-235">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="29675-236">publisher</span><span class="sxs-lookup"><span data-stu-id="29675-236">publisher</span></span> |<span data-ttu-id="29675-237">Publisher of the solution.</span><span class="sxs-lookup"><span data-stu-id="29675-237">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="29675-238">Sample</span><span class="sxs-lookup"><span data-stu-id="29675-238">Sample</span></span>
<span data-ttu-id="29675-239">You can view samples of solution files with a solution resource at the following locations.</span><span class="sxs-lookup"><span data-stu-id="29675-239">You can view samples of solution files with a solution resource at the following locations.</span></span>

- [<span data-ttu-id="29675-240">Automation resources</span><span class="sxs-lookup"><span data-stu-id="29675-240">Automation resources</span></span>](monitoring-solutions-resources-automation.md#sample)
- [<span data-ttu-id="29675-241">Search and alert resources</span><span class="sxs-lookup"><span data-stu-id="29675-241">Search and alert resources</span></span>](monitoring-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="29675-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="29675-242">Next steps</span></span>
* <span data-ttu-id="29675-243">[Add saved searches and alerts](monitoring-solutions-resources-searches-alerts.md) to your management solution.</span><span class="sxs-lookup"><span data-stu-id="29675-243">[Add saved searches and alerts](monitoring-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="29675-244">[Add views](monitoring-solutions-resources-views.md) to your management solution.</span><span class="sxs-lookup"><span data-stu-id="29675-244">[Add views](monitoring-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="29675-245">[Add runbooks and other Automation resources](monitoring-solutions-resources-automation.md) to your management solution.</span><span class="sxs-lookup"><span data-stu-id="29675-245">[Add runbooks and other Automation resources](monitoring-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="29675-246">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="29675-246">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="29675-247">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="29675-247">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
