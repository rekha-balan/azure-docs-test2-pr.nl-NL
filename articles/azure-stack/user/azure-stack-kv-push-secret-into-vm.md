---
title: Deploy a virtual machine with a securely stored certificate on Azure Stack | Microsoft Docs
description: Learn how to deploy a virtual machine and push a certificate onto it by using a key vault in Azure Stack
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/15/2018
ms.author: sethm
ms.openlocfilehash: aef706d18d558f5fe321735c7f93361a5ef50606
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869259"
---
# <a name="create-a-virtual-machine-and-install-a-certificate-retrieved-from-an-azure-stack-key-vault"></a><span data-ttu-id="e51c6-103">Create a virtual machine and install a certificate retrieved from an Azure Stack key vault</span><span class="sxs-lookup"><span data-stu-id="e51c6-103">Create a virtual machine and install a certificate retrieved from an Azure Stack key vault</span></span>

<span data-ttu-id="e51c6-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="e51c6-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="e51c6-105">Learn how to create an Azure Stack virtual machine (VM) with a  key vault certificate installed.</span><span class="sxs-lookup"><span data-stu-id="e51c6-105">Learn how to create an Azure Stack virtual machine (VM) with a  key vault certificate installed.</span></span>

## <a name="overview"></a><span data-ttu-id="e51c6-106">Overview</span><span class="sxs-lookup"><span data-stu-id="e51c6-106">Overview</span></span>

<span data-ttu-id="e51c6-107">Certificates are used in many scenarios, such as authenticating to Active Directory, or encrypting web traffic.</span><span class="sxs-lookup"><span data-stu-id="e51c6-107">Certificates are used in many scenarios, such as authenticating to Active Directory, or encrypting web traffic.</span></span> <span data-ttu-id="e51c6-108">You can securely store certificates as secrets in an Azure Stack key vault.</span><span class="sxs-lookup"><span data-stu-id="e51c6-108">You can securely store certificates as secrets in an Azure Stack key vault.</span></span> <span data-ttu-id="e51c6-109">The benefits of using Azure Stack Key Vault are:</span><span class="sxs-lookup"><span data-stu-id="e51c6-109">The benefits of using Azure Stack Key Vault are:</span></span>

* <span data-ttu-id="e51c6-110">Certificates aren't exposed in a script, command-line history, or template.</span><span class="sxs-lookup"><span data-stu-id="e51c6-110">Certificates aren't exposed in a script, command-line history, or template.</span></span>
* <span data-ttu-id="e51c6-111">The certificate management process is streamlined.</span><span class="sxs-lookup"><span data-stu-id="e51c6-111">The certificate management process is streamlined.</span></span>
* <span data-ttu-id="e51c6-112">You have control of the keys that access certificates.</span><span class="sxs-lookup"><span data-stu-id="e51c6-112">You have control of the keys that access certificates.</span></span>

### <a name="process-description"></a><span data-ttu-id="e51c6-113">Process description</span><span class="sxs-lookup"><span data-stu-id="e51c6-113">Process description</span></span>

<span data-ttu-id="e51c6-114">The following steps describe the process required to push a certificate onto the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="e51c6-114">The following steps describe the process required to push a certificate onto the virtual machine:</span></span>

1. <span data-ttu-id="e51c6-115">Create a Key Vault secret.</span><span class="sxs-lookup"><span data-stu-id="e51c6-115">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="e51c6-116">Update the azuredeploy.parameters.json file.</span><span class="sxs-lookup"><span data-stu-id="e51c6-116">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="e51c6-117">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="e51c6-117">Deploy the template</span></span>

> [!NOTE]
> <span data-ttu-id="e51c6-118">You can use these steps from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span><span class="sxs-lookup"><span data-stu-id="e51c6-118">You can use these steps from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e51c6-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e51c6-119">Prerequisites</span></span>

* <span data-ttu-id="e51c6-120">You must subscribe to an offer that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="e51c6-120">You must subscribe to an offer that includes the Key Vault service.</span></span>
* [<span data-ttu-id="e51c6-121">Install PowerShell for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e51c6-121">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="e51c6-122">Configure the Azure Stack user's PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="e51c6-122">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="e51c6-123">Create a Key Vault secret</span><span class="sxs-lookup"><span data-stu-id="e51c6-123">Create a Key Vault secret</span></span>

<span data-ttu-id="e51c6-124">The following script creates a certificate in the .pfx format, creates a key vault, and stores the certificate in the key vault as a secret.</span><span class="sxs-lookup"><span data-stu-id="e51c6-124">The following script creates a certificate in the .pfx format, creates a key vault, and stores the certificate in the key vault as a secret.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e51c6-125">You must use the `-EnabledForDeployment` parameter when creating the key vault.</span><span class="sxs-lookup"><span data-stu-id="e51c6-125">You must use the `-EnabledForDeployment` parameter when creating the key vault.</span></span> <span data-ttu-id="e51c6-126">This parameter ensures that the key vault can be referenced from Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="e51c6-126">This parameter ensures that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in the .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used to export the certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in the previous step>" `
  -FilePath "<Fully qualified path where the exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload the certificate into the key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where the exported certificate can be stored>"
$certPassword = "<Password used to export the certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

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

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret

```

<span data-ttu-id="e51c6-127">When you run the previous script, the output includes the secret URI.</span><span class="sxs-lookup"><span data-stu-id="e51c6-127">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="e51c6-128">Make a note of this URI.</span><span class="sxs-lookup"><span data-stu-id="e51c6-128">Make a note of this URI.</span></span> <span data-ttu-id="e51c6-129">You have to reference it in the [Push certificate to Windows Resource Manager template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate).</span><span class="sxs-lookup"><span data-stu-id="e51c6-129">You have to reference it in the [Push certificate to Windows Resource Manager template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate).</span></span> <span data-ttu-id="e51c6-130">Download the [vm-push-certificate-windows template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate) folder onto your development computer.</span><span class="sxs-lookup"><span data-stu-id="e51c6-130">Download the [vm-push-certificate-windows template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate) folder onto your development computer.</span></span> <span data-ttu-id="e51c6-131">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span><span class="sxs-lookup"><span data-stu-id="e51c6-131">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="e51c6-132">Modify the `azuredeploy.parameters.json` file according to your environment values.</span><span class="sxs-lookup"><span data-stu-id="e51c6-132">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="e51c6-133">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span><span class="sxs-lookup"><span data-stu-id="e51c6-133">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="e51c6-134">The following file is an example of a parameter file:</span><span class="sxs-lookup"><span data-stu-id="e51c6-134">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="e51c6-135">Update the azuredeploy.parameters.json file</span><span class="sxs-lookup"><span data-stu-id="e51c6-135">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="e51c6-136">Update the azuredeploy.parameters.json file with the vaultName, secret URI, VmName, and other values as per your environment.</span><span class="sxs-lookup"><span data-stu-id="e51c6-136">Update the azuredeploy.parameters.json file with the vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="e51c6-137">The following JSON file shows an example of the template parameters file:</span><span class="sxs-lookup"><span data-stu-id="e51c6-137">The following JSON file shows an example of the template parameters file:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-the-template"></a><span data-ttu-id="e51c6-138">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="e51c6-138">Deploy the template</span></span>

<span data-ttu-id="e51c6-139">Deploy the template by using the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="e51c6-139">Deploy the template by using the following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template to create a VM and push the secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

<span data-ttu-id="e51c6-140">When the template is deployed successfully, it results in the following output:</span><span class="sxs-lookup"><span data-stu-id="e51c6-140">When the template is deployed successfully, it results in the following output:</span></span>

![Template deployment results](media/azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="e51c6-142">Azure Stack pushes the certificate onto the virtual machine during deployment.</span><span class="sxs-lookup"><span data-stu-id="e51c6-142">Azure Stack pushes the certificate onto the virtual machine during deployment.</span></span> <span data-ttu-id="e51c6-143">The certificate's location depends on the VM's operating system:</span><span class="sxs-lookup"><span data-stu-id="e51c6-143">The certificate's location depends on the VM's operating system:</span></span>

* <span data-ttu-id="e51c6-144">In Windows, the certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span><span class="sxs-lookup"><span data-stu-id="e51c6-144">In Windows, the certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span></span>
* <span data-ttu-id="e51c6-145">In Linux, the certificate is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for the private key.</span><span class="sxs-lookup"><span data-stu-id="e51c6-145">In Linux, the certificate is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for the private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="e51c6-146">Retire certificates</span><span class="sxs-lookup"><span data-stu-id="e51c6-146">Retire certificates</span></span>

<span data-ttu-id="e51c6-147">Retiring certificates is part of the certificate management process.</span><span class="sxs-lookup"><span data-stu-id="e51c6-147">Retiring certificates is part of the certificate management process.</span></span> <span data-ttu-id="e51c6-148">You can't delete the older version of a certificate, but you can disable it by using the `Set-AzureKeyVaultSecretAttribute` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e51c6-148">You can't delete the older version of a certificate, but you can disable it by using the `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span>

<span data-ttu-id="e51c6-149">The following example shows how to disable a certifcate.</span><span class="sxs-lookup"><span data-stu-id="e51c6-149">The following example shows how to disable a certifcate.</span></span> <span data-ttu-id="e51c6-150">Use your own values for the **VaultName**, **Name**, and **Version** parameters.</span><span class="sxs-lookup"><span data-stu-id="e51c6-150">Use your own values for the **VaultName**, **Name**, and **Version** parameters.</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="e51c6-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="e51c6-151">Next steps</span></span>

* [<span data-ttu-id="e51c6-152">Deploy a VM with a Key Vault password</span><span class="sxs-lookup"><span data-stu-id="e51c6-152">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="e51c6-153">Allow an application to access Key Vault</span><span class="sxs-lookup"><span data-stu-id="e51c6-153">Allow an application to access Key Vault</span></span>](azure-stack-kv-sample-app.md)
