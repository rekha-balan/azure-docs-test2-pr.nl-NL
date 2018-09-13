---
title: Encrypt disks on a Linux VM with the Azure CLI 1.0 | Microsoft Docs
description: How to encrypt disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: fa8be45d173927a547031c902ec9e697ecebc215
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551695"
---
# <a name="encrypt-disks-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="c7e56-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c7e56-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="c7e56-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="c7e56-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="c7e56-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="c7e56-106">You control these cryptographic keys and can audit their use.</span><span class="sxs-lookup"><span data-stu-id="c7e56-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c7e56-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="c7e56-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="c7e56-108">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="c7e56-108">CLI versions to complete the task</span></span>
<span data-ttu-id="c7e56-109">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="c7e56-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="c7e56-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="c7e56-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c7e56-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="c7e56-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c7e56-112">Quick commands</span><span class="sxs-lookup"><span data-stu-id="c7e56-112">Quick commands</span></span>
<span data-ttu-id="c7e56-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span><span class="sxs-lookup"><span data-stu-id="c7e56-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="c7e56-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="c7e56-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="c7e56-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c7e56-116">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="c7e56-116">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c7e56-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c7e56-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="c7e56-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span><span class="sxs-lookup"><span data-stu-id="c7e56-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="c7e56-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="c7e56-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="c7e56-120">Create an Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="c7e56-121">The following example creates a Key Vault named `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="c7e56-121">The following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="c7e56-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span><span class="sxs-lookup"><span data-stu-id="c7e56-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="c7e56-123">The following example creates a key named `myKey`:</span><span class="sxs-lookup"><span data-stu-id="c7e56-123">The following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="c7e56-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c7e56-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span><span class="sxs-lookup"><span data-stu-id="c7e56-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span></span> <span data-ttu-id="c7e56-126">For the highest level of security, client secrets should be used instead of passwords.</span><span class="sxs-lookup"><span data-stu-id="c7e56-126">For the highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="c7e56-127">The Azure CLI cannot currently generate client secrets.</span><span class="sxs-lookup"><span data-stu-id="c7e56-127">The Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="c7e56-128">Client secrets can only be generated in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7e56-128">Client secrets can only be generated in the Azure portal.</span></span> <span data-ttu-id="c7e56-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="c7e56-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="c7e56-130">Specify your own password as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="c7e56-131">Note the `applicationId` shown in the output from the preceding command.</span><span class="sxs-lookup"><span data-stu-id="c7e56-131">Note the `applicationId` shown in the output from the preceding command.</span></span> <span data-ttu-id="c7e56-132">This application ID is used in the following steps:</span><span class="sxs-lookup"><span data-stu-id="c7e56-132">This application ID is used in the following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="c7e56-133">Add a data disk to an existing VM.</span><span class="sxs-lookup"><span data-stu-id="c7e56-133">Add a data disk to an existing VM.</span></span> <span data-ttu-id="c7e56-134">The following example adds a data disk to a VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="c7e56-134">The following example adds a data disk to a VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="c7e56-135">Review the details for your Key Vault and the key you created.</span><span class="sxs-lookup"><span data-stu-id="c7e56-135">Review the details for your Key Vault and the key you created.</span></span> <span data-ttu-id="c7e56-136">You need the Key Vault ID, URI, and key URL in the final step.</span><span class="sxs-lookup"><span data-stu-id="c7e56-136">You need the Key Vault ID, URI, and key URL in the final step.</span></span> <span data-ttu-id="c7e56-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span><span class="sxs-lookup"><span data-stu-id="c7e56-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="c7e56-138">Encrypt your disks as follows, entering your own parameter names throughout:</span><span class="sxs-lookup"><span data-stu-id="c7e56-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="c7e56-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span><span class="sxs-lookup"><span data-stu-id="c7e56-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="c7e56-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="c7e56-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="c7e56-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \ 
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="c7e56-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span><span class="sxs-lookup"><span data-stu-id="c7e56-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="c7e56-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="c7e56-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="c7e56-144">Overview of disk encryption</span><span class="sxs-lookup"><span data-stu-id="c7e56-144">Overview of disk encryption</span></span>
<span data-ttu-id="c7e56-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="c7e56-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="c7e56-146">There is no charge for encrypting virtual disks in Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e56-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="c7e56-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span><span class="sxs-lookup"><span data-stu-id="c7e56-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="c7e56-148">You retain control of these cryptographic keys and can audit their use.</span><span class="sxs-lookup"><span data-stu-id="c7e56-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c7e56-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span><span class="sxs-lookup"><span data-stu-id="c7e56-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="c7e56-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span><span class="sxs-lookup"><span data-stu-id="c7e56-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="c7e56-151">The process for encrypting a VM is as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="c7e56-152">Create a cryptographic key in an Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="c7e56-153">Configure the cryptographic key to be usable for encrypting disks.</span><span class="sxs-lookup"><span data-stu-id="c7e56-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="c7e56-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span><span class="sxs-lookup"><span data-stu-id="c7e56-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span></span>
4. <span data-ttu-id="c7e56-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span><span class="sxs-lookup"><span data-stu-id="c7e56-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="c7e56-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="c7e56-157">The virtual disks are encrypted using the provided cryptographic key.</span><span class="sxs-lookup"><span data-stu-id="c7e56-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="c7e56-158">Supporting services and encryption process</span><span class="sxs-lookup"><span data-stu-id="c7e56-158">Supporting services and encryption process</span></span>
<span data-ttu-id="c7e56-159">Disk encryption relies on the following additional components:</span><span class="sxs-lookup"><span data-stu-id="c7e56-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="c7e56-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span><span class="sxs-lookup"><span data-stu-id="c7e56-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="c7e56-161">If one exists, you can use an existing Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="c7e56-162">You do not have to dedicate a Key Vault to encrypting disks.</span><span class="sxs-lookup"><span data-stu-id="c7e56-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="c7e56-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="c7e56-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span><span class="sxs-lookup"><span data-stu-id="c7e56-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="c7e56-165">You can typically use an existing Azure Active Directory instance for housing your application.</span><span class="sxs-lookup"><span data-stu-id="c7e56-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span> 
  * <span data-ttu-id="c7e56-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span><span class="sxs-lookup"><span data-stu-id="c7e56-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="c7e56-167">You are not developing an actual application that integrates with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c7e56-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="c7e56-168">Requirements and limitations</span><span class="sxs-lookup"><span data-stu-id="c7e56-168">Requirements and limitations</span></span>
<span data-ttu-id="c7e56-169">Supported scenarios and requirements for disk encryption:</span><span class="sxs-lookup"><span data-stu-id="c7e56-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="c7e56-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="c7e56-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="c7e56-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span><span class="sxs-lookup"><span data-stu-id="c7e56-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="c7e56-172">Standard A, D, DS, G, and GS series VMs.</span><span class="sxs-lookup"><span data-stu-id="c7e56-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="c7e56-173">Disk encryption is not currently supported in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="c7e56-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="c7e56-174">Basic tier VMs.</span><span class="sxs-lookup"><span data-stu-id="c7e56-174">Basic tier VMs.</span></span>
* <span data-ttu-id="c7e56-175">VMs created using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="c7e56-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="c7e56-176">Disabling OS disk encryption on Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="c7e56-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="c7e56-177">Updating the cryptographic keys on an already encrypted Linux VM.</span><span class="sxs-lookup"><span data-stu-id="c7e56-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-the-azure-key-vault-and-keys"></a><span data-ttu-id="c7e56-178">Create the Azure Key Vault and keys</span><span class="sxs-lookup"><span data-stu-id="c7e56-178">Create the Azure Key Vault and keys</span></span>
<span data-ttu-id="c7e56-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c7e56-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span><span class="sxs-lookup"><span data-stu-id="c7e56-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="c7e56-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span><span class="sxs-lookup"><span data-stu-id="c7e56-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="c7e56-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span><span class="sxs-lookup"><span data-stu-id="c7e56-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="c7e56-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span><span class="sxs-lookup"><span data-stu-id="c7e56-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="c7e56-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span><span class="sxs-lookup"><span data-stu-id="c7e56-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="c7e56-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span><span class="sxs-lookup"><span data-stu-id="c7e56-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="c7e56-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="c7e56-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="c7e56-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span><span class="sxs-lookup"><span data-stu-id="c7e56-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="c7e56-188">The following example creates an Azure Key Vault named `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="c7e56-188">The following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="c7e56-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span><span class="sxs-lookup"><span data-stu-id="c7e56-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="c7e56-190">Using an HSM requires a premium Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="c7e56-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span><span class="sxs-lookup"><span data-stu-id="c7e56-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="c7e56-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span><span class="sxs-lookup"><span data-stu-id="c7e56-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="c7e56-193">The following example uses software-protected keys since we created a standard Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-193">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="c7e56-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span><span class="sxs-lookup"><span data-stu-id="c7e56-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="c7e56-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span><span class="sxs-lookup"><span data-stu-id="c7e56-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="c7e56-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span><span class="sxs-lookup"><span data-stu-id="c7e56-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-the-azure-active-directory-application"></a><span data-ttu-id="c7e56-197">Create the Azure Active Directory application</span><span class="sxs-lookup"><span data-stu-id="c7e56-197">Create the Azure Active Directory application</span></span>
<span data-ttu-id="c7e56-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7e56-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c7e56-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span><span class="sxs-lookup"><span data-stu-id="c7e56-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="c7e56-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span><span class="sxs-lookup"><span data-stu-id="c7e56-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="c7e56-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span><span class="sxs-lookup"><span data-stu-id="c7e56-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span></span> <span data-ttu-id="c7e56-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7e56-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span></span> <span data-ttu-id="c7e56-203">As this time, generating keys cannot be done from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c7e56-203">As this time, generating keys cannot be done from the Azure CLI.</span></span> 

<span data-ttu-id="c7e56-204">Create your Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="c7e56-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="c7e56-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="c7e56-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="c7e56-206">Specify your own password as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="c7e56-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span><span class="sxs-lookup"><span data-stu-id="c7e56-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span></span> <span data-ttu-id="c7e56-208">This application ID is used in some of the remaining steps.</span><span class="sxs-lookup"><span data-stu-id="c7e56-208">This application ID is used in some of the remaining steps.</span></span> <span data-ttu-id="c7e56-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span><span class="sxs-lookup"><span data-stu-id="c7e56-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span></span> <span data-ttu-id="c7e56-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span><span class="sxs-lookup"><span data-stu-id="c7e56-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span></span> 

<span data-ttu-id="c7e56-211">Create the SPN and set the appropriate permissions as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-211">Create the SPN and set the appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="c7e56-212">Add a virtual disk and review encryption status</span><span class="sxs-lookup"><span data-stu-id="c7e56-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="c7e56-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span><span class="sxs-lookup"><span data-stu-id="c7e56-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span></span> <span data-ttu-id="c7e56-214">Add a 5Gb data disk to an existing VM as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-214">Add a 5Gb data disk to an existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="c7e56-215">The virtual disks are not currently encrypted.</span><span class="sxs-lookup"><span data-stu-id="c7e56-215">The virtual disks are not currently encrypted.</span></span> <span data-ttu-id="c7e56-216">Review the current encryption status of your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-216">Review the current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="c7e56-217">Encrypt virtual disks</span><span class="sxs-lookup"><span data-stu-id="c7e56-217">Encrypt virtual disks</span></span>
<span data-ttu-id="c7e56-218">To now encrypt the virtual disks, you bring together all the previous components:</span><span class="sxs-lookup"><span data-stu-id="c7e56-218">To now encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="c7e56-219">Specify the Azure Active Directory application and password.</span><span class="sxs-lookup"><span data-stu-id="c7e56-219">Specify the Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="c7e56-220">Specify the Key Vault to store the metadata for your encrypted disks.</span><span class="sxs-lookup"><span data-stu-id="c7e56-220">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="c7e56-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span><span class="sxs-lookup"><span data-stu-id="c7e56-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="c7e56-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span><span class="sxs-lookup"><span data-stu-id="c7e56-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="c7e56-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span><span class="sxs-lookup"><span data-stu-id="c7e56-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="c7e56-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="c7e56-225">As the preceding command has many variables, the following example is the complete command for reference:</span><span class="sxs-lookup"><span data-stu-id="c7e56-225">As the preceding command has many variables, the following example is the complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \ 
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="c7e56-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span><span class="sxs-lookup"><span data-stu-id="c7e56-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="c7e56-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span><span class="sxs-lookup"><span data-stu-id="c7e56-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span></span>

<span data-ttu-id="c7e56-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span><span class="sxs-lookup"><span data-stu-id="c7e56-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="c7e56-229">Add additional data disks</span><span class="sxs-lookup"><span data-stu-id="c7e56-229">Add additional data disks</span></span>
<span data-ttu-id="c7e56-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span><span class="sxs-lookup"><span data-stu-id="c7e56-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="c7e56-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span><span class="sxs-lookup"><span data-stu-id="c7e56-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="c7e56-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span><span class="sxs-lookup"><span data-stu-id="c7e56-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="c7e56-233">For example, lets add a second virtual disk to your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-233">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="c7e56-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span><span class="sxs-lookup"><span data-stu-id="c7e56-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="c7e56-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7e56-235">Next steps</span></span>
* <span data-ttu-id="c7e56-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c7e56-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md).</span></span>
* <span data-ttu-id="c7e56-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="c7e56-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>

