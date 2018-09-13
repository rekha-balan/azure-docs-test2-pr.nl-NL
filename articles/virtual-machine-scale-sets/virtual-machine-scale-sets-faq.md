---
title: Azure virtual machine scale sets FAQs | Microsoft Docs
description: Get answers to frequently asked questions about virtual machine scale sets.
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/10/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 1c7b4c4b7675bfc33e102c9abb4f942a1dd33ad4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554958"
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="64e8f-103">Azure virtual machine scale sets FAQs</span><span class="sxs-lookup"><span data-stu-id="64e8f-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="64e8f-104">Get answers to frequently asked questions about virtual machine scale sets in Azure.</span><span class="sxs-lookup"><span data-stu-id="64e8f-104">Get answers to frequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="64e8f-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="64e8f-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="64e8f-106">What are best practices for Azure Autoscale?</span><span class="sxs-lookup"><span data-stu-id="64e8f-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="64e8f-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="64e8f-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="64e8f-108">Where do I find metric names for autoscaling that uses host-based metrics?</span><span class="sxs-lookup"><span data-stu-id="64e8f-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="64e8f-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="64e8f-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span><span class="sxs-lookup"><span data-stu-id="64e8f-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="64e8f-111">Yes.</span><span class="sxs-lookup"><span data-stu-id="64e8f-111">Yes.</span></span> <span data-ttu-id="64e8f-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="64e8f-113">For a Service Bus queue, use the following JSON:</span><span class="sxs-lookup"><span data-stu-id="64e8f-113">For a Service Bus queue, use the following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="64e8f-114">For a storage queue, use the following JSON:</span><span class="sxs-lookup"><span data-stu-id="64e8f-114">For a storage queue, use the following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="64e8f-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span><span class="sxs-lookup"><span data-stu-id="64e8f-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="64e8f-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span><span class="sxs-lookup"><span data-stu-id="64e8f-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="64e8f-117">You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.</span><span class="sxs-lookup"><span data-stu-id="64e8f-117">You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="64e8f-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="64e8f-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="64e8f-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="64e8f-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="64e8f-120">The sample uses the host-level CPU metric and a message count metric.</span><span class="sxs-lookup"><span data-stu-id="64e8f-120">The sample uses the host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-121">How do I set alert rules on a virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="64e8f-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="64e8f-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="64e8f-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="64e8f-124">The TargetResourceId of the virtual machine scale set looks like this:</span><span class="sxs-lookup"><span data-stu-id="64e8f-124">The TargetResourceId of the virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="64e8f-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="64e8f-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="64e8f-126">You can choose any VM performance counter as the metric to set an alert for.</span><span class="sxs-lookup"><span data-stu-id="64e8f-126">You can choose any VM performance counter as the metric to set an alert for.</span></span> <span data-ttu-id="64e8f-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span><span class="sxs-lookup"><span data-stu-id="64e8f-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="64e8f-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span><span class="sxs-lookup"><span data-stu-id="64e8f-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="64e8f-129">To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-129">To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="64e8f-130">Certificates</span><span class="sxs-lookup"><span data-stu-id="64e8f-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-to-the-vm-how-do-i-provision-a-virtual-machine-scale-set-to-run-a-website-where-the-ssl-for-the-website-is-shipped-securely-from-a-certificate-configuration-the-common-certificate-rotation-operation-would-be-almost-the-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-to-do-this"></a><span data-ttu-id="64e8f-131">How do I securely ship a certificate to the VM?</span><span class="sxs-lookup"><span data-stu-id="64e8f-131">How do I securely ship a certificate to the VM?</span></span> <span data-ttu-id="64e8f-132">How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration?</span><span class="sxs-lookup"><span data-stu-id="64e8f-132">How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="64e8f-133">(The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this?</span><span class="sxs-lookup"><span data-stu-id="64e8f-133">(The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this?</span></span> 

<span data-ttu-id="64e8f-134">To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.</span><span class="sxs-lookup"><span data-stu-id="64e8f-134">To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.</span></span>

<span data-ttu-id="64e8f-135">Use the following JSON:</span><span class="sxs-lookup"><span data-stu-id="64e8f-135">Use the following JSON:</span></span>

```json
        "secrets": [ {
              "sourceVault": {
                      "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
          },
          "vaultCertificates": [ {
                      "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                  "certificateStore": "certificateStoreName"
          } ]
        } ]
```

<span data-ttu-id="64e8f-136">The code supports Windows and Linux.</span><span class="sxs-lookup"><span data-stu-id="64e8f-136">The code supports Windows and Linux.</span></span>

<span data-ttu-id="64e8f-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="64e8f-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="64e8f-138">Example of Self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="64e8f-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="64e8f-139">Create a self-signed certificate in a key vault.</span><span class="sxs-lookup"><span data-stu-id="64e8f-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="64e8f-140">Use the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="64e8f-140">Use the following PowerShell commands:</span></span>

  ```powershell
  Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

  Login-AzureRmAccount

  Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
  ```

  <span data-ttu-id="64e8f-141">This command gives you the input for the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="64e8f-141">This command gives you the input for the Azure Resource Manager template.</span></span>

  <span data-ttu-id="64e8f-142">For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-142">For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="64e8f-143">Change the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="64e8f-143">Change the Resource Manager template.</span></span>

  <span data-ttu-id="64e8f-144">Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:</span><span class="sxs-lookup"><span data-stu-id="64e8f-144">Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:</span></span>

  ```json 
  "osProfile": {
              "computerNamePrefix": "[variables('namingInfix')]",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]",
              "secrets": [
                {
                  "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                  },
                  "vaultCertificates": [
                    {
                      "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                      "certificateStore": "My"
                    }
                  ]
                }
              ]
            }
  ```
  

### <a name="can-i-specify-an-ssh-key-pair-to-use-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="64e8f-145">Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span><span class="sxs-lookup"><span data-stu-id="64e8f-145">Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="64e8f-146">Yes.</span><span class="sxs-lookup"><span data-stu-id="64e8f-146">Yes.</span></span> <span data-ttu-id="64e8f-147">The REST API for **osProfile** is similar to the standard VM REST API.</span><span class="sxs-lookup"><span data-stu-id="64e8f-147">The REST API for **osProfile** is similar to the standard VM REST API.</span></span> 

<span data-ttu-id="64e8f-148">Include **osProfile** in your template:</span><span class="sxs-lookup"><span data-stu-id="64e8f-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
          "computerName": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUserName')]",
          "linuxConfiguration": {
            "disablePasswordAuthentication": "true",
            "ssh": {
              "publicKeys": [
                {
                  "path": "[variables('sshKeyPath')]",
                  "keyData": "[parameters('sshKeyData')]"
                }
              ]
            }
          }
        }
```
 
<span data-ttu-id="64e8f-149">This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="64e8f-149">This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="64e8f-150">The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="64e8f-150">The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="64e8f-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="64e8f-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="64e8f-152">How do I remove deprecated certificates?</span><span class="sxs-lookup"><span data-stu-id="64e8f-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="64e8f-153">To remove deprecated certificates, remove the old certificate from the vault certificates list.</span><span class="sxs-lookup"><span data-stu-id="64e8f-153">To remove deprecated certificates, remove the old certificate from the vault certificates list.</span></span> <span data-ttu-id="64e8f-154">Leave all the certificates that you want to remain on your computer in the list.</span><span class="sxs-lookup"><span data-stu-id="64e8f-154">Leave all the certificates that you want to remain on your computer in the list.</span></span> <span data-ttu-id="64e8f-155">This does not remove the certificate from all your VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-155">This does not remove the certificate from all your VMs.</span></span> <span data-ttu-id="64e8f-156">It also does not add the certificate to new VMs that are created in the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="64e8f-156">It also does not add the certificate to new VMs that are created in the virtual machine scale set.</span></span> 

<span data-ttu-id="64e8f-157">To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.</span><span class="sxs-lookup"><span data-stu-id="64e8f-157">To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-the-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-to-store-the-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="64e8f-158">How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning?</span><span class="sxs-lookup"><span data-stu-id="64e8f-158">How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="64e8f-159">I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="64e8f-159">I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="64e8f-160">If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="64e8f-160">If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault.</span></span> <span data-ttu-id="64e8f-161">Public keys are not secret.</span><span class="sxs-lookup"><span data-stu-id="64e8f-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="64e8f-162">You can provide SSH public keys in plain text when you create a Linux VM:</span><span class="sxs-lookup"><span data-stu-id="64e8f-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {  
          "ssh": {  
            "publicKeys": [ {  
              "path": "path",
              "keyData": "publickey"
            } ]
          }
```
 
<span data-ttu-id="64e8f-163">linuxConfiguration element name</span><span class="sxs-lookup"><span data-stu-id="64e8f-163">linuxConfiguration element name</span></span> | <span data-ttu-id="64e8f-164">Required</span><span class="sxs-lookup"><span data-stu-id="64e8f-164">Required</span></span> | <span data-ttu-id="64e8f-165">Type</span><span class="sxs-lookup"><span data-stu-id="64e8f-165">Type</span></span> | <span data-ttu-id="64e8f-166">Description</span><span class="sxs-lookup"><span data-stu-id="64e8f-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="64e8f-167">ssh</span><span class="sxs-lookup"><span data-stu-id="64e8f-167">ssh</span></span> | <span data-ttu-id="64e8f-168">No</span><span class="sxs-lookup"><span data-stu-id="64e8f-168">No</span></span> | <span data-ttu-id="64e8f-169">Collection</span><span class="sxs-lookup"><span data-stu-id="64e8f-169">Collection</span></span> | <span data-ttu-id="64e8f-170">Specifies the SSH key configuration for a Linux OS</span><span class="sxs-lookup"><span data-stu-id="64e8f-170">Specifies the SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="64e8f-171">path</span><span class="sxs-lookup"><span data-stu-id="64e8f-171">path</span></span> | <span data-ttu-id="64e8f-172">Yes</span><span class="sxs-lookup"><span data-stu-id="64e8f-172">Yes</span></span> | <span data-ttu-id="64e8f-173">String</span><span class="sxs-lookup"><span data-stu-id="64e8f-173">String</span></span> | <span data-ttu-id="64e8f-174">Specifies the Linux file path where the SSH keys or certificate should be located</span><span class="sxs-lookup"><span data-stu-id="64e8f-174">Specifies the Linux file path where the SSH keys or certificate should be located</span></span>
<span data-ttu-id="64e8f-175">keyData</span><span class="sxs-lookup"><span data-stu-id="64e8f-175">keyData</span></span> | <span data-ttu-id="64e8f-176">Yes</span><span class="sxs-lookup"><span data-stu-id="64e8f-176">Yes</span></span> | <span data-ttu-id="64e8f-177">String</span><span class="sxs-lookup"><span data-stu-id="64e8f-177">String</span></span> | <span data-ttu-id="64e8f-178">Specifies a base64-encoded SSH public key</span><span class="sxs-lookup"><span data-stu-id="64e8f-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="64e8f-179">For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="64e8f-179">For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-the-same-key-vault-i-see-the-following-message"></a><span data-ttu-id="64e8f-180">When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:</span><span class="sxs-lookup"><span data-stu-id="64e8f-180">When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:</span></span>
 
  <span data-ttu-id="64e8f-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span><span class="sxs-lookup"><span data-stu-id="64e8f-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="64e8f-182">This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault.</span><span class="sxs-lookup"><span data-stu-id="64e8f-182">This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault.</span></span> <span data-ttu-id="64e8f-183">The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span><span class="sxs-lookup"><span data-stu-id="64e8f-183">The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="64e8f-184">To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span><span class="sxs-lookup"><span data-stu-id="64e8f-184">To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="64e8f-185">For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="64e8f-185">For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="64e8f-186">Find the secret in the virtual machine scale set object that is in the key vault.</span><span class="sxs-lookup"><span data-stu-id="64e8f-186">Find the secret in the virtual machine scale set object that is in the key vault.</span></span> <span data-ttu-id="64e8f-187">Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="64e8f-187">Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="64e8f-188">Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.</span><span class="sxs-lookup"><span data-stu-id="64e8f-188">Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.</span></span>
>

<span data-ttu-id="64e8f-189">New VMs will not have the old certificate.</span><span class="sxs-lookup"><span data-stu-id="64e8f-189">New VMs will not have the old certificate.</span></span> <span data-ttu-id="64e8f-190">However, VMs that have the certificate and which are already deployed will have the old certificate.</span><span class="sxs-lookup"><span data-stu-id="64e8f-190">However, VMs that have the certificate and which are already deployed will have the old certificate.</span></span>
 
### <a name="can-i-push-certificates-to-the-virtual-machine-scale-set-without-providing-the-password-when-the-certificate-is-in-the-secret-store"></a><span data-ttu-id="64e8f-191">Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?</span><span class="sxs-lookup"><span data-stu-id="64e8f-191">Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?</span></span>

<span data-ttu-id="64e8f-192">You do not need to hard-code passwords in scripts.</span><span class="sxs-lookup"><span data-stu-id="64e8f-192">You do not need to hard-code passwords in scripts.</span></span> <span data-ttu-id="64e8f-193">You can dynamically retrieve passwords with the permissions you use to run the deployment script.</span><span class="sxs-lookup"><span data-stu-id="64e8f-193">You can dynamically retrieve passwords with the permissions you use to run the deployment script.</span></span> <span data-ttu-id="64e8f-194">If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="64e8f-194">If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.</span></span>
 
### <a name="how-does-the-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-the-sourcevault-value-when-i-have-to-specify-the-absolute-uri-for-a-certificate-by-using-the-certificateurl-property"></a><span data-ttu-id="64e8f-195">How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span><span class="sxs-lookup"><span data-stu-id="64e8f-195">How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="64e8f-196">Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property?</span><span class="sxs-lookup"><span data-stu-id="64e8f-196">Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property?</span></span> 

<span data-ttu-id="64e8f-197">A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile.</span><span class="sxs-lookup"><span data-stu-id="64e8f-197">A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile.</span></span> 

<span data-ttu-id="64e8f-198">The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span><span class="sxs-lookup"><span data-stu-id="64e8f-198">The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="64e8f-199">If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP).</span><span class="sxs-lookup"><span data-stu-id="64e8f-199">If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="64e8f-200">ACLs exist even for resources that do not exist.</span><span class="sxs-lookup"><span data-stu-id="64e8f-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="64e8f-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.</span><span class="sxs-lookup"><span data-stu-id="64e8f-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.</span></span>
 
### <a name="if-i-add-secrets-to-an-existing-virtual-machine-scale-set-are-the-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="64e8f-202">If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones?</span><span class="sxs-lookup"><span data-stu-id="64e8f-202">If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="64e8f-203">Certificates are added to all your VMs, even preexisting ones.</span><span class="sxs-lookup"><span data-stu-id="64e8f-203">Certificates are added to all your VMs, even preexisting ones.</span></span> <span data-ttu-id="64e8f-204">If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.</span><span class="sxs-lookup"><span data-stu-id="64e8f-204">If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="64e8f-205">Where do I put certificates for Linux VMs?</span><span class="sxs-lookup"><span data-stu-id="64e8f-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="64e8f-206">To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-206">To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-to-a-new-certificate-object"></a><span data-ttu-id="64e8f-207">How do I add a new vault certificate to a new certificate object?</span><span class="sxs-lookup"><span data-stu-id="64e8f-207">How do I add a new vault certificate to a new certificate object?</span></span>

<span data-ttu-id="64e8f-208">To add a vault certificate to an existing secret, see the following PowerShell example.</span><span class="sxs-lookup"><span data-stu-id="64e8f-208">To add a vault certificate to an existing secret, see the following PowerShell example.</span></span> <span data-ttu-id="64e8f-209">Use only one secret object.</span><span class="sxs-lookup"><span data-stu-id="64e8f-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-to-certificates-if-you-reimage-a-vm"></a><span data-ttu-id="64e8f-210">What happens to certificates if you reimage a VM?</span><span class="sxs-lookup"><span data-stu-id="64e8f-210">What happens to certificates if you reimage a VM?</span></span>

<span data-ttu-id="64e8f-211">If you reimage a VM, certificates are deleted.</span><span class="sxs-lookup"><span data-stu-id="64e8f-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="64e8f-212">Reimaging deletes the entire OS disk.</span><span class="sxs-lookup"><span data-stu-id="64e8f-212">Reimaging deletes the entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-the-key-vault"></a><span data-ttu-id="64e8f-213">What happens if you delete a certificate from the key vault?</span><span class="sxs-lookup"><span data-stu-id="64e8f-213">What happens if you delete a certificate from the key vault?</span></span>

<span data-ttu-id="64e8f-214">If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span><span class="sxs-lookup"><span data-stu-id="64e8f-214">If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="64e8f-215">The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot.</span><span class="sxs-lookup"><span data-stu-id="64e8f-215">The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot.</span></span> <span data-ttu-id="64e8f-216">In this scenario, you can delete the certificates from the virtual machine scale set model.</span><span class="sxs-lookup"><span data-stu-id="64e8f-216">In this scenario, you can delete the certificates from the virtual machine scale set model.</span></span> 

<span data-ttu-id="64e8f-217">The CRP component does not persist customer secrets.</span><span class="sxs-lookup"><span data-stu-id="64e8f-217">The CRP component does not persist customer secrets.</span></span> <span data-ttu-id="64e8f-218">If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted.</span><span class="sxs-lookup"><span data-stu-id="64e8f-218">If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted.</span></span> <span data-ttu-id="64e8f-219">In this scenario, secrets are retrieved from the key vault.</span><span class="sxs-lookup"><span data-stu-id="64e8f-219">In this scenario, secrets are retrieved from the key vault.</span></span>

<span data-ttu-id="64e8f-220">You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).</span><span class="sxs-lookup"><span data-stu-id="64e8f-220">You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-to-specify-the-exact-location-for-the-certificate-url-httpsname-of-the-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="64e8f-221">Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="64e8f-221">Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="64e8f-222">The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.</span><span class="sxs-lookup"><span data-stu-id="64e8f-222">The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.</span></span>
 
<span data-ttu-id="64e8f-223">Method</span><span class="sxs-lookup"><span data-stu-id="64e8f-223">Method</span></span> | <span data-ttu-id="64e8f-224">URL</span><span class="sxs-lookup"><span data-stu-id="64e8f-224">URL</span></span>
--- | ---
<span data-ttu-id="64e8f-225">GET</span><span class="sxs-lookup"><span data-stu-id="64e8f-225">GET</span></span> | https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}

<span data-ttu-id="64e8f-226">Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="64e8f-226">Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve.</span></span> <span data-ttu-id="64e8f-227">The secret version might be excluded.</span><span class="sxs-lookup"><span data-stu-id="64e8f-227">The secret version might be excluded.</span></span> <span data-ttu-id="64e8f-228">In that case, the current version is retrieved.</span><span class="sxs-lookup"><span data-stu-id="64e8f-228">In that case, the current version is retrieved.</span></span>
  
### <a name="why-do-i-have-to-specify-the-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="64e8f-229">Why do I have to specify the certificate version when I use Key Vault?</span><span class="sxs-lookup"><span data-stu-id="64e8f-229">Why do I have to specify the certificate version when I use Key Vault?</span></span>

<span data-ttu-id="64e8f-230">The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-230">The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="64e8f-231">If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-231">If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs.</span></span> <span data-ttu-id="64e8f-232">But your VMs appear to reference it, and new VMs get the new secret.</span><span class="sxs-lookup"><span data-stu-id="64e8f-232">But your VMs appear to reference it, and new VMs get the new secret.</span></span> <span data-ttu-id="64e8f-233">To avoid this, you are required to reference a secret version.</span><span class="sxs-lookup"><span data-stu-id="64e8f-233">To avoid this, you are required to reference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-to-us-as-cer-public-keys-what-is-the-recommended-approach-for-deploying-these-certificates-to-a-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-234">My team works with several certificates that are distributed to us as .cer public keys.</span><span class="sxs-lookup"><span data-stu-id="64e8f-234">My team works with several certificates that are distributed to us as .cer public keys.</span></span> <span data-ttu-id="64e8f-235">What is the recommended approach for deploying these certificates to a virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-235">What is the recommended approach for deploying these certificates to a virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-236">To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span><span class="sxs-lookup"><span data-stu-id="64e8f-236">To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="64e8f-237">To do this, use `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="64e8f-237">To do this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="64e8f-238">For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method.</span><span class="sxs-lookup"><span data-stu-id="64e8f-238">For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method.</span></span> 

<span data-ttu-id="64e8f-239">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="64e8f-239">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-to-pass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="64e8f-240">I do not see an option for users to pass in certificates as base64 strings.</span><span class="sxs-lookup"><span data-stu-id="64e8f-240">I do not see an option for users to pass in certificates as base64 strings.</span></span> <span data-ttu-id="64e8f-241">Most other resource providers have this option.</span><span class="sxs-lookup"><span data-stu-id="64e8f-241">Most other resource providers have this option.</span></span>

<span data-ttu-id="64e8f-242">To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="64e8f-242">To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="64e8f-243">Include the following JSON property in your Resource Manager template:</span><span class="sxs-lookup"><span data-stu-id="64e8f-243">Include the following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-to-wrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="64e8f-244">Do I have to wrap certificates in JSON objects in key vaults?</span><span class="sxs-lookup"><span data-stu-id="64e8f-244">Do I have to wrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="64e8f-245">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span><span class="sxs-lookup"><span data-stu-id="64e8f-245">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="64e8f-246">We also support the content type application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="64e8f-246">We also support the content type application/x-pkcs12.</span></span> <span data-ttu-id="64e8f-247">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-247">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="64e8f-248">We currently do not support .cer files.</span><span class="sxs-lookup"><span data-stu-id="64e8f-248">We currently do not support .cer files.</span></span> <span data-ttu-id="64e8f-249">To use .cer files, export them into .pfx containers.</span><span class="sxs-lookup"><span data-stu-id="64e8f-249">To use .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="64e8f-250">Compliance</span><span class="sxs-lookup"><span data-stu-id="64e8f-250">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="64e8f-251">Are virtual machine scale sets PCI-compliant?</span><span class="sxs-lookup"><span data-stu-id="64e8f-251">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="64e8f-252">Virtual machine scale sets are a thin API layer on top of the CRP.</span><span class="sxs-lookup"><span data-stu-id="64e8f-252">Virtual machine scale sets are a thin API layer on top of the CRP.</span></span> <span data-ttu-id="64e8f-253">Both components are part of the compute platform in the Azure service tree.</span><span class="sxs-lookup"><span data-stu-id="64e8f-253">Both components are part of the compute platform in the Azure service tree.</span></span>

<span data-ttu-id="64e8f-254">From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform.</span><span class="sxs-lookup"><span data-stu-id="64e8f-254">From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform.</span></span> <span data-ttu-id="64e8f-255">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself.</span><span class="sxs-lookup"><span data-stu-id="64e8f-255">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself.</span></span> <span data-ttu-id="64e8f-256">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.</span><span class="sxs-lookup"><span data-stu-id="64e8f-256">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="64e8f-257">For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="64e8f-257">For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="64e8f-258">Extensions</span><span class="sxs-lookup"><span data-stu-id="64e8f-258">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="64e8f-259">How do I delete a virtual machine scale set extension?</span><span class="sxs-lookup"><span data-stu-id="64e8f-259">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="64e8f-260">To delete a virtual machine scale set extension, use the following PowerShell example:</span><span class="sxs-lookup"><span data-stu-id="64e8f-260">To delete a virtual machine scale set extension, use the following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="64e8f-261">You can find the extensionName value in `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="64e8f-261">You can find the extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="64e8f-262">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="64e8f-262">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="64e8f-263">For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="64e8f-263">For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-to-run-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-to-fail-what-can-i-do-to-fix-this"></a><span data-ttu-id="64e8f-264">Extensions seem to run in parallel on virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="64e8f-264">Extensions seem to run in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="64e8f-265">This causes my custom script extension to fail.</span><span class="sxs-lookup"><span data-stu-id="64e8f-265">This causes my custom script extension to fail.</span></span> <span data-ttu-id="64e8f-266">What can I do to fix this?</span><span class="sxs-lookup"><span data-stu-id="64e8f-266">What can I do to fix this?</span></span>

<span data-ttu-id="64e8f-267">To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-267">To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-the-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-268">How do I reset the password for VMs in my virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-268">How do I reset the password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-269">To reset the password for VMs in your virtual machine scale set, use VM access extensions.</span><span class="sxs-lookup"><span data-stu-id="64e8f-269">To reset the password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="64e8f-270">Use the following PowerShell example:</span><span class="sxs-lookup"><span data-stu-id="64e8f-270">Use the following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-to-all-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-271">How do I add an extension to all VMs in my virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-271">How do I add an extension to all VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-272">If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-272">If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.</span></span>

<span data-ttu-id="64e8f-273">If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-273">If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-the-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-the-vms-not-match-the-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-the-scripts-that-are-currently-configured-on-the-virtual-machine-scale-set-executed-or-are-the-scripts-that-were-configured-when-the-vm-was-first-created-used"></a><span data-ttu-id="64e8f-274">If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span><span class="sxs-lookup"><span data-stu-id="64e8f-274">If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="64e8f-275">(That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored?</span><span class="sxs-lookup"><span data-stu-id="64e8f-275">(That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="64e8f-276">When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?</span><span class="sxs-lookup"><span data-stu-id="64e8f-276">When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?</span></span>

<span data-ttu-id="64e8f-277">If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-277">If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs.</span></span> <span data-ttu-id="64e8f-278">If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model.</span><span class="sxs-lookup"><span data-stu-id="64e8f-278">If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model.</span></span> 

<span data-ttu-id="64e8f-279">If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun.</span><span class="sxs-lookup"><span data-stu-id="64e8f-279">If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun.</span></span> <span data-ttu-id="64e8f-280">If it is reimaged, it's like replacing the OS drive with the source image.</span><span class="sxs-lookup"><span data-stu-id="64e8f-280">If it is reimaged, it's like replacing the OS drive with the source image.</span></span> <span data-ttu-id="64e8f-281">Any specialization from the latest model, such as extensions, are run.</span><span class="sxs-lookup"><span data-stu-id="64e8f-281">Any specialization from the latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-to-an-azure-ad-domain"></a><span data-ttu-id="64e8f-282">How do I join a virtual machine scale set to an Azure AD domain?</span><span class="sxs-lookup"><span data-stu-id="64e8f-282">How do I join a virtual machine scale set to an Azure AD domain?</span></span>

<span data-ttu-id="64e8f-283">To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension.</span><span class="sxs-lookup"><span data-stu-id="64e8f-283">To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="64e8f-284">To define an extension, use the JsonADDomainExtension property:</span><span class="sxs-lookup"><span data-stu-id="64e8f-284">To define an extension, use the JsonADDomainExtension property:</span></span>

```json
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "joindomain",
                                "properties": {
                                    "publisher": "Microsoft.Compute",
                                    "type": "JsonADDomainExtension",
                                    "typeHandlerVersion": "1.0",
                                    "settings": {
                                        "Name": "[parameters('domainName')]",
                                        "OUPath": "[variables('ouPath')]",
                                        "User": "[variables('domainAndUsername')]",
                                        "Restart": "true",
                                        "Options": "[variables('domainJoinOptions')]"
                                    },
                                    "protectedsettings": {
                                        "Password": "[parameters('domainJoinPassword')]"
                                    }
                                }
                            }
                        ]
                    }
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-to-install-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="64e8f-285">My virtual machine scale set extension is trying to install something that requires a reboot.</span><span class="sxs-lookup"><span data-stu-id="64e8f-285">My virtual machine scale set extension is trying to install something that requires a reboot.</span></span> <span data-ttu-id="64e8f-286">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="64e8f-286">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="64e8f-287">If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension.</span><span class="sxs-lookup"><span data-stu-id="64e8f-287">If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="64e8f-288">If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration.</span><span class="sxs-lookup"><span data-stu-id="64e8f-288">If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-289">How do I turn on antimalware in my virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-289">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-290">To turn on antimalware on your virtual machine scale set, use the following PowerShell example:</span><span class="sxs-lookup"><span data-stu-id="64e8f-290">To turn on antimalware on your virtual machine scale set, use the following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve the most recent version number of the extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-to-execute-a-custom-script-thats-hosted-in-a-private-storage-account-the-script-runs-successfully-when-the-storage-is-public-but-when-i-try-to-use-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="64e8f-291">I need to execute a custom script that's hosted in a private storage account.</span><span class="sxs-lookup"><span data-stu-id="64e8f-291">I need to execute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="64e8f-292">The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails.</span><span class="sxs-lookup"><span data-stu-id="64e8f-292">The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="64e8f-293">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span><span class="sxs-lookup"><span data-stu-id="64e8f-293">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="64e8f-294">Link+SAS works fine from my local browser.</span><span class="sxs-lookup"><span data-stu-id="64e8f-294">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="64e8f-295">To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name.</span><span class="sxs-lookup"><span data-stu-id="64e8f-295">To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name.</span></span> <span data-ttu-id="64e8f-296">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="64e8f-296">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="64e8f-297">Networking</span><span class="sxs-lookup"><span data-stu-id="64e8f-297">Networking</span></span>
 
### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-the-same-subscription-and-same-region"></a><span data-ttu-id="64e8f-298">How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?</span><span class="sxs-lookup"><span data-stu-id="64e8f-298">How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?</span></span>

<span data-ttu-id="64e8f-299">To do a VIP swap for virtual machine scale sets in the same subscription and same region, see [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-299">To do a VIP swap for virtual machine scale sets in the same subscription and same region, see [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/).</span></span>
 
  
### <a name="what-is-the-resourceguid-property-on-a-nic-used-for"></a><span data-ttu-id="64e8f-300">What is the resourceGuid property on a NIC used for?</span><span class="sxs-lookup"><span data-stu-id="64e8f-300">What is the resourceGuid property on a NIC used for?</span></span>

<span data-ttu-id="64e8f-301">The resourceGuid property on a network interface card (NIC) is a unique ID.</span><span class="sxs-lookup"><span data-stu-id="64e8f-301">The resourceGuid property on a network interface card (NIC) is a unique ID.</span></span> <span data-ttu-id="64e8f-302">Lower layers will log this ID at some point in the future.</span><span class="sxs-lookup"><span data-stu-id="64e8f-302">Lower layers will log this ID at some point in the future.</span></span> 
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-to-use-for-static-private-ip-address-allocation"></a><span data-ttu-id="64e8f-303">How do I specify a range of private IP addresses to use for static private IP address allocation?</span><span class="sxs-lookup"><span data-stu-id="64e8f-303">How do I specify a range of private IP addresses to use for static private IP address allocation?</span></span>

<span data-ttu-id="64e8f-304">IP addresses are selected from a subnet that you specify.</span><span class="sxs-lookup"><span data-stu-id="64e8f-304">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="64e8f-305">The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span><span class="sxs-lookup"><span data-stu-id="64e8f-305">The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="64e8f-306">In this case, "dynamic" only means that you do not specify the IP address in a PUT request.</span><span class="sxs-lookup"><span data-stu-id="64e8f-306">In this case, "dynamic" only means that you do not specify the IP address in a PUT request.</span></span> <span data-ttu-id="64e8f-307">Specify the static set by using the subnet.</span><span class="sxs-lookup"><span data-stu-id="64e8f-307">Specify the static set by using the subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-to-an-existing-azure-virtual-network"></a><span data-ttu-id="64e8f-308">How do I deploy a virtual machine scale set to an existing Azure virtual network?</span><span class="sxs-lookup"><span data-stu-id="64e8f-308">How do I deploy a virtual machine scale set to an existing Azure virtual network?</span></span> 

<span data-ttu-id="64e8f-309">To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="64e8f-309">To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-the-ip-address-of-the-first-vm-in-a-virtual-machine-scale-set-to-the-output-of-a-template"></a><span data-ttu-id="64e8f-310">How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?</span><span class="sxs-lookup"><span data-stu-id="64e8f-310">How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?</span></span>

<span data-ttu-id="64e8f-311">To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="64e8f-311">To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>



## <a name="scale"></a><span data-ttu-id="64e8f-312">Scale</span><span class="sxs-lookup"><span data-stu-id="64e8f-312">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="64e8f-313">In what case would I create a virtual machine scale set with fewer than two VMs?</span><span class="sxs-lookup"><span data-stu-id="64e8f-313">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="64e8f-314">One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="64e8f-314">One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="64e8f-315">For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-315">For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="64e8f-316">Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.</span><span class="sxs-lookup"><span data-stu-id="64e8f-316">Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.</span></span>

<span data-ttu-id="64e8f-317">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-317">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="64e8f-318">Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible.</span><span class="sxs-lookup"><span data-stu-id="64e8f-318">Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="64e8f-319">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span><span class="sxs-lookup"><span data-stu-id="64e8f-319">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="64e8f-320">Many stateless workloads do not track individual units.</span><span class="sxs-lookup"><span data-stu-id="64e8f-320">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="64e8f-321">If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.</span><span class="sxs-lookup"><span data-stu-id="64e8f-321">If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.</span></span>

### <a name="how-do-i-change-the-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-322">How do I change the number of VMs in a virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-322">How do I change the number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-323">To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="64e8f-323">To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="64e8f-324">How do I define custom alerts for when certain thresholds are reached?</span><span class="sxs-lookup"><span data-stu-id="64e8f-324">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="64e8f-325">You have some flexibility in how you handle alerts for specified thresholds.</span><span class="sxs-lookup"><span data-stu-id="64e8f-325">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="64e8f-326">For example, you can define customized webhooks.</span><span class="sxs-lookup"><span data-stu-id="64e8f-326">For example, you can define customized webhooks.</span></span> <span data-ttu-id="64e8f-327">The following webhook example is from a Resource Manager template:</span><span class="sxs-lookup"><span data-stu-id="64e8f-327">The following webhook example is from a Resource Manager template:</span></span>

```json
   {
         "type": "Microsoft.Insights/autoscaleSettings",
           "apiVersion": "[variables('insightsApi')]",
                 "name": "autoscale",
                   "location": "[parameters('resourceLocation')]",
                     "dependsOn": [
                         "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
                 ],
                 "properties": {
                         "name": "autoscale",
                     "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
                     "enabled": true,
                     "notifications": [{
                              "operation": "Scale",
                              "email": {
                                   "sendToSubscriptionAdministrator": true,
                                   "sendToSubscriptionCoAdministrators": true,
                                   "customEmails": [
                                      "youremail@address.com"
                                   ]},
                              "webhooks": [{
                                    "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                                    "properties": {
                                        "key1": "custommetric",
                                        "key2": "scalevmss"
                                    }
                                    }
                              ]}],
```

<span data-ttu-id="64e8f-328">In this example, an alert goes to Pagerduty.com when a threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="64e8f-328">In this example, an alert goes to Pagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="64e8f-329">Patching and operations</span><span class="sxs-lookup"><span data-stu-id="64e8f-329">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="64e8f-330">How do I create a scale set in an existing resource group?</span><span class="sxs-lookup"><span data-stu-id="64e8f-330">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="64e8f-331">Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="64e8f-331">Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="64e8f-332">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span><span class="sxs-lookup"><span data-stu-id="64e8f-332">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-to-another-resource-group"></a><span data-ttu-id="64e8f-333">Can we move a scale set to another resource group?</span><span class="sxs-lookup"><span data-stu-id="64e8f-333">Can we move a scale set to another resource group?</span></span>

<span data-ttu-id="64e8f-334">Yes, you can move scale set resources to a new subscription or resource group.</span><span class="sxs-lookup"><span data-stu-id="64e8f-334">Yes, you can move scale set resources to a new subscription or resource group.</span></span>

### <a name="how-to-i-update-my-virtual-machine-scale-set-to-a-new-image-how-do-i-manage-patching"></a><span data-ttu-id="64e8f-335">How to I update my virtual machine scale set to a new image?</span><span class="sxs-lookup"><span data-stu-id="64e8f-335">How to I update my virtual machine scale set to a new image?</span></span> <span data-ttu-id="64e8f-336">How do I manage patching?</span><span class="sxs-lookup"><span data-stu-id="64e8f-336">How do I manage patching?</span></span>

<span data-ttu-id="64e8f-337">To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="64e8f-337">To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-the-reimage-operation-to-reset-a-vm-without-changing-the-image-that-is-i-want-reset-a-vm-to-factory-settings-rather-than-to-a-new-image"></a><span data-ttu-id="64e8f-338">Can I use the reimage operation to reset a VM without changing the image?</span><span class="sxs-lookup"><span data-stu-id="64e8f-338">Can I use the reimage operation to reset a VM without changing the image?</span></span> <span data-ttu-id="64e8f-339">(That is, I want reset a VM to factory settings rather than to a new image.)</span><span class="sxs-lookup"><span data-stu-id="64e8f-339">(That is, I want reset a VM to factory settings rather than to a new image.)</span></span>

<span data-ttu-id="64e8f-340">Yes, you can use the reimage operation to reset a VM without changing the image.</span><span class="sxs-lookup"><span data-stu-id="64e8f-340">Yes, you can use the reimage operation to reset a VM without changing the image.</span></span> <span data-ttu-id="64e8f-341">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.</span><span class="sxs-lookup"><span data-stu-id="64e8f-341">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.</span></span>

<span data-ttu-id="64e8f-342">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="64e8f-342">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="64e8f-343">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="64e8f-343">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="64e8f-344">How do I turn on boot diagnostics?</span><span class="sxs-lookup"><span data-stu-id="64e8f-344">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="64e8f-345">To turn on boot diagnostics, first, create a storage account.</span><span class="sxs-lookup"><span data-stu-id="64e8f-345">To turn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="64e8f-346">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="64e8f-346">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:</span></span>

```json
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": true,
          "storageUri": "http://yourstorageaccount.blob.core.windows.net"
        }
      }
```

<span data-ttu-id="64e8f-347">When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on.</span><span class="sxs-lookup"><span data-stu-id="64e8f-347">When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on.</span></span> <span data-ttu-id="64e8f-348">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="64e8f-348">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="64e8f-349">Virtual machine properties</span><span class="sxs-lookup"><span data-stu-id="64e8f-349">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-the-fault-domain-for-each-of-the-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-350">How do I get property information for each VM without making multiple calls?</span><span class="sxs-lookup"><span data-stu-id="64e8f-350">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="64e8f-351">For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-351">For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-352">To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:</span><span class="sxs-lookup"><span data-stu-id="64e8f-352">To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:</span></span>

<span data-ttu-id="64e8f-353">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="64e8f-353">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-to-different-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="64e8f-354">Can I pass different extension arguments to different VMs in a virtual machine scale set?</span><span class="sxs-lookup"><span data-stu-id="64e8f-354">Can I pass different extension arguments to different VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="64e8f-355">No, you cannot pass different extension arguments to different VMs in a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="64e8f-355">No, you cannot pass different extension arguments to different VMs in a virtual machine scale set.</span></span> <span data-ttu-id="64e8f-356">However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name.</span><span class="sxs-lookup"><span data-stu-id="64e8f-356">However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name.</span></span> <span data-ttu-id="64e8f-357">Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.</span><span class="sxs-lookup"><span data-stu-id="64e8f-357">Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="64e8f-358">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span><span class="sxs-lookup"><span data-stu-id="64e8f-358">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="64e8f-359">For example: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="64e8f-359">For example: 0, 1, 3...</span></span>

<span data-ttu-id="64e8f-360">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**.</span><span class="sxs-lookup"><span data-stu-id="64e8f-360">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**.</span></span> <span data-ttu-id="64e8f-361">If overprovisioning is set to **true**, more VMs than requested are created.</span><span class="sxs-lookup"><span data-stu-id="64e8f-361">If overprovisioning is set to **true**, more VMs than requested are created.</span></span> <span data-ttu-id="64e8f-362">Extra VMs are then deleted.</span><span class="sxs-lookup"><span data-stu-id="64e8f-362">Extra VMs are then deleted.</span></span> <span data-ttu-id="64e8f-363">In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span><span class="sxs-lookup"><span data-stu-id="64e8f-363">In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="64e8f-364">You can set this property to **false**.</span><span class="sxs-lookup"><span data-stu-id="64e8f-364">You can set this property to **false**.</span></span> <span data-ttu-id="64e8f-365">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span><span class="sxs-lookup"><span data-stu-id="64e8f-365">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-the-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-the-vm-when-should-i-choose-one-over-the-other"></a><span data-ttu-id="64e8f-366">What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM?</span><span class="sxs-lookup"><span data-stu-id="64e8f-366">What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM?</span></span> <span data-ttu-id="64e8f-367">When should I choose one over the other?</span><span class="sxs-lookup"><span data-stu-id="64e8f-367">When should I choose one over the other?</span></span>

<span data-ttu-id="64e8f-368">The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs).</span><span class="sxs-lookup"><span data-stu-id="64e8f-368">The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs).</span></span> <span data-ttu-id="64e8f-369">There are storage costs associated with running `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="64e8f-369">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="64e8f-370">You might use one or the other for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="64e8f-370">You might use one or the other for one of the following reasons:</span></span>

- <span data-ttu-id="64e8f-371">You want to stop paying compute costs, but you want to keep the disk state of the VMs.</span><span class="sxs-lookup"><span data-stu-id="64e8f-371">You want to stop paying compute costs, but you want to keep the disk state of the VMs.</span></span>
- <span data-ttu-id="64e8f-372">You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="64e8f-372">You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="64e8f-373">Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span><span class="sxs-lookup"><span data-stu-id="64e8f-373">Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="64e8f-374">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span><span class="sxs-lookup"><span data-stu-id="64e8f-374">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="64e8f-375">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span><span class="sxs-lookup"><span data-stu-id="64e8f-375">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="64e8f-376">Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.</span><span class="sxs-lookup"><span data-stu-id="64e8f-376">Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.</span></span>

