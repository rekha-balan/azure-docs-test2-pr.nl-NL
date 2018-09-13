---
title: Configuring DHCPv6 for Linux VMs | Microsoft Docs
description: How to configure DHCPv6 for Linux VMs.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: ''
keywords: ipv6, azure load balancer, dual stack, public ip, native ipv6, mobile, iot
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555585"
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="5d798-104">Configuring DHCPv6 for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="5d798-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="5d798-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span><span class="sxs-lookup"><span data-stu-id="5d798-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="5d798-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span><span class="sxs-lookup"><span data-stu-id="5d798-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="5d798-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span><span class="sxs-lookup"><span data-stu-id="5d798-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="5d798-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5d798-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="5d798-109">No additional changes are required when using those images.</span><span class="sxs-lookup"><span data-stu-id="5d798-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="5d798-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span><span class="sxs-lookup"><span data-stu-id="5d798-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="5d798-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span><span class="sxs-lookup"><span data-stu-id="5d798-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="5d798-112">We recommended that you test your configuration changes on non-production systems.</span><span class="sxs-lookup"><span data-stu-id="5d798-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="5d798-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5d798-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="5d798-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span><span class="sxs-lookup"><span data-stu-id="5d798-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="5d798-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="5d798-115">Ubuntu</span></span>

1. <span data-ttu-id="5d798-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span><span class="sxs-lookup"><span data-stu-id="5d798-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="5d798-117">Edit the network configuration for the eth0 interface with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="5d798-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="5d798-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="5d798-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="5d798-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="5d798-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="5d798-120">Renew IPv6 address:</span><span class="sxs-lookup"><span data-stu-id="5d798-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="5d798-121">Debian</span><span class="sxs-lookup"><span data-stu-id="5d798-121">Debian</span></span>

1. <span data-ttu-id="5d798-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span><span class="sxs-lookup"><span data-stu-id="5d798-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="5d798-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span><span class="sxs-lookup"><span data-stu-id="5d798-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="5d798-124">Renew IPv6 address:</span><span class="sxs-lookup"><span data-stu-id="5d798-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="5d798-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="5d798-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="5d798-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span><span class="sxs-lookup"><span data-stu-id="5d798-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="5d798-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span><span class="sxs-lookup"><span data-stu-id="5d798-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="5d798-128">Renew IPv6 address:</span><span class="sxs-lookup"><span data-stu-id="5d798-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="5d798-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="5d798-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="5d798-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5d798-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="5d798-131">No additional changes are required when using those images.</span><span class="sxs-lookup"><span data-stu-id="5d798-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="5d798-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d798-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="5d798-133">Install the `dhcp-client` package, if needed:</span><span class="sxs-lookup"><span data-stu-id="5d798-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="5d798-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span><span class="sxs-lookup"><span data-stu-id="5d798-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="5d798-135">Renew the IPv6 address:</span><span class="sxs-lookup"><span data-stu-id="5d798-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="5d798-136">SLES 12 and openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="5d798-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="5d798-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5d798-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="5d798-138">No additional changes are required when using those images.</span><span class="sxs-lookup"><span data-stu-id="5d798-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="5d798-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d798-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="5d798-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span><span class="sxs-lookup"><span data-stu-id="5d798-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="5d798-141">with the following value:</span><span class="sxs-lookup"><span data-stu-id="5d798-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="5d798-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="5d798-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="5d798-143">Renew the IPv6 address:</span><span class="sxs-lookup"><span data-stu-id="5d798-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="5d798-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5d798-144">CoreOS</span></span>

<span data-ttu-id="5d798-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5d798-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="5d798-146">No additional changes are required when using those images.</span><span class="sxs-lookup"><span data-stu-id="5d798-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="5d798-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="5d798-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="5d798-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="5d798-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="5d798-149">Renew the IPv6 address:</span><span class="sxs-lookup"><span data-stu-id="5d798-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
