---
title: DocumentDB Automation - Managing Regions | Microsoft Docs
description: Use Azure CLI 1.0 and Azure Resource Manager to manage regions in a DocumentDB database account. DocumentDB is a cloud-based NoSQL database for JSON data.
services: documentdb
author: dmakwana
manager: jhubbard
editor: ''
tags: azure-resource-manager
documentationcenter: ''
ms.assetid: 7f765c17-8549-4108-9475-46394fc3a218
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: dimakwan
ms.openlocfilehash: 598cdc91e9fc019b473d6e85bfc7167aaa95ef93
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563454"
---
# <a name="automate-documentdb-account-region-management-using-azure-cli-10-and-azure-resource-manager-templates"></a><span data-ttu-id="ecb86-104">Automate DocumentDB account region management using Azure CLI 1.0 and Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ecb86-104">Automate DocumentDB account region management using Azure CLI 1.0 and Azure Resource Manager templates</span></span>

<span data-ttu-id="ecb86-105">This article shows you how to add/remove a region in your Azure DocumentDB account by using Azure CLI 1.0 commands and Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="ecb86-105">This article shows you how to add/remove a region in your Azure DocumentDB account by using Azure CLI 1.0 commands and Azure Resource Manager templates.</span></span> <span data-ttu-id="ecb86-106">Region management can also be accomplished through the [Azure Portal](documentdb-portal-global-replication.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-106">Region management can also be accomplished through the [Azure Portal](documentdb-portal-global-replication.md).</span></span> <span data-ttu-id="ecb86-107">Note that the commands in the following tutorial do not allow you to change failover priorities of the various regions.</span><span class="sxs-lookup"><span data-stu-id="ecb86-107">Note that the commands in the following tutorial do not allow you to change failover priorities of the various regions.</span></span> <span data-ttu-id="ecb86-108">Only read regions can  be added or removed.</span><span class="sxs-lookup"><span data-stu-id="ecb86-108">Only read regions can  be added or removed.</span></span> <span data-ttu-id="ecb86-109">The write region of a database account (failover priority of 0) cannot be added/removed.</span><span class="sxs-lookup"><span data-stu-id="ecb86-109">The write region of a database account (failover priority of 0) cannot be added/removed.</span></span>

<span data-ttu-id="ecb86-110">DocumentDB database accounts are currently the only DocumentDB resource that can be created/modified using [Azure Resource Manager templates and Azure CLI 1.0](documentdb-automation-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-110">DocumentDB database accounts are currently the only DocumentDB resource that can be created/modified using [Azure Resource Manager templates and Azure CLI 1.0](documentdb-automation-resource-manager-cli.md).</span></span>

## <a name="getting-ready"></a><span data-ttu-id="ecb86-111">Getting ready</span><span class="sxs-lookup"><span data-stu-id="ecb86-111">Getting ready</span></span>

<span data-ttu-id="ecb86-112">Before you can use Azure CLI 1.0 with Azure resource groups, you need to have the right Azure CLI 1.0 version and an Azure account.</span><span class="sxs-lookup"><span data-stu-id="ecb86-112">Before you can use Azure CLI 1.0 with Azure resource groups, you need to have the right Azure CLI 1.0 version and an Azure account.</span></span> <span data-ttu-id="ecb86-113">If you don't have Azure CLI 1.0, [install it](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-113">If you don't have Azure CLI 1.0, [install it](../cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-10-version"></a><span data-ttu-id="ecb86-114">Update your Azure CLI 1.0 version</span><span class="sxs-lookup"><span data-stu-id="ecb86-114">Update your Azure CLI 1.0 version</span></span>

<span data-ttu-id="ecb86-115">At the command prompt, type `azure --version` to see whether you have already installed version 0.10.4 or later.</span><span class="sxs-lookup"><span data-stu-id="ecb86-115">At the command prompt, type `azure --version` to see whether you have already installed version 0.10.4 or later.</span></span> <span data-ttu-id="ecb86-116">You may be prompted to participate in Microsoft Azure CLI 1.0 data collection at this step, and can select y or n to opt-in or opt-out.</span><span class="sxs-lookup"><span data-stu-id="ecb86-116">You may be prompted to participate in Microsoft Azure CLI 1.0 data collection at this step, and can select y or n to opt-in or opt-out.</span></span>

    azure --version
    0.10.4 (node: 4.2.4)

<span data-ttu-id="ecb86-117">If your version is not 0.10.4 or later, you need to either [install Azure CLI 1.0](../cli-install-nodejs.md) or update by using one of the native installers, or through **npm** by typing `npm update -g azure-cli` to update or `npm install -g azure-cli` to install.</span><span class="sxs-lookup"><span data-stu-id="ecb86-117">If your version is not 0.10.4 or later, you need to either [install Azure CLI 1.0](../cli-install-nodejs.md) or update by using one of the native installers, or through **npm** by typing `npm update -g azure-cli` to update or `npm install -g azure-cli` to install.</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="ecb86-118">Set your Azure account and subscription</span><span class="sxs-lookup"><span data-stu-id="ecb86-118">Set your Azure account and subscription</span></span>

<span data-ttu-id="ecb86-119">If you don't already have an Azure subscription but you do have a Visual Studio subscription, you can activate your [Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="ecb86-119">If you don't already have an Azure subscription but you do have a Visual Studio subscription, you can activate your [Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="ecb86-120">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecb86-120">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="ecb86-121">You need to have a work or school account or a Microsoft account identity to use Azure resource management templates.</span><span class="sxs-lookup"><span data-stu-id="ecb86-121">You need to have a work or school account or a Microsoft account identity to use Azure resource management templates.</span></span> <span data-ttu-id="ecb86-122">If you have one of these accounts, type the following command.</span><span class="sxs-lookup"><span data-stu-id="ecb86-122">If you have one of these accounts, type the following command.</span></span>

    azure login

<span data-ttu-id="ecb86-123">Which produces the following output:</span><span class="sxs-lookup"><span data-stu-id="ecb86-123">Which produces the following output:</span></span> 

    info:    Executing command login
    |info:    To sign in, use a web browser to open the page https://aka.ms/devicelogin. 
    Enter the code E1A2B3C4D to authenticate.

> [!NOTE]
> <span data-ttu-id="ecb86-124">If you don't have an Azure account, you'll see an error message indicating that you need a different type of account.</span><span class="sxs-lookup"><span data-stu-id="ecb86-124">If you don't have an Azure account, you'll see an error message indicating that you need a different type of account.</span></span> <span data-ttu-id="ecb86-125">To create one from your current Azure account, see [Creating a work or school identity in Azure Active Directory](../virtual-machines/windows/create-aad-work-id.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-125">To create one from your current Azure account, see [Creating a work or school identity in Azure Active Directory](../virtual-machines/windows/create-aad-work-id.md).</span></span>

<span data-ttu-id="ecb86-126">Open [https://aka.ms/devicelogin](https://aka.ms/devicelogin) in a browser and enter the code provided in the command output.</span><span class="sxs-lookup"><span data-stu-id="ecb86-126">Open [https://aka.ms/devicelogin](https://aka.ms/devicelogin) in a browser and enter the code provided in the command output.</span></span>

![Screenshot showing the device login screen for Microsoft Azure CLI 1.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/azure-cli-login-code.png)

<span data-ttu-id="ecb86-128">Once you've entered the code, select the identity you want to use in the browser and provide your user name and password if needed.</span><span class="sxs-lookup"><span data-stu-id="ecb86-128">Once you've entered the code, select the identity you want to use in the browser and provide your user name and password if needed.</span></span>

![Screenshot showing where to select the Microsoft identity account associated with the Azure subscription you want to use](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/identity-cli-login.png)

<span data-ttu-id="ecb86-130">You'll receive the following confirmation screen when you're successfully logged in, and you can then close the browser window.</span><span class="sxs-lookup"><span data-stu-id="ecb86-130">You'll receive the following confirmation screen when you're successfully logged in, and you can then close the browser window.</span></span>

![Screenshot showing confirmation of login to the Microsoft Azure Cross-platform Command Line Interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/login-confirmation.png)

<span data-ttu-id="ecb86-132">The command shell also provides the following output.</span><span class="sxs-lookup"><span data-stu-id="ecb86-132">The command shell also provides the following output.</span></span>

    /info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

<span data-ttu-id="ecb86-133">In addition to the interactive login method described here, there are additional Azure CLI 1.0 login methods available.</span><span class="sxs-lookup"><span data-stu-id="ecb86-133">In addition to the interactive login method described here, there are additional Azure CLI 1.0 login methods available.</span></span> <span data-ttu-id="ecb86-134">For more information about the other methods and information about handling multiple subscriptions, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI 1.0)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-134">For more information about the other methods and information about handling multiple subscriptions, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI 1.0)](../xplat-cli-connect.md).</span></span>

### <a name="switch-to-azure-cli-10-resource-group-mode"></a><span data-ttu-id="ecb86-135">Switch to Azure CLI 1.0 resource group mode</span><span class="sxs-lookup"><span data-stu-id="ecb86-135">Switch to Azure CLI 1.0 resource group mode</span></span>

<span data-ttu-id="ecb86-136">By default, Azure CLI 1.0 starts in the service management mode (**asm** mode).</span><span class="sxs-lookup"><span data-stu-id="ecb86-136">By default, Azure CLI 1.0 starts in the service management mode (**asm** mode).</span></span> <span data-ttu-id="ecb86-137">Type the following to switch to resource group mode.</span><span class="sxs-lookup"><span data-stu-id="ecb86-137">Type the following to switch to resource group mode.</span></span>

    azure config mode arm

<span data-ttu-id="ecb86-138">Which provides the following output:</span><span class="sxs-lookup"><span data-stu-id="ecb86-138">Which provides the following output:</span></span>

    info:    Executing command config mode
    info:    New mode is arm
    info:    config mode command OK

<span data-ttu-id="ecb86-139">If needed, you can switch back to the default set of commands by typing `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="ecb86-139">If needed, you can switch back to the default set of commands by typing `azure config mode asm`.</span></span>

### <a name="create-or-retrieve-your-resource-group"></a><span data-ttu-id="ecb86-140">Create or retrieve your resource group</span><span class="sxs-lookup"><span data-stu-id="ecb86-140">Create or retrieve your resource group</span></span>

<span data-ttu-id="ecb86-141">In order to create a DocumentDB account, you first need a resource group.</span><span class="sxs-lookup"><span data-stu-id="ecb86-141">In order to create a DocumentDB account, you first need a resource group.</span></span> <span data-ttu-id="ecb86-142">If you already know the name of the resource group that you'd like to use, then skip to [Step 2](#create-documentdb-account-cli).</span><span class="sxs-lookup"><span data-stu-id="ecb86-142">If you already know the name of the resource group that you'd like to use, then skip to [Step 2](#create-documentdb-account-cli).</span></span> 

<span data-ttu-id="ecb86-143">To review a list of all of your current resource groups, run the following command and take note of the resource group name you'd like to use:</span><span class="sxs-lookup"><span data-stu-id="ecb86-143">To review a list of all of your current resource groups, run the following command and take note of the resource group name you'd like to use:</span></span> 

    azure group list

<span data-ttu-id="ecb86-144">To create a new resource group, run the following command, specify the name of the new resource group to create, and the region in which to create the resource group:</span><span class="sxs-lookup"><span data-stu-id="ecb86-144">To create a new resource group, run the following command, specify the name of the new resource group to create, and the region in which to create the resource group:</span></span> 

    azure group create <resourcegroupname> <resourcegrouplocation>

 - <span data-ttu-id="ecb86-145">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span><span class="sxs-lookup"><span data-stu-id="ecb86-145">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span></span> 
 - <span data-ttu-id="ecb86-146">`<resourcegrouplocation>` must be one of the regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="ecb86-146">`<resourcegrouplocation>` must be one of the regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="ecb86-147">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ecb86-147">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

<span data-ttu-id="ecb86-148">Example input:</span><span class="sxs-lookup"><span data-stu-id="ecb86-148">Example input:</span></span>

    azure group create new_res_group westus

<span data-ttu-id="ecb86-149">Which produces the following output:</span><span class="sxs-lookup"><span data-stu-id="ecb86-149">Which produces the following output:</span></span>

    info:    Executing command group create
    + Getting resource group new_res_group
    + Creating resource group new_res_group
    info:    Created resource group new_res_group
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/new_res_group
    data:    Name:                new_res_group
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="ecb86-150">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ecb86-150">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span> 

## <a name="understanding-azure-resource-manager-templates-and-resource-groups"></a><span data-ttu-id="ecb86-151">Understanding Azure Resource Manager templates and resource groups</span><span class="sxs-lookup"><span data-stu-id="ecb86-151">Understanding Azure Resource Manager templates and resource groups</span></span>

<span data-ttu-id="ecb86-152">Most applications are built from a combination of different resource types (such as one or more DocumentDB account, storage accounts, a virtual network, or a content delivery network).</span><span class="sxs-lookup"><span data-stu-id="ecb86-152">Most applications are built from a combination of different resource types (such as one or more DocumentDB account, storage accounts, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="ecb86-153">The default Azure service management API and the Azure portal represented these items by using a service-by-service approach.</span><span class="sxs-lookup"><span data-stu-id="ecb86-153">The default Azure service management API and the Azure portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="ecb86-154">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span><span class="sxs-lookup"><span data-stu-id="ecb86-154">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="ecb86-155">*Azure Resource Manager templates* make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span><span class="sxs-lookup"><span data-stu-id="ecb86-155">*Azure Resource Manager templates* make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="ecb86-156">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span><span class="sxs-lookup"><span data-stu-id="ecb86-156">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span></span>

<span data-ttu-id="ecb86-157">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-157">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ecb86-158">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-158">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>


## <a id="add-region-documentdb-account"></a><span data-ttu-id="ecb86-159">Task: Add Region to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="ecb86-159">Task: Add Region to a DocumentDB account</span></span>

<span data-ttu-id="ecb86-160">DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ecb86-160">DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="ecb86-161">The instructions in this section describe how to add a read region to an existing DocumentDB account with Azure CLI 1.0 and Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="ecb86-161">The instructions in this section describe how to add a read region to an existing DocumentDB account with Azure CLI 1.0 and Resource Manager templates.</span></span> <span data-ttu-id="ecb86-162">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="ecb86-162">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span></span>

### <a id="add-region-documentdb-account-cli"></a> <span data-ttu-id="ecb86-163">Add Region to a DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ecb86-163">Add Region to a DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span></span>

<span data-ttu-id="ecb86-164">Add a region to an existing DocumentDB account in the new or existing resource group by entering the command below at the command prompt.</span><span class="sxs-lookup"><span data-stu-id="ecb86-164">Add a region to an existing DocumentDB account in the new or existing resource group by entering the command below at the command prompt.</span></span> <span data-ttu-id="ecb86-165">Note that the "locations" array should reflect the current region configuration within the DocumentDB account with the exception of the new region to be added.</span><span class="sxs-lookup"><span data-stu-id="ecb86-165">Note that the "locations" array should reflect the current region configuration within the DocumentDB account with the exception of the new region to be added.</span></span> <span data-ttu-id="ecb86-166">The example below shows a command to add a second region to the account.</span><span class="sxs-lookup"><span data-stu-id="ecb86-166">The example below shows a command to add a second region to the account.</span></span>

<span data-ttu-id="ecb86-167">Match the failover priority values to the existing configuration.</span><span class="sxs-lookup"><span data-stu-id="ecb86-167">Match the failover priority values to the existing configuration.</span></span> <span data-ttu-id="ecb86-168">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="ecb86-168">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span></span> <span data-ttu-id="ecb86-169">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span><span class="sxs-lookup"><span data-stu-id="ecb86-169">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span></span> <span data-ttu-id="ecb86-170">The new region will be a "Read" region and must have a failover priority value greater than 0.</span><span class="sxs-lookup"><span data-stu-id="ecb86-170">The new region will be a "Read" region and must have a failover priority value greater than 0.</span></span>

> [!TIP]
> <span data-ttu-id="ecb86-171">If you run this command in Azure PowerShell or Windows PowerShell you will receive an error about an unexpected token.</span><span class="sxs-lookup"><span data-stu-id="ecb86-171">If you run this command in Azure PowerShell or Windows PowerShell you will receive an error about an unexpected token.</span></span> <span data-ttu-id="ecb86-172">Instead, run this command at the Windows Command Prompt.</span><span class="sxs-lookup"><span data-stu-id="ecb86-172">Instead, run this command at the Windows Command Prompt.</span></span>

    azure resource create -g <resourcegroupname> -n <databaseaccountname> -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l <resourcegrouplocation> -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"<ip-range-filter>\",\"locations\":["{\"locationName\":\"<databaseaccountlocation>\",\"failoverPriority\":\"<failoverPriority1>\"},{\"locationName\":\"<newdatabaseaccountlocation>\",\"failoverPriority\":\"<failoverPriority2>\"}"]}"

 - <span data-ttu-id="ecb86-173">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span><span class="sxs-lookup"><span data-stu-id="ecb86-173">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span></span>
 - <span data-ttu-id="ecb86-174">`<resourcegrouplocation>` is the region of the current resource group.</span><span class="sxs-lookup"><span data-stu-id="ecb86-174">`<resourcegrouplocation>` is the region of the current resource group.</span></span>
 - <span data-ttu-id="ecb86-175">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="ecb86-175">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="ecb86-176">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="ecb86-176">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="ecb86-177">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="ecb86-177">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span></span>
 - <span data-ttu-id="ecb86-178">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="ecb86-178">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>
 - <span data-ttu-id="ecb86-179">`<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="ecb86-179">`<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="ecb86-180">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ecb86-180">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>
 - <span data-ttu-id="ecb86-181">`<newdatabaseaccountlocation>` is the new region to be added and must be one of the regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="ecb86-181">`<newdatabaseaccountlocation>` is the new region to be added and must be one of the regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="ecb86-182">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ecb86-182">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>


<span data-ttu-id="ecb86-183">Example input for adding the "East US" region as a read region in the DocumentDB account:</span><span class="sxs-lookup"><span data-stu-id="ecb86-183">Example input for adding the "East US" region as a read region in the DocumentDB account:</span></span> 

    azure resource create -g new_res_group -n samplecliacct -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l westus -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"\",\"locations\":["{\"locationName\":\"westus\",\"failoverPriority\":\"0\"},{\"locationName\":\"eastus\",\"failoverPriority\":\"1\"}"]}"

<span data-ttu-id="ecb86-184">Which produces the following output as your new account is provisioned:</span><span class="sxs-lookup"><span data-stu-id="ecb86-184">Which produces the following output as your new account is provisioned:</span></span>

    info:    Executing command resource create
    + Getting resource samplecliacct
    + Creating resource samplecliacct
    info:    Resource samplecliacct is updated
    data:
    data:    Id:        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/new_res_group/providers/Microsoft.DocumentDB/databaseAccounts/samplecliacct
    data:    Name:      samplecliacct
    data:    Type:      Microsoft.DocumentDB/databaseAccounts
    data:    Parent:
    data:    Location:  West US
    data:    Tags:
    data:
    info:    resource create command OK

<span data-ttu-id="ecb86-185">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ecb86-185">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span> 

<span data-ttu-id="ecb86-186">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="ecb86-186">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="ecb86-187">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="ecb86-187">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

### <a id="add-region-documentdb-account-cli-arm"></a> <span data-ttu-id="ecb86-188">Add Region to a DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ecb86-188">Add Region to a DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span></span>

<span data-ttu-id="ecb86-189">The instructions in this section describe how to add a region to an existing DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span><span class="sxs-lookup"><span data-stu-id="ecb86-189">The instructions in this section describe how to add a region to an existing DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span></span> <span data-ttu-id="ecb86-190">Using a template enables you to describe exactly what you want and repeat it without errors.</span><span class="sxs-lookup"><span data-stu-id="ecb86-190">Using a template enables you to describe exactly what you want and repeat it without errors.</span></span>

<span data-ttu-id="ecb86-191">Match the failover priority values to the existing configuration.</span><span class="sxs-lookup"><span data-stu-id="ecb86-191">Match the failover priority values to the existing configuration.</span></span> <span data-ttu-id="ecb86-192">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="ecb86-192">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span></span> <span data-ttu-id="ecb86-193">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span><span class="sxs-lookup"><span data-stu-id="ecb86-193">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span></span> <span data-ttu-id="ecb86-194">The new region will be a "Read" region and must have a failover priority value greater than 0.</span><span class="sxs-lookup"><span data-stu-id="ecb86-194">The new region will be a "Read" region and must have a failover priority value greater than 0.</span></span>

<span data-ttu-id="ecb86-195">Create a local template file similar to the one below that matches your current DocumentDB region configuration.</span><span class="sxs-lookup"><span data-stu-id="ecb86-195">Create a local template file similar to the one below that matches your current DocumentDB region configuration.</span></span> <span data-ttu-id="ecb86-196">The "locations" array should contain all of the existing regions in the database account alongside the new region to be added.</span><span class="sxs-lookup"><span data-stu-id="ecb86-196">The "locations" array should contain all of the existing regions in the database account alongside the new region to be added.</span></span> <span data-ttu-id="ecb86-197">Name the file azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="ecb86-197">Name the file azuredeploy.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "type": "string"
            },
            "locationName1": {
                "type": "string"
            },
            "locationName2": {
                "type": "string"
            },
            "newLocationName": {
                "type": "string"
            }
        },
        "variables": {},
        "resources": [
            {
                "apiVersion": "2015-04-08",
                "type": "Microsoft.DocumentDb/databaseAccounts",
                "name": "[parameters('databaseAccountName')]",
                "location": "[resourceGroup().location]",
                "properties": {
                    "databaseAccountOfferType": "Standard",
                    "ipRangeFilter": "",
                    "locations": [
                        {
                            "failoverPriority": 0,
                            "locationName": "[parameters('locationName1')]"
                        },
                        {
                            "failoverPriority": 1,
                            "locationName": "[parameters('locationName2')]"
                        },
                        {
                            "failoverPriority": 2,
                            "locationName": "[parameters('newLocationName')]"
                        }
                    ]
                }
            }
        ]
    }

<span data-ttu-id="ecb86-198">The above template file demonstrates an example where a new region is being added to a DocumentDB account which already has 2 regions.</span><span class="sxs-lookup"><span data-stu-id="ecb86-198">The above template file demonstrates an example where a new region is being added to a DocumentDB account which already has 2 regions.</span></span>

<span data-ttu-id="ecb86-199">You can either enter the parameter values at the command line, or create a parameter file to specify the value.</span><span class="sxs-lookup"><span data-stu-id="ecb86-199">You can either enter the parameter values at the command line, or create a parameter file to specify the value.</span></span>

<span data-ttu-id="ecb86-200">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="ecb86-200">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span></span> <span data-ttu-id="ecb86-201">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span><span class="sxs-lookup"><span data-stu-id="ecb86-201">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "value": "samplearmacct"
            },
            "locationName1": {
                "value": "westus"
            },
            "locationName2": {
                "value": "eastus"
            },
            "newLocationName": {
                "value": "northeurope"
            }
        }
    }

<span data-ttu-id="ecb86-202">In the azuredeploy.parameters.json file, update the value field of  `"databaseAccountName"` to the database name you'd like to use, then save the file.</span><span class="sxs-lookup"><span data-stu-id="ecb86-202">In the azuredeploy.parameters.json file, update the value field of  `"databaseAccountName"` to the database name you'd like to use, then save the file.</span></span> <span data-ttu-id="ecb86-203">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="ecb86-203">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span> <span data-ttu-id="ecb86-204">Update the value fields of `"locationName1"` and `"locationName2"` to the regions where your DocumentDB account exists.</span><span class="sxs-lookup"><span data-stu-id="ecb86-204">Update the value fields of `"locationName1"` and `"locationName2"` to the regions where your DocumentDB account exists.</span></span> <span data-ttu-id="ecb86-205">Update the value field of `"newLocationName"` to the region that you would like to add.</span><span class="sxs-lookup"><span data-stu-id="ecb86-205">Update the value field of `"newLocationName"` to the region that you would like to add.</span></span>

<span data-ttu-id="ecb86-206">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span><span class="sxs-lookup"><span data-stu-id="ecb86-206">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span></span> 

<span data-ttu-id="ecb86-207">To use a parameter file:</span><span class="sxs-lookup"><span data-stu-id="ecb86-207">To use a parameter file:</span></span>

    azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g <resourcegroupname> -n <deploymentname>

 - <span data-ttu-id="ecb86-208">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="ecb86-208">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span></span> <span data-ttu-id="ecb86-209">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="ecb86-209">If your path name has spaces in it, put double quotes around this parameter.</span></span>
 - <span data-ttu-id="ecb86-210">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="ecb86-210">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span></span> <span data-ttu-id="ecb86-211">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="ecb86-211">If your path name has spaces in it, put double quotes around this parameter.</span></span>
 - <span data-ttu-id="ecb86-212">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="ecb86-212">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span></span> 
 - <span data-ttu-id="ecb86-213">`<deploymentname>` is the optional name of the deployment.</span><span class="sxs-lookup"><span data-stu-id="ecb86-213">`<deploymentname>` is the optional name of the deployment.</span></span>

<span data-ttu-id="ecb86-214">Example input:</span><span class="sxs-lookup"><span data-stu-id="ecb86-214">Example input:</span></span> 

    azure group deployment create -f azuredeploy.json -e azuredeploy.parameters.json -g new_res_group -n azuredeploy

<span data-ttu-id="ecb86-215">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ecb86-215">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span></span>

    azure group deployment create -f <PathToTemplate> -g <resourcegroupname> -n <deploymentname>

<span data-ttu-id="ecb86-216">Example input which shows the prompt and entry for a database account named samplearmacct:</span><span class="sxs-lookup"><span data-stu-id="ecb86-216">Example input which shows the prompt and entry for a database account named samplearmacct:</span></span>

    azure group deployment create -f azuredeploy.json -g new_res_group -n azuredeploy
    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    databaseAccountName: samplearmacct

<span data-ttu-id="ecb86-217">As the account is provisioned, you will receive the following information:</span><span class="sxs-lookup"><span data-stu-id="ecb86-217">As the account is provisioned, you will receive the following information:</span></span> 

    info:    Executing command group deployment create
    + Initializing template configurations and parameters
    + Creating a deployment
    info:    Created template deployment "azuredeploy"
    + Waiting for deployment to complete
    + 
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Running
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Succeeded
    data:    DeploymentName     : azuredeploy
    data:    ResourceGroupName  : new_res_group
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          : 2015-11-30T18:50:23.6300288Z
    data:    Mode               : Incremental
    data:    CorrelationId      : 4a5d4049-c494-4053-bad4-cc804d454700
    data:    DeploymentParameters :
    data:    Name                 Type    Value
    data:    -------------------  ------  ------------------
    data:    locationName1        String  westus
    data:    locationName2        String  eastus
    data:    newLocationName      String  eastus
    data:    databaseAccountName  String  samplearmacct
    info:    group deployment create command OK

<span data-ttu-id="ecb86-218">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ecb86-218">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>  

<span data-ttu-id="ecb86-219">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="ecb86-219">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="ecb86-220">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="ecb86-220">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

## <a id="remove-region-documentdb-account"></a><span data-ttu-id="ecb86-221">Task: Remove Region from a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="ecb86-221">Task: Remove Region from a DocumentDB account</span></span>

<span data-ttu-id="ecb86-222">DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ecb86-222">DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="ecb86-223">The instructions in this section describe how to remove a region from an existing DocumentDB account with Azure CLI 1.0 and Resource Manager Templates.</span><span class="sxs-lookup"><span data-stu-id="ecb86-223">The instructions in this section describe how to remove a region from an existing DocumentDB account with Azure CLI 1.0 and Resource Manager Templates.</span></span> <span data-ttu-id="ecb86-224">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="ecb86-224">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span></span>

### <a id="remove-region-documentdb-account-cli"></a> <span data-ttu-id="ecb86-225">Remove Region to a DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ecb86-225">Remove Region to a DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span></span>

<span data-ttu-id="ecb86-226">To remove a region from an existing DocumentDB account, the command below can be executed with Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="ecb86-226">To remove a region from an existing DocumentDB account, the command below can be executed with Azure CLI 1.0.</span></span> <span data-ttu-id="ecb86-227">The "locations" array should contain only the regions that are to remain after the removal of the region.</span><span class="sxs-lookup"><span data-stu-id="ecb86-227">The "locations" array should contain only the regions that are to remain after the removal of the region.</span></span> <span data-ttu-id="ecb86-228">**The omitted location will be removed from the DocumentDB account**.</span><span class="sxs-lookup"><span data-stu-id="ecb86-228">**The omitted location will be removed from the DocumentDB account**.</span></span> <span data-ttu-id="ecb86-229">Enter the following command in the command prompt.</span><span class="sxs-lookup"><span data-stu-id="ecb86-229">Enter the following command in the command prompt.</span></span>

<span data-ttu-id="ecb86-230">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="ecb86-230">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span></span> <span data-ttu-id="ecb86-231">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span><span class="sxs-lookup"><span data-stu-id="ecb86-231">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span></span> 

> [!TIP]
> <span data-ttu-id="ecb86-232">If you run this command in Azure PowerShell or Windows PowerShell you will receive an error about an unexpected token.</span><span class="sxs-lookup"><span data-stu-id="ecb86-232">If you run this command in Azure PowerShell or Windows PowerShell you will receive an error about an unexpected token.</span></span> <span data-ttu-id="ecb86-233">Instead, run this command at the Windows Command Prompt.</span><span class="sxs-lookup"><span data-stu-id="ecb86-233">Instead, run this command at the Windows Command Prompt.</span></span>

    azure resource create -g <resourcegroupname> -n <databaseaccountname> -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l <resourcegrouplocation> -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"<ip-range-filter>\",\"locations\":["{\"locationName\":\"<databaseaccountlocation>\",\"failoverPriority\":\"<failoverPriority>\"}"]}"

 - <span data-ttu-id="ecb86-234">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span><span class="sxs-lookup"><span data-stu-id="ecb86-234">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span></span>
 - <span data-ttu-id="ecb86-235">`<resourcegrouplocation>` is the region of the current resource group.</span><span class="sxs-lookup"><span data-stu-id="ecb86-235">`<resourcegrouplocation>` is the region of the current resource group.</span></span>
 - <span data-ttu-id="ecb86-236">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="ecb86-236">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="ecb86-237">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="ecb86-237">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="ecb86-238">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="ecb86-238">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span></span>
 - <span data-ttu-id="ecb86-239">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="ecb86-239">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>
 - <span data-ttu-id="ecb86-240">`<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="ecb86-240">`<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="ecb86-241">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ecb86-241">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

<span data-ttu-id="ecb86-242">Example input:</span><span class="sxs-lookup"><span data-stu-id="ecb86-242">Example input:</span></span> 

    azure resource create -g new_res_group -n samplecliacct -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l westus -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"\",\"locations\":["{\"locationName\":\"westus\",\"failoverPriority\":\"0\"}"]}"

<span data-ttu-id="ecb86-243">Which produces the following output as your new account is provisioned:</span><span class="sxs-lookup"><span data-stu-id="ecb86-243">Which produces the following output as your new account is provisioned:</span></span>

    info:    Executing command resource create
    + Getting resource samplecliacct
    + Creating resource samplecliacct
    info:    Resource samplecliacct is updated
    data:
    data:    Id:        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/new_res_group/providers/Microsoft.DocumentDB/databaseAccounts/samplecliacct
    data:    Name:      samplecliacct
    data:    Type:      Microsoft.DocumentDB/databaseAccounts
    data:    Parent:
    data:    Location:  West US
    data:    Tags:
    data:
    info:    resource create command OK

<span data-ttu-id="ecb86-244">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ecb86-244">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span> 

<span data-ttu-id="ecb86-245">After the command returns, the account will be in the **Updating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="ecb86-245">After the command returns, the account will be in the **Updating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="ecb86-246">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="ecb86-246">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

### <a id="remove-region-documentdb-account-cli-arm"></a> <span data-ttu-id="ecb86-247">Remove Region from a DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ecb86-247">Remove Region from a DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span></span>

<span data-ttu-id="ecb86-248">The instructions in this section describe how to remove a region from an existing DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span><span class="sxs-lookup"><span data-stu-id="ecb86-248">The instructions in this section describe how to remove a region from an existing DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span></span> <span data-ttu-id="ecb86-249">Using a template enables you to describe exactly what you want and repeat it without errors.</span><span class="sxs-lookup"><span data-stu-id="ecb86-249">Using a template enables you to describe exactly what you want and repeat it without errors.</span></span>

<span data-ttu-id="ecb86-250">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="ecb86-250">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span></span> <span data-ttu-id="ecb86-251">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span><span class="sxs-lookup"><span data-stu-id="ecb86-251">The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions.</span></span> 

<span data-ttu-id="ecb86-252">Create a local template file similar to the one below that matches your current DocumentDB region configuration.</span><span class="sxs-lookup"><span data-stu-id="ecb86-252">Create a local template file similar to the one below that matches your current DocumentDB region configuration.</span></span> <span data-ttu-id="ecb86-253">The "locations" array should contain only the regions that are to remain after the removal of the region.</span><span class="sxs-lookup"><span data-stu-id="ecb86-253">The "locations" array should contain only the regions that are to remain after the removal of the region.</span></span> <span data-ttu-id="ecb86-254">**The omitted location will be removed from the DocumentDB account**.</span><span class="sxs-lookup"><span data-stu-id="ecb86-254">**The omitted location will be removed from the DocumentDB account**.</span></span> <span data-ttu-id="ecb86-255">Name the file azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="ecb86-255">Name the file azuredeploy.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "type": "string"
            },
            "locationName1": {
                "type": "string"
            }
        },
        "variables": {},
        "resources": [
            {
                "apiVersion": "2015-04-08",
                "type": "Microsoft.DocumentDb/databaseAccounts",
                "name": "[parameters('databaseAccountName')]",
                "location": "[resourceGroup().location]",
                "properties": {
                    "databaseAccountOfferType": "Standard",
                    "ipRangeFilter": "",
                    "locations": [
                        {
                            "failoverPriority": 0,
                            "locationName": "[parameters('locationName1')]"
                        }
                    ]
                }
            }
        ]
    }

<span data-ttu-id="ecb86-256">You can either enter the parameter values at the command line, or create a parameter file to specify the value.</span><span class="sxs-lookup"><span data-stu-id="ecb86-256">You can either enter the parameter values at the command line, or create a parameter file to specify the value.</span></span>

<span data-ttu-id="ecb86-257">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="ecb86-257">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span></span> <span data-ttu-id="ecb86-258">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span><span class="sxs-lookup"><span data-stu-id="ecb86-258">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span></span> <span data-ttu-id="ecb86-259">Be sure to add the necessary parameters that are defined in your Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="ecb86-259">Be sure to add the necessary parameters that are defined in your Azure Resource Manager template.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "value": "samplearmacct"
            },
            "locationName1": {
                "value": "westus"
            }
        }
    }

<span data-ttu-id="ecb86-260">In the azuredeploy.parameters.json file, update the value field of  `"databaseAccountName"` to the database name you'd like to use, then save the file.</span><span class="sxs-lookup"><span data-stu-id="ecb86-260">In the azuredeploy.parameters.json file, update the value field of  `"databaseAccountName"` to the database name you'd like to use, then save the file.</span></span> <span data-ttu-id="ecb86-261">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="ecb86-261">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span> <span data-ttu-id="ecb86-262">Update the value field of `"locationName1"` to the regions where you want the DocumentDB account to exist after the removal of the region.</span><span class="sxs-lookup"><span data-stu-id="ecb86-262">Update the value field of `"locationName1"` to the regions where you want the DocumentDB account to exist after the removal of the region.</span></span>

<span data-ttu-id="ecb86-263">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span><span class="sxs-lookup"><span data-stu-id="ecb86-263">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span></span> 

<span data-ttu-id="ecb86-264">To use a parameter file:</span><span class="sxs-lookup"><span data-stu-id="ecb86-264">To use a parameter file:</span></span>

    azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g <resourcegroupname> -n <deploymentname>

 - <span data-ttu-id="ecb86-265">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="ecb86-265">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span></span> <span data-ttu-id="ecb86-266">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="ecb86-266">If your path name has spaces in it, put double quotes around this parameter.</span></span>
 - <span data-ttu-id="ecb86-267">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="ecb86-267">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span></span> <span data-ttu-id="ecb86-268">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="ecb86-268">If your path name has spaces in it, put double quotes around this parameter.</span></span>
 - <span data-ttu-id="ecb86-269">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="ecb86-269">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span></span> 
 - <span data-ttu-id="ecb86-270">`<deploymentname>` is the optional name of the deployment.</span><span class="sxs-lookup"><span data-stu-id="ecb86-270">`<deploymentname>` is the optional name of the deployment.</span></span>

<span data-ttu-id="ecb86-271">Example input:</span><span class="sxs-lookup"><span data-stu-id="ecb86-271">Example input:</span></span> 

    azure group deployment create -f azuredeploy.json -e azuredeploy.parameters.json -g new_res_group -n azuredeploy

<span data-ttu-id="ecb86-272">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ecb86-272">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span></span>

    azure group deployment create -f <PathToTemplate> -g <resourcegroupname> -n <deploymentname>

<span data-ttu-id="ecb86-273">Example input which shows the prompt and entry for a database account named samplearmacct:</span><span class="sxs-lookup"><span data-stu-id="ecb86-273">Example input which shows the prompt and entry for a database account named samplearmacct:</span></span>

    azure group deployment create -f azuredeploy.json -g new_res_group -n azuredeploy
    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    databaseAccountName: samplearmacct

<span data-ttu-id="ecb86-274">As the account is provisioned, you will receive the following information:</span><span class="sxs-lookup"><span data-stu-id="ecb86-274">As the account is provisioned, you will receive the following information:</span></span> 

    info:    Executing command group deployment create
    + Initializing template configurations and parameters
    + Creating a deployment
    info:    Created template deployment "azuredeploy"
    + Waiting for deployment to complete
    + 
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Running
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Succeeded
    data:    DeploymentName     : azuredeploy
    data:    ResourceGroupName  : new_res_group
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          : 2015-11-30T18:50:23.6300288Z
    data:    Mode               : Incremental
    data:    CorrelationId      : 4a5d4049-c494-4053-bad4-cc804d454700
    data:    DeploymentParameters :
    data:    Name                 Type    Value
    data:    -------------------  ------  ------------------
    data:    databaseAccountName  String  samplearmacct
    data:    locationName1        String  westus
    info:    group deployment create command OK

<span data-ttu-id="ecb86-275">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ecb86-275">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>  

<span data-ttu-id="ecb86-276">After the command returns, the account will be in the **Updating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="ecb86-276">After the command returns, the account will be in the **Updating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="ecb86-277">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="ecb86-277">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ecb86-278">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ecb86-278">Troubleshooting</span></span>

<span data-ttu-id="ecb86-279">If you receive errors like `Deployment provisioning state was not successful` while creating your resource group or database account, you have a few troubleshooting options.</span><span class="sxs-lookup"><span data-stu-id="ecb86-279">If you receive errors like `Deployment provisioning state was not successful` while creating your resource group or database account, you have a few troubleshooting options.</span></span> 

> [!NOTE]
> <span data-ttu-id="ecb86-280">Providing incorrect characters in the database account name or providing a location in which DocumentDB is not available will cause deployment errors.</span><span class="sxs-lookup"><span data-stu-id="ecb86-280">Providing incorrect characters in the database account name or providing a location in which DocumentDB is not available will cause deployment errors.</span></span> <span data-ttu-id="ecb86-281">Database account names can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="ecb86-281">Database account names can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span> <span data-ttu-id="ecb86-282">All valid database account locations are listed on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ecb86-282">All valid database account locations are listed on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

- <span data-ttu-id="ecb86-283">If your output contains the following `Error information has been recorded to C:\Users\wendy\.azure\azure.err`, then review the error info in the azure.err file.</span><span class="sxs-lookup"><span data-stu-id="ecb86-283">If your output contains the following `Error information has been recorded to C:\Users\wendy\.azure\azure.err`, then review the error info in the azure.err file.</span></span>

- <span data-ttu-id="ecb86-284">You may find useful info in the log file for the resource group.</span><span class="sxs-lookup"><span data-stu-id="ecb86-284">You may find useful info in the log file for the resource group.</span></span> <span data-ttu-id="ecb86-285">To view the log file, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ecb86-285">To view the log file, run the following command:</span></span>

        azure group log show <resourcegroupname> --last-deployment

    <span data-ttu-id="ecb86-286">Example input:       azure group log show new_res_group --last-deployment</span><span class="sxs-lookup"><span data-stu-id="ecb86-286">Example input:       azure group log show new_res_group --last-deployment</span></span>

    <span data-ttu-id="ecb86-287">Then see [Troubleshooting resource group deployments in Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md) for additional information.</span><span class="sxs-lookup"><span data-stu-id="ecb86-287">Then see [Troubleshooting resource group deployments in Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md) for additional information.</span></span>

- <span data-ttu-id="ecb86-288">Error information is also available in the Azure Portal as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="ecb86-288">Error information is also available in the Azure Portal as shown in the following screenshot.</span></span> <span data-ttu-id="ecb86-289">To navigate to the error info: click Resource Groups in the Jumpbar, select the Resource Group that had the error, then in the Essentials area of the Resource group blade click the date of the Last Deployment, then in the Deployment history blade select the failed deployment, then in the Deployment blade click the Operation detail with the red exclamation mark.</span><span class="sxs-lookup"><span data-stu-id="ecb86-289">To navigate to the error info: click Resource Groups in the Jumpbar, select the Resource Group that had the error, then in the Essentials area of the Resource group blade click the date of the Last Deployment, then in the Deployment history blade select the failed deployment, then in the Deployment blade click the Operation detail with the red exclamation mark.</span></span> <span data-ttu-id="ecb86-290">The Status Message for the failed deployment is displayed in the Operation details blade.</span><span class="sxs-lookup"><span data-stu-id="ecb86-290">The Status Message for the failed deployment is displayed in the Operation details blade.</span></span> 

    ![Screenshot of the Azure portal showing how to navigate to the deployment error message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/portal-troubleshooting-deploy.png) 

## <a name="next-steps"></a><span data-ttu-id="ecb86-292">Next steps</span><span class="sxs-lookup"><span data-stu-id="ecb86-292">Next steps</span></span>

<span data-ttu-id="ecb86-293">Now that you have a DocumentDB account, the next step is to create a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="ecb86-293">Now that you have a DocumentDB account, the next step is to create a DocumentDB database.</span></span> <span data-ttu-id="ecb86-294">You can create a database by using one of the following:</span><span class="sxs-lookup"><span data-stu-id="ecb86-294">You can create a database by using one of the following:</span></span>

- <span data-ttu-id="ecb86-295">The Azure portal, as described in [Create a DocumentDB collection and database using the Azure portal](documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="ecb86-295">The Azure portal, as described in [Create a DocumentDB collection and database using the Azure portal](documentdb-create-collection.md).</span></span>
- <span data-ttu-id="ecb86-296">The C# .NET samples in the [DatabaseManagement](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples/DatabaseManagement) project of the [azure-documentdb-dotnet](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples) repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="ecb86-296">The C# .NET samples in the [DatabaseManagement](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples/DatabaseManagement) project of the [azure-documentdb-dotnet](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples) repository on GitHub.</span></span>
- <span data-ttu-id="ecb86-297">The [DocumentDB SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecb86-297">The [DocumentDB SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span></span> <span data-ttu-id="ecb86-298">DocumentDB has .NET, Java, Python, Node.js, and JavaScript API SDKs.</span><span class="sxs-lookup"><span data-stu-id="ecb86-298">DocumentDB has .NET, Java, Python, Node.js, and JavaScript API SDKs.</span></span> 

<span data-ttu-id="ecb86-299">After creating your database, you need to [add one or more collections](documentdb-create-collection.md) to the database, then [add documents](documentdb-view-json-document-explorer.md) to the collections.</span><span class="sxs-lookup"><span data-stu-id="ecb86-299">After creating your database, you need to [add one or more collections](documentdb-create-collection.md) to the database, then [add documents](documentdb-view-json-document-explorer.md) to the collections.</span></span> 

<span data-ttu-id="ecb86-300">After you have documents in a collection, you can use [DocumentDB SQL](documentdb-sql-query.md) to [execute queries](documentdb-sql-query.md#ExecutingSqlQueries) against your documents by using the [Query Explorer](documentdb-query-collections-query-explorer.md) in the portal, the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), or one of the [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecb86-300">After you have documents in a collection, you can use [DocumentDB SQL](documentdb-sql-query.md) to [execute queries](documentdb-sql-query.md#ExecutingSqlQueries) against your documents by using the [Query Explorer](documentdb-query-collections-query-explorer.md) in the portal, the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), or one of the [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span></span>

<span data-ttu-id="ecb86-301">To learn more about DocumentDB, explore these resources:</span><span class="sxs-lookup"><span data-stu-id="ecb86-301">To learn more about DocumentDB, explore these resources:</span></span>

-   [<span data-ttu-id="ecb86-302">Learning path for DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ecb86-302">Learning path for DocumentDB</span></span>](https://azure.microsoft.com/documentation/learning-paths/documentdb/)
-   [<span data-ttu-id="ecb86-303">DocumentDB resource model and concepts</span><span class="sxs-lookup"><span data-stu-id="ecb86-303">DocumentDB resource model and concepts</span></span>](documentdb-resources.md)

<span data-ttu-id="ecb86-304">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="ecb86-304">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[distribute-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally
[scaling-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally/#scaling-across-the-planet




