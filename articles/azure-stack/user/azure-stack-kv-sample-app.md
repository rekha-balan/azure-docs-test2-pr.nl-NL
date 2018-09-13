---
title: Allow applications to retrieve Azure Stack Key Vault secrets | Microsoft Docs
description: Use a sample app to work with Azure Stack Key Vault
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/15/2018
ms.author: sethm
ms.openlocfilehash: ed02174247de1a99f3d9a4880fd0afa60f867552
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867359"
---
# <a name="a-sample-application-that-uses-keys-and-secrets-stored-in-a-key-vault"></a><span data-ttu-id="42de9-103">A sample application that uses keys and secrets stored in a key vault</span><span class="sxs-lookup"><span data-stu-id="42de9-103">A sample application that uses keys and secrets stored in a key vault</span></span>

<span data-ttu-id="42de9-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="42de9-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="42de9-105">Follow the steps in this article to run a sample application (HelloKeyVault) that retrieves keys and secrets from a key vault in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="42de9-105">Follow the steps in this article to run a sample application (HelloKeyVault) that retrieves keys and secrets from a key vault in Azure Stack.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42de9-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42de9-106">Prerequisites</span></span>

<span data-ttu-id="42de9-107">You can install the following prerequisites from the Azure Stack [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="42de9-107">You can install the following prerequisites from the Azure Stack [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="42de9-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="42de9-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>
* <span data-ttu-id="42de9-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="42de9-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>

## <a name="create-and-get-the-key-vault-and-application-settings"></a><span data-ttu-id="42de9-110">Create and get the key vault and application settings</span><span class="sxs-lookup"><span data-stu-id="42de9-110">Create and get the key vault and application settings</span></span>

<span data-ttu-id="42de9-111">To prepare for the sample application:</span><span class="sxs-lookup"><span data-stu-id="42de9-111">To prepare for the sample application:</span></span>

* <span data-ttu-id="42de9-112">Create a key vault in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="42de9-112">Create a key vault in Azure Stack.</span></span>
* <span data-ttu-id="42de9-113">Register an application in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42de9-113">Register an application in Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42de9-114">You can use the Azure portal or PowerShell to prepare for the sample application.</span><span class="sxs-lookup"><span data-stu-id="42de9-114">You can use the Azure portal or PowerShell to prepare for the sample application.</span></span> <span data-ttu-id="42de9-115">This article shows how to create a key vault and register an application by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42de9-115">This article shows how to create a key vault and register an application by using PowerShell.</span></span>

>[!NOTE]
><span data-ttu-id="42de9-116">By default, the PowerShell script creates a new application in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42de9-116">By default, the PowerShell script creates a new application in Active Directory.</span></span> <span data-ttu-id="42de9-117">However, you can register one of your existing applications.</span><span class="sxs-lookup"><span data-stu-id="42de9-117">However, you can register one of your existing applications.</span></span>

 <span data-ttu-id="42de9-118">Before running the following script, make sure you provide values for the `aadTenantName` and `applicationPassword` variables.</span><span class="sxs-lookup"><span data-stu-id="42de9-118">Before running the following script, make sure you provide values for the `aadTenantName` and `applicationPassword` variables.</span></span> <span data-ttu-id="42de9-119">If you don't specify a value for `applicationPassword`, this script generates a random password.</span><span class="sxs-lookup"><span data-stu-id="42de9-119">If you don't specify a value for `applicationPassword`, this script generates a random password.</span></span>

```powershell
$vaultName           = 'myVault'
$resourceGroupName   = 'myResourceGroup'
$applicationName     = 'myApp'
$location            = 'local'

# Password for the application. If not specified, this script will generate a random password during app creation.
$applicationPassword = ''

# Function to generate a random password for the application.
Function GenerateSymmetricKey()
{
    $key = New-Object byte[](32)
    $rng = [System.Security.Cryptography.RNGCryptoServiceProvider]::Create()
    $rng.GetBytes($key)
    return [System.Convert]::ToBase64String($key)
}

Write-Host 'Please log into your Azure Stack user environment' -foregroundcolor Green

$tenantARM = "https://management.local.azurestack.external"
$aadTenantName = "PLEASE FILL THIS IN WITH YOUR AAD TENANT NAME. FOR EXAMPLE: myazurestack.onmicrosoft.com"

# Configure the Azure Stack operator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackUser" `
  -ArmEndpoint $tenantARM

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $aadTenantName `
  -EnvironmentName AzureStackUser

# Sign in to the user portal.
Add-AzureRmAccount `
  -EnvironmentName "AzureStackUser" `
  -TenantId $TenantID `

$now = [System.DateTime]::Now
$oneYearFromNow = $now.AddYears(1)

$applicationPassword = GenerateSymmetricKey

# Create a new Azure AD application.
$identifierUri = [string]::Format("http://localhost:8080/{0}",[Guid]::NewGuid().ToString("N"))
$homePage = "http://contoso.com"

Write-Host "Creating a new AAD Application"
$ADApp = New-AzureRmADApplication `
  -DisplayName $applicationName `
  -HomePage $homePage `
  -IdentifierUris $identifierUri `
  -StartDate $now `
  -EndDate $oneYearFromNow `
  -Password $applicationPassword

Write-Host "Creating a new AAD service principal"
$servicePrincipal = New-AzureRmADServicePrincipal `
  -ApplicationId $ADApp.ApplicationId

# Create a new resource group and a key vault in that resource group.
New-AzureRmResourceGroup `
  -Name $resourceGroupName `
  -Location $location

Write-Host "Creating vault $vaultName"
$vault = New-AzureRmKeyVault -VaultName $vaultName `
  -ResourceGroupName $resourceGroupName `
  -Sku standard `
  -Location $location

# Specify full privileges to the vault for the application.
Write-Host "Setting access policy"
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName `
  -ObjectId $servicePrincipal.Id `
  -PermissionsToKeys all `
  -PermissionsToSecrets all

Write-Host "Paste the following settings into the app.config file for the HelloKeyVault project:"
'<add key="VaultUrl" value="' + $vault.VaultUri + '"/>'
'<add key="AuthClientId" value="' + $servicePrincipal.ApplicationId + '"/>'
'<add key="AuthClientSecret" value="' + $applicationPassword + '"/>'
Write-Host

```

<span data-ttu-id="42de9-120">The next screen capture shows the output from the script used to create the key vault:</span><span class="sxs-lookup"><span data-stu-id="42de9-120">The next screen capture shows the output from the script used to create the key vault:</span></span>

![Key vault with access keys](media/azure-stack-kv-sample-app/settingsoutput.png)

<span data-ttu-id="42de9-122">Make a note of the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span><span class="sxs-lookup"><span data-stu-id="42de9-122">Make a note of the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="42de9-123">You use these values to run the HelloKeyVault application.</span><span class="sxs-lookup"><span data-stu-id="42de9-123">You use these values to run the HelloKeyVault application.</span></span>

## <a name="download-and-configure-the-sample-application"></a><span data-ttu-id="42de9-124">Download and configure the sample application</span><span class="sxs-lookup"><span data-stu-id="42de9-124">Download and configure the sample application</span></span>

<span data-ttu-id="42de9-125">Download the key vault sample from the Azure [Key Vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343) page.</span><span class="sxs-lookup"><span data-stu-id="42de9-125">Download the key vault sample from the Azure [Key Vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343) page.</span></span> <span data-ttu-id="42de9-126">Extract the contents of the .zip file on your development workstation.</span><span class="sxs-lookup"><span data-stu-id="42de9-126">Extract the contents of the .zip file on your development workstation.</span></span> <span data-ttu-id="42de9-127">There are two applications in the samples folder, this article uses HelloKeyVault.</span><span class="sxs-lookup"><span data-stu-id="42de9-127">There are two applications in the samples folder, this article uses HelloKeyVault.</span></span>

<span data-ttu-id="42de9-128">To load the HelloKeyVault sample:</span><span class="sxs-lookup"><span data-stu-id="42de9-128">To load the HelloKeyVault sample:</span></span>

* <span data-ttu-id="42de9-129">Browse to the **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault** folder.</span><span class="sxs-lookup"><span data-stu-id="42de9-129">Browse to the **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault** folder.</span></span>
* <span data-ttu-id="42de9-130">Open the HelloKeyVault application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42de9-130">Open the HelloKeyVault application in Visual Studio.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="42de9-131">Configure the sample application</span><span class="sxs-lookup"><span data-stu-id="42de9-131">Configure the sample application</span></span>

<span data-ttu-id="42de9-132">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="42de9-132">In Visual Studio:</span></span>

* <span data-ttu-id="42de9-133">Open the HelloKeyVault\App.config file and find browse to the &lt;**appSettings**&gt; element.</span><span class="sxs-lookup"><span data-stu-id="42de9-133">Open the HelloKeyVault\App.config file and find browse to the &lt;**appSettings**&gt; element.</span></span>
* <span data-ttu-id="42de9-134">Update the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** keys with the values returned by the used to create the key vault.</span><span class="sxs-lookup"><span data-stu-id="42de9-134">Update the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** keys with the values returned by the used to create the key vault.</span></span> <span data-ttu-id="42de9-135">(By default, the App.config file has a placeholder for *AuthCertThumbprint*.</span><span class="sxs-lookup"><span data-stu-id="42de9-135">(By default, the App.config file has a placeholder for *AuthCertThumbprint*.</span></span> <span data-ttu-id="42de9-136">Replace this placeholder with *AuthClientSecret*.)</span><span class="sxs-lookup"><span data-stu-id="42de9-136">Replace this placeholder with *AuthClientSecret*.)</span></span>

  ![App settings](media/azure-stack-kv-sample-app/appconfig.png)

* <span data-ttu-id="42de9-138">Rebuild the solution.</span><span class="sxs-lookup"><span data-stu-id="42de9-138">Rebuild the solution.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="42de9-139">Run the application</span><span class="sxs-lookup"><span data-stu-id="42de9-139">Run the application</span></span>

<span data-ttu-id="42de9-140">When you run HelloKeyVault, the application signs in to Azure AD, and then uses the AuthClientSecret token to authenticate to the key vault in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="42de9-140">When you run HelloKeyVault, the application signs in to Azure AD, and then uses the AuthClientSecret token to authenticate to the key vault in Azure Stack.</span></span>

<span data-ttu-id="42de9-141">You can use the HelloKeyVault sample to:</span><span class="sxs-lookup"><span data-stu-id="42de9-141">You can use the HelloKeyVault sample to:</span></span>

* <span data-ttu-id="42de9-142">Perform basic operations such as create, encrypt, wrap, and delete on the keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="42de9-142">Perform basic operations such as create, encrypt, wrap, and delete on the keys and secrets.</span></span>
* <span data-ttu-id="42de9-143">Pass parameters such as *encrypt* and *decrypt* to HelloKeyVault, and apply the specified changes to a key vault.</span><span class="sxs-lookup"><span data-stu-id="42de9-143">Pass parameters such as *encrypt* and *decrypt* to HelloKeyVault, and apply the specified changes to a key vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42de9-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="42de9-144">Next steps</span></span>

[<span data-ttu-id="42de9-145">Deploy a VM with a Key Vault password</span><span class="sxs-lookup"><span data-stu-id="42de9-145">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="42de9-146">Deploy a VM with a Key Vault certificate</span><span class="sxs-lookup"><span data-stu-id="42de9-146">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)
