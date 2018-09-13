---
title: DocumentDB Automation - Resource Manager - Azure CLI 1.0 | Microsoft Docs
description: Use Azure Resource Manager templates or CLI to deploy a DocumentDB database account. DocumentDB is a cloud-based NoSQL database for JSON data.
services: documentdb
author: mimig1
manager: jhubbard
editor: ''
tags: azure-resource-manager
documentationcenter: ''
ms.assetid: eae5eec6-0e27-442c-abfc-ef6b7fd3f8d2
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: mimig
ms.openlocfilehash: 36b046001d688d0d845a0a1d636027c15eaedb6b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660942"
---
# <a name="automate-documentdb-account-creation-using-azure-cli-10-and-azure-resource-manager-templates"></a><span data-ttu-id="7b1c4-104">Automate DocumentDB account creation using Azure CLI 1.0 and Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="7b1c4-104">Automate DocumentDB account creation using Azure CLI 1.0 and Azure Resource Manager templates</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](documentdb-create-account.md)
> * [Azure CLI 1.0](documentdb-automation-resource-manager-cli-nodejs.md)
> * [Azure CLI 2.0](documentdb-automation-resource-manager-cli.md)
> * [Azure PowerShell](documentdb-manage-account-with-powershell.md)

<span data-ttu-id="7b1c4-109">This article shows you how to create an Azure DocumentDB account by using Azure Resource Manager templates or directly with Azure Command-Line Interface (CLI) 1.0.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-109">This article shows you how to create an Azure DocumentDB account by using Azure Resource Manager templates or directly with Azure Command-Line Interface (CLI) 1.0.</span></span> <span data-ttu-id="7b1c4-110">To create a DocumentDB account using the Azure portal, see [Create a DocumentDB database account using the Azure portal](documentdb-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-110">To create a DocumentDB account using the Azure portal, see [Create a DocumentDB database account using the Azure portal](documentdb-create-account.md).</span></span>

<span data-ttu-id="7b1c4-111">DocumentDB database accounts are currently the only DocumentDB resource that can be created using Resource Manager templates and Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-111">DocumentDB database accounts are currently the only DocumentDB resource that can be created using Resource Manager templates and Azure CLI 1.0.</span></span>

## <a name="getting-ready"></a><span data-ttu-id="7b1c4-112">Getting ready</span><span class="sxs-lookup"><span data-stu-id="7b1c4-112">Getting ready</span></span>
<span data-ttu-id="7b1c4-113">Before you can use Azure CLI 1.0 with Azure resource groups, you need to have the right  version and an Azure account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-113">Before you can use Azure CLI 1.0 with Azure resource groups, you need to have the right  version and an Azure account.</span></span> <span data-ttu-id="7b1c4-114">If you don't have Azure CLI 1.0, [install it](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-114">If you don't have Azure CLI 1.0, [install it](../cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-10-version"></a><span data-ttu-id="7b1c4-115">Update your Azure CLI 1.0 version</span><span class="sxs-lookup"><span data-stu-id="7b1c4-115">Update your Azure CLI 1.0 version</span></span>
<span data-ttu-id="7b1c4-116">At the command prompt, type `azure --version` to see whether you have already installed version 0.10.4 or later.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-116">At the command prompt, type `azure --version` to see whether you have already installed version 0.10.4 or later.</span></span> <span data-ttu-id="7b1c4-117">You may be prompted to participate in Microsoft Azure CLI data collection at this step, and can select y or n to opt-in or opt-out.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-117">You may be prompted to participate in Microsoft Azure CLI data collection at this step, and can select y or n to opt-in or opt-out.</span></span>

    azure --version
    0.10.4 (node: 4.2.4)

<span data-ttu-id="7b1c4-118">If your version is not 0.10.4 or later, you need to either [install Azure CLI 1.0](../cli-install-nodejs.md) or update by using one of the native installers, or through **npm** by typing `npm update -g azure-cli` to update or `npm install -g azure-cli` to install.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-118">If your version is not 0.10.4 or later, you need to either [install Azure CLI 1.0](../cli-install-nodejs.md) or update by using one of the native installers, or through **npm** by typing `npm update -g azure-cli` to update or `npm install -g azure-cli` to install.</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="7b1c4-119">Set your Azure account and subscription</span><span class="sxs-lookup"><span data-stu-id="7b1c4-119">Set your Azure account and subscription</span></span>
<span data-ttu-id="7b1c4-120">If you don't already have an Azure subscription but you do have a Visual Studio subscription, you can activate your [Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-120">If you don't already have an Azure subscription but you do have a Visual Studio subscription, you can activate your [Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="7b1c4-121">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-121">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="7b1c4-122">You need to have a work or school account or a Microsoft account identity to use Azure resource management templates.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-122">You need to have a work or school account or a Microsoft account identity to use Azure resource management templates.</span></span> <span data-ttu-id="7b1c4-123">If you have one of these accounts, type the following command:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-123">If you have one of these accounts, type the following command:</span></span>

    azure login

<span data-ttu-id="7b1c4-124">Which produces the following output:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-124">Which produces the following output:</span></span>

    info:    Executing command login
    |info:    To sign in, use a web browser to open the page https://aka.ms/devicelogin.
    Enter the code E1A2B3C4D to authenticate.

> [!NOTE]
> If you don't have an Azure account, you see an error message indicating that you need a different type of account. To create one from your current Azure account, see [Creating a work or school identity in Azure Active Directory](../virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

<span data-ttu-id="7b1c4-127">Open [https://aka.ms/devicelogin](https://aka.ms/devicelogin) in a browser and enter the code provided in the command output.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-127">Open [https://aka.ms/devicelogin](https://aka.ms/devicelogin) in a browser and enter the code provided in the command output.</span></span>

![Screenshot showing the device login screen for Microsoft Azure CLI 1.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/azure-cli-login-code.png)

<span data-ttu-id="7b1c4-129">Once you've entered the code, select the identity you want to use in the browser and provide your user name and password if needed.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-129">Once you've entered the code, select the identity you want to use in the browser and provide your user name and password if needed.</span></span>

![Screenshot showing where to select the Microsoft identity account associated with the Azure subscription you want to use](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/identity-cli-login.png)

<span data-ttu-id="7b1c4-131">You receive the following confirmation screen when you're successfully logged in, and you can then close the browser window.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-131">You receive the following confirmation screen when you're successfully logged in, and you can then close the browser window.</span></span>

![Screenshot showing confirmation of login to the Microsoft Azure Cross-platform Command Line Interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/login-confirmation.png)

<span data-ttu-id="7b1c4-133">The command shell also provides the following output:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-133">The command shell also provides the following output:</span></span>

    /info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

<span data-ttu-id="7b1c4-134">In addition to the interactive login method described here, there are additional Azure CLI 1.0 login methods available.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-134">In addition to the interactive login method described here, there are additional Azure CLI 1.0 login methods available.</span></span> <span data-ttu-id="7b1c4-135">For more information about the other methods and information about handling multiple subscriptions, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI 1.0)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-135">For more information about the other methods and information about handling multiple subscriptions, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI 1.0)](../xplat-cli-connect.md).</span></span>

### <a name="switch-to-azure-cli-10-resource-group-mode"></a><span data-ttu-id="7b1c4-136">Switch to Azure CLI 1.0 resource group mode</span><span class="sxs-lookup"><span data-stu-id="7b1c4-136">Switch to Azure CLI 1.0 resource group mode</span></span>
<span data-ttu-id="7b1c4-137">By default, Azure CLI 1.0 starts in the service management mode (**asm** mode).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-137">By default, Azure CLI 1.0 starts in the service management mode (**asm** mode).</span></span> <span data-ttu-id="7b1c4-138">Type the following to switch to resource group mode.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-138">Type the following to switch to resource group mode.</span></span>

    azure config mode arm

<span data-ttu-id="7b1c4-139">Which provides the following output:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-139">Which provides the following output:</span></span>

    info:    Executing command config mode
    info:    New mode is arm
    info:    config mode command OK

<span data-ttu-id="7b1c4-140">If needed, you can switch back to the default set of commands by typing `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-140">If needed, you can switch back to the default set of commands by typing `azure config mode asm`.</span></span>

### <a name="create-or-retrieve-your-resource-group"></a><span data-ttu-id="7b1c4-141">Create or retrieve your resource group</span><span class="sxs-lookup"><span data-stu-id="7b1c4-141">Create or retrieve your resource group</span></span>
<span data-ttu-id="7b1c4-142">To create a DocumentDB account, you first need a resource group.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-142">To create a DocumentDB account, you first need a resource group.</span></span> <span data-ttu-id="7b1c4-143">If you already know the name of the resource group that you'd like to use, then skip to [Step 2](#create-documentdb-account-cli).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-143">If you already know the name of the resource group that you'd like to use, then skip to [Step 2](#create-documentdb-account-cli).</span></span>

<span data-ttu-id="7b1c4-144">To review a list of all your current resource groups, run the following command and take note of the resource group name you'd like to use:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-144">To review a list of all your current resource groups, run the following command and take note of the resource group name you'd like to use:</span></span>

    azure group list

<span data-ttu-id="7b1c4-145">To create a resource group, run the following command, specify the name of the new resource group to create, and the region in which to create the resource group:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-145">To create a resource group, run the following command, specify the name of the new resource group to create, and the region in which to create the resource group:</span></span>

    azure group create <resourcegroupname> <resourcegrouplocation>

* <span data-ttu-id="7b1c4-146">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-146">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span></span>
* <span data-ttu-id="7b1c4-147">`<resourcegrouplocation>` must be one of the regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-147">`<resourcegrouplocation>` must be one of the regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="7b1c4-148">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-148">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

<span data-ttu-id="7b1c4-149">Example input:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-149">Example input:</span></span>

    azure group create new_res_group westus

<span data-ttu-id="7b1c4-150">Which produces the following output:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-150">Which produces the following output:</span></span>

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

<span data-ttu-id="7b1c4-151">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-151">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>

## <a name="understanding-resource-manager-templates-and-resource-groups"></a><span data-ttu-id="7b1c4-152">Understanding Resource Manager templates and resource groups</span><span class="sxs-lookup"><span data-stu-id="7b1c4-152">Understanding Resource Manager templates and resource groups</span></span>
<span data-ttu-id="7b1c4-153">Most applications are built from a combination of different resource types (such as one or more DocumentDB account, storage accounts, a virtual network, or a content delivery network).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-153">Most applications are built from a combination of different resource types (such as one or more DocumentDB account, storage accounts, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="7b1c4-154">The default Azure service management API and the Azure portal represented these items by using a service-by-service approach.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-154">The default Azure service management API and the Azure portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="7b1c4-155">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-155">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="7b1c4-156">*Azure Resource Manager templates* make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-156">*Azure Resource Manager templates* make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="7b1c4-157">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-157">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span></span>

<span data-ttu-id="7b1c4-158">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-158">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="7b1c4-159">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-159">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

## <a id="quick-create-documentdb-account"></a><span data-ttu-id="7b1c4-160">Task: Create a single region DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="7b1c4-160">Task: Create a single region DocumentDB account</span></span>
<span data-ttu-id="7b1c4-161">Use the instructions in this section to create a Single Region DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-161">Use the instructions in this section to create a Single Region DocumentDB account.</span></span> <span data-ttu-id="7b1c4-162">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-162">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span></span>

### <a id="create-single-documentdb-account-cli-arm"></a> <span data-ttu-id="7b1c4-163">Create a single region DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="7b1c4-163">Create a single region DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span></span>
<span data-ttu-id="7b1c4-164">Create a DocumentDB account in the new or existing resource group by entering the following command at the command prompt:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-164">Create a DocumentDB account in the new or existing resource group by entering the following command at the command prompt:</span></span>

> [!TIP]
> If you run this command in Azure PowerShell or Windows PowerShell you receive an error about an unexpected token. Instead, run this command at the Windows Command Prompt.
>
>

    azure resource create -g <resourcegroupname> -n <databaseaccountname> -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l <resourcegrouplocation> -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"<ip-range-filter>\",\"locations\":["{\"locationName\":\"<databaseaccountlocation>\",\"failoverPriority\":\"<failoverPriority>\"}"]}"

* <span data-ttu-id="7b1c4-167">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-167">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span></span>
* <span data-ttu-id="7b1c4-168">`<resourcegrouplocation>` is the region of the current resource group.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-168">`<resourcegrouplocation>` is the region of the current resource group.</span></span>
* <span data-ttu-id="7b1c4-169">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-169">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="7b1c4-170">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-170">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="7b1c4-171">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="7b1c4-171">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span></span>
* <span data-ttu-id="7b1c4-172">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-172">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>
* <span data-ttu-id="7b1c4-173">`<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-173">`<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="7b1c4-174">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-174">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

<span data-ttu-id="7b1c4-175">Example input:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-175">Example input:</span></span>

    azure resource create -g new_res_group -n samplecliacct -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l westus -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"\",\"locations\":["{\"locationName\":\"westus\",\"failoverPriority\":\"0\"}"]}"

<span data-ttu-id="7b1c4-176">Which produces the following output as your new account is provisioned:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-176">Which produces the following output as your new account is provisioned:</span></span>

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

<span data-ttu-id="7b1c4-177">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-177">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>

<span data-ttu-id="7b1c4-178">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-178">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="7b1c4-179">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-179">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

### <a id="create-single-documentdb-account-cli-arm"></a> <span data-ttu-id="7b1c4-180">Create a single region DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="7b1c4-180">Create a single region DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span></span>
<span data-ttu-id="7b1c4-181">The instructions in this section describe how to create a DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-181">The instructions in this section describe how to create a DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span></span> <span data-ttu-id="7b1c4-182">Using a template enables you to describe exactly what you want and repeat it without errors.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-182">Using a template enables you to describe exactly what you want and repeat it without errors.</span></span>

<span data-ttu-id="7b1c4-183">Create a local template file with the following content.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-183">Create a local template file with the following content.</span></span> <span data-ttu-id="7b1c4-184">Name the file azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-184">Name the file azuredeploy.json.</span></span>

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

<span data-ttu-id="7b1c4-185">The failoverPriority must be set to 0 since this is a single region account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-185">The failoverPriority must be set to 0 since this is a single region account.</span></span> <span data-ttu-id="7b1c4-186">A failoverPriority of 0 indicates that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="7b1c4-186">A failoverPriority of 0 indicates that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span></span>
<span data-ttu-id="7b1c4-187">You can either enter the value at the command line, or create a parameter file to specify the value.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-187">You can either enter the value at the command line, or create a parameter file to specify the value.</span></span>

<span data-ttu-id="7b1c4-188">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-188">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span></span> <span data-ttu-id="7b1c4-189">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-189">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span></span>

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

<span data-ttu-id="7b1c4-190">In the azuredeploy.parameters.json file, update the value field of `"samplearmacct"` to the database name you'd like to use, then save the file.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-190">In the azuredeploy.parameters.json file, update the value field of `"samplearmacct"` to the database name you'd like to use, then save the file.</span></span> <span data-ttu-id="7b1c4-191">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-191">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span> <span data-ttu-id="7b1c4-192">Update the value field of `"locationName1"` to the region where you would like to create the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-192">Update the value field of `"locationName1"` to the region where you would like to create the DocumentDB account.</span></span>

<span data-ttu-id="7b1c4-193">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-193">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span></span>

<span data-ttu-id="7b1c4-194">To use a parameter file:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-194">To use a parameter file:</span></span>

    azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g <resourcegroupname> -n <deploymentname>

* <span data-ttu-id="7b1c4-195">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-195">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span></span> <span data-ttu-id="7b1c4-196">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-196">If your path name has spaces in it, put double quotes around this parameter.</span></span>
* <span data-ttu-id="7b1c4-197">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-197">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span></span> <span data-ttu-id="7b1c4-198">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-198">If your path name has spaces in it, put double quotes around this parameter.</span></span>
* <span data-ttu-id="7b1c4-199">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-199">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span></span>
* <span data-ttu-id="7b1c4-200">`<deploymentname>` is the optional name of the deployment.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-200">`<deploymentname>` is the optional name of the deployment.</span></span>

<span data-ttu-id="7b1c4-201">Example input:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-201">Example input:</span></span>

    azure group deployment create -f azuredeploy.json -e azuredeploy.parameters.json -g new_res_group -n azuredeploy

<span data-ttu-id="7b1c4-202">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-202">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span></span>

    azure group deployment create -f <PathToTemplate> -g <resourcegroupname> -n <deploymentname>

<span data-ttu-id="7b1c4-203">Example input which shows the prompt and entry for a database account named samplearmacct:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-203">Example input which shows the prompt and entry for a database account named samplearmacct:</span></span>

    azure group deployment create -f azuredeploy.json -g new_res_group -n azuredeploy
    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    databaseAccountName: samplearmacct

<span data-ttu-id="7b1c4-204">As the account is provisioned, you receive the following information:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-204">As the account is provisioned, you receive the following information:</span></span>

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

<span data-ttu-id="7b1c4-205">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-205">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>  

<span data-ttu-id="7b1c4-206">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-206">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="7b1c4-207">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-207">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

## <a id="quick-create-documentdb-with-mongodb-api-account"></a><span data-ttu-id="7b1c4-208">Task: Create a single region DocumentDB: API for MongoDB account</span><span class="sxs-lookup"><span data-stu-id="7b1c4-208">Task: Create a single region DocumentDB: API for MongoDB account</span></span>
<span data-ttu-id="7b1c4-209">Use the instructions in this section to create a single region API for MongoDB account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-209">Use the instructions in this section to create a single region API for MongoDB account.</span></span> <span data-ttu-id="7b1c4-210">This can be accomplished using Azure CLI 1.0 with Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-210">This can be accomplished using Azure CLI 1.0 with Resource Manager templates.</span></span>

### <a id="create-single-documentdb-with-mongodb-api-account-cli-arm"></a> <span data-ttu-id="7b1c4-211">Create a single region MongoDB account using Azure CLI 1.0 with Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="7b1c4-211">Create a single region MongoDB account using Azure CLI 1.0 with Resource Manager templates</span></span>
<span data-ttu-id="7b1c4-212">The instructions in this section describe how to create an API for MongoDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-212">The instructions in this section describe how to create an API for MongoDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span></span> <span data-ttu-id="7b1c4-213">Using a template enables you to describe exactly what you want and repeat it without errors.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-213">Using a template enables you to describe exactly what you want and repeat it without errors.</span></span>

<span data-ttu-id="7b1c4-214">Create a local template file with the following content.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-214">Create a local template file with the following content.</span></span> <span data-ttu-id="7b1c4-215">Name the file azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-215">Name the file azuredeploy.json.</span></span>

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
                "kind": "MongoDB",
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

<span data-ttu-id="7b1c4-216">The kind must be set to MongoDB to specify that this account will support MongoDB APIs.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-216">The kind must be set to MongoDB to specify that this account will support MongoDB APIs.</span></span> <span data-ttu-id="7b1c4-217">If no kind property is specified, the default will be a native DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-217">If no kind property is specified, the default will be a native DocumentDB account.</span></span>

<span data-ttu-id="7b1c4-218">The failoverPriority must be set to 0 since this is a single region account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-218">The failoverPriority must be set to 0 since this is a single region account.</span></span> <span data-ttu-id="7b1c4-219">A failoverPriority of 0 indicates that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="7b1c4-219">A failoverPriority of 0 indicates that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span></span>
<span data-ttu-id="7b1c4-220">You can either enter the value at the command line, or create a parameter file to specify the value.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-220">You can either enter the value at the command line, or create a parameter file to specify the value.</span></span>

<span data-ttu-id="7b1c4-221">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-221">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span></span> <span data-ttu-id="7b1c4-222">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-222">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span></span>

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

<span data-ttu-id="7b1c4-223">In the azuredeploy.parameters.json file, update the value field of `"samplearmacct"` to the database name you'd like to use, then save the file.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-223">In the azuredeploy.parameters.json file, update the value field of `"samplearmacct"` to the database name you'd like to use, then save the file.</span></span> <span data-ttu-id="7b1c4-224">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-224">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span> <span data-ttu-id="7b1c4-225">Update the value field of `"locationName1"` to the region where you would like to create the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-225">Update the value field of `"locationName1"` to the region where you would like to create the DocumentDB account.</span></span>

<span data-ttu-id="7b1c4-226">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-226">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span></span>

<span data-ttu-id="7b1c4-227">To use a parameter file:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-227">To use a parameter file:</span></span>

    azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g <resourcegroupname> -n <deploymentname>

* <span data-ttu-id="7b1c4-228">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-228">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span></span> <span data-ttu-id="7b1c4-229">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-229">If your path name has spaces in it, put double quotes around this parameter.</span></span>
* <span data-ttu-id="7b1c4-230">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-230">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span></span> <span data-ttu-id="7b1c4-231">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-231">If your path name has spaces in it, put double quotes around this parameter.</span></span>
* <span data-ttu-id="7b1c4-232">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-232">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span></span>
* <span data-ttu-id="7b1c4-233">`<deploymentname>` is the optional name of the deployment.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-233">`<deploymentname>` is the optional name of the deployment.</span></span>

<span data-ttu-id="7b1c4-234">Example input:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-234">Example input:</span></span>

    azure group deployment create -f azuredeploy.json -e azuredeploy.parameters.json -g new_res_group -n azuredeploy

<span data-ttu-id="7b1c4-235">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-235">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span></span>

    azure group deployment create -f <PathToTemplate> -g <resourcegroupname> -n <deploymentname>

<span data-ttu-id="7b1c4-236">Example input which shows the prompt and entry for a database account named samplearmacct:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-236">Example input which shows the prompt and entry for a database account named samplearmacct:</span></span>

    azure group deployment create -f azuredeploy.json -g new_res_group -n azuredeploy
    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    databaseAccountName: samplearmacct

<span data-ttu-id="7b1c4-237">As the account is provisioned, you receive the following information:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-237">As the account is provisioned, you receive the following information:</span></span>

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

<span data-ttu-id="7b1c4-238">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-238">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>  

<span data-ttu-id="7b1c4-239">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-239">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="7b1c4-240">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-240">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

## <a id="create-multi-documentdb-account"></a><span data-ttu-id="7b1c4-241">Task: Create a multi-region DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="7b1c4-241">Task: Create a multi-region DocumentDB account</span></span>
<span data-ttu-id="7b1c4-242">DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-242">DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="7b1c4-243">When creating a DocumentDB account, the regions in which you would like the service to exist can be specified.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-243">When creating a DocumentDB account, the regions in which you would like the service to exist can be specified.</span></span> <span data-ttu-id="7b1c4-244">Use the instructions in this section to create a multi-region DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-244">Use the instructions in this section to create a multi-region DocumentDB account.</span></span> <span data-ttu-id="7b1c4-245">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-245">This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.</span></span>

### <a id="create-multi-documentdb-account-cli"></a> <span data-ttu-id="7b1c4-246">Create a multi-region DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="7b1c4-246">Create a multi-region DocumentDB account using Azure CLI 1.0 without Resource Manager templates</span></span>
<span data-ttu-id="7b1c4-247">Create a DocumentDB account in the new or existing resource group by entering the following command at the command prompt:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-247">Create a DocumentDB account in the new or existing resource group by entering the following command at the command prompt:</span></span>

> [!TIP]
> If you run this command in Azure PowerShell or Windows PowerShell you receive an error about an unexpected token. Instead, run this command at the Windows Command Prompt.
>
>

    azure resource create -g <resourcegroupname> -n <databaseaccountname> -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l <resourcegrouplocation> -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"<ip-range-filter>\",\"locations\":["{\"locationName\":\"<databaseaccountlocation1>\",\"failoverPriority\":\"<failoverPriority1>\"},{\"locationName\":\"<databaseaccountlocation2>\",\"failoverPriority\":\"<failoverPriority2>\"}"]}"

* <span data-ttu-id="7b1c4-250">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-250">`<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.</span></span>
* <span data-ttu-id="7b1c4-251">`<resourcegrouplocation>` is the region of the current resource group.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-251">`<resourcegrouplocation>` is the region of the current resource group.</span></span>
* <span data-ttu-id="7b1c4-252">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-252">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="7b1c4-253">IP addresses/ranges must be comma separated and must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-253">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="7b1c4-254">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="7b1c4-254">For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)</span></span>
* <span data-ttu-id="7b1c4-255">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-255">`<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>
* <span data-ttu-id="7b1c4-256">`<databaseaccountlocation1>` and `<databaseaccountlocation2>` must be regions in which DocumentDB is generally available.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-256">`<databaseaccountlocation1>` and `<databaseaccountlocation2>` must be regions in which DocumentDB is generally available.</span></span> <span data-ttu-id="7b1c4-257">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-257">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

<span data-ttu-id="7b1c4-258">Example input:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-258">Example input:</span></span>

    azure resource create -g new_res_group -n samplecliacct -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l westus -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"\",\"locations\":["{\"locationName\":\"westus\",\"failoverPriority\":\"0\"},{\"locationName\":\"eastus\",\"failoverPriority\":\"1\"}"]}"

<span data-ttu-id="7b1c4-259">Which produces the following output as your new account is provisioned:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-259">Which produces the following output as your new account is provisioned:</span></span>

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

<span data-ttu-id="7b1c4-260">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-260">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>

<span data-ttu-id="7b1c4-261">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-261">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="7b1c4-262">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-262">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

### <a id="create-multi-documentdb-account-cli-arm"></a> <span data-ttu-id="7b1c4-263">Create a multi-region DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="7b1c4-263">Create a multi-region DocumentDB account using Azure CLI 1.0 with Resource Manager templates</span></span>
<span data-ttu-id="7b1c4-264">The instructions in this section describe how to create a DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-264">The instructions in this section describe how to create a DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files.</span></span> <span data-ttu-id="7b1c4-265">Using a template enables you to describe exactly what you want and repeat it without errors.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-265">Using a template enables you to describe exactly what you want and repeat it without errors.</span></span>

<span data-ttu-id="7b1c4-266">Create a local template file with the following content.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-266">Create a local template file with the following content.</span></span> <span data-ttu-id="7b1c4-267">Name the file azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-267">Name the file azuredeploy.json.</span></span>

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
                        }
                    ]
                }
            }
        ]
    }

<span data-ttu-id="7b1c4-268">The preceding template file can be used to create a DocumentDB account with two regions.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-268">The preceding template file can be used to create a DocumentDB account with two regions.</span></span> <span data-ttu-id="7b1c4-269">To create the account with more regions, add it to the "locations" array and add the corresponding parameters.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-269">To create the account with more regions, add it to the "locations" array and add the corresponding parameters.</span></span>

<span data-ttu-id="7b1c4-270">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="7b1c4-270">One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally].</span></span> <span data-ttu-id="7b1c4-271">The failover priority values must be unique among the locations and the highest failover priority value must be less than the total number of regions.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-271">The failover priority values must be unique among the locations and the highest failover priority value must be less than the total number of regions.</span></span> <span data-ttu-id="7b1c4-272">You can either enter the value at the command line, or create a parameter file to specify the value.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-272">You can either enter the value at the command line, or create a parameter file to specify the value.</span></span>

<span data-ttu-id="7b1c4-273">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-273">To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json.</span></span> <span data-ttu-id="7b1c4-274">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-274">If you plan on specifying the database account name at the command prompt, you can continue without creating this file.</span></span>

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
            }
        }
    }

<span data-ttu-id="7b1c4-275">In the azuredeploy.parameters.json file, update the value field of `"samplearmacct"` to the database name you'd like to use, then save the file.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-275">In the azuredeploy.parameters.json file, update the value field of `"samplearmacct"` to the database name you'd like to use, then save the file.</span></span> <span data-ttu-id="7b1c4-276">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-276">`"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span> <span data-ttu-id="7b1c4-277">Update the value field of `"locationName1"` and `"locationName2"` to the region where you would like to create the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-277">Update the value field of `"locationName1"` and `"locationName2"` to the region where you would like to create the DocumentDB account.</span></span>

<span data-ttu-id="7b1c4-278">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-278">To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional).</span></span>

<span data-ttu-id="7b1c4-279">To use a parameter file:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-279">To use a parameter file:</span></span>

    azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g <resourcegroupname> -n <deploymentname>

* <span data-ttu-id="7b1c4-280">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-280">`<PathToTemplate>` is the path to the azuredeploy.json file created in step 1.</span></span> <span data-ttu-id="7b1c4-281">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-281">If your path name has spaces in it, put double quotes around this parameter.</span></span>
* <span data-ttu-id="7b1c4-282">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-282">`<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1.</span></span> <span data-ttu-id="7b1c4-283">If your path name has spaces in it, put double quotes around this parameter.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-283">If your path name has spaces in it, put double quotes around this parameter.</span></span>
* <span data-ttu-id="7b1c4-284">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-284">`<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account.</span></span>
* <span data-ttu-id="7b1c4-285">`<deploymentname>` is the optional name of the deployment.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-285">`<deploymentname>` is the optional name of the deployment.</span></span>

<span data-ttu-id="7b1c4-286">Example input:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-286">Example input:</span></span>

    azure group deployment create -f azuredeploy.json -e azuredeploy.parameters.json -g new_res_group -n azuredeploy

<span data-ttu-id="7b1c4-287">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-287">OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:</span></span>

    azure group deployment create -f <PathToTemplate> -g <resourcegroupname> -n <deploymentname>

<span data-ttu-id="7b1c4-288">Example input, which shows the prompt and entry for a database account named samplearmacct:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-288">Example input, which shows the prompt and entry for a database account named samplearmacct:</span></span>

    azure group deployment create -f azuredeploy.json -g new_res_group -n azuredeploy
    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    databaseAccountName: samplearmacct

<span data-ttu-id="7b1c4-289">As the account is provisioned, you receive the following information:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-289">As the account is provisioned, you receive the following information:</span></span>

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
    data:    locationName2        String  eastus
    info:    group deployment create command OK

<span data-ttu-id="7b1c4-290">If you encounter errors, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-290">If you encounter errors, see [Troubleshooting](#troubleshooting).</span></span>  

<span data-ttu-id="7b1c4-291">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-291">After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use.</span></span> <span data-ttu-id="7b1c4-292">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-292">You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7b1c4-293">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="7b1c4-293">Troubleshooting</span></span>
<span data-ttu-id="7b1c4-294">If you receive errors like `Deployment provisioning state was not successful` while creating your resource group or database account, you have a few troubleshooting options.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-294">If you receive errors like `Deployment provisioning state was not successful` while creating your resource group or database account, you have a few troubleshooting options.</span></span>

> [!NOTE]
> Providing incorrect characters in the database account name or providing a location in which DocumentDB is not available will cause deployment errors. Database account names can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters. All valid database account locations are listed on the [Azure Regions page](https://azure.microsoft.com/regions/#services).
>
>

* <span data-ttu-id="7b1c4-298">If your output contains the following `Error information has been recorded to C:\Users\wendy\.azure\azure.err`, then review the error info in the azure.err file.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-298">If your output contains the following `Error information has been recorded to C:\Users\wendy\.azure\azure.err`, then review the error info in the azure.err file.</span></span>
* <span data-ttu-id="7b1c4-299">You may find useful info in the log file for the resource group.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-299">You may find useful info in the log file for the resource group.</span></span> <span data-ttu-id="7b1c4-300">To view the log file, run the following command:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-300">To view the log file, run the following command:</span></span>

        azure group log show <resourcegroupname> --last-deployment

    <span data-ttu-id="7b1c4-301">Example input:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-301">Example input:</span></span>

        azure group log show new_res_group --last-deployment

    <span data-ttu-id="7b1c4-302">Then see [Troubleshooting resource group deployments in Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md) for additional information.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-302">Then see [Troubleshooting resource group deployments in Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md) for additional information.</span></span>
* <span data-ttu-id="7b1c4-303">Error information is also available in the Azure portal as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-303">Error information is also available in the Azure portal as shown in the following screenshot.</span></span> <span data-ttu-id="7b1c4-304">To navigate to the error info: click Resource Groups in the Jumpbar, select the Resource Group that had the error, then in the Essentials area of the Resource group blade click the date of the Last Deployment, then in the Deployment history blade select the failed deployment, then in the Deployment blade click the Operation detail with the red exclamation mark.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-304">To navigate to the error info: click Resource Groups in the Jumpbar, select the Resource Group that had the error, then in the Essentials area of the Resource group blade click the date of the Last Deployment, then in the Deployment history blade select the failed deployment, then in the Deployment blade click the Operation detail with the red exclamation mark.</span></span> <span data-ttu-id="7b1c4-305">The Status Message for the failed deployment is displayed in the Operation details blade.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-305">The Status Message for the failed deployment is displayed in the Operation details blade.</span></span>

    ![Screenshot of the Azure portal showing how to navigate to the deployment error message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/portal-troubleshooting-deploy.png)

## <a name="next-steps"></a><span data-ttu-id="7b1c4-307">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b1c4-307">Next steps</span></span>
<span data-ttu-id="7b1c4-308">Now that you have a DocumentDB account, the next step is to create a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-308">Now that you have a DocumentDB account, the next step is to create a DocumentDB database.</span></span> <span data-ttu-id="7b1c4-309">You can create a database by using one of the following:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-309">You can create a database by using one of the following:</span></span>

* <span data-ttu-id="7b1c4-310">The Azure portal, as described in [Create a DocumentDB collection and database using the Azure portal](documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-310">The Azure portal, as described in [Create a DocumentDB collection and database using the Azure portal](documentdb-create-collection.md).</span></span>
* <span data-ttu-id="7b1c4-311">The C# .NET samples in the [DatabaseManagement](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples/DatabaseManagement) project of the [azure-documentdb-dotnet](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples) repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-311">The C# .NET samples in the [DatabaseManagement](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples/DatabaseManagement) project of the [azure-documentdb-dotnet](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples) repository on GitHub.</span></span>
* <span data-ttu-id="7b1c4-312">The [DocumentDB SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-312">The [DocumentDB SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span></span> <span data-ttu-id="7b1c4-313">DocumentDB has .NET, Java, Python, Node.js, and JavaScript API SDKs.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-313">DocumentDB has .NET, Java, Python, Node.js, and JavaScript API SDKs.</span></span>

<span data-ttu-id="7b1c4-314">After creating your database, you need to [add one or more collections](documentdb-create-collection.md) to the database, then [add documents](documentdb-view-json-document-explorer.md) to the collections.</span><span class="sxs-lookup"><span data-stu-id="7b1c4-314">After creating your database, you need to [add one or more collections](documentdb-create-collection.md) to the database, then [add documents](documentdb-view-json-document-explorer.md) to the collections.</span></span>

<span data-ttu-id="7b1c4-315">After you have documents in a collection, you can use [DocumentDB SQL](documentdb-sql-query.md) to [execute queries](documentdb-sql-query.md#ExecutingSqlQueries) against your documents by using the [Query Explorer](documentdb-query-collections-query-explorer.md) in the portal, the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), or one of the [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-315">After you have documents in a collection, you can use [DocumentDB SQL](documentdb-sql-query.md) to [execute queries](documentdb-sql-query.md#ExecutingSqlQueries) against your documents by using the [Query Explorer](documentdb-query-collections-query-explorer.md) in the portal, the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), or one of the [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span></span>

<span data-ttu-id="7b1c4-316">To learn more about DocumentDB, explore these resources:</span><span class="sxs-lookup"><span data-stu-id="7b1c4-316">To learn more about DocumentDB, explore these resources:</span></span>

* [<span data-ttu-id="7b1c4-317">Learning path for DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7b1c4-317">Learning path for DocumentDB</span></span>](https://azure.microsoft.com/documentation/learning-paths/documentdb/)
* [<span data-ttu-id="7b1c4-318">DocumentDB resource model and concepts</span><span class="sxs-lookup"><span data-stu-id="7b1c4-318">DocumentDB resource model and concepts</span></span>](documentdb-resources.md)

<span data-ttu-id="7b1c4-319">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="7b1c4-319">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[distribute-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally
[scaling-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally/#scaling-across-the-planet




