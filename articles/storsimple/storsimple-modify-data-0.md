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
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-device"></a>Modify the DATA 0 network interface settings on your StorSimple device
## <a name="overview"></a>Overview
Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5. The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled. Note that you cannot configure DATA 0 network interface through the Azure classic portal. 

The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device. When the device is in an operational mode, you may need to reconfigure DATA 0 settings. This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.

After reading this tutorial, you will be able to:

* Modify DATA 0 network setting through the setup wizard
* Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modify DATA 0 network settings through setup wizard
You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session. Perform the following steps to modify DATA 0 settings:

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a>To modify DATA 0 network settings through setup wizard
1. In the serial console menu, choose option 1, **Log in with full access**. When prompted provide the **device administrator password**. The default password is `Password1`.
2. At the command prompt, type:
   
    `Invoke-HcsSetupWizard`
3. A setup wizard will appear to help you configure the DATA 0 interface of your device. Provide new values for the IP address, gateway, and netmask.

> [!NOTE]
> The fixed controllers IPs will need to be reconfigured through the **Configure** page of the StorSimple device in the Azure classic portal. For more information, go to [Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modify DATA 0 network settings through Set-HcsNetInterface cmdlet
An alternate way to reconfigure DATA 0 network interface is through the use of  the `Set-HcsNetInterface` cmdlet. The cmdlet is executed from the Windows PowerShell interface of your StorSimple device. When using this procedure, the controller fixed IPs can also be configured here. Perform the following steps to modify the DATA 0 settings: 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a>To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet
1. In the serial console menu, choose option 1, **Log in with full access**. When prompted provide the device administrator password. The default password is `Password1`.
2. At the command prompt, type:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    In the angled brackets, type the following values for DATA 0:
   
   * IPv4 address
   * IPv4 gateway
   * IPv4 subnet mask
   * Fixed IPv4 address for Controller 0
   * Fixed IPv4 address for Controller 1
     
     For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Next steps
* To configure network interfaces other than DATA 0, you can use the [Configure page in the Azure classic portal](storsimple-modify-device-config.md). 
* If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).
