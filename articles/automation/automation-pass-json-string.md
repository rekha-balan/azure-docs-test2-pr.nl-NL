---
title: Pass a JSON object to an Azure Automation runbook
description: How to pass parameters to a runbook as a JSON object
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 03/16/2018
ms.topic: conceptual
manager: carmonm
keywords: powershell,  runbook, json, azure automation
ms.openlocfilehash: 5e1ab8d6bd2de24251851cfc60d270a2fef4090d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856512"
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="f53fd-104">Pass a JSON object to an Azure Automation runbook</span><span class="sxs-lookup"><span data-stu-id="f53fd-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="f53fd-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="f53fd-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="f53fd-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span><span class="sxs-lookup"><span data-stu-id="f53fd-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="f53fd-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span><span class="sxs-lookup"><span data-stu-id="f53fd-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="f53fd-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span><span class="sxs-lookup"><span data-stu-id="f53fd-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="f53fd-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span><span class="sxs-lookup"><span data-stu-id="f53fd-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f53fd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f53fd-110">Prerequisites</span></span>
<span data-ttu-id="f53fd-111">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="f53fd-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="f53fd-112">Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f53fd-112">Azure subscription.</span></span> <span data-ttu-id="f53fd-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or [sign up for a free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f53fd-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or [sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="f53fd-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f53fd-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="f53fd-115">This account must have permission to start and stop the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f53fd-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="f53fd-116">An Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f53fd-116">An Azure virtual machine.</span></span> <span data-ttu-id="f53fd-117">We stop and start this machine so it should not be a production VM.</span><span class="sxs-lookup"><span data-stu-id="f53fd-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="f53fd-118">Azure Powershell installed on a local machine.</span><span class="sxs-lookup"><span data-stu-id="f53fd-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="f53fd-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f53fd-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="f53fd-120">Create the JSON file</span><span class="sxs-lookup"><span data-stu-id="f53fd-120">Create the JSON file</span></span>

<span data-ttu-id="f53fd-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span><span class="sxs-lookup"><span data-stu-id="f53fd-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="f53fd-122">Create the runbook</span><span class="sxs-lookup"><span data-stu-id="f53fd-122">Create the runbook</span></span>

<span data-ttu-id="f53fd-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f53fd-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="f53fd-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f53fd-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="f53fd-125">To accept the JSON data, the runbook must take an object as an input parameter.</span><span class="sxs-lookup"><span data-stu-id="f53fd-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="f53fd-126">The runbook can then use the properties defined in the JSON.</span><span class="sxs-lookup"><span data-stu-id="f53fd-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Connect-AzureRmAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="f53fd-127">Save and publish this runbook in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="f53fd-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="f53fd-128">Call the runbook from PowerShell</span><span class="sxs-lookup"><span data-stu-id="f53fd-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="f53fd-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f53fd-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="f53fd-130">Run the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="f53fd-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="f53fd-131">Log in to Azure:</span><span class="sxs-lookup"><span data-stu-id="f53fd-131">Log in to Azure:</span></span>
   ```powershell
   Connect-AzureRmAccount
   ```
    <span data-ttu-id="f53fd-132">You are prompted to enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="f53fd-132">You are prompted to enter your Azure credentials.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f53fd-133">**Add-AzureRmAccount** is now an alias for **Connect-AzureRMAccount**.</span><span class="sxs-lookup"><span data-stu-id="f53fd-133">**Add-AzureRmAccount** is now an alias for **Connect-AzureRMAccount**.</span></span> <span data-ttu-id="f53fd-134">When searching your library items, if you do not see **Connect-AzureRMAccount**, you can use **Add-AzureRmAccount**, or you can update your modules in your Automation Account.</span><span class="sxs-lookup"><span data-stu-id="f53fd-134">When searching your library items, if you do not see **Connect-AzureRMAccount**, you can use **Add-AzureRmAccount**, or you can update your modules in your Automation Account.</span></span>

1. <span data-ttu-id="f53fd-135">Get the contents of the JSON file and convert it to a string:</span><span class="sxs-lookup"><span data-stu-id="f53fd-135">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="f53fd-136">`JsonPath` is the path where you saved the JSON file.</span><span class="sxs-lookup"><span data-stu-id="f53fd-136">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="f53fd-137">Convert the string contents of `$json` to a PowerShell object:</span><span class="sxs-lookup"><span data-stu-id="f53fd-137">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="f53fd-138">Create a hashtable for the parameters for `Start-AzureRmAutomationRunbook`:</span><span class="sxs-lookup"><span data-stu-id="f53fd-138">Create a hashtable for the parameters for `Start-AzureRmAutomationRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="f53fd-139">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span><span class="sxs-lookup"><span data-stu-id="f53fd-139">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="f53fd-140">Start the runbook</span><span class="sxs-lookup"><span data-stu-id="f53fd-140">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="f53fd-141">The runbook uses the values from the JSON file to start a VM.</span><span class="sxs-lookup"><span data-stu-id="f53fd-141">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f53fd-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="f53fd-142">Next steps</span></span>

* <span data-ttu-id="f53fd-143">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="f53fd-143">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="f53fd-144">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="f53fd-144">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


