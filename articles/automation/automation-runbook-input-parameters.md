---
title: Runbook input parameters| Microsoft Docs
description: Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to a runbook when it is started. This article describes different scenarios where input parameters are used in runbooks.
services: automation
documentationcenter: ''
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: 545c1bede161751ab19235ab47d8c6b94424bf6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660862"
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="d3e85-104">Runbook input parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-104">Runbook input parameters</span></span>
<span data-ttu-id="d3e85-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span><span class="sxs-lookup"><span data-stu-id="d3e85-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="d3e85-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span><span class="sxs-lookup"><span data-stu-id="d3e85-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="d3e85-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span><span class="sxs-lookup"><span data-stu-id="d3e85-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="d3e85-108">Configure input parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-108">Configure input parameters</span></span>
<span data-ttu-id="d3e85-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span><span class="sxs-lookup"><span data-stu-id="d3e85-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="d3e85-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span><span class="sxs-lookup"><span data-stu-id="d3e85-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="d3e85-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span><span class="sxs-lookup"><span data-stu-id="d3e85-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="d3e85-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span><span class="sxs-lookup"><span data-stu-id="d3e85-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="d3e85-113">These methods include starting  a runbook from the portal  or a web service.</span><span class="sxs-lookup"><span data-stu-id="d3e85-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="d3e85-114">You can also start one as a child runbook that is called inline in another runbook.</span><span class="sxs-lookup"><span data-stu-id="d3e85-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="d3e85-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span><span class="sxs-lookup"><span data-stu-id="d3e85-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="d3e85-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span><span class="sxs-lookup"><span data-stu-id="d3e85-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="d3e85-117">**Property**</span><span class="sxs-lookup"><span data-stu-id="d3e85-117">**Property**</span></span> | <span data-ttu-id="d3e85-118">**Description**</span><span class="sxs-lookup"><span data-stu-id="d3e85-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="d3e85-119">Type</span><span class="sxs-lookup"><span data-stu-id="d3e85-119">Type</span></span> |<span data-ttu-id="d3e85-120">Required.</span><span class="sxs-lookup"><span data-stu-id="d3e85-120">Required.</span></span> <span data-ttu-id="d3e85-121">The data type expected for the parameter value.</span><span class="sxs-lookup"><span data-stu-id="d3e85-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="d3e85-122">Any .NET type is valid.</span><span class="sxs-lookup"><span data-stu-id="d3e85-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="d3e85-123">Name</span><span class="sxs-lookup"><span data-stu-id="d3e85-123">Name</span></span> |<span data-ttu-id="d3e85-124">Required.</span><span class="sxs-lookup"><span data-stu-id="d3e85-124">Required.</span></span> <span data-ttu-id="d3e85-125">The name of the parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-125">The name of the parameter.</span></span> <span data-ttu-id="d3e85-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span><span class="sxs-lookup"><span data-stu-id="d3e85-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="d3e85-127">It must start with a letter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-127">It must start with a letter.</span></span> |
| <span data-ttu-id="d3e85-128">Mandatory</span><span class="sxs-lookup"><span data-stu-id="d3e85-128">Mandatory</span></span> |<span data-ttu-id="d3e85-129">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-129">Optional.</span></span> <span data-ttu-id="d3e85-130">Specifies whether a value must be provided for the parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="d3e85-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span><span class="sxs-lookup"><span data-stu-id="d3e85-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="d3e85-132">If you set this to **$false**, then a value is optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="d3e85-133">Default value</span><span class="sxs-lookup"><span data-stu-id="d3e85-133">Default value</span></span> |<span data-ttu-id="d3e85-134">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-134">Optional.</span></span>  <span data-ttu-id="d3e85-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span><span class="sxs-lookup"><span data-stu-id="d3e85-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="d3e85-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span><span class="sxs-lookup"><span data-stu-id="d3e85-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="d3e85-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span><span class="sxs-lookup"><span data-stu-id="d3e85-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="d3e85-138">However, Azure Automation currently supports only the input parameters listed above.</span><span class="sxs-lookup"><span data-stu-id="d3e85-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="d3e85-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span><span class="sxs-lookup"><span data-stu-id="d3e85-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="d3e85-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="d3e85-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span><span class="sxs-lookup"><span data-stu-id="d3e85-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="d3e85-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span><span class="sxs-lookup"><span data-stu-id="d3e85-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="d3e85-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span><span class="sxs-lookup"><span data-stu-id="d3e85-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![Automation PowerShell Workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="d3e85-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span><span class="sxs-lookup"><span data-stu-id="d3e85-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="d3e85-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span><span class="sxs-lookup"><span data-stu-id="d3e85-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="d3e85-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span><span class="sxs-lookup"><span data-stu-id="d3e85-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="d3e85-148">For example, if you have the following parameter in a runbook:</span><span class="sxs-lookup"><span data-stu-id="d3e85-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="d3e85-149">Then you can pass the following value to the parameter:</span><span class="sxs-lookup"><span data-stu-id="d3e85-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="d3e85-150">Configure input parameters in graphical runbooks</span><span class="sxs-lookup"><span data-stu-id="d3e85-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="d3e85-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span><span class="sxs-lookup"><span data-stu-id="d3e85-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="d3e85-152">Configuring a runbook consists of two major activities, as described below.</span><span class="sxs-lookup"><span data-stu-id="d3e85-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="d3e85-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span><span class="sxs-lookup"><span data-stu-id="d3e85-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="d3e85-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d3e85-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="d3e85-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d3e85-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="d3e85-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span><span class="sxs-lookup"><span data-stu-id="d3e85-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="d3e85-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span><span class="sxs-lookup"><span data-stu-id="d3e85-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="d3e85-158">Here are the steps to add input parameters:</span><span class="sxs-lookup"><span data-stu-id="d3e85-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="d3e85-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span><span class="sxs-lookup"><span data-stu-id="d3e85-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="d3e85-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span><span class="sxs-lookup"><span data-stu-id="d3e85-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![Automation graphical runbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="d3e85-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span><span class="sxs-lookup"><span data-stu-id="d3e85-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="d3e85-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="d3e85-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span><span class="sxs-lookup"><span data-stu-id="d3e85-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="d3e85-165">There, you can configure the following parameters:</span><span class="sxs-lookup"><span data-stu-id="d3e85-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="d3e85-166">**Property**</span><span class="sxs-lookup"><span data-stu-id="d3e85-166">**Property**</span></span> | <span data-ttu-id="d3e85-167">**Description**</span><span class="sxs-lookup"><span data-stu-id="d3e85-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="d3e85-168">Name</span><span class="sxs-lookup"><span data-stu-id="d3e85-168">Name</span></span> |<span data-ttu-id="d3e85-169">Required.</span><span class="sxs-lookup"><span data-stu-id="d3e85-169">Required.</span></span>  <span data-ttu-id="d3e85-170">The name of the parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-170">The name of the parameter.</span></span> <span data-ttu-id="d3e85-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span><span class="sxs-lookup"><span data-stu-id="d3e85-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="d3e85-172">It must start with a letter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="d3e85-173">Description</span><span class="sxs-lookup"><span data-stu-id="d3e85-173">Description</span></span> |<span data-ttu-id="d3e85-174">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-174">Optional.</span></span> <span data-ttu-id="d3e85-175">Description about the purpose of input parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="d3e85-176">Type</span><span class="sxs-lookup"><span data-stu-id="d3e85-176">Type</span></span> |<span data-ttu-id="d3e85-177">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-177">Optional.</span></span> <span data-ttu-id="d3e85-178">The data type that's expected for the parameter value.</span><span class="sxs-lookup"><span data-stu-id="d3e85-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="d3e85-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span><span class="sxs-lookup"><span data-stu-id="d3e85-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="d3e85-180">If a data type is not selected, it defaults to **String**.</span><span class="sxs-lookup"><span data-stu-id="d3e85-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="d3e85-181">Mandatory</span><span class="sxs-lookup"><span data-stu-id="d3e85-181">Mandatory</span></span> |<span data-ttu-id="d3e85-182">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-182">Optional.</span></span> <span data-ttu-id="d3e85-183">Specifies whether a value must be provided for the parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="d3e85-184">If you choose **yes**, then a value must be provided when the runbook is started.</span><span class="sxs-lookup"><span data-stu-id="d3e85-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="d3e85-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span><span class="sxs-lookup"><span data-stu-id="d3e85-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="d3e85-186">Default Value</span><span class="sxs-lookup"><span data-stu-id="d3e85-186">Default Value</span></span> |<span data-ttu-id="d3e85-187">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-187">Optional.</span></span> <span data-ttu-id="d3e85-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span><span class="sxs-lookup"><span data-stu-id="d3e85-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="d3e85-189">A default value can be set for a parameter that's not mandatory.</span><span class="sxs-lookup"><span data-stu-id="d3e85-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="d3e85-190">To set a default value, choose **Custom**.</span><span class="sxs-lookup"><span data-stu-id="d3e85-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="d3e85-191">This value is used unless another value is provided when the runbook is started.</span><span class="sxs-lookup"><span data-stu-id="d3e85-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="d3e85-192">Choose **None** if you don’t want to provide any default value.</span><span class="sxs-lookup"><span data-stu-id="d3e85-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![Add new input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="d3e85-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span><span class="sxs-lookup"><span data-stu-id="d3e85-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="d3e85-195">**Parameter1:**</span><span class="sxs-lookup"><span data-stu-id="d3e85-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="d3e85-196">Name - VMName</span><span class="sxs-lookup"><span data-stu-id="d3e85-196">Name - VMName</span></span>
     * <span data-ttu-id="d3e85-197">Type - String</span><span class="sxs-lookup"><span data-stu-id="d3e85-197">Type - String</span></span>
     * <span data-ttu-id="d3e85-198">Mandatory - No</span><span class="sxs-lookup"><span data-stu-id="d3e85-198">Mandatory - No</span></span>
   * <span data-ttu-id="d3e85-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="d3e85-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="d3e85-200">Name - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="d3e85-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="d3e85-201">Type - String</span><span class="sxs-lookup"><span data-stu-id="d3e85-201">Type - String</span></span>
     * <span data-ttu-id="d3e85-202">Mandatory - No</span><span class="sxs-lookup"><span data-stu-id="d3e85-202">Mandatory - No</span></span>
     * <span data-ttu-id="d3e85-203">Default value - Custom</span><span class="sxs-lookup"><span data-stu-id="d3e85-203">Default value - Custom</span></span>
     * <span data-ttu-id="d3e85-204">Custom default value - \<Name of the resource group that contains the virtual machines></span><span class="sxs-lookup"><span data-stu-id="d3e85-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="d3e85-205">Once you add the parameters, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3e85-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="d3e85-206">You can now view them in the **Input and output blade**.</span><span class="sxs-lookup"><span data-stu-id="d3e85-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="d3e85-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span><span class="sxs-lookup"><span data-stu-id="d3e85-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="d3e85-208">Assign values to input parameters in runbooks</span><span class="sxs-lookup"><span data-stu-id="d3e85-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="d3e85-209">You can pass values to input parameters in runbooks in the following scenarios.</span><span class="sxs-lookup"><span data-stu-id="d3e85-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="d3e85-210">Start a runbook and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="d3e85-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span><span class="sxs-lookup"><span data-stu-id="d3e85-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="d3e85-212">Below we discuss different methods for starting a runbook and assigning parameters.</span><span class="sxs-lookup"><span data-stu-id="d3e85-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="d3e85-213">Start a published runbook by using the Azure portal and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="d3e85-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span><span class="sxs-lookup"><span data-stu-id="d3e85-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![Start using the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="d3e85-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="d3e85-217">Attributes include mandatory or optional, type, and  default value.</span><span class="sxs-lookup"><span data-stu-id="d3e85-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="d3e85-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span><span class="sxs-lookup"><span data-stu-id="d3e85-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="d3e85-219">This information includes whether a parameter is mandatory or optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="d3e85-220">It also includes the type and default value (if any), and other helpful notes.</span><span class="sxs-lookup"><span data-stu-id="d3e85-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![Help balloon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="d3e85-222">String type parameters support **Empty** String values.</span><span class="sxs-lookup"><span data-stu-id="d3e85-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="d3e85-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e85-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="d3e85-224">Also, String type parameters don’t support **Null** values being passed.</span><span class="sxs-lookup"><span data-stu-id="d3e85-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="d3e85-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span><span class="sxs-lookup"><span data-stu-id="d3e85-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="d3e85-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="d3e85-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3e85-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="d3e85-228">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3e85-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="d3e85-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3e85-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="d3e85-230">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d3e85-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="d3e85-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d3e85-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="d3e85-232">You can view this parameter in the **Job details** blade.</span><span class="sxs-lookup"><span data-stu-id="d3e85-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="d3e85-233">Start a runbook by using an SDK and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="d3e85-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span><span class="sxs-lookup"><span data-stu-id="d3e85-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="d3e85-235">Below is a C# code snippet for starting a runbook in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="d3e85-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="d3e85-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="d3e85-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="d3e85-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span><span class="sxs-lookup"><span data-stu-id="d3e85-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="d3e85-238">Below is a C# code snippet for starting a runbook in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="d3e85-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="d3e85-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="d3e85-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="d3e85-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span><span class="sxs-lookup"><span data-stu-id="d3e85-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="d3e85-241">Then start the runbook.</span><span class="sxs-lookup"><span data-stu-id="d3e85-241">Then start the runbook.</span></span> <span data-ttu-id="d3e85-242">Below is the C# code snippet for calling the method that's defined above.</span><span class="sxs-lookup"><span data-stu-id="d3e85-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="d3e85-243">Start a runbook by using the REST API and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="d3e85-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span><span class="sxs-lookup"><span data-stu-id="d3e85-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="d3e85-245">In the request URI, replace the following parameters:</span><span class="sxs-lookup"><span data-stu-id="d3e85-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="d3e85-246">**subscription-id:** Your Azure subscription ID.</span><span class="sxs-lookup"><span data-stu-id="d3e85-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="d3e85-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span><span class="sxs-lookup"><span data-stu-id="d3e85-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="d3e85-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span><span class="sxs-lookup"><span data-stu-id="d3e85-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="d3e85-249">**job-id:** The GUID for the job.</span><span class="sxs-lookup"><span data-stu-id="d3e85-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="d3e85-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span><span class="sxs-lookup"><span data-stu-id="d3e85-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="d3e85-251">In order to pass parameters to the runbook job, use the request body.</span><span class="sxs-lookup"><span data-stu-id="d3e85-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="d3e85-252">It takes the following two properties provided in JSON format:</span><span class="sxs-lookup"><span data-stu-id="d3e85-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="d3e85-253">**Runbook name:** Required.</span><span class="sxs-lookup"><span data-stu-id="d3e85-253">**Runbook name:** Required.</span></span> <span data-ttu-id="d3e85-254">The name of the runbook for the job to start.</span><span class="sxs-lookup"><span data-stu-id="d3e85-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="d3e85-255">**Runbook parameters:** Optional.</span><span class="sxs-lookup"><span data-stu-id="d3e85-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="d3e85-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span><span class="sxs-lookup"><span data-stu-id="d3e85-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="d3e85-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span><span class="sxs-lookup"><span data-stu-id="d3e85-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="d3e85-258">A HTTP status code 201 is returned if the job is successfully created.</span><span class="sxs-lookup"><span data-stu-id="d3e85-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="d3e85-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="d3e85-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="d3e85-260">Test a runbook and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="d3e85-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span><span class="sxs-lookup"><span data-stu-id="d3e85-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![Test and assign parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="d3e85-263">Link a schedule to a runbook and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="d3e85-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span><span class="sxs-lookup"><span data-stu-id="d3e85-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="d3e85-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span><span class="sxs-lookup"><span data-stu-id="d3e85-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="d3e85-266">You can’t save the schedule until all mandatory parameter values are provided.</span><span class="sxs-lookup"><span data-stu-id="d3e85-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![Schedule and assign parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="d3e85-268">Create a webhook for a runbook and assign parameters</span><span class="sxs-lookup"><span data-stu-id="d3e85-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="d3e85-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span><span class="sxs-lookup"><span data-stu-id="d3e85-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="d3e85-270">You can’t save the webhook until all mandatory parameter values are provided.</span><span class="sxs-lookup"><span data-stu-id="d3e85-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Create webhook and assign parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="d3e85-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span><span class="sxs-lookup"><span data-stu-id="d3e85-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="d3e85-273">You can click to expand the **WebhookData** parameter for more details.</span><span class="sxs-lookup"><span data-stu-id="d3e85-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![WebhookData parameter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="d3e85-275">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3e85-275">Next steps</span></span>
* <span data-ttu-id="d3e85-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="d3e85-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="d3e85-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d3e85-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="d3e85-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d3e85-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="d3e85-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d3e85-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>










