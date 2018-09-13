---
title: Deploy a VM with a securely stored certificate on Azure Stack  | Microsoft Docs
description: Learn how deploy a VM and inject a certificate from Azure Stack Key Vault
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/15/2017
ms.author: sngun
ms.openlocfilehash: e4a79b78b0dc05795faa52c1b8e74802d932fe0b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552569"
---
# <a name="create-vms-and-include-certificates-retrieved-from-key-vault"></a><span data-ttu-id="0ac58-103">Create VMs and include certificates retrieved from Key Vault</span><span class="sxs-lookup"><span data-stu-id="0ac58-103">Create VMs and include certificates retrieved from Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="0ac58-104">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span><span class="sxs-lookup"><span data-stu-id="0ac58-104">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span></span> <span data-ttu-id="0ac58-105">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span><span class="sxs-lookup"><span data-stu-id="0ac58-105">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span></span>

<span data-ttu-id="0ac58-106">In Azure Stack, VMs are deployed through Azure Resource Manager, and you can now store certificates in Azure Stack Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0ac58-106">In Azure Stack, VMs are deployed through Azure Resource Manager, and you can now store certificates in Azure Stack Key Vault.</span></span> <span data-ttu-id="0ac58-107">Then Azure Stack (Microsoft.Compute resource provider to be specific) pushes them into your VMs when the VMs are deployed.</span><span class="sxs-lookup"><span data-stu-id="0ac58-107">Then Azure Stack (Microsoft.Compute resource provider to be specific) pushes them into your VMs when the VMs are deployed.</span></span> <span data-ttu-id="0ac58-108">Certificates can be used in many scenarios, including SSL, encryption, and certificate based authentication.</span><span class="sxs-lookup"><span data-stu-id="0ac58-108">Certificates can be used in many scenarios, including SSL, encryption, and certificate based authentication.</span></span>

<span data-ttu-id="0ac58-109">By using this method, you can keep the certificate safe.</span><span class="sxs-lookup"><span data-stu-id="0ac58-109">By using this method, you can keep the certificate safe.</span></span> <span data-ttu-id="0ac58-110">It's now not in the VM image, or in the application's configuration files or some other unsafe location.</span><span class="sxs-lookup"><span data-stu-id="0ac58-110">It's now not in the VM image, or in the application's configuration files or some other unsafe location.</span></span> <span data-ttu-id="0ac58-111">By setting appropriate access policy for the key vault, you can also control who gets access to your certificate.</span><span class="sxs-lookup"><span data-stu-id="0ac58-111">By setting appropriate access policy for the key vault, you can also control who gets access to your certificate.</span></span> <span data-ttu-id="0ac58-112">Another benefit is that you can manage all your certificates in one place in Azure Stack Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0ac58-112">Another benefit is that you can manage all your certificates in one place in Azure Stack Key Vault.</span></span>

<span data-ttu-id="0ac58-113">Here is a quick overview of the process:</span><span class="sxs-lookup"><span data-stu-id="0ac58-113">Here is a quick overview of the process:</span></span>

* <span data-ttu-id="0ac58-114">You need a certificate in the .pfx format.</span><span class="sxs-lookup"><span data-stu-id="0ac58-114">You need a certificate in the .pfx format.</span></span>
* <span data-ttu-id="0ac58-115">Create a key vault (using either a template or the following sample script).</span><span class="sxs-lookup"><span data-stu-id="0ac58-115">Create a key vault (using either a template or the following sample script).</span></span>
* <span data-ttu-id="0ac58-116">Make sure you have turned on the EnabledForDeployment switch.</span><span class="sxs-lookup"><span data-stu-id="0ac58-116">Make sure you have turned on the EnabledForDeployment switch.</span></span>
* <span data-ttu-id="0ac58-117">Upload the certificate as a secret.</span><span class="sxs-lookup"><span data-stu-id="0ac58-117">Upload the certificate as a secret.</span></span>

## <a name="deploying-vms"></a><span data-ttu-id="0ac58-118">Deploying VMs</span><span class="sxs-lookup"><span data-stu-id="0ac58-118">Deploying VMs</span></span>
<span data-ttu-id="0ac58-119">This sample script creates a key vault, and then stores a certificate stored in the .pfx file in a local directory, to the key vault as a secret.</span><span class="sxs-lookup"><span data-stu-id="0ac58-119">This sample script creates a key vault, and then stores a certificate stored in the .pfx file in a local directory, to the key vault as a secret.</span></span>

    $vaultName = "contosovault"
    $resourceGroup = "contosovaultrg"
    $location = "local"
    $secretName = "servicecert"
    $fileName = "keyvault.pfx"
    $certPassword = "abcd1234"

    # =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=

    $fileContentBytes = get-content $fileName -Encoding Byte

    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@
    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
    Switch-AzureMode -Name AzureResourceManager
    New-AzureRmResourceGroup -Name $resourceGroup -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroup -Location $location -sku standard -EnabledForDeployment
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $vaultName -Name $secretName -SecretValue $secret

<span data-ttu-id="0ac58-120">The first part of the script reads the .pfx file, and then stores it as a JSON object with the file content base64 encoded.</span><span class="sxs-lookup"><span data-stu-id="0ac58-120">The first part of the script reads the .pfx file, and then stores it as a JSON object with the file content base64 encoded.</span></span> <span data-ttu-id="0ac58-121">Then the JSON object is also base64 encoded.</span><span class="sxs-lookup"><span data-stu-id="0ac58-121">Then the JSON object is also base64 encoded.</span></span>

<span data-ttu-id="0ac58-122">Next, it creates a new resource group and then creates a key vault.</span><span class="sxs-lookup"><span data-stu-id="0ac58-122">Next, it creates a new resource group and then creates a key vault.</span></span> <span data-ttu-id="0ac58-123">Note the last parameter to the New-AzureKeyVault command, '-EnabledForDeployment', which grants access to Azure (specifically to the Microsoft.Compute resource provider) to read secrets from the key vault for deployments.</span><span class="sxs-lookup"><span data-stu-id="0ac58-123">Note the last parameter to the New-AzureKeyVault command, '-EnabledForDeployment', which grants access to Azure (specifically to the Microsoft.Compute resource provider) to read secrets from the key vault for deployments.</span></span>

<span data-ttu-id="0ac58-124">The last command simply stores the base64 encoded JSON object in the key vault as a secret.</span><span class="sxs-lookup"><span data-stu-id="0ac58-124">The last command simply stores the base64 encoded JSON object in the key vault as a secret.</span></span>

<span data-ttu-id="0ac58-125">Here's sample output from the preceding script:</span><span class="sxs-lookup"><span data-stu-id="0ac58-125">Here's sample output from the preceding script:</span></span>

    VERBOSE:  – Created resource group 'contosovaultrg' in
    location
    'eastus'
    ResourceGroupName : contosovaultrg
    Location          : eastus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions NotActions
                        ======= ==========
                        \*
    ResourceId        :
    /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-dd149b4aeb56/re
    sourceGroups/contosovaultrg
    VaultUri             : https://contosovault.vault.azure.net
    TenantId             : xxxxxxxx-xxxx-xxxx-xxxx-2d7cd011db47
    TenantName           : xxxxxxxx
    Sku                  : standard
    EnabledForDeployment : True
    AccessPolicies       : {xxxxxxxx-xxxx-xxxx-xxxx-2d7cd011db47}
    AccessPoliciesText   :
                           Tenant ID              :
                           xxxxxxxx-xxxx-xxxx-xxxx-2d7cd011db47
                           Object ID              :
                           xxxxxxxx-xxxx-xxxx-xxxx-b092cebf0c80
                           Application ID         :
                           Display Name           : Derick Developer  (derick@contoso.com)
                           Permissions to Keys    : get, create, delete,
                           list, update, import, backup, restore
                           Permissions to Secrets : all
    OriginalVault        : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId           :
    /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-dd149b4aeb56                 
    /resourceGroups/contosovaultrg/providers/Microsoft.KeyV
                           ault/vaults/contosovault
    VaultName            : contosovault
    ResourceGroupName    : contosovaultrg
    Location             : eastus
    Tags                 : {}
    TagsTable            :
    SecretValue     : System.Security.SecureString
    SecretValueText :
    ew0KImRhdGEiOiAiTUlJSkN3SUJBekNDQ01jR0NTcUdTSWIzRFFFSEFh
    Q0NDTGdFZ2dpME1JSUlzRENDQmdnR0NTcUdTSWIzRFFFSEFhQ0NCZmtF           
    Z2dYMU1JSUY4VENDQmUwR0N5cUdTSWIzRFFFTUNnRUNvSUlFL2pDQ0JQ
    &lt;&lt;&lt; Output truncated… &gt;&gt;&gt;
    Attributes      :
    Microsoft.Azure.Commands.KeyVault.Models.SecretAttributes
    VaultName       : contosovault
    Name            : servicecert
    Version         : e3391a126b65414f93f6f9806743a1f7
    Id              :
    https://contosovault.vault.azure.net:443/secrets/servicecert
                      /e3391a126b65414f93f6f9806743a1f7

<span data-ttu-id="0ac58-126">Now we are ready to deploy a VM template.</span><span class="sxs-lookup"><span data-stu-id="0ac58-126">Now we are ready to deploy a VM template.</span></span> <span data-ttu-id="0ac58-127">Note the URI of the secret from the output.</span><span class="sxs-lookup"><span data-stu-id="0ac58-127">Note the URI of the secret from the output.</span></span>

<span data-ttu-id="0ac58-128">You'll need a template located [here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span><span class="sxs-lookup"><span data-stu-id="0ac58-128">You'll need a template located [here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="0ac58-129">The parameters of special interest (besides the usual VM parameters) are the vault name, the vault resource group, and the secret URI.</span><span class="sxs-lookup"><span data-stu-id="0ac58-129">The parameters of special interest (besides the usual VM parameters) are the vault name, the vault resource group, and the secret URI.</span></span> <span data-ttu-id="0ac58-130">Of course, you can also download it from GitHub and modify as needed.</span><span class="sxs-lookup"><span data-stu-id="0ac58-130">Of course, you can also download it from GitHub and modify as needed.</span></span>

<span data-ttu-id="0ac58-131">When this VM is deployed, Azure injects the certificate into the VM.</span><span class="sxs-lookup"><span data-stu-id="0ac58-131">When this VM is deployed, Azure injects the certificate into the VM.</span></span>
<span data-ttu-id="0ac58-132">On Windows, certificates in the .pfx file are added with the private key not exportable.</span><span class="sxs-lookup"><span data-stu-id="0ac58-132">On Windows, certificates in the .pfx file are added with the private key not exportable.</span></span> <span data-ttu-id="0ac58-133">The certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span><span class="sxs-lookup"><span data-stu-id="0ac58-133">The certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span></span> <span data-ttu-id="0ac58-134">On Linux, the certificate file is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file, and &lt;UppercaseThumbprint&gt;.prv for the private key.</span><span class="sxs-lookup"><span data-stu-id="0ac58-134">On Linux, the certificate file is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file, and &lt;UppercaseThumbprint&gt;.prv for the private key.</span></span>
<span data-ttu-id="0ac58-135">Both of these files are .pem formatted.</span><span class="sxs-lookup"><span data-stu-id="0ac58-135">Both of these files are .pem formatted.</span></span>

<span data-ttu-id="0ac58-136">The application usually finds the certificate by using the thumbprint and doesn't need modification.</span><span class="sxs-lookup"><span data-stu-id="0ac58-136">The application usually finds the certificate by using the thumbprint and doesn't need modification.</span></span>

## <a name="retiring-certificates"></a><span data-ttu-id="0ac58-137">Retiring certificates</span><span class="sxs-lookup"><span data-stu-id="0ac58-137">Retiring certificates</span></span>
<span data-ttu-id="0ac58-138">In the preceding section, we showed you how to push a new certificate to your existing VMs.</span><span class="sxs-lookup"><span data-stu-id="0ac58-138">In the preceding section, we showed you how to push a new certificate to your existing VMs.</span></span> <span data-ttu-id="0ac58-139">But your old certificate is still in the VM and cannot be removed.</span><span class="sxs-lookup"><span data-stu-id="0ac58-139">But your old certificate is still in the VM and cannot be removed.</span></span> <span data-ttu-id="0ac58-140">For added security, you can change the attribute for old secret to 'Disabled', so that even if an old template tries to create a VM with this old version of certificate, it will.</span><span class="sxs-lookup"><span data-stu-id="0ac58-140">For added security, you can change the attribute for old secret to 'Disabled', so that even if an old template tries to create a VM with this old version of certificate, it will.</span></span> <span data-ttu-id="0ac58-141">Here's how you set a specific secret version to be disabled:</span><span class="sxs-lookup"><span data-stu-id="0ac58-141">Here's how you set a specific secret version to be disabled:</span></span>

    Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0

## <a name="conclusion"></a><span data-ttu-id="0ac58-142">Conclusion</span><span class="sxs-lookup"><span data-stu-id="0ac58-142">Conclusion</span></span>
<span data-ttu-id="0ac58-143">With this new method, the certificate can be kept separate from the VM image or the application payload.</span><span class="sxs-lookup"><span data-stu-id="0ac58-143">With this new method, the certificate can be kept separate from the VM image or the application payload.</span></span> <span data-ttu-id="0ac58-144">So we have removed one point of exposure.</span><span class="sxs-lookup"><span data-stu-id="0ac58-144">So we have removed one point of exposure.</span></span>

<span data-ttu-id="0ac58-145">The certificate can also be renewed and uploaded to Key Vault without having to re-build the VM image or the application deployment package.</span><span class="sxs-lookup"><span data-stu-id="0ac58-145">The certificate can also be renewed and uploaded to Key Vault without having to re-build the VM image or the application deployment package.</span></span> <span data-ttu-id="0ac58-146">The application still needs to be supplied with the new URI for this new certificate version though.</span><span class="sxs-lookup"><span data-stu-id="0ac58-146">The application still needs to be supplied with the new URI for this new certificate version though.</span></span>

<span data-ttu-id="0ac58-147">By separating the certificate from the VM or the application payload, we have now reduced the number of personnel that will have direct access to the certificate.</span><span class="sxs-lookup"><span data-stu-id="0ac58-147">By separating the certificate from the VM or the application payload, we have now reduced the number of personnel that will have direct access to the certificate.</span></span>

<span data-ttu-id="0ac58-148">As an added benefit, you now have one convenient place in Key Vault to manage all your certificates, including the all the versions that were deployed over time.</span><span class="sxs-lookup"><span data-stu-id="0ac58-148">As an added benefit, you now have one convenient place in Key Vault to manage all your certificates, including the all the versions that were deployed over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ac58-149">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0ac58-149">Next Steps</span></span>
[<span data-ttu-id="0ac58-150">Deploy a VM with a Key Vault password</span><span class="sxs-lookup"><span data-stu-id="0ac58-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="0ac58-151">Allow an application to access Key Vault</span><span class="sxs-lookup"><span data-stu-id="0ac58-151">Allow an application to access Key Vault</span></span>](azure-stack-kv-sample-app.md)

