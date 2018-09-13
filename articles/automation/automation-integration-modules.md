---
title: Create an Azure Automation Integration Module | Microsoft Docs
description: Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: ''
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: 0ef89ccd6bda035a513937eff4804db7f171ca23
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551639"
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="3ddf0-103">Azure Automation Integration Modules</span><span class="sxs-lookup"><span data-stu-id="3ddf0-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="3ddf0-104">PowerShell is the fundamental technology behind Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="3ddf0-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="3ddf0-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="3ddf0-107">What is a PowerShell Module?</span><span class="sxs-lookup"><span data-stu-id="3ddf0-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="3ddf0-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="3ddf0-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="3ddf0-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="3ddf0-111">Both of these modules ship with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="3ddf0-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="3ddf0-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="3ddf0-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ddf0-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="3ddf0-115">What is an Azure Automation Integration Module?</span><span class="sxs-lookup"><span data-stu-id="3ddf0-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="3ddf0-116">An Integration Module isn't very different from a PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="3ddf0-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="3ddf0-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="3ddf0-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="3ddf0-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="3ddf0-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="3ddf0-122">Certain modules are shipped as “global modules” in the Automation service.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="3ddf0-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="3ddf0-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="3ddf0-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="3ddf0-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="3ddf0-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="3ddf0-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="3ddf0-129">This will end up creating a connection type in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="3ddf0-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="3ddf0-131">The following is a template in the json file format:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-131">The following is a template in the json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="3ddf0-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="3ddf0-133">Authoring Best Practices</span><span class="sxs-lookup"><span data-stu-id="3ddf0-133">Authoring Best Practices</span></span>
<span data-ttu-id="3ddf0-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="3ddf0-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="3ddf0-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="3ddf0-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="3ddf0-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="3ddf0-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="3ddf0-140">For example, when inserting activities during runbook authoring.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="3ddf0-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="3ddf0-142">![Integration Module Help](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="3ddf0-142">![Integration Module Help](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="3ddf0-143">If the module runs against a remote system,</span><span class="sxs-lookup"><span data-stu-id="3ddf0-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="3ddf0-144">a.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-144">a.</span></span> <span data-ttu-id="3ddf0-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="3ddf0-146">b.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-146">b.</span></span> <span data-ttu-id="3ddf0-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="3ddf0-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="3ddf0-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="3ddf0-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="3ddf0-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span><span class="sxs-lookup"><span data-stu-id="3ddf0-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="3ddf0-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span><span class="sxs-lookup"><span data-stu-id="3ddf0-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="3ddf0-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="3ddf0-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="3ddf0-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="3ddf0-156">**UseConnectionObject** lets you pass the connection straight through.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="3ddf0-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="3ddf0-158">Define output type for all cmdlets in the module.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="3ddf0-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="3ddf0-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="3ddf0-161">![Graphical Runbook Output Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="3ddf0-161">![Graphical Runbook Output Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="3ddf0-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="3ddf0-163">![POSH IntelliSense](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="3ddf0-163">![POSH IntelliSense](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="3ddf0-164">Cmdlets in the module should not take complex object types for parameters.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="3ddf0-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="3ddf0-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="3ddf0-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="3ddf0-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="3ddf0-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="3ddf0-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="3ddf0-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="3ddf0-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="3ddf0-172">Here is the wrong way to do it.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="3ddf0-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="3ddf0-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="3ddf0-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="3ddf0-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="3ddf0-177">Hashtable is one of these.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-177">Hashtable is one of these.</span></span> <span data-ttu-id="3ddf0-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="3ddf0-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="3ddf0-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="3ddf0-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="3ddf0-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="3ddf0-183">Make all cmdlets in the module stateless.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="3ddf0-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="3ddf0-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="3ddf0-186">Here is an example of what not to do.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-186">Here is an example of what not to do.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="3ddf0-187">The module should be fully contained in an Xcopy-able package.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="3ddf0-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="3ddf0-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="3ddf0-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="3ddf0-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3ddf0-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ddf0-192">Next steps</span></span>

* <span data-ttu-id="3ddf0-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="3ddf0-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="3ddf0-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="3ddf0-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>




