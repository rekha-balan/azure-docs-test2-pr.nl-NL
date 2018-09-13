---
title: Configure MPIO on StorSimple Linux host| Microsoft Docs
description: Configure MPIO on StorSimple connected to a Linux host running CentOS 6.6
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: fec1b3ad794d7bcfa9564076e25fb78030b71c0e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554725"
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="3102d-103">Configure MPIO on a StorSimple host running CentOS</span><span class="sxs-lookup"><span data-stu-id="3102d-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="3102d-104">This article explains the steps required to configure Multipathing IO (MPIO) on your Centos 6.6 host server.</span><span class="sxs-lookup"><span data-stu-id="3102d-104">This article explains the steps required to configure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="3102d-105">The host server is connected to your Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span><span class="sxs-lookup"><span data-stu-id="3102d-105">The host server is connected to your Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="3102d-106">It describes in detail the automatic discovery of multipath devices and the specific setup only for StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="3102d-106">It describes in detail the automatic discovery of multipath devices and the specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="3102d-107">This procedure is applicable to all the models of StorSimple 8000 series devices.</span><span class="sxs-lookup"><span data-stu-id="3102d-107">This procedure is applicable to all the models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="3102d-108">This procedure cannot be used for a StorSimple virtual device.</span><span class="sxs-lookup"><span data-stu-id="3102d-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="3102d-109">For more information, see how to configure host servers for your virtual device.</span><span class="sxs-lookup"><span data-stu-id="3102d-109">For more information, see how to configure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="3102d-110">About multipathing</span><span class="sxs-lookup"><span data-stu-id="3102d-110">About multipathing</span></span>
<span data-ttu-id="3102d-111">The multipathing feature allows you to configure multiple I/O paths between a host server and a storage device.</span><span class="sxs-lookup"><span data-stu-id="3102d-111">The multipathing feature allows you to configure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="3102d-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span><span class="sxs-lookup"><span data-stu-id="3102d-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="3102d-113">Multipathing aggregates the I/O paths, to configure a new device that is associated with all of the aggregated paths.</span><span class="sxs-lookup"><span data-stu-id="3102d-113">Multipathing aggregates the I/O paths, to configure a new device that is associated with all of the aggregated paths.</span></span>

<span data-ttu-id="3102d-114">The purpose of multipathing is two-fold:</span><span class="sxs-lookup"><span data-stu-id="3102d-114">The purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="3102d-115">**High availability**: It provides an alternate path if any element of the I/O path (such as a cable, switch, network interface, or controller) fails.</span><span class="sxs-lookup"><span data-stu-id="3102d-115">**High availability**: It provides an alternate path if any element of the I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="3102d-116">**Load balancing**: Depending on the configuration of your storage device, it can improve the performance by detecting loads on the I/O paths and dynamically rebalancing those loads.</span><span class="sxs-lookup"><span data-stu-id="3102d-116">**Load balancing**: Depending on the configuration of your storage device, it can improve the performance by detecting loads on the I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="3102d-117">About multipathing components</span><span class="sxs-lookup"><span data-stu-id="3102d-117">About multipathing components</span></span>
<span data-ttu-id="3102d-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span><span class="sxs-lookup"><span data-stu-id="3102d-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="3102d-119">**Kernel**: The main component is the *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span><span class="sxs-lookup"><span data-stu-id="3102d-119">**Kernel**: The main component is the *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="3102d-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing the device-mapper multipath module what to do.</span><span class="sxs-lookup"><span data-stu-id="3102d-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing the device-mapper multipath module what to do.</span></span> <span data-ttu-id="3102d-121">The tools consist of:</span><span class="sxs-lookup"><span data-stu-id="3102d-121">The tools consist of:</span></span>
   
   * <span data-ttu-id="3102d-122">**Multipath**: lists and configures multipathed devices.</span><span class="sxs-lookup"><span data-stu-id="3102d-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="3102d-123">**Multipathd**: daemon that executes multipath and monitors the paths.</span><span class="sxs-lookup"><span data-stu-id="3102d-123">**Multipathd**: daemon that executes multipath and monitors the paths.</span></span>
   * <span data-ttu-id="3102d-124">**Devmap-name**: provides a meaningful device-name to udev for devmaps.</span><span class="sxs-lookup"><span data-stu-id="3102d-124">**Devmap-name**: provides a meaningful device-name to udev for devmaps.</span></span>
   * <span data-ttu-id="3102d-125">**Kpartx**: maps linear devmaps to device partitions to make multipath maps partitionable.</span><span class="sxs-lookup"><span data-stu-id="3102d-125">**Kpartx**: maps linear devmaps to device partitions to make multipath maps partitionable.</span></span>
   * <span data-ttu-id="3102d-126">**Multipath.conf**: configuration file for multipath daemon that is used to overwrite the built-in configuration table.</span><span class="sxs-lookup"><span data-stu-id="3102d-126">**Multipath.conf**: configuration file for multipath daemon that is used to overwrite the built-in configuration table.</span></span>

### <a name="about-the-multipathconf-configuration-file"></a><span data-ttu-id="3102d-127">About the multipath.conf configuration file</span><span class="sxs-lookup"><span data-stu-id="3102d-127">About the multipath.conf configuration file</span></span>
<span data-ttu-id="3102d-128">The configuration file `/etc/multipath.conf` makes many of the multipathing features user-configurable.</span><span class="sxs-lookup"><span data-stu-id="3102d-128">The configuration file `/etc/multipath.conf` makes many of the multipathing features user-configurable.</span></span> <span data-ttu-id="3102d-129">The `multipath` command and the kernel daemon `multipathd` use information found in this file.</span><span class="sxs-lookup"><span data-stu-id="3102d-129">The `multipath` command and the kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="3102d-130">The file is consulted only during the configuration of the multipath devices.</span><span class="sxs-lookup"><span data-stu-id="3102d-130">The file is consulted only during the configuration of the multipath devices.</span></span> <span data-ttu-id="3102d-131">Make sure that all changes are made before you run the `multipath` command.</span><span class="sxs-lookup"><span data-stu-id="3102d-131">Make sure that all changes are made before you run the `multipath` command.</span></span> <span data-ttu-id="3102d-132">If you modify the file afterwards, you will need to stop and start multipathd again for the changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="3102d-132">If you modify the file afterwards, you will need to stop and start multipathd again for the changes to take effect.</span></span>

<span data-ttu-id="3102d-133">The multipath.conf has five sections:</span><span class="sxs-lookup"><span data-stu-id="3102d-133">The multipath.conf has five sections:</span></span>

- <span data-ttu-id="3102d-134">**System level defaults** *(defaults)*: You can override system level defaults.</span><span class="sxs-lookup"><span data-stu-id="3102d-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="3102d-135">**Blacklisted devices** *(blacklist)*: You can specify the list of devices that should not be controlled by device-mapper.</span><span class="sxs-lookup"><span data-stu-id="3102d-135">**Blacklisted devices** *(blacklist)*: You can specify the list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="3102d-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices to be treated as multipath devices even if listed in the blacklist.</span><span class="sxs-lookup"><span data-stu-id="3102d-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices to be treated as multipath devices even if listed in the blacklist.</span></span>
- <span data-ttu-id="3102d-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied to devices that have Vendor and Product information.</span><span class="sxs-lookup"><span data-stu-id="3102d-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied to devices that have Vendor and Product information.</span></span>
- <span data-ttu-id="3102d-138">**Device specific settings** *(multipaths)*: You can use this section to fine-tune the configuration settings for individual LUNs.</span><span class="sxs-lookup"><span data-stu-id="3102d-138">**Device specific settings** *(multipaths)*: You can use this section to fine-tune the configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-to-linux-host"></a><span data-ttu-id="3102d-139">Configure multipathing on StorSimple connected to Linux host</span><span class="sxs-lookup"><span data-stu-id="3102d-139">Configure multipathing on StorSimple connected to Linux host</span></span>
<span data-ttu-id="3102d-140">A StorSimple device connected to a Linux host can be configured for high availability and load balancing.</span><span class="sxs-lookup"><span data-stu-id="3102d-140">A StorSimple device connected to a Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="3102d-141">For example, if the Linux host has two interfaces connected to the SAN and the device has two interfaces connected to the SAN such that these interfaces are on the same subnet, then there will be 4 paths available.</span><span class="sxs-lookup"><span data-stu-id="3102d-141">For example, if the Linux host has two interfaces connected to the SAN and the device has two interfaces connected to the SAN such that these interfaces are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="3102d-142">However, if each DATA interface on the device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span><span class="sxs-lookup"><span data-stu-id="3102d-142">However, if each DATA interface on the device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="3102d-143">You can configure multipathing to automatically discover all the available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span><span class="sxs-lookup"><span data-stu-id="3102d-143">You can configure multipathing to automatically discover all the available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="3102d-144">The following procedure describes how to configure multipathing when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span><span class="sxs-lookup"><span data-stu-id="3102d-144">The following procedure describes how to configure multipathing when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3102d-145">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3102d-145">Prerequisites</span></span>
<span data-ttu-id="3102d-146">This section details the configuration prerequisites for CentOS server and your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-146">This section details the configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="3102d-147">On CentOS host</span><span class="sxs-lookup"><span data-stu-id="3102d-147">On CentOS host</span></span>
1. <span data-ttu-id="3102d-148">Make sure that your CentOS host has 2 network interfaces enabled.</span><span class="sxs-lookup"><span data-stu-id="3102d-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="3102d-149">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="3102d-150">The following example shows the output when two network interfaces (`eth0` and `eth1`) are present on the host.</span><span class="sxs-lookup"><span data-stu-id="3102d-150">The following example shows the output when two network interfaces (`eth0` and `eth1`) are present on the host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="3102d-151">Install *iSCSI-initiator-utils* on your CentOS server.</span><span class="sxs-lookup"><span data-stu-id="3102d-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="3102d-152">Perform the following steps to install *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="3102d-152">Perform the following steps to install *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="3102d-153">Log on as `root` into your CentOS host.</span><span class="sxs-lookup"><span data-stu-id="3102d-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="3102d-154">Install the *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="3102d-154">Install the *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="3102d-155">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="3102d-156">After the *iSCSI-Initiator-utils* is successfully installed, start the iSCSI service.</span><span class="sxs-lookup"><span data-stu-id="3102d-156">After the *iSCSI-Initiator-utils* is successfully installed, start the iSCSI service.</span></span> <span data-ttu-id="3102d-157">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="3102d-158">On occasions, `iscsid` may not actually start and the `--force` option may be needed</span><span class="sxs-lookup"><span data-stu-id="3102d-158">On occasions, `iscsid` may not actually start and the `--force` option may be needed</span></span>
   4. <span data-ttu-id="3102d-159">To ensure that your iSCSI initiator is enabled during boot time, use the `chkconfig` command to enable the service.</span><span class="sxs-lookup"><span data-stu-id="3102d-159">To ensure that your iSCSI initiator is enabled during boot time, use the `chkconfig` command to enable the service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="3102d-160">To verify that that it was properly setup, run the command:</span><span class="sxs-lookup"><span data-stu-id="3102d-160">To verify that that it was properly setup, run the command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="3102d-161">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="3102d-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="3102d-162">From the above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span><span class="sxs-lookup"><span data-stu-id="3102d-162">From the above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="3102d-163">Install *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="3102d-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="3102d-164">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="3102d-165">The installation will start.</span><span class="sxs-lookup"><span data-stu-id="3102d-165">The installation will start.</span></span> <span data-ttu-id="3102d-166">Type **Y** to continue when prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="3102d-166">Type **Y** to continue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="3102d-167">On StorSimple device</span><span class="sxs-lookup"><span data-stu-id="3102d-167">On StorSimple device</span></span>
<span data-ttu-id="3102d-168">Your StorSimple device should have:</span><span class="sxs-lookup"><span data-stu-id="3102d-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="3102d-169">A minimum of two interfaces enabled for iSCSI.</span><span class="sxs-lookup"><span data-stu-id="3102d-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="3102d-170">To verify that two interfaces are iSCSI-enabled on your StorSimple device, perform the following steps in the Azure classic portal for your StorSimple device:</span><span class="sxs-lookup"><span data-stu-id="3102d-170">To verify that two interfaces are iSCSI-enabled on your StorSimple device, perform the following steps in the Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="3102d-171">Log into the classic portal for your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-171">Log into the classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="3102d-172">Select your StorSimple Manager service, click **Devices** and choose the specific StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-172">Select your StorSimple Manager service, click **Devices** and choose the specific StorSimple device.</span></span> <span data-ttu-id="3102d-173">Click **Configure** and verify the network interface settings.</span><span class="sxs-lookup"><span data-stu-id="3102d-173">Click **Configure** and verify the network interface settings.</span></span> <span data-ttu-id="3102d-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span><span class="sxs-lookup"><span data-stu-id="3102d-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="3102d-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span><span class="sxs-lookup"><span data-stu-id="3102d-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![MPIO StorsSimple DATA 2 config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple DATA 3 Config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="3102d-178">In the **Configure** page</span><span class="sxs-lookup"><span data-stu-id="3102d-178">In the **Configure** page</span></span>
     
     1. <span data-ttu-id="3102d-179">Ensure that both network interfaces are iSCSI-enabled.</span><span class="sxs-lookup"><span data-stu-id="3102d-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="3102d-180">The **iSCSI enabled** field should be set to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="3102d-180">The **iSCSI enabled** field should be set to **Yes**.</span></span>
     2. <span data-ttu-id="3102d-181">Ensure that the network interfaces have the same speed, both should be 1 GbE or 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="3102d-181">Ensure that the network interfaces have the same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="3102d-182">Note the IPv4 addresses of the iSCSI-enabled interfaces and save for later use on the host.</span><span class="sxs-lookup"><span data-stu-id="3102d-182">Note the IPv4 addresses of the iSCSI-enabled interfaces and save for later use on the host.</span></span>
* <span data-ttu-id="3102d-183">The iSCSI interfaces on your StorSimple device should be reachable from the CentOS server.</span><span class="sxs-lookup"><span data-stu-id="3102d-183">The iSCSI interfaces on your StorSimple device should be reachable from the CentOS server.</span></span>
      <span data-ttu-id="3102d-184">To verify this, you need to provide the IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span><span class="sxs-lookup"><span data-stu-id="3102d-184">To verify this, you need to provide the IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="3102d-185">The commands used and the corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span><span class="sxs-lookup"><span data-stu-id="3102d-185">The commands used and the corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="3102d-186">Hardware configuration</span><span class="sxs-lookup"><span data-stu-id="3102d-186">Hardware configuration</span></span>
<span data-ttu-id="3102d-187">We recommend that you connect the two iSCSI network interfaces on separate paths for redundancy.</span><span class="sxs-lookup"><span data-stu-id="3102d-187">We recommend that you connect the two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="3102d-188">The figure below shows the recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-188">The figure below shows the recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![MPIO hardware config for StorSimple to Linux host](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="3102d-190">As shown in the preceding figure:</span><span class="sxs-lookup"><span data-stu-id="3102d-190">As shown in the preceding figure:</span></span>

* <span data-ttu-id="3102d-191">Your StorSimple device is in an active-passive configuration with two controllers.</span><span class="sxs-lookup"><span data-stu-id="3102d-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="3102d-192">Two SAN switches are connected to your device controllers.</span><span class="sxs-lookup"><span data-stu-id="3102d-192">Two SAN switches are connected to your device controllers.</span></span>
* <span data-ttu-id="3102d-193">Two iSCSI initiators are enabled on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="3102d-194">Two network interfaces are enabled on your CentOS host.</span><span class="sxs-lookup"><span data-stu-id="3102d-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="3102d-195">The above configuration will yield 4 separate paths between your device and the host if the host and data interfaces are routable.</span><span class="sxs-lookup"><span data-stu-id="3102d-195">The above configuration will yield 4 separate paths between your device and the host if the host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="3102d-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span><span class="sxs-lookup"><span data-stu-id="3102d-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="3102d-197">When using two network interfaces, both the interfaces should be the identical type.</span><span class="sxs-lookup"><span data-stu-id="3102d-197">When using two network interfaces, both the interfaces should be the identical type.</span></span>
> * <span data-ttu-id="3102d-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span><span class="sxs-lookup"><span data-stu-id="3102d-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="3102d-199">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="3102d-199">Configuration steps</span></span>
<span data-ttu-id="3102d-200">The configuration steps for multipathing involve configuring the available paths for automatic discovery, specifying the load-balancing algorithm to use, enabling multipathing and finally verifying the configuration.</span><span class="sxs-lookup"><span data-stu-id="3102d-200">The configuration steps for multipathing involve configuring the available paths for automatic discovery, specifying the load-balancing algorithm to use, enabling multipathing and finally verifying the configuration.</span></span> <span data-ttu-id="3102d-201">Each of these steps is discussed in detail in the following sections.</span><span class="sxs-lookup"><span data-stu-id="3102d-201">Each of these steps is discussed in detail in the following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="3102d-202">Step 1: Configure multipathing for automatic discovery</span><span class="sxs-lookup"><span data-stu-id="3102d-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="3102d-203">The multipath-supported devices can be automatically discovered and configured.</span><span class="sxs-lookup"><span data-stu-id="3102d-203">The multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="3102d-204">Initialize `/etc/multipath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="3102d-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="3102d-205">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="3102d-206">The above command will create a `sample/etc/multipath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="3102d-206">The above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="3102d-207">Start multipath service.</span><span class="sxs-lookup"><span data-stu-id="3102d-207">Start multipath service.</span></span> <span data-ttu-id="3102d-208">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="3102d-209">You will see the following output:</span><span class="sxs-lookup"><span data-stu-id="3102d-209">You will see the following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="3102d-210">Enable automatic discovery of multipaths.</span><span class="sxs-lookup"><span data-stu-id="3102d-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="3102d-211">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="3102d-212">This will modify the defaults section of your `multipath.conf` as shown below:</span><span class="sxs-lookup"><span data-stu-id="3102d-212">This will modify the defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="3102d-213">Step 2: Configure multipathing for StorSimple volumes</span><span class="sxs-lookup"><span data-stu-id="3102d-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="3102d-214">By default, all devices are black listed in the multipath.conf file and will be bypassed.</span><span class="sxs-lookup"><span data-stu-id="3102d-214">By default, all devices are black listed in the multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="3102d-215">You will need to create blacklist exceptions to allow multipathing for volumes from StorSimple devices.</span><span class="sxs-lookup"><span data-stu-id="3102d-215">You will need to create blacklist exceptions to allow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="3102d-216">Edit the `/etc/mulitpath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="3102d-216">Edit the `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="3102d-217">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="3102d-218">Locate the blacklist_exceptions section in the multipath.conf file.</span><span class="sxs-lookup"><span data-stu-id="3102d-218">Locate the blacklist_exceptions section in the multipath.conf file.</span></span> <span data-ttu-id="3102d-219">Your StorSimple device needs to be listed as a blacklist exception in this section.</span><span class="sxs-lookup"><span data-stu-id="3102d-219">Your StorSimple device needs to be listed as a blacklist exception in this section.</span></span> <span data-ttu-id="3102d-220">You can uncomment relevant lines in this file to modify it as shown below (use only the specific model of the device you are using):</span><span class="sxs-lookup"><span data-stu-id="3102d-220">You can uncomment relevant lines in this file to modify it as shown below (use only the specific model of the device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="3102d-221">Step 3: Configure round-robin multipathing</span><span class="sxs-lookup"><span data-stu-id="3102d-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="3102d-222">This load-balancing algorithm uses all the available multipaths to the active controller in a balanced, round-robin fashion.</span><span class="sxs-lookup"><span data-stu-id="3102d-222">This load-balancing algorithm uses all the available multipaths to the active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="3102d-223">Edit the `/etc/multipath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="3102d-223">Edit the `/etc/multipath.conf` file.</span></span> <span data-ttu-id="3102d-224">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="3102d-225">Under the `defaults` section, set the `path_grouping_policy` to `multibus`.</span><span class="sxs-lookup"><span data-stu-id="3102d-225">Under the `defaults` section, set the `path_grouping_policy` to `multibus`.</span></span> <span data-ttu-id="3102d-226">The `path_grouping_policy` specifies the default path grouping policy to apply to unspecified multipaths.</span><span class="sxs-lookup"><span data-stu-id="3102d-226">The `path_grouping_policy` specifies the default path grouping policy to apply to unspecified multipaths.</span></span> <span data-ttu-id="3102d-227">The defaults section will look as shown below.</span><span class="sxs-lookup"><span data-stu-id="3102d-227">The defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="3102d-228">The most common values of `path_grouping_policy` include:</span><span class="sxs-lookup"><span data-stu-id="3102d-228">The most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="3102d-229">failover = 1 path per priority group</span><span class="sxs-lookup"><span data-stu-id="3102d-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="3102d-230">multibus = all valid paths in 1 priority group</span><span class="sxs-lookup"><span data-stu-id="3102d-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="3102d-231">Step 4: Enable multipathing</span><span class="sxs-lookup"><span data-stu-id="3102d-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="3102d-232">Restart the `multipathd` daemon.</span><span class="sxs-lookup"><span data-stu-id="3102d-232">Restart the `multipathd` daemon.</span></span> <span data-ttu-id="3102d-233">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="3102d-234">The output will be as shown below:</span><span class="sxs-lookup"><span data-stu-id="3102d-234">The output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="3102d-235">Step 5: Verify multipathing</span><span class="sxs-lookup"><span data-stu-id="3102d-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="3102d-236">First make sure that iSCSI connection is established with the StorSimple device as follows:</span><span class="sxs-lookup"><span data-stu-id="3102d-236">First make sure that iSCSI connection is established with the StorSimple device as follows:</span></span>
   
   <span data-ttu-id="3102d-237">a.</span><span class="sxs-lookup"><span data-stu-id="3102d-237">a.</span></span> <span data-ttu-id="3102d-238">Discover your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-238">Discover your StorSimple device.</span></span> <span data-ttu-id="3102d-239">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on the device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="3102d-240">The output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on the StorSimple device for outbound iSCSI traffic is as shown below:</span><span class="sxs-lookup"><span data-stu-id="3102d-240">The output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on the StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="3102d-241">Copy the IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from the preceding output.</span><span class="sxs-lookup"><span data-stu-id="3102d-241">Copy the IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from the preceding output.</span></span>

   <span data-ttu-id="3102d-242">b.</span><span class="sxs-lookup"><span data-stu-id="3102d-242">b.</span></span> <span data-ttu-id="3102d-243">Connect to the device using target IQN.</span><span class="sxs-lookup"><span data-stu-id="3102d-243">Connect to the device using target IQN.</span></span> <span data-ttu-id="3102d-244">The StorSimple device is the iSCSI target here.</span><span class="sxs-lookup"><span data-stu-id="3102d-244">The StorSimple device is the iSCSI target here.</span></span> <span data-ttu-id="3102d-245">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="3102d-246">The following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="3102d-246">The following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="3102d-247">The output indicates that you have successfully connected to the two iSCSI-enabled network interfaces on your device.</span><span class="sxs-lookup"><span data-stu-id="3102d-247">The output indicates that you have successfully connected to the two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="3102d-248">If you see only one host interface and two paths here, then you need to enable both the interfaces on host for iSCSI.</span><span class="sxs-lookup"><span data-stu-id="3102d-248">If you see only one host interface and two paths here, then you need to enable both the interfaces on host for iSCSI.</span></span> <span data-ttu-id="3102d-249">You can follow the [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="3102d-249">You can follow the [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="3102d-250">A volume is exposed to the CentOS server from the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-250">A volume is exposed to the CentOS server from the StorSimple device.</span></span> <span data-ttu-id="3102d-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via the Azure classic portal on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via the Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="3102d-252">Verify the available paths.</span><span class="sxs-lookup"><span data-stu-id="3102d-252">Verify the available paths.</span></span> <span data-ttu-id="3102d-253">Type:</span><span class="sxs-lookup"><span data-stu-id="3102d-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="3102d-254">The following example shows the output for two network interfaces on a StorSimple device connected to a single host network interface with two available paths.</span><span class="sxs-lookup"><span data-stu-id="3102d-254">The following example shows the output for two network interfaces on a StorSimple device connected to a single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        The following example shows the output for two network interfaces on a StorSimple device connected to two host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After the paths are configured, refer to the specific instructions on your host operating system (Centos 6.6) to mount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="3102d-255">Troubleshoot multipathing</span><span class="sxs-lookup"><span data-stu-id="3102d-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="3102d-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span><span class="sxs-lookup"><span data-stu-id="3102d-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="3102d-257">Q.</span><span class="sxs-lookup"><span data-stu-id="3102d-257">Q.</span></span> <span data-ttu-id="3102d-258">I do not see the changes in `multipath.conf` file taking effect.</span><span class="sxs-lookup"><span data-stu-id="3102d-258">I do not see the changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="3102d-259">A.</span><span class="sxs-lookup"><span data-stu-id="3102d-259">A.</span></span> <span data-ttu-id="3102d-260">If you have made any changes to the `multipath.conf` file, you will need to restart the multipathing service.</span><span class="sxs-lookup"><span data-stu-id="3102d-260">If you have made any changes to the `multipath.conf` file, you will need to restart the multipathing service.</span></span> <span data-ttu-id="3102d-261">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="3102d-261">Type the following command:</span></span>

    service multipathd restart

<span data-ttu-id="3102d-262">Q.</span><span class="sxs-lookup"><span data-stu-id="3102d-262">Q.</span></span> <span data-ttu-id="3102d-263">I have enabled two network interfaces on the StorSimple device and two network interfaces on the host.</span><span class="sxs-lookup"><span data-stu-id="3102d-263">I have enabled two network interfaces on the StorSimple device and two network interfaces on the host.</span></span> <span data-ttu-id="3102d-264">When I list the available paths, I see only two paths.</span><span class="sxs-lookup"><span data-stu-id="3102d-264">When I list the available paths, I see only two paths.</span></span> <span data-ttu-id="3102d-265">I expected to see four available paths.</span><span class="sxs-lookup"><span data-stu-id="3102d-265">I expected to see four available paths.</span></span>

<span data-ttu-id="3102d-266">A.</span><span class="sxs-lookup"><span data-stu-id="3102d-266">A.</span></span> <span data-ttu-id="3102d-267">Make sure that the two paths are on the same subnet and routable.</span><span class="sxs-lookup"><span data-stu-id="3102d-267">Make sure that the two paths are on the same subnet and routable.</span></span> <span data-ttu-id="3102d-268">If the network interfaces are on different vLANs and not routable, you will see only two paths.</span><span class="sxs-lookup"><span data-stu-id="3102d-268">If the network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="3102d-269">One way to verify this is to make sure that you can reach both the host interfaces from a network interface on the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-269">One way to verify this is to make sure that you can reach both the host interfaces from a network interface on the StorSimple device.</span></span> <span data-ttu-id="3102d-270">You will need to [contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span><span class="sxs-lookup"><span data-stu-id="3102d-270">You will need to [contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="3102d-271">Q.</span><span class="sxs-lookup"><span data-stu-id="3102d-271">Q.</span></span> <span data-ttu-id="3102d-272">When I list available paths, I do not see any output.</span><span class="sxs-lookup"><span data-stu-id="3102d-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="3102d-273">A.</span><span class="sxs-lookup"><span data-stu-id="3102d-273">A.</span></span> <span data-ttu-id="3102d-274">Typically, not seeing any multipathed paths suggests a problem with the multipathing daemon, and it’s most likely that any problem here lies in the `multipath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="3102d-274">Typically, not seeing any multipathed paths suggests a problem with the multipathing daemon, and it’s most likely that any problem here lies in the `multipath.conf` file.</span></span>

<span data-ttu-id="3102d-275">It would also be worth checking that you can actually see some disks after connecting to the target, as no response from the multipath listings could also mean you don’t have any disks.</span><span class="sxs-lookup"><span data-stu-id="3102d-275">It would also be worth checking that you can actually see some disks after connecting to the target, as no response from the multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="3102d-276">Use the following command to rescan the SCSI bus:</span><span class="sxs-lookup"><span data-stu-id="3102d-276">Use the following command to rescan the SCSI bus:</span></span>
  
    <span data-ttu-id="3102d-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span><span class="sxs-lookup"><span data-stu-id="3102d-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="3102d-278">Type the following commands:</span><span class="sxs-lookup"><span data-stu-id="3102d-278">Type the following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="3102d-279">Or</span><span class="sxs-lookup"><span data-stu-id="3102d-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="3102d-280">These will return details of recently added disks.</span><span class="sxs-lookup"><span data-stu-id="3102d-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="3102d-281">To determine whether it is a StorSimple disk, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="3102d-281">To determine whether it is a StorSimple disk, use the following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="3102d-282">This will return a string, which will determine if it’s a StorSimple disk.</span><span class="sxs-lookup"><span data-stu-id="3102d-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="3102d-283">A less likely but possible cause could also be stale iscsid pid.</span><span class="sxs-lookup"><span data-stu-id="3102d-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="3102d-284">Use the following command to log off from the iSCSI sessions:</span><span class="sxs-lookup"><span data-stu-id="3102d-284">Use the following command to log off from the iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="3102d-285">Repeat this command for all the connected network interfaces on the iSCSI target, which is your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="3102d-285">Repeat this command for all the connected network interfaces on the iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="3102d-286">Once you have logged off from all the iSCSI sessions, use the iSCSI target IQN to reestablish the iSCSI session.</span><span class="sxs-lookup"><span data-stu-id="3102d-286">Once you have logged off from all the iSCSI sessions, use the iSCSI target IQN to reestablish the iSCSI session.</span></span> <span data-ttu-id="3102d-287">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="3102d-287">Type the following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="3102d-288">Q.</span><span class="sxs-lookup"><span data-stu-id="3102d-288">Q.</span></span> <span data-ttu-id="3102d-289">I am not sure if my device is whitelisted.</span><span class="sxs-lookup"><span data-stu-id="3102d-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="3102d-290">A.</span><span class="sxs-lookup"><span data-stu-id="3102d-290">A.</span></span> <span data-ttu-id="3102d-291">To verify whether your device is whitelisted, use the following troubleshooting interactive command:</span><span class="sxs-lookup"><span data-stu-id="3102d-291">To verify whether your device is whitelisted, use the following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="3102d-292">For more information, go to [use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="3102d-292">For more information, go to [use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="3102d-293">List of useful commands</span><span class="sxs-lookup"><span data-stu-id="3102d-293">List of useful commands</span></span>
| <span data-ttu-id="3102d-294">Type</span><span class="sxs-lookup"><span data-stu-id="3102d-294">Type</span></span> | <span data-ttu-id="3102d-295">Command</span><span class="sxs-lookup"><span data-stu-id="3102d-295">Command</span></span> | <span data-ttu-id="3102d-296">Description</span><span class="sxs-lookup"><span data-stu-id="3102d-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3102d-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="3102d-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="3102d-298">Start iSCSI service</span><span class="sxs-lookup"><span data-stu-id="3102d-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="3102d-299">Stop iSCSI service</span><span class="sxs-lookup"><span data-stu-id="3102d-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="3102d-300">Restart iSCSI service</span><span class="sxs-lookup"><span data-stu-id="3102d-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="3102d-301">Discover available targets on the specified address</span><span class="sxs-lookup"><span data-stu-id="3102d-301">Discover available targets on the specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="3102d-302">Log in to the iSCSI target</span><span class="sxs-lookup"><span data-stu-id="3102d-302">Log in to the iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="3102d-303">Log out from the iSCSI target</span><span class="sxs-lookup"><span data-stu-id="3102d-303">Log out from the iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="3102d-304">Print iSCSI initiator name</span><span class="sxs-lookup"><span data-stu-id="3102d-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="3102d-305">Check the state of the iSCSI session and volume discovered on the host</span><span class="sxs-lookup"><span data-stu-id="3102d-305">Check the state of the iSCSI session and volume discovered on the host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="3102d-306">Shows all the iSCSI sessions established between the host and the StorSimple device</span><span class="sxs-lookup"><span data-stu-id="3102d-306">Shows all the iSCSI sessions established between the host and the StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="3102d-307">**Multipathing**</span><span class="sxs-lookup"><span data-stu-id="3102d-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="3102d-308">Start multipath daemon</span><span class="sxs-lookup"><span data-stu-id="3102d-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="3102d-309">Stop multipath daemon</span><span class="sxs-lookup"><span data-stu-id="3102d-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="3102d-310">Restart multipath daemon</span><span class="sxs-lookup"><span data-stu-id="3102d-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="3102d-311">OR</span><span class="sxs-lookup"><span data-stu-id="3102d-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="3102d-312">Enable multipath daemon to start at boot time</span><span class="sxs-lookup"><span data-stu-id="3102d-312">Enable multipath daemon to start at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="3102d-313">Start the interactive console for troubleshooting</span><span class="sxs-lookup"><span data-stu-id="3102d-313">Start the interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="3102d-314">List multipath connections and devices</span><span class="sxs-lookup"><span data-stu-id="3102d-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="3102d-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="3102d-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="3102d-316">Next steps</span><span class="sxs-lookup"><span data-stu-id="3102d-316">Next steps</span></span>
<span data-ttu-id="3102d-317">As you are configuring MPIO on Linux host, you may also need to refer to the following CentoS 6.6 documents:</span><span class="sxs-lookup"><span data-stu-id="3102d-317">As you are configuring MPIO on Linux host, you may also need to refer to the following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="3102d-318">Setting up MPIO on CentOS</span><span class="sxs-lookup"><span data-stu-id="3102d-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="3102d-319">Linux Training Guide</span><span class="sxs-lookup"><span data-stu-id="3102d-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)




