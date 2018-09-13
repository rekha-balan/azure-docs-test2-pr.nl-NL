---
services: virtual-machines
title: Setting up PowerShell
author: JoeDavies-MSFT
solutions: ''
manager: timlt
editor: tysonn
ms.service: virtual-machines
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 05/12/2015
ms.author: rasquill
ms.openlocfilehash: 19c704d965ff3e2fc9ac8c5b623aeb386cb0b974
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564122"
---
## <a name="setting-up-powershell"></a><span data-ttu-id="3a2c5-102">Setting up PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a2c5-102">Setting up PowerShell</span></span>
<span data-ttu-id="3a2c5-103">Before you can use Azure PowerShell, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-103">Before you can use Azure PowerShell, follow these steps.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="3a2c5-104">Verify PowerShell versions</span><span class="sxs-lookup"><span data-stu-id="3a2c5-104">Verify PowerShell versions</span></span>
<span data-ttu-id="3a2c5-105">Before you can use Windows PowerShell, you must have Windows PowerShell, Version 3.0 or 4.0.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-105">Before you can use Windows PowerShell, you must have Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="3a2c5-106">To find the version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-106">To find the version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="3a2c5-107">You should see something like this.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-107">You should see something like this.</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2

<span data-ttu-id="3a2c5-108">Verify that the value of **PSVersion** is 3.0 or 4.0.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-108">Verify that the value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="3a2c5-109">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-109">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="3a2c5-110">You should also have Azure PowerShell version 0.8.0 or later.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-110">You should also have Azure PowerShell version 0.8.0 or later.</span></span> <span data-ttu-id="3a2c5-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version

<span data-ttu-id="3a2c5-112">You should see something like this.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-112">You should see something like this.</span></span>

    Version
    -------
    0.8.16.1

<span data-ttu-id="3a2c5-113">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-113">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="3a2c5-114">Set your Azure account and subscription</span><span class="sxs-lookup"><span data-stu-id="3a2c5-114">Set your Azure account and subscription</span></span>
<span data-ttu-id="3a2c5-115">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-115">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="3a2c5-116">Open an Azure PowerShell command prompt and log on to Azure with this command.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-116">Open an Azure PowerShell command prompt and log on to Azure with this command.</span></span>

    Add-AzureAccount

<span data-ttu-id="3a2c5-117">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-117">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureSubscription

<span data-ttu-id="3a2c5-118">You will receive the following type of information:</span><span class="sxs-lookup"><span data-stu-id="3a2c5-118">You will receive the following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName : 
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="3a2c5-119">You can set the current Azure subscription by running these commands at the Azure PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-119">You can set the current Azure subscription by running these commands at the Azure PowerShell command prompt.</span></span> <span data-ttu-id="3a2c5-120">Replace everything within the quotes, including the < and > characters, with the correct name.</span><span class="sxs-lookup"><span data-stu-id="3a2c5-120">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<SubscriptionName from the display of Get-AzureSubscription>"
    Select-AzureSubscription -SubscriptionName $subscr -Current    

<span data-ttu-id="3a2c5-121">For more information about Azure subscriptions and accounts, see [How to: Connect to your subscription](/powershell/azureps-cmdlets-docs#Connect).</span><span class="sxs-lookup"><span data-stu-id="3a2c5-121">For more information about Azure subscriptions and accounts, see [How to: Connect to your subscription](/powershell/azureps-cmdlets-docs#Connect).</span></span>

