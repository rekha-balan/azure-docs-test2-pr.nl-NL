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
## <a name="using-azure-cli"></a><span data-ttu-id="9378a-102">Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9378a-102">Using Azure CLI</span></span>
<span data-ttu-id="9378a-103">The following steps help you use Azure CLI easily with the most recent version and the proper subscription.</span><span class="sxs-lookup"><span data-stu-id="9378a-103">The following steps help you use Azure CLI easily with the most recent version and the proper subscription.</span></span> <span data-ttu-id="9378a-104">If you need to install Azure CLI and connect it to your account first, see the [Azure Command-Line Interface (Azure CLI)](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9378a-104">If you need to install Azure CLI and connect it to your account first, see the [Azure Command-Line Interface (Azure CLI)](../articles/cli-install-nodejs.md).</span></span>

### <a name="step-1-update-azure-cli-version"></a><span data-ttu-id="9378a-105">Step 1: Update Azure CLI version</span><span class="sxs-lookup"><span data-stu-id="9378a-105">Step 1: Update Azure CLI version</span></span>
<span data-ttu-id="9378a-106">To use Azure CLI for imperative commands with service management mode, you should have a recent version if possible.</span><span class="sxs-lookup"><span data-stu-id="9378a-106">To use Azure CLI for imperative commands with service management mode, you should have a recent version if possible.</span></span> <span data-ttu-id="9378a-107">To verify your version, type `azure --version`.</span><span class="sxs-lookup"><span data-stu-id="9378a-107">To verify your version, type `azure --version`.</span></span> <span data-ttu-id="9378a-108">You should see something like:</span><span class="sxs-lookup"><span data-stu-id="9378a-108">You should see something like:</span></span>

    $ azure --version
    0.8.17 (node: 0.10.25)

<span data-ttu-id="9378a-109">If you want to update your version of Azure CLI, see [Azure CLI](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="9378a-109">If you want to update your version of Azure CLI, see [Azure CLI](https://github.com/Azure/azure-xplat-cli).</span></span>

### <a name="step-2-set-the-azure-account-and-subscription"></a><span data-ttu-id="9378a-110">Step 2: Set the Azure account and subscription</span><span class="sxs-lookup"><span data-stu-id="9378a-110">Step 2: Set the Azure account and subscription</span></span>
<span data-ttu-id="9378a-111">Once you have connected your Azure CLI with the account you want to use, you may have more than one subscription.</span><span class="sxs-lookup"><span data-stu-id="9378a-111">Once you have connected your Azure CLI with the account you want to use, you may have more than one subscription.</span></span> <span data-ttu-id="9378a-112">If you do, you should review the subscriptions available for your account by typing `azure account list`, and then select the subscription you want to use by typing `azure account set <subscription id or name> true` where *subscription id or name* is either the subscription id or the subscription name that you would like to work with in the current session.</span><span class="sxs-lookup"><span data-stu-id="9378a-112">If you do, you should review the subscriptions available for your account by typing `azure account list`, and then select the subscription you want to use by typing `azure account set <subscription id or name> true` where *subscription id or name* is either the subscription id or the subscription name that you would like to work with in the current session.</span></span> <span data-ttu-id="9378a-113">You should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="9378a-113">You should see something like the following:</span></span>

    $ azure account set "Visual Studio Ultimate with MSDN" true
    info:    Executing command account set
    info:    Setting subscription to "Visual Studio Ultimate with MSDN" with id "0e220bf6-5caa-4e9f-8383-51f16b6c109f".
    info:    Changes saved
    info:    account set command OK

> [!NOTE]
> <span data-ttu-id="9378a-114">If you don't already have an Azure account but you do have a subscription to MSDN subscription, you can get free Azure credits by activating your [MSDN subscriber benefits here](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -- or you can use the free account.</span><span class="sxs-lookup"><span data-stu-id="9378a-114">If you don't already have an Azure account but you do have a subscription to MSDN subscription, you can get free Azure credits by activating your [MSDN subscriber benefits here](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -- or you can use the free account.</span></span> <span data-ttu-id="9378a-115">Either will work for Azure access.</span><span class="sxs-lookup"><span data-stu-id="9378a-115">Either will work for Azure access.</span></span>
> 
> 

