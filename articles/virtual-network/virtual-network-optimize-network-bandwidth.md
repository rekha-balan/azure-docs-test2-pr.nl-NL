---
title: Optimize VM network throughput | Microsoft Docs
description: Learn how to optimize Azure virtual machine network throughput.
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/15/2017
ms.author: steveesp
ms.openlocfilehash: b604782f917584d1ecec432c20de75f427176ed1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44801221"
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="e18ba-103">Optimize network throughput for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="e18ba-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="e18ba-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span><span class="sxs-lookup"><span data-stu-id="e18ba-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="e18ba-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS, and Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e18ba-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS, and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="e18ba-106">Windows VM</span><span class="sxs-lookup"><span data-stu-id="e18ba-106">Windows VM</span></span>

<span data-ttu-id="e18ba-107">If your Windows VM supports [Accelerated Networking](create-vm-accelerated-networking-powershell.md), enabling that feature would be the optimal configuration for throughput.</span><span class="sxs-lookup"><span data-stu-id="e18ba-107">If your Windows VM supports [Accelerated Networking](create-vm-accelerated-networking-powershell.md), enabling that feature would be the optimal configuration for throughput.</span></span> <span data-ttu-id="e18ba-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span><span class="sxs-lookup"><span data-stu-id="e18ba-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="e18ba-109">RSS may be disabled by default in a Windows VM.</span><span class="sxs-lookup"><span data-stu-id="e18ba-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="e18ba-110">To determine whether RSS is enabled, and enable it if it's currently disabled, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="e18ba-110">To determine whether RSS is enabled, and enable it if it's currently disabled, complete the following steps:</span></span>

1. <span data-ttu-id="e18ba-111">See if RSS is enabled for a network adapter with the `Get-NetAdapterRss` PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="e18ba-111">See if RSS is enabled for a network adapter with the `Get-NetAdapterRss` PowerShell command.</span></span> <span data-ttu-id="e18ba-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span><span class="sxs-lookup"><span data-stu-id="e18ba-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled                 : False
    ```
2. <span data-ttu-id="e18ba-113">To enable RSS, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="e18ba-113">To enable RSS, enter the following command:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="e18ba-114">The previous command does not have an output.</span><span class="sxs-lookup"><span data-stu-id="e18ba-114">The previous command does not have an output.</span></span> <span data-ttu-id="e18ba-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span><span class="sxs-lookup"><span data-stu-id="e18ba-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="e18ba-116">A Reconnecting dialog box appears during the connectivity loss.</span><span class="sxs-lookup"><span data-stu-id="e18ba-116">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="e18ba-117">Connectivity is typically restored after the third attempt.</span><span class="sxs-lookup"><span data-stu-id="e18ba-117">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="e18ba-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span><span class="sxs-lookup"><span data-stu-id="e18ba-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="e18ba-119">If successful, the following example output is returned:</span><span class="sxs-lookup"><span data-stu-id="e18ba-119">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled                  : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="e18ba-120">Linux VM</span><span class="sxs-lookup"><span data-stu-id="e18ba-120">Linux VM</span></span>

<span data-ttu-id="e18ba-121">RSS is always enabled by default in an Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="e18ba-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="e18ba-122">Linux kernels released since October 2017 include new network optimizations options that enable a Linux VM to achieve higher network throughput.</span><span class="sxs-lookup"><span data-stu-id="e18ba-122">Linux kernels released since October 2017 include new network optimizations options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu-for-new-deployments"></a><span data-ttu-id="e18ba-123">Ubuntu for new deployments</span><span class="sxs-lookup"><span data-stu-id="e18ba-123">Ubuntu for new deployments</span></span>

<span data-ttu-id="e18ba-124">The Ubuntu Azure kernel provides the best network performance on Azure and has been the default kernel since September 21, 2017.</span><span class="sxs-lookup"><span data-stu-id="e18ba-124">The Ubuntu Azure kernel provides the best network performance on Azure and has been the default kernel since September 21, 2017.</span></span> <span data-ttu-id="e18ba-125">In order to get this kernel, first install the latest supported version of 16.04-LTS, as follows:</span><span class="sxs-lookup"><span data-stu-id="e18ba-125">In order to get this kernel, first install the latest supported version of 16.04-LTS, as follows:</span></span>

```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```

<span data-ttu-id="e18ba-126">After the creation is complete, enter the following commands to get the latest updates.</span><span class="sxs-lookup"><span data-stu-id="e18ba-126">After the creation is complete, enter the following commands to get the latest updates.</span></span> <span data-ttu-id="e18ba-127">These steps also work for VMs currently running the Ubuntu Azure kernel.</span><span class="sxs-lookup"><span data-stu-id="e18ba-127">These steps also work for VMs currently running the Ubuntu Azure kernel.</span></span>

```bash
#run as root or preface with sudo
apt-get -y update
apt-get -y upgrade
apt-get -y dist-upgrade
```

<span data-ttu-id="e18ba-128">The following optional command set may be helpful for existing Ubuntu deployments that already have the Azure kernel but that have failed to further updates with errors.</span><span class="sxs-lookup"><span data-stu-id="e18ba-128">The following optional command set may be helpful for existing Ubuntu deployments that already have the Azure kernel but that have failed to further updates with errors.</span></span>

```bash
#optional steps may be helpful in existing deployments with the Azure kernel
#run as root or preface with sudo
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
apt-get -y dist-upgrade
```

#### <a name="ubuntu-azure-kernel-upgrade-for-existing-vms"></a><span data-ttu-id="e18ba-129">Ubuntu Azure kernel upgrade for existing VMs</span><span class="sxs-lookup"><span data-stu-id="e18ba-129">Ubuntu Azure kernel upgrade for existing VMs</span></span>

<span data-ttu-id="e18ba-130">Significant throughput performance can be achieved by upgrading to the Azure Linux kernel.</span><span class="sxs-lookup"><span data-stu-id="e18ba-130">Significant throughput performance can be achieved by upgrading to the Azure Linux kernel.</span></span> <span data-ttu-id="e18ba-131">To verify whether you have this kernel, check your kernel version.</span><span class="sxs-lookup"><span data-stu-id="e18ba-131">To verify whether you have this kernel, check your kernel version.</span></span>

```bash
#Azure kernel name ends with "-azure"
uname -r

#sample output on Azure kernel:
#4.13.0-1007-azure
```

<span data-ttu-id="e18ba-132">If your VM does not have the Azure kernel, the version number usually begins with "4.4."</span><span class="sxs-lookup"><span data-stu-id="e18ba-132">If your VM does not have the Azure kernel, the version number usually begins with "4.4."</span></span> <span data-ttu-id="e18ba-133">If the VM does not have the Azure kernel, run the following commands as root:</span><span class="sxs-lookup"><span data-stu-id="e18ba-133">If the VM does not have the Azure kernel, run the following commands as root:</span></span>

```bash
#run as root or preface with sudo
apt-get update
apt-get upgrade -y
apt-get dist-upgrade -y
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="e18ba-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="e18ba-134">CentOS</span></span>

<span data-ttu-id="e18ba-135">In order to get the latest optimizations, it is best to create a VM with the latest supported version by specifying the following parameters:</span><span class="sxs-lookup"><span data-stu-id="e18ba-135">In order to get the latest optimizations, it is best to create a VM with the latest supported version by specifying the following parameters:</span></span>

```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.4",
"Version": "latest"
```

<span data-ttu-id="e18ba-136">New and existing VMs can benefit from installing the latest Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="e18ba-136">New and existing VMs can benefit from installing the latest Linux Integration Services (LIS).</span></span> <span data-ttu-id="e18ba-137">The throughput optimization is in LIS, starting from 4.2.2-2, although later versions contain further improvements.</span><span class="sxs-lookup"><span data-stu-id="e18ba-137">The throughput optimization is in LIS, starting from 4.2.2-2, although later versions contain further improvements.</span></span> <span data-ttu-id="e18ba-138">Enter the following commands to install the latest LIS:</span><span class="sxs-lookup"><span data-stu-id="e18ba-138">Enter the following commands to install the latest LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="e18ba-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="e18ba-139">Red Hat</span></span>

<span data-ttu-id="e18ba-140">In order to get the optimizations, it is best to create a VM with the latest supported version by specifying the following parameters:</span><span class="sxs-lookup"><span data-stu-id="e18ba-140">In order to get the optimizations, it is best to create a VM with the latest supported version by specifying the following parameters:</span></span>

```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7-RAW"
"Version": "latest"
```

<span data-ttu-id="e18ba-141">New and existing VMs can benefit from installing the latest Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="e18ba-141">New and existing VMs can benefit from installing the latest Linux Integration Services (LIS).</span></span> <span data-ttu-id="e18ba-142">The throughput optimization is in LIS, starting from 4.2.</span><span class="sxs-lookup"><span data-stu-id="e18ba-142">The throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="e18ba-143">Enter the following commands to download and install LIS:</span><span class="sxs-lookup"><span data-stu-id="e18ba-143">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.2.3-5
cd lis4.2.3-5
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.3-5.tar.gz
tar xvzf lis-rpms-4.2.3-5.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="e18ba-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="e18ba-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e18ba-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="e18ba-145">Next steps</span></span>
* <span data-ttu-id="e18ba-146">See the optimized result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span><span class="sxs-lookup"><span data-stu-id="e18ba-146">See the optimized result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="e18ba-147">Read about how [bandwidth is allocated to virtual machines] (virtual-machine-network-throughput.md)</span><span class="sxs-lookup"><span data-stu-id="e18ba-147">Read about how [bandwidth is allocated to virtual machines] (virtual-machine-network-throughput.md)</span></span>
* <span data-ttu-id="e18ba-148">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e18ba-148">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
