---
title: Create an Azure Service Fabric cluster from a template | Microsoft Docs
description: This article describes how to set up a secure Service Fabric cluster in Azure by using Azure Resource Manager, Azure Key Vault, and Azure Active Directory (Azure AD) for client authentication.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/22/2017
ms.author: chackdan
ms.openlocfilehash: 456b99800a04780a8956684fa44e3778020c6f8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552143"
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="36a11-103">Create a Service Fabric cluster by using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36a11-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure portal](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="36a11-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36a11-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="36a11-107">We acknowledge that the article is long.</span><span class="sxs-lookup"><span data-stu-id="36a11-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="36a11-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span><span class="sxs-lookup"><span data-stu-id="36a11-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="36a11-109">The guide covers the following procedures:</span><span class="sxs-lookup"><span data-stu-id="36a11-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="36a11-110">Setting up an Azure key vault to upload certificates for cluster and application security</span><span class="sxs-lookup"><span data-stu-id="36a11-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="36a11-111">Creating a secured cluster in Azure by using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36a11-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="36a11-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span><span class="sxs-lookup"><span data-stu-id="36a11-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="36a11-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span><span class="sxs-lookup"><span data-stu-id="36a11-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="36a11-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span><span class="sxs-lookup"><span data-stu-id="36a11-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="36a11-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span><span class="sxs-lookup"><span data-stu-id="36a11-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="36a11-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span><span class="sxs-lookup"><span data-stu-id="36a11-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="36a11-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span><span class="sxs-lookup"><span data-stu-id="36a11-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="36a11-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span><span class="sxs-lookup"><span data-stu-id="36a11-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="36a11-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="36a11-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="36a11-120">Sign in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="36a11-120">Sign in to your Azure account</span></span>
<span data-ttu-id="36a11-121">This guide uses [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="36a11-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="36a11-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span><span class="sxs-lookup"><span data-stu-id="36a11-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="36a11-123">Sign in to your Azure account:</span><span class="sxs-lookup"><span data-stu-id="36a11-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="36a11-124">Select your subscription:</span><span class="sxs-lookup"><span data-stu-id="36a11-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="36a11-125">Set up a key vault</span><span class="sxs-lookup"><span data-stu-id="36a11-125">Set up a key vault</span></span>
<span data-ttu-id="36a11-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span><span class="sxs-lookup"><span data-stu-id="36a11-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="36a11-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="36a11-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="36a11-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span><span class="sxs-lookup"><span data-stu-id="36a11-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="36a11-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="36a11-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="36a11-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span><span class="sxs-lookup"><span data-stu-id="36a11-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="36a11-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span><span class="sxs-lookup"><span data-stu-id="36a11-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagram of certificate installation][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="36a11-133">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="36a11-133">Create a resource group</span></span>
<span data-ttu-id="36a11-134">The first step is to create a resource group specifically for your key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="36a11-135">We recommend that you put the key vault into its own resource group.</span><span class="sxs-lookup"><span data-stu-id="36a11-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="36a11-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="36a11-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="36a11-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span><span class="sxs-lookup"><span data-stu-id="36a11-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="36a11-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span><span class="sxs-lookup"><span data-stu-id="36a11-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="36a11-139">The output should look like this:</span><span class="sxs-lookup"><span data-stu-id="36a11-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="36a11-140">Create a key vault in the new resource group</span><span class="sxs-lookup"><span data-stu-id="36a11-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="36a11-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span><span class="sxs-lookup"><span data-stu-id="36a11-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="36a11-142">The output should look like this:</span><span class="sxs-lookup"><span data-stu-id="36a11-142">The output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="36a11-143">Use an existing key vault</span><span class="sxs-lookup"><span data-stu-id="36a11-143">Use an existing key vault</span></span>

<span data-ttu-id="36a11-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span><span class="sxs-lookup"><span data-stu-id="36a11-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="36a11-145">Add certificates to your key vault</span><span class="sxs-lookup"><span data-stu-id="36a11-145">Add certificates to your key vault</span></span>

<span data-ttu-id="36a11-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span><span class="sxs-lookup"><span data-stu-id="36a11-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="36a11-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="36a11-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="36a11-148">Cluster and server certificate (required)</span><span class="sxs-lookup"><span data-stu-id="36a11-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="36a11-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span><span class="sxs-lookup"><span data-stu-id="36a11-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="36a11-150">It provides cluster security in two ways:</span><span class="sxs-lookup"><span data-stu-id="36a11-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="36a11-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span><span class="sxs-lookup"><span data-stu-id="36a11-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="36a11-152">Only nodes that can prove their identity with this certificate can join the cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="36a11-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="36a11-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="36a11-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="36a11-155">To serve these purposes, the certificate must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="36a11-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="36a11-156">The certificate must contain a private key.</span><span class="sxs-lookup"><span data-stu-id="36a11-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="36a11-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span><span class="sxs-lookup"><span data-stu-id="36a11-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="36a11-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="36a11-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="36a11-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="36a11-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span><span class="sxs-lookup"><span data-stu-id="36a11-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="36a11-161">You must obtain a custom domain name for your cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="36a11-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="36a11-163">Application certificates (optional)</span><span class="sxs-lookup"><span data-stu-id="36a11-163">Application certificates (optional)</span></span>
<span data-ttu-id="36a11-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span><span class="sxs-lookup"><span data-stu-id="36a11-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="36a11-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span><span class="sxs-lookup"><span data-stu-id="36a11-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="36a11-166">Encryption and decryption of application configuration values.</span><span class="sxs-lookup"><span data-stu-id="36a11-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="36a11-167">Encryption of data across nodes during replication.</span><span class="sxs-lookup"><span data-stu-id="36a11-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="36a11-168">Formatting certificates for Azure resource provider use</span><span class="sxs-lookup"><span data-stu-id="36a11-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="36a11-169">You can add and use private key files (.pfx) directly through your key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="36a11-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span><span class="sxs-lookup"><span data-stu-id="36a11-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="36a11-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span><span class="sxs-lookup"><span data-stu-id="36a11-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="36a11-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="36a11-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="36a11-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="36a11-174">To use the module, do the following:</span><span class="sxs-lookup"><span data-stu-id="36a11-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="36a11-175">Download the entire contents of the repo into a local directory.</span><span class="sxs-lookup"><span data-stu-id="36a11-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="36a11-176">Go to the local directory.</span><span class="sxs-lookup"><span data-stu-id="36a11-176">Go to the local directory.</span></span>
2. <span data-ttu-id="36a11-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="36a11-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="36a11-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="36a11-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="36a11-180">Repeat this step for any additional certificates you want to install in your cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="36a11-181">Uploading an existing certificate</span><span class="sxs-lookup"><span data-stu-id="36a11-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="36a11-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span><span class="sxs-lookup"><span data-stu-id="36a11-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="36a11-183">To resolve the conflict, change the key vault name.</span><span class="sxs-lookup"><span data-stu-id="36a11-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="36a11-184">After the conflict is resolved, the output should look like this:</span><span class="sxs-lookup"><span data-stu-id="36a11-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security. If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="36a11-187">Creating a self-signed certificate and uploading it to the key vault</span><span class="sxs-lookup"><span data-stu-id="36a11-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="36a11-188">If you have already uploaded your certificates to the key vault, skip this step.</span><span class="sxs-lookup"><span data-stu-id="36a11-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="36a11-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="36a11-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span><span class="sxs-lookup"><span data-stu-id="36a11-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResouceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="36a11-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span><span class="sxs-lookup"><span data-stu-id="36a11-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="36a11-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span><span class="sxs-lookup"><span data-stu-id="36a11-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="36a11-193">After the conflict is resolved, the output should look like this:</span><span class="sxs-lookup"><span data-stu-id="36a11-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security. If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.

 <span data-ttu-id="36a11-196">At this point, you should have the following elements in place:</span><span class="sxs-lookup"><span data-stu-id="36a11-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="36a11-197">The key vault resource group.</span><span class="sxs-lookup"><span data-stu-id="36a11-197">The key vault resource group.</span></span>
* <span data-ttu-id="36a11-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span><span class="sxs-lookup"><span data-stu-id="36a11-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="36a11-199">The cluster server authentication certificate and its URL in the key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="36a11-200">The application certificates and their URLs in the key vault.</span><span class="sxs-lookup"><span data-stu-id="36a11-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="36a11-201">Set up Azure Active Directory for client authentication</span><span class="sxs-lookup"><span data-stu-id="36a11-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="36a11-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span><span class="sxs-lookup"><span data-stu-id="36a11-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="36a11-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span><span class="sxs-lookup"><span data-stu-id="36a11-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="36a11-204">In this article, we assume that you have already created a tenant.</span><span class="sxs-lookup"><span data-stu-id="36a11-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="36a11-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="36a11-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="36a11-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="36a11-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="36a11-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span><span class="sxs-lookup"><span data-stu-id="36a11-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="36a11-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="36a11-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> You must complete the following steps before you create the cluster. Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.

1. <span data-ttu-id="36a11-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span><span class="sxs-lookup"><span data-stu-id="36a11-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="36a11-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="36a11-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="36a11-213">Extract the zip file.</span><span class="sxs-lookup"><span data-stu-id="36a11-213">Extract the zip file.</span></span>
4. <span data-ttu-id="36a11-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span><span class="sxs-lookup"><span data-stu-id="36a11-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="36a11-215">For example:</span><span class="sxs-lookup"><span data-stu-id="36a11-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="36a11-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="36a11-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="36a11-217">Executing this command displays the TenantId for every subscription.</span><span class="sxs-lookup"><span data-stu-id="36a11-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="36a11-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span><span class="sxs-lookup"><span data-stu-id="36a11-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="36a11-219">It does not need to match the actual cluster name exactly.</span><span class="sxs-lookup"><span data-stu-id="36a11-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="36a11-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span><span class="sxs-lookup"><span data-stu-id="36a11-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="36a11-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span><span class="sxs-lookup"><span data-stu-id="36a11-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="36a11-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span><span class="sxs-lookup"><span data-stu-id="36a11-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="36a11-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="36a11-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="36a11-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="36a11-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="36a11-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="36a11-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span><span class="sxs-lookup"><span data-stu-id="36a11-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="36a11-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="36a11-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="36a11-228">*ClusterName*\_Client</span><span class="sxs-lookup"><span data-stu-id="36a11-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="36a11-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span><span class="sxs-lookup"><span data-stu-id="36a11-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="36a11-230">Create a Service Fabric cluster Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="36a11-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="36a11-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="36a11-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="36a11-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="36a11-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="36a11-233">These templates can be used as a starting point for your cluster template.</span><span class="sxs-lookup"><span data-stu-id="36a11-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="36a11-234">Create the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="36a11-234">Create the Resource Manager template</span></span>
<span data-ttu-id="36a11-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span><span class="sxs-lookup"><span data-stu-id="36a11-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="36a11-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="36a11-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="36a11-237">Add certificates</span><span class="sxs-lookup"><span data-stu-id="36a11-237">Add certificates</span></span>
<span data-ttu-id="36a11-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span><span class="sxs-lookup"><span data-stu-id="36a11-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="36a11-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span><span class="sxs-lookup"><span data-stu-id="36a11-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="36a11-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span><span class="sxs-lookup"><span data-stu-id="36a11-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="36a11-241">Add all certificates to the virtual machine scale set osProfile</span><span class="sxs-lookup"><span data-stu-id="36a11-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="36a11-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="36a11-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="36a11-243">This action instructs the resource provider to install the certificate on the VMs.</span><span class="sxs-lookup"><span data-stu-id="36a11-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="36a11-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span><span class="sxs-lookup"><span data-stu-id="36a11-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="36a11-245">Configure the Service Fabric cluster certificate</span><span class="sxs-lookup"><span data-stu-id="36a11-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="36a11-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span><span class="sxs-lookup"><span data-stu-id="36a11-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="36a11-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span><span class="sxs-lookup"><span data-stu-id="36a11-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="36a11-248">Virtual machine scale set resource:</span><span class="sxs-lookup"><span data-stu-id="36a11-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="36a11-249">Service Fabric resource:</span><span class="sxs-lookup"><span data-stu-id="36a11-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="36a11-250">Insert Azure AD configuration</span><span class="sxs-lookup"><span data-stu-id="36a11-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="36a11-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="36a11-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="36a11-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span><span class="sxs-lookup"><span data-stu-id="36a11-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <a "configure-arm" ></a><span data-ttu-id="36a11-253">Configure Resource Manager template parameters</span><span class="sxs-lookup"><span data-stu-id="36a11-253">Configure Resource Manager template parameters</span></span>
<span data-ttu-id="36a11-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span><span class="sxs-lookup"><span data-stu-id="36a11-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="36a11-255">At this point, you should have the following elements in place:</span><span class="sxs-lookup"><span data-stu-id="36a11-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="36a11-256">Key vault resource group</span><span class="sxs-lookup"><span data-stu-id="36a11-256">Key vault resource group</span></span>
  * <span data-ttu-id="36a11-257">Key vault</span><span class="sxs-lookup"><span data-stu-id="36a11-257">Key vault</span></span>
  * <span data-ttu-id="36a11-258">Cluster server authentication certificate</span><span class="sxs-lookup"><span data-stu-id="36a11-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="36a11-259">Data encipherment certificate</span><span class="sxs-lookup"><span data-stu-id="36a11-259">Data encipherment certificate</span></span>
* <span data-ttu-id="36a11-260">Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="36a11-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="36a11-261">Azure AD application for web-based management and Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="36a11-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="36a11-262">Azure AD application for native client management</span><span class="sxs-lookup"><span data-stu-id="36a11-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="36a11-263">Users and their assigned roles</span><span class="sxs-lookup"><span data-stu-id="36a11-263">Users and their assigned roles</span></span>
* <span data-ttu-id="36a11-264">Service Fabric cluster Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="36a11-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="36a11-265">Certificates configured through key vault</span><span class="sxs-lookup"><span data-stu-id="36a11-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="36a11-266">Azure Active Directory configured</span><span class="sxs-lookup"><span data-stu-id="36a11-266">Azure Active Directory configured</span></span>

<span data-ttu-id="36a11-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="36a11-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Resource Manager dependency map][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="36a11-269">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="36a11-269">Create the cluster</span></span>
<span data-ttu-id="36a11-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="36a11-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="36a11-271">Test it</span><span class="sxs-lookup"><span data-stu-id="36a11-271">Test it</span></span>
<span data-ttu-id="36a11-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span><span class="sxs-lookup"><span data-stu-id="36a11-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="36a11-273">Deploy it</span><span class="sxs-lookup"><span data-stu-id="36a11-273">Deploy it</span></span>
<span data-ttu-id="36a11-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span><span class="sxs-lookup"><span data-stu-id="36a11-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="36a11-275">Assign users to roles</span><span class="sxs-lookup"><span data-stu-id="36a11-275">Assign users to roles</span></span>
<span data-ttu-id="36a11-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="36a11-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="36a11-277">In the Azure portal, go to your tenant, and then select **Applications**.</span><span class="sxs-lookup"><span data-stu-id="36a11-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="36a11-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="36a11-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="36a11-279">Click the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="36a11-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="36a11-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="36a11-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![Assign users to roles button][assign-users-to-roles-button]
5. <span data-ttu-id="36a11-282">Select the role to assign to the user.</span><span class="sxs-lookup"><span data-stu-id="36a11-282">Select the role to assign to the user.</span></span>

    !["Assign Users" dialog box][assign-users-to-roles-dialog]

> [!NOTE]
> For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-cluster"></a>

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="36a11-285">Create secure clusters on Linux</span><span class="sxs-lookup"><span data-stu-id="36a11-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="36a11-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="36a11-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="36a11-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span><span class="sxs-lookup"><span data-stu-id="36a11-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="36a11-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span><span class="sxs-lookup"><span data-stu-id="36a11-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="36a11-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span><span class="sxs-lookup"><span data-stu-id="36a11-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="36a11-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span><span class="sxs-lookup"><span data-stu-id="36a11-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="36a11-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span><span class="sxs-lookup"><span data-stu-id="36a11-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="36a11-292">The parameter -h prints out the help text.</span><span class="sxs-lookup"><span data-stu-id="36a11-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="36a11-293">This command returns the following three strings as the output:</span><span class="sxs-lookup"><span data-stu-id="36a11-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="36a11-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span><span class="sxs-lookup"><span data-stu-id="36a11-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="36a11-295">CertificateUrl for accessing the certificate</span><span class="sxs-lookup"><span data-stu-id="36a11-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="36a11-296">CertificateThumbprint, which is used for authentication</span><span class="sxs-lookup"><span data-stu-id="36a11-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="36a11-297">The following example shows how to use the command:</span><span class="sxs-lookup"><span data-stu-id="36a11-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="36a11-298">Executing the preceding command gives you the three strings as follows:</span><span class="sxs-lookup"><span data-stu-id="36a11-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="36a11-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="36a11-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="36a11-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="36a11-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span><span class="sxs-lookup"><span data-stu-id="36a11-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="36a11-302">You must obtain a custom domain name for your cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="36a11-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="36a11-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="36a11-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="36a11-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="36a11-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="36a11-306">Linux preview clusters do not support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="36a11-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="36a11-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span><span class="sxs-lookup"><span data-stu-id="36a11-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="36a11-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span><span class="sxs-lookup"><span data-stu-id="36a11-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="36a11-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span><span class="sxs-lookup"><span data-stu-id="36a11-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="36a11-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span><span class="sxs-lookup"><span data-stu-id="36a11-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="36a11-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span><span class="sxs-lookup"><span data-stu-id="36a11-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="36a11-312">For example, see the following command for creating and uploading a self-signed certificate:</span><span class="sxs-lookup"><span data-stu-id="36a11-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="36a11-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="36a11-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="36a11-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span><span class="sxs-lookup"><span data-stu-id="36a11-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="36a11-315">You need the self-signed certificate to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="36a11-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="36a11-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="36a11-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="36a11-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="36a11-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="36a11-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span><span class="sxs-lookup"><span data-stu-id="36a11-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="36a11-320">You must obtain a custom domain name for your cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="36a11-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="36a11-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="36a11-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36a11-323">Next steps</span><span class="sxs-lookup"><span data-stu-id="36a11-323">Next steps</span></span>
<span data-ttu-id="36a11-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span><span class="sxs-lookup"><span data-stu-id="36a11-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="36a11-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="36a11-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="36a11-326">Troubleshoot setting up Azure Active Directory for client authentication</span><span class="sxs-lookup"><span data-stu-id="36a11-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="36a11-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span><span class="sxs-lookup"><span data-stu-id="36a11-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="36a11-328">Service Fabric Explorer prompts you to select a certificate</span><span class="sxs-lookup"><span data-stu-id="36a11-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="36a11-329">Problem</span><span class="sxs-lookup"><span data-stu-id="36a11-329">Problem</span></span>
<span data-ttu-id="36a11-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span><span class="sxs-lookup"><span data-stu-id="36a11-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![SFX select certificate dialog][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="36a11-332">Reason</span><span class="sxs-lookup"><span data-stu-id="36a11-332">Reason</span></span>
<span data-ttu-id="36a11-333">The user isn’t assigned a role in the Azure AD cluster application.</span><span class="sxs-lookup"><span data-stu-id="36a11-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="36a11-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="36a11-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="36a11-335">Service Fabric Explorer falls back to certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="36a11-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="36a11-336">Solution</span><span class="sxs-lookup"><span data-stu-id="36a11-336">Solution</span></span>
<span data-ttu-id="36a11-337">Follow the instructions for setting up Azure AD, and assign user roles.</span><span class="sxs-lookup"><span data-stu-id="36a11-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="36a11-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span><span class="sxs-lookup"><span data-stu-id="36a11-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="36a11-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span><span class="sxs-lookup"><span data-stu-id="36a11-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="36a11-340">Problem</span><span class="sxs-lookup"><span data-stu-id="36a11-340">Problem</span></span>
<span data-ttu-id="36a11-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span><span class="sxs-lookup"><span data-stu-id="36a11-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="36a11-342">Solution</span><span class="sxs-lookup"><span data-stu-id="36a11-342">Solution</span></span>
<span data-ttu-id="36a11-343">This solution is the same as the preceding one.</span><span class="sxs-lookup"><span data-stu-id="36a11-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="36a11-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="36a11-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="36a11-345">Problem</span><span class="sxs-lookup"><span data-stu-id="36a11-345">Problem</span></span>
<span data-ttu-id="36a11-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="36a11-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![SFX reply address does not match][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="36a11-348">Reason</span><span class="sxs-lookup"><span data-stu-id="36a11-348">Reason</span></span>
<span data-ttu-id="36a11-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span><span class="sxs-lookup"><span data-stu-id="36a11-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="36a11-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span><span class="sxs-lookup"><span data-stu-id="36a11-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="36a11-351">Solution</span><span class="sxs-lookup"><span data-stu-id="36a11-351">Solution</span></span>
<span data-ttu-id="36a11-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span><span class="sxs-lookup"><span data-stu-id="36a11-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="36a11-353">When you have finished, save your change.</span><span class="sxs-lookup"><span data-stu-id="36a11-353">When you have finished, save your change.</span></span>

![Web application reply url][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="36a11-355">Connect the cluster by using Azure AD authentication via PowerShell</span><span class="sxs-lookup"><span data-stu-id="36a11-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="36a11-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span><span class="sxs-lookup"><span data-stu-id="36a11-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="36a11-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="36a11-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="36a11-358">Can I reuse the same Azure AD tenant in multiple clusters?</span><span class="sxs-lookup"><span data-stu-id="36a11-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="36a11-359">Yes.</span><span class="sxs-lookup"><span data-stu-id="36a11-359">Yes.</span></span> <span data-ttu-id="36a11-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span><span class="sxs-lookup"><span data-stu-id="36a11-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="36a11-361">Otherwise, Service Fabric Explorer doesn’t work.</span><span class="sxs-lookup"><span data-stu-id="36a11-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="36a11-362">Why do I still need a server certificate while Azure AD is enabled?</span><span class="sxs-lookup"><span data-stu-id="36a11-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="36a11-363">FabricClient and FabricGateway perform a mutual authentication.</span><span class="sxs-lookup"><span data-stu-id="36a11-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="36a11-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span><span class="sxs-lookup"><span data-stu-id="36a11-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="36a11-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="36a11-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png







