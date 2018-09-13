---
title: Configure SSHD on Azure Linux Virtual Machines | Microsoft Docs
description: Configure SSHD for security best practices and to lockdown SSH to Azure Linux Virtual Machines.
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: 6119e396c9c3773c891c986a0340de31ad2674fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549686"
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="5d072-103">Configure SSHD on Azure Linux VMs</span><span class="sxs-lookup"><span data-stu-id="5d072-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="5d072-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span><span class="sxs-lookup"><span data-stu-id="5d072-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="5d072-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span><span class="sxs-lookup"><span data-stu-id="5d072-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="5d072-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d072-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="5d072-107">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="5d072-107">Quick Commands</span></span>

<span data-ttu-id="5d072-108">Configure `/etc/ssh/sshd_config` with the following settings:</span><span class="sxs-lookup"><span data-stu-id="5d072-108">Configure `/etc/ssh/sshd_config` with the following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="5d072-109">Disable password logins</span><span class="sxs-lookup"><span data-stu-id="5d072-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a><span data-ttu-id="5d072-110">Disable login by the root user</span><span class="sxs-lookup"><span data-stu-id="5d072-110">Disable login by the root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="5d072-111">Allowed groups list</span><span class="sxs-lookup"><span data-stu-id="5d072-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="5d072-112">Allowed users list</span><span class="sxs-lookup"><span data-stu-id="5d072-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="5d072-113">Disable SSH protocol version 1</span><span class="sxs-lookup"><span data-stu-id="5d072-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="5d072-114">Minimum key bits</span><span class="sxs-lookup"><span data-stu-id="5d072-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="5d072-115">Disconnect idle users</span><span class="sxs-lookup"><span data-stu-id="5d072-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="5d072-116">Detailed Walkthrough</span><span class="sxs-lookup"><span data-stu-id="5d072-116">Detailed Walkthrough</span></span>

<span data-ttu-id="5d072-117">SSHD is the SSH Server that runs on the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5d072-117">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="5d072-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span><span class="sxs-lookup"><span data-stu-id="5d072-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="5d072-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span><span class="sxs-lookup"><span data-stu-id="5d072-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="5d072-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span><span class="sxs-lookup"><span data-stu-id="5d072-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span></span>  <span data-ttu-id="5d072-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span><span class="sxs-lookup"><span data-stu-id="5d072-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span></span>  <span data-ttu-id="5d072-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span><span class="sxs-lookup"><span data-stu-id="5d072-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="5d072-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d072-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5d072-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span><span class="sxs-lookup"><span data-stu-id="5d072-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="5d072-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span><span class="sxs-lookup"><span data-stu-id="5d072-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="5d072-126">We use the second terminal to test those changes once the service is restarted.</span><span class="sxs-lookup"><span data-stu-id="5d072-126">We use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="5d072-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span><span class="sxs-lookup"><span data-stu-id="5d072-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="5d072-128">Disable password logins</span><span class="sxs-lookup"><span data-stu-id="5d072-128">Disable password logins</span></span>

<span data-ttu-id="5d072-129">The quickest way to secure you Linux VM is to disable password logins.</span><span class="sxs-lookup"><span data-stu-id="5d072-129">The quickest way to secure you Linux VM is to disable password logins.</span></span>  <span data-ttu-id="5d072-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span><span class="sxs-lookup"><span data-stu-id="5d072-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span></span>  <span data-ttu-id="5d072-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span><span class="sxs-lookup"><span data-stu-id="5d072-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a><span data-ttu-id="5d072-132">Disable login by the root user</span><span class="sxs-lookup"><span data-stu-id="5d072-132">Disable login by the root user</span></span>

<span data-ttu-id="5d072-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="5d072-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="5d072-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span><span class="sxs-lookup"><span data-stu-id="5d072-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="5d072-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span><span class="sxs-lookup"><span data-stu-id="5d072-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="5d072-136">Allowed groups list</span><span class="sxs-lookup"><span data-stu-id="5d072-136">Allowed groups list</span></span>

<span data-ttu-id="5d072-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span><span class="sxs-lookup"><span data-stu-id="5d072-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="5d072-138">This feature uses lists to approve or deny specific users and groups from logging in.</span><span class="sxs-lookup"><span data-stu-id="5d072-138">This feature uses lists to approve or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="5d072-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span><span class="sxs-lookup"><span data-stu-id="5d072-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="5d072-140">Allowed users list</span><span class="sxs-lookup"><span data-stu-id="5d072-140">Allowed users list</span></span>

<span data-ttu-id="5d072-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span><span class="sxs-lookup"><span data-stu-id="5d072-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="5d072-142">Disable SSH protocol version 1</span><span class="sxs-lookup"><span data-stu-id="5d072-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="5d072-143">SSH protocol version 1 is insecure and should be disabled.</span><span class="sxs-lookup"><span data-stu-id="5d072-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="5d072-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span><span class="sxs-lookup"><span data-stu-id="5d072-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span></span>  <span data-ttu-id="5d072-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span><span class="sxs-lookup"><span data-stu-id="5d072-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span></span>  <span data-ttu-id="5d072-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span><span class="sxs-lookup"><span data-stu-id="5d072-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="5d072-147">Minimum key bits</span><span class="sxs-lookup"><span data-stu-id="5d072-147">Minimum key bits</span></span>

<span data-ttu-id="5d072-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span><span class="sxs-lookup"><span data-stu-id="5d072-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span></span>  <span data-ttu-id="5d072-149">These SSH keys can be created using different length keys, measured in bits.</span><span class="sxs-lookup"><span data-stu-id="5d072-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="5d072-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span><span class="sxs-lookup"><span data-stu-id="5d072-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span></span>  <span data-ttu-id="5d072-151">Keys of less than 2048 bits could theoretically be broken.</span><span class="sxs-lookup"><span data-stu-id="5d072-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="5d072-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="5d072-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="5d072-153">Disconnect idle users</span><span class="sxs-lookup"><span data-stu-id="5d072-153">Disconnect idle users</span></span>

<span data-ttu-id="5d072-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span><span class="sxs-lookup"><span data-stu-id="5d072-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="5d072-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5d072-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="5d072-156">Restart SSHD</span><span class="sxs-lookup"><span data-stu-id="5d072-156">Restart SSHD</span></span>

<span data-ttu-id="5d072-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span><span class="sxs-lookup"><span data-stu-id="5d072-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span></span>  <span data-ttu-id="5d072-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span><span class="sxs-lookup"><span data-stu-id="5d072-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span></span>  <span data-ttu-id="5d072-159">To test the new SSH server settings use a second terminal window or tab.  Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span><span class="sxs-lookup"><span data-stu-id="5d072-159">To test the new SSH server settings use a second terminal window or tab.  Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="5d072-160">On Redhat, Centos and Fedora</span><span class="sxs-lookup"><span data-stu-id="5d072-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="5d072-161">On Debian & Ubuntu</span><span class="sxs-lookup"><span data-stu-id="5d072-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="5d072-162">Reset SSHD using Azure reset-access</span><span class="sxs-lookup"><span data-stu-id="5d072-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="5d072-163">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span><span class="sxs-lookup"><span data-stu-id="5d072-163">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span></span>

<span data-ttu-id="5d072-164">Replace any example names with your own.</span><span class="sxs-lookup"><span data-stu-id="5d072-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="5d072-165">Install Fail2ban</span><span class="sxs-lookup"><span data-stu-id="5d072-165">Install Fail2ban</span></span>

<span data-ttu-id="5d072-166">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span><span class="sxs-lookup"><span data-stu-id="5d072-166">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="5d072-167">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span><span class="sxs-lookup"><span data-stu-id="5d072-167">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span></span>

* [<span data-ttu-id="5d072-168">Fail2ban homepage</span><span class="sxs-lookup"><span data-stu-id="5d072-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="5d072-169">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5d072-169">Next Steps</span></span>

<span data-ttu-id="5d072-170">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span><span class="sxs-lookup"><span data-stu-id="5d072-170">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="5d072-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="5d072-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="5d072-172">Encrypt disks on a Linux VM using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5d072-172">Encrypt disks on a Linux VM using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="5d072-173">Access and security in Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="5d072-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
