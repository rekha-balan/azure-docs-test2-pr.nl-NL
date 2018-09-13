---
title: Add a user to a Linux VM on Azure | Microsoft Docs
description: Add a user to a Linux VM on Azure.
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: a95157f57c0cbd1f2a9ed68a0fe83140d7c9ec40
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564684"
---
# <a name="add-a-user-to-an-azure-vm"></a><span data-ttu-id="0e7b6-103">Add a user to an Azure VM</span><span class="sxs-lookup"><span data-stu-id="0e7b6-103">Add a user to an Azure VM</span></span>
<span data-ttu-id="0e7b6-104">One of the first tasks on any new Linux VM is to create a new user.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-104">One of the first tasks on any new Linux VM is to create a new user.</span></span>  <span data-ttu-id="0e7b6-105">In this article, we walk through creating a sudo user account, setting the password, adding SSH Public Keys, and finally use `visudo` to allow sudo without a password.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-105">In this article, we walk through creating a sudo user account, setting the password, adding SSH Public Keys, and finally use `visudo` to allow sudo without a password.</span></span>

<span data-ttu-id="0e7b6-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and the Azure CLI installed and switched to Azure Resource Manager mode using `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and the Azure CLI installed and switched to Azure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0e7b6-107">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="0e7b6-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy the SSH Public Key to the new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers to allow no password
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify the SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0e7b6-108">Detailed Walkthrough</span><span class="sxs-lookup"><span data-stu-id="0e7b6-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="0e7b6-109">Introduction</span><span class="sxs-lookup"><span data-stu-id="0e7b6-109">Introduction</span></span>
<span data-ttu-id="0e7b6-110">One of the first and most common task with a new server is to add a user account.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-110">One of the first and most common task with a new server is to add a user account.</span></span>  <span data-ttu-id="0e7b6-111">Root logins should be disabled and the root account itself should not be used with your Linux server, only sudo.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-111">Root logins should be disabled and the root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="0e7b6-112">Giving a user root escalation privileges using sudo it the proper way to administer and use Linux.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-112">Giving a user root escalation privileges using sudo it the proper way to administer and use Linux.</span></span>

<span data-ttu-id="0e7b6-113">Using the command `useradd` we are adding user accounts to the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-113">Using the command `useradd` we are adding user accounts to the Linux VM.</span></span>  <span data-ttu-id="0e7b6-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="0e7b6-115">We are adding a command-line flag to the `useradd` command to also add the new user to the proper sudo group on Linux.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-115">We are adding a command-line flag to the `useradd` command to also add the new user to the proper sudo group on Linux.</span></span>  <span data-ttu-id="0e7b6-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give the new user account a password.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give the new user account a password.</span></span>  <span data-ttu-id="0e7b6-117">We are creating an initial password for the new user using the simple `passwd` command.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-117">We are creating an initial password for the new user using the simple `passwd` command.</span></span>  <span data-ttu-id="0e7b6-118">The last step is to modify the sudo rules to allow that user to execute commands with sudo privileges without having to enter a password for every command.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-118">The last step is to modify the sudo rules to allow that user to execute commands with sudo privileges without having to enter a password for every command.</span></span>  <span data-ttu-id="0e7b6-119">Logging in using the Private key we are assuming that user account is safe from bad actors and are going to allow sudo access without a password.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-119">Logging in using the Private key we are assuming that user account is safe from bad actors and are going to allow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-to-an-azure-vm"></a><span data-ttu-id="0e7b6-120">Adding a single sudo user to an Azure VM</span><span class="sxs-lookup"><span data-stu-id="0e7b6-120">Adding a single sudo user to an Azure VM</span></span>
<span data-ttu-id="0e7b6-121">Log in to the Azure VM using SSH keys.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-121">Log in to the Azure VM using SSH keys.</span></span>  <span data-ttu-id="0e7b6-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="0e7b6-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="0e7b6-123">The `useradd` command completes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="0e7b6-123">The `useradd` command completes the following tasks:</span></span>

* <span data-ttu-id="0e7b6-124">create a new user account</span><span class="sxs-lookup"><span data-stu-id="0e7b6-124">create a new user account</span></span>
* <span data-ttu-id="0e7b6-125">create a new user group with the same name</span><span class="sxs-lookup"><span data-stu-id="0e7b6-125">create a new user group with the same name</span></span>
* <span data-ttu-id="0e7b6-126">add a blank entry to `/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="0e7b6-126">add a blank entry to `/etc/passwd`</span></span>
* <span data-ttu-id="0e7b6-127">add a blank entry to `/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="0e7b6-127">add a blank entry to `/etc/gpasswd`</span></span>

<span data-ttu-id="0e7b6-128">The `-G` command-line flag adds the new user account to the proper Linux group giving the new user account root escalation privileges.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-128">The `-G` command-line flag adds the new user account to the proper Linux group giving the new user account root escalation privileges.</span></span>

#### <a name="add-the-user"></a><span data-ttu-id="0e7b6-129">Add the user</span><span class="sxs-lookup"><span data-stu-id="0e7b6-129">Add the user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="0e7b6-130">Set a password</span><span class="sxs-lookup"><span data-stu-id="0e7b6-130">Set a password</span></span>
<span data-ttu-id="0e7b6-131">The `useradd` command creates the user and adds an entry to both `/etc/passwd` and `/etc/gpasswd` but does not actually set the password.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-131">The `useradd` command creates the user and adds an entry to both `/etc/passwd` and `/etc/gpasswd` but does not actually set the password.</span></span>  <span data-ttu-id="0e7b6-132">The password is added to the entry using the `passwd` command.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-132">The password is added to the entry using the `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="0e7b6-133">We now have a user with sudo privileges on the server.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-133">We now have a user with sudo privileges on the server.</span></span>

### <a name="add-your-ssh-public-key-to-the-new-user-account"></a><span data-ttu-id="0e7b6-134">Add your SSH Public Key to the new user account</span><span class="sxs-lookup"><span data-stu-id="0e7b6-134">Add your SSH Public Key to the new user account</span></span>
<span data-ttu-id="0e7b6-135">From your machine, use the `ssh-copy-id` command with the new password.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-135">From your machine, use the `ssh-copy-id` command with the new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-to-allow-sudo-usage-without-a-password"></a><span data-ttu-id="0e7b6-136">Using visudo to allow sudo usage without a password</span><span class="sxs-lookup"><span data-stu-id="0e7b6-136">Using visudo to allow sudo usage without a password</span></span>
<span data-ttu-id="0e7b6-137">Using `visudo` to edit the `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-137">Using `visudo` to edit the `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="0e7b6-138">Upon executing `visudo`, the `/etc/sudoers` file is locked to ensure no other user can make changes while it is actively being edited.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-138">Upon executing `visudo`, the `/etc/sudoers` file is locked to ensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="0e7b6-139">The `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt to save or exit so you cannot save a broken sudoers file.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-139">The `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt to save or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="0e7b6-140">We already have users in the correct default group for sudo access.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-140">We already have users in the correct default group for sudo access.</span></span>  <span data-ttu-id="0e7b6-141">Now we are going to enable those groups to use sudo with no password.</span><span class="sxs-lookup"><span data-stu-id="0e7b6-141">Now we are going to enable those groups to use sudo with no password.</span></span>

```bash
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-the-user-ssh-keys-and-sudo"></a><span data-ttu-id="0e7b6-142">Verify the user, ssh keys, and sudo</span><span class="sxs-lookup"><span data-stu-id="0e7b6-142">Verify the user, ssh keys, and sudo</span></span>
```bash
# Verify the SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
