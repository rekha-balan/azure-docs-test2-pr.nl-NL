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
# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a>Join a RedHat Linux VM to an Azure Active Directory Domain Service

This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.  The requirements are:

- [an Azure account](https://azure.microsoft.com/pricing/free-trial/)

- [SSH public and private key files](mac-create-ssh-keys.md)

- [an Azure Active Directory Domain Services DC](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Quick Commands

_Replace any examples with your own settings._

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a>Switch the azure-cli to classic deployment mode

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Search for a RHEL version and image

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Create a Redhat Linux VM

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

### <a name="ssh-to-the-vm"></a>SSH to the VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>Update YUM packages

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Install packages needed

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.

### <a name="discover-the-aad-domain-services-managed-domain"></a>Discover the AAD Domain Services managed domain

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Initialize kerberos

Ensure that you specify a user who belongs to the 'AAD DC Administrators' group. Only these users can join computers to the managed domain.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a>Join the machine to the domain

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a>Verify the machine is joined to the domain

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Next Steps

* [Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Set up Key Vault for virtual machines in Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
