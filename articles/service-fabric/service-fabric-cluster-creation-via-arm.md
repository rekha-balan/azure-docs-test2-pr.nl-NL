---
title: Create an Azure Service Fabric cluster | Microsoft Docs
description: Learn how to set up a secure Service Fabric cluster in Azure using Azure Resource Manager.  You can create a cluster using a default template or using your own cluster template.
services: service-fabric
documentationcenter: .net
author: aljo-microsoft
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2018
ms.author: aljo
ms.openlocfilehash: aab985270cf17b94d6353536c96a3825b5e3b73f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819395"
---
# <a name="create-a-service-fabric-cluster-using-azure-resource-manager"></a><span data-ttu-id="9081c-104">Create a Service Fabric cluster using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9081c-104">Create a Service Fabric cluster using Azure Resource Manager</span></span> 
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure portal](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="9081c-107">An [Azure Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual machines into which your microservices are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="9081c-107">An [Azure Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual machines into which your microservices are deployed and managed.</span></span>  <span data-ttu-id="9081c-108">A Service Fabric cluster running in Azure is an Azure resource and is deployed using the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9081c-108">A Service Fabric cluster running in Azure is an Azure resource and is deployed using the Azure Resource Manager.</span></span> <span data-ttu-id="9081c-109">This article describes how to deploy a secure Service Fabric cluster in Azure using the Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9081c-109">This article describes how to deploy a secure Service Fabric cluster in Azure using the Resource Manager.</span></span> <span data-ttu-id="9081c-110">You can use a default cluster template or a custom template.</span><span class="sxs-lookup"><span data-stu-id="9081c-110">You can use a default cluster template or a custom template.</span></span>  <span data-ttu-id="9081c-111">If you don't already have a custom template, you can [learn how to create one](service-fabric-cluster-creation-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="9081c-111">If you don't already have a custom template, you can [learn how to create one](service-fabric-cluster-creation-create-template.md).</span></span>

<span data-ttu-id="9081c-112">Cluster security is configured when the cluster is first setup and cannot be changed later.</span><span class="sxs-lookup"><span data-stu-id="9081c-112">Cluster security is configured when the cluster is first setup and cannot be changed later.</span></span> <span data-ttu-id="9081c-113">Before setting up a cluster, read [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="9081c-113">Before setting up a cluster, read [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span> <span data-ttu-id="9081c-114">In Azure, Service Fabric uses x509 certificate to secure your cluster and its endpoints, authenticate clients, and encrypt data.</span><span class="sxs-lookup"><span data-stu-id="9081c-114">In Azure, Service Fabric uses x509 certificate to secure your cluster and its endpoints, authenticate clients, and encrypt data.</span></span> <span data-ttu-id="9081c-115">Azure Active Directory is also recommended to secure access to management endpoints.</span><span class="sxs-lookup"><span data-stu-id="9081c-115">Azure Active Directory is also recommended to secure access to management endpoints.</span></span> <span data-ttu-id="9081c-116">Azure AD tenants and users must be created before creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="9081c-116">Azure AD tenants and users must be created before creating the cluster.</span></span>  <span data-ttu-id="9081c-117">For more information, read [Set up Azure AD to authenticate clients](service-fabric-cluster-creation-setup-aad.md).</span><span class="sxs-lookup"><span data-stu-id="9081c-117">For more information, read [Set up Azure AD to authenticate clients](service-fabric-cluster-creation-setup-aad.md).</span></span>

<span data-ttu-id="9081c-118">If you are creating a production cluster to run production workloads, we recommend you first read through the [production readiness checklist](service-fabric-production-readiness-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="9081c-118">If you are creating a production cluster to run production workloads, we recommend you first read through the [production readiness checklist](service-fabric-production-readiness-checklist.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9081c-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9081c-119">Prerequisites</span></span> 
<span data-ttu-id="9081c-120">In this article, use the Service Fabric RM powershell or Azure CLI modules to deploy a cluster:</span><span class="sxs-lookup"><span data-stu-id="9081c-120">In this article, use the Service Fabric RM powershell or Azure CLI modules to deploy a cluster:</span></span>

* <span data-ttu-id="9081c-121">[Azure PowerShell 4.1 and above][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="9081c-121">[Azure PowerShell 4.1 and above][azure-powershell]</span></span>
* <span data-ttu-id="9081c-122">[Azure CLI 2.0 and above][azure-CLI]</span><span class="sxs-lookup"><span data-stu-id="9081c-122">[Azure CLI 2.0 and above][azure-CLI]</span></span>

<span data-ttu-id="9081c-123">You can find the reference documentation for the Service Fabric modules here:</span><span class="sxs-lookup"><span data-stu-id="9081c-123">You can find the reference documentation for the Service Fabric modules here:</span></span>
* [<span data-ttu-id="9081c-124">AzureRM.ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="9081c-124">AzureRM.ServiceFabric</span></span>](https://docs.microsoft.com/powershell/module/azurerm.servicefabric)
* [<span data-ttu-id="9081c-125">az SF CLI module</span><span class="sxs-lookup"><span data-stu-id="9081c-125">az SF CLI module</span></span>](https://docs.microsoft.com/cli/azure/sf?view=azure-cli-latest)

### <a name="sign-in-to-azure"></a><span data-ttu-id="9081c-126">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="9081c-126">Sign in to Azure</span></span>

<span data-ttu-id="9081c-127">Before running any of the commands in this article, first sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="9081c-127">Before running any of the commands in this article, first sign in to Azure.</span></span>

```powershell
Connect-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subscriptionId>
```

```azurecli
az login
az account set --subscription $subscriptionId
```

## <a name="create-a-new-cluster-using-a-system-generated-self-signed-certificate"></a><span data-ttu-id="9081c-128">Create a new cluster using a system generated self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="9081c-128">Create a new cluster using a system generated self-signed certificate</span></span>

<span data-ttu-id="9081c-129">Use the following commands to create a cluster secured with a system generated self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="9081c-129">Use the following commands to create a cluster secured with a system generated self-signed certificate.</span></span> <span data-ttu-id="9081c-130">This command sets up a primary cluster certificate that is used for cluster security and to set up admin access to perform management operations using that certificate.</span><span class="sxs-lookup"><span data-stu-id="9081c-130">This command sets up a primary cluster certificate that is used for cluster security and to set up admin access to perform management operations using that certificate.</span></span>  <span data-ttu-id="9081c-131">Self-signed certificates are useful for securing test clusters.</span><span class="sxs-lookup"><span data-stu-id="9081c-131">Self-signed certificates are useful for securing test clusters.</span></span>  <span data-ttu-id="9081c-132">Production clusters should be secured with a certificate from a certificate authority (CA).</span><span class="sxs-lookup"><span data-stu-id="9081c-132">Production clusters should be secured with a certificate from a certificate authority (CA).</span></span>

### <a name="use-the-default-cluster-template-that-ships-in-the-module"></a><span data-ttu-id="9081c-133">Use the default cluster template that ships in the module</span><span class="sxs-lookup"><span data-stu-id="9081c-133">Use the default cluster template that ships in the module</span></span>

<span data-ttu-id="9081c-134">Use the following command to create a cluster quickly, by specifying minimal parameters, using the default template.</span><span class="sxs-lookup"><span data-stu-id="9081c-134">Use the following command to create a cluster quickly, by specifying minimal parameters, using the default template.</span></span>

<span data-ttu-id="9081c-135">The template that is used is available on the [Azure Service Fabric template samples : windows template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Windows-1-NodeTypes-Secure-NSG) and [Ubuntu template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Ubuntu-1-NodeTypes-Secure)</span><span class="sxs-lookup"><span data-stu-id="9081c-135">The template that is used is available on the [Azure Service Fabric template samples : windows template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Windows-1-NodeTypes-Secure-NSG) and [Ubuntu template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Ubuntu-1-NodeTypes-Secure)</span></span>

<span data-ttu-id="9081c-136">The following command can create either Windows or Linux clusters, you need to specify the OS accordingly.</span><span class="sxs-lookup"><span data-stu-id="9081c-136">The following command can create either Windows or Linux clusters, you need to specify the OS accordingly.</span></span> <span data-ttu-id="9081c-137">The PowerShell/CLI commands also output the certificate in the specified *CertificateOutputFolder*; however, make sure certificate folder already created.</span><span class="sxs-lookup"><span data-stu-id="9081c-137">The PowerShell/CLI commands also output the certificate in the specified *CertificateOutputFolder*; however, make sure certificate folder already created.</span></span> <span data-ttu-id="9081c-138">The command takes in other parameters such as VM SKU as well.</span><span class="sxs-lookup"><span data-stu-id="9081c-138">The command takes in other parameters such as VM SKU as well.</span></span>

> [!NOTE]
> The following PowerShell command only works with Azure Resource Manager PowerShell version > 6.1. To check the current version of Azure Resource Manager PowerShell version, run the following PowerShell command "Get-Module AzureRM". Follow [this link](/powershell/azure/install-azurerm-ps?view=azurermps-6.3.0) to upgrade your Azure Resource Manager PowerShell version. 
>
>

<span data-ttu-id="9081c-142">Deploy the cluster using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9081c-142">Deploy the cluster using PowerShell:</span></span>

```powershell
$resourceGroupLocation="westus"
$resourceGroupName="mycluster"
$vaultName="myvault"
$vaultResourceGroupName="myvaultrg"
$CertSubjectName="mycluster.westus.cloudapp.azure.com"
$certPassword="Password123!@#" | ConvertTo-SecureString -AsPlainText -Force 
$vmpassword="Password4321!@#" | ConvertTo-SecureString -AsPlainText -Force
$vmuser="myadmin"
$os="WindowsServer2016DatacenterwithContainers"
$certOutputFolder="c:\certificates"

New-AzureRmServiceFabricCluster -ResourceGroupName $resourceGroupName -Location $resourceGroupLocation -CertificateOutputFolder $certOutputFolder -CertificatePassword $certpassword -CertificateSubjectName $CertSubjectName -OS $os -VmPassword $vmpassword -VmUserName $vmuser
```

<span data-ttu-id="9081c-143">Deploy the cluster using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="9081c-143">Deploy the cluster using Azure CLI:</span></span>

```azurecli
declare resourceGroupLocation="westus"
declare resourceGroupName="mylinux"
declare vaultResourceGroupName="myvaultrg"
declare vaultName="myvault"
declare CertSubjectName="mylinux.westus.cloudapp.azure.com"
declare vmpassword="Password!1"
declare certpassword="Password!4321"
declare vmuser="myadmin"
declare vmOs="UbuntuServer1604"
declare certOutputFolder="c:\certificates"

az sf cluster create --resource-group $resourceGroupName --location $resourceGroupLocation  \
    --certificate-output-folder $certOutputFolder --certificate-password $certpassword  \
    --vault-name $vaultName --vault-resource-group $resourceGroupName  \
    --template-file $templateFilePath --parameter-file $parametersFilePath --vm-os $vmOs  \
    --vm-password $vmpassword --vm-user-name $vmuser
```

### <a name="use-your-own-custom-template"></a><span data-ttu-id="9081c-144">Use your own custom template</span><span class="sxs-lookup"><span data-stu-id="9081c-144">Use your own custom template</span></span>

<span data-ttu-id="9081c-145">If you need to author a custom template to suit your needs, it is highly recommended that you start with one of the templates that are available on the [Azure Service Fabric template samples](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master).</span><span class="sxs-lookup"><span data-stu-id="9081c-145">If you need to author a custom template to suit your needs, it is highly recommended that you start with one of the templates that are available on the [Azure Service Fabric template samples](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master).</span></span> <span data-ttu-id="9081c-146">Learn how to [customize your cluster template][customize-your-cluster-template].</span><span class="sxs-lookup"><span data-stu-id="9081c-146">Learn how to [customize your cluster template][customize-your-cluster-template].</span></span>

<span data-ttu-id="9081c-147">If you already have a custom template, double-check that all the three certificate related parameters in the template and the parameter file are named as follows and values are null as follows:</span><span class="sxs-lookup"><span data-stu-id="9081c-147">If you already have a custom template, double-check that all the three certificate related parameters in the template and the parameter file are named as follows and values are null as follows:</span></span>

```json
   "certificateThumbprint": {
      "value": ""
    },
    "sourceVaultValue": {
      "value": ""
    },
    "certificateUrlValue": {
      "value": ""
    },
```

<span data-ttu-id="9081c-148">Deploy the cluster using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9081c-148">Deploy the cluster using PowerShell:</span></span>

```powershell
$resourceGroupLocation="westus"
$resourceGroupName="mycluster"
$CertSubjectName="mycluster.westus.cloudapp.azure.com"
$certPassword="Password!1" | ConvertTo-SecureString -AsPlainText -Force 
$certOutputFolder="c:\certificates"

$parameterFilePath="c:\mytemplates\mytemplateparm.json"
$templateFilePath="c:\mytemplates\mytemplate.json"

New-AzureRmServiceFabricCluster -ResourceGroupName $resourceGroupName -CertificateOutputFolder $certOutputFolder -CertificatePassword $certpassword -CertificateSubjectName $CertSubjectName -TemplateFile $templateFilePath -ParameterFile $parameterFilePath 
```

<span data-ttu-id="9081c-149">Deploy the cluster using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="9081c-149">Deploy the cluster using Azure CLI:</span></span>

```azurecli
declare certPassword=""
declare resourceGroupLocation="westus"
declare resourceGroupName="mylinux"
declare certSubjectName="mylinuxsecure.westus.cloudapp.azure.com"
declare parameterFilePath="c:\mytemplates\linuxtemplateparm.json"
declare templateFilePath="c:\mytemplates\linuxtemplate.json"
declare certOutputFolder="c:\certificates"

az sf cluster create --resource-group $resourceGroupName --location $resourceGroupLocation  \
    --certificate-output-folder $certOutputFolder --certificate-password $certPassword  \
    --certificate-subject-name $certSubjectName \
    --template-file $templateFilePath --parameter-file $parametersFilePath
```

## <a name="create-a-new-cluster-using-your-own-x509-certificate"></a><span data-ttu-id="9081c-150">Create a new cluster using your own X.509 certificate</span><span class="sxs-lookup"><span data-stu-id="9081c-150">Create a new cluster using your own X.509 certificate</span></span>

<span data-ttu-id="9081c-151">Use the following command to create cluster, if you have a certificate that you want to use to secure your cluster with.</span><span class="sxs-lookup"><span data-stu-id="9081c-151">Use the following command to create cluster, if you have a certificate that you want to use to secure your cluster with.</span></span>

<span data-ttu-id="9081c-152">If this is a CA signed certificate that you will end up using for other purposes as well, then it is recommended that you provide a distinct resource group specifically for your key vault.</span><span class="sxs-lookup"><span data-stu-id="9081c-152">If this is a CA signed certificate that you will end up using for other purposes as well, then it is recommended that you provide a distinct resource group specifically for your key vault.</span></span> <span data-ttu-id="9081c-153">We recommend that you put the key vault into its own resource group.</span><span class="sxs-lookup"><span data-stu-id="9081c-153">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="9081c-154">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="9081c-154">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="9081c-155">**The resource group that contains your key vault *must be in the same region* as the cluster that is using it.**</span><span class="sxs-lookup"><span data-stu-id="9081c-155">**The resource group that contains your key vault *must be in the same region* as the cluster that is using it.**</span></span>

### <a name="use-the-default-five-node-one-node-type-template-that-ships-in-the-module"></a><span data-ttu-id="9081c-156">Use the default five node, one node type template that ships in the module</span><span class="sxs-lookup"><span data-stu-id="9081c-156">Use the default five node, one node type template that ships in the module</span></span>
<span data-ttu-id="9081c-157">The template that is used is available on the [Azure samples : Windows template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Windows-1-NodeTypes-Secure-NSG) and [Ubuntu template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Ubuntu-1-NodeTypes-Secure)</span><span class="sxs-lookup"><span data-stu-id="9081c-157">The template that is used is available on the [Azure samples : Windows template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Windows-1-NodeTypes-Secure-NSG) and [Ubuntu template](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master/5-VM-Ubuntu-1-NodeTypes-Secure)</span></span>

<span data-ttu-id="9081c-158">Deploy the cluster using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9081c-158">Deploy the cluster using PowerShell:</span></span>

```powershell
$resourceGroupLocation="westus"
$resourceGroupName="mylinux"
$vaultName="myvault"
$vaultResourceGroupName="myvaultrg"
$certPassword="Password!1" | ConvertTo-SecureString -AsPlainText -Force 
$vmpassword=("Password!4321" | ConvertTo-SecureString -AsPlainText -Force) 
$vmuser="myadmin"
$os="WindowsServer2016DatacenterwithContainers"

New-AzureRmServiceFabricCluster -ResourceGroupName $resourceGroupName -Location $resourceGroupLocation -KeyVaultResouceGroupName $vaultResourceGroupName -KeyVaultName $vaultName -CertificateFile C:\MyCertificates\chackocertificate3.pfx -CertificatePassword $certPassword -OS $os -VmPassword $vmpassword -VmUserName $vmuser 
```

<span data-ttu-id="9081c-159">Deploy the cluster using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="9081c-159">Deploy the cluster using Azure CLI:</span></span>

```azurecli
declare vmPassword="Password!1"
declare certPassword="Password!1"
declare vmUser="myadmin"
declare resourceGroupLocation="westus"
declare resourceGroupName="mylinux"
declare vaultResourceGroupName="myvaultrg"
declare vaultName="myvault"
declare certificate-file="c:\certificates\mycert.pem"
declare vmOs="UbuntuServer1604"

az sf cluster create --resource-group $resourceGroupName --location $resourceGroupLocation  \
    --certificate-file $certificate-file --certificate-password $certPassword  \
    --vault-name $vaultName --vault-resource-group $vaultResourceGroupName  \
    --vm-os vmOs \
    --vm-password $vmPassword --vm-user-name $vmUser
```

### <a name="use-your-own-custom-cluster-template"></a><span data-ttu-id="9081c-160">Use your own custom cluster template</span><span class="sxs-lookup"><span data-stu-id="9081c-160">Use your own custom cluster template</span></span>
<span data-ttu-id="9081c-161">If you need to author a custom template to suit your needs, it is highly recommended that you start with one of the templates that are available on the [Azure Service Fabric template samples](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master).</span><span class="sxs-lookup"><span data-stu-id="9081c-161">If you need to author a custom template to suit your needs, it is highly recommended that you start with one of the templates that are available on the [Azure Service Fabric template samples](https://github.com/Azure-Samples/service-fabric-cluster-templates/tree/master).</span></span> <span data-ttu-id="9081c-162">Learn how to [customize your cluster template][customize-your-cluster-template].</span><span class="sxs-lookup"><span data-stu-id="9081c-162">Learn how to [customize your cluster template][customize-your-cluster-template].</span></span>

<span data-ttu-id="9081c-163">If you already have a custom template, then make sure to double check that all the three certificate related parameters in the template and the parameter file are named as follows and values are null as follows.</span><span class="sxs-lookup"><span data-stu-id="9081c-163">If you already have a custom template, then make sure to double check that all the three certificate related parameters in the template and the parameter file are named as follows and values are null as follows.</span></span>

```json
   "certificateThumbprint": {
      "value": ""
    },
    "sourceVaultValue": {
      "value": ""
    },
    "certificateUrlValue": {
      "value": ""
    },
```

<span data-ttu-id="9081c-164">Deploy the cluster using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9081c-164">Deploy the cluster using PowerShell:</span></span>

```powershell
$resourceGroupLocation="westus"
$resourceGroupName="mylinux"
$vaultName="myvault"
$vaultResourceGroupName="myvaultrg"
$certPassword="Password!1" | ConvertTo-SecureString -AsPlainText -Force 
$os="WindowsServer2016DatacenterwithContainers"
$parameterFilePath="c:\mytemplates\mytemplateparm.json"
$templateFilePath="c:\mytemplates\mytemplate.json"
$certificateFile="C:\MyCertificates\chackonewcertificate3.pem"

New-AzureRmServiceFabricCluster -ResourceGroupName $resourceGroupName -Location $resourceGroupLocation -TemplateFile $templateFilePath -ParameterFile $parameterFilePath -KeyVaultResouceGroupName $vaultResourceGroupName -KeyVaultName $vaultName -CertificateFile $certificateFile -CertificatePassword $certPassword
```

<span data-ttu-id="9081c-165">Deploy the cluster using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="9081c-165">Deploy the cluster using Azure CLI:</span></span>

```azurecli
declare certPassword="Password!1"
declare resourceGroupLocation="westus"
declare resourceGroupName="mylinux"
declare vaultResourceGroupName="myvaultrg"
declare vaultName="myvault"
declare parameterFilePath="c:\mytemplates\linuxtemplateparm.json"
declare templateFilePath="c:\mytemplates\linuxtemplate.json"

az sf cluster create --resource-group $resourceGroupName --location $resourceGroupLocation  \
    --certificate-file $certificate-file --certificate-password $password  \
    --vault-name $vaultName --vault-resource-group $vaultResourceGroupName  \
    --template-file $templateFilePath --parameter-file $parametersFilePath 
```

### <a name="use-a-pointer-to-a-secret-uploaded-into-a-key-vault"></a><span data-ttu-id="9081c-166">Use a pointer to a secret uploaded into a key vault</span><span class="sxs-lookup"><span data-stu-id="9081c-166">Use a pointer to a secret uploaded into a key vault</span></span>

<span data-ttu-id="9081c-167">To use an existing key vault, the key vault must be [enabled for deployment](../key-vault/key-vault-manage-with-cli2.md#bkmk_KVperCLI) to allow the compute resource provider to get certificates from it and install it on cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="9081c-167">To use an existing key vault, the key vault must be [enabled for deployment](../key-vault/key-vault-manage-with-cli2.md#bkmk_KVperCLI) to allow the compute resource provider to get certificates from it and install it on cluster nodes.</span></span>

<span data-ttu-id="9081c-168">Deploy the cluster using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9081c-168">Deploy the cluster using PowerShell:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

$parameterFilePath="c:\mytemplates\mytemplate.json"
$templateFilePath="c:\mytemplates\mytemplateparm.json"
$secretID="https://test1.vault.azure.net:443/secrets/testcertificate4/55ec7c4dc61a462bbc645ffc9b4b225f"

New-AzureRmServiceFabricCluster -ResourceGroupName $resourceGroupName -SecretIdentifier $secretId -TemplateFile $templateFilePath -ParameterFile $parameterFilePath 
```

<span data-ttu-id="9081c-169">Deploy the cluster using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="9081c-169">Deploy the cluster using Azure CLI:</span></span>

```azurecli
declare $resourceGroupName = "testRG"
declare $parameterFilePath="c:\mytemplates\mytemplate.json"
declare $templateFilePath="c:\mytemplates\mytemplateparm.json"
declare $secertId="https://test1.vault.azure.net:443/secrets/testcertificate4/55ec7c4dc61a462bbc645ffc9b4b225f"

az sf cluster create --resource-group $resourceGroupName --location $resourceGroupLocation  \
    --secret-identifier az $secretID  \
    --template-file $templateFilePath --parameter-file $parametersFilePath 
```

## <a name="next-steps"></a><span data-ttu-id="9081c-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="9081c-170">Next steps</span></span>
<span data-ttu-id="9081c-171">At this point, you have a secure cluster running in Azure.</span><span class="sxs-lookup"><span data-stu-id="9081c-171">At this point, you have a secure cluster running in Azure.</span></span> <span data-ttu-id="9081c-172">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="9081c-172">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

<!-- Links -->
[azure-powershell]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[azure-CLI]:https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[customize-your-cluster-template]: service-fabric-cluster-creation-via-arm.md#create-a-service-fabric-cluster-resource-manager-template
