---
title: Azure Automation Source Control Integration with GitHub Enterprise | Microsoft Docs
description: Describes the details of how to configure integration with GitHub Enterprise  for source control of Automation runbooks.
services: automation
documentationCenter: ''
authors: mgoedtel
manager: jwhit
editor: ''
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: magoedte
ms.openlocfilehash: 8a760e6c6f43ebd3780d048a67777de401f5fdb0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562797"
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a><span data-ttu-id="03ee3-103">Azure Automation scenario - Automation source control integration with GitHub Enterprise</span><span class="sxs-lookup"><span data-stu-id="03ee3-103">Azure Automation scenario - Automation source control integration with GitHub Enterprise</span></span>

<span data-ttu-id="03ee3-104">Automation currently supports source control integration, which allows you to associate runbooks in your Automation account to a GitHub source control repository.</span><span class="sxs-lookup"><span data-stu-id="03ee3-104">Automation currently supports source control integration, which allows you to associate runbooks in your Automation account to a GitHub source control repository.</span></span>  <span data-ttu-id="03ee3-105">However, customers who have deployed [GitHub Enterprise](https://enterprise.github.com/home) to support their DevOps practices, also want to use it to manage the lifecycle of runbooks that are developed to automate business processes and service management operations.</span><span class="sxs-lookup"><span data-stu-id="03ee3-105">However, customers who have deployed [GitHub Enterprise](https://enterprise.github.com/home) to support their DevOps practices, also want to use it to manage the lifecycle of runbooks that are developed to automate business processes and service management operations.</span></span>  

<span data-ttu-id="03ee3-106">In this scenario, you will have a Windows computer in your data center configured as a Hybrid Runbook Worker with the Azure RM modules and Git tools installed.</span><span class="sxs-lookup"><span data-stu-id="03ee3-106">In this scenario, you will have a Windows computer in your data center configured as a Hybrid Runbook Worker with the Azure RM modules and Git tools installed.</span></span>  <span data-ttu-id="03ee3-107">The Hybrid worker machine will have a clone of the local Git repository.</span><span class="sxs-lookup"><span data-stu-id="03ee3-107">The Hybrid worker machine will have a clone of the local Git repository.</span></span>  <span data-ttu-id="03ee3-108">When the runbook is run on the hybrid worker, the Git directory is synchronized and the runbook file contents are imported into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="03ee3-108">When the runbook is run on the hybrid worker, the Git directory is synchronized and the runbook file contents are imported into the Automation account.</span></span>

<span data-ttu-id="03ee3-109">This article describes how to set up this configuration in your Azure Automation environment.</span><span class="sxs-lookup"><span data-stu-id="03ee3-109">This article describes how to set up this configuration in your Azure Automation environment.</span></span> <span data-ttu-id="03ee3-110">We will start by configuring Automation with the security credentials, runbooks required to support this scenario, and deployment of a Hybrid Runbook Worker in your data center to run the runbooks and access your GitHub Enterprise repository to synchronize runbooks with your Automation account.</span><span class="sxs-lookup"><span data-stu-id="03ee3-110">We will start by configuring Automation with the security credentials, runbooks required to support this scenario, and deployment of a Hybrid Runbook Worker in your data center to run the runbooks and access your GitHub Enterprise repository to synchronize runbooks with your Automation account.</span></span>  


## <a name="getting-the-scenario"></a><span data-ttu-id="03ee3-111">Getting the scenario</span><span class="sxs-lookup"><span data-stu-id="03ee3-111">Getting the scenario</span></span>

<span data-ttu-id="03ee3-112">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span><span class="sxs-lookup"><span data-stu-id="03ee3-112">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="03ee3-113">Runbooks</span><span class="sxs-lookup"><span data-stu-id="03ee3-113">Runbooks</span></span>

<span data-ttu-id="03ee3-114">Runbook</span><span class="sxs-lookup"><span data-stu-id="03ee3-114">Runbook</span></span> | <span data-ttu-id="03ee3-115">Description</span><span class="sxs-lookup"><span data-stu-id="03ee3-115">Description</span></span>| 
--------|------------|
<span data-ttu-id="03ee3-116">Export-RunAsCertificateToHybridWorker</span><span class="sxs-lookup"><span data-stu-id="03ee3-116">Export-RunAsCertificateToHybridWorker</span></span> | <span data-ttu-id="03ee3-117">Runbook will export a RunAs certificate from an Automation account to a hybrid worker so that runbooks on the worker can authenticate with Azure in order to import runbooks into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="03ee3-117">Runbook will export a RunAs certificate from an Automation account to a hybrid worker so that runbooks on the worker can authenticate with Azure in order to import runbooks into the Automation account.</span></span>| 
<span data-ttu-id="03ee3-118">Sync-LocalGitFolderToAutomationAccount</span><span class="sxs-lookup"><span data-stu-id="03ee3-118">Sync-LocalGitFolderToAutomationAccount</span></span> | <span data-ttu-id="03ee3-119">Runbook will sync the local Git folder on the hybrid machine and then import the runbook files (\*.ps1) into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="03ee3-119">Runbook will sync the local Git folder on the hybrid machine and then import the runbook files (\*.ps1) into the Automation account.</span></span>|

### <a name="credentials"></a><span data-ttu-id="03ee3-120">Credentials</span><span class="sxs-lookup"><span data-stu-id="03ee3-120">Credentials</span></span>

<span data-ttu-id="03ee3-121">Credential</span><span class="sxs-lookup"><span data-stu-id="03ee3-121">Credential</span></span> | <span data-ttu-id="03ee3-122">Description</span><span class="sxs-lookup"><span data-stu-id="03ee3-122">Description</span></span>|
-----------|------------|
<span data-ttu-id="03ee3-123">GitHRWCredential</span><span class="sxs-lookup"><span data-stu-id="03ee3-123">GitHRWCredential</span></span> | <span data-ttu-id="03ee3-124">Credential asset you will create that contains the username and password for a user with permissions to the hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="03ee3-124">Credential asset you will create that contains the username and password for a user with permissions to the hybrid worker.</span></span>|

## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="03ee3-125">Installing and configuring this scenario</span><span class="sxs-lookup"><span data-stu-id="03ee3-125">Installing and configuring this scenario</span></span>

### <a name="prerequisites"></a><span data-ttu-id="03ee3-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="03ee3-126">Prerequisites</span></span>

1. <span data-ttu-id="03ee3-127">The Sync-LocalGitFolderToAutomationAccount runbook authenticates using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="03ee3-127">The Sync-LocalGitFolderToAutomationAccount runbook authenticates using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span> 

2. <span data-ttu-id="03ee3-128">A Microsoft Operations Management Suite (OMS) workspace with the Azure Automation solution enabled and configured is also required.</span><span class="sxs-lookup"><span data-stu-id="03ee3-128">A Microsoft Operations Management Suite (OMS) workspace with the Azure Automation solution enabled and configured is also required.</span></span>  <span data-ttu-id="03ee3-129">If you do not have one that is associated with the Automation account used to install and configure this scenario, it will be created and configured for you when you execute the **New-OnPremiseHybridWorker.ps1** script from the hybrid runbook worker.</span><span class="sxs-lookup"><span data-stu-id="03ee3-129">If you do not have one that is associated with the Automation account used to install and configure this scenario, it will be created and configured for you when you execute the **New-OnPremiseHybridWorker.ps1** script from the hybrid runbook worker.</span></span>        

    > [!NOTE]
    > <span data-ttu-id="03ee3-130">Currently these are the only regions supported for Automation integration with OMS - **Australia Southeast**, **East US 2**, **Southeast Asia**, and **West Europe**.</span><span class="sxs-lookup"><span data-stu-id="03ee3-130">Currently these are the only regions supported for Automation integration with OMS - **Australia Southeast**, **East US 2**, **Southeast Asia**, and **West Europe**.</span></span> 

3. <span data-ttu-id="03ee3-131">A computer that can serve as a dedicated Hybrid Runbook Worker that will also host the GitHub software and maintain the runbook files (*runbook*.ps1) in a source directory on the file system to synchronize between GitHub and your Automation account.</span><span class="sxs-lookup"><span data-stu-id="03ee3-131">A computer that can serve as a dedicated Hybrid Runbook Worker that will also host the GitHub software and maintain the runbook files (*runbook*.ps1) in a source directory on the file system to synchronize between GitHub and your Automation account.</span></span>

### <a name="import-and-publish-the-runbooks"></a><span data-ttu-id="03ee3-132">Import and publish the runbooks</span><span class="sxs-lookup"><span data-stu-id="03ee3-132">Import and publish the runbooks</span></span>

<span data-ttu-id="03ee3-133">To import the *Export-RunAsCertificateToHybridWorker* and *Sync-LocalGitFolderToAutomationAccount* runbooks from the Runbook Gallery from your Automation account in the Azure portal, please follow the procedures in [Import Runbook from the Runbook Gallery](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="03ee3-133">To import the *Export-RunAsCertificateToHybridWorker* and *Sync-LocalGitFolderToAutomationAccount* runbooks from the Runbook Gallery from your Automation account in the Azure portal, please follow the procedures in [Import Runbook from the Runbook Gallery](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal).</span></span> <span data-ttu-id="03ee3-134">Publish the runbooks after they have been successfully imported into your Automation account.</span><span class="sxs-lookup"><span data-stu-id="03ee3-134">Publish the runbooks after they have been successfully imported into your Automation account.</span></span>

### <a name="deploy-and-configure-hybrid-runbook-worker"></a><span data-ttu-id="03ee3-135">Deploy and Configure Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="03ee3-135">Deploy and Configure Hybrid Runbook Worker</span></span>

<span data-ttu-id="03ee3-136">If you do not have a Hybrid Runbook Worker already deployed in your data center, you should review the requirements and follow the automated installation steps using the procedure in [Azure Automation Hybrid Runbook Workers - Automate Install and Configuration](automation-hybrid-runbook-worker.md#automated-deployment).</span><span class="sxs-lookup"><span data-stu-id="03ee3-136">If you do not have a Hybrid Runbook Worker already deployed in your data center, you should review the requirements and follow the automated installation steps using the procedure in [Azure Automation Hybrid Runbook Workers - Automate Install and Configuration](automation-hybrid-runbook-worker.md#automated-deployment).</span></span>  <span data-ttu-id="03ee3-137">Once you have successfully installed the hybrid worker on a computer, perform the following steps to complete its configuration to support this scenario.</span><span class="sxs-lookup"><span data-stu-id="03ee3-137">Once you have successfully installed the hybrid worker on a computer, perform the following steps to complete its configuration to support this scenario.</span></span>

1. <span data-ttu-id="03ee3-138">Log onto the computer hosting the Hybrid Runbook Worker role with an account that has local administrative rights and create a directory to hold the Git runbook files.</span><span class="sxs-lookup"><span data-stu-id="03ee3-138">Log onto the computer hosting the Hybrid Runbook Worker role with an account that has local administrative rights and create a directory to hold the Git runbook files.</span></span>  <span data-ttu-id="03ee3-139">Clone  the internal Git repository to the directory.</span><span class="sxs-lookup"><span data-stu-id="03ee3-139">Clone  the internal Git repository to the directory.</span></span>
2. <span data-ttu-id="03ee3-140">If you do not already have a RunAs account created or you want to create a new one dedicated for this purpose, from the Azure portal navigate to Automation accounts, select your Automation account and create a [credential asset](automation-credentials.md) that contains the username and password for a user with permissions to the hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="03ee3-140">If you do not already have a RunAs account created or you want to create a new one dedicated for this purpose, from the Azure portal navigate to Automation accounts, select your Automation account and create a [credential asset](automation-credentials.md) that contains the username and password for a user with permissions to the hybrid worker.</span></span>  
3. <span data-ttu-id="03ee3-141">From your Automation account, [edit the runbook](automation-edit-textual-runbook.md)  **Export-RunAsCertificateToHybridWorker** and modify the value for the variable *$Password* with a strong password.</span><span class="sxs-lookup"><span data-stu-id="03ee3-141">From your Automation account, [edit the runbook](automation-edit-textual-runbook.md)  **Export-RunAsCertificateToHybridWorker** and modify the value for the variable *$Password* with a strong password.</span></span>  <span data-ttu-id="03ee3-142">After you modify the value, click **Publish** to have the draft version of the runbook published.</span><span class="sxs-lookup"><span data-stu-id="03ee3-142">After you modify the value, click **Publish** to have the draft version of the runbook published.</span></span> 
5. <span data-ttu-id="03ee3-143">Start the runbook **Export-RunAsCertificateToHybridWorker**, and in the **Start Runbook** blade, under the option **Run settings** select the option **Hybrid Worker** and in the drop-down list select the Hybrid worker group you created earlier for this scenario.</span><span class="sxs-lookup"><span data-stu-id="03ee3-143">Start the runbook **Export-RunAsCertificateToHybridWorker**, and in the **Start Runbook** blade, under the option **Run settings** select the option **Hybrid Worker** and in the drop-down list select the Hybrid worker group you created earlier for this scenario.</span></span>  

    <span data-ttu-id="03ee3-144">This will export a certificate to the hybrid worker so that runbooks on the worker can authenticate with Azure using the Run As connection in order to manage Azure resources (in particular for this scenario - import runbooks to the Automation account).</span><span class="sxs-lookup"><span data-stu-id="03ee3-144">This will export a certificate to the hybrid worker so that runbooks on the worker can authenticate with Azure using the Run As connection in order to manage Azure resources (in particular for this scenario - import runbooks to the Automation account).</span></span>

4. <span data-ttu-id="03ee3-145">From your Automation account, select the Hybrid worker group created earlier and [specify a RunAs account](automation-hybrid-runbook-worker.md#runas-account) for the for the Hybrid worker group, and chose the credential asset you just or already have created.</span><span class="sxs-lookup"><span data-stu-id="03ee3-145">From your Automation account, select the Hybrid worker group created earlier and [specify a RunAs account](automation-hybrid-runbook-worker.md#runas-account) for the for the Hybrid worker group, and chose the credential asset you just or already have created.</span></span>  <span data-ttu-id="03ee3-146">This assures that the Sync runbook can run Git commands.</span><span class="sxs-lookup"><span data-stu-id="03ee3-146">This assures that the Sync runbook can run Git commands.</span></span> 
5. <span data-ttu-id="03ee3-147">Start the runbook **Sync-LocalGitFolderToAutomationAccount**, provide the following required input parameter values and in the **Start Runbook** blade, under the option **Run settings** select the option **Hybrid Worker** and in the drop-down list select the Hybrid worker group you created earlier for this scenario:</span><span class="sxs-lookup"><span data-stu-id="03ee3-147">Start the runbook **Sync-LocalGitFolderToAutomationAccount**, provide the following required input parameter values and in the **Start Runbook** blade, under the option **Run settings** select the option **Hybrid Worker** and in the drop-down list select the Hybrid worker group you created earlier for this scenario:</span></span>
    * <span data-ttu-id="03ee3-148">*ResourceGroup* - the name of your resource group associated with your Automation account</span><span class="sxs-lookup"><span data-stu-id="03ee3-148">*ResourceGroup* - the name of your resource group associated with your Automation account</span></span>
    * <span data-ttu-id="03ee3-149">*AutomationAccountName* - the name of your Automation account</span><span class="sxs-lookup"><span data-stu-id="03ee3-149">*AutomationAccountName* - the name of your Automation account</span></span>
    * <span data-ttu-id="03ee3-150">*GitPath* - The local folder or file on the Hybrid Runbook Worker where Git is set up to pull latest changes into</span><span class="sxs-lookup"><span data-stu-id="03ee3-150">*GitPath* - The local folder or file on the Hybrid Runbook Worker where Git is set up to pull latest changes into</span></span>

    <span data-ttu-id="03ee3-151">This will sync the local Git folder on the hybrid worker computer and then import the .ps1 files from the source directory to the Automation account.</span><span class="sxs-lookup"><span data-stu-id="03ee3-151">This will sync the local Git folder on the hybrid worker computer and then import the .ps1 files from the source directory to the Automation account.</span></span>

    ![Start Sync-LocalGitFolderToAutomationAccount Runbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. <span data-ttu-id="03ee3-153">View job summary details for the runbook by selecting it from the **Runbooks** blade in your Automation account, and then select the **Jobs** tile.</span><span class="sxs-lookup"><span data-stu-id="03ee3-153">View job summary details for the runbook by selecting it from the **Runbooks** blade in your Automation account, and then select the **Jobs** tile.</span></span>  <span data-ttu-id="03ee3-154">Confirm it completed successfully by selecting the **All logs** tile and reviewing the detailed log stream.</span><span class="sxs-lookup"><span data-stu-id="03ee3-154">Confirm it completed successfully by selecting the **All logs** tile and reviewing the detailed log stream.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="03ee3-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="03ee3-155">Next steps</span></span>

-  <span data-ttu-id="03ee3-156">To know more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="03ee3-156">To know more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>
-  <span data-ttu-id="03ee3-157">For more information on PowerShell script support feature, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span><span class="sxs-lookup"><span data-stu-id="03ee3-157">For more information on PowerShell script support feature, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span></span>
