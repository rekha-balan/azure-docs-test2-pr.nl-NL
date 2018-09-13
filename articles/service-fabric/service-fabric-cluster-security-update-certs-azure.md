---
title: Manage certificates in an Azure Service Fabric cluster | Microsoft Docs
description: Describes how to add new certificates, rollover certificate, and remove certificate to or from a Service Fabric cluster.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: ''
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/23/2018
ms.author: chackdan
ms.openlocfilehash: a1cfd68b526d8ce63fcfbc3b6e0eac84926fabaa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825411"
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="27e94-103">Add or remove certificates for a Service Fabric cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="27e94-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="27e94-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="27e94-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="27e94-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span><span class="sxs-lookup"><span data-stu-id="27e94-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="27e94-106">Azure Service Fabrics SDK's default certificate load behavior, is to deploy and use a defined certificate with an expiring date furthest into the future; regardless of their primary or secondary configuration definition.</span><span class="sxs-lookup"><span data-stu-id="27e94-106">Azure Service Fabrics SDK's default certificate load behavior, is to deploy and use a defined certificate with an expiring date furthest into the future; regardless of their primary or secondary configuration definition.</span></span> <span data-ttu-id="27e94-107">Falling back to the classic behavior is a non recommended advanced action, and requires setting the "UseSecondaryIfNever" setting parameter value to false within your Fabric.Code configuration.</span><span class="sxs-lookup"><span data-stu-id="27e94-107">Falling back to the classic behavior is a non recommended advanced action, and requires setting the "UseSecondaryIfNever" setting parameter value to false within your Fabric.Code configuration.</span></span>

<span data-ttu-id="27e94-108">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span><span class="sxs-lookup"><span data-stu-id="27e94-108">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span></span> <span data-ttu-id="27e94-109">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span><span class="sxs-lookup"><span data-stu-id="27e94-109">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="27e94-110">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span><span class="sxs-lookup"><span data-stu-id="27e94-110">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span></span> <span data-ttu-id="27e94-111">After cluster creation, you can add a new certificate as a secondary.</span><span class="sxs-lookup"><span data-stu-id="27e94-111">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="27e94-112">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span><span class="sxs-lookup"><span data-stu-id="27e94-112">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span></span> <span data-ttu-id="27e94-113">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span><span class="sxs-lookup"><span data-stu-id="27e94-113">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span></span> <span data-ttu-id="27e94-114">There is currently no email or any other notification that Service Fabric sends out on this article.</span><span class="sxs-lookup"><span data-stu-id="27e94-114">There is currently no email or any other notification that Service Fabric sends out on this article.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a><span data-ttu-id="27e94-115">Add a secondary cluster certificate using the portal</span><span class="sxs-lookup"><span data-stu-id="27e94-115">Add a secondary cluster certificate using the portal</span></span>
<span data-ttu-id="27e94-116">Secondary cluster certificate cannot be added through the Azure portal, use Azure powershell.</span><span class="sxs-lookup"><span data-stu-id="27e94-116">Secondary cluster certificate cannot be added through the Azure portal, use Azure powershell.</span></span> <span data-ttu-id="27e94-117">The process is outlined later in this document.</span><span class="sxs-lookup"><span data-stu-id="27e94-117">The process is outlined later in this document.</span></span>

## <a name="remove-a-cluster-certificate-using-the-portal"></a><span data-ttu-id="27e94-118">Remove a cluster certificate using the portal</span><span class="sxs-lookup"><span data-stu-id="27e94-118">Remove a cluster certificate using the portal</span></span>
<span data-ttu-id="27e94-119">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate.</span><span class="sxs-lookup"><span data-stu-id="27e94-119">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate.</span></span> <span data-ttu-id="27e94-120">The certificate deployed with the furthest into the future expiring date will be in use, and removing it will make your cluster stop functioning; ensure to only remove the certificate that is expired, or a unused certificate that expires the soonest.</span><span class="sxs-lookup"><span data-stu-id="27e94-120">The certificate deployed with the furthest into the future expiring date will be in use, and removing it will make your cluster stop functioning; ensure to only remove the certificate that is expired, or a unused certificate that expires the soonest.</span></span>

<span data-ttu-id="27e94-121">To remove an unused cluster security certificate, Navigate to the Security section and select the 'Delete' option from the context menu on the unused certificate.</span><span class="sxs-lookup"><span data-stu-id="27e94-121">To remove an unused cluster security certificate, Navigate to the Security section and select the 'Delete' option from the context menu on the unused certificate.</span></span>

<span data-ttu-id="27e94-122">If your intent is to remove the certificate that is marked primary, then you will need to deploy a secondary certificate with an expiring date further into the future than the primary certificate, enabling the auto rollover behavior; delete the primary certificate after the auto rollover has completed.</span><span class="sxs-lookup"><span data-stu-id="27e94-122">If your intent is to remove the certificate that is marked primary, then you will need to deploy a secondary certificate with an expiring date further into the future than the primary certificate, enabling the auto rollover behavior; delete the primary certificate after the auto rollover has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="27e94-123">Add a secondary certificate using Resource Manager Powershell</span><span class="sxs-lookup"><span data-stu-id="27e94-123">Add a secondary certificate using Resource Manager Powershell</span></span>
> [!TIP]
> <span data-ttu-id="27e94-124">It is now better and easier way to add a secondary certificate using the [Add-AzureRmServiceFabricClusterCertificate](/powershell/module/azurerm.servicefabric/add-azurermservicefabricclustercertificate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="27e94-124">It is now better and easier way to add a secondary certificate using the [Add-AzureRmServiceFabricClusterCertificate](/powershell/module/azurerm.servicefabric/add-azurermservicefabricclustercertificate) cmdlet.</span></span> <span data-ttu-id="27e94-125">You don't need to follow the rest of the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="27e94-125">You don't need to follow the rest of the steps in this section.</span></span>  <span data-ttu-id="27e94-126">Also, you do not need the template originally used to create and deploy the cluster when using the [Add-AzureRmServiceFabricClusterCertificate](/powershell/module/azurerm.servicefabric/add-azurermservicefabricclustercertificate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="27e94-126">Also, you do not need the template originally used to create and deploy the cluster when using the [Add-AzureRmServiceFabricClusterCertificate](/powershell/module/azurerm.servicefabric/add-azurermservicefabricclustercertificate) cmdlet.</span></span>

<span data-ttu-id="27e94-127">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span><span class="sxs-lookup"><span data-stu-id="27e94-127">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span></span> <span data-ttu-id="27e94-128">It is also assumed that you are comfortable using JSON.</span><span class="sxs-lookup"><span data-stu-id="27e94-128">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="27e94-129">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="27e94-129">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="27e94-130">Edit your Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="27e94-130">Edit your Resource Manager template</span></span>

<span data-ttu-id="27e94-131">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span><span class="sxs-lookup"><span data-stu-id="27e94-131">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span></span> <span data-ttu-id="27e94-132">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="27e94-132">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="27e94-133">**Make sure to follow all the steps**</span><span class="sxs-lookup"><span data-stu-id="27e94-133">**Make sure to follow all the steps**</span></span>

1. <span data-ttu-id="27e94-134">Open up the Resource Manager template you used to deploy you Cluster.</span><span class="sxs-lookup"><span data-stu-id="27e94-134">Open up the Resource Manager template you used to deploy you Cluster.</span></span> <span data-ttu-id="27e94-135">(If you have downloaded the sample from the preceding repo, then use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span><span class="sxs-lookup"><span data-stu-id="27e94-135">(If you have downloaded the sample from the preceding repo, then use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span></span>

2. <span data-ttu-id="27e94-136">Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span><span class="sxs-lookup"><span data-stu-id="27e94-136">Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span></span> <span data-ttu-id="27e94-137">You can copy the following code snippet and add it to the template.</span><span class="sxs-lookup"><span data-stu-id="27e94-137">You can copy the following code snippet and add it to the template.</span></span> <span data-ttu-id="27e94-138">Depending on the source of your template, you may already have these defined, if so move to the next step.</span><span class="sxs-lookup"><span data-stu-id="27e94-138">Depending on the source of your template, you may already have these defined, if so move to the next step.</span></span> 
 
    ```json
       "secCertificateThumbprint": {
          "type": "string",
          "metadata": {
            "description": "Certificate Thumbprint"
          }
        },
        "secCertificateUrlValue": {
          "type": "string",
          "metadata": {
            "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
          }
        },
    
    ```

3. <span data-ttu-id="27e94-139">Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span><span class="sxs-lookup"><span data-stu-id="27e94-139">Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="27e94-140">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="27e94-140">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span></span>
   
    ```JSON
          "properties": {
            "certificate": {
              "thumbprint": "[parameters('certificateThumbprint')]",
              "x509StoreName": "[parameters('certificateStoreValue')]"
         }
    ``` 

    <span data-ttu-id="27e94-141">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span><span class="sxs-lookup"><span data-stu-id="27e94-141">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

    <span data-ttu-id="27e94-142">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span><span class="sxs-lookup"><span data-stu-id="27e94-142">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span></span> 

    ```JSON
          "properties": {
            "certificate": {
              "thumbprint": "[parameters('certificateThumbprint')]",
              "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
              "x509StoreName": "[parameters('certificateStoreValue')]"
         }
    ``` 

    <span data-ttu-id="27e94-143">If you want to **roll over the cert**, then specify the new cert as primary and moving the current primary as secondary.</span><span class="sxs-lookup"><span data-stu-id="27e94-143">If you want to **roll over the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="27e94-144">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span><span class="sxs-lookup"><span data-stu-id="27e94-144">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span></span>
    
    ```JSON
          "properties": {
            "certificate": {
              "thumbprint": "[parameters('secCertificateThumbprint')]",
              "thumbprintSecondary": "[parameters('certificateThumbprint')]",
              "x509StoreName": "[parameters('certificateStoreValue')]"
         }
    ``` 

4. <span data-ttu-id="27e94-145">Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span><span class="sxs-lookup"><span data-stu-id="27e94-145">Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="27e94-146">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="27e94-146">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

    <span data-ttu-id="27e94-147">In the Service Fabric publisher settings, you should see something like this.</span><span class="sxs-lookup"><span data-stu-id="27e94-147">In the Service Fabric publisher settings, you should see something like this.</span></span>
    
    ![Json_Pub_Setting1][Json_Pub_Setting1]
    
    <span data-ttu-id="27e94-149">Add the new cert entries to it</span><span class="sxs-lookup"><span data-stu-id="27e94-149">Add the new cert entries to it</span></span>
    
    ```json
                   "certificateSecondary": {
                        "thumbprint": "[parameters('secCertificateThumbprint')]",
                        "x509StoreName": "[parameters('certificateStoreValue')]"
                        }
                      },
    
    ```

    <span data-ttu-id="27e94-150">The properties should now look like this</span><span class="sxs-lookup"><span data-stu-id="27e94-150">The properties should now look like this</span></span>
    
    ![Json_Pub_Setting2][Json_Pub_Setting2]
    
    <span data-ttu-id="27e94-152">If you want to **roll over the cert**, then specify the new cert as primary and moving the current primary as secondary.</span><span class="sxs-lookup"><span data-stu-id="27e94-152">If you want to **roll over the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="27e94-153">This results in the rollover of your current certificate to the new certificate in one deployment step.</span><span class="sxs-lookup"><span data-stu-id="27e94-153">This results in the rollover of your current certificate to the new certificate in one deployment step.</span></span>     

    ```json
                   "certificate": {
                       "thumbprint": "[parameters('secCertificateThumbprint')]",
                       "x509StoreName": "[parameters('certificateStoreValue')]"
                         },
                   "certificateSecondary": {
                        "thumbprint": "[parameters('certificateThumbprint')]",
                        "x509StoreName": "[parameters('certificateStoreValue')]"
                        }
                      },
    ```

    <span data-ttu-id="27e94-154">The properties should now look like this</span><span class="sxs-lookup"><span data-stu-id="27e94-154">The properties should now look like this</span></span>    
    ![Json_Pub_Setting3][Json_Pub_Setting3]

5. <span data-ttu-id="27e94-156">Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span><span class="sxs-lookup"><span data-stu-id="27e94-156">Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="27e94-157">Scroll to the "vaultCertificates": , under "OSProfile".</span><span class="sxs-lookup"><span data-stu-id="27e94-157">Scroll to the "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="27e94-158">it should look something like this.</span><span class="sxs-lookup"><span data-stu-id="27e94-158">it should look something like this.</span></span>

    ![Json_Pub_Setting4][Json_Pub_Setting4]
    
    <span data-ttu-id="27e94-160">Add the secCertificateUrlValue to it.</span><span class="sxs-lookup"><span data-stu-id="27e94-160">Add the secCertificateUrlValue to it.</span></span> <span data-ttu-id="27e94-161">use the following snippet:</span><span class="sxs-lookup"><span data-stu-id="27e94-161">use the following snippet:</span></span>
    
    ```json
                      {
                        "certificateStore": "[parameters('certificateStoreValue')]",
                        "certificateUrl": "[parameters('secCertificateUrlValue')]"
                      }
    
    ```
    <span data-ttu-id="27e94-162">Now the resulting Json should look something like this.</span><span class="sxs-lookup"><span data-stu-id="27e94-162">Now the resulting Json should look something like this.</span></span>
    <span data-ttu-id="27e94-163">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="27e94-163">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="27e94-164">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span><span class="sxs-lookup"><span data-stu-id="27e94-164">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="27e94-165">If you miss one of them, the certificate will not get installed on that virtual machine scale set and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span><span class="sxs-lookup"><span data-stu-id="27e94-165">If you miss one of them, the certificate will not get installed on that virtual machine scale set and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span></span> <span data-ttu-id="27e94-166">So double check, before proceeding further.</span><span class="sxs-lookup"><span data-stu-id="27e94-166">So double check, before proceeding further.</span></span>
> 
> 

### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a><span data-ttu-id="27e94-167">Edit your template file to reflect the new parameters you added above</span><span class="sxs-lookup"><span data-stu-id="27e94-167">Edit your template file to reflect the new parameters you added above</span></span>
<span data-ttu-id="27e94-168">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="27e94-168">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="27e94-169">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="27e94-169">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a><span data-ttu-id="27e94-170">Deploy the template to Azure</span><span class="sxs-lookup"><span data-stu-id="27e94-170">Deploy the template to Azure</span></span>

- <span data-ttu-id="27e94-171">You are now ready to deploy your template to Azure.</span><span class="sxs-lookup"><span data-stu-id="27e94-171">You are now ready to deploy your template to Azure.</span></span> <span data-ttu-id="27e94-172">Open an Azure PS version 1+ command prompt.</span><span class="sxs-lookup"><span data-stu-id="27e94-172">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="27e94-173">Log in to your Azure Account and select the specific azure subscription.</span><span class="sxs-lookup"><span data-stu-id="27e94-173">Log in to your Azure Account and select the specific azure subscription.</span></span> <span data-ttu-id="27e94-174">This is an important step for folks who have access to more than one azure subscription.</span><span class="sxs-lookup"><span data-stu-id="27e94-174">This is an important step for folks who have access to more than one azure subscription.</span></span>

```powershell
Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="27e94-175">Test the template prior to deploying it.</span><span class="sxs-lookup"><span data-stu-id="27e94-175">Test the template prior to deploying it.</span></span> <span data-ttu-id="27e94-176">Use the same Resource Group that your cluster is currently deployed to.</span><span class="sxs-lookup"><span data-stu-id="27e94-176">Use the same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="27e94-177">Deploy the template to your resource group.</span><span class="sxs-lookup"><span data-stu-id="27e94-177">Deploy the template to your resource group.</span></span> <span data-ttu-id="27e94-178">Use the same Resource Group that your cluster is currently deployed to.</span><span class="sxs-lookup"><span data-stu-id="27e94-178">Use the same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="27e94-179">Run the New-AzureRmResourceGroupDeployment command.</span><span class="sxs-lookup"><span data-stu-id="27e94-179">Run the New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="27e94-180">You do not need to specify the mode, since the default value is **incremental**.</span><span class="sxs-lookup"><span data-stu-id="27e94-180">You do not need to specify the mode, since the default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="27e94-181">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span><span class="sxs-lookup"><span data-stu-id="27e94-181">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="27e94-182">So do not use it in this scenario.</span><span class="sxs-lookup"><span data-stu-id="27e94-182">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="27e94-183">Here is a filled out example of the same powershell.</span><span class="sxs-lookup"><span data-stu-id="27e94-183">Here is a filled out example of the same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="27e94-184">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span><span class="sxs-lookup"><span data-stu-id="27e94-184">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span></span> <span data-ttu-id="27e94-185">If you are able to do.</span><span class="sxs-lookup"><span data-stu-id="27e94-185">If you are able to do.</span></span> <span data-ttu-id="27e94-186">Then you can delete the old certificate.</span><span class="sxs-lookup"><span data-stu-id="27e94-186">Then you can delete the old certificate.</span></span> 

<span data-ttu-id="27e94-187">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span><span class="sxs-lookup"><span data-stu-id="27e94-187">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="27e94-188">For quick reference here is the command to connect to a secure cluster</span><span class="sxs-lookup"><span data-stu-id="27e94-188">For quick reference here is the command to connect to a secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="27e94-189">For quick reference here is the command to get cluster health</span><span class="sxs-lookup"><span data-stu-id="27e94-189">For quick reference here is the command to get cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a><span data-ttu-id="27e94-190">Deploying Application certificates to the cluster.</span><span class="sxs-lookup"><span data-stu-id="27e94-190">Deploying Application certificates to the cluster.</span></span>

<span data-ttu-id="27e94-191">You can use the same steps as outlined in the preceding Steps 5 to have the certificates deployed from a keyvault to the Nodes.</span><span class="sxs-lookup"><span data-stu-id="27e94-191">You can use the same steps as outlined in the preceding Steps 5 to have the certificates deployed from a keyvault to the Nodes.</span></span> <span data-ttu-id="27e94-192">You just need define and use different parameters.</span><span class="sxs-lookup"><span data-stu-id="27e94-192">You just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="27e94-193">Adding or removing Client certificates</span><span class="sxs-lookup"><span data-stu-id="27e94-193">Adding or removing Client certificates</span></span>

<span data-ttu-id="27e94-194">In addition to the cluster certificates, you can add client certificates to perform management operations on a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="27e94-194">In addition to the cluster certificates, you can add client certificates to perform management operations on a Service Fabric cluster.</span></span>

<span data-ttu-id="27e94-195">You can add two kinds of client certificates - Admin or Read-only.</span><span class="sxs-lookup"><span data-stu-id="27e94-195">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="27e94-196">These then can be used to control access to the admin operations and Query operations on the cluster.</span><span class="sxs-lookup"><span data-stu-id="27e94-196">These then can be used to control access to the admin operations and Query operations on the cluster.</span></span> <span data-ttu-id="27e94-197">By default, the cluster certificates are added to the allowed Admin certificates list.</span><span class="sxs-lookup"><span data-stu-id="27e94-197">By default, the cluster certificates are added to the allowed Admin certificates list.</span></span>

<span data-ttu-id="27e94-198">you can specify any number of client certificates.</span><span class="sxs-lookup"><span data-stu-id="27e94-198">you can specify any number of client certificates.</span></span> <span data-ttu-id="27e94-199">Each addition/deletion results in a configuration update to the Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="27e94-199">Each addition/deletion results in a configuration update to the Service Fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="27e94-200">Adding client certificates - Admin or Read-Only via portal</span><span class="sxs-lookup"><span data-stu-id="27e94-200">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="27e94-201">Navigate to the Security section, and select the '+ Authentication' button on top of the security section.</span><span class="sxs-lookup"><span data-stu-id="27e94-201">Navigate to the Security section, and select the '+ Authentication' button on top of the security section.</span></span>
2. <span data-ttu-id="27e94-202">On the 'Add Authentication' section, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span><span class="sxs-lookup"><span data-stu-id="27e94-202">On the 'Add Authentication' section, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="27e94-203">Now choose the Authorization method.</span><span class="sxs-lookup"><span data-stu-id="27e94-203">Now choose the Authorization method.</span></span> <span data-ttu-id="27e94-204">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span><span class="sxs-lookup"><span data-stu-id="27e94-204">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span></span> <span data-ttu-id="27e94-205">In general, it is not a good security practice to use the authorization method of subject name.</span><span class="sxs-lookup"><span data-stu-id="27e94-205">In general, it is not a good security practice to use the authorization method of subject name.</span></span> 

![Add Client certificate][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a><span data-ttu-id="27e94-207">Deletion of Client Certificates - Admin or Read-Only using the portal</span><span class="sxs-lookup"><span data-stu-id="27e94-207">Deletion of Client Certificates - Admin or Read-Only using the portal</span></span>

<span data-ttu-id="27e94-208">To remove a secondary certificate from being used for cluster security, Navigate to the Security section and select the 'Delete' option from the context menu on the specific certificate.</span><span class="sxs-lookup"><span data-stu-id="27e94-208">To remove a secondary certificate from being used for cluster security, Navigate to the Security section and select the 'Delete' option from the context menu on the specific certificate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27e94-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="27e94-209">Next steps</span></span>
<span data-ttu-id="27e94-210">Read these articles for more information on cluster management:</span><span class="sxs-lookup"><span data-stu-id="27e94-210">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="27e94-211">Service Fabric Cluster upgrade process and expectations from you</span><span class="sxs-lookup"><span data-stu-id="27e94-211">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="27e94-212">Setup role-based access for clients</span><span class="sxs-lookup"><span data-stu-id="27e94-212">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


