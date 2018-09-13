---
title: Diagnostics Tool to troubleshoot StorSimple 8000 device | Microsoft Docs
description: Describes the StorSimple device modes and explains how to use Windows PowerShell for StorSimple to change the device mode.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: alkohli
ms.openlocfilehash: d3488b1e7857799d8ed7de796610e8d52034bd8f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564398"
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="d45c6-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span><span class="sxs-lookup"><span data-stu-id="d45c6-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="d45c6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d45c6-104">Overview</span></span>

<span data-ttu-id="d45c6-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="d45c6-106">The diagnostics tool can be used in various scenarios.</span><span class="sxs-lookup"><span data-stu-id="d45c6-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="d45c6-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="d45c6-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="d45c6-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span><span class="sxs-lookup"><span data-stu-id="d45c6-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="d45c6-110">Run diagnostics tool</span><span class="sxs-lookup"><span data-stu-id="d45c6-110">Run diagnostics tool</span></span>

<span data-ttu-id="d45c6-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="d45c6-112">There are two ways to access the local interface of your device:</span><span class="sxs-lookup"><span data-stu-id="d45c6-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="d45c6-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d45c6-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="d45c6-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d45c6-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="d45c6-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d45c6-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="d45c6-116">To run the diagnostics tool</span><span class="sxs-lookup"><span data-stu-id="d45c6-116">To run the diagnostics tool</span></span>

<span data-ttu-id="d45c6-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d45c6-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="d45c6-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d45c6-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="d45c6-119">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="d45c6-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="d45c6-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span><span class="sxs-lookup"><span data-stu-id="d45c6-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="d45c6-121">These tests include system, hardware component health, network, and performance.</span><span class="sxs-lookup"><span data-stu-id="d45c6-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="d45c6-122">To run only a specific test, specify the scope parameter.</span><span class="sxs-lookup"><span data-stu-id="d45c6-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="d45c6-123">For instance, to run only the network test, type</span><span class="sxs-lookup"><span data-stu-id="d45c6-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="d45c6-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span><span class="sxs-lookup"><span data-stu-id="d45c6-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="d45c6-125">Scenarios to use the diagnostics tool</span><span class="sxs-lookup"><span data-stu-id="d45c6-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="d45c6-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span><span class="sxs-lookup"><span data-stu-id="d45c6-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="d45c6-127">Here are some possible scenarios:</span><span class="sxs-lookup"><span data-stu-id="d45c6-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="d45c6-128">**Device offline** - Your StorSimple 8000 series device is offline.</span><span class="sxs-lookup"><span data-stu-id="d45c6-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="d45c6-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span><span class="sxs-lookup"><span data-stu-id="d45c6-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="d45c6-130">You can use this tool to then determine the network state.</span><span class="sxs-lookup"><span data-stu-id="d45c6-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="d45c6-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span><span class="sxs-lookup"><span data-stu-id="d45c6-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="d45c6-132">A valid IP is assigned to the device during setup wizard and registration.</span><span class="sxs-lookup"><span data-stu-id="d45c6-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="d45c6-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span><span class="sxs-lookup"><span data-stu-id="d45c6-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="d45c6-134">Use the scope parameter, for example:</span><span class="sxs-lookup"><span data-stu-id="d45c6-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="d45c6-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span><span class="sxs-lookup"><span data-stu-id="d45c6-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="d45c6-136">For instance, registration is failing.</span><span class="sxs-lookup"><span data-stu-id="d45c6-136">For instance, registration is failing.</span></span> <span data-ttu-id="d45c6-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span><span class="sxs-lookup"><span data-stu-id="d45c6-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="d45c6-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="d45c6-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="d45c6-139">We recommend that you run this tool and capture the output of this tool.</span><span class="sxs-lookup"><span data-stu-id="d45c6-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="d45c6-140">You can then provide this output to Support to expedite troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="d45c6-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="d45c6-141">If there are any hardware component or cluster failures, you should log in a Support request.</span><span class="sxs-lookup"><span data-stu-id="d45c6-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="d45c6-142">**Low device performance** - Your StorSimple device is slow.</span><span class="sxs-lookup"><span data-stu-id="d45c6-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="d45c6-143">In this case, run this cmdlet with scope parameter set to performance.</span><span class="sxs-lookup"><span data-stu-id="d45c6-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="d45c6-144">Analyze the output.</span><span class="sxs-lookup"><span data-stu-id="d45c6-144">Analyze the output.</span></span> <span data-ttu-id="d45c6-145">You get the cloud read-write latencies.</span><span class="sxs-lookup"><span data-stu-id="d45c6-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="d45c6-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span><span class="sxs-lookup"><span data-stu-id="d45c6-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="d45c6-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span><span class="sxs-lookup"><span data-stu-id="d45c6-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="d45c6-148">Diagnostics test and sample outputs</span><span class="sxs-lookup"><span data-stu-id="d45c6-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="d45c6-149">Hardware test</span><span class="sxs-lookup"><span data-stu-id="d45c6-149">Hardware test</span></span>

<span data-ttu-id="d45c6-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span><span class="sxs-lookup"><span data-stu-id="d45c6-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="d45c6-151">The hardware components reported are those components that failed the test or are not present in the system.</span><span class="sxs-lookup"><span data-stu-id="d45c6-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="d45c6-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span><span class="sxs-lookup"><span data-stu-id="d45c6-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="d45c6-153">For a complete list of hardware components, go to:</span><span class="sxs-lookup"><span data-stu-id="d45c6-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="d45c6-154">Components in primary enclosure</span><span class="sxs-lookup"><span data-stu-id="d45c6-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="d45c6-155">Components in EBOD enclosure</span><span class="sxs-lookup"><span data-stu-id="d45c6-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="d45c6-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d45c6-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="d45c6-157">Sample output of hardware test run on an 8100 device</span><span class="sxs-lookup"><span data-stu-id="d45c6-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="d45c6-158">Here is a sample output from a StorSimple 8100 device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="d45c6-159">In the 8100 model device, the EBOD enclosure is not present.</span><span class="sxs-lookup"><span data-stu-id="d45c6-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="d45c6-160">Hence, the EBOD controller components are not reported.</span><span class="sxs-lookup"><span data-stu-id="d45c6-160">Hence, the EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="d45c6-161">System test</span><span class="sxs-lookup"><span data-stu-id="d45c6-161">System test</span></span>

<span data-ttu-id="d45c6-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="d45c6-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span><span class="sxs-lookup"><span data-stu-id="d45c6-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="d45c6-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="d45c6-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="d45c6-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span><span class="sxs-lookup"><span data-stu-id="d45c6-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="d45c6-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span><span class="sxs-lookup"><span data-stu-id="d45c6-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="d45c6-167">Your device is up-to-date.</span><span class="sxs-lookup"><span data-stu-id="d45c6-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="d45c6-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span><span class="sxs-lookup"><span data-stu-id="d45c6-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="d45c6-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d45c6-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="d45c6-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="d45c6-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span><span class="sxs-lookup"><span data-stu-id="d45c6-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="d45c6-172">Sample output of system test run on an 8100 device</span><span class="sxs-lookup"><span data-stu-id="d45c6-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="d45c6-173">Here is a sample output of the system test run on an 8100 device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-173">Here is a sample output of the system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="d45c6-174">Network test</span><span class="sxs-lookup"><span data-stu-id="d45c6-174">Network test</span></span>

<span data-ttu-id="d45c6-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="d45c6-176">Sample output of network test when only DATA0 is enabled</span><span class="sxs-lookup"><span data-stu-id="d45c6-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="d45c6-177">Here is a sample output of the 8100 device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="d45c6-178">You can see in the output that:</span><span class="sxs-lookup"><span data-stu-id="d45c6-178">You can see in the output that:</span></span>
* <span data-ttu-id="d45c6-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span><span class="sxs-lookup"><span data-stu-id="d45c6-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="d45c6-180">DATA 2 - 5 are not enabled in the portal.</span><span class="sxs-lookup"><span data-stu-id="d45c6-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="d45c6-181">The DNS server configuration is valid and the device can connect via the DNS server.</span><span class="sxs-lookup"><span data-stu-id="d45c6-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="d45c6-182">The NTP server connectivity is also fine.</span><span class="sxs-lookup"><span data-stu-id="d45c6-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="d45c6-183">Ports 80 and 443 are open.</span><span class="sxs-lookup"><span data-stu-id="d45c6-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="d45c6-184">However, port 9354 is blocked.</span><span class="sxs-lookup"><span data-stu-id="d45c6-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="d45c6-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span><span class="sxs-lookup"><span data-stu-id="d45c6-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="d45c6-186">The SSL certification is valid.</span><span class="sxs-lookup"><span data-stu-id="d45c6-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="d45c6-187">The device can connect to the storage account: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="d45c6-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="d45c6-188">The connectivity to Update servers is valid.</span><span class="sxs-lookup"><span data-stu-id="d45c6-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="d45c6-189">The web proxy is not configured on this device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="d45c6-190">Sample output of network test when DATA0 and DATA1 are enabled</span><span class="sxs-lookup"><span data-stu-id="d45c6-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="d45c6-191">Performance test</span><span class="sxs-lookup"><span data-stu-id="d45c6-191">Performance test</span></span>

<span data-ttu-id="d45c6-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="d45c6-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d45c6-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="d45c6-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span><span class="sxs-lookup"><span data-stu-id="d45c6-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="d45c6-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span><span class="sxs-lookup"><span data-stu-id="d45c6-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="d45c6-196">The test simulates the blob sizes associated with the different volume types on the device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="d45c6-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span><span class="sxs-lookup"><span data-stu-id="d45c6-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="d45c6-198">Tiered volumes with archive option checked use 512 KB blob data size.</span><span class="sxs-lookup"><span data-stu-id="d45c6-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="d45c6-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span><span class="sxs-lookup"><span data-stu-id="d45c6-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="d45c6-200">To use this tool, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d45c6-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="d45c6-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span><span class="sxs-lookup"><span data-stu-id="d45c6-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="d45c6-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span><span class="sxs-lookup"><span data-stu-id="d45c6-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="d45c6-203">Run the cmdlet after you have created and configured the volumes.</span><span class="sxs-lookup"><span data-stu-id="d45c6-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="d45c6-204">Type:</span><span class="sxs-lookup"><span data-stu-id="d45c6-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="d45c6-205">Make a note of the read-write latencies reported by the tool.</span><span class="sxs-lookup"><span data-stu-id="d45c6-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="d45c6-206">This test can take several minutes to run before it reports the results.</span><span class="sxs-lookup"><span data-stu-id="d45c6-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="d45c6-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span><span class="sxs-lookup"><span data-stu-id="d45c6-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="d45c6-208">Factor in some overhead for internal data processing.</span><span class="sxs-lookup"><span data-stu-id="d45c6-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="d45c6-209">If the read-write latencies reported by the diagnostics tool are high:</span><span class="sxs-lookup"><span data-stu-id="d45c6-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="d45c6-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="d45c6-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="d45c6-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/storage-enable-and-view-metrics-classic-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d45c6-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/storage-enable-and-view-metrics-classic-portal.md).</span></span> <span data-ttu-id="d45c6-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span><span class="sxs-lookup"><span data-stu-id="d45c6-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="d45c6-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span><span class="sxs-lookup"><span data-stu-id="d45c6-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="d45c6-214">Sample output of performance test run on an 8100 device</span><span class="sxs-lookup"><span data-stu-id="d45c6-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="d45c6-215">Appendix: interpreting system information</span><span class="sxs-lookup"><span data-stu-id="d45c6-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="d45c6-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span><span class="sxs-lookup"><span data-stu-id="d45c6-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="d45c6-217">PowerShell Parameter</span><span class="sxs-lookup"><span data-stu-id="d45c6-217">PowerShell Parameter</span></span>    | <span data-ttu-id="d45c6-218">Description</span><span class="sxs-lookup"><span data-stu-id="d45c6-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="d45c6-219">Instance ID</span><span class="sxs-lookup"><span data-stu-id="d45c6-219">Instance ID</span></span>             | <span data-ttu-id="d45c6-220">Every controller has a unique identifier or a GUID associated with it.</span><span class="sxs-lookup"><span data-stu-id="d45c6-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="d45c6-221">Name</span><span class="sxs-lookup"><span data-stu-id="d45c6-221">Name</span></span>                    | <span data-ttu-id="d45c6-222">The friendly name of the device as configured through the Azure portal during device deployment.</span><span class="sxs-lookup"><span data-stu-id="d45c6-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="d45c6-223">The default friendly name is the device serial number.</span><span class="sxs-lookup"><span data-stu-id="d45c6-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="d45c6-224">Model</span><span class="sxs-lookup"><span data-stu-id="d45c6-224">Model</span></span>                   | <span data-ttu-id="d45c6-225">The model of your StorSimple 8000 series device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="d45c6-226">The model can be 8100 or 8600.</span><span class="sxs-lookup"><span data-stu-id="d45c6-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="d45c6-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="d45c6-227">SerialNumber</span></span>            | <span data-ttu-id="d45c6-228">The device serial number is assigned at the factory and is 15 characters long.</span><span class="sxs-lookup"><span data-stu-id="d45c6-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="d45c6-229">For instance, 8600-SHX0991003G44HT indicates:</span><span class="sxs-lookup"><span data-stu-id="d45c6-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="d45c6-230">8600 – Is the device model.</span><span class="sxs-lookup"><span data-stu-id="d45c6-230">8600 – Is the device model.</span></span><br><span data-ttu-id="d45c6-231">SHX – Is the manufacturing site.</span><span class="sxs-lookup"><span data-stu-id="d45c6-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="d45c6-232">0991003 - Is a specific product.</span><span class="sxs-lookup"><span data-stu-id="d45c6-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="d45c6-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span><span class="sxs-lookup"><span data-stu-id="d45c6-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="d45c6-234">This may not be a sequential set.</span><span class="sxs-lookup"><span data-stu-id="d45c6-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="d45c6-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="d45c6-235">TimeZone</span></span>                | <span data-ttu-id="d45c6-236">The device time zone as configured in the Azure portal during device deployment.</span><span class="sxs-lookup"><span data-stu-id="d45c6-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="d45c6-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="d45c6-237">CurrentController</span></span>       | <span data-ttu-id="d45c6-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="d45c6-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="d45c6-239">ActiveController</span></span>        | <span data-ttu-id="d45c6-240">The controller that is active on your device and is controlling all the network and disk operations.</span><span class="sxs-lookup"><span data-stu-id="d45c6-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="d45c6-241">This can be Controller 0 or Controller 1.</span><span class="sxs-lookup"><span data-stu-id="d45c6-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="d45c6-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="d45c6-242">Controller0Status</span></span>       | <span data-ttu-id="d45c6-243">The status of Controller 0 on your device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="d45c6-244">The controller status can be normal, in recovery mode, or unreachable.</span><span class="sxs-lookup"><span data-stu-id="d45c6-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="d45c6-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="d45c6-245">Controller1Status</span></span>       | <span data-ttu-id="d45c6-246">The status of Controller 1 on your device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="d45c6-247">The controller status can be normal, in recovery mode, or unreachable.</span><span class="sxs-lookup"><span data-stu-id="d45c6-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="d45c6-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="d45c6-248">SystemMode</span></span>              | <span data-ttu-id="d45c6-249">The overall status of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="d45c6-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="d45c6-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="d45c6-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="d45c6-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="d45c6-252">The friendly string that corresponds to the device software version.</span><span class="sxs-lookup"><span data-stu-id="d45c6-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="d45c6-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="d45c6-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="d45c6-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="d45c6-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="d45c6-255">The HCS software version running on your device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-255">The HCS software version running on your device.</span></span> <span data-ttu-id="d45c6-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="d45c6-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="d45c6-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="d45c6-257">ApiVersion</span></span>              | <span data-ttu-id="d45c6-258">The software version of the Windows PowerShell API of the HCS device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="d45c6-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="d45c6-259">VhdVersion</span></span>              | <span data-ttu-id="d45c6-260">The software version of the factory image that the device was shipped with.</span><span class="sxs-lookup"><span data-stu-id="d45c6-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="d45c6-261">If you reset your device to factory defaults, then it runs this software version.</span><span class="sxs-lookup"><span data-stu-id="d45c6-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="d45c6-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="d45c6-262">OSVersion</span></span>               | <span data-ttu-id="d45c6-263">The software version of the Windows Server operating system running on the device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="d45c6-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span><span class="sxs-lookup"><span data-stu-id="d45c6-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="d45c6-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="d45c6-265">CisAgentVersion</span></span>         | <span data-ttu-id="d45c6-266">The version for your Cis agent running on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="d45c6-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span><span class="sxs-lookup"><span data-stu-id="d45c6-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="d45c6-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="d45c6-268">MdsAgentVersion</span></span>         | <span data-ttu-id="d45c6-269">The version corresponding to the Mds agent running on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="d45c6-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span><span class="sxs-lookup"><span data-stu-id="d45c6-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="d45c6-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="d45c6-271">Lsisas2Version</span></span>          | <span data-ttu-id="d45c6-272">The version corresponding to the LSI drivers on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="d45c6-273">Capacity</span><span class="sxs-lookup"><span data-stu-id="d45c6-273">Capacity</span></span>                | <span data-ttu-id="d45c6-274">The total capacity of the device in bytes.</span><span class="sxs-lookup"><span data-stu-id="d45c6-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="d45c6-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="d45c6-275">RemoteManagementMode</span></span>    | <span data-ttu-id="d45c6-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span><span class="sxs-lookup"><span data-stu-id="d45c6-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="d45c6-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="d45c6-277">FipsMode</span></span>                | <span data-ttu-id="d45c6-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="d45c6-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span><span class="sxs-lookup"><span data-stu-id="d45c6-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="d45c6-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="d45c6-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d45c6-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="d45c6-281">Next steps</span></span>

* <span data-ttu-id="d45c6-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="d45c6-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="d45c6-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d45c6-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
