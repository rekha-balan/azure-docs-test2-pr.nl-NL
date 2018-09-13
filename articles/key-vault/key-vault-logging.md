---
title: Azure Key Vault Logging | Microsoft Docs
description: Use this tutorial to help you get started with Azure Key Vault logging.
services: key-vault
documentationcenter: ''
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: cabailey
ms.openlocfilehash: 51732acdad74dd6dbfc47fae62efc87df6ce5c15
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553580"
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="edd40-103">Azure Key Vault Logging</span><span class="sxs-lookup"><span data-stu-id="edd40-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="edd40-104">Azure Key Vault is available in most regions.</span><span class="sxs-lookup"><span data-stu-id="edd40-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="edd40-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="edd40-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="edd40-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="edd40-106">Introduction</span></span>
<span data-ttu-id="edd40-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span><span class="sxs-lookup"><span data-stu-id="edd40-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="edd40-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span><span class="sxs-lookup"><span data-stu-id="edd40-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="edd40-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span><span class="sxs-lookup"><span data-stu-id="edd40-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="edd40-110">You can access your logging information at most, 10 minutes after the key vault operation.</span><span class="sxs-lookup"><span data-stu-id="edd40-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="edd40-111">In most cases, it will be quicker than this.</span><span class="sxs-lookup"><span data-stu-id="edd40-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="edd40-112">It's up to you to manage your logs in your storage account:</span><span class="sxs-lookup"><span data-stu-id="edd40-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="edd40-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span><span class="sxs-lookup"><span data-stu-id="edd40-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="edd40-114">Delete logs that you no longer want to keep in your storage account.</span><span class="sxs-lookup"><span data-stu-id="edd40-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="edd40-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span><span class="sxs-lookup"><span data-stu-id="edd40-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="edd40-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span><span class="sxs-lookup"><span data-stu-id="edd40-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="edd40-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="edd40-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="edd40-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="edd40-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli.md).</span></span>
> 
> <span data-ttu-id="edd40-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="edd40-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="edd40-120">Instead, use these Azure PowerShell instructions.</span><span class="sxs-lookup"><span data-stu-id="edd40-120">Instead, use these Azure PowerShell instructions.</span></span>
> 
> 

<span data-ttu-id="edd40-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="edd40-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edd40-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="edd40-122">Prerequisites</span></span>
<span data-ttu-id="edd40-123">To complete this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="edd40-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="edd40-124">An existing key vault that you have been using.</span><span class="sxs-lookup"><span data-stu-id="edd40-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="edd40-125">Azure PowerShell, **minimum version of 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="edd40-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="edd40-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="edd40-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="edd40-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="edd40-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="edd40-128">Sufficient storage on Azure for your Key Vault logs.</span><span class="sxs-lookup"><span data-stu-id="edd40-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <a id="connect"></a><span data-ttu-id="edd40-129">Connect to your subscriptions</span><span class="sxs-lookup"><span data-stu-id="edd40-129">Connect to your subscriptions</span></span>
<span data-ttu-id="edd40-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span><span class="sxs-lookup"><span data-stu-id="edd40-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="edd40-131">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="edd40-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="edd40-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span><span class="sxs-lookup"><span data-stu-id="edd40-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="edd40-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="edd40-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="edd40-134">Type the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="edd40-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="edd40-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span><span class="sxs-lookup"><span data-stu-id="edd40-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="edd40-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span><span class="sxs-lookup"><span data-stu-id="edd40-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="edd40-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span><span class="sxs-lookup"><span data-stu-id="edd40-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span> 
>   
>

<span data-ttu-id="edd40-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="edd40-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a id="storage"></a><span data-ttu-id="edd40-139">Create a new storage account for your logs</span><span class="sxs-lookup"><span data-stu-id="edd40-139">Create a new storage account for your logs</span></span>
<span data-ttu-id="edd40-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span><span class="sxs-lookup"><span data-stu-id="edd40-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="edd40-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span><span class="sxs-lookup"><span data-stu-id="edd40-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="edd40-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span><span class="sxs-lookup"><span data-stu-id="edd40-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="edd40-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span><span class="sxs-lookup"><span data-stu-id="edd40-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="edd40-144">Substitute these values for your own, as applicable:</span><span class="sxs-lookup"><span data-stu-id="edd40-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="edd40-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="edd40-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
> 
> 

## <a id="identify"></a><span data-ttu-id="edd40-146">Identify the key vault for your logs</span><span class="sxs-lookup"><span data-stu-id="edd40-146">Identify the key vault for your logs</span></span>
<span data-ttu-id="edd40-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span><span class="sxs-lookup"><span data-stu-id="edd40-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a><span data-ttu-id="edd40-148">Enable logging</span><span class="sxs-lookup"><span data-stu-id="edd40-148">Enable logging</span></span>
<span data-ttu-id="edd40-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span><span class="sxs-lookup"><span data-stu-id="edd40-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="edd40-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span><span class="sxs-lookup"><span data-stu-id="edd40-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="edd40-151">The output for this includes:</span><span class="sxs-lookup"><span data-stu-id="edd40-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="edd40-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span><span class="sxs-lookup"><span data-stu-id="edd40-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="edd40-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="edd40-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="edd40-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="edd40-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="edd40-155">What's logged:</span><span class="sxs-lookup"><span data-stu-id="edd40-155">What's logged:</span></span>

* <span data-ttu-id="edd40-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span><span class="sxs-lookup"><span data-stu-id="edd40-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="edd40-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span><span class="sxs-lookup"><span data-stu-id="edd40-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="edd40-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span><span class="sxs-lookup"><span data-stu-id="edd40-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="edd40-159">Unauthenticated requests that result in a 401 response.</span><span class="sxs-lookup"><span data-stu-id="edd40-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="edd40-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span><span class="sxs-lookup"><span data-stu-id="edd40-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <a id="access"></a><span data-ttu-id="edd40-161">Access your logs</span><span class="sxs-lookup"><span data-stu-id="edd40-161">Access your logs</span></span>
<span data-ttu-id="edd40-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span><span class="sxs-lookup"><span data-stu-id="edd40-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="edd40-163">To list all the blobs in this container, type:</span><span class="sxs-lookup"><span data-stu-id="edd40-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="edd40-164">First, create a variable for the container name.</span><span class="sxs-lookup"><span data-stu-id="edd40-164">First, create a variable for the container name.</span></span> <span data-ttu-id="edd40-165">This will be used throughout the rest of the walk through.</span><span class="sxs-lookup"><span data-stu-id="edd40-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="edd40-166">To list all the blobs in this container, type:</span><span class="sxs-lookup"><span data-stu-id="edd40-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="edd40-167">The output will look something similar to this:</span><span class="sxs-lookup"><span data-stu-id="edd40-167">The output will look something similar to this:</span></span>

<span data-ttu-id="edd40-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="edd40-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="edd40-169">**Name**</span><span class="sxs-lookup"><span data-stu-id="edd40-169">**Name**</span></span>

- - -
<span data-ttu-id="edd40-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="edd40-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="edd40-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="edd40-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="edd40-172">\*\*resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="edd40-172">\*\*resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json\*\*\*\*</span></span>

<span data-ttu-id="edd40-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="edd40-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="edd40-174">The date and time values use UTC.</span><span class="sxs-lookup"><span data-stu-id="edd40-174">The date and time values use UTC.</span></span>

<span data-ttu-id="edd40-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span><span class="sxs-lookup"><span data-stu-id="edd40-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="edd40-176">But before we do that, we'll first cover how to download all the blobs.</span><span class="sxs-lookup"><span data-stu-id="edd40-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="edd40-177">First, create a folder to download the blobs.</span><span class="sxs-lookup"><span data-stu-id="edd40-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="edd40-178">For example:</span><span class="sxs-lookup"><span data-stu-id="edd40-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="edd40-179">Then get a list of all blobs:</span><span class="sxs-lookup"><span data-stu-id="edd40-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="edd40-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span><span class="sxs-lookup"><span data-stu-id="edd40-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="edd40-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span><span class="sxs-lookup"><span data-stu-id="edd40-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="edd40-182">To selectively download blobs, use wildcards.</span><span class="sxs-lookup"><span data-stu-id="edd40-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="edd40-183">For example:</span><span class="sxs-lookup"><span data-stu-id="edd40-183">For example:</span></span>

* <span data-ttu-id="edd40-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="edd40-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>
  
        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="edd40-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="edd40-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>
  
        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="edd40-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="edd40-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>
  
        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="edd40-187">You're now ready to start looking at what's in the logs.</span><span class="sxs-lookup"><span data-stu-id="edd40-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="edd40-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span><span class="sxs-lookup"><span data-stu-id="edd40-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="edd40-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="edd40-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="edd40-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="edd40-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <a id="interpret"></a><span data-ttu-id="edd40-191">Interpret your Key Vault logs</span><span class="sxs-lookup"><span data-stu-id="edd40-191">Interpret your Key Vault logs</span></span>
<span data-ttu-id="edd40-192">Individual blobs are stored as text, formatted as a JSON blob.</span><span class="sxs-lookup"><span data-stu-id="edd40-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="edd40-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="edd40-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="edd40-194">The following table lists the field names and descriptions.</span><span class="sxs-lookup"><span data-stu-id="edd40-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="edd40-195">Field name</span><span class="sxs-lookup"><span data-stu-id="edd40-195">Field name</span></span> | <span data-ttu-id="edd40-196">Description</span><span class="sxs-lookup"><span data-stu-id="edd40-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="edd40-197">time</span><span class="sxs-lookup"><span data-stu-id="edd40-197">time</span></span> |<span data-ttu-id="edd40-198">Date and time (UTC).</span><span class="sxs-lookup"><span data-stu-id="edd40-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="edd40-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="edd40-199">resourceId</span></span> |<span data-ttu-id="edd40-200">Azure Resource Manager Resource ID.</span><span class="sxs-lookup"><span data-stu-id="edd40-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="edd40-201">For Key Vault logs, this is always the  Key Vault resource ID.</span><span class="sxs-lookup"><span data-stu-id="edd40-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="edd40-202">operationName</span><span class="sxs-lookup"><span data-stu-id="edd40-202">operationName</span></span> |<span data-ttu-id="edd40-203">Name of the operation, as documented in the next table.</span><span class="sxs-lookup"><span data-stu-id="edd40-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="edd40-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="edd40-204">operationVersion</span></span> |<span data-ttu-id="edd40-205">This is the REST API version requested by the client.</span><span class="sxs-lookup"><span data-stu-id="edd40-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="edd40-206">category</span><span class="sxs-lookup"><span data-stu-id="edd40-206">category</span></span> |<span data-ttu-id="edd40-207">For Key Vault logs, AuditEvent is the single, available value.</span><span class="sxs-lookup"><span data-stu-id="edd40-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="edd40-208">resultType</span><span class="sxs-lookup"><span data-stu-id="edd40-208">resultType</span></span> |<span data-ttu-id="edd40-209">Result of REST API request.</span><span class="sxs-lookup"><span data-stu-id="edd40-209">Result of REST API request.</span></span> |
| <span data-ttu-id="edd40-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="edd40-210">resultSignature</span></span> |<span data-ttu-id="edd40-211">HTTP status.</span><span class="sxs-lookup"><span data-stu-id="edd40-211">HTTP status.</span></span> |
| <span data-ttu-id="edd40-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="edd40-212">resultDescription</span></span> |<span data-ttu-id="edd40-213">Additional description about the result, when available.</span><span class="sxs-lookup"><span data-stu-id="edd40-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="edd40-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="edd40-214">durationMs</span></span> |<span data-ttu-id="edd40-215">Time it took to service the REST API request, in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="edd40-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="edd40-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span><span class="sxs-lookup"><span data-stu-id="edd40-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="edd40-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="edd40-217">callerIpAddress</span></span> |<span data-ttu-id="edd40-218">IP address of the client who made the request.</span><span class="sxs-lookup"><span data-stu-id="edd40-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="edd40-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="edd40-219">correlationId</span></span> |<span data-ttu-id="edd40-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span><span class="sxs-lookup"><span data-stu-id="edd40-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="edd40-221">identity</span><span class="sxs-lookup"><span data-stu-id="edd40-221">identity</span></span> |<span data-ttu-id="edd40-222">Identity from the token that was presented when making the REST API request.</span><span class="sxs-lookup"><span data-stu-id="edd40-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="edd40-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="edd40-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="edd40-224">properties</span><span class="sxs-lookup"><span data-stu-id="edd40-224">properties</span></span> |<span data-ttu-id="edd40-225">This field will contain different information based on the operation (operationName).</span><span class="sxs-lookup"><span data-stu-id="edd40-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="edd40-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span><span class="sxs-lookup"><span data-stu-id="edd40-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="edd40-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span><span class="sxs-lookup"><span data-stu-id="edd40-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="edd40-228">The **operationName** field values are in ObjectVerb format.</span><span class="sxs-lookup"><span data-stu-id="edd40-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="edd40-229">For example:</span><span class="sxs-lookup"><span data-stu-id="edd40-229">For example:</span></span>

* <span data-ttu-id="edd40-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="edd40-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="edd40-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="edd40-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="edd40-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="edd40-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="edd40-233">The following table lists the operationName and corresponding REST API command.</span><span class="sxs-lookup"><span data-stu-id="edd40-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="edd40-234">operationName</span><span class="sxs-lookup"><span data-stu-id="edd40-234">operationName</span></span> | <span data-ttu-id="edd40-235">REST API Command</span><span class="sxs-lookup"><span data-stu-id="edd40-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="edd40-236">Authentication</span><span class="sxs-lookup"><span data-stu-id="edd40-236">Authentication</span></span> |<span data-ttu-id="edd40-237">Via Azure Active Directory endpoint</span><span class="sxs-lookup"><span data-stu-id="edd40-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="edd40-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="edd40-238">VaultGet</span></span> |[<span data-ttu-id="edd40-239">Get information about a key vault</span><span class="sxs-lookup"><span data-stu-id="edd40-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="edd40-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="edd40-240">VaultPut</span></span> |[<span data-ttu-id="edd40-241">Create or update a key vault</span><span class="sxs-lookup"><span data-stu-id="edd40-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="edd40-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="edd40-242">VaultDelete</span></span> |[<span data-ttu-id="edd40-243">Delete a key vault</span><span class="sxs-lookup"><span data-stu-id="edd40-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="edd40-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="edd40-244">VaultPatch</span></span> |[<span data-ttu-id="edd40-245">Update a key vault</span><span class="sxs-lookup"><span data-stu-id="edd40-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="edd40-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="edd40-246">VaultList</span></span> |[<span data-ttu-id="edd40-247">List all key vaults in a resource group</span><span class="sxs-lookup"><span data-stu-id="edd40-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="edd40-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="edd40-248">KeyCreate</span></span> |[<span data-ttu-id="edd40-249">Create a key</span><span class="sxs-lookup"><span data-stu-id="edd40-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="edd40-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="edd40-250">KeyGet</span></span> |[<span data-ttu-id="edd40-251">Get information about a key</span><span class="sxs-lookup"><span data-stu-id="edd40-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="edd40-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="edd40-252">KeyImport</span></span> |[<span data-ttu-id="edd40-253">Import a key into a vault</span><span class="sxs-lookup"><span data-stu-id="edd40-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="edd40-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="edd40-254">KeyBackup</span></span> |<span data-ttu-id="edd40-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="edd40-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="edd40-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="edd40-256">KeyDelete</span></span> |[<span data-ttu-id="edd40-257">Delete a key</span><span class="sxs-lookup"><span data-stu-id="edd40-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="edd40-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="edd40-258">KeyRestore</span></span> |[<span data-ttu-id="edd40-259">Restore a key</span><span class="sxs-lookup"><span data-stu-id="edd40-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="edd40-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="edd40-260">KeySign</span></span> |[<span data-ttu-id="edd40-261">Sign with a key</span><span class="sxs-lookup"><span data-stu-id="edd40-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="edd40-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="edd40-262">KeyVerify</span></span> |[<span data-ttu-id="edd40-263">Verify with a key</span><span class="sxs-lookup"><span data-stu-id="edd40-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="edd40-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="edd40-264">KeyWrap</span></span> |[<span data-ttu-id="edd40-265">Wrap a key</span><span class="sxs-lookup"><span data-stu-id="edd40-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="edd40-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="edd40-266">KeyUnwrap</span></span> |[<span data-ttu-id="edd40-267">Unwrap a key</span><span class="sxs-lookup"><span data-stu-id="edd40-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="edd40-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="edd40-268">KeyEncrypt</span></span> |[<span data-ttu-id="edd40-269">Encrypt with a key</span><span class="sxs-lookup"><span data-stu-id="edd40-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="edd40-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="edd40-270">KeyDecrypt</span></span> |[<span data-ttu-id="edd40-271">Decrypt with a key</span><span class="sxs-lookup"><span data-stu-id="edd40-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="edd40-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="edd40-272">KeyUpdate</span></span> |[<span data-ttu-id="edd40-273">Update a key</span><span class="sxs-lookup"><span data-stu-id="edd40-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="edd40-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="edd40-274">KeyList</span></span> |[<span data-ttu-id="edd40-275">List the keys in a vault</span><span class="sxs-lookup"><span data-stu-id="edd40-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="edd40-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="edd40-276">KeyListVersions</span></span> |[<span data-ttu-id="edd40-277">List the versions of a key</span><span class="sxs-lookup"><span data-stu-id="edd40-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="edd40-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="edd40-278">SecretSet</span></span> |[<span data-ttu-id="edd40-279">Create a secret</span><span class="sxs-lookup"><span data-stu-id="edd40-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="edd40-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="edd40-280">SecretGet</span></span> |[<span data-ttu-id="edd40-281">Get secret</span><span class="sxs-lookup"><span data-stu-id="edd40-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="edd40-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="edd40-282">SecretUpdate</span></span> |[<span data-ttu-id="edd40-283">Update a secret</span><span class="sxs-lookup"><span data-stu-id="edd40-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="edd40-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="edd40-284">SecretDelete</span></span> |[<span data-ttu-id="edd40-285">Delete a secret</span><span class="sxs-lookup"><span data-stu-id="edd40-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="edd40-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="edd40-286">SecretList</span></span> |[<span data-ttu-id="edd40-287">List secrets in a vault</span><span class="sxs-lookup"><span data-stu-id="edd40-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="edd40-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="edd40-288">SecretListVersions</span></span> |[<span data-ttu-id="edd40-289">List versions of a secret</span><span class="sxs-lookup"><span data-stu-id="edd40-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a><span data-ttu-id="edd40-290">Use Log Analytics</span><span class="sxs-lookup"><span data-stu-id="edd40-290">Use Log Analytics</span></span>

<span data-ttu-id="edd40-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span><span class="sxs-lookup"><span data-stu-id="edd40-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="edd40-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="edd40-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="edd40-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span><span class="sxs-lookup"><span data-stu-id="edd40-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <a id="next"></a><span data-ttu-id="edd40-294">Next steps</span><span class="sxs-lookup"><span data-stu-id="edd40-294">Next steps</span></span>
<span data-ttu-id="edd40-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="edd40-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="edd40-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="edd40-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="edd40-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="edd40-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span>

<span data-ttu-id="edd40-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="edd40-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>

