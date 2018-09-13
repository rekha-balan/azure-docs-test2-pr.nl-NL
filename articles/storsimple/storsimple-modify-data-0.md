---
title: Modify the DATA 0 settings on a StorSimple device | Microsoft Docs
description: Learn how to use Windows PowerShell for StorSimple to reconfigure the DATA 0 network interface on your StorSimple device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 3a47ff1eed220cede820e8698c3384300e94688d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549209"
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="ef6c6-103">Modify the DATA 0 network interface settings on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="ef6c6-103">Modify the DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="ef6c6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ef6c6-104">Overview</span></span>
<span data-ttu-id="ef6c6-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="ef6c6-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="ef6c6-107">Note that you cannot configure DATA 0 network interface through the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-107">Note that you cannot configure DATA 0 network interface through the Azure classic portal.</span></span> 

<span data-ttu-id="ef6c6-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="ef6c6-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="ef6c6-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="ef6c6-111">After reading this tutorial, you will be able to:</span><span class="sxs-lookup"><span data-stu-id="ef6c6-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="ef6c6-112">Modify DATA 0 network setting through the setup wizard</span><span class="sxs-lookup"><span data-stu-id="ef6c6-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="ef6c6-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="ef6c6-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="ef6c6-114">Modify DATA 0 network settings through setup wizard</span><span class="sxs-lookup"><span data-stu-id="ef6c6-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="ef6c6-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="ef6c6-116">Perform the following steps to modify DATA 0 settings:</span><span class="sxs-lookup"><span data-stu-id="ef6c6-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="ef6c6-117">To modify DATA 0 network settings through setup wizard</span><span class="sxs-lookup"><span data-stu-id="ef6c6-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="ef6c6-118">In the serial console menu, choose option 1, **Log in with full access**.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="ef6c6-119">When prompted provide the **device administrator password**.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="ef6c6-120">The default password is `Password1`.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="ef6c6-121">At the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="ef6c6-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="ef6c6-122">A setup wizard will appear to help you configure the DATA 0 interface of your device.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-122">A setup wizard will appear to help you configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="ef6c6-123">Provide new values for the IP address, gateway, and netmask.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="ef6c6-124">The fixed controllers IPs will need to be reconfigured through the **Configure** page of the StorSimple device in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-124">The fixed controllers IPs will need to be reconfigured through the **Configure** page of the StorSimple device in the Azure classic portal.</span></span> <span data-ttu-id="ef6c6-125">For more information, go to [Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="ef6c6-125">For more information, go to [Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="ef6c6-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span><span class="sxs-lookup"><span data-stu-id="ef6c6-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="ef6c6-127">An alternate way to reconfigure DATA 0 network interface is through the use of  the `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-127">An alternate way to reconfigure DATA 0 network interface is through the use of  the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="ef6c6-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="ef6c6-129">When using this procedure, the controller fixed IPs can also be configured here.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="ef6c6-130">Perform the following steps to modify the DATA 0 settings:</span><span class="sxs-lookup"><span data-stu-id="ef6c6-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="ef6c6-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span><span class="sxs-lookup"><span data-stu-id="ef6c6-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="ef6c6-132">In the serial console menu, choose option 1, **Log in with full access**.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="ef6c6-133">When prompted provide the device administrator password.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="ef6c6-134">The default password is `Password1`.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="ef6c6-135">At the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="ef6c6-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="ef6c6-136">In the angled brackets, type the following values for DATA 0:</span><span class="sxs-lookup"><span data-stu-id="ef6c6-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="ef6c6-137">IPv4 address</span><span class="sxs-lookup"><span data-stu-id="ef6c6-137">IPv4 address</span></span>
   * <span data-ttu-id="ef6c6-138">IPv4 gateway</span><span class="sxs-lookup"><span data-stu-id="ef6c6-138">IPv4 gateway</span></span>
   * <span data-ttu-id="ef6c6-139">IPv4 subnet mask</span><span class="sxs-lookup"><span data-stu-id="ef6c6-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="ef6c6-140">Fixed IPv4 address for Controller 0</span><span class="sxs-lookup"><span data-stu-id="ef6c6-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="ef6c6-141">Fixed IPv4 address for Controller 1</span><span class="sxs-lookup"><span data-stu-id="ef6c6-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="ef6c6-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef6c6-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef6c6-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef6c6-143">Next steps</span></span>
* <span data-ttu-id="ef6c6-144">To configure network interfaces other than DATA 0, you can use the [Configure page in the Azure classic portal](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="ef6c6-144">To configure network interfaces other than DATA 0, you can use the [Configure page in the Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="ef6c6-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ef6c6-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

