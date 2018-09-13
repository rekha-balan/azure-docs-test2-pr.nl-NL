---
title: Remote Desktop to a Linux VM | Microsoft Docs
description: Learn how to install and configure Remote Desktop to connect to a Microsoft Azure Linux VM
services: virtual-machines-linux
documentationcenter: ''
author: SuperScottz
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 2332843798061dad3dca31695c5949c73957a475
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556647"
---
# <a name="using-remote-desktop-to-connect-to-a-microsoft-azure-linux-vm"></a><span data-ttu-id="5220e-103">Using Remote Desktop to connect to a Microsoft Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="5220e-103">Using Remote Desktop to connect to a Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="5220e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5220e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5220e-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="5220e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5220e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="5220e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="overview"></a><span data-ttu-id="5220e-107">Overview</span><span class="sxs-lookup"><span data-stu-id="5220e-107">Overview</span></span>
<span data-ttu-id="5220e-108">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span><span class="sxs-lookup"><span data-stu-id="5220e-108">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="5220e-109">How can we use RDP to connect to a Linux VM (virtual machine) remotely?</span><span class="sxs-lookup"><span data-stu-id="5220e-109">How can we use RDP to connect to a Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="5220e-110">This guidance will give you the answer!</span><span class="sxs-lookup"><span data-stu-id="5220e-110">This guidance will give you the answer!</span></span> <span data-ttu-id="5220e-111">It will help you to install and config xrdp on your Microsoft Azure Linux VM, and you are able to connect it with Remote Desktop from a Windows machine.</span><span class="sxs-lookup"><span data-stu-id="5220e-111">It will help you to install and config xrdp on your Microsoft Azure Linux VM, and you are able to connect it with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="5220e-112">We will use Linux VM running Ubuntu or OpenSUSE as the example in this guidance.</span><span class="sxs-lookup"><span data-stu-id="5220e-112">We will use Linux VM running Ubuntu or OpenSUSE as the example in this guidance.</span></span>

<span data-ttu-id="5220e-113">Xrdp is an open source RDP server, which allows you to connect your Linux server with Remote Desktop from a Windows machine.</span><span class="sxs-lookup"><span data-stu-id="5220e-113">Xrdp is an open source RDP server, which allows you to connect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="5220e-114">It performs much nicer than VNC (Virtual Network Computing).</span><span class="sxs-lookup"><span data-stu-id="5220e-114">It performs much nicer than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="5220e-115">VNC has this streak of “JPEG” quality and slow behavior, whereas RDP is fast and crystal clear.</span><span class="sxs-lookup"><span data-stu-id="5220e-115">VNC has this streak of “JPEG” quality and slow behavior, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="5220e-116">You must already have an Microsoft Azure VM running Linux.</span><span class="sxs-lookup"><span data-stu-id="5220e-116">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="5220e-117">To create and set up a Linux VM, see the [Azure Linux VM tutorial](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="5220e-117">To create and set up a Linux VM, see the [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-endpoint-for-remote-desktop"></a><span data-ttu-id="5220e-118">Create endpoint for Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="5220e-118">Create endpoint for Remote Desktop</span></span>
<span data-ttu-id="5220e-119">We will use the default endpoint 3389 for Remote Desktop in this doc. So set up 3389 endpoint as Remote Desktop to your Linux VM like below:</span><span class="sxs-lookup"><span data-stu-id="5220e-119">We will use the default endpoint 3389 for Remote Desktop in this doc. So set up 3389 endpoint as Remote Desktop to your Linux VM like below:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/remote-desktop/no1.png)

<span data-ttu-id="5220e-121">if you didn't know how to set up endpoint to your VM, see [guidance](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="5220e-121">if you didn't know how to set up endpoint to your VM, see [guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="5220e-122">Install Gnome Desktop</span><span class="sxs-lookup"><span data-stu-id="5220e-122">Install Gnome Desktop</span></span>
<span data-ttu-id="5220e-123">Connect to your Linux VM through putty, and install `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="5220e-123">Connect to your Linux VM through putty, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="5220e-124">For Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-124">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="5220e-125">For OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-125">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="5220e-126">Install xrdp</span><span class="sxs-lookup"><span data-stu-id="5220e-126">Install xrdp</span></span>
<span data-ttu-id="5220e-127">For Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-127">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="5220e-128">For OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-128">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="5220e-129">Update the OpenSUSE version with the version you are using into below command, below is an example command for `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="5220e-129">Update the OpenSUSE version with the version you are using into below command, below is an example command for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="5220e-130">Start xrdp and set xdrp service at boot-up</span><span class="sxs-lookup"><span data-stu-id="5220e-130">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="5220e-131">For OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-131">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="5220e-132">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span><span class="sxs-lookup"><span data-stu-id="5220e-132">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="5220e-133">Using xfce if you are using Ubuntu version later than Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="5220e-133">Using xfce if you are using Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="5220e-134">Because current xrdp could not support the Gnome Desktop from Ubuntu version later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span><span class="sxs-lookup"><span data-stu-id="5220e-134">Because current xrdp could not support the Gnome Desktop from Ubuntu version later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="5220e-135">Install `xfce`, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-135">Install `xfce`, use:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="5220e-136">Then enable `xfce`, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-136">Then enable `xfce`, use:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="5220e-137">Edit the config file `/etc/xrdp/startwm.sh`, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-137">Edit the config file `/etc/xrdp/startwm.sh`, use:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="5220e-138">Add line `xfce4-session` before the line `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="5220e-138">Add line `xfce4-session` before the line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="5220e-139">Restart xrdp service, use:</span><span class="sxs-lookup"><span data-stu-id="5220e-139">Restart xrdp service, use:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="5220e-140">Connect your Linux VM from a Windows machine</span><span class="sxs-lookup"><span data-stu-id="5220e-140">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="5220e-141">In a Windows machine, start the remote desktop client, input your Linux VM DNS name, or go to `Dashboard` of your VM in Azure classic portal and click `Connect` to connect your Linux VM, you will see below login window:</span><span class="sxs-lookup"><span data-stu-id="5220e-141">In a Windows machine, start the remote desktop client, input your Linux VM DNS name, or go to `Dashboard` of your VM in Azure classic portal and click `Connect` to connect your Linux VM, you will see below login window:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/remote-desktop/no2.png)

<span data-ttu-id="5220e-143">Login with the `user` & `password` of your Linux VM, and enjoy the Remote Desktop from your Microsoft Azure Linux VM right now!</span><span class="sxs-lookup"><span data-stu-id="5220e-143">Login with the `user` & `password` of your Linux VM, and enjoy the Remote Desktop from your Microsoft Azure Linux VM right now!</span></span>

## <a name="next"></a><span data-ttu-id="5220e-144">Next</span><span class="sxs-lookup"><span data-stu-id="5220e-144">Next</span></span>
<span data-ttu-id="5220e-145">For more information to use xrdp, you could refer [here](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="5220e-145">For more information to use xrdp, you could refer [here](http://www.xrdp.org/).</span></span>



