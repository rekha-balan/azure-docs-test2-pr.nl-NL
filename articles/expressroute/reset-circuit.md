---
title: 'Reset a failed Azure ExpressRoute circuit: PowerShell | Microsoft Docs'
description: This article helps you reset an ExpressRoute circuit that is in a failed state.
documentationcenter: na
services: expressroute
author: anzaman
manager: ''
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/28/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 423bc1d6409e5b7fe02339a05d0775f4ff42de49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856550"
---
# <a name="reset-a-failed-expressroute-circuit"></a><span data-ttu-id="5e6c6-103">Reset a failed ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="5e6c6-103">Reset a failed ExpressRoute circuit</span></span>

<span data-ttu-id="5e6c6-104">When an operation on an ExpressRoute circuit does not complete successfully, the circuit may go into a 'failed' state.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-104">When an operation on an ExpressRoute circuit does not complete successfully, the circuit may go into a 'failed' state.</span></span> <span data-ttu-id="5e6c6-105">This article helps you reset a failed Azure ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-105">This article helps you reset a failed Azure ExpressRoute circuit.</span></span>

## <a name="reset-a-circuit"></a><span data-ttu-id="5e6c6-106">Reset a circuit</span><span class="sxs-lookup"><span data-stu-id="5e6c6-106">Reset a circuit</span></span>

1. <span data-ttu-id="5e6c6-107">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-107">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5e6c6-108">For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="5e6c6-108">For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

2. <span data-ttu-id="5e6c6-109">Open your PowerShell console with elevated privileges, and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-109">Open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="5e6c6-110">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="5e6c6-110">Use the following example to help you connect:</span></span>

  ```powershell
  Connect-AzureRmAccount
  ```
3. <span data-ttu-id="5e6c6-111">If you have multiple Azure subscriptions, check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-111">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
4. <span data-ttu-id="5e6c6-112">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-112">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```
5. <span data-ttu-id="5e6c6-113">Run the following commands to reset a circuit that is in a failed state:</span><span class="sxs-lookup"><span data-stu-id="5e6c6-113">Run the following commands to reset a circuit that is in a failed state:</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

<span data-ttu-id="5e6c6-114">The circuit should now be healthy.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-114">The circuit should now be healthy.</span></span> <span data-ttu-id="5e6c6-115">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if the circuit is still in a failed state.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-115">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if the circuit is still in a failed state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e6c6-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e6c6-116">Next steps</span></span>

<span data-ttu-id="5e6c6-117">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span><span class="sxs-lookup"><span data-stu-id="5e6c6-117">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>
