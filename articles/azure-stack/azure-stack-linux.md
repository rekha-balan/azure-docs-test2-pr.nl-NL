---
title: Linux Guests on Azure Stack | Microsoft Docs
description: Learn how create Linux-based virtual machines on Azure Stack.
services: azure-stack
documentationcenter: ''
author: anjayajodha
manager: byronr
editor: ''
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: anajod
ms.openlocfilehash: f660e77de6df94bac5101a2693a3a7d85af5fd39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671320"
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="e6d7d-103">Deploy Linux virtual machines on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e6d7d-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="e6d7d-104">You can deploy Linux virtual machines on the Azure Stack POC by adding a Linux-based image into the Azure Stack Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-104">You can deploy Linux virtual machines on the Azure Stack POC by adding a Linux-based image into the Azure Stack Marketplace.</span></span> <span data-ttu-id="e6d7d-105">Several Linux vendors have provided images that can be added into an Azure Stack POC or you can build your own.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-105">Several Linux vendors have provided images that can be added into an Azure Stack POC or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="e6d7d-106">Download an image</span><span class="sxs-lookup"><span data-stu-id="e6d7d-106">Download an image</span></span>
1. <span data-ttu-id="e6d7d-107">Download and extract an Azure Stack-compatible image from the following links, or prepare your own:</span><span class="sxs-lookup"><span data-stu-id="e6d7d-107">Download and extract an Azure Stack-compatible image from the following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="e6d7d-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="e6d7d-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="e6d7d-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="e6d7d-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="e6d7d-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e6d7d-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="e6d7d-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="e6d7d-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="e6d7d-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e6d7d-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="e6d7d-113">Extract the image VHD if necessary and [add the image to the Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="e6d7d-113">Extract the image VHD if necessary and [add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="e6d7d-114">Make sure that the `OSType` parameter is set to `Linux`.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-114">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
3. <span data-ttu-id="e6d7d-115">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-115">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="e6d7d-116">Prepare your own image</span><span class="sxs-lookup"><span data-stu-id="e6d7d-116">Prepare your own image</span></span>
1. <span data-ttu-id="e6d7d-117">Prepare your own Linux image using one of the following instructions:</span><span class="sxs-lookup"><span data-stu-id="e6d7d-117">Prepare your own Linux image using one of the following instructions:</span></span>
   
   * [<span data-ttu-id="e6d7d-118">CentOS-based Distributions</span><span class="sxs-lookup"><span data-stu-id="e6d7d-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="e6d7d-119">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="e6d7d-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="e6d7d-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="e6d7d-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="e6d7d-121">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="e6d7d-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="e6d7d-122">SLES & openSUSE</span><span class="sxs-lookup"><span data-stu-id="e6d7d-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="e6d7d-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e6d7d-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="e6d7d-124">Download and install the [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="e6d7d-124">Download and install the [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="e6d7d-125">The Azure Linux Agent version 2.1.3 or higher is required to provision your Linux VM on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-125">The Azure Linux Agent version 2.1.3 or higher is required to provision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="e6d7d-126">Many of the distributions listed above already include this version of the agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span><span class="sxs-lookup"><span data-stu-id="e6d7d-126">Many of the distributions listed above already include this version of the agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="e6d7d-127">However, if the version of the Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install the agent manually.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-127">However, if the version of the Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install the agent manually.</span></span> <span data-ttu-id="e6d7d-128">The installed version can be determined either from the package name or by running `/usr/sbin/waagent -version` on the VM.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-128">The installed version can be determined either from the package name or by running `/usr/sbin/waagent -version` on the VM.</span></span>
   
    <span data-ttu-id="e6d7d-129">Follow the instructions below to install the Azure Linux agent manually -</span><span class="sxs-lookup"><span data-stu-id="e6d7d-129">Follow the instructions below to install the Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="e6d7d-130">First, download the latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span><span class="sxs-lookup"><span data-stu-id="e6d7d-130">First, download the latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="e6d7d-131">Unpack the Azure agent:</span><span class="sxs-lookup"><span data-stu-id="e6d7d-131">Unpack the Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="e6d7d-132">Install python-setuptools</span><span class="sxs-lookup"><span data-stu-id="e6d7d-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="e6d7d-133">**Debian / Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e6d7d-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="e6d7d-134">**Ubuntu 16.04+**</span><span class="sxs-lookup"><span data-stu-id="e6d7d-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="e6d7d-135">**RHEL / CentOS / Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="e6d7d-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="e6d7d-136">Install the Azure agent:</span><span class="sxs-lookup"><span data-stu-id="e6d7d-136">Install the Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="e6d7d-137">Systems with Python 2.x and Python 3.x installed side-by-side may need to run the following command:</span><span class="sxs-lookup"><span data-stu-id="e6d7d-137">Systems with Python 2.x and Python 3.x installed side-by-side may need to run the following command:</span></span>
     
     # <a name="sudo-python3-setuppy-install---register-service"></a><span data-ttu-id="e6d7d-138">sudo python3 setup.py install --register-service</span><span class="sxs-lookup"><span data-stu-id="e6d7d-138">sudo python3 setup.py install --register-service</span></span>
     <span data-ttu-id="e6d7d-139">For more information, see the Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e6d7d-139">For more information, see the Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="e6d7d-140">[Add the image to the Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="e6d7d-140">[Add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="e6d7d-141">Make sure that the `OSType` parameter is set to `Linux`.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-141">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
4. <span data-ttu-id="e6d7d-142">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e6d7d-142">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6d7d-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6d7d-143">Next steps</span></span>
[<span data-ttu-id="e6d7d-144">Frequently asked questions for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e6d7d-144">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

