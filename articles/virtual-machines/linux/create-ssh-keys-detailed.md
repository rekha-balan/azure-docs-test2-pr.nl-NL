---
title: Detailed steps to create an SSH key pair for Linux VMs in Azure | Microsoft Docs
description: Learn additional steps to create an SSH public and private key pair for Linux VMs in Azure, along with specific certificates for different use cases.
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 2/6/2016
ms.author: rasquill
ms.openlocfilehash: 6afdc746e00ae8aedfb05ad2ad08280f8eec4caa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555638"
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="1cca8-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="1cca8-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="1cca8-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span><span class="sxs-lookup"><span data-stu-id="1cca8-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="1cca8-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span><span class="sxs-lookup"><span data-stu-id="1cca8-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="1cca8-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span><span class="sxs-lookup"><span data-stu-id="1cca8-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="1cca8-107">This article provides detailed steps and additional examples of generating certificates such as for use with the Classic portal.</span><span class="sxs-lookup"><span data-stu-id="1cca8-107">This article provides detailed steps and additional examples of generating certificates such as for use with the Classic portal.</span></span> <span data-ttu-id="1cca8-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="1cca8-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="1cca8-109">Understanding SSH keys</span><span class="sxs-lookup"><span data-stu-id="1cca8-109">Understanding SSH keys</span></span>

<span data-ttu-id="1cca8-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span><span class="sxs-lookup"><span data-stu-id="1cca8-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="1cca8-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span><span class="sxs-lookup"><span data-stu-id="1cca8-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="1cca8-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span><span class="sxs-lookup"><span data-stu-id="1cca8-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="1cca8-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span><span class="sxs-lookup"><span data-stu-id="1cca8-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="1cca8-114">This password is just to access the private SSH key file and **is not** the user account password.</span><span class="sxs-lookup"><span data-stu-id="1cca8-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="1cca8-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span><span class="sxs-lookup"><span data-stu-id="1cca8-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="1cca8-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span><span class="sxs-lookup"><span data-stu-id="1cca8-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="1cca8-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span><span class="sxs-lookup"><span data-stu-id="1cca8-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="1cca8-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1cca8-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="1cca8-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span><span class="sxs-lookup"><span data-stu-id="1cca8-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="1cca8-120">SSH keys use and benefits</span><span class="sxs-lookup"><span data-stu-id="1cca8-120">SSH keys use and benefits</span></span>

<span data-ttu-id="1cca8-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span><span class="sxs-lookup"><span data-stu-id="1cca8-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="1cca8-122">(The classic portal uses the `.pem` file format.</span><span class="sxs-lookup"><span data-stu-id="1cca8-122">(The classic portal uses the `.pem` file format.</span></span> <span data-ttu-id="1cca8-123">See ) To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span><span class="sxs-lookup"><span data-stu-id="1cca8-123">See ) To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="1cca8-124">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span><span class="sxs-lookup"><span data-stu-id="1cca8-124">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="1cca8-125">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span><span class="sxs-lookup"><span data-stu-id="1cca8-125">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="1cca8-126">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span><span class="sxs-lookup"><span data-stu-id="1cca8-126">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="1cca8-127">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span><span class="sxs-lookup"><span data-stu-id="1cca8-127">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="1cca8-128">Using ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1cca8-128">Using ssh-keygen</span></span>

<span data-ttu-id="1cca8-129">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span><span class="sxs-lookup"><span data-stu-id="1cca8-129">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="1cca8-130">SSH keys are by default kept in the `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="1cca8-130">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="1cca8-131">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span><span class="sxs-lookup"><span data-stu-id="1cca8-131">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="1cca8-132">*Command explained*</span><span class="sxs-lookup"><span data-stu-id="1cca8-132">*Command explained*</span></span>

<span data-ttu-id="1cca8-133">`ssh-keygen` = the program used to create the keys</span><span class="sxs-lookup"><span data-stu-id="1cca8-133">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="1cca8-134">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="1cca8-134">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="1cca8-135">`-b 2048` = bits of the key</span><span class="sxs-lookup"><span data-stu-id="1cca8-135">`-b 2048` = bits of the key</span></span>

<span data-ttu-id="1cca8-136">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span><span class="sxs-lookup"><span data-stu-id="1cca8-136">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="1cca8-137">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1cca8-137">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="1cca8-138">Classic portal and X.509 certs</span><span class="sxs-lookup"><span data-stu-id="1cca8-138">Classic portal and X.509 certs</span></span>

<span data-ttu-id="1cca8-139">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certificate .pem file for the SSH keys.</span><span class="sxs-lookup"><span data-stu-id="1cca8-139">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certificate .pem file for the SSH keys.</span></span>  <span data-ttu-id="1cca8-140">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span><span class="sxs-lookup"><span data-stu-id="1cca8-140">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="1cca8-141">To create an X.509 cert from your existing SSH-RSA private key:</span><span class="sxs-lookup"><span data-stu-id="1cca8-141">To create an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="1cca8-142">Classic deploy using `asm`</span><span class="sxs-lookup"><span data-stu-id="1cca8-142">Classic deploy using `asm`</span></span>

<span data-ttu-id="1cca8-143">If you are using the classic deploy model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span><span class="sxs-lookup"><span data-stu-id="1cca8-143">If you are using the classic deploy model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="1cca8-144">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="1cca8-144">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="1cca8-145">To create a RFC4716 formatted key from an existing SSH public key:</span><span class="sxs-lookup"><span data-stu-id="1cca8-145">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="1cca8-146">Example of ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1cca8-146">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
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

<span data-ttu-id="1cca8-147">Saved key files:</span><span class="sxs-lookup"><span data-stu-id="1cca8-147">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="1cca8-148">The key pair name for this article.</span><span class="sxs-lookup"><span data-stu-id="1cca8-148">The key pair name for this article.</span></span>  <span data-ttu-id="1cca8-149">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span><span class="sxs-lookup"><span data-stu-id="1cca8-149">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="1cca8-150">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span><span class="sxs-lookup"><span data-stu-id="1cca8-150">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="1cca8-151">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="1cca8-151">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="1cca8-152">A listing of the `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="1cca8-152">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="1cca8-153">Key Password:</span><span class="sxs-lookup"><span data-stu-id="1cca8-153">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="1cca8-154">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span><span class="sxs-lookup"><span data-stu-id="1cca8-154">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="1cca8-155">It is *strongly* recommended to add a password to your private key.</span><span class="sxs-lookup"><span data-stu-id="1cca8-155">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="1cca8-156">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span><span class="sxs-lookup"><span data-stu-id="1cca8-156">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="1cca8-157">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span><span class="sxs-lookup"><span data-stu-id="1cca8-157">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="1cca8-158">Using ssh-agent to store your private key password</span><span class="sxs-lookup"><span data-stu-id="1cca8-158">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="1cca8-159">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span><span class="sxs-lookup"><span data-stu-id="1cca8-159">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="1cca8-160">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1cca8-160">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="1cca8-161">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span><span class="sxs-lookup"><span data-stu-id="1cca8-161">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="1cca8-162">Now add the private key to `ssh-agent` using the command `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="1cca8-162">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="1cca8-163">The private key password is now stored in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1cca8-163">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="1cca8-164">Using `ssh-copy-id` to copy the key to an existing VM</span><span class="sxs-lookup"><span data-stu-id="1cca8-164">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="1cca8-165">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span><span class="sxs-lookup"><span data-stu-id="1cca8-165">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="1cca8-166">Create and configure an SSH config file</span><span class="sxs-lookup"><span data-stu-id="1cca8-166">Create and configure an SSH config file</span></span>

<span data-ttu-id="1cca8-167">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span><span class="sxs-lookup"><span data-stu-id="1cca8-167">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="1cca8-168">The following example shows a standard configuration.</span><span class="sxs-lookup"><span data-stu-id="1cca8-168">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="1cca8-169">Create the file</span><span class="sxs-lookup"><span data-stu-id="1cca8-169">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="1cca8-170">Edit the file to add the new SSH configuration:</span><span class="sxs-lookup"><span data-stu-id="1cca8-170">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="1cca8-171">Example `~/.ssh/config` file:</span><span class="sxs-lookup"><span data-stu-id="1cca8-171">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="1cca8-172">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span><span class="sxs-lookup"><span data-stu-id="1cca8-172">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="1cca8-173">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span><span class="sxs-lookup"><span data-stu-id="1cca8-173">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="1cca8-174">Config file explained</span><span class="sxs-lookup"><span data-stu-id="1cca8-174">Config file explained</span></span>

<span data-ttu-id="1cca8-175">`Host` = the name of the host being called on the terminal.</span><span class="sxs-lookup"><span data-stu-id="1cca8-175">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="1cca8-176">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span><span class="sxs-lookup"><span data-stu-id="1cca8-176">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="1cca8-177">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span><span class="sxs-lookup"><span data-stu-id="1cca8-177">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="1cca8-178">`User ahmet` = the remote user account to use when logging in to the server.</span><span class="sxs-lookup"><span data-stu-id="1cca8-178">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="1cca8-179">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span><span class="sxs-lookup"><span data-stu-id="1cca8-179">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="1cca8-180">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span><span class="sxs-lookup"><span data-stu-id="1cca8-180">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="1cca8-181">SSH into Linux without a password</span><span class="sxs-lookup"><span data-stu-id="1cca8-181">SSH into Linux without a password</span></span>

<span data-ttu-id="1cca8-182">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span><span class="sxs-lookup"><span data-stu-id="1cca8-182">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="1cca8-183">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span><span class="sxs-lookup"><span data-stu-id="1cca8-183">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="1cca8-184">Command explained</span><span class="sxs-lookup"><span data-stu-id="1cca8-184">Command explained</span></span>

<span data-ttu-id="1cca8-185">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="1cca8-185">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cca8-186">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1cca8-186">Next Steps</span></span>

<span data-ttu-id="1cca8-187">Next up is to create Azure Linux VMs using the new SSH public key.</span><span class="sxs-lookup"><span data-stu-id="1cca8-187">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="1cca8-188">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span><span class="sxs-lookup"><span data-stu-id="1cca8-188">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="1cca8-189">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span><span class="sxs-lookup"><span data-stu-id="1cca8-189">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="1cca8-190">Create a secure Linux VM using an Azure template</span><span class="sxs-lookup"><span data-stu-id="1cca8-190">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1cca8-191">Create a secure Linux VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1cca8-191">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1cca8-192">Create a secure Linux VM using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1cca8-192">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
