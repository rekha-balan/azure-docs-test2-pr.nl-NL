---
title: Create an SSH key pair for Linux VMs on Azure | Microsoft Docs
description: Securely create an SSH public and private key pair for Azure Linux VMs.
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: ''
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: 4dcfdc9ebd26cdf610a6e04a35a66e4aa3c25c05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554957"
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="93c9f-103">Create an SSH public and private key pair for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="93c9f-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="93c9f-104">This article shows you how to generate an SSH protocol version 2 RSA public and private key file pair to use with Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="93c9f-104">This article shows you how to generate an SSH protocol version 2 RSA public and private key file pair to use with Linux VMs.</span></span>  <span data-ttu-id="93c9f-105">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span><span class="sxs-lookup"><span data-stu-id="93c9f-105">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span>  <span data-ttu-id="93c9f-106">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span><span class="sxs-lookup"><span data-stu-id="93c9f-106">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="93c9f-107">VMs created with Azure Templates or the `azure-cli` can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span><span class="sxs-lookup"><span data-stu-id="93c9f-107">VMs created with Azure Templates or the `azure-cli` can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="93c9f-108">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="93c9f-108">Quick Commands</span></span>

<span data-ttu-id="93c9f-109">Run the following commands from a Bash shell, replacing the examples with your own choices.</span><span class="sxs-lookup"><span data-stu-id="93c9f-109">Run the following commands from a Bash shell, replacing the examples with your own choices.</span></span>

<span data-ttu-id="93c9f-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="93c9f-111">When prompted using the following command, you should create a "passphrase" to secure your private key.</span><span class="sxs-lookup"><span data-stu-id="93c9f-111">When prompted using the following command, you should create a "passphrase" to secure your private key.</span></span> <span data-ttu-id="93c9f-112">(The passphrase is a password used to encrypt your private key.)</span><span class="sxs-lookup"><span data-stu-id="93c9f-112">(The passphrase is a password used to encrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="93c9f-113">Add the newly created key to `ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="93c9f-113">Add the newly created key to `ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="93c9f-114">The above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as the environment can be radically constrained.</span><span class="sxs-lookup"><span data-stu-id="93c9f-114">The above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as the environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="93c9f-115">Detailed Walkthrough</span><span class="sxs-lookup"><span data-stu-id="93c9f-115">Detailed Walkthrough</span></span>

<span data-ttu-id="93c9f-116">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span><span class="sxs-lookup"><span data-stu-id="93c9f-116">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="93c9f-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span><span class="sxs-lookup"><span data-stu-id="93c9f-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93c9f-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span><span class="sxs-lookup"><span data-stu-id="93c9f-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="93c9f-119">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span><span class="sxs-lookup"><span data-stu-id="93c9f-119">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="93c9f-120">This password is just to access the private SSH key and **is not** the user account password.</span><span class="sxs-lookup"><span data-stu-id="93c9f-120">This password is just to access the private SSH key and **is not** the user account password.</span></span>  <span data-ttu-id="93c9f-121">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span><span class="sxs-lookup"><span data-stu-id="93c9f-121">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="93c9f-122">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span><span class="sxs-lookup"><span data-stu-id="93c9f-122">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="93c9f-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span><span class="sxs-lookup"><span data-stu-id="93c9f-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="93c9f-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on the Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="93c9f-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on the Resource Manager.</span></span>  <span data-ttu-id="93c9f-125">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span><span class="sxs-lookup"><span data-stu-id="93c9f-125">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="93c9f-126">Disable SSH passwords by using SSH keys</span><span class="sxs-lookup"><span data-stu-id="93c9f-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="93c9f-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span><span class="sxs-lookup"><span data-stu-id="93c9f-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="93c9f-128">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span><span class="sxs-lookup"><span data-stu-id="93c9f-128">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="93c9f-129">When an Azure VM is created, the public key is copied to `~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-129">When an Azure VM is created, the public key is copied to `~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="93c9f-130">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span><span class="sxs-lookup"><span data-stu-id="93c9f-130">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="93c9f-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span><span class="sxs-lookup"><span data-stu-id="93c9f-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="93c9f-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the sshd_config config file.</span><span class="sxs-lookup"><span data-stu-id="93c9f-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="93c9f-133">Using ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="93c9f-133">Using ssh-keygen</span></span>

<span data-ttu-id="93c9f-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span><span class="sxs-lookup"><span data-stu-id="93c9f-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="93c9f-135">SSH keys are by default kept in the `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="93c9f-135">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="93c9f-136">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span><span class="sxs-lookup"><span data-stu-id="93c9f-136">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="93c9f-137">*Command explained*</span><span class="sxs-lookup"><span data-stu-id="93c9f-137">*Command explained*</span></span>

<span data-ttu-id="93c9f-138">`ssh-keygen` = the program used to create the keys</span><span class="sxs-lookup"><span data-stu-id="93c9f-138">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="93c9f-139">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="93c9f-139">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="93c9f-140">`-b 2048` = bits of the key</span><span class="sxs-lookup"><span data-stu-id="93c9f-140">`-b 2048` = bits of the key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="93c9f-141">Classic portal and X.509 certs</span><span class="sxs-lookup"><span data-stu-id="93c9f-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="93c9f-142">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for the SSH keys.</span><span class="sxs-lookup"><span data-stu-id="93c9f-142">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for the SSH keys.</span></span>  <span data-ttu-id="93c9f-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span><span class="sxs-lookup"><span data-stu-id="93c9f-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="93c9f-144">To create an X.509 cert from your existing SSH-RSA private key:</span><span class="sxs-lookup"><span data-stu-id="93c9f-144">To create an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="93c9f-145">Classic deploy using `asm`</span><span class="sxs-lookup"><span data-stu-id="93c9f-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="93c9f-146">If you are using the classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span><span class="sxs-lookup"><span data-stu-id="93c9f-146">If you are using the classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="93c9f-147">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-147">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="93c9f-148">To create a RFC4716 formatted key from an existing SSH public key:</span><span class="sxs-lookup"><span data-stu-id="93c9f-148">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="93c9f-149">Example of ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="93c9f-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
The keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="93c9f-150">Saved key files:</span><span class="sxs-lookup"><span data-stu-id="93c9f-150">Saved key files:</span></span>

`Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="93c9f-151">The key pair name for this article.</span><span class="sxs-lookup"><span data-stu-id="93c9f-151">The key pair name for this article.</span></span>  <span data-ttu-id="93c9f-152">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span><span class="sxs-lookup"><span data-stu-id="93c9f-152">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="93c9f-153">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span><span class="sxs-lookup"><span data-stu-id="93c9f-153">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="93c9f-154">If not specified with a full path, `ssh-keygen` will create the keys in the current working directory, not the default `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-154">If not specified with a full path, `ssh-keygen` will create the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="93c9f-155">A listing of the `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="93c9f-155">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="93c9f-156">Key Password:</span><span class="sxs-lookup"><span data-stu-id="93c9f-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="93c9f-157">`ssh-keygen` refers to a password used to encrypt the private key as "a passphrase."</span><span class="sxs-lookup"><span data-stu-id="93c9f-157">`ssh-keygen` refers to a password used to encrypt the private key as "a passphrase."</span></span>  <span data-ttu-id="93c9f-158">It is *strongly* recommended to add a passphrase to your key pairs.</span><span class="sxs-lookup"><span data-stu-id="93c9f-158">It is *strongly* recommended to add a passphrase to your key pairs.</span></span> <span data-ttu-id="93c9f-159">Without a passphrase protecting the private key, anyone with the key file can use it to log in to any server that has the corresponding public key.</span><span class="sxs-lookup"><span data-stu-id="93c9f-159">Without a passphrase protecting the private key, anyone with the key file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="93c9f-160">Adding a passphrase offers more protection in case someone is able to gain access to your private key file, giving you time to change the keys used to authenticate you.</span><span class="sxs-lookup"><span data-stu-id="93c9f-160">Adding a passphrase offers more protection in case someone is able to gain access to your private key file, giving you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="93c9f-161">Using ssh-agent to store your private key password</span><span class="sxs-lookup"><span data-stu-id="93c9f-161">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="93c9f-162">To avoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` to cache your private key file password.</span><span class="sxs-lookup"><span data-stu-id="93c9f-162">To avoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="93c9f-163">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-163">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="93c9f-164">Verify and use `ssh-agent` and `ssh-add` to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span><span class="sxs-lookup"><span data-stu-id="93c9f-164">Verify and use `ssh-agent` and `ssh-add` to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="93c9f-165">Now add the private key to `ssh-agent` using the command `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-165">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="93c9f-166">The private key password is now stored in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-166">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-install-the-new-key"></a><span data-ttu-id="93c9f-167">Using `ssh-copy-id` to install the new key</span><span class="sxs-lookup"><span data-stu-id="93c9f-167">Using `ssh-copy-id` to install the new key</span></span>
<span data-ttu-id="93c9f-168">If you have already created a VM you can install the new SSH public key to your Linux VM with the following command, replacing the VM username and the server address with your own values:</span><span class="sxs-lookup"><span data-stu-id="93c9f-168">If you have already created a VM you can install the new SSH public key to your Linux VM with the following command, replacing the VM username and the server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="93c9f-169">Create and configure an SSH config file</span><span class="sxs-lookup"><span data-stu-id="93c9f-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="93c9f-170">It is a best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span><span class="sxs-lookup"><span data-stu-id="93c9f-170">It is a best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="93c9f-171">The following example shows a standard configuration.</span><span class="sxs-lookup"><span data-stu-id="93c9f-171">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="93c9f-172">Create the file</span><span class="sxs-lookup"><span data-stu-id="93c9f-172">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="93c9f-173">Edit the file to add the new SSH configuration:</span><span class="sxs-lookup"><span data-stu-id="93c9f-173">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="93c9f-174">Example `~/.ssh/config` file:</span><span class="sxs-lookup"><span data-stu-id="93c9f-174">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="93c9f-175">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span><span class="sxs-lookup"><span data-stu-id="93c9f-175">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="93c9f-176">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span><span class="sxs-lookup"><span data-stu-id="93c9f-176">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="93c9f-177">Config file explained</span><span class="sxs-lookup"><span data-stu-id="93c9f-177">Config file explained</span></span>

<span data-ttu-id="93c9f-178">`Host` = the name of the host being called on the terminal.</span><span class="sxs-lookup"><span data-stu-id="93c9f-178">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="93c9f-179">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span><span class="sxs-lookup"><span data-stu-id="93c9f-179">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="93c9f-180">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span><span class="sxs-lookup"><span data-stu-id="93c9f-180">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="93c9f-181">`User ahmet` = the remote user account to use when logging in to the server.</span><span class="sxs-lookup"><span data-stu-id="93c9f-181">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="93c9f-182">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span><span class="sxs-lookup"><span data-stu-id="93c9f-182">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="93c9f-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span><span class="sxs-lookup"><span data-stu-id="93c9f-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="93c9f-184">SSH into Linux without a password</span><span class="sxs-lookup"><span data-stu-id="93c9f-184">SSH into Linux without a password</span></span>

<span data-ttu-id="93c9f-185">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span><span class="sxs-lookup"><span data-stu-id="93c9f-185">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="93c9f-186">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span><span class="sxs-lookup"><span data-stu-id="93c9f-186">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="93c9f-187">Command explained</span><span class="sxs-lookup"><span data-stu-id="93c9f-187">Command explained</span></span>

<span data-ttu-id="93c9f-188">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="93c9f-188">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93c9f-189">Next Steps</span><span class="sxs-lookup"><span data-stu-id="93c9f-189">Next Steps</span></span>

<span data-ttu-id="93c9f-190">Next up is to create Azure Linux VMs using the new SSH public key.</span><span class="sxs-lookup"><span data-stu-id="93c9f-190">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="93c9f-191">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span><span class="sxs-lookup"><span data-stu-id="93c9f-191">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="93c9f-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span><span class="sxs-lookup"><span data-stu-id="93c9f-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="93c9f-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="93c9f-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="93c9f-194">Create a secure Linux VM using an Azure template</span><span class="sxs-lookup"><span data-stu-id="93c9f-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="93c9f-195">Create a secure Linux VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="93c9f-195">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="93c9f-196">Create a secure Linux VM using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93c9f-196">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
