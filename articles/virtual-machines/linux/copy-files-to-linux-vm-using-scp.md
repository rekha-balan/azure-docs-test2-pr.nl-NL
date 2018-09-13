---
title: Moving files to and from a Linux VM using SCP | Microsoft Docs
description: Securely moving files to and from a Linux VM using SCP and an SSH key pair.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: vlivech
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: 33a26679ce655f4abcf104d30f9c14abe7875405
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555695"
---
# <a name="moving-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="efae5-103">Moving files to and from a Linux VM using SCP</span><span class="sxs-lookup"><span data-stu-id="efae5-103">Moving files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="efae5-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span><span class="sxs-lookup"><span data-stu-id="efae5-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span>  <span data-ttu-id="efae5-105">For an example, we are moving Azure configuration files up to a Linux VM and pulling down a log file directory, both using SCP and SSH keys.</span><span class="sxs-lookup"><span data-stu-id="efae5-105">For an example, we are moving Azure configuration files up to a Linux VM and pulling down a log file directory, both using SCP and SSH keys.</span></span>   

<span data-ttu-id="efae5-106">For this article, the requirements are:</span><span class="sxs-lookup"><span data-stu-id="efae5-106">For this article, the requirements are:</span></span>

- [<span data-ttu-id="efae5-107">an Azure account</span><span class="sxs-lookup"><span data-stu-id="efae5-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="efae5-108">SSH public and private key files</span><span class="sxs-lookup"><span data-stu-id="efae5-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="efae5-109">Quick commands</span><span class="sxs-lookup"><span data-stu-id="efae5-109">Quick commands</span></span>

<span data-ttu-id="efae5-110">Copy a file up to the Linux VM</span><span class="sxs-lookup"><span data-stu-id="efae5-110">Copy a file up to the Linux VM</span></span>

```bash
scp file user@host:directory/targetfile
```

<span data-ttu-id="efae5-111">Copy a file down from the Linux VM</span><span class="sxs-lookup"><span data-stu-id="efae5-111">Copy a file down from the Linux VM</span></span>

```bash
scp user@host:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="efae5-112">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="efae5-112">Detailed walkthrough</span></span>

<span data-ttu-id="efae5-113">Moving files back and forth between your workstation and a Linux VM, quickly and securely, is a critical part of managing your Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="efae5-113">Moving files back and forth between your workstation and a Linux VM, quickly and securely, is a critical part of managing your Azure infrastructure.</span></span>  <span data-ttu-id="efae5-114">For this article we walk through using SCP, a tool built on top of SSH, and included in the default Bash shell of Linux, Mac and Windows.</span><span class="sxs-lookup"><span data-stu-id="efae5-114">For this article we walk through using SCP, a tool built on top of SSH, and included in the default Bash shell of Linux, Mac and Windows.</span></span>

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="efae5-115">SSH key pair authentication</span><span class="sxs-lookup"><span data-stu-id="efae5-115">SSH key pair authentication</span></span>

<span data-ttu-id="efae5-116">SCP uses SSH for the transport layer.</span><span class="sxs-lookup"><span data-stu-id="efae5-116">SCP uses SSH for the transport layer.</span></span>  <span data-ttu-id="efae5-117">By using SSH for the transport, SSH handles the authentication on the destination host while also moving the file in an encrypted tunnel provided by default with SSH.</span><span class="sxs-lookup"><span data-stu-id="efae5-117">By using SSH for the transport, SSH handles the authentication on the destination host while also moving the file in an encrypted tunnel provided by default with SSH.</span></span>  <span data-ttu-id="efae5-118">For SSH authentication, usernames and passwords can be used but SSH public and private key authentication are strongly recommended as a security best practice.</span><span class="sxs-lookup"><span data-stu-id="efae5-118">For SSH authentication, usernames and passwords can be used but SSH public and private key authentication are strongly recommended as a security best practice.</span></span> <span data-ttu-id="efae5-119">Once SSH has authenticated the connection, SCP then begins the process of copying the file.</span><span class="sxs-lookup"><span data-stu-id="efae5-119">Once SSH has authenticated the connection, SCP then begins the process of copying the file.</span></span>  <span data-ttu-id="efae5-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established without using a username and just using a server name.</span><span class="sxs-lookup"><span data-stu-id="efae5-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established without using a username and just using a server name.</span></span>  <span data-ttu-id="efae5-121">If you only have one SSH key, SCP will look for it in the `~/.ssh/` directory, and use it by default to login to the VM.</span><span class="sxs-lookup"><span data-stu-id="efae5-121">If you only have one SSH key, SCP will look for it in the `~/.ssh/` directory, and use it by default to login to the VM.</span></span>

<span data-ttu-id="efae5-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, follow this article, [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efae5-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, follow this article, [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="efae5-123">SCP a file to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="efae5-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="efae5-124">For the first example, we are copying an Azure credential file up to a Linux VM that is used to deploy automation.</span><span class="sxs-lookup"><span data-stu-id="efae5-124">For the first example, we are copying an Azure credential file up to a Linux VM that is used to deploy automation.</span></span>  <span data-ttu-id="efae5-125">Because this file contains Azure API credentials, which include secrets, security is important and the encrypted tunnel SSH provides, protects the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="efae5-125">Because this file contains Azure API credentials, which include secrets, security is important and the encrypted tunnel SSH provides, protects the contents of the file.</span></span>

```bash
scp ~/.azure/credentials myserver:/home/ahmet/.azure/credentials
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="efae5-126">SCP a directory from a Linux VM</span><span class="sxs-lookup"><span data-stu-id="efae5-126">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="efae5-127">For this example, we are copying a directory full of log files from the Linux VM down to your workstation.</span><span class="sxs-lookup"><span data-stu-id="efae5-127">For this example, we are copying a directory full of log files from the Linux VM down to your workstation.</span></span>  <span data-ttu-id="efae5-128">A log file may or may not contain sensitive or secret data and using SCP ensures the contents of the log files is encrypted.</span><span class="sxs-lookup"><span data-stu-id="efae5-128">A log file may or may not contain sensitive or secret data and using SCP ensures the contents of the log files is encrypted.</span></span>  <span data-ttu-id="efae5-129">Using SCP to securely transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span><span class="sxs-lookup"><span data-stu-id="efae5-129">Using SCP to securely transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

```bash
scp -r myserver:/home/ahmet/logs/ /tmp/.
```

<span data-ttu-id="efae5-130">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span><span class="sxs-lookup"><span data-stu-id="efae5-130">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="efae5-131">Also notice that the command-line syntax is similar to a `cp` copy command.</span><span class="sxs-lookup"><span data-stu-id="efae5-131">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efae5-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="efae5-132">Next steps</span></span>

* [<span data-ttu-id="efae5-133">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="efae5-133">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="efae5-134">Disable SSH passwords on your Linux VM by configuring SSHD</span><span class="sxs-lookup"><span data-stu-id="efae5-134">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>](mac-disable-ssh-password-usage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
