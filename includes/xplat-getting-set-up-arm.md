---
services: virtual-machines
title: Using Azure CLI with Azure Resource Manager
author: squillace
solutions: ''
manager: timlt
editor: tysonn
ms.service: virtual-machine
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: linux
ms.workload: infrastructure
ms.date: 04/13/2015
ms.author: rasquill
ms.openlocfilehash: e2f9d2c74e5dfa0a08f25685062903a985ba641c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551738"
---
## <a name="using-azure-cli-with-azure-resource-manager-arm"></a><span data-ttu-id="03ef0-102">Using Azure CLI with Azure Resource Manager (ARM)</span><span class="sxs-lookup"><span data-stu-id="03ef0-102">Using Azure CLI with Azure Resource Manager (ARM)</span></span>
<span data-ttu-id="03ef0-103">Before you can use the Azure CLI with Resource Manager commands and templates to deploy Azure resources and workloads using resource groups, you will need an account with Azure (of course).</span><span class="sxs-lookup"><span data-stu-id="03ef0-103">Before you can use the Azure CLI with Resource Manager commands and templates to deploy Azure resources and workloads using resource groups, you will need an account with Azure (of course).</span></span> <span data-ttu-id="03ef0-104">If you do not have an account, you can get a [free Azure trial here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03ef0-104">If you do not have an account, you can get a [free Azure trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

> [!NOTE]
> <span data-ttu-id="03ef0-105">If you don't already have an Azure account but you do have a subscription to MSDN subscription, you can get free Azure credits by activating your [MSDN subscriber benefits here](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -- or you can use the free account.</span><span class="sxs-lookup"><span data-stu-id="03ef0-105">If you don't already have an Azure account but you do have a subscription to MSDN subscription, you can get free Azure credits by activating your [MSDN subscriber benefits here](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -- or you can use the free account.</span></span> <span data-ttu-id="03ef0-106">Either will work for Azure access.</span><span class="sxs-lookup"><span data-stu-id="03ef0-106">Either will work for Azure access.</span></span>
> 
> 

### <a name="step-1-verify-the-azure-cli-version"></a><span data-ttu-id="03ef0-107">Step 1: Verify the Azure CLI version</span><span class="sxs-lookup"><span data-stu-id="03ef0-107">Step 1: Verify the Azure CLI version</span></span>
<span data-ttu-id="03ef0-108">To use Azure CLI for imperative commands and ARM templates, you need to have at least version 0.8.17.</span><span class="sxs-lookup"><span data-stu-id="03ef0-108">To use Azure CLI for imperative commands and ARM templates, you need to have at least version 0.8.17.</span></span> <span data-ttu-id="03ef0-109">To verify your version, type `azure --version`.</span><span class="sxs-lookup"><span data-stu-id="03ef0-109">To verify your version, type `azure --version`.</span></span> <span data-ttu-id="03ef0-110">You should see something like:</span><span class="sxs-lookup"><span data-stu-id="03ef0-110">You should see something like:</span></span>

    $ azure --version
    0.8.17 (node: 0.10.25)

<span data-ttu-id="03ef0-111">If you need to update your version of Azure CLI, see [Azure CLI](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="03ef0-111">If you need to update your version of Azure CLI, see [Azure CLI](https://github.com/Azure/azure-xplat-cli).</span></span>

### <a name="step-2-verify-you-are-using-a-work-or-school-identity-with-azure"></a><span data-ttu-id="03ef0-112">Step 2: Verify you are using a work or school identity with Azure</span><span class="sxs-lookup"><span data-stu-id="03ef0-112">Step 2: Verify you are using a work or school identity with Azure</span></span>
<span data-ttu-id="03ef0-113">You can only use the ARM command mode if you are using an [Azure Active Directory tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) or a [Service Principal Name](https://msdn.microsoft.com/library/azure/dn132633.aspx).</span><span class="sxs-lookup"><span data-stu-id="03ef0-113">You can only use the ARM command mode if you are using an [Azure Active Directory tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) or a [Service Principal Name](https://msdn.microsoft.com/library/azure/dn132633.aspx).</span></span> <span data-ttu-id="03ef0-114">(These are also called *organizational ids*.)</span><span class="sxs-lookup"><span data-stu-id="03ef0-114">(These are also called *organizational ids*.)</span></span>

<span data-ttu-id="03ef0-115">To see if you have one, log in by typing `azure login` and using your work or school username and password when prompted.</span><span class="sxs-lookup"><span data-stu-id="03ef0-115">To see if you have one, log in by typing `azure login` and using your work or school username and password when prompted.</span></span> <span data-ttu-id="03ef0-116">If you do have one, you should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="03ef0-116">If you do have one, you should see something like the following:</span></span>

    $ azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@contoso.onmicrosoft.com
    Password: *********
    |info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Setting subscription Visual Studio Ultimate with MSDN as default
    info:    Added subscription Azure Free Trial
    +
    info:    login command OK

<span data-ttu-id="03ef0-117">If you do not see this, you must create a new tenant (or service principal) with your Microsoft account identity.</span><span class="sxs-lookup"><span data-stu-id="03ef0-117">If you do not see this, you must create a new tenant (or service principal) with your Microsoft account identity.</span></span> <span data-ttu-id="03ef0-118">(This is often the case with personal MSDN subscriptions or free trial subscriptions.) To create a work or school id from your Azure account created with a Microsoft id, see [Associate an Azure AD Directory with a new Azure Subscription](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span><span class="sxs-lookup"><span data-stu-id="03ef0-118">(This is often the case with personal MSDN subscriptions or free trial subscriptions.) To create a work or school id from your Azure account created with a Microsoft id, see [Associate an Azure AD Directory with a new Azure Subscription](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> <span data-ttu-id="03ef0-119">If you think you should have an organizational id already, you may need to talk with the person who created the account for you.</span><span class="sxs-lookup"><span data-stu-id="03ef0-119">If you think you should have an organizational id already, you may need to talk with the person who created the account for you.</span></span>

### <a name="step-3-choose-your-azure-subscription"></a><span data-ttu-id="03ef0-120">Step 3: Choose your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="03ef0-120">Step 3: Choose your Azure subscription</span></span>
<span data-ttu-id="03ef0-121">If you have only one subscription in your Azure account, Azure CLI associates itself with that subscription by default.</span><span class="sxs-lookup"><span data-stu-id="03ef0-121">If you have only one subscription in your Azure account, Azure CLI associates itself with that subscription by default.</span></span> <span data-ttu-id="03ef0-122">If you have more than one subscription, you need to select the subscription you want to use by typing `azure account set <subscription id or name> true` where *subscription id or name* is either the subscription id or the subscription name that you would like to work with in the current session.</span><span class="sxs-lookup"><span data-stu-id="03ef0-122">If you have more than one subscription, you need to select the subscription you want to use by typing `azure account set <subscription id or name> true` where *subscription id or name* is either the subscription id or the subscription name that you would like to work with in the current session.</span></span>

<span data-ttu-id="03ef0-123">You should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="03ef0-123">You should see something like the following:</span></span>

    $ azure account set "Azure Free Trial" true
    info:    Executing command account set
    info:    Setting subscription to "Azure Free Trial" with id "2lskd82-434-4730-9df9-akd83lsk92sa".
    info:    Changes saved
    info:    account set command OK

### <a name="step-4-place-your-azure-cli-in-the-arm-mode"></a><span data-ttu-id="03ef0-124">Step 4: Place your Azure CLI in the ARM mode</span><span class="sxs-lookup"><span data-stu-id="03ef0-124">Step 4: Place your Azure CLI in the ARM mode</span></span>
<span data-ttu-id="03ef0-125">To use the Azure Resource Management (ARM) mode with the Azure CLI, type `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="03ef0-125">To use the Azure Resource Management (ARM) mode with the Azure CLI, type `azure config mode arm`.</span></span> <span data-ttu-id="03ef0-126">You should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="03ef0-126">You should see something like the following:</span></span>

    $ azure config mode arm
    info:    New mode is arm

> [!NOTE]
> <span data-ttu-id="03ef0-127">You can switch back to use Azure service management commands by typing `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="03ef0-127">You can switch back to use Azure service management commands by typing `azure config mode asm`.</span></span>
> 
> 

