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
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Azure virtual machine scale sets FAQs

Get answers to frequently asked questions about virtual machine scale sets in Azure.

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>What are best practices for Azure Autoscale?

For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Where do I find metric names for autoscaling that uses host-based metrics?

For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?

Yes. For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

For a Service Bus queue, use the following JSON:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

For a storage queue, use the following JSON:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Replace example values with your resource Uniform Resource Identifiers (URIs).


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Should I autoscale by using host-based metrics or a diagnostics extension?

You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.

For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

The sample uses the host-level CPU metric and a message count metric.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>How do I set alert rules on a virtual machine scale set?

You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI. For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

The TargetResourceId of the virtual machine scale set looks like this: 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

You can choose any VM performance counter as the metric to set an alert for. For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>How do I set up autoscale on a virtual machine scale set by using PowerShell?

To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certificates

### <a name="how-do-i-securely-ship-a-certificate-to-the-vm-how-do-i-provision-a-virtual-machine-scale-set-to-run-a-website-where-the-ssl-for-the-website-is-shipped-securely-from-a-certificate-configuration-the-common-certificate-rotation-operation-would-be-almost-the-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-to-do-this"></a>How do I securely ship a certificate to the VM? How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration? (The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this? 

To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.

Use the following JSON:

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

The code supports Windows and Linux.

For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Example of Self-signed certificate

1.  Create a self-signed certificate in a key vault.

    Use the following PowerShell commands:

  ```powershell
  Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

  Login-AzureRmAccount

  Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
  ```

  This command gives you the input for the Azure Resource Manager template.

  For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Change the Resource Manager template.

  Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:

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
  

### <a name="can-i-specify-an-ssh-key-pair-to-use-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?  

Yes. The REST API for **osProfile** is similar to the standard VM REST API. 

Include **osProfile** in your template:

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
 
This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>How do I remove deprecated certificates? 

To remove deprecated certificates, remove the old certificate from the vault certificates list. Leave all the certificates that you want to remain on your computer in the list. This does not remove the certificate from all your VMs. It also does not add the certificate to new VMs that are created in the virtual machine scale set. 

To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-the-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-to-store-the-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning? I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.

If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault. Public keys are not secret.
 
You can provide SSH public keys in plain text when you create a Linux VM:

```json
"linuxConfiguration": {  
          "ssh": {  
            "publicKeys": [ {  
              "path": "path",
              "keyData": "publickey"
            } ]
          }
```
 
linuxConfiguration element name | Required | Type | Description
--- | --- | --- | --- |  ---
ssh | No | Collection | Specifies the SSH key configuration for a Linux OS
path | Yes | String | Specifies the Linux file path where the SSH keys or certificate should be located
keyData | Yes | String | Specifies a base64-encoded SSH public key

For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-the-same-key-vault-i-see-the-following-message"></a>When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:
 
  Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.
 
This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault. The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.
 
To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.
 
For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Find the secret in the virtual machine scale set object that is in the key vault. Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.

> [!NOTE] 
> Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.
>

New VMs will not have the old certificate. However, VMs that have the certificate and which are already deployed will have the old certificate.
 
### <a name="can-i-push-certificates-to-the-virtual-machine-scale-set-without-providing-the-password-when-the-certificate-is-in-the-secret-store"></a>Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?

You do not need to hard-code passwords in scripts. You can dynamically retrieve passwords with the permissions you use to run the deployment script. If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.
 
### <a name="how-does-the-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-the-sourcevault-value-when-i-have-to-specify-the-absolute-uri-for-a-certificate-by-using-the-certificateurl-property"></a>How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work? Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property? 

A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile. 

The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model. If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP). ACLs exist even for resources that do not exist.

If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.
 
### <a name="if-i-add-secrets-to-an-existing-virtual-machine-scale-set-are-the-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones? 

Certificates are added to all your VMs, even preexisting ones. If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Where do I put certificates for Linux VMs?

To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-to-a-new-certificate-object"></a>How do I add a new vault certificate to a new certificate object?

To add a vault certificate to an existing secret, see the following PowerShell example. Use only one secret object.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-to-certificates-if-you-reimage-a-vm"></a>What happens to certificates if you reimage a VM?

If you reimage a VM, certificates are deleted. Reimaging deletes the entire OS disk. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-the-key-vault"></a>What happens if you delete a certificate from the key vault?

If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure. The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot. In this scenario, you can delete the certificates from the virtual machine scale set model. 

The CRP component does not persist customer secrets. If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted. In this scenario, secrets are retrieved from the key vault.

You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).
 
### <a name="why-do-i-have-to-specify-the-exact-location-for-the-certificate-url-httpsname-of-the-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.
 
Method | URL
--- | ---
GET | https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}

Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve. The secret version might be excluded. In that case, the current version is retrieved.
  
### <a name="why-do-i-have-to-specify-the-certificate-version-when-i-use-key-vault"></a>Why do I have to specify the certificate version when I use Key Vault?

The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.

If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs. But your VMs appear to reference it, and new VMs get the new secret. To avoid this, you are required to reference a secret version.

### <a name="my-team-works-with-several-certificates-that-are-distributed-to-us-as-cer-public-keys-what-is-the-recommended-approach-for-deploying-these-certificates-to-a-virtual-machine-scale-set"></a>My team works with several certificates that are distributed to us as .cer public keys. What is the recommended approach for deploying these certificates to a virtual machine scale set?

To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files. To do this, use `X509ContentType = Pfx`. For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method. 

For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-to-pass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>I do not see an option for users to pass in certificates as base64 strings. Most other resource providers have this option.

To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template. Include the following JSON property in your Resource Manager template:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-to-wrap-certificates-in-json-objects-in-key-vaults"></a>Do I have to wrap certificates in JSON objects in key vaults?

In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects. 

We also support the content type application/x-pkcs12. For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
We currently do not support .cer files. To use .cer files, export them into .pfx containers.



## <a name="compliance"></a>Compliance

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Are virtual machine scale sets PCI-compliant?

Virtual machine scale sets are a thin API layer on top of the CRP. Both components are part of the compute platform in the Azure service tree.

From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform. They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself. Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.

For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Extensions

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>How do I delete a virtual machine scale set extension?

To delete a virtual machine scale set extension, use the following PowerShell example:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
You can find the extensionName value in `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Is there a virtual machine scale set template example that integrates with Operations Management Suite?

For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-to-run-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-to-fail-what-can-i-do-to-fix-this"></a>Extensions seem to run in parallel on virtual machine scale sets. This causes my custom script extension to fail. What can I do to fix this?

To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-the-password-for-vms-in-my-virtual-machine-scale-set"></a>How do I reset the password for VMs in my virtual machine scale set?

To reset the password for VMs in your virtual machine scale set, use VM access extensions. 

Use the following PowerShell example:

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
 
 
### <a name="how-do-i-add-an-extension-to-all-vms-in-my-virtual-machine-scale-set"></a>How do I add an extension to all VMs in my virtual machine scale set?

If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.

If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.

  
### <a name="if-the-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-the-vms-not-match-the-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-the-scripts-that-are-currently-configured-on-the-virtual-machine-scale-set-executed-or-are-the-scripts-that-were-configured-when-the-vm-was-first-created-used"></a>If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected? (That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored? When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?

If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs. If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model. 

If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun. If it is reimaged, it's like replacing the OS drive with the source image. Any specialization from the latest model, such as extensions, are run.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-to-an-azure-ad-domain"></a>How do I join a virtual machine scale set to an Azure AD domain?

To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension. 

To define an extension, use the JsonADDomainExtension property:

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-to-install-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>My virtual machine scale set extension is trying to install something that requires a reboot. For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"

If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension. If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>How do I turn on antimalware in my virtual machine scale set?

To turn on antimalware on your virtual machine scale set, use the following PowerShell example:

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

### <a name="i-need-to-execute-a-custom-script-thats-hosted-in-a-private-storage-account-the-script-runs-successfully-when-the-storage-is-public-but-when-i-try-to-use-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>I need to execute a custom script that's hosted in a private storage account. The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails. This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”. Link+SAS works fine from my local browser.

To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name. For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Networking
 
### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-the-same-subscription-and-same-region"></a>How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?

To do a VIP swap for virtual machine scale sets in the same subscription and same region, see [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/).
 
  
### <a name="what-is-the-resourceguid-property-on-a-nic-used-for"></a>What is the resourceGuid property on a NIC used for?

The resourceGuid property on a network interface card (NIC) is a unique ID. Lower layers will log this ID at some point in the future. 
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-to-use-for-static-private-ip-address-allocation"></a>How do I specify a range of private IP addresses to use for static private IP address allocation?

IP addresses are selected from a subnet that you specify. 

The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change. In this case, "dynamic" only means that you do not specify the IP address in a PUT request. Specify the static set by using the subnet. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-to-an-existing-azure-virtual-network"></a>How do I deploy a virtual machine scale set to an existing Azure virtual network? 

To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-the-ip-address-of-the-first-vm-in-a-virtual-machine-scale-set-to-the-output-of-a-template"></a>How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?

To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).



## <a name="scale"></a>Scale

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>In what case would I create a virtual machine scale set with fewer than two VMs?

One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set. For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs. Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.

Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs. Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible. This uniformity is a key differentiator for virtual machine scale sets versus availability sets. Many stateless workloads do not track individual units. If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.

### <a name="how-do-i-change-the-number-of-vms-in-a-virtual-machine-scale-set"></a>How do I change the number of VMs in a virtual machine scale set?

To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>How do I define custom alerts for when certain thresholds are reached?

You have some flexibility in how you handle alerts for specified thresholds. For example, you can define customized webhooks. The following webhook example is from a Resource Manager template:

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

In this example, an alert goes to Pagerduty.com when a threshold is reached.



## <a name="patching-and-operations"></a>Patching and operations

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>How do I create a scale set in an existing resource group?

Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template. You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.

### <a name="can-we-move-a-scale-set-to-another-resource-group"></a>Can we move a scale set to another resource group?

Yes, you can move scale set resources to a new subscription or resource group.

### <a name="how-to-i-update-my-virtual-machine-scale-set-to-a-new-image-how-do-i-manage-patching"></a>How to I update my virtual machine scale set to a new image? How do I manage patching?

To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-the-reimage-operation-to-reset-a-vm-without-changing-the-image-that-is-i-want-reset-a-vm-to-factory-settings-rather-than-to-a-new-image"></a>Can I use the reimage operation to reset a VM without changing the image? (That is, I want reset a VM to factory settings rather than to a new image.)

Yes, you can use the reimage operation to reset a VM without changing the image. However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.

For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Troubleshooting

### <a name="how-do-i-turn-on-boot-diagnostics"></a>How do I turn on boot diagnostics?

To turn on boot diagnostics, first, create a storage account. Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:

```json
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": true,
          "storageUri": "http://yourstorageaccount.blob.core.windows.net"
        }
      }
```

When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on. Here's an example:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Virtual machine properties

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-the-fault-domain-for-each-of-the-100-vms-in-my-virtual-machine-scale-set"></a>How do I get property information for each VM without making multiple calls? For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?

To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:

/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView

### <a name="can-i-pass-different-extension-arguments-to-different-vms-in-a-virtual-machine-scale-set"></a>Can I pass different extension arguments to different VMs in a virtual machine scale set?

No, you cannot pass different extension arguments to different VMs in a virtual machine scale set. However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name. Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Why are there gaps between my virtual machine scale set VM machine names and VM IDs? For example: 0, 1, 3...

There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**. If overprovisioning is set to **true**, more VMs than requested are created. Extra VMs are then deleted. In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules. 

You can set this property to **false**. For small virtual machine scale sets, this doesn't significantly affect deployment reliability.

### <a name="what-is-the-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-the-vm-when-should-i-choose-one-over-the-other"></a>What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM? When should I choose one over the other?

The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs). There are storage costs associated with running `stop deallocate`. You might use one or the other for one of the following reasons:

- You want to stop paying compute costs, but you want to keep the disk state of the VMs.
- You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.
  - Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.
- You have a virtual machine scale set that is unevenly distributed across fault domains or update domains. This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning. Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.

