---
title: Integrate Azure Automation with Visual Stuido Team Services source control | Microsoft Docs
description: Scenario walks you through setting up integration with an Azure Automation account and Visual Stuido Team Services source control.
services: automation
documentationcenter: ''
author: eamono
manager: ''
editor: ''
keywords: azure powershell, VSTS, source control, automation
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 34eb2c5652e18ca83022f44bde8dab7de2895738
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555456"
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="138b6-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="138b6-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="138b6-105">In this scenario, you have a Visual Studio Team Services project that you are using to manage Azure Automation runbooks or DSC configurations under source control.</span><span class="sxs-lookup"><span data-stu-id="138b6-105">In this scenario, you have a Visual Studio Team Services project that you are using to manage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="138b6-106">This article describes how to integrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span><span class="sxs-lookup"><span data-stu-id="138b6-106">This article describes how to integrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="138b6-107">Getting the scenario</span><span class="sxs-lookup"><span data-stu-id="138b6-107">Getting the scenario</span></span>

<span data-ttu-id="138b6-108">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span><span class="sxs-lookup"><span data-stu-id="138b6-108">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="138b6-109">Runbooks</span><span class="sxs-lookup"><span data-stu-id="138b6-109">Runbooks</span></span>

<span data-ttu-id="138b6-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="138b6-110">Runbook</span></span> | <span data-ttu-id="138b6-111">Description</span><span class="sxs-lookup"><span data-stu-id="138b6-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="138b6-112">Sync-VSTS</span><span class="sxs-lookup"><span data-stu-id="138b6-112">Sync-VSTS</span></span> | <span data-ttu-id="138b6-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span><span class="sxs-lookup"><span data-stu-id="138b6-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="138b6-114">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="138b6-114">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>| 
<span data-ttu-id="138b6-115">Sync-VSTSGit</span><span class="sxs-lookup"><span data-stu-id="138b6-115">Sync-VSTSGit</span></span> | <span data-ttu-id="138b6-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span><span class="sxs-lookup"><span data-stu-id="138b6-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="138b6-117">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="138b6-117">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="138b6-118">Variables</span><span class="sxs-lookup"><span data-stu-id="138b6-118">Variables</span></span>

<span data-ttu-id="138b6-119">Variable</span><span class="sxs-lookup"><span data-stu-id="138b6-119">Variable</span></span> | <span data-ttu-id="138b6-120">Description</span><span class="sxs-lookup"><span data-stu-id="138b6-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="138b6-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="138b6-121">VSToken</span></span> | <span data-ttu-id="138b6-122">Secure variable asset you will create that contains the VSTS personal access token.</span><span class="sxs-lookup"><span data-stu-id="138b6-122">Secure variable asset you will create that contains the VSTS personal access token.</span></span> <span data-ttu-id="138b6-123">You can learn how to create a VSTS personal access token on the [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span><span class="sxs-lookup"><span data-stu-id="138b6-123">You can learn how to create a VSTS personal access token on the [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="138b6-124">Installing and configuring this scenario</span><span class="sxs-lookup"><span data-stu-id="138b6-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="138b6-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use to sync the runbooks or configurations into your automation account.</span><span class="sxs-lookup"><span data-stu-id="138b6-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use to sync the runbooks or configurations into your automation account.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="138b6-126">Create a [secure variable](automation-variables.md) in your automation account to hold the personal access token so that the runbook can authenticate to VSTS and sync the runbooks or configurations into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="138b6-126">Create a [secure variable](automation-variables.md) in your automation account to hold the personal access token so that the runbook can authenticate to VSTS and sync the runbooks or configurations into the Automation account.</span></span> <span data-ttu-id="138b6-127">You can name this VSToken.</span><span class="sxs-lookup"><span data-stu-id="138b6-127">You can name this VSToken.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="138b6-128">Import the runbook that will sync your runbooks or configurations into the automation account.</span><span class="sxs-lookup"><span data-stu-id="138b6-128">Import the runbook that will sync your runbooks or configurations into the automation account.</span></span> <span data-ttu-id="138b6-129">You can use the [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or the [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy to your automation account.</span><span class="sxs-lookup"><span data-stu-id="138b6-129">You can use the [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or the [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy to your automation account.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="138b6-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span><span class="sxs-lookup"><span data-stu-id="138b6-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="138b6-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in the parameters as shown below.</span><span class="sxs-lookup"><span data-stu-id="138b6-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in the parameters as shown below.</span></span> <span data-ttu-id="138b6-132">Make sure you copy the webhook url as you will need it for a service hook in VSTS.</span><span class="sxs-lookup"><span data-stu-id="138b6-132">Make sure you copy the webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="138b6-133">The VSAccessTokenVariableName is the name (VSToken) of the secure variable that you created earlier to hold the personal access token.</span><span class="sxs-lookup"><span data-stu-id="138b6-133">The VSAccessTokenVariableName is the name (VSToken) of the secure variable that you created earlier to hold the personal access token.</span></span> 

<span data-ttu-id="138b6-134">Integrating with VSTS (Sync-VSTS.ps1) will take the following parameters.</span><span class="sxs-lookup"><span data-stu-id="138b6-134">Integrating with VSTS (Sync-VSTS.ps1) will take the following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="138b6-135">Sync-VSTS Parameters</span><span class="sxs-lookup"><span data-stu-id="138b6-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="138b6-136">Parameter</span><span class="sxs-lookup"><span data-stu-id="138b6-136">Parameter</span></span> | <span data-ttu-id="138b6-137">Description</span><span class="sxs-lookup"><span data-stu-id="138b6-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="138b6-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="138b6-138">WebhookData</span></span> | <span data-ttu-id="138b6-139">This will contain the checkin information sent from the VSTS service hook.</span><span class="sxs-lookup"><span data-stu-id="138b6-139">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="138b6-140">You should leave this parameter blank.</span><span class="sxs-lookup"><span data-stu-id="138b6-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="138b6-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="138b6-141">ResourceGroup</span></span> | <span data-ttu-id="138b6-142">This is the name of the resource group that the automation account is in.</span><span class="sxs-lookup"><span data-stu-id="138b6-142">This is the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="138b6-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="138b6-143">AutomationAccountName</span></span> | <span data-ttu-id="138b6-144">The name of the automation account that will sync with VSTS.</span><span class="sxs-lookup"><span data-stu-id="138b6-144">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="138b6-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="138b6-145">VSFolder</span></span> | <span data-ttu-id="138b6-146">The name of the folder in VSTS where the runbooks and configurations exist.</span><span class="sxs-lookup"><span data-stu-id="138b6-146">The name of the folder in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="138b6-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="138b6-147">VSAccount</span></span> | <span data-ttu-id="138b6-148">The name of the Visual Studio Team Services account.</span><span class="sxs-lookup"><span data-stu-id="138b6-148">The name of the Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="138b6-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="138b6-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="138b6-150">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span><span class="sxs-lookup"><span data-stu-id="138b6-150">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>| 


![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="138b6-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take the following parameters.</span><span class="sxs-lookup"><span data-stu-id="138b6-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take the following parameters.</span></span>

<span data-ttu-id="138b6-152">Parameter</span><span class="sxs-lookup"><span data-stu-id="138b6-152">Parameter</span></span> | <span data-ttu-id="138b6-153">Description</span><span class="sxs-lookup"><span data-stu-id="138b6-153">Description</span></span>|
--------|------------|
<span data-ttu-id="138b6-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="138b6-154">WebhookData</span></span> | <span data-ttu-id="138b6-155">This will contain the checkin information sent from the VSTS service hook.</span><span class="sxs-lookup"><span data-stu-id="138b6-155">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="138b6-156">You should leave this parameter blank.</span><span class="sxs-lookup"><span data-stu-id="138b6-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="138b6-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="138b6-157">ResourceGroup</span></span> | <span data-ttu-id="138b6-158">This the name of the resource group that the automation account is in.</span><span class="sxs-lookup"><span data-stu-id="138b6-158">This the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="138b6-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="138b6-159">AutomationAccountName</span></span> | <span data-ttu-id="138b6-160">The name of the automation account that will sync with VSTS.</span><span class="sxs-lookup"><span data-stu-id="138b6-160">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="138b6-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="138b6-161">VSAccount</span></span> | <span data-ttu-id="138b6-162">The name of the Visual Studio Team Services account.</span><span class="sxs-lookup"><span data-stu-id="138b6-162">The name of the Visual Studio Team Services account.</span></span>|
<span data-ttu-id="138b6-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="138b6-163">VSProject</span></span> | <span data-ttu-id="138b6-164">The name of the project in VSTS where the runbooks and configurations exist.</span><span class="sxs-lookup"><span data-stu-id="138b6-164">The name of the project in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="138b6-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="138b6-165">GitRepo</span></span> | <span data-ttu-id="138b6-166">The name of the Git repository.</span><span class="sxs-lookup"><span data-stu-id="138b6-166">The name of the Git repository.</span></span>|
<span data-ttu-id="138b6-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="138b6-167">GitBranch</span></span> | <span data-ttu-id="138b6-168">The name of the branch in VSTS Git repository.</span><span class="sxs-lookup"><span data-stu-id="138b6-168">The name of the branch in VSTS Git repository.</span></span>|
<span data-ttu-id="138b6-169">Folder</span><span class="sxs-lookup"><span data-stu-id="138b6-169">Folder</span></span> | <span data-ttu-id="138b6-170">The name of the folder in VSTS Git branch.</span><span class="sxs-lookup"><span data-stu-id="138b6-170">The name of the folder in VSTS Git branch.</span></span>|
<span data-ttu-id="138b6-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="138b6-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="138b6-172">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span><span class="sxs-lookup"><span data-stu-id="138b6-172">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>|

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="138b6-173">Create a service hook in VSTS for check-ins to the folder that triggers this webhook on code check-in.</span><span class="sxs-lookup"><span data-stu-id="138b6-173">Create a service hook in VSTS for check-ins to the folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="138b6-174">Select Web Hooks as the service to integrate with when you create a new subscription.</span><span class="sxs-lookup"><span data-stu-id="138b6-174">Select Web Hooks as the service to integrate with when you create a new subscription.</span></span> <span data-ttu-id="138b6-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span><span class="sxs-lookup"><span data-stu-id="138b6-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="138b6-176">You should now be able to do all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span><span class="sxs-lookup"><span data-stu-id="138b6-176">You should now be able to do all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="138b6-177">If you run this runbook manually without being triggered by VSTS, you can leave the webhookdata parameter empty and it will do a full sync from the VSTS folder specified.</span><span class="sxs-lookup"><span data-stu-id="138b6-177">If you run this runbook manually without being triggered by VSTS, you can leave the webhookdata parameter empty and it will do a full sync from the VSTS folder specified.</span></span>

<span data-ttu-id="138b6-178">If you wish to uninstall the scenario, remove the service hook from VSTS, delete the runbook, and the VSToken variable.</span><span class="sxs-lookup"><span data-stu-id="138b6-178">If you wish to uninstall the scenario, remove the service hook from VSTS, delete the runbook, and the VSToken variable.</span></span>








