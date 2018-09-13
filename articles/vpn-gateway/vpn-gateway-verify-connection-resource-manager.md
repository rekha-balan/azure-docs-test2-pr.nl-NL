---
title: Verify a VPN Gateway connection | Microsoft Docs
description: This article shows you how to verify a virtual network VPN Gateway connection.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: cherylmc
ms.openlocfilehash: 90af66c64762de3786b7ff9378d02ed9050340e3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554248"
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="89704-103">Verify a VPN Gateway connection</span><span class="sxs-lookup"><span data-stu-id="89704-103">Verify a VPN Gateway connection</span></span>
<span data-ttu-id="89704-104">You can verify your virtual network VPN Gateway connection by using the portal and by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89704-104">You can verify your virtual network VPN Gateway connection by using the portal and by using PowerShell.</span></span> <span data-ttu-id="89704-105">This article contains steps for both the Resource Manager and classic deployment models.</span><span class="sxs-lookup"><span data-stu-id="89704-105">This article contains steps for both the Resource Manager and classic deployment models.</span></span>

## <a name="verify-using-the-azure-portal"></a><span data-ttu-id="89704-106">Verify using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="89704-106">Verify using the Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="verify-using-powershell"></a><span data-ttu-id="89704-107">Verify using PowerShell</span><span class="sxs-lookup"><span data-stu-id="89704-107">Verify using PowerShell</span></span>

<span data-ttu-id="89704-108">To verify by using PowerShell, install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="89704-108">To verify by using PowerShell, install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="89704-109">For information on installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="89704-109">For information on installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="89704-110">For more information about using Resource Manager cmdlets, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="89704-110">For more information about using Resource Manager cmdlets, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="log-in-to-your-azure-account"></a><span data-ttu-id="89704-111">Log in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="89704-111">Log in to your Azure account</span></span>
1. <span data-ttu-id="89704-112">Open your PowerShell console with elevated privileges and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="89704-112">Open your PowerShell console with elevated privileges and connect to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="89704-113">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="89704-113">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ``` 
3. <span data-ttu-id="89704-114">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="89704-114">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

### <a name="verify-your-connection"></a><span data-ttu-id="89704-115">Verify your connection</span><span class="sxs-lookup"><span data-stu-id="89704-115">Verify your connection</span></span>

[!INCLUDE [Powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="verify-using-the-azure-portal-classic"></a><span data-ttu-id="89704-116">Verify using the Azure portal (classic)</span><span class="sxs-lookup"><span data-stu-id="89704-116">Verify using the Azure portal (classic)</span></span>
[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


## <a name="verify-using-powershell-classic"></a><span data-ttu-id="89704-117">Verify using PowerShell (classic)</span><span class="sxs-lookup"><span data-stu-id="89704-117">Verify using PowerShell (classic)</span></span>
<span data-ttu-id="89704-118">To verify by using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="89704-118">To verify by using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="89704-119">Be sure to download and install both the Resource Manager and Service Management (SM) versions.</span><span class="sxs-lookup"><span data-stu-id="89704-119">Be sure to download and install both the Resource Manager and Service Management (SM) versions.</span></span> <span data-ttu-id="89704-120">For information on installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="89704-120">For information on installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> 

### <a name="log-in-to-your-azure-account"></a><span data-ttu-id="89704-121">Log in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="89704-121">Log in to your Azure account</span></span>
1. <span data-ttu-id="89704-122">Open your PowerShell console with elevated privileges and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="89704-122">Open your PowerShell console with elevated privileges and connect to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="89704-123">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="89704-123">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription 
  ```
3. <span data-ttu-id="89704-124">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="89704-124">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```
4. <span data-ttu-id="89704-125">Log in to use the Service Management cmdlets for the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="89704-125">Log in to use the Service Management cmdlets for the classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```

### <a name="verify-your-connection"></a><span data-ttu-id="89704-126">Verify your connection</span><span class="sxs-lookup"><span data-stu-id="89704-126">Verify your connection</span></span>
[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="89704-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="89704-127">Next steps</span></span>
* <span data-ttu-id="89704-128">You can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="89704-128">You can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="89704-129">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span><span class="sxs-lookup"><span data-stu-id="89704-129">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

