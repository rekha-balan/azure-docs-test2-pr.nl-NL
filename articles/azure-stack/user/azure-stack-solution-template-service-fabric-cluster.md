---
title: Deploy a secured Service Fabric cluster in Azure Stack | Microsoft Docs
description: Learn how to deploy a secured Service Fabric cluster in Azure Stack
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 05/08/2018
ms.author: mattbriggs
ms.reviewer: shnatara
ms.openlocfilehash: 9feb2e538d3578fe259aa3fbc693a1e953f2f894
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966161"
---
# <a name="deploy-a-service-fabric-cluster-in-azure-stack"></a><span data-ttu-id="155a4-103">Deploy a Service Fabric cluster in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="155a4-103">Deploy a Service Fabric cluster in Azure Stack</span></span>

<span data-ttu-id="155a4-104">Use the **Service Fabric Cluster** item from the Azure Marketplace to deploy a secured Service Fabric cluster in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="155a4-104">Use the **Service Fabric Cluster** item from the Azure Marketplace to deploy a secured Service Fabric cluster in Azure Stack.</span></span> 

<span data-ttu-id="155a4-105">For more information about working with Service Fabric, see [Overview of Azure Service Frabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) and [Service Fabric cluster security scenarios](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security), in the Azure documentation.</span><span class="sxs-lookup"><span data-stu-id="155a4-105">For more information about working with Service Fabric, see [Overview of Azure Service Frabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) and [Service Fabric cluster security scenarios](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security), in the Azure documentation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="155a4-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="155a4-106">Prerequisites</span></span>

<span data-ttu-id="155a4-107">The following are required to deploy the Service Fabric cluster:</span><span class="sxs-lookup"><span data-stu-id="155a4-107">The following are required to deploy the Service Fabric cluster:</span></span>
1. <span data-ttu-id="155a4-108">**Cluster certificate**</span><span class="sxs-lookup"><span data-stu-id="155a4-108">**Cluster certificate**</span></span>  
   <span data-ttu-id="155a4-109">This is the X.509 server certificate you add to KeyVault when deploying Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="155a4-109">This is the X.509 server certificate you add to KeyVault when deploying Service Fabric.</span></span> 
   - <span data-ttu-id="155a4-110">The **CN** on this cert must match the Fully Qualified Domain Name (FQDN) of the Service Fabric cluster you create.</span><span class="sxs-lookup"><span data-stu-id="155a4-110">The **CN** on this cert must match the Fully Qualified Domain Name (FQDN) of the Service Fabric cluster you create.</span></span> 
   - <span data-ttu-id="155a4-111">The certificate format must be PFX, as both the public and private keys are required.</span><span class="sxs-lookup"><span data-stu-id="155a4-111">The certificate format must be PFX, as both the public and private keys are required.</span></span> 
   <span data-ttu-id="155a4-112">See [requirements](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) for creating this server-side cert.</span><span class="sxs-lookup"><span data-stu-id="155a4-112">See [requirements](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) for creating this server-side cert.</span></span>

    > [!NOTE]  
    > <span data-ttu-id="155a4-113">You can use a self-signed certificate inplace of the x.509 server certificate for test purposes.</span><span class="sxs-lookup"><span data-stu-id="155a4-113">You can use a self-signed certificate inplace of the x.509 server certificate for test purposes.</span></span> <span data-ttu-id="155a4-114">Self-signed certificates do not need to match the FQDN of the cluster.</span><span class="sxs-lookup"><span data-stu-id="155a4-114">Self-signed certificates do not need to match the FQDN of the cluster.</span></span>

1.  <span data-ttu-id="155a4-115">**Admin Client certificate** This is the certificate that the client will use to authenticate to the Service Fabric cluster, which can be self-signed.</span><span class="sxs-lookup"><span data-stu-id="155a4-115">**Admin Client certificate** This is the certificate that the client will use to authenticate to the Service Fabric cluster, which can be self-signed.</span></span> <span data-ttu-id="155a4-116">See [requirements](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) for creating this client cert.</span><span class="sxs-lookup"><span data-stu-id="155a4-116">See [requirements](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) for creating this client cert.</span></span>

1.  <span data-ttu-id="155a4-117">**The following items must be available in the Azure Stack Marketplace:**</span><span class="sxs-lookup"><span data-stu-id="155a4-117">**The following items must be available in the Azure Stack Marketplace:**</span></span>
     - <span data-ttu-id="155a4-118">**Windows Server 2016** – The template uses the Windows Server 2016 image to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="155a4-118">**Windows Server 2016** – The template uses the Windows Server 2016 image to create the cluster.</span></span>  
     - <span data-ttu-id="155a4-119">**Customer Script Extension** - Virtual Machine Extension from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="155a4-119">**Customer Script Extension** - Virtual Machine Extension from Microsoft.</span></span>  
     - <span data-ttu-id="155a4-120">**PowerShell Desired Stage Configuration** - Virtual Machine Extension from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="155a4-120">**PowerShell Desired Stage Configuration** - Virtual Machine Extension from Microsoft.</span></span>


## <a name="add-a-secret-to-key-vault"></a><span data-ttu-id="155a4-121">Add a secret to Key Vault</span><span class="sxs-lookup"><span data-stu-id="155a4-121">Add a secret to Key Vault</span></span>
<span data-ttu-id="155a4-122">To deploy a Service Fabric cluster, you must specify the correct KeyVault *Secret Identifier* or URL for the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="155a4-122">To deploy a Service Fabric cluster, you must specify the correct KeyVault *Secret Identifier* or URL for the Service Fabric cluster.</span></span> <span data-ttu-id="155a4-123">The Azure Resource Manager template takes a KeyVault as input and then retrieves the Cluster certificate during installation of the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="155a4-123">The Azure Resource Manager template takes a KeyVault as input and then retrieves the Cluster certificate during installation of the Service Fabric cluster.</span></span> 

> [!IMPORTANT]  
> <span data-ttu-id="155a4-124">You must use PowerShell to add a secret to KeyVault for use with Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="155a4-124">You must use PowerShell to add a secret to KeyVault for use with Service Fabric.</span></span> <span data-ttu-id="155a4-125">Do not use the portal.</span><span class="sxs-lookup"><span data-stu-id="155a4-125">Do not use the portal.</span></span>  

<span data-ttu-id="155a4-126">Use the following script to create the KeyVault and add the *cluster certificate* to it.</span><span class="sxs-lookup"><span data-stu-id="155a4-126">Use the following script to create the KeyVault and add the *cluster certificate* to it.</span></span> <span data-ttu-id="155a4-127">(See the [prerequisites](#prerequisites).) Before you run the script, review the sample script and update the indicated parameters to match your environment.</span><span class="sxs-lookup"><span data-stu-id="155a4-127">(See the [prerequisites](#prerequisites).) Before you run the script, review the sample script and update the indicated parameters to match your environment.</span></span> <span data-ttu-id="155a4-128">This script will also output the values you need to provide to the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="155a4-128">This script will also output the values you need to provide to the Azure Resource Manager template.</span></span> 

> [!TIP]  
> <span data-ttu-id="155a4-129">Before the script can succeed, there must be a public offer that includes the services for Compute, Network, Storage, and KeyVault.</span><span class="sxs-lookup"><span data-stu-id="155a4-129">Before the script can succeed, there must be a public offer that includes the services for Compute, Network, Storage, and KeyVault.</span></span> 

  ```PowerShell
    function Get-ThumbprintFromPfx($PfxFilePath, $Password) 
        {
            return New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($PfxFilePath, $Password)
        }
    
    function Publish-SecretToKeyVault ($PfxFilePath, $Password, $KeyVaultName)
       {
            $keyVaultSecretName = "ClusterCertificate"
            $certContentInBytes = [io.file]::ReadAllBytes($PfxFilePath)
            $pfxAsBase64EncodedString = [System.Convert]::ToBase64String($certContentInBytes)
    
            $jsonObject = ConvertTo-Json -Depth 10 ([pscustomobject]@{
                data     = $pfxAsBase64EncodedString
                dataType = 'pfx'
                password = $Password
            })
    
            $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
            $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
            $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
            $keyVaultSecret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $keyVaultSecretName -SecretValue $secret
            
            $pfxCertObject = Get-ThumbprintFromPfx -PfxFilePath $PfxFilePath -Password $Password
    
            Write-Host "KeyVault id: " -ForegroundColor Green
            (Get-AzureRmKeyVault -VaultName $KeyVaultName).ResourceId
            
            Write-Host "Secret Id: " -ForegroundColor Green
            (Get-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $keyVaultSecretName).id
    
            Write-Host "Cluster Certificate Thumbprint: " -ForegroundColor Green
            $pfxCertObject.Thumbprint
       }
    
    #========================== CHANGE THESE VALUES ===============================
    $armEndpoint = "https://management.local.azurestack.external"
    $tenantId = "your_tenant_ID"
    $location = "local"
    $clusterCertPfxPath = "Your_path_to_ClusterCert.pfx"
    $clusterCertPfxPassword = "Your_password_for_ClusterCert.pfx"
    #==============================================================================
    
    Add-AzureRmEnvironment -Name AzureStack -ARMEndpoint $armEndpoint
    Login-AzureRmAccount -Environment AzureStack -TenantId $tenantId
    
    $rgName = "sfvaultrg"
    Write-Host "Creating Resource Group..." -ForegroundColor Yellow
    New-AzureRmResourceGroup -Name $rgName -Location $location
    
    Write-Host "Creating Key Vault..." -ForegroundColor Yellow
    $Vault = New-AzureRmKeyVault -VaultName sfvault -ResourceGroupName $rgName -Location $location -EnabledForTemplateDeployment -EnabledForDeployment -EnabledForDiskEncryption
    
    Write-Host "Publishing certificate to Vault..." -ForegroundColor Yellow
    Publish-SecretToKeyVault -PfxFilePath $clusterCertPfxPath -Password $clusterCertPfxPassword -KeyVaultName $vault.VaultName
   ``` 


<span data-ttu-id="155a4-130">For more information, see [Manage KeyVault on Azure Stack with PowerShell](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-kv-manage-powershell).</span><span class="sxs-lookup"><span data-stu-id="155a4-130">For more information, see [Manage KeyVault on Azure Stack with PowerShell](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-kv-manage-powershell).</span></span>

## <a name="deploy-the-marketplace-item"></a><span data-ttu-id="155a4-131">Deploy the Marketplace item</span><span class="sxs-lookup"><span data-stu-id="155a4-131">Deploy the Marketplace item</span></span>

1. <span data-ttu-id="155a4-132">In the user portal, go to **New** > **Compute** > **Service Fabric Cluster**.</span><span class="sxs-lookup"><span data-stu-id="155a4-132">In the user portal, go to **New** > **Compute** > **Service Fabric Cluster**.</span></span> 

   ![Select Service Fabric Cluster](./media/azure-stack-solution-template-service-fabric-cluster/image2.png)

1. <span data-ttu-id="155a4-134">For each page, like *Basics*, fill out the deployment form.</span><span class="sxs-lookup"><span data-stu-id="155a4-134">For each page, like *Basics*, fill out the deployment form.</span></span> <span data-ttu-id="155a4-135">Use defaults if you're not sure of a value.</span><span class="sxs-lookup"><span data-stu-id="155a4-135">Use defaults if you're not sure of a value.</span></span> <span data-ttu-id="155a4-136">Select **OK** to advance to the next page:</span><span class="sxs-lookup"><span data-stu-id="155a4-136">Select **OK** to advance to the next page:</span></span>

   ![Basics](media/azure-stack-solution-template-service-fabric-cluster/image3.png)

1. <span data-ttu-id="155a4-138">On the *Network Settings* page, you can specify specific ports to open for your applications:</span><span class="sxs-lookup"><span data-stu-id="155a4-138">On the *Network Settings* page, you can specify specific ports to open for your applications:</span></span>

   ![Network Settings](media/azure-stack-solution-template-service-fabric-cluster/image4.png)

1. <span data-ttu-id="155a4-140">On the *Security* page, add the values that you got from [creating the Azure KeyVault](#add-a-secret-to-key-vault) and Uploading the Secret.</span><span class="sxs-lookup"><span data-stu-id="155a4-140">On the *Security* page, add the values that you got from [creating the Azure KeyVault](#add-a-secret-to-key-vault) and Uploading the Secret.</span></span>

   <span data-ttu-id="155a4-141">For the *Admin Client Certificate Thumbprint*, enter the thumbprint of the *Admin Client certificate*.</span><span class="sxs-lookup"><span data-stu-id="155a4-141">For the *Admin Client Certificate Thumbprint*, enter the thumbprint of the *Admin Client certificate*.</span></span> <span data-ttu-id="155a4-142">(See the [prerequisites](#prerequisites).)</span><span class="sxs-lookup"><span data-stu-id="155a4-142">(See the [prerequisites](#prerequisites).)</span></span>
   
   - <span data-ttu-id="155a4-143">Source Key Vault:  Specify entire *keyVault id* string from the script results.</span><span class="sxs-lookup"><span data-stu-id="155a4-143">Source Key Vault:  Specify entire *keyVault id* string from the script results.</span></span> 
   - <span data-ttu-id="155a4-144">Cluster Certificate URL: Specify the entire URL from the *Secret Id* from the script results.</span><span class="sxs-lookup"><span data-stu-id="155a4-144">Cluster Certificate URL: Specify the entire URL from the *Secret Id* from the script results.</span></span> 
   - <span data-ttu-id="155a4-145">Cluster Certificate thumbprint: Specify the *Cluster Certificate Thumbprint* from the script results.</span><span class="sxs-lookup"><span data-stu-id="155a4-145">Cluster Certificate thumbprint: Specify the *Cluster Certificate Thumbprint* from the script results.</span></span>
   - <span data-ttu-id="155a4-146">Admin Client Certificate Thumbprints: Specify the *Admin Client Certificate Thumbprint* you have created in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="155a4-146">Admin Client Certificate Thumbprints: Specify the *Admin Client Certificate Thumbprint* you have created in the prerequisites.</span></span> 

   ![Script output](media/azure-stack-solution-template-service-fabric-cluster/image5.png)

   ![Security](media/azure-stack-solution-template-service-fabric-cluster/image6.png)

1. <span data-ttu-id="155a4-149">Complete the wizard, and then select **Create** to deploy the Service Fabric Cluster.</span><span class="sxs-lookup"><span data-stu-id="155a4-149">Complete the wizard, and then select **Create** to deploy the Service Fabric Cluster.</span></span>



## <a name="access-the-service-fabric-cluster"></a><span data-ttu-id="155a4-150">Access the Service Fabric Cluster</span><span class="sxs-lookup"><span data-stu-id="155a4-150">Access the Service Fabric Cluster</span></span>
<span data-ttu-id="155a4-151">You can access the Service Fabric cluster by using either the Service Fabric Explorer or Service Fabric PowerShell.</span><span class="sxs-lookup"><span data-stu-id="155a4-151">You can access the Service Fabric cluster by using either the Service Fabric Explorer or Service Fabric PowerShell.</span></span>


### <a name="use-service-fabric-explorer"></a><span data-ttu-id="155a4-152">Use Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="155a4-152">Use Service Fabric Explorer</span></span>
1.  <span data-ttu-id="155a4-153">Validate that the Web browser has access to your Admin client certificate and can authenticate to your Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="155a4-153">Validate that the Web browser has access to your Admin client certificate and can authenticate to your Service Fabric cluster.</span></span>  

    <span data-ttu-id="155a4-154">a.</span><span class="sxs-lookup"><span data-stu-id="155a4-154">a.</span></span> <span data-ttu-id="155a4-155">Open Internet Explorer and go to **Internet Options** > **Content** > **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="155a4-155">Open Internet Explorer and go to **Internet Options** > **Content** > **Certificates**.</span></span>
  
    <span data-ttu-id="155a4-156">b.</span><span class="sxs-lookup"><span data-stu-id="155a4-156">b.</span></span> <span data-ttu-id="155a4-157">On Certificates, select **Import** to start the *Certificate Import Wizard*, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="155a4-157">On Certificates, select **Import** to start the *Certificate Import Wizard*, and then click **Next**.</span></span> <span data-ttu-id="155a4-158">On the *File to Import* page click **Browse**, and select the **Admin Client certificate** you provided to the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="155a4-158">On the *File to Import* page click **Browse**, and select the **Admin Client certificate** you provided to the Azure Resource Manager template.</span></span>
        
       > [!NOTE]  
       > <span data-ttu-id="155a4-159">This certificate is not the Cluster certificate that was previously added to KeyVault.</span><span class="sxs-lookup"><span data-stu-id="155a4-159">This certificate is not the Cluster certificate that was previously added to KeyVault.</span></span>  

    <span data-ttu-id="155a4-160">c.</span><span class="sxs-lookup"><span data-stu-id="155a4-160">c.</span></span> <span data-ttu-id="155a4-161">Ensure that you have “Personal Information Exchange” selected in the extension dropdown of the File Explorer window.</span><span class="sxs-lookup"><span data-stu-id="155a4-161">Ensure that you have “Personal Information Exchange” selected in the extension dropdown of the File Explorer window.</span></span>  

       ![Personal information exchange](media/azure-stack-solution-template-service-fabric-cluster/image8.png)  

    <span data-ttu-id="155a4-163">d.</span><span class="sxs-lookup"><span data-stu-id="155a4-163">d.</span></span> <span data-ttu-id="155a4-164">On the *Certificate Store* page, select **Personal**, and then complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="155a4-164">On the *Certificate Store* page, select **Personal**, and then complete the wizard.</span></span>  
       <span data-ttu-id="155a4-165">![Certificate store](media/azure-stack-solution-template-service-fabric-cluster/image9.png)</span><span class="sxs-lookup"><span data-stu-id="155a4-165">![Certificate store](media/azure-stack-solution-template-service-fabric-cluster/image9.png)</span></span>  
1. <span data-ttu-id="155a4-166">To find the FQDN of your Service Fabric cluster:</span><span class="sxs-lookup"><span data-stu-id="155a4-166">To find the FQDN of your Service Fabric cluster:</span></span>  

    <span data-ttu-id="155a4-167">a.</span><span class="sxs-lookup"><span data-stu-id="155a4-167">a.</span></span> <span data-ttu-id="155a4-168">Go to the resource group that is associated with your Service Fabric cluster and locate the *Public IP address* resource.</span><span class="sxs-lookup"><span data-stu-id="155a4-168">Go to the resource group that is associated with your Service Fabric cluster and locate the *Public IP address* resource.</span></span> <span data-ttu-id="155a4-169">Select the object associated with the Public IP address to open the *Public IP address* blade.</span><span class="sxs-lookup"><span data-stu-id="155a4-169">Select the object associated with the Public IP address to open the *Public IP address* blade.</span></span>  

      ![Public IP address](media/azure-stack-solution-template-service-fabric-cluster/image10.png)   

    <span data-ttu-id="155a4-171">b.</span><span class="sxs-lookup"><span data-stu-id="155a4-171">b.</span></span> <span data-ttu-id="155a4-172">On the Public IP address blade, the FQDN displays as *DNS name*.</span><span class="sxs-lookup"><span data-stu-id="155a4-172">On the Public IP address blade, the FQDN displays as *DNS name*.</span></span>  

      ![DNS name](media/azure-stack-solution-template-service-fabric-cluster/image11.png)  

1. <span data-ttu-id="155a4-174">To find the URL for the Service Fabric Explorer, and the Client connection endpoint, review the results of the Template deployment.</span><span class="sxs-lookup"><span data-stu-id="155a4-174">To find the URL for the Service Fabric Explorer, and the Client connection endpoint, review the results of the Template deployment.</span></span>

1. <span data-ttu-id="155a4-175">In your browser, go to https://*FQDN*:19080.</span><span class="sxs-lookup"><span data-stu-id="155a4-175">In your browser, go to https://*FQDN*:19080.</span></span> <span data-ttu-id="155a4-176">Replace *FQDN* with the FQDN of your Service Fabric cluster from step 2.</span><span class="sxs-lookup"><span data-stu-id="155a4-176">Replace *FQDN* with the FQDN of your Service Fabric cluster from step 2.</span></span>   
   <span data-ttu-id="155a4-177">If you’ve used a self signed certificate, you’ll get a warning that the connection is not secure.</span><span class="sxs-lookup"><span data-stu-id="155a4-177">If you’ve used a self signed certificate, you’ll get a warning that the connection is not secure.</span></span> <span data-ttu-id="155a4-178">To proceed to the web site, select **More Information**, and then **Go on to the webpage**.</span><span class="sxs-lookup"><span data-stu-id="155a4-178">To proceed to the web site, select **More Information**, and then **Go on to the webpage**.</span></span> 

1. <span data-ttu-id="155a4-179">To authenticate to the site you must select a certificate to use.</span><span class="sxs-lookup"><span data-stu-id="155a4-179">To authenticate to the site you must select a certificate to use.</span></span> <span data-ttu-id="155a4-180">Select **More choices**, pick the appropriate certificate, and then click **OK** to connect to the Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="155a4-180">Select **More choices**, pick the appropriate certificate, and then click **OK** to connect to the Service Fabric Explorer.</span></span> 

   ![Authenticate](media/azure-stack-solution-template-service-fabric-cluster/image14.png)



## <a name="use-service-fabric-powershell"></a><span data-ttu-id="155a4-182">Use Service Fabric PowerShell</span><span class="sxs-lookup"><span data-stu-id="155a4-182">Use Service Fabric PowerShell</span></span>

1. <span data-ttu-id="155a4-183">Install the *Microsoft Azure Service Fabric SDK* from [Prepare your development environment on Windows](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started#install-the-sdk-and-tools) in the Azure Service Fabric documentation.</span><span class="sxs-lookup"><span data-stu-id="155a4-183">Install the *Microsoft Azure Service Fabric SDK* from [Prepare your development environment on Windows](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started#install-the-sdk-and-tools) in the Azure Service Fabric documentation.</span></span>  

1. <span data-ttu-id="155a4-184">After the installation is complete, configure the system Environment variables to ensure that the Service Fabric cmdlets are accessible from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="155a4-184">After the installation is complete, configure the system Environment variables to ensure that the Service Fabric cmdlets are accessible from PowerShell.</span></span>  
    
    <span data-ttu-id="155a4-185">a.</span><span class="sxs-lookup"><span data-stu-id="155a4-185">a.</span></span> <span data-ttu-id="155a4-186">Go to **Control Panel** > **System and Security** > **System**, and then select **Advanced system settings**.</span><span class="sxs-lookup"><span data-stu-id="155a4-186">Go to **Control Panel** > **System and Security** > **System**, and then select **Advanced system settings**.</span></span>  
    
      ![Control panel](media/azure-stack-solution-template-service-fabric-cluster/image15.png) 

    <span data-ttu-id="155a4-188">b.</span><span class="sxs-lookup"><span data-stu-id="155a4-188">b.</span></span> <span data-ttu-id="155a4-189">On the **Advanced** tab of *System Properties*, select **Environment Variables**.</span><span class="sxs-lookup"><span data-stu-id="155a4-189">On the **Advanced** tab of *System Properties*, select **Environment Variables**.</span></span>  

    <span data-ttu-id="155a4-190">c.</span><span class="sxs-lookup"><span data-stu-id="155a4-190">c.</span></span> <span data-ttu-id="155a4-191">For *System variables*, edit **Path** and make sure that **C:\\Program Files\\Microsoft Service Fabric\\bin\\Fabric\\Fabric.Code** is at the top of the list of environment variables.</span><span class="sxs-lookup"><span data-stu-id="155a4-191">For *System variables*, edit **Path** and make sure that **C:\\Program Files\\Microsoft Service Fabric\\bin\\Fabric\\Fabric.Code** is at the top of the list of environment variables.</span></span>  

      ![Environment variable list](media/azure-stack-solution-template-service-fabric-cluster/image16.png)

1. <span data-ttu-id="155a4-193">After changing the order of the environment variables, restart PowerShell and then run the following PowerShell script to gain access to the Service Fabric cluster:</span><span class="sxs-lookup"><span data-stu-id="155a4-193">After changing the order of the environment variables, restart PowerShell and then run the following PowerShell script to gain access to the Service Fabric cluster:</span></span>

   ````PowerShell  
    Connect-ServiceFabricCluster -ConnectionEndpoint "\[Service Fabric
    CLUSTER FQDN\]:19000" \`

    -X509Credential -ServerCertThumbprint
    761A0D17B030723A37AA2E08225CD7EA8BE9F86A \`

    -FindType FindByThumbprint -FindValue
    0272251171BA32CEC7938A65B8A6A553AA2D3283 \`

    -StoreLocation CurrentUser -StoreName My -Verbose
   ````
   
   > [!NOTE]  
   > <span data-ttu-id="155a4-194">There is no *https://* before the name of the cluster in the script.</span><span class="sxs-lookup"><span data-stu-id="155a4-194">There is no *https://* before the name of the cluster in the script.</span></span> <span data-ttu-id="155a4-195">Port 19000 is required.</span><span class="sxs-lookup"><span data-stu-id="155a4-195">Port 19000 is required.</span></span>
 
