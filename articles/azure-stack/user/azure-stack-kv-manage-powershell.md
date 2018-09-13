---
title: Manage Key Vault in Azure Stack by using PowerShell | Microsoft Docs
description: Learn how to manage Key Vault in Azure Stack by using PowerShell
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 22B62A3B-B5A9-4B8C-81C9-DA461838FAE5
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.openlocfilehash: b2dc79c9000c9cb1a826791b4b152cfd2bdb1584
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869213"
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="58e37-103">Manage Key Vault in Azure Stack using PowerShell</span><span class="sxs-lookup"><span data-stu-id="58e37-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="58e37-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="58e37-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="58e37-105">You can manage Key Vault in Azure Stack using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58e37-105">You can manage Key Vault in Azure Stack using PowerShell.</span></span> <span data-ttu-id="58e37-106">Learn how to use Key Vault PowerShell cmdlets to:</span><span class="sxs-lookup"><span data-stu-id="58e37-106">Learn how to use Key Vault PowerShell cmdlets to:</span></span>

* <span data-ttu-id="58e37-107">Create a key vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-107">Create a key vault.</span></span>
* <span data-ttu-id="58e37-108">Store and manage cryptographic keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="58e37-108">Store and manage cryptographic keys and secrets.</span></span>
* <span data-ttu-id="58e37-109">Authorize users or applications to invoke operations in the vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-109">Authorize users or applications to invoke operations in the vault.</span></span>

>[!NOTE]
><span data-ttu-id="58e37-110">The Key Vault PowerShell cmdlets descibed in this article are provided in the Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="58e37-110">The Key Vault PowerShell cmdlets descibed in this article are provided in the Azure PowerShell SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58e37-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="58e37-111">Prerequisites</span></span>

* <span data-ttu-id="58e37-112">You must subscribe to an offer that includes the Azure Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="58e37-112">You must subscribe to an offer that includes the Azure Key Vault service.</span></span>
* <span data-ttu-id="58e37-113">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="58e37-113">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>
* <span data-ttu-id="58e37-114">[Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md).</span><span class="sxs-lookup"><span data-stu-id="58e37-114">[Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md).</span></span>

## <a name="enable-your-tenant-subscription-for-key-vault-operations"></a><span data-ttu-id="58e37-115">Enable your tenant subscription for Key Vault operations</span><span class="sxs-lookup"><span data-stu-id="58e37-115">Enable your tenant subscription for Key Vault operations</span></span>

<span data-ttu-id="58e37-116">Before you can issue any operations against a key vault, you need to ensure that your tenant subscription is enabled for vault operations.</span><span class="sxs-lookup"><span data-stu-id="58e37-116">Before you can issue any operations against a key vault, you need to ensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="58e37-117">To verify that vault operations are enabled, run the following command:</span><span class="sxs-lookup"><span data-stu-id="58e37-117">To verify that vault operations are enabled, run the following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```

<span data-ttu-id="58e37-118">**Output**</span><span class="sxs-lookup"><span data-stu-id="58e37-118">**Output**</span></span>

<span data-ttu-id="58e37-119">If your subscription is enabled for vault operations, the output shows “RegistrationState” is “Registered” for all resource types of a key vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-119">If your subscription is enabled for vault operations, the output shows “RegistrationState” is “Registered” for all resource types of a key vault.</span></span>

![Key vault registration state](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="58e37-121">If vault operations are not enabled, invoke the following command to register the Key Vault service in your subscription:</span><span class="sxs-lookup"><span data-stu-id="58e37-121">If vault operations are not enabled, invoke the following command to register the Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="58e37-122">**Output**</span><span class="sxs-lookup"><span data-stu-id="58e37-122">**Output**</span></span>

<span data-ttu-id="58e37-123">If the registration is successful, the following output is returned:</span><span class="sxs-lookup"><span data-stu-id="58e37-123">If the registration is successful, the following output is returned:</span></span>

<span data-ttu-id="58e37-124">![Register](media/azure-stack-kv-manage-powershell/image2.png) When you invoke the key vault commands, you might get an error, such as "The subscription is not registered to use namespace 'Microsoft.KeyVault'." If you get an error, confirm that you have [enabled the Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) by following the instructions that were mentioned previously.</span><span class="sxs-lookup"><span data-stu-id="58e37-124">![Register](media/azure-stack-kv-manage-powershell/image2.png) When you invoke the key vault commands, you might get an error, such as "The subscription is not registered to use namespace 'Microsoft.KeyVault'." If you get an error, confirm that you have [enabled the Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) by following the instructions that were mentioned previously.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="58e37-125">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="58e37-125">Create a key vault</span></span>

<span data-ttu-id="58e37-126">Before you create a key vault, create a resource group so that all of the resources related to the key vault exist in a resource group.</span><span class="sxs-lookup"><span data-stu-id="58e37-126">Before you create a key vault, create a resource group so that all of the resources related to the key vault exist in a resource group.</span></span> <span data-ttu-id="58e37-127">Use the following command to create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="58e37-127">Use the following command to create a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="58e37-128">**Output**</span><span class="sxs-lookup"><span data-stu-id="58e37-128">**Output**</span></span>

![New resource group](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="58e37-130">Now, use the **New-AzureRMKeyVault** command to create a key vault in the resource group that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="58e37-130">Now, use the **New-AzureRMKeyVault** command to create a key vault in the resource group that you created earlier.</span></span> <span data-ttu-id="58e37-131">This command reads three mandatory parameters: resource group name, key vault name, and geographic location.</span><span class="sxs-lookup"><span data-stu-id="58e37-131">This command reads three mandatory parameters: resource group name, key vault name, and geographic location.</span></span>

<span data-ttu-id="58e37-132">Run the following command to create a key vault:</span><span class="sxs-lookup"><span data-stu-id="58e37-132">Run the following command to create a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```

<span data-ttu-id="58e37-133">**Output**</span><span class="sxs-lookup"><span data-stu-id="58e37-133">**Output**</span></span>

![New key vault](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="58e37-135">The output of this command shows the properties of the key vault that you created.</span><span class="sxs-lookup"><span data-stu-id="58e37-135">The output of this command shows the properties of the key vault that you created.</span></span> <span data-ttu-id="58e37-136">When an application accesses this vault, it must use the **Vault URI** property, which is "https://vault01.vault.local.azurestack.external" in this example.</span><span class="sxs-lookup"><span data-stu-id="58e37-136">When an application accesses this vault, it must use the **Vault URI** property, which is "https://vault01.vault.local.azurestack.external" in this example.</span></span>

### <a name="active-directory-federation-services-ad-fs-deployment"></a><span data-ttu-id="58e37-137">Active Directory Federation Services (AD FS) deployment</span><span class="sxs-lookup"><span data-stu-id="58e37-137">Active Directory Federation Services (AD FS) deployment</span></span>

<span data-ttu-id="58e37-138">In an AD FS deployment, you might get this warning: "Access policy is not set.</span><span class="sxs-lookup"><span data-stu-id="58e37-138">In an AD FS deployment, you might get this warning: "Access policy is not set.</span></span> <span data-ttu-id="58e37-139">No user or application has access permission to use this vault."</span><span class="sxs-lookup"><span data-stu-id="58e37-139">No user or application has access permission to use this vault."</span></span> <span data-ttu-id="58e37-140">To resolve this issue, set an access policy for the vault by using the [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span><span class="sxs-lookup"><span data-stu-id="58e37-140">To resolve this issue, set an access policy for the vault by using the [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain the security identifier(SID) of the active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value

# Set the key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="58e37-141">Manage keys and secrets</span><span class="sxs-lookup"><span data-stu-id="58e37-141">Manage keys and secrets</span></span>

<span data-ttu-id="58e37-142">After you create a vault, use the following steps to create and manage keys and secrets in the vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-142">After you create a vault, use the following steps to create and manage keys and secrets in the vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="58e37-143">Create a key</span><span class="sxs-lookup"><span data-stu-id="58e37-143">Create a key</span></span>

<span data-ttu-id="58e37-144">Use the **Add-AzureKeyVaultKey** command to create or import a software-protected key in a key vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-144">Use the **Add-AzureKeyVaultKey** command to create or import a software-protected key in a key vault.</span></span>

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```

<span data-ttu-id="58e37-145">The **Destination** parameter is used to specify that the key is software protected.</span><span class="sxs-lookup"><span data-stu-id="58e37-145">The **Destination** parameter is used to specify that the key is software protected.</span></span> <span data-ttu-id="58e37-146">When the key is successfully created, the command outputs the details of the created key.</span><span class="sxs-lookup"><span data-stu-id="58e37-146">When the key is successfully created, the command outputs the details of the created key.</span></span>

<span data-ttu-id="58e37-147">**Output**</span><span class="sxs-lookup"><span data-stu-id="58e37-147">**Output**</span></span>

![New key](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="58e37-149">You can now reference the created key by using its URI.</span><span class="sxs-lookup"><span data-stu-id="58e37-149">You can now reference the created key by using its URI.</span></span> <span data-ttu-id="58e37-150">If you create or import a key that has same name as an existing key, the original key is updated with the values specified in the new key.</span><span class="sxs-lookup"><span data-stu-id="58e37-150">If you create or import a key that has same name as an existing key, the original key is updated with the values specified in the new key.</span></span> <span data-ttu-id="58e37-151">You can access the previous version by using the version-specific URI of the key.</span><span class="sxs-lookup"><span data-stu-id="58e37-151">You can access the previous version by using the version-specific URI of the key.</span></span> <span data-ttu-id="58e37-152">For example:</span><span class="sxs-lookup"><span data-stu-id="58e37-152">For example:</span></span>

* <span data-ttu-id="58e37-153">Use "https://vault10.vault.local.azurestack.external:443/keys/key01" to always get the current version.</span><span class="sxs-lookup"><span data-stu-id="58e37-153">Use "https://vault10.vault.local.azurestack.external:443/keys/key01" to always get the current version.</span></span>
* <span data-ttu-id="58e37-154">Use "https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a" to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="58e37-154">Use "https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a" to get this specific version.</span></span>

### <a name="get-a-key"></a><span data-ttu-id="58e37-155">Get a key</span><span class="sxs-lookup"><span data-stu-id="58e37-155">Get a key</span></span>

<span data-ttu-id="58e37-156">Use the **Get-AzureKeyVaultKey** command to read a key and its details.</span><span class="sxs-lookup"><span data-stu-id="58e37-156">Use the **Get-AzureKeyVaultKey** command to read a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="58e37-157">Create a secret</span><span class="sxs-lookup"><span data-stu-id="58e37-157">Create a secret</span></span>

<span data-ttu-id="58e37-158">Use the **Set-AzureKeyVaultSecret** command to create or update a secret in a vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-158">Use the **Set-AzureKeyVaultSecret** command to create or update a secret in a vault.</span></span> <span data-ttu-id="58e37-159">A secret is created if one doesn’t already exist.</span><span class="sxs-lookup"><span data-stu-id="58e37-159">A secret is created if one doesn’t already exist.</span></span> <span data-ttu-id="58e37-160">A new version of the secret is created if it already exists.</span><span class="sxs-lookup"><span data-stu-id="58e37-160">A new version of the secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="58e37-161">**Output**</span><span class="sxs-lookup"><span data-stu-id="58e37-161">**Output**</span></span>

![Create a secret](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="58e37-163">Get a secret</span><span class="sxs-lookup"><span data-stu-id="58e37-163">Get a secret</span></span>

<span data-ttu-id="58e37-164">Use the **Get-AzureKeyVaultSecret** command to read a secret in a key vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-164">Use the **Get-AzureKeyVaultSecret** command to read a secret in a key vault.</span></span> <span data-ttu-id="58e37-165">This command can return all or specific versions of a secret.</span><span class="sxs-lookup"><span data-stu-id="58e37-165">This command can return all or specific versions of a secret.</span></span>

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="58e37-166">After you create the keys and secrets, you can authorize external applications to use them.</span><span class="sxs-lookup"><span data-stu-id="58e37-166">After you create the keys and secrets, you can authorize external applications to use them.</span></span>

## <a name="authorize-an-application-to-use-a-key-or-secret"></a><span data-ttu-id="58e37-167">Authorize an application to use a key or secret</span><span class="sxs-lookup"><span data-stu-id="58e37-167">Authorize an application to use a key or secret</span></span>

<span data-ttu-id="58e37-168">Use the **Set-AzureRmKeyVaultAccessPolicy** command to authorize an application to access a key or secret in the key vault.</span><span class="sxs-lookup"><span data-stu-id="58e37-168">Use the **Set-AzureRmKeyVaultAccessPolicy** command to authorize an application to access a key or secret in the key vault.</span></span>
<span data-ttu-id="58e37-169">In the following example, the vault name is *ContosoKeyVault* and the application you want to authorize has a client ID of *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*.</span><span class="sxs-lookup"><span data-stu-id="58e37-169">In the following example, the vault name is *ContosoKeyVault* and the application you want to authorize has a client ID of *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*.</span></span> <span data-ttu-id="58e37-170">To authorize the application, run the following command.</span><span class="sxs-lookup"><span data-stu-id="58e37-170">To authorize the application, run the following command.</span></span> <span data-ttu-id="58e37-171">Optionally, you can specify the **PermissionsToKeys** parameter to set permissions for a user, application, or a security group.</span><span class="sxs-lookup"><span data-stu-id="58e37-171">Optionally, you can specify the **PermissionsToKeys** parameter to set permissions for a user, application, or a security group.</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="58e37-172">If you want to authorize that same application to read secrets in your vault, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="58e37-172">If you want to authorize that same application to read secrets in your vault, run the following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="58e37-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="58e37-173">Next steps</span></span>

* [<span data-ttu-id="58e37-174">Deploy a VM with a password stored in Key Vault</span><span class="sxs-lookup"><span data-stu-id="58e37-174">Deploy a VM with a password stored in Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="58e37-175">Deploy a VM with a certificate stored in Key Vault</span><span class="sxs-lookup"><span data-stu-id="58e37-175">Deploy a VM with a certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md)
