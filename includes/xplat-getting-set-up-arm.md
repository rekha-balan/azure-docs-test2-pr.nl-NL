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
## <a name="using-azure-cli-with-azure-resource-manager-arm"></a>Using Azure CLI with Azure Resource Manager (ARM)
Before you can use the Azure CLI with Resource Manager commands and templates to deploy Azure resources and workloads using resource groups, you will need an account with Azure (of course). If you do not have an account, you can get a [free Azure trial here](https://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> If you don't already have an Azure account but you do have a subscription to MSDN subscription, you can get free Azure credits by activating your [MSDN subscriber benefits here](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -- or you can use the free account. Either will work for Azure access.
> 
> 

### <a name="step-1-verify-the-azure-cli-version"></a>Step 1: Verify the Azure CLI version
To use Azure CLI for imperative commands and ARM templates, you need to have at least version 0.8.17. To verify your version, type `azure --version`. You should see something like:

    $ azure --version
    0.8.17 (node: 0.10.25)

If you need to update your version of Azure CLI, see [Azure CLI](https://github.com/Azure/azure-xplat-cli).

### <a name="step-2-verify-you-are-using-a-work-or-school-identity-with-azure"></a>Step 2: Verify you are using a work or school identity with Azure
You can only use the ARM command mode if you are using an [Azure Active Directory tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) or a [Service Principal Name](https://msdn.microsoft.com/library/azure/dn132633.aspx). (These are also called *organizational ids*.)

To see if you have one, log in by typing `azure login` and using your work or school username and password when prompted. If you do have one, you should see something like the following:

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

If you do not see this, you must create a new tenant (or service principal) with your Microsoft account identity. (This is often the case with personal MSDN subscriptions or free trial subscriptions.) To create a work or school id from your Azure account created with a Microsoft id, see [Associate an Azure AD Directory with a new Azure Subscription](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). If you think you should have an organizational id already, you may need to talk with the person who created the account for you.

### <a name="step-3-choose-your-azure-subscription"></a>Step 3: Choose your Azure subscription
If you have only one subscription in your Azure account, Azure CLI associates itself with that subscription by default. If you have more than one subscription, you need to select the subscription you want to use by typing `azure account set <subscription id or name> true` where *subscription id or name* is either the subscription id or the subscription name that you would like to work with in the current session.

You should see something like the following:

    $ azure account set "Azure Free Trial" true
    info:    Executing command account set
    info:    Setting subscription to "Azure Free Trial" with id "2lskd82-434-4730-9df9-akd83lsk92sa".
    info:    Changes saved
    info:    account set command OK

### <a name="step-4-place-your-azure-cli-in-the-arm-mode"></a>Step 4: Place your Azure CLI in the ARM mode
To use the Azure Resource Management (ARM) mode with the Azure CLI, type `azure config mode arm`. You should see something like the following:

    $ azure config mode arm
    info:    New mode is arm

> [!NOTE]
> You can switch back to use Azure service management commands by typing `azure config mode asm`.
> 
> 

