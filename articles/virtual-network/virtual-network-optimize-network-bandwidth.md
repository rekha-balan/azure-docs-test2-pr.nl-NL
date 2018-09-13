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
ms.date: 02/01/2017
ms.author: steveesp
ms.openlocfilehash: 1ff280063ef872a9c637a501a0cc73935779b631
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554392"
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="9c8f7-103">Optimize network throughput for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="9c8f7-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="9c8f7-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="9c8f7-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="9c8f7-106">Windows VM</span><span class="sxs-lookup"><span data-stu-id="9c8f7-106">Windows VM</span></span>

<span data-ttu-id="9c8f7-107">A VM using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-107">A VM using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="9c8f7-108">RSS may be disabled by default in a Windows VM.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-108">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="9c8f7-109">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-109">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span></span>

1. <span data-ttu-id="9c8f7-110">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-110">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="9c8f7-111">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-111">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="9c8f7-112">Enter the following command to enable RSS:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-112">Enter the following command to enable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="9c8f7-113">The previous command does not have an output.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-113">The previous command does not have an output.</span></span> <span data-ttu-id="9c8f7-114">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-114">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="9c8f7-115">A Reconnecting dialog box appears during the connectivity loss.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-115">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="9c8f7-116">Connectivity is typically restored after the third attempt.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-116">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="9c8f7-117">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-117">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="9c8f7-118">If successful, the following example output is returned:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-118">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="9c8f7-119">Linux VM</span><span class="sxs-lookup"><span data-stu-id="9c8f7-119">Linux VM</span></span>

<span data-ttu-id="9c8f7-120">RSS is always enabled by default in an Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-120">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="9c8f7-121">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-121">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="9c8f7-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9c8f7-122">Ubuntu</span></span>

<span data-ttu-id="9c8f7-123">In order to get the optimization, first update to the latest supported version, as of January 2017, which is:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-123">In order to get the optimization, first update to the latest supported version, as of January 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="9c8f7-124">After the update is complete, enter the following commands to get the latest kernel:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-124">After the update is complete, enter the following commands to get the latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="9c8f7-125">Optional command:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-125">Optional command:</span></span>

`apt-get -y dist-upgrade`

### <a name="centos"></a><span data-ttu-id="9c8f7-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="9c8f7-126">CentOS</span></span>

<span data-ttu-id="9c8f7-127">In order to get the optimization, first update to the latest supported version, as of January 2017, which is:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-127">In order to get the optimization, first update to the latest supported version, as of January 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="9c8f7-128">After the update is complete, install the latest Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="9c8f7-128">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="9c8f7-129">The throughput optimization is in LIS, starting from 4.1.3.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-129">The throughput optimization is in LIS, starting from 4.1.3.</span></span> <span data-ttu-id="9c8f7-130">Enter the following commands to install LIS:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-130">Enter the following commands to install LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="9c8f7-131">Red Hat</span><span class="sxs-lookup"><span data-stu-id="9c8f7-131">Red Hat</span></span>

<span data-ttu-id="9c8f7-132">In order to get the optimization, first update to the latest supported version, as of January 2017, which is:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-132">In order to get the optimization, first update to the latest supported version, as of January 2017, which is:</span></span>

<span data-ttu-id="9c8f7-133">"Publisher": "RedHat" "Offer": "RHEL" "Sku": "7.3" "Version": "7.3.20161104"</span><span class="sxs-lookup"><span data-stu-id="9c8f7-133">"Publisher": "RedHat" "Offer": "RHEL" "Sku": "7.3" "Version": "7.3.20161104"</span></span>

<span data-ttu-id="9c8f7-134">After the update is complete, install the latest Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="9c8f7-134">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="9c8f7-135">The throughput optimization is in LIS, starting from 4.1.3.</span><span class="sxs-lookup"><span data-stu-id="9c8f7-135">The throughput optimization is in LIS, starting from 4.1.3.</span></span> <span data-ttu-id="9c8f7-136">Enter the following commands to download and install LIS:</span><span class="sxs-lookup"><span data-stu-id="9c8f7-136">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.1.3
cd lis4.1.3
wget https://download.microsoft.com/download/7/6/B/76BE7A6E-E39F-436C-9353-F4B44EF966E9/lis-rpms-4.1.3.tar.gz
tar xvzf lis-rpms-4.1.3.tar.gz
cd LISISO
install.sh #or upgrade.sh if previous LIS was previously installed
```
 
<span data-ttu-id="9c8f7-137">Learn more about Linux Integration Services Version 4.1 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=51612).</span><span class="sxs-lookup"><span data-stu-id="9c8f7-137">Learn more about Linux Integration Services Version 4.1 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=51612).</span></span>
