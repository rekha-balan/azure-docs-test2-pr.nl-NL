---
title: Join a RedHat Linux VM to an Azure Active Directory DS | Microsoft Docs
description: How to join an existing RedHat Enterprise Linux 7 VM to an Azure Active Directory Domain Service.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f02dc049444abec60c5b5b841aef22014a0bf685
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549494"
---
# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a><span data-ttu-id="c7992-103">Join a RedHat Linux VM to an Azure Active Directory Domain Service</span><span class="sxs-lookup"><span data-stu-id="c7992-103">Join a RedHat Linux VM to an Azure Active Directory Domain Service</span></span>

<span data-ttu-id="c7992-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.</span><span class="sxs-lookup"><span data-stu-id="c7992-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="c7992-105">The requirements are:</span><span class="sxs-lookup"><span data-stu-id="c7992-105">The requirements are:</span></span>

- [<span data-ttu-id="c7992-106">an Azure account</span><span class="sxs-lookup"><span data-stu-id="c7992-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="c7992-107">SSH public and private key files</span><span class="sxs-lookup"><span data-stu-id="c7992-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="c7992-108">an Azure Active Directory Domain Services DC</span><span class="sxs-lookup"><span data-stu-id="c7992-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="c7992-109">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="c7992-109">Quick Commands</span></span>

<span data-ttu-id="c7992-110">_Replace any examples with your own settings._</span><span class="sxs-lookup"><span data-stu-id="c7992-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a><span data-ttu-id="c7992-111">Switch the azure-cli to classic deployment mode</span><span class="sxs-lookup"><span data-stu-id="c7992-111">Switch the azure-cli to classic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="c7992-112">Search for a RHEL version and image</span><span class="sxs-lookup"><span data-stu-id="c7992-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="c7992-113">Create a Redhat Linux VM</span><span class="sxs-lookup"><span data-stu-id="c7992-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-to-the-vm"></a><span data-ttu-id="c7992-114">SSH to the VM</span><span class="sxs-lookup"><span data-stu-id="c7992-114">SSH to the VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="c7992-115">Update YUM packages</span><span class="sxs-lookup"><span data-stu-id="c7992-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="c7992-116">Install packages needed</span><span class="sxs-lookup"><span data-stu-id="c7992-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="c7992-117">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c7992-117">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

### <a name="discover-the-aad-domain-services-managed-domain"></a><span data-ttu-id="c7992-118">Discover the AAD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="c7992-118">Discover the AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="c7992-119">Initialize kerberos</span><span class="sxs-lookup"><span data-stu-id="c7992-119">Initialize kerberos</span></span>

<span data-ttu-id="c7992-120">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="c7992-120">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="c7992-121">Only these users can join computers to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c7992-121">Only these users can join computers to the managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a><span data-ttu-id="c7992-122">Join the machine to the domain</span><span class="sxs-lookup"><span data-stu-id="c7992-122">Join the machine to the domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a><span data-ttu-id="c7992-123">Verify the machine is joined to the domain</span><span class="sxs-lookup"><span data-stu-id="c7992-123">Verify the machine is joined to the domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="c7992-124">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c7992-124">Next Steps</span></span>

* [<span data-ttu-id="c7992-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="c7992-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c7992-126">Set up Key Vault for virtual machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7992-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c7992-127">Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c7992-127">Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI</span></span>](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
