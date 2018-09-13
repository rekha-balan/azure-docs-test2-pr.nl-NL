---
title: Encrypt disks on a Linux VM in Azure | Microsoft Docs
description: How to encrypt virtual disks on a Linux VM for enhanced security using the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/23/2017
ms.author: iainfou
ms.openlocfilehash: 99458401a6c1cdcdf4c0e8a46724bdae241200f7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553396"
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a>How to encrypt virtual disks on a Linux VM
For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted. Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault. You control these cryptographic keys and can audit their use. This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0. You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Quick commands
If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM. More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).

You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login). In the following examples, replace example parameter names with your own values. Example parameter names include `myResourceGroup`, `myKey`, and `myVM`.

First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create). The following example creates a resource group name `myResourceGroup` in the `WestUS` location:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location WestUS
```

Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption. Specify a unique Key Vault name for `keyvault_name` as follows:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create --name $keyvault_name --resource-group myResourceGroup \
  --location WestUS --enabled-for-disk-encryption True
```

Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create). The following example creates a key named `myKey`:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). The service principal handles the authentication and exchange of cryptographic keys from Key Vault. The following example reads in the values for the service principal Id and password for use in later commands:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

The password is only output when you create the service principal. If desired, view and record the password (`echo $sp_password`). You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).

Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy). In the following example, the service principal Id is supplied from the preceding command:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions all \
  --secret-permissions all
```

Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk. Only certain marketplace images support disk encryption. The following example creates a VM named `myVM` using a **CentOS 7.2n** image:

```azurecli
az vm create -g myResourceGroup -n myVM --image OpenLogic:CentOS:7.2n:7.2.20160629 \
  --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
  --data-disk-sizes-gb 5
```

SSH to your VM. Create a partition and filesystem, then mount the data disk. For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Close your SSH session.

Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable). The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:

```azurecli
az vm encryption enable --resource-group myResourceGroup --name myVM \
  --aad-client-id $sp_id \
  --aad-client-secret $sp_password \
  --disk-encryption-keyvault $keyvault_name \
  --key-encryption-key myKey \
  --volume-type all
```

It takes some time for the disk encryption process to complete. Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

The status shows **EncryptionInProgress**. Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

 The status should now report both the OS disk and data disk as **Encrypted**.

## <a name="overview-of-disk-encryption"></a>Overview of disk encryption
Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). There is no charge for encrypting virtual disks in Azure. Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards. You retain control of these cryptographic keys and can audit their use. These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM. An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.

The process for encrypting a VM is as follows:

1. Create a cryptographic key in an Azure Key Vault.
2. Configure the cryptographic key to be usable for encrypting disks.
3. To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.
4. Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.
5. The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.
6. The virtual disks are encrypted using the provided cryptographic key.

## <a name="encryption-process"></a>Encryption process
Disk encryption relies on the following additional components:

* **Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process. 
  * If one exists, you can use an existing Azure Key Vault. You do not have to dedicate a Key Vault to encrypting disks.
  * To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.
* **Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions. 
  * You can typically use an existing Azure Active Directory instance for housing your application.
  * The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys. You are not developing an actual application that integrates with Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requirements and limitations
Supported scenarios and requirements for disk encryption:

* The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.
* All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.
* Standard A, D, DS, G, and GS series VMs.

Disk encryption is not currently supported in the following scenarios:

* Basic tier VMs.
* VMs created using the Classic deployment model.
* Disabling OS disk encryption on Linux VMs.
* Updating the cryptographic keys on an already encrypted Linux VM.

## <a name="create-azure-key-vault-and-keys"></a>Create Azure Key Vault and keys
You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login). Throughout the command examples, replace all example parameters with your own names, location, and key values. The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.

Throughout the command examples, replace all example parameters with your own names, location, and key values. The following examples use a convention of `myResourceGroup`, `myKey`, `myVM`, etc.

The first step is to create an Azure Key Vault to store your cryptographic keys. Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services. For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks. 

Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create). The following example creates a resource group name `myResourceGroup` in the `WestUS` location:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location WestUS
```

The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region. Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption. Specify a unique Key Vault name for `keyvault_name` as follows:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create --name $keyvault_name --resource-group myResourceGroup \
  --location WestUS --enabled-for-disk-encryption True
```

You can store cryptographic keys using software or Hardware Security Model (HSM) protection. Using an HSM requires a premium Key Vault. There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys. To create a premium Key Vault, in the preceding step add `--sku Premium` to the command. The following example uses software-protected keys since we created a standard Key Vault. 

For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks. Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create). The following example creates a key named `myKey`:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a>Create the Azure Active Directory service principal
When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault. This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM. A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.

Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). The following example reads in the values for the service principal Id and password for use in later commands:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

The password is only displayed when you create the service principal. If desired, view and record the password (`echo $sp_password`). You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).

To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys. Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy). In the following example, the service principal Id is supplied from the preceding command:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions all \
  --secret-permissions all
```


## <a name="create-virtual-machine"></a>Create virtual machine
To actually encrypt some virtual disks, lets create a VM and add a data disk. Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk. Only certain marketplace images support disk encryption. The following example creates a VM named `myVM` using a **CentOS 7.2n** image:

```azurecli
az vm create -g myResourceGroup -n myVM --image OpenLogic:CentOS:7.2n:7.2.20160629 \
  --data-disk-sizes-gb 5
```

SSH to your VM with to create a partition and filesystem, then mount the data disk. For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Close your SSH session.


## <a name="encrypt-virtual-machine"></a>Encrypt virtual machine
To encrypt the virtual disks, you bring together all the previous components:

1. Specify the Azure Active Directory service principal and password.
2. Specify the Key Vault to store the metadata for your encrypted disks.
3. Specify the cryptographic keys to use for the actual encryption and decryption.
4. Specify whether you want to encrypt the OS disk, the data disks, or all.

Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable). The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:

```azurecli
az vm encryption enable --resource-group myResourceGroup --name myVM \
  --aad-client-id $sp_id \
  --aad-client-secret $sp_password \
  --disk-encryption-keyvault $keyvault_name \
  --key-encryption-key myKey \
  --volume-type all
```

It takes some time for the disk encryption process to complete. Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

The output is similar to the following truncated example:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

The status should now report both the OS disk and data disk as **Encrypted**.


## <a name="add-additional-data-disks"></a>Add additional data disks
Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them. When you run the `az vm encryption enable` command, increment the sequence version using the `--sequence-version` parameter. This sequence version parameter allows you to perform repeated operations on the same VM.

For example, lets add a second virtual disk to your VM as follows:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:

```azurecli
az vm encryption enable --resource-group myResourceGroup --name myVM \
  --aad-client-id $sp_id \
  --aad-client-secret $sp_password \
  --disk-encryption-keyvault $keyvault_name \
  --key-encryption-key myKey \
  --volume-type all \
  --sequence-version 2
```


## <a name="next-steps"></a>Next steps
* For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md).
* For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).

