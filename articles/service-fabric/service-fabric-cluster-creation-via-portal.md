---
title: Create Service Fabric cluster in the Azure portal | Microsoft Docs
description: This article describes how to set up a secure Service Fabric cluster in Azure using the Azure portal and Azure Key Vault.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: chackdan
ms.openlocfilehash: e9272df2ad458a36de1d7af1228396219ef6f08b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662626"
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="3fd36-103">Create a Service Fabric cluster in Azure using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3fd36-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure portal](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="3fd36-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3fd36-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="3fd36-107">This guide walks you through the following steps:</span><span class="sxs-lookup"><span data-stu-id="3fd36-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="3fd36-108">Set up Key Vault to manage keys for cluster security.</span><span class="sxs-lookup"><span data-stu-id="3fd36-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="3fd36-109">Create a secured cluster in Azure through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3fd36-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="3fd36-110">Authenticate administrators using certificates.</span><span class="sxs-lookup"><span data-stu-id="3fd36-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].
> 
> 

<span data-ttu-id="3fd36-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span><span class="sxs-lookup"><span data-stu-id="3fd36-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="3fd36-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span><span class="sxs-lookup"><span data-stu-id="3fd36-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="3fd36-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="3fd36-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span><span class="sxs-lookup"><span data-stu-id="3fd36-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="3fd36-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span><span class="sxs-lookup"><span data-stu-id="3fd36-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="3fd36-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-cluster).</span><span class="sxs-lookup"><span data-stu-id="3fd36-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-cluster).</span></span> <span data-ttu-id="3fd36-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="3fd36-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="3fd36-119">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="3fd36-119">Log in to Azure</span></span>
<span data-ttu-id="3fd36-120">This guide uses [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="3fd36-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="3fd36-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span><span class="sxs-lookup"><span data-stu-id="3fd36-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="3fd36-122">Log in to your azure account:</span><span class="sxs-lookup"><span data-stu-id="3fd36-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3fd36-123">Select your subscription:</span><span class="sxs-lookup"><span data-stu-id="3fd36-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="3fd36-124">Set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="3fd36-124">Set up Key Vault</span></span>
<span data-ttu-id="3fd36-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span><span class="sxs-lookup"><span data-stu-id="3fd36-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="3fd36-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="3fd36-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="3fd36-127">Service Fabric uses X.509 certificates to secure a cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="3fd36-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fd36-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="3fd36-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span><span class="sxs-lookup"><span data-stu-id="3fd36-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="3fd36-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span><span class="sxs-lookup"><span data-stu-id="3fd36-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Certificate installation][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="3fd36-132">Create a Resource Group</span><span class="sxs-lookup"><span data-stu-id="3fd36-132">Create a Resource Group</span></span>
<span data-ttu-id="3fd36-133">The first step is to create a new resource group specifically for Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3fd36-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="3fd36-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="3fd36-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="3fd36-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span><span class="sxs-lookup"><span data-stu-id="3fd36-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="3fd36-136">Create Key Vault</span><span class="sxs-lookup"><span data-stu-id="3fd36-136">Create Key Vault</span></span>
<span data-ttu-id="3fd36-137">Create a Key Vault in the new resource group.</span><span class="sxs-lookup"><span data-stu-id="3fd36-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="3fd36-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span><span class="sxs-lookup"><span data-stu-id="3fd36-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

<span data-ttu-id="3fd36-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="3fd36-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="3fd36-140">Add certificates to Key Vault</span><span class="sxs-lookup"><span data-stu-id="3fd36-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="3fd36-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span><span class="sxs-lookup"><span data-stu-id="3fd36-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="3fd36-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="3fd36-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="3fd36-143">Cluster and server certificate (required)</span><span class="sxs-lookup"><span data-stu-id="3fd36-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="3fd36-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span><span class="sxs-lookup"><span data-stu-id="3fd36-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="3fd36-145">It provides cluster security in a couple ways:</span><span class="sxs-lookup"><span data-stu-id="3fd36-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="3fd36-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span><span class="sxs-lookup"><span data-stu-id="3fd36-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="3fd36-147">Only nodes that can prove their identity with this certificate can join the cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="3fd36-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="3fd36-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3fd36-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="3fd36-150">To serve these purposes, the certificate must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="3fd36-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="3fd36-151">The certificate must contain a private key.</span><span class="sxs-lookup"><span data-stu-id="3fd36-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="3fd36-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span><span class="sxs-lookup"><span data-stu-id="3fd36-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="3fd36-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="3fd36-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="3fd36-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="3fd36-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span><span class="sxs-lookup"><span data-stu-id="3fd36-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="3fd36-156">Acquire a custom domain name for your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="3fd36-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="3fd36-158">Client authentication certificates</span><span class="sxs-lookup"><span data-stu-id="3fd36-158">Client authentication certificates</span></span>
<span data-ttu-id="3fd36-159">Additional client certificates authenticate administrators for cluster management tasks.</span><span class="sxs-lookup"><span data-stu-id="3fd36-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="3fd36-160">Service Fabric has two access levels: **admin** and **read-only user**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="3fd36-161">At minimum, a single certificate for administrative access should be used.</span><span class="sxs-lookup"><span data-stu-id="3fd36-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="3fd36-162">For additional user-level access, a separate certificate must be provided.</span><span class="sxs-lookup"><span data-stu-id="3fd36-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="3fd36-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="3fd36-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="3fd36-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3fd36-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="3fd36-165">These certificates only need to be provided to users who are authorized for cluster management.</span><span class="sxs-lookup"><span data-stu-id="3fd36-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> Azure Active Directory is the recommended way to authenticate clients for cluster management operations. To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="3fd36-168">Application certificates (optional)</span><span class="sxs-lookup"><span data-stu-id="3fd36-168">Application certificates (optional)</span></span>
<span data-ttu-id="3fd36-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span><span class="sxs-lookup"><span data-stu-id="3fd36-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="3fd36-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span><span class="sxs-lookup"><span data-stu-id="3fd36-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="3fd36-171">Encryption and decryption of application configuration values</span><span class="sxs-lookup"><span data-stu-id="3fd36-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="3fd36-172">Encryption of data across nodes during replication</span><span class="sxs-lookup"><span data-stu-id="3fd36-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="3fd36-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3fd36-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="3fd36-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="3fd36-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="3fd36-175">You can also add application certificates to the cluster after it has been created.</span><span class="sxs-lookup"><span data-stu-id="3fd36-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="3fd36-176">Formatting certificates for Azure resource provider use</span><span class="sxs-lookup"><span data-stu-id="3fd36-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="3fd36-177">Private key files (.pfx) can be added and used directly through Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3fd36-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="3fd36-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span><span class="sxs-lookup"><span data-stu-id="3fd36-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="3fd36-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3fd36-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="3fd36-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="3fd36-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="3fd36-181">Follow these steps to use the module:</span><span class="sxs-lookup"><span data-stu-id="3fd36-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="3fd36-182">Download the entire contents of the repo into a local directory.</span><span class="sxs-lookup"><span data-stu-id="3fd36-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="3fd36-183">Import the module in your PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="3fd36-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="3fd36-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3fd36-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="3fd36-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3fd36-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="3fd36-186">Repeat this step for any additional certificates you want to install in your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="3fd36-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="3fd36-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="3fd36-188">At this point, you should now have the following setup in Azure:</span><span class="sxs-lookup"><span data-stu-id="3fd36-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="3fd36-189">Key Vault resource group</span><span class="sxs-lookup"><span data-stu-id="3fd36-189">Key Vault resource group</span></span>
  * <span data-ttu-id="3fd36-190">Key Vault</span><span class="sxs-lookup"><span data-stu-id="3fd36-190">Key Vault</span></span>
    * <span data-ttu-id="3fd36-191">Cluster server authentication certificate</span><span class="sxs-lookup"><span data-stu-id="3fd36-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="3fd36-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="3fd36-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="3fd36-193">Create cluster in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3fd36-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="3fd36-194">Search for the Service Fabric cluster resource</span><span class="sxs-lookup"><span data-stu-id="3fd36-194">Search for the Service Fabric cluster resource</span></span>
![search for Service Fabric cluster template on the Azure portal.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="3fd36-196">Sign in to the [Azure portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3fd36-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="3fd36-197">Click **New** to add a new resource template.</span><span class="sxs-lookup"><span data-stu-id="3fd36-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="3fd36-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="3fd36-199">Select **Service Fabric Cluster** from the list.</span><span class="sxs-lookup"><span data-stu-id="3fd36-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="3fd36-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span><span class="sxs-lookup"><span data-stu-id="3fd36-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="3fd36-201">The **Create Service Fabric cluster** blade has the following four steps.</span><span class="sxs-lookup"><span data-stu-id="3fd36-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="3fd36-202">1. Basics</span><span class="sxs-lookup"><span data-stu-id="3fd36-202">1. Basics</span></span>
![Screen shot of creating a new resource group.][CreateRG]

<span data-ttu-id="3fd36-204">In the Basics blade you need to provide the basic details for your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="3fd36-205">Enter the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="3fd36-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span><span class="sxs-lookup"><span data-stu-id="3fd36-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="3fd36-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3fd36-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="3fd36-208">Create a **new resource group**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-208">Create a **new resource group**.</span></span> <span data-ttu-id="3fd36-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > Although you can decide to use an existing resource group, it is a good practice to create a new resource group. This makes it easy to delete clusters that you do not need.
   > 
   > 
5. <span data-ttu-id="3fd36-212">Select the **region** in which you want to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="3fd36-213">You must use the same region that your Key Vault is in.</span><span class="sxs-lookup"><span data-stu-id="3fd36-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="3fd36-214">2. Cluster configuration</span><span class="sxs-lookup"><span data-stu-id="3fd36-214">2. Cluster configuration</span></span>
![Create a node type][CreateNodeType]

<span data-ttu-id="3fd36-216">Configure your cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="3fd36-216">Configure your cluster nodes.</span></span> <span data-ttu-id="3fd36-217">Node types define the VM sizes, the number of VMs, and their properties.</span><span class="sxs-lookup"><span data-stu-id="3fd36-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="3fd36-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span><span class="sxs-lookup"><span data-stu-id="3fd36-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="3fd36-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span><span class="sxs-lookup"><span data-stu-id="3fd36-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> A common scenario for multiple node types is an application that contains a front-end service and a back-end service. You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.
> 
> 

1. <span data-ttu-id="3fd36-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span><span class="sxs-lookup"><span data-stu-id="3fd36-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="3fd36-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="3fd36-224">The default for the durability tier is bronze.</span><span class="sxs-lookup"><span data-stu-id="3fd36-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="3fd36-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="3fd36-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="3fd36-226">Select the VM size and pricing tier.</span><span class="sxs-lookup"><span data-stu-id="3fd36-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="3fd36-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span><span class="sxs-lookup"><span data-stu-id="3fd36-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="3fd36-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span><span class="sxs-lookup"><span data-stu-id="3fd36-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="3fd36-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span><span class="sxs-lookup"><span data-stu-id="3fd36-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="3fd36-230">The default for the reliability tier is Silver.</span><span class="sxs-lookup"><span data-stu-id="3fd36-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="3fd36-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="3fd36-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="3fd36-232">Choose the number of VMs for the node type.</span><span class="sxs-lookup"><span data-stu-id="3fd36-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="3fd36-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span><span class="sxs-lookup"><span data-stu-id="3fd36-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="3fd36-234">Other node types can have a minimum of 1 VM.</span><span class="sxs-lookup"><span data-stu-id="3fd36-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="3fd36-235">Configure custom endpoints.</span><span class="sxs-lookup"><span data-stu-id="3fd36-235">Configure custom endpoints.</span></span> <span data-ttu-id="3fd36-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span><span class="sxs-lookup"><span data-stu-id="3fd36-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="3fd36-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="3fd36-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="3fd36-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="3fd36-239">Configure cluster **diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="3fd36-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span><span class="sxs-lookup"><span data-stu-id="3fd36-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="3fd36-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="3fd36-242">Turning off diagnostics is **not** recommended.</span><span class="sxs-lookup"><span data-stu-id="3fd36-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="3fd36-243">Select the Fabric upgrade mode you want set your cluster to.</span><span class="sxs-lookup"><span data-stu-id="3fd36-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="3fd36-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span><span class="sxs-lookup"><span data-stu-id="3fd36-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="3fd36-245">Set the mode to **Manual**, if you want to choose a supported version.</span><span class="sxs-lookup"><span data-stu-id="3fd36-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> We support only clusters that are running supported versions of service Fabric. By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version. For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a><span data-ttu-id="3fd36-249">3. Security</span><span class="sxs-lookup"><span data-stu-id="3fd36-249">3. Security</span></span>
![Screen shot of security configurations on Azure portal.][SecurityConfigs]

<span data-ttu-id="3fd36-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span><span class="sxs-lookup"><span data-stu-id="3fd36-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="3fd36-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="3fd36-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="3fd36-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="3fd36-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span><span class="sxs-lookup"><span data-stu-id="3fd36-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="3fd36-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span><span class="sxs-lookup"><span data-stu-id="3fd36-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="3fd36-256">4. Summary</span><span class="sxs-lookup"><span data-stu-id="3fd36-256">4. Summary</span></span>
![<span data-ttu-id="3fd36-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span><span class="sxs-lookup"><span data-stu-id="3fd36-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="3fd36-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd36-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="3fd36-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span><span class="sxs-lookup"><span data-stu-id="3fd36-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="3fd36-260">You can see the creation progress in the notifications.</span><span class="sxs-lookup"><span data-stu-id="3fd36-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="3fd36-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span><span class="sxs-lookup"><span data-stu-id="3fd36-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="3fd36-262">View your cluster status</span><span class="sxs-lookup"><span data-stu-id="3fd36-262">View your cluster status</span></span>
![Screen shot of cluster details in the dashboard.][ClusterDashboard]

<span data-ttu-id="3fd36-264">Once your cluster is created, you can inspect your cluster in the portal:</span><span class="sxs-lookup"><span data-stu-id="3fd36-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="3fd36-265">Go to **Browse** and click **Service Fabric Clusters**.</span><span class="sxs-lookup"><span data-stu-id="3fd36-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="3fd36-266">Locate your cluster and click it.</span><span class="sxs-lookup"><span data-stu-id="3fd36-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="3fd36-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="3fd36-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="3fd36-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span><span class="sxs-lookup"><span data-stu-id="3fd36-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="3fd36-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="3fd36-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum". Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="3fd36-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span><span class="sxs-lookup"><span data-stu-id="3fd36-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="3fd36-273">Each of the NodeTypes you specify in your cluster results in a VM Scale Set getting set-up.</span><span class="sxs-lookup"><span data-stu-id="3fd36-273">Each of the NodeTypes you specify in your cluster results in a VM Scale Set getting set-up.</span></span> <span data-ttu-id="3fd36-274">See [Remote connect to a VM Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span><span class="sxs-lookup"><span data-stu-id="3fd36-274">See [Remote connect to a VM Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fd36-275">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fd36-275">Next steps</span></span>
<span data-ttu-id="3fd36-276">At this point, you have a secure cluster using certificates for management authentication.</span><span class="sxs-lookup"><span data-stu-id="3fd36-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="3fd36-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="3fd36-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="3fd36-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="3fd36-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png







