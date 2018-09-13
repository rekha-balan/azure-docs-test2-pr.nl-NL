---
title: HPC Pack 2016 cluster in Azure | Microsoft Docs
description: Learn how to deploy an HPC Pack 2016 cluster in Azure
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 03/09/2018
ms.author: danlep
ms.openlocfilehash: 24cd71b704c812eecbb55b11cc20cf521d31bbc4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827749"
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="01ee2-103">Deploy an HPC Pack 2016 cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="01ee2-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="01ee2-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016 Update 1](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="01ee2-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016 Update 1](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="01ee2-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span><span class="sxs-lookup"><span data-stu-id="01ee2-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="01ee2-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span><span class="sxs-lookup"><span data-stu-id="01ee2-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="01ee2-107">You have several choices of cluster topology with different numbers and types of cluster head nodes and compute nodes.</span><span class="sxs-lookup"><span data-stu-id="01ee2-107">You have several choices of cluster topology with different numbers and types of cluster head nodes and compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01ee2-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="01ee2-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="01ee2-109">PFX certificate</span><span class="sxs-lookup"><span data-stu-id="01ee2-109">PFX certificate</span></span>

<span data-ttu-id="01ee2-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span><span class="sxs-lookup"><span data-stu-id="01ee2-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="01ee2-111">The certificate must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="01ee2-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="01ee2-112">It must have a private key capable of key exchange</span><span class="sxs-lookup"><span data-stu-id="01ee2-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="01ee2-113">Key usage includes Digital Signature and Key Encipherment</span><span class="sxs-lookup"><span data-stu-id="01ee2-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="01ee2-114">Enhanced key usage includes Client Authentication and Server Authentication</span><span class="sxs-lookup"><span data-stu-id="01ee2-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="01ee2-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span><span class="sxs-lookup"><span data-stu-id="01ee2-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="01ee2-116">Alternatively, use the following commands to generate the self-signed certificate based on the operating system on which you run the command.</span><span class="sxs-lookup"><span data-stu-id="01ee2-116">Alternatively, use the following commands to generate the self-signed certificate based on the operating system on which you run the command.</span></span> <span data-ttu-id="01ee2-117">Then, export the certificate as a password-protected PFX file with private key.</span><span class="sxs-lookup"><span data-stu-id="01ee2-117">Then, export the certificate as a password-protected PFX file with private key.</span></span>

* <span data-ttu-id="01ee2-118">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span><span class="sxs-lookup"><span data-stu-id="01ee2-118">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="01ee2-119">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="01ee2-119">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="01ee2-120">Extract its contents and run the following commands at a PowerShell prompt:</span><span class="sxs-lookup"><span data-stu-id="01ee2-120">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

<span data-ttu-id="01ee2-121">After the certificate is created in the Current User store, use the Certificates snap-in to export the certificate as a password-protected PFX file with private key.</span><span class="sxs-lookup"><span data-stu-id="01ee2-121">After the certificate is created in the Current User store, use the Certificates snap-in to export the certificate as a password-protected PFX file with private key.</span></span> <span data-ttu-id="01ee2-122">You can also export the certificate using the [Export-Pfxcertificate](/powershell/module/pkiclient/export-pfxcertificate?view=win10-ps) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01ee2-122">You can also export the certificate using the [Export-Pfxcertificate](/powershell/module/pkiclient/export-pfxcertificate?view=win10-ps) PowerShell cmdlet.</span></span>

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="01ee2-123">Upload certificate to an Azure key vault</span><span class="sxs-lookup"><span data-stu-id="01ee2-123">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="01ee2-124">Before deploying the HPC cluster, upload the PFX certificate to an [Azure key vault](../../key-vault/index.yml) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span><span class="sxs-lookup"><span data-stu-id="01ee2-124">Before deploying the HPC cluster, upload the PFX certificate to an [Azure key vault](../../key-vault/index.yml) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="01ee2-125">A sample PowerShell script to upload the certificate, create the key vault, and generate the required information follows.</span><span class="sxs-lookup"><span data-stu-id="01ee2-125">A sample PowerShell script to upload the certificate, create the key vault, and generate the required information follows.</span></span> <span data-ttu-id="01ee2-126">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-126">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="01ee2-127">Supported topologies</span><span class="sxs-lookup"><span data-stu-id="01ee2-127">Supported topologies</span></span>

<span data-ttu-id="01ee2-128">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span><span class="sxs-lookup"><span data-stu-id="01ee2-128">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="01ee2-129">Following are high-level architectures of three example cluster topologies.</span><span class="sxs-lookup"><span data-stu-id="01ee2-129">Following are high-level architectures of three example cluster topologies.</span></span> <span data-ttu-id="01ee2-130">High-availability topologies include multiple cluster head nodes.</span><span class="sxs-lookup"><span data-stu-id="01ee2-130">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="01ee2-131">High-availability cluster with Active Directory domain</span><span class="sxs-lookup"><span data-stu-id="01ee2-131">High-availability cluster with Active Directory domain</span></span>

    ![HA cluster in AD domain](./media/hpcpack-2016-cluster/haad.png)


2. <span data-ttu-id="01ee2-133">High-availability cluster without Active Directory domain</span><span class="sxs-lookup"><span data-stu-id="01ee2-133">High-availability cluster without Active Directory domain</span></span>

    ![HA cluster without AD domain](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="01ee2-135">Cluster with a single head node</span><span class="sxs-lookup"><span data-stu-id="01ee2-135">Cluster with a single head node</span></span>

   ![Cluster with single head node](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="01ee2-137">Deploy a cluster</span><span class="sxs-lookup"><span data-stu-id="01ee2-137">Deploy a cluster</span></span>

<span data-ttu-id="01ee2-138">To create the cluster, choose a template and click **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="01ee2-138">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="01ee2-139">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span><span class="sxs-lookup"><span data-stu-id="01ee2-139">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="01ee2-140">Each template creates all Azure resources required for the HPC cluster infrastructure.</span><span class="sxs-lookup"><span data-stu-id="01ee2-140">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="01ee2-141">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span><span class="sxs-lookup"><span data-stu-id="01ee2-141">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="01ee2-142">Step 1: Select the subscription, location, and resource group</span><span class="sxs-lookup"><span data-stu-id="01ee2-142">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="01ee2-143">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="01ee2-143">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="01ee2-144">We recommend that you create a different **Resource group** for the deployment.</span><span class="sxs-lookup"><span data-stu-id="01ee2-144">We recommend that you create a different **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="01ee2-145">Step 2: Specify the parameter settings</span><span class="sxs-lookup"><span data-stu-id="01ee2-145">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="01ee2-146">Enter or modify values for the template parameters.</span><span class="sxs-lookup"><span data-stu-id="01ee2-146">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="01ee2-147">Click the icon next to each parameter for help information.</span><span class="sxs-lookup"><span data-stu-id="01ee2-147">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="01ee2-148">Also see the guidance for [available VM sizes](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-148">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="01ee2-149">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span><span class="sxs-lookup"><span data-stu-id="01ee2-149">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-terms-and-create"></a><span data-ttu-id="01ee2-150">Step 3.</span><span class="sxs-lookup"><span data-stu-id="01ee2-150">Step 3.</span></span> <span data-ttu-id="01ee2-151">Review terms and create</span><span class="sxs-lookup"><span data-stu-id="01ee2-151">Review terms and create</span></span>
<span data-ttu-id="01ee2-152">Review the terms and conditions associated with the template.</span><span class="sxs-lookup"><span data-stu-id="01ee2-152">Review the terms and conditions associated with the template.</span></span> <span data-ttu-id="01ee2-153">If you agree, click **Purchase** to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="01ee2-153">If you agree, click **Purchase** to start the deployment.</span></span>

<span data-ttu-id="01ee2-154">Depending on the cluster topology, deployment can take 30 minutes or longer to complete.</span><span class="sxs-lookup"><span data-stu-id="01ee2-154">Depending on the cluster topology, deployment can take 30 minutes or longer to complete.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="01ee2-155">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="01ee2-155">Connect to the cluster</span></span>
1. <span data-ttu-id="01ee2-156">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01ee2-156">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="01ee2-157">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span><span class="sxs-lookup"><span data-stu-id="01ee2-157">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="01ee2-158">You can find the head node virtual machines.</span><span class="sxs-lookup"><span data-stu-id="01ee2-158">You can find the head node virtual machines.</span></span>

    ![Cluster head nodes in the portal](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="01ee2-160">Click one head node (in a high-availability cluster, click any of the head nodes).</span><span class="sxs-lookup"><span data-stu-id="01ee2-160">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="01ee2-161">In **Overview**, you can find the public IP address or full DNS name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="01ee2-161">In **Overview**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![Cluster connection settings](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="01ee2-163">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span><span class="sxs-lookup"><span data-stu-id="01ee2-163">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="01ee2-164">If the cluster you deployed is in an Active Directory Domain, the user name is of the form \<privateDomainName>\\\<adminUsername> (for example, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="01ee2-164">If the cluster you deployed is in an Active Directory Domain, the user name is of the form \<privateDomainName>\\\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01ee2-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="01ee2-165">Next steps</span></span>
* <span data-ttu-id="01ee2-166">Submit jobs to your cluster.</span><span class="sxs-lookup"><span data-stu-id="01ee2-166">Submit jobs to your cluster.</span></span> <span data-ttu-id="01ee2-167">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-167">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

