---
services: virtual-machines
title: Setting up Azure CLI for service management
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
ms.openlocfilehash: 737e4be21eefcbd6fbd31d15a6f77770cd59ca67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670210"
---
## <a name="using-azure-cli"></a>Using Azure CLI
The following steps help you use Azure CLI easily with the most recent version and the proper subscription. If you need to install Azure CLI and connect it to your account first, see the [Azure Command-Line Interface (Azure CLI)](../articles/cli-install-nodejs.md).

### <a name="step-1-update-azure-cli-version"></a>Step 1: Update Azure CLI version
To use Azure CLI for imperative commands with service management mode, you should have a recent version if possible. To verify your version, type `azure --version`. You should see something like:

    $ azure --version
    0.8.17 (node: 0.10.25)

If you want to update your version of Azure CLI, see [Azure CLI](https://github.com/Azure/azure-xplat-cli).

### <a name="step-2-set-the-azure-account-and-subscription"></a>Step 2: Set the Azure account and subscription
Once you have connected your Azure CLI with the account you want to use, you may have more than one subscription. If you do, you should review the subscriptions available for your account by typing `azure account list`, and then select the subscription you want to use by typing `azure account set <subscription id or name> true` where *subscription id or name* is either the subscription id or the subscription name that you would like to work with in the current session. You should see something like the following:

    $ azure account set "Visual Studio Ultimate with MSDN" true
    info:    Executing command account set
    info:    Setting subscription to "Visual Studio Ultimate with MSDN" with id "0e220bf6-5caa-4e9f-8383-51f16b6c109f".
    info:    Changes saved
    info:    account set command OK

> [!NOTE]
> If you don't already have an Azure account but you do have a subscription to MSDN subscription, you can get free Azure credits by activating your [MSDN subscriber benefits here](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -- or you can use the free account. Either will work for Azure access.
> 
> 

