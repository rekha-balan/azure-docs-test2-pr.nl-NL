---
title: Create and use an SSH key pair for Linux VMs in Azure | Microsoft Docs
description: How to create and use an SSH public and private key pair for Linux VMs in Azure to improve the security of the authentication process.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 9dc30b7d60e69307ed0679bf1759bc7c785bbd86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553373"
---
# <a name="how-to-create-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="f198a-103">How to create and use an SSH public and private key pair for Linux VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="f198a-103">How to create and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="f198a-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating the need for passwords to log in.</span><span class="sxs-lookup"><span data-stu-id="f198a-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="f198a-105">This article shows you how to quickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="f198a-105">This article shows you how to quickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="f198a-106">For more detailed steps and additional examples, such as for use with the classic portal, see [detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="f198a-106">For more detailed steps and additional examples, such as for use with the classic portal, see [detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="f198a-107">Create an SSH key pair</span><span class="sxs-lookup"><span data-stu-id="f198a-107">Create an SSH key pair</span></span>
<span data-ttu-id="f198a-108">Use the `ssh-keygen` command to create SSH public and private key files that are by default created in the `~/.ssh` directory, but you can specify a different location and additional passphrase (a password to access the private key file) when prompted.</span><span class="sxs-lookup"><span data-stu-id="f198a-108">Use the `ssh-keygen` command to create SSH public and private key files that are by default created in the `~/.ssh` directory, but you can specify a different location and additional passphrase (a password to access the private key file) when prompted.</span></span> <span data-ttu-id="f198a-109">Run the following command from a Bash shell, answering the prompts with your own information.</span><span class="sxs-lookup"><span data-stu-id="f198a-109">Run the following command from a Bash shell, answering the prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

## <a name="use-the-ssh-key-pair"></a><span data-ttu-id="f198a-110">Use the SSH key pair</span><span class="sxs-lookup"><span data-stu-id="f198a-110">Use the SSH key pair</span></span>
<span data-ttu-id="f198a-111">The public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed the location when you created them.</span><span class="sxs-lookup"><span data-stu-id="f198a-111">The public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed the location when you created them.</span></span> <span data-ttu-id="f198a-112">If you use the [Azure CLI 2.0](/cli/azure) to create your VM, specify the location of this public key when you use the [az vm create](/cli/azure/vm#create) with the `--ssh-key-path` option.</span><span class="sxs-lookup"><span data-stu-id="f198a-112">If you use the [Azure CLI 2.0](/cli/azure) to create your VM, specify the location of this public key when you use the [az vm create](/cli/azure/vm#create) with the `--ssh-key-path` option.</span></span> <span data-ttu-id="f198a-113">If you copy and paste the contents of the public key file to use in the Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span><span class="sxs-lookup"><span data-stu-id="f198a-113">If you copy and paste the contents of the public key file to use in the Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="f198a-114">For example, if you use OS X, you can pipe the public key file (by default, **~/.ssh/id_rsa.pub**) to **pbcopy** to copy the contents (there are other Linux programs that do the same thing, such as `xclip`).</span><span class="sxs-lookup"><span data-stu-id="f198a-114">For example, if you use OS X, you can pipe the public key file (by default, **~/.ssh/id_rsa.pub**) to **pbcopy** to copy the contents (there are other Linux programs that do the same thing, such as `xclip`).</span></span> 

<span data-ttu-id="f198a-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span><span class="sxs-lookup"><span data-stu-id="f198a-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="f198a-116">With the public key on your Azure VM, SSH to your VM using the IP address or DNS name of your VM (remember to replace `azureuser` and `myvm.westus.cloudapp.azure.com` below with the admin username and the fully qualified domain name -- or IP address):</span><span class="sxs-lookup"><span data-stu-id="f198a-116">With the public key on your Azure VM, SSH to your VM using the IP address or DNS name of your VM (remember to replace `azureuser` and `myvm.westus.cloudapp.azure.com` below with the admin username and the fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="f198a-117">If you provided a passphrase when you created your key pair, enter the passphrase when prompted during the login process.</span><span class="sxs-lookup"><span data-stu-id="f198a-117">If you provided a passphrase when you created your key pair, enter the passphrase when prompted during the login process.</span></span> <span data-ttu-id="f198a-118">(The server is added to your `~/.ssh/known_hosts` folder, and you won't be asked to connect again until the public key on your Azure VM changes or the server name is removed from `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="f198a-118">(The server is added to your `~/.ssh/known_hosts` folder, and you won't be asked to connect again until the public key on your Azure VM changes or the server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f198a-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="f198a-119">Next steps</span></span>

<span data-ttu-id="f198a-120">VMs created using SSH keys are by default configured with passwords disabled, to make brute-forced guessing attempts vastly more expensive and therefore difficult.</span><span class="sxs-lookup"><span data-stu-id="f198a-120">VMs created using SSH keys are by default configured with passwords disabled, to make brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="f198a-121">This topic describes creating a simple SSH key pair for quick usage.</span><span class="sxs-lookup"><span data-stu-id="f198a-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="f198a-122">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="f198a-122">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="f198a-123">You can create VMs that use your SSH key pair using the Azure portal, CLI, and templates:</span><span class="sxs-lookup"><span data-stu-id="f198a-123">You can create VMs that use your SSH key pair using the Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="f198a-124">Create a secure Linux VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f198a-124">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f198a-125">Create a secure Linux VM using the Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="f198a-125">Create a secure Linux VM using the Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f198a-126">Create a secure Linux VM using an Azure template</span><span class="sxs-lookup"><span data-stu-id="f198a-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
