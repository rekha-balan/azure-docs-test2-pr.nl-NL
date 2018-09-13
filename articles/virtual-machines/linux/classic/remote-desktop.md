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
# <a name="using-remote-desktop-to-connect-to-a-microsoft-azure-linux-vm"></a>Using Remote Desktop to connect to a Microsoft Azure Linux VM
> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model.

## <a name="overview"></a>Overview
RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows. How can we use RDP to connect to a Linux VM (virtual machine) remotely?

This guidance will give you the answer! It will help you to install and config xrdp on your Microsoft Azure Linux VM, and you are able to connect it with Remote Desktop from a Windows machine. We will use Linux VM running Ubuntu or OpenSUSE as the example in this guidance.

Xrdp is an open source RDP server, which allows you to connect your Linux server with Remote Desktop from a Windows machine. It performs much nicer than VNC (Virtual Network Computing). VNC has this streak of “JPEG” quality and slow behavior, whereas RDP is fast and crystal clear.

> [!NOTE]
> You must already have an Microsoft Azure VM running Linux. To create and set up a Linux VM, see the [Azure Linux VM tutorial](createportal.md).
> 
> 

## <a name="create-endpoint-for-remote-desktop"></a>Create endpoint for Remote Desktop
We will use the default endpoint 3389 for Remote Desktop in this doc. So set up 3389 endpoint as Remote Desktop to your Linux VM like below:

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/remote-desktop/no1.png)

if you didn't know how to set up endpoint to your VM, see [guidance](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Install Gnome Desktop
Connect to your Linux VM through putty, and install `Gnome Desktop`.

For Ubuntu, use:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


For OpenSUSE, use:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Install xrdp
For Ubuntu, use:

    #sudo apt-get install xrdp

For OpenSUSE, use:

> [!NOTE]
> Update the OpenSUSE version with the version you are using into below command, below is an example command for `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Start xrdp and set xdrp service at boot-up
For OpenSUSE, use:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.

## <a name="using-xfce-if-you-are-using-ubuntu-version-later-than-ubuntu-1204lts"></a>Using xfce if you are using Ubuntu version later than Ubuntu 12.04LTS
Because current xrdp could not support the Gnome Desktop from Ubuntu version later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.

Install `xfce`, use:

    #sudo apt-get install xubuntu-desktop

Then enable `xfce`, use:

    #echo xfce4-session >~/.xsession

Edit the config file `/etc/xrdp/startwm.sh`, use:

    #sudo vi /etc/xrdp/startwm.sh   

Add line `xfce4-session` before the line `/etc/X11/Xsession`.

Restart xrdp service, use:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Connect your Linux VM from a Windows machine
In a Windows machine, start the remote desktop client, input your Linux VM DNS name, or go to `Dashboard` of your VM in Azure classic portal and click `Connect` to connect your Linux VM, you will see below login window:

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/remote-desktop/no2.png)

Login with the `user` & `password` of your Linux VM, and enjoy the Remote Desktop from your Microsoft Azure Linux VM right now!

## <a name="next"></a>Next
For more information to use xrdp, you could refer [here](http://www.xrdp.org/).



