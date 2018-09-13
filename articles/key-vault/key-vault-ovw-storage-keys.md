---
ms.assetid: ''
title: Azure Key Vault Storage Account Keys
description: Storage account keys provide a seemless integration between Azure Key Vault and key based access to Azure Storage Account.
ms.topic: conceptual
services: key-vault
ms.service: key-vault
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 08/21/2017
ms.openlocfilehash: 7545a035541a4e464a6c82acb9fa9de18cf8e86d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870293"
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="985b4-103">Azure Key Vault Storage Account Keys</span><span class="sxs-lookup"><span data-stu-id="985b4-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="985b4-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span><span class="sxs-lookup"><span data-stu-id="985b4-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="985b4-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="985b4-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span>

<span data-ttu-id="985b4-106">The Azure Storage Account (ASA) key feature manages secret rotation for you.</span><span class="sxs-lookup"><span data-stu-id="985b4-106">The Azure Storage Account (ASA) key feature manages secret rotation for you.</span></span> <span data-ttu-id="985b4-107">It also removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span><span class="sxs-lookup"><span data-stu-id="985b4-107">It also removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span>

<span data-ttu-id="985b4-108">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="985b4-108">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="985b4-109">Supporting interfaces</span><span class="sxs-lookup"><span data-stu-id="985b4-109">Supporting interfaces</span></span>

<span data-ttu-id="985b4-110">You'll find a complete listing and links to our programming and scripting interfaces in the [Key Vault Developer's Guide](key-vault-developers-guide.md#coding-with-key-vault).</span><span class="sxs-lookup"><span data-stu-id="985b4-110">You'll find a complete listing and links to our programming and scripting interfaces in the [Key Vault Developer's Guide](key-vault-developers-guide.md#coding-with-key-vault).</span></span>


## <a name="what-key-vault-manages"></a><span data-ttu-id="985b4-111">What Key Vault manages</span><span class="sxs-lookup"><span data-stu-id="985b4-111">What Key Vault manages</span></span>

<span data-ttu-id="985b4-112">Key Vault performs several internal management functions on your behalf when you use Managed Storage Account Keys.</span><span class="sxs-lookup"><span data-stu-id="985b4-112">Key Vault performs several internal management functions on your behalf when you use Managed Storage Account Keys.</span></span>

- <span data-ttu-id="985b4-113">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span><span class="sxs-lookup"><span data-stu-id="985b4-113">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span>
    - <span data-ttu-id="985b4-114">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="985b4-114">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>
    - <span data-ttu-id="985b4-115">Azure Key Vault regenerates (rotates) the keys periodically.</span><span class="sxs-lookup"><span data-stu-id="985b4-115">Azure Key Vault regenerates (rotates) the keys periodically.</span></span>
    - <span data-ttu-id="985b4-116">Key values are never returned in response to caller.</span><span class="sxs-lookup"><span data-stu-id="985b4-116">Key values are never returned in response to caller.</span></span>
    - <span data-ttu-id="985b4-117">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span><span class="sxs-lookup"><span data-stu-id="985b4-117">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span>
- <span data-ttu-id="985b4-118">Azure Key Vault allows you, the vault/object owner, to create SAS (Shared Access Signature, account or service SAS) definitions.</span><span class="sxs-lookup"><span data-stu-id="985b4-118">Azure Key Vault allows you, the vault/object owner, to create SAS (Shared Access Signature, account or service SAS) definitions.</span></span>
    - <span data-ttu-id="985b4-119">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span><span class="sxs-lookup"><span data-stu-id="985b4-119">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="985b4-120">For more information, see the SAS definition operations in the [Azure Key Vault REST API reference](/rest/api/keyvault).</span><span class="sxs-lookup"><span data-stu-id="985b4-120">For more information, see the SAS definition operations in the [Azure Key Vault REST API reference](/rest/api/keyvault).</span></span>

## <a name="naming-guidance"></a><span data-ttu-id="985b4-121">Naming guidance</span><span class="sxs-lookup"><span data-stu-id="985b4-121">Naming guidance</span></span>

- <span data-ttu-id="985b4-122">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span><span class="sxs-lookup"><span data-stu-id="985b4-122">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>
- <span data-ttu-id="985b4-123">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span><span class="sxs-lookup"><span data-stu-id="985b4-123">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="985b4-124">Developer experience</span><span class="sxs-lookup"><span data-stu-id="985b4-124">Developer experience</span></span>

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="985b4-125">Before Azure Key Vault Storage Keys</span><span class="sxs-lookup"><span data-stu-id="985b4-125">Before Azure Key Vault Storage Keys</span></span>

<span data-ttu-id="985b4-126">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="985b4-126">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span>
1. <span data-ttu-id="985b4-127">Store connection string or SAS token in Azure AppService application settings or another storage.</span><span class="sxs-lookup"><span data-stu-id="985b4-127">Store connection string or SAS token in Azure AppService application settings or another storage.</span></span>
1. <span data-ttu-id="985b4-128">At application start-up, fetch the connection string or SAS token.</span><span class="sxs-lookup"><span data-stu-id="985b4-128">At application start-up, fetch the connection string or SAS token.</span></span>
1. <span data-ttu-id="985b4-129">Create [CloudStorageAccount](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount) to interact with storage.</span><span class="sxs-lookup"><span data-stu-id="985b4-129">Create [CloudStorageAccount](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount) to interact with storage.</span></span>

```cs
// The Connection string is being fetched from App Service application settings
var connectionStringOrSasToken = CloudConfigurationManager.GetSetting("StorageConnectionString");
var storageAccount = CloudStorageAccount.Parse(connectionStringOrSasToken);
var blobClient = storageAccount.CreateCloudBlobClient();
 ```

### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="985b4-130">After Azure Key Vault Storage Keys</span><span class="sxs-lookup"><span data-stu-id="985b4-130">After Azure Key Vault Storage Keys</span></span>

<span data-ttu-id="985b4-131">Developers create a [KeyVaultClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault.keyvaultclient) and leverage that to get the SAS token for their storage.</span><span class="sxs-lookup"><span data-stu-id="985b4-131">Developers create a [KeyVaultClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault.keyvaultclient) and leverage that to get the SAS token for their storage.</span></span> <span data-ttu-id="985b4-132">Afterwards, they create [CloudStorageAccount](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount) with that token.</span><span class="sxs-lookup"><span data-stu-id="985b4-132">Afterwards, they create [CloudStorageAccount](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount) with that token.</span></span>

```cs
// Create KeyVaultClient with vault credentials
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

// Get a SAS token for our storage from Key Vault
var sasToken = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token.
var accountSasCredential = new StorageCredentials(sasToken.Value);

// Use the storage credentials and the Blob storage endpoint to create a new Blob service client.
var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null);

var blobClientWithSas = accountWithSas.CreateCloudBlobClient();

// Use the blobClientWithSas
...

// If your SAS token is about to expire, get the SAS Token again from Key Vault and update it.
sasToken = await kv.GetSecretAsync("SecretUri");
accountSasCredential.UpdateSASToken(sasToken);
```

 ### <a name="developer-guidance"></a><span data-ttu-id="985b4-133">Developer guidance</span><span class="sxs-lookup"><span data-stu-id="985b4-133">Developer guidance</span></span>

- <span data-ttu-id="985b4-134">Only allow Key Vault to manage your ASA keys.</span><span class="sxs-lookup"><span data-stu-id="985b4-134">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="985b4-135">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span><span class="sxs-lookup"><span data-stu-id="985b4-135">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span>
- <span data-ttu-id="985b4-136">Do not allow ASA keys to be managed by more than one Key Vault object.</span><span class="sxs-lookup"><span data-stu-id="985b4-136">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span>
- <span data-ttu-id="985b4-137">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span><span class="sxs-lookup"><span data-stu-id="985b4-137">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span>

## <a name="getting-started"></a><span data-ttu-id="985b4-138">Getting started</span><span class="sxs-lookup"><span data-stu-id="985b4-138">Getting started</span></span>

### <a name="give-key-vault-access-to-your-storage-account"></a><span data-ttu-id="985b4-139">Give Key Vault access to your Storage Account</span><span class="sxs-lookup"><span data-stu-id="985b4-139">Give Key Vault access to your Storage Account</span></span> 

<span data-ttu-id="985b4-140">Like many applications, Key Vault is registered with Azure AD in order to use OAuth to access other services.</span><span class="sxs-lookup"><span data-stu-id="985b4-140">Like many applications, Key Vault is registered with Azure AD in order to use OAuth to access other services.</span></span> <span data-ttu-id="985b4-141">During registration, [a service principal](/azure/active-directory/develop/app-objects-and-service-principals) object is created, which is used to represent the application's identity at run time.</span><span class="sxs-lookup"><span data-stu-id="985b4-141">During registration, [a service principal](/azure/active-directory/develop/app-objects-and-service-principals) object is created, which is used to represent the application's identity at run time.</span></span> <span data-ttu-id="985b4-142">The service principal is also used to authorize the application's identity to access another resource, through role-based access control (RBAC).</span><span class="sxs-lookup"><span data-stu-id="985b4-142">The service principal is also used to authorize the application's identity to access another resource, through role-based access control (RBAC).</span></span>

<span data-ttu-id="985b4-143">The Azure Key Vault application identity needs permissions to *list* and *regenerate* keys for your storage account.</span><span class="sxs-lookup"><span data-stu-id="985b4-143">The Azure Key Vault application identity needs permissions to *list* and *regenerate* keys for your storage account.</span></span> <span data-ttu-id="985b4-144">Set up these permissions using the following steps:</span><span class="sxs-lookup"><span data-stu-id="985b4-144">Set up these permissions using the following steps:</span></span>

```powershell
# Get the resource ID of the Azure Storage Account you want to manage.
# Below, we are fetching a storage account using Azure Resource Manager
$storage = Get-AzureRmStorageAccount -ResourceGroupName "mystorageResourceGroup" -StorageAccountName "mystorage"

# Get Application ID of Azure Key Vault's service principal
$servicePrincipal = Get-AzureRmADServicePrincipal -ServicePrincipalName cfa8b339-82a2-471a-a3c9-0fc0be7a4093

# Assign Storage Key Operator role to Azure Key Vault Identity
New-AzureRmRoleAssignment -ObjectId $servicePrincipal.Id -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope $storage.Id
```

    >[!NOTE]
    > For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role."*

## <a name="working-example"></a><span data-ttu-id="985b4-145">Working example</span><span class="sxs-lookup"><span data-stu-id="985b4-145">Working example</span></span>

<span data-ttu-id="985b4-146">The following example demonstrates creating a Key Vault managed Azure Storage Account and the associated SAS definitions.</span><span class="sxs-lookup"><span data-stu-id="985b4-146">The following example demonstrates creating a Key Vault managed Azure Storage Account and the associated SAS definitions.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="985b4-147">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="985b4-147">Prerequisite</span></span>

<span data-ttu-id="985b4-148">Ensure you have completed [Setup for role-based access control (RBAC) permissions](#setup-for-role-based-access-control-rbac-permissions).</span><span class="sxs-lookup"><span data-stu-id="985b4-148">Ensure you have completed [Setup for role-based access control (RBAC) permissions](#setup-for-role-based-access-control-rbac-permissions).</span></span>

### <a name="setup"></a><span data-ttu-id="985b4-149">Setup</span><span class="sxs-lookup"><span data-stu-id="985b4-149">Setup</span></span>

```powershell
# This is the name of our Key Vault
$keyVaultName = "mykeyVault"

# Fetching all the storage account object, of the ASA we want to manage with KeyVault
$storage = Get-AzureRmStorageAccount -ResourceGroupName "mystorageResourceGroup" -StorageAccountName "mystorage"

# Get ObjectId of Azure KeyVault Identity service principal
$servicePrincipalId = $(Get-AzureRmADServicePrincipal -ServicePrincipalName cfa8b339-82a2-471a-a3c9-0fc0be7a4093).Id
```

<span data-ttu-id="985b4-150">Next, set the permissions for **your account** to ensure that you can manage all the storage permissions in the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="985b4-150">Next, set the permissions for **your account** to ensure that you can manage all the storage permissions in the Key Vault.</span></span> <span data-ttu-id="985b4-151">In the example below, our Azure account is _developer@contoso.com_.</span><span class="sxs-lookup"><span data-stu-id="985b4-151">In the example below, our Azure account is _developer@contoso.com_.</span></span>

```powershell
# Searching our Azure Active Directory for our account's ObjectId
$userPrincipalId = $(Get-AzureRmADUser -SearchString "developer@contoso.com").Id

# We use the ObjectId we found to setting permissions on the vault
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ObjectId $userPrincipalId -PermissionsToStorage all
```

### <a name="create-a-key-vault-managed-storage-account"></a><span data-ttu-id="985b4-152">Create a Key Vault Managed Storage Account</span><span class="sxs-lookup"><span data-stu-id="985b4-152">Create a Key Vault Managed Storage Account</span></span>

<span data-ttu-id="985b4-153">Now, create a Managed Storage Account in Azure Key Vault and use an access key from your storage account to create the SAS tokens.</span><span class="sxs-lookup"><span data-stu-id="985b4-153">Now, create a Managed Storage Account in Azure Key Vault and use an access key from your storage account to create the SAS tokens.</span></span>
- <span data-ttu-id="985b4-154">`-ActiveKeyName` uses 'key2' to generate the SAS tokens.</span><span class="sxs-lookup"><span data-stu-id="985b4-154">`-ActiveKeyName` uses 'key2' to generate the SAS tokens.</span></span>
- <span data-ttu-id="985b4-155">`-AccountName` is used to identify your managed storage account.</span><span class="sxs-lookup"><span data-stu-id="985b4-155">`-AccountName` is used to identify your managed storage account.</span></span> <span data-ttu-id="985b4-156">Below, we are using the storage account name to keep it simple but it can be any name.</span><span class="sxs-lookup"><span data-stu-id="985b4-156">Below, we are using the storage account name to keep it simple but it can be any name.</span></span>
- <span data-ttu-id="985b4-157">`-DisableAutoRegenerateKey` specifies not regenerate the storage account keys.</span><span class="sxs-lookup"><span data-stu-id="985b4-157">`-DisableAutoRegenerateKey` specifies not regenerate the storage account keys.</span></span>

```powershell
# Adds your storage account to be managed by Key Vault and will use the access key, key2
Add-AzureKeyVaultManagedStorageAccount -VaultName $keyVaultName -AccountName $storage.StorageAccountName -AccountResourceId $storage.Id -ActiveKeyName key2 -DisableAutoRegenerateKey
```

### <a name="key-regeneration"></a><span data-ttu-id="985b4-158">Key regeneration</span><span class="sxs-lookup"><span data-stu-id="985b4-158">Key regeneration</span></span>

<span data-ttu-id="985b4-159">If you want Key Vault to regenerate your storage's access keys periodically, you can set a regeneration period.</span><span class="sxs-lookup"><span data-stu-id="985b4-159">If you want Key Vault to regenerate your storage's access keys periodically, you can set a regeneration period.</span></span> <span data-ttu-id="985b4-160">Below, we are setting a regeneration period of 3 days.</span><span class="sxs-lookup"><span data-stu-id="985b4-160">Below, we are setting a regeneration period of 3 days.</span></span> <span data-ttu-id="985b4-161">After 3 days, Key Vault will regenerate 'key1' and swap the active key from 'key2' to 'key1'.</span><span class="sxs-lookup"><span data-stu-id="985b4-161">After 3 days, Key Vault will regenerate 'key1' and swap the active key from 'key2' to 'key1'.</span></span>

```powershell
$regenPeriod = [System.Timespan]::FromDays(3)
$accountName = $storage.StorageAccountName

Add-AzureKeyVaultManagedStorageAccount -VaultName $keyVaultName -AccountName $accountName -AccountResourceId $storage.Id -ActiveKeyName key2 -RegenerationPeriod $regenPeriod
```

### <a name="set-sas-definitions"></a><span data-ttu-id="985b4-162">Set SAS definitions</span><span class="sxs-lookup"><span data-stu-id="985b4-162">Set SAS definitions</span></span>

<span data-ttu-id="985b4-163">The account SAS provides access to the blob service with different permissions.</span><span class="sxs-lookup"><span data-stu-id="985b4-163">The account SAS provides access to the blob service with different permissions.</span></span>
<span data-ttu-id="985b4-164">Set the SAS definitions in Key Vault for your managed storage account.</span><span class="sxs-lookup"><span data-stu-id="985b4-164">Set the SAS definitions in Key Vault for your managed storage account.</span></span>
- <span data-ttu-id="985b4-165">`-AccountName` is the name of the managed storage account in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="985b4-165">`-AccountName` is the name of the managed storage account in Key Vault.</span></span>
- <span data-ttu-id="985b4-166">`-Name` is the identifier for the SAS token in your storage.</span><span class="sxs-lookup"><span data-stu-id="985b4-166">`-Name` is the identifier for the SAS token in your storage.</span></span>
- <span data-ttu-id="985b4-167">`-ValidityPeriod` sets the expiration date for the generated SAS token.</span><span class="sxs-lookup"><span data-stu-id="985b4-167">`-ValidityPeriod` sets the expiration date for the generated SAS token.</span></span>

```powershell
$validityPeriod = [System.Timespan]::FromDays(1)
$readSasName = "readBlobSas"
$writeSasName = "writeBlobSas"

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName $keyVaultName -AccountName $accountName -Name $readSasName -Protocol HttpsOnly -ValidityPeriod $validityPeriod -Permission Read,List

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service,Object -VaultName $keyVaultName -AccountName $accountName -Name $writeSasName -Protocol HttpsOnly -ValidityPeriod $validityPeriod -Permission Read,List,Write
```

### <a name="get-sas-tokens"></a><span data-ttu-id="985b4-168">Get SAS tokens</span><span class="sxs-lookup"><span data-stu-id="985b4-168">Get SAS tokens</span></span>

<span data-ttu-id="985b4-169">Get the corresponding SAS tokens and make calls to storage.</span><span class="sxs-lookup"><span data-stu-id="985b4-169">Get the corresponding SAS tokens and make calls to storage.</span></span> <span data-ttu-id="985b4-170">`-SecretName` is constructed using the input from the `AccountName` and `Name` parameters when you executed [Set-AzureKeyVaultManagedStorageSasDefinition](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Set-AzureKeyVaultManagedStorageSasDefinition).</span><span class="sxs-lookup"><span data-stu-id="985b4-170">`-SecretName` is constructed using the input from the `AccountName` and `Name` parameters when you executed [Set-AzureKeyVaultManagedStorageSasDefinition](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Set-AzureKeyVaultManagedStorageSasDefinition).</span></span>

```powershell
$readSasToken = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -SecretName "$accountName-$readSasName").SecretValueText
$writeSasToken = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -SecretName "$accountName-$writeSasName").SecretValueText
```

### <a name="create-storage"></a><span data-ttu-id="985b4-171">Create storage</span><span class="sxs-lookup"><span data-stu-id="985b4-171">Create storage</span></span>

<span data-ttu-id="985b4-172">Notice that trying to access with *$readSasToken* fails, but that we are able to access with *$writeSasToken*.</span><span class="sxs-lookup"><span data-stu-id="985b4-172">Notice that trying to access with *$readSasToken* fails, but that we are able to access with *$writeSasToken*.</span></span>

```powershell
$context1 = New-AzureStorageContext -SasToken $readSasToken -StorageAccountName $storage.StorageAccountName
$context2 = New-AzureStorageContext -SasToken $writeSasToken -StorageAccountName $storage.StorageAccountName

# Ensure the txt file in command exists in local path mentioned
Set-AzureStorageBlobContent -Container containertest1 -File "./abc.txt" -Context $context1
Set-AzureStorageBlobContent -Container cont1-file "./file.txt" -Context $context2
```

<span data-ttu-id="985b4-173">You are able access the storage blob content with the SAS token that has write access.</span><span class="sxs-lookup"><span data-stu-id="985b4-173">You are able access the storage blob content with the SAS token that has write access.</span></span>

### <a name="relevant-powershell-cmdlets"></a><span data-ttu-id="985b4-174">Relevant Powershell cmdlets</span><span class="sxs-lookup"><span data-stu-id="985b4-174">Relevant Powershell cmdlets</span></span>

- [<span data-ttu-id="985b4-175">Get-AzureKeyVaultManagedStorageAccount</span><span class="sxs-lookup"><span data-stu-id="985b4-175">Get-AzureKeyVaultManagedStorageAccount</span></span>](https://docs.microsoft.com/powershell/module/azurerm.keyvault/get-azurekeyvaultmanagedstorageaccount)
- [<span data-ttu-id="985b4-176">Add-AzureKeyVaultManagedStorageAccount</span><span class="sxs-lookup"><span data-stu-id="985b4-176">Add-AzureKeyVaultManagedStorageAccount</span></span>](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Add-AzureKeyVaultManagedStorageAccount)
- [<span data-ttu-id="985b4-177">Get-AzureKeyVaultManagedStorageSasDefinition</span><span class="sxs-lookup"><span data-stu-id="985b4-177">Get-AzureKeyVaultManagedStorageSasDefinition</span></span>](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Get-AzureKeyVaultManagedStorageSasDefinition)
- [<span data-ttu-id="985b4-178">Update-AzureKeyVaultManagedStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="985b4-178">Update-AzureKeyVaultManagedStorageAccountKey</span></span>](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Update-AzureKeyVaultManagedStorageAccountKey)
- [<span data-ttu-id="985b4-179">Remove-AzureKeyVaultManagedStorageAccount</span><span class="sxs-lookup"><span data-stu-id="985b4-179">Remove-AzureKeyVaultManagedStorageAccount</span></span>](https://docs.microsoft.com/powershell/module/azurerm.keyvault/remove-azurekeyvaultmanagedstorageaccount)
- [<span data-ttu-id="985b4-180">Remove-AzureKeyVaultManagedStorageSasDefinition</span><span class="sxs-lookup"><span data-stu-id="985b4-180">Remove-AzureKeyVaultManagedStorageSasDefinition</span></span>](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Remove-AzureKeyVaultManagedStorageSasDefinition)
- [<span data-ttu-id="985b4-181">Set-AzureKeyVaultManagedStorageSasDefinition</span><span class="sxs-lookup"><span data-stu-id="985b4-181">Set-AzureKeyVaultManagedStorageSasDefinition</span></span>](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Set-AzureKeyVaultManagedStorageSasDefinition)

## <a name="storage-account-onboarding"></a><span data-ttu-id="985b4-182">Storage account onboarding</span><span class="sxs-lookup"><span data-stu-id="985b4-182">Storage account onboarding</span></span>

<span data-ttu-id="985b4-183">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span><span class="sxs-lookup"><span data-stu-id="985b4-183">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="985b4-184">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span><span class="sxs-lookup"><span data-stu-id="985b4-184">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="985b4-185">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span><span class="sxs-lookup"><span data-stu-id="985b4-185">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="985b4-186">If the *list* call fails, the Key Vault object creation fails with an HTTP status code of *Forbidden*.</span><span class="sxs-lookup"><span data-stu-id="985b4-186">If the *list* call fails, the Key Vault object creation fails with an HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="985b4-187">The keys listed in this fashion are cached with your key vault entity storage.</span><span class="sxs-lookup"><span data-stu-id="985b4-187">The keys listed in this fashion are cached with your key vault entity storage.</span></span>

<span data-ttu-id="985b4-188">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span><span class="sxs-lookup"><span data-stu-id="985b4-188">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="985b4-189">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span><span class="sxs-lookup"><span data-stu-id="985b4-189">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="985b4-190">Key Vault lists RBAC permissions on the storage account resource.</span><span class="sxs-lookup"><span data-stu-id="985b4-190">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="985b4-191">Key Vault validates the response via regular expression matching of actions and non-actions.</span><span class="sxs-lookup"><span data-stu-id="985b4-191">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span>

<span data-ttu-id="985b4-192">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=key+vault+storage&type=&language=).</span><span class="sxs-lookup"><span data-stu-id="985b4-192">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=key+vault+storage&type=&language=).</span></span>

<span data-ttu-id="985b4-193">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span><span class="sxs-lookup"><span data-stu-id="985b4-193">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span>

<span data-ttu-id="985b4-194">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span><span class="sxs-lookup"><span data-stu-id="985b4-194">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="985b4-195">Other applications</span><span class="sxs-lookup"><span data-stu-id="985b4-195">Other applications</span></span>

- <span data-ttu-id="985b4-196">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="985b4-196">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="985b4-197">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="985b4-197">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="985b4-198">See also</span><span class="sxs-lookup"><span data-stu-id="985b4-198">See also</span></span>

- [<span data-ttu-id="985b4-199">About keys, secrets, and certificates</span><span class="sxs-lookup"><span data-stu-id="985b4-199">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="985b4-200">Key Vault Team Blog</span><span class="sxs-lookup"><span data-stu-id="985b4-200">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
