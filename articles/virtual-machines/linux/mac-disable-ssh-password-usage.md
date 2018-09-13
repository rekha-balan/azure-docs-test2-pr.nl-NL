---
title: Disable SSH passwords on your Linux VM by configuring SSHD | Microsoft Docs
description: Secure your Linux VM on Azure by disabling password logins for SSH.
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: ''
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: 413d9b737e3d23ad93a6e84efdd13afd0acc80ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551496"
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="fa5f9-103">Disable SSH passwords on your Linux VM by configuring SSHD</span><span class="sxs-lookup"><span data-stu-id="fa5f9-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="fa5f9-104">This article focuses on how to lock down the login security of your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-104">This article focuses on how to lock down the login security of your Linux VM.</span></span>  <span data-ttu-id="fa5f9-105">As soon as the SSH port 22 is opened to the world bots start trying to login by guessing passwords.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-105">As soon as the SSH port 22 is opened to the world bots start trying to login by guessing passwords.</span></span>  <span data-ttu-id="fa5f9-106">What we will do in this article is disable password logins over SSH.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="fa5f9-107">By completely removing the ability to use passwords we protect the Linux VM from this type of brute force attack.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-107">By completely removing the ability to use passwords we protect the Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="fa5f9-108">The added bonus is we will configure Linux SSHD to only allow logins via SSH public & private keys, by far the most secure way to login to Linux.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-108">The added bonus is we will configure Linux SSHD to only allow logins via SSH public & private keys, by far the most secure way to login to Linux.</span></span>  <span data-ttu-id="fa5f9-109">The possible combinations of it would require to guess the private key is immense and therefore discourages bots from even bothering to try to brute force SSH keys.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-109">The possible combinations of it would require to guess the private key is immense and therefore discourages bots from even bothering to try to brute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="fa5f9-110">Goals</span><span class="sxs-lookup"><span data-stu-id="fa5f9-110">Goals</span></span>
* <span data-ttu-id="fa5f9-111">Configure SSHD to disallow:</span><span class="sxs-lookup"><span data-stu-id="fa5f9-111">Configure SSHD to disallow:</span></span>
  * <span data-ttu-id="fa5f9-112">Password logins</span><span class="sxs-lookup"><span data-stu-id="fa5f9-112">Password logins</span></span>
  * <span data-ttu-id="fa5f9-113">Root user login</span><span class="sxs-lookup"><span data-stu-id="fa5f9-113">Root user login</span></span>
  * <span data-ttu-id="fa5f9-114">Challenge-response authentication</span><span class="sxs-lookup"><span data-stu-id="fa5f9-114">Challenge-response authentication</span></span>
* <span data-ttu-id="fa5f9-115">Configure SSHD to allow:</span><span class="sxs-lookup"><span data-stu-id="fa5f9-115">Configure SSHD to allow:</span></span>
  * <span data-ttu-id="fa5f9-116">only SSH key logins</span><span class="sxs-lookup"><span data-stu-id="fa5f9-116">only SSH key logins</span></span>
* <span data-ttu-id="fa5f9-117">Restart SSHD while still logged in</span><span class="sxs-lookup"><span data-stu-id="fa5f9-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="fa5f9-118">Test the new SSHD configuration</span><span class="sxs-lookup"><span data-stu-id="fa5f9-118">Test the new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="fa5f9-119">Introduction</span><span class="sxs-lookup"><span data-stu-id="fa5f9-119">Introduction</span></span>
[<span data-ttu-id="fa5f9-120">SSH defined</span><span class="sxs-lookup"><span data-stu-id="fa5f9-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="fa5f9-121">SSHD is the SSH Server that runs on the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-121">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="fa5f9-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="fa5f9-123">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-123">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM.</span></span>

<span data-ttu-id="fa5f9-124">For this article it is very important to keep one login to your Linux VM open for the entire walk through.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-124">For this article it is very important to keep one login to your Linux VM open for the entire walk through.</span></span>  <span data-ttu-id="fa5f9-125">For this reason we will open two terminals and SSH to the Linux VM from both of them.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-125">For this reason we will open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="fa5f9-126">We will use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-126">We will use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="fa5f9-127">We will use the second terminal to test those changes once the service is restarted.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-127">We will use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="fa5f9-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa5f9-129">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fa5f9-129">Prerequisites</span></span>
* [<span data-ttu-id="fa5f9-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="fa5f9-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="fa5f9-131">Azure account</span><span class="sxs-lookup"><span data-stu-id="fa5f9-131">Azure account</span></span>
  * [<span data-ttu-id="fa5f9-132">free trial signup</span><span class="sxs-lookup"><span data-stu-id="fa5f9-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="fa5f9-133">Azure portal</span><span class="sxs-lookup"><span data-stu-id="fa5f9-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="fa5f9-134">Linux VM running on azure</span><span class="sxs-lookup"><span data-stu-id="fa5f9-134">Linux VM running on azure</span></span>
* <span data-ttu-id="fa5f9-135">SSH public & private key pair in `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="fa5f9-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="fa5f9-136">SSH public key in `~/.ssh/authorized_keys` on the Linux VM</span><span class="sxs-lookup"><span data-stu-id="fa5f9-136">SSH public key in `~/.ssh/authorized_keys` on the Linux VM</span></span>
* <span data-ttu-id="fa5f9-137">Sudo rights on the VM</span><span class="sxs-lookup"><span data-stu-id="fa5f9-137">Sudo rights on the VM</span></span>
* <span data-ttu-id="fa5f9-138">Port 22 open</span><span class="sxs-lookup"><span data-stu-id="fa5f9-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="fa5f9-139">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="fa5f9-139">Quick Commands</span></span>
<span data-ttu-id="fa5f9-140">*Seasoned Linux Admins who just want the TLDR version start here.  For everyone else that wants the detailed explanation and walk through skip this section.*</span><span class="sxs-lookup"><span data-stu-id="fa5f9-140">*Seasoned Linux Admins who just want the TLDR version start here.  For everyone else that wants the detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="fa5f9-141">Edit the config file as follows:</span><span class="sxs-lookup"><span data-stu-id="fa5f9-141">Edit the config file as follows:</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

<span data-ttu-id="fa5f9-142">Restart the SSHD service.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-142">Restart the SSHD service.</span></span> <span data-ttu-id="fa5f9-143">On Debian-based distros:</span><span class="sxs-lookup"><span data-stu-id="fa5f9-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="fa5f9-144">On Red Hat-based distros:</span><span class="sxs-lookup"><span data-stu-id="fa5f9-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="fa5f9-145">Detailed Walk Through</span><span class="sxs-lookup"><span data-stu-id="fa5f9-145">Detailed Walk Through</span></span>
<span data-ttu-id="fa5f9-146">Login to the Linux VM on terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="fa5f9-146">Login to the Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="fa5f9-147">Login to the Linux VM on terminal 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="fa5f9-147">Login to the Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="fa5f9-148">On T2 we are going to edit the SSHD configuration file.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-148">On T2 we are going to edit the SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="fa5f9-149">From here we will edit just the settings to disable passwords and enable SSH key logins.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-149">From here we will edit just the settings to disable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="fa5f9-150">There are many settings in this file that you should research and change to make Linux & SSH as secure as you need.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-150">There are many settings in this file that you should research and change to make Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="fa5f9-151">Disable Password logins</span><span class="sxs-lookup"><span data-stu-id="fa5f9-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="fa5f9-152">Enable Public Key Authentication</span><span class="sxs-lookup"><span data-stu-id="fa5f9-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="fa5f9-153">Disable Root Login</span><span class="sxs-lookup"><span data-stu-id="fa5f9-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="fa5f9-154">Disable Challenge-response Authentication</span><span class="sxs-lookup"><span data-stu-id="fa5f9-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="fa5f9-155">Restart SSHD</span><span class="sxs-lookup"><span data-stu-id="fa5f9-155">Restart SSHD</span></span>
<span data-ttu-id="fa5f9-156">From the T1 shell verify that you are still logged in.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-156">From the T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="fa5f9-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="fa5f9-158">If any setting are incorrect on your Linux VM you can use T1 to fix sshd_config as you will still be logged in and SSH will keep the connection alive during the SSHD service restart.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-158">If any setting are incorrect on your Linux VM you can use T1 to fix sshd_config as you will still be logged in and SSH will keep the connection alive during the SSHD service restart.</span></span>

<span data-ttu-id="fa5f9-159">From T2 run:</span><span class="sxs-lookup"><span data-stu-id="fa5f9-159">From T2 run:</span></span>

##### <a name="on-the-debian-family"></a><span data-ttu-id="fa5f9-160">On the Debian Family</span><span class="sxs-lookup"><span data-stu-id="fa5f9-160">On the Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a><span data-ttu-id="fa5f9-161">On the RedHat Family</span><span class="sxs-lookup"><span data-stu-id="fa5f9-161">On the RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="fa5f9-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="fa5f9-163">With only SSH Keys allowed you will be able to login faster and much more secure.</span><span class="sxs-lookup"><span data-stu-id="fa5f9-163">With only SSH Keys allowed you will be able to login faster and much more secure.</span></span>

