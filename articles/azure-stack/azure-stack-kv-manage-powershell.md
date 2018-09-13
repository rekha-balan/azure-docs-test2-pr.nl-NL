---
title: Manage Key Vault in Azure Stack using PowerShell | Microsoft Docs
description: Learn how to manage Key Vault in Azure Stack using PowerShell.
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: sngun
ms.openlocfilehash: 46e45f4c06431e1bf38fbd03720fca5294c62b4b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550752"
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="7f1df-103">Manage Key Vault in Azure Stack using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f1df-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="7f1df-104">This article helps you get started to create and manage Key Vault in Azure Stack by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f1df-104">This article helps you get started to create and manage Key Vault in Azure Stack by using PowerShell.</span></span> 

> [!NOTE]
> <span data-ttu-id="7f1df-105">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span><span class="sxs-lookup"><span data-stu-id="7f1df-105">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span></span> <span data-ttu-id="7f1df-106">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span><span class="sxs-lookup"><span data-stu-id="7f1df-106">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span></span> 

<span data-ttu-id="7f1df-107">The Key Vault PowerShell commands described in this article are available as a part of the Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="7f1df-107">The Key Vault PowerShell commands described in this article are available as a part of the Azure PowerShell SDK.</span></span>  <span data-ttu-id="7f1df-108">Following sections describe the PowerShell commands required to create a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications to invoke operations in the vault.</span><span class="sxs-lookup"><span data-stu-id="7f1df-108">Following sections describe the PowerShell commands required to create a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications to invoke operations in the vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7f1df-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7f1df-109">Prerequisites</span></span>
* [<span data-ttu-id="7f1df-110">Install PowerShell for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7f1df-110">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* <span data-ttu-id="7f1df-111">Azure Stack administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="7f1df-111">Azure Stack administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="7f1df-112">Tenants must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="7f1df-112">Tenants must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span> 

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="7f1df-113">Enable your tenant subscription for vault operations</span><span class="sxs-lookup"><span data-stu-id="7f1df-113">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="7f1df-114">Before you can issue any operations against a key vault, you need to ensure that your tenant subscription is enabled for vault operations.</span><span class="sxs-lookup"><span data-stu-id="7f1df-114">Before you can issue any operations against a key vault, you need to ensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="7f1df-115">To verify, run the following command:</span><span class="sxs-lookup"><span data-stu-id="7f1df-115">To verify, run the following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="7f1df-116">**Output**</span><span class="sxs-lookup"><span data-stu-id="7f1df-116">**Output**</span></span>

<span data-ttu-id="7f1df-117">If your subscription is enabled for vault operations, the output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span><span class="sxs-lookup"><span data-stu-id="7f1df-117">If your subscription is enabled for vault operations, the output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![registration state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="7f1df-119">If that’s not the case, invoke the following command to register the Key Vault service in your subscription:</span><span class="sxs-lookup"><span data-stu-id="7f1df-119">If that’s not the case, invoke the following command to register the Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="7f1df-120">**Output**</span><span class="sxs-lookup"><span data-stu-id="7f1df-120">**Output**</span></span>

<span data-ttu-id="7f1df-121">If the registration is successful, the output shows the following:</span><span class="sxs-lookup"><span data-stu-id="7f1df-121">If the registration is successful, the output shows the following:</span></span>

![register](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="7f1df-123">The following sections assume Key Vault service is registered within the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="7f1df-123">The following sections assume Key Vault service is registered within the tenant subscription.</span></span> <span data-ttu-id="7f1df-124">When invoking key vault commands, if you get an error- "The subscription is not registered to use namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled the Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span><span class="sxs-lookup"><span data-stu-id="7f1df-124">When invoking key vault commands, if you get an error- "The subscription is not registered to use namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled the Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="7f1df-125">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="7f1df-125">Create a key vault</span></span> 

<span data-ttu-id="7f1df-126">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span><span class="sxs-lookup"><span data-stu-id="7f1df-126">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="7f1df-127">Use the following command to create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="7f1df-127">Use the following command to create a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="7f1df-128">**Output**</span><span class="sxs-lookup"><span data-stu-id="7f1df-128">**Output**</span></span>

![new resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="7f1df-130">Now, use the **New-AzureRMKeyVault** command to create a key vault in the resource group that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7f1df-130">Now, use the **New-AzureRMKeyVault** command to create a key vault in the resource group that you created earlier.</span></span> <span data-ttu-id="7f1df-131">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span><span class="sxs-lookup"><span data-stu-id="7f1df-131">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="7f1df-132">Run the following command to create a key vault:</span><span class="sxs-lookup"><span data-stu-id="7f1df-132">Run the following command to create a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="7f1df-133">**Output**</span><span class="sxs-lookup"><span data-stu-id="7f1df-133">**Output**</span></span>

![new kv](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="7f1df-135">The output of this command shows the properties of the key vault that you created.</span><span class="sxs-lookup"><span data-stu-id="7f1df-135">The output of this command shows the properties of the key vault that you created.</span></span> <span data-ttu-id="7f1df-136">When an application accesses this vault, it uses the **Vault URI** property shown in the output.</span><span class="sxs-lookup"><span data-stu-id="7f1df-136">When an application accesses this vault, it uses the **Vault URI** property shown in the output.</span></span> <span data-ttu-id="7f1df-137">For example, the vault URI here is **https://vault01.vault.local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="7f1df-137">For example, the vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="7f1df-138">Applications interacting with this key vault through REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="7f1df-138">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="7f1df-139">In ADFS based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span><span class="sxs-lookup"><span data-stu-id="7f1df-139">In ADFS based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="7f1df-140">No user or application have access permission to use this vault".</span><span class="sxs-lookup"><span data-stu-id="7f1df-140">No user or application have access permission to use this vault".</span></span> <span data-ttu-id="7f1df-141">To resolve this issue, set an access policy for the vault by using the [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span><span class="sxs-lookup"><span data-stu-id="7f1df-141">To resolve this issue, set an access policy for the vault by using the [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain the security identifier(SID) of the active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set the key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="7f1df-142">Manage keys and secrets</span><span class="sxs-lookup"><span data-stu-id="7f1df-142">Manage keys and secrets</span></span>

<span data-ttu-id="7f1df-143">After creating a vault, use the following steps to create and manage keys and secrets within the vault.</span><span class="sxs-lookup"><span data-stu-id="7f1df-143">After creating a vault, use the following steps to create and manage keys and secrets within the vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="7f1df-144">Create a key</span><span class="sxs-lookup"><span data-stu-id="7f1df-144">Create a key</span></span>

<span data-ttu-id="7f1df-145">Use the **Add-AzureKeyVaultKey** command to create or import a software protected key in a key vault.</span><span class="sxs-lookup"><span data-stu-id="7f1df-145">Use the **Add-AzureKeyVaultKey** command to create or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="7f1df-146">The **Destination** parameter is used to specify that the key is software protected.</span><span class="sxs-lookup"><span data-stu-id="7f1df-146">The **Destination** parameter is used to specify that the key is software protected.</span></span> <span data-ttu-id="7f1df-147">When the key is successfully created, the command outputs the details of the created key.</span><span class="sxs-lookup"><span data-stu-id="7f1df-147">When the key is successfully created, the command outputs the details of the created key.</span></span>

<span data-ttu-id="7f1df-148">**Output**</span><span class="sxs-lookup"><span data-stu-id="7f1df-148">**Output**</span></span>

![New Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="7f1df-150">You can now reference the created key by using its URI.</span><span class="sxs-lookup"><span data-stu-id="7f1df-150">You can now reference the created key by using its URI.</span></span> <span data-ttu-id="7f1df-151">If you create or import a key that has same name as an existing key, the original key is updated with the values specified in the new key.</span><span class="sxs-lookup"><span data-stu-id="7f1df-151">If you create or import a key that has same name as an existing key, the original key is updated with the values specified in the new key.</span></span>  <span data-ttu-id="7f1df-152">You can access the previous version by using the version-specific URI of the key.</span><span class="sxs-lookup"><span data-stu-id="7f1df-152">You can access the previous version by using the version-specific URI of the key.</span></span> <span data-ttu-id="7f1df-153">For example,</span><span class="sxs-lookup"><span data-stu-id="7f1df-153">For example,</span></span> 

* <span data-ttu-id="7f1df-154">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** to always get the current version</span><span class="sxs-lookup"><span data-stu-id="7f1df-154">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** to always get the current version</span></span>  
* <span data-ttu-id="7f1df-155">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** to get this specific version</span><span class="sxs-lookup"><span data-stu-id="7f1df-155">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** to get this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="7f1df-156">Get a key</span><span class="sxs-lookup"><span data-stu-id="7f1df-156">Get a key</span></span>

<span data-ttu-id="7f1df-157">Use the **Get-AzureKeyVaultKey** command to read a key and its details.</span><span class="sxs-lookup"><span data-stu-id="7f1df-157">Use the **Get-AzureKeyVaultKey** command to read a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="7f1df-158">Create a secret</span><span class="sxs-lookup"><span data-stu-id="7f1df-158">Create a secret</span></span>

<span data-ttu-id="7f1df-159">Use the **Set-AzureKeyVaultSecret** command to create or update a secret in a vault.</span><span class="sxs-lookup"><span data-stu-id="7f1df-159">Use the **Set-AzureKeyVaultSecret** command to create or update a secret in a vault.</span></span> <span data-ttu-id="7f1df-160">A secret is created if it doesn’t already exist, and a new version of the secret is created if it already exists.</span><span class="sxs-lookup"><span data-stu-id="7f1df-160">A secret is created if it doesn’t already exist, and a new version of the secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="7f1df-161">**Output**</span><span class="sxs-lookup"><span data-stu-id="7f1df-161">**Output**</span></span>

![create secret](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="7f1df-163">Get a secret</span><span class="sxs-lookup"><span data-stu-id="7f1df-163">Get a secret</span></span>

<span data-ttu-id="7f1df-164">Use the **Get-AzureKeyVaultSecret** command to read a secret in a key vault.</span><span class="sxs-lookup"><span data-stu-id="7f1df-164">Use the **Get-AzureKeyVaultSecret** command to read a secret in a key vault.</span></span> <span data-ttu-id="7f1df-165">This command can return all or specific versions of a secret.</span><span class="sxs-lookup"><span data-stu-id="7f1df-165">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="7f1df-166">After creating keys and secrets, you can authorize external applications to use them.</span><span class="sxs-lookup"><span data-stu-id="7f1df-166">After creating keys and secrets, you can authorize external applications to use them.</span></span>

## <a name="authorize-an-application-to-use-a-key-or-secret"></a><span data-ttu-id="7f1df-167">Authorize an application to use a key or secret</span><span class="sxs-lookup"><span data-stu-id="7f1df-167">Authorize an application to use a key or secret</span></span>

<span data-ttu-id="7f1df-168">To authorize an application to access a key or secret in the key vault, use the **Set-AzureRmKeyVaultAccessPolicy** command.</span><span class="sxs-lookup"><span data-stu-id="7f1df-168">To authorize an application to access a key or secret in the key vault, use the **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="7f1df-169">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span><span class="sxs-lookup"><span data-stu-id="7f1df-169">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="7f1df-170">Run the following command to authorize the application.</span><span class="sxs-lookup"><span data-stu-id="7f1df-170">Run the following command to authorize the application.</span></span> <span data-ttu-id="7f1df-171">Optionally, you can specify the **PermissionsToKeys** parameter to set permissions for a user, application, or a security group:</span><span class="sxs-lookup"><span data-stu-id="7f1df-171">Optionally, you can specify the **PermissionsToKeys** parameter to set permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="7f1df-172">If you want to authorize that same application to read secrets in your vault, run the following:</span><span class="sxs-lookup"><span data-stu-id="7f1df-172">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="7f1df-173">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7f1df-173">Next Steps</span></span>
* [<span data-ttu-id="7f1df-174">Deploy a VM with password stored in a Key Vault</span><span class="sxs-lookup"><span data-stu-id="7f1df-174">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="7f1df-175">Deploy a VM with certificate stored in Key Vault</span><span class="sxs-lookup"><span data-stu-id="7f1df-175">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 






