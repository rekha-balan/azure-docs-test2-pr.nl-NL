---
title: Update the Azure Linux Agent from GitHub | Microsoft Docs
description: Learn how to the update Azure Linux Agent for your Linux VM in Azure to the lateset version from GitHub
services: virtual-machines-linux
documentationcenter: ''
author: SuperScottz
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/14/2015
ms.author: mingzhan
ms.openlocfilehash: 8e45c03e410bdb8c088364c852ff5385e56e8086
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555577"
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm-to-the-latest-version-from-github"></a><span data-ttu-id="84db4-103">How to update the Azure Linux Agent on a VM to the latest version from GitHub</span><span class="sxs-lookup"><span data-stu-id="84db4-103">How to update the Azure Linux Agent on a VM to the latest version from GitHub</span></span>
<span data-ttu-id="84db4-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span><span class="sxs-lookup"><span data-stu-id="84db4-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

1. <span data-ttu-id="84db4-105">A running Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="84db4-105">A running Linux VM in Azure.</span></span>
2. <span data-ttu-id="84db4-106">A connection to that Linux VM using SSH.</span><span class="sxs-lookup"><span data-stu-id="84db4-106">A connection to that Linux VM using SSH.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<br>

> [!NOTE]
> <span data-ttu-id="84db4-107">If you will  be performing this task from a Windows computer, you can use PuTTY to SSH into your Linux machine.</span><span class="sxs-lookup"><span data-stu-id="84db4-107">If you will  be performing this task from a Windows computer, you can use PuTTY to SSH into your Linux machine.</span></span> <span data-ttu-id="84db4-108">For more information, see [How to Log on to a Virtual Machine Running Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84db4-108">For more information, see [How to Log on to a Virtual Machine Running Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="84db4-109">Azure-endorsed Linux distros have put the Azure Linux Agent package in their repositories, so please check and install the latest version from that Distro repository first if possible.</span><span class="sxs-lookup"><span data-stu-id="84db4-109">Azure-endorsed Linux distros have put the Azure Linux Agent package in their repositories, so please check and install the latest version from that Distro repository first if possible.</span></span>  

<span data-ttu-id="84db4-110">For Ubuntu, just type:</span><span class="sxs-lookup"><span data-stu-id="84db4-110">For Ubuntu, just type:</span></span>

```bash
sudo apt-get install walinuxagent
```

<span data-ttu-id="84db4-111">And on CentOS, type:</span><span class="sxs-lookup"><span data-stu-id="84db4-111">And on CentOS, type:</span></span>

```bash
sudo yum install waagent
```

<span data-ttu-id="84db4-112">For Oracle Linux, make sure that the `Addons` repository is enabled.</span><span class="sxs-lookup"><span data-stu-id="84db4-112">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="84db4-113">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span><span class="sxs-lookup"><span data-stu-id="84db4-113">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="84db4-114">Then, to install the latest version of the Azure Linux Agent, type:</span><span class="sxs-lookup"><span data-stu-id="84db4-114">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="84db4-115">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span><span class="sxs-lookup"><span data-stu-id="84db4-115">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="84db4-116">For Oracle Linux 6 virtual machines:</span><span class="sxs-lookup"><span data-stu-id="84db4-116">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="84db4-117">For Oracle Linux 7 virtual machines:</span><span class="sxs-lookup"><span data-stu-id="84db4-117">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="84db4-118">Then type:</span><span class="sxs-lookup"><span data-stu-id="84db4-118">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="84db4-119">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="84db4-119">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>

## <a name="install-wget"></a><span data-ttu-id="84db4-120">Install wget</span><span class="sxs-lookup"><span data-stu-id="84db4-120">Install wget</span></span>
<span data-ttu-id="84db4-121">Login to your VM using SSH.</span><span class="sxs-lookup"><span data-stu-id="84db4-121">Login to your VM using SSH.</span></span>

<span data-ttu-id="84db4-122">Install wget (there are some distros that don't install it by default such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `#sudo yum install wget` on the command line.</span><span class="sxs-lookup"><span data-stu-id="84db4-122">Install wget (there are some distros that don't install it by default such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `#sudo yum install wget` on the command line.</span></span>

## <a name="download-the-latest-version"></a><span data-ttu-id="84db4-123">Download the latest version</span><span class="sxs-lookup"><span data-stu-id="84db4-123">Download the latest version</span></span>
<span data-ttu-id="84db4-124">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span><span class="sxs-lookup"><span data-stu-id="84db4-124">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="84db4-125">(You can locate your current version by typing `#waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="84db4-125">(You can locate your current version by typing `#waagent --version`.)</span></span>

### <a name="for-version-20x-type"></a><span data-ttu-id="84db4-126">For version 2.0.x, type:</span><span class="sxs-lookup"><span data-stu-id="84db4-126">For version 2.0.x, type:</span></span>

```bash
wget https://raw.githubusercontent.com/Azure/WALinuxAgent/WALinuxAgent-[version]/waagent
```

<span data-ttu-id="84db4-127">The following line uses version 2.0.14 as an example:</span><span class="sxs-lookup"><span data-stu-id="84db4-127">The following line uses version 2.0.14 as an example:</span></span>

```bash
wget https://raw.githubusercontent.com/Azure/WALinuxAgent/WALinuxAgent-2.0.14/waagent
```

### <a name="for-version-21x-or-later-type"></a><span data-ttu-id="84db4-128">For version 2.1.x or later, type:</span><span class="sxs-lookup"><span data-stu-id="84db4-128">For version 2.1.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/WALinuxAgent-[version].zip
unzip WALinuxAgent-[version].zip
cd WALinuxAgent-[version]
```

<span data-ttu-id="84db4-129">The following line uses version 2.1.0 as an example:</span><span class="sxs-lookup"><span data-stu-id="84db4-129">The following line uses version 2.1.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/WALinuxAgent-2.1.0.zip
unzip WALinuxAgent-2.1.0.zip  
cd WALinuxAgent-2.1.0
```

## <a name="install-the-azure-linux-agent"></a><span data-ttu-id="84db4-130">Install the Azure Linux Agent</span><span class="sxs-lookup"><span data-stu-id="84db4-130">Install the Azure Linux Agent</span></span>
### <a name="for-version-20x-use"></a><span data-ttu-id="84db4-131">For version 2.0.x, use:</span><span class="sxs-lookup"><span data-stu-id="84db4-131">For version 2.0.x, use:</span></span>
<span data-ttu-id="84db4-132">Make waagent executable:</span><span class="sxs-lookup"><span data-stu-id="84db4-132">Make waagent executable:</span></span>

```bash
chmod +x waagent
```

<span data-ttu-id="84db4-133">Copy new the executable to /usr/sbin/.</span><span class="sxs-lookup"><span data-stu-id="84db4-133">Copy new the executable to /usr/sbin/.</span></span>

<span data-ttu-id="84db4-134">For most of Linux, use:</span><span class="sxs-lookup"><span data-stu-id="84db4-134">For most of Linux, use:</span></span>

```bash
sudo cp waagent /usr/sbin
```

<span data-ttu-id="84db4-135">For CoreOS, use:</span><span class="sxs-lookup"><span data-stu-id="84db4-135">For CoreOS, use:</span></span>

```bash
sudo cp waagent /usr/share/oem/bin/
```

<span data-ttu-id="84db4-136">If this is a new installation of the Azure Linux Agent, run:</span><span class="sxs-lookup"><span data-stu-id="84db4-136">If this is a new installation of the Azure Linux Agent, run:</span></span>

```bash
sudo /usr/sbin/waagent -install -verbose
```

### <a name="for-version-21x-use"></a><span data-ttu-id="84db4-137">For version 2.1.x, use:</span><span class="sxs-lookup"><span data-stu-id="84db4-137">For version 2.1.x, use:</span></span>
<span data-ttu-id="84db4-138">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="84db4-138">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="84db4-139">Then run:</span><span class="sxs-lookup"><span data-stu-id="84db4-139">Then run:</span></span>

```bash
sudo python setup.py install
```

## <a name="restart-the-waagent-service"></a><span data-ttu-id="84db4-140">Restart the waagent service</span><span class="sxs-lookup"><span data-stu-id="84db4-140">Restart the waagent service</span></span>
<span data-ttu-id="84db4-141">For most of linux Distros:</span><span class="sxs-lookup"><span data-stu-id="84db4-141">For most of linux Distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="84db4-142">For Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="84db4-142">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="84db4-143">For CoreOS, use:</span><span class="sxs-lookup"><span data-stu-id="84db4-143">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

## <a name="confirm-the-azure-linux-agent-version"></a><span data-ttu-id="84db4-144">Confirm the Azure Linux Agent version</span><span class="sxs-lookup"><span data-stu-id="84db4-144">Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="84db4-145">For CoreOS, the above command may not work.</span><span class="sxs-lookup"><span data-stu-id="84db4-145">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="84db4-146">You will see that the Azure Linux Agent version has been updated to the new version.</span><span class="sxs-lookup"><span data-stu-id="84db4-146">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="84db4-147">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="84db4-147">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>

