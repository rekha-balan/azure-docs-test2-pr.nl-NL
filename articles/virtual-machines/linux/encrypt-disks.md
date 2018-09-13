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
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="fe859-103">How to encrypt virtual disks on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="fe859-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="fe859-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span><span class="sxs-lookup"><span data-stu-id="fe859-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="fe859-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="fe859-106">You control these cryptographic keys and can audit their use.</span><span class="sxs-lookup"><span data-stu-id="fe859-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="fe859-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="fe859-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="fe859-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe859-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="fe859-109">Quick commands</span><span class="sxs-lookup"><span data-stu-id="fe859-109">Quick commands</span></span>
<span data-ttu-id="fe859-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span><span class="sxs-lookup"><span data-stu-id="fe859-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="fe859-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="fe859-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="fe859-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fe859-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="fe859-113">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="fe859-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fe859-114">Example parameter names include `myResourceGroup`, `myKey`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="fe859-114">Example parameter names include `myResourceGroup`, `myKey`, and `myVM`.</span></span>

<span data-ttu-id="fe859-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fe859-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fe859-116">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="fe859-116">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location WestUS
```

<span data-ttu-id="fe859-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span><span class="sxs-lookup"><span data-stu-id="fe859-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="fe859-118">Specify a unique Key Vault name for `keyvault_name` as follows:</span><span class="sxs-lookup"><span data-stu-id="fe859-118">Specify a unique Key Vault name for `keyvault_name` as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create --name $keyvault_name --resource-group myResourceGroup \
  --location WestUS --enabled-for-disk-encryption True
```

<span data-ttu-id="fe859-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="fe859-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="fe859-120">The following example creates a key named `myKey`:</span><span class="sxs-lookup"><span data-stu-id="fe859-120">The following example creates a key named `myKey`:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="fe859-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="fe859-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="fe859-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="fe859-123">The following example reads in the values for the service principal Id and password for use in later commands:</span><span class="sxs-lookup"><span data-stu-id="fe859-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="fe859-124">The password is only output when you create the service principal.</span><span class="sxs-lookup"><span data-stu-id="fe859-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="fe859-125">If desired, view and record the password (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="fe859-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="fe859-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="fe859-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="fe859-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="fe859-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="fe859-128">In the following example, the service principal Id is supplied from the preceding command:</span><span class="sxs-lookup"><span data-stu-id="fe859-128">In the following example, the service principal Id is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions all \
  --secret-permissions all
```

<span data-ttu-id="fe859-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span><span class="sxs-lookup"><span data-stu-id="fe859-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="fe859-130">Only certain marketplace images support disk encryption.</span><span class="sxs-lookup"><span data-stu-id="fe859-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="fe859-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span><span class="sxs-lookup"><span data-stu-id="fe859-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create -g myResourceGroup -n myVM --image OpenLogic:CentOS:7.2n:7.2.20160629 \
  --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
  --data-disk-sizes-gb 5
```

<span data-ttu-id="fe859-132">SSH to your VM.</span><span class="sxs-lookup"><span data-stu-id="fe859-132">SSH to your VM.</span></span> <span data-ttu-id="fe859-133">Create a partition and filesystem, then mount the data disk.</span><span class="sxs-lookup"><span data-stu-id="fe859-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="fe859-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="fe859-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="fe859-135">Close your SSH session.</span><span class="sxs-lookup"><span data-stu-id="fe859-135">Close your SSH session.</span></span>

<span data-ttu-id="fe859-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="fe859-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="fe859-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span><span class="sxs-lookup"><span data-stu-id="fe859-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable --resource-group myResourceGroup --name myVM \
  --aad-client-id $sp_id \
  --aad-client-secret $sp_password \
  --disk-encryption-keyvault $keyvault_name \
  --key-encryption-key myKey \
  --volume-type all
```

<span data-ttu-id="fe859-138">It takes some time for the disk encryption process to complete.</span><span class="sxs-lookup"><span data-stu-id="fe859-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="fe859-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="fe859-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe859-140">The status shows **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="fe859-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="fe859-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="fe859-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe859-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="fe859-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

 <span data-ttu-id="fe859-143">The status should now report both the OS disk and data disk as **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="fe859-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="fe859-144">Overview of disk encryption</span><span class="sxs-lookup"><span data-stu-id="fe859-144">Overview of disk encryption</span></span>
<span data-ttu-id="fe859-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="fe859-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="fe859-146">There is no charge for encrypting virtual disks in Azure.</span><span class="sxs-lookup"><span data-stu-id="fe859-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="fe859-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span><span class="sxs-lookup"><span data-stu-id="fe859-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="fe859-148">You retain control of these cryptographic keys and can audit their use.</span><span class="sxs-lookup"><span data-stu-id="fe859-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="fe859-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span><span class="sxs-lookup"><span data-stu-id="fe859-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="fe859-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span><span class="sxs-lookup"><span data-stu-id="fe859-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="fe859-151">The process for encrypting a VM is as follows:</span><span class="sxs-lookup"><span data-stu-id="fe859-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="fe859-152">Create a cryptographic key in an Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="fe859-153">Configure the cryptographic key to be usable for encrypting disks.</span><span class="sxs-lookup"><span data-stu-id="fe859-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="fe859-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span><span class="sxs-lookup"><span data-stu-id="fe859-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="fe859-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span><span class="sxs-lookup"><span data-stu-id="fe859-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="fe859-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="fe859-157">The virtual disks are encrypted using the provided cryptographic key.</span><span class="sxs-lookup"><span data-stu-id="fe859-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="fe859-158">Encryption process</span><span class="sxs-lookup"><span data-stu-id="fe859-158">Encryption process</span></span>
<span data-ttu-id="fe859-159">Disk encryption relies on the following additional components:</span><span class="sxs-lookup"><span data-stu-id="fe859-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="fe859-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span><span class="sxs-lookup"><span data-stu-id="fe859-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="fe859-161">If one exists, you can use an existing Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="fe859-162">You do not have to dedicate a Key Vault to encrypting disks.</span><span class="sxs-lookup"><span data-stu-id="fe859-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="fe859-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="fe859-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span><span class="sxs-lookup"><span data-stu-id="fe859-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="fe859-165">You can typically use an existing Azure Active Directory instance for housing your application.</span><span class="sxs-lookup"><span data-stu-id="fe859-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="fe859-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span><span class="sxs-lookup"><span data-stu-id="fe859-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="fe859-167">You are not developing an actual application that integrates with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe859-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="fe859-168">Requirements and limitations</span><span class="sxs-lookup"><span data-stu-id="fe859-168">Requirements and limitations</span></span>
<span data-ttu-id="fe859-169">Supported scenarios and requirements for disk encryption:</span><span class="sxs-lookup"><span data-stu-id="fe859-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="fe859-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="fe859-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="fe859-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span><span class="sxs-lookup"><span data-stu-id="fe859-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="fe859-172">Standard A, D, DS, G, and GS series VMs.</span><span class="sxs-lookup"><span data-stu-id="fe859-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="fe859-173">Disk encryption is not currently supported in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="fe859-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="fe859-174">Basic tier VMs.</span><span class="sxs-lookup"><span data-stu-id="fe859-174">Basic tier VMs.</span></span>
* <span data-ttu-id="fe859-175">VMs created using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="fe859-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="fe859-176">Disabling OS disk encryption on Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="fe859-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="fe859-177">Updating the cryptographic keys on an already encrypted Linux VM.</span><span class="sxs-lookup"><span data-stu-id="fe859-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="fe859-178">Create Azure Key Vault and keys</span><span class="sxs-lookup"><span data-stu-id="fe859-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="fe859-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fe859-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="fe859-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span><span class="sxs-lookup"><span data-stu-id="fe859-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="fe859-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span><span class="sxs-lookup"><span data-stu-id="fe859-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="fe859-182">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span><span class="sxs-lookup"><span data-stu-id="fe859-182">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="fe859-183">The following examples use a convention of `myResourceGroup`, `myKey`, `myVM`, etc.</span><span class="sxs-lookup"><span data-stu-id="fe859-183">The following examples use a convention of `myResourceGroup`, `myKey`, `myVM`, etc.</span></span>

<span data-ttu-id="fe859-184">The first step is to create an Azure Key Vault to store your cryptographic keys.</span><span class="sxs-lookup"><span data-stu-id="fe859-184">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="fe859-185">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span><span class="sxs-lookup"><span data-stu-id="fe859-185">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="fe859-186">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span><span class="sxs-lookup"><span data-stu-id="fe859-186">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="fe859-187">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fe859-187">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fe859-188">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="fe859-188">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location WestUS
```

<span data-ttu-id="fe859-189">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span><span class="sxs-lookup"><span data-stu-id="fe859-189">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="fe859-190">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span><span class="sxs-lookup"><span data-stu-id="fe859-190">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="fe859-191">Specify a unique Key Vault name for `keyvault_name` as follows:</span><span class="sxs-lookup"><span data-stu-id="fe859-191">Specify a unique Key Vault name for `keyvault_name` as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create --name $keyvault_name --resource-group myResourceGroup \
  --location WestUS --enabled-for-disk-encryption True
```

<span data-ttu-id="fe859-192">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span><span class="sxs-lookup"><span data-stu-id="fe859-192">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="fe859-193">Using an HSM requires a premium Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-193">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="fe859-194">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span><span class="sxs-lookup"><span data-stu-id="fe859-194">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="fe859-195">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span><span class="sxs-lookup"><span data-stu-id="fe859-195">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="fe859-196">The following example uses software-protected keys since we created a standard Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-196">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="fe859-197">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span><span class="sxs-lookup"><span data-stu-id="fe859-197">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="fe859-198">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="fe859-198">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="fe859-199">The following example creates a key named `myKey`:</span><span class="sxs-lookup"><span data-stu-id="fe859-199">The following example creates a key named `myKey`:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="fe859-200">Create the Azure Active Directory service principal</span><span class="sxs-lookup"><span data-stu-id="fe859-200">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="fe859-201">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe859-201">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="fe859-202">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span><span class="sxs-lookup"><span data-stu-id="fe859-202">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="fe859-203">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span><span class="sxs-lookup"><span data-stu-id="fe859-203">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="fe859-204">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="fe859-204">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="fe859-205">The following example reads in the values for the service principal Id and password for use in later commands:</span><span class="sxs-lookup"><span data-stu-id="fe859-205">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="fe859-206">The password is only displayed when you create the service principal.</span><span class="sxs-lookup"><span data-stu-id="fe859-206">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="fe859-207">If desired, view and record the password (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="fe859-207">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="fe859-208">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="fe859-208">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="fe859-209">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span><span class="sxs-lookup"><span data-stu-id="fe859-209">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="fe859-210">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="fe859-210">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="fe859-211">In the following example, the service principal Id is supplied from the preceding command:</span><span class="sxs-lookup"><span data-stu-id="fe859-211">In the following example, the service principal Id is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions all \
  --secret-permissions all
```


## <a name="create-virtual-machine"></a><span data-ttu-id="fe859-212">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="fe859-212">Create virtual machine</span></span>
<span data-ttu-id="fe859-213">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span><span class="sxs-lookup"><span data-stu-id="fe859-213">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="fe859-214">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span><span class="sxs-lookup"><span data-stu-id="fe859-214">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="fe859-215">Only certain marketplace images support disk encryption.</span><span class="sxs-lookup"><span data-stu-id="fe859-215">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="fe859-216">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span><span class="sxs-lookup"><span data-stu-id="fe859-216">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create -g myResourceGroup -n myVM --image OpenLogic:CentOS:7.2n:7.2.20160629 \
  --data-disk-sizes-gb 5
```

<span data-ttu-id="fe859-217">SSH to your VM with to create a partition and filesystem, then mount the data disk.</span><span class="sxs-lookup"><span data-stu-id="fe859-217">SSH to your VM with to create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="fe859-218">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="fe859-218">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="fe859-219">Close your SSH session.</span><span class="sxs-lookup"><span data-stu-id="fe859-219">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="fe859-220">Encrypt virtual machine</span><span class="sxs-lookup"><span data-stu-id="fe859-220">Encrypt virtual machine</span></span>
<span data-ttu-id="fe859-221">To encrypt the virtual disks, you bring together all the previous components:</span><span class="sxs-lookup"><span data-stu-id="fe859-221">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="fe859-222">Specify the Azure Active Directory service principal and password.</span><span class="sxs-lookup"><span data-stu-id="fe859-222">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="fe859-223">Specify the Key Vault to store the metadata for your encrypted disks.</span><span class="sxs-lookup"><span data-stu-id="fe859-223">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="fe859-224">Specify the cryptographic keys to use for the actual encryption and decryption.</span><span class="sxs-lookup"><span data-stu-id="fe859-224">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="fe859-225">Specify whether you want to encrypt the OS disk, the data disks, or all.</span><span class="sxs-lookup"><span data-stu-id="fe859-225">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="fe859-226">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="fe859-226">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="fe859-227">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span><span class="sxs-lookup"><span data-stu-id="fe859-227">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable --resource-group myResourceGroup --name myVM \
  --aad-client-id $sp_id \
  --aad-client-secret $sp_password \
  --disk-encryption-keyvault $keyvault_name \
  --key-encryption-key myKey \
  --volume-type all
```

<span data-ttu-id="fe859-228">It takes some time for the disk encryption process to complete.</span><span class="sxs-lookup"><span data-stu-id="fe859-228">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="fe859-229">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="fe859-229">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe859-230">The output is similar to the following truncated example:</span><span class="sxs-lookup"><span data-stu-id="fe859-230">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="fe859-231">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="fe859-231">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe859-232">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="fe859-232">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe859-233">The status should now report both the OS disk and data disk as **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="fe859-233">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="fe859-234">Add additional data disks</span><span class="sxs-lookup"><span data-stu-id="fe859-234">Add additional data disks</span></span>
<span data-ttu-id="fe859-235">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span><span class="sxs-lookup"><span data-stu-id="fe859-235">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="fe859-236">When you run the `az vm encryption enable` command, increment the sequence version using the `--sequence-version` parameter.</span><span class="sxs-lookup"><span data-stu-id="fe859-236">When you run the `az vm encryption enable` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="fe859-237">This sequence version parameter allows you to perform repeated operations on the same VM.</span><span class="sxs-lookup"><span data-stu-id="fe859-237">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="fe859-238">For example, lets add a second virtual disk to your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="fe859-238">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="fe859-239">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span><span class="sxs-lookup"><span data-stu-id="fe859-239">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

```azurecli
az vm encryption enable --resource-group myResourceGroup --name myVM \
  --aad-client-id $sp_id \
  --aad-client-secret $sp_password \
  --disk-encryption-keyvault $keyvault_name \
  --key-encryption-key myKey \
  --volume-type all \
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="fe859-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe859-240">Next steps</span></span>
* <span data-ttu-id="fe859-241">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fe859-241">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md).</span></span>
* <span data-ttu-id="fe859-242">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="fe859-242">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>

