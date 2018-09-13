---
title: Deploy a VM with securely stored password on Azure Stack | Microsoft Docs
description: Learn how to deploy a VM using a password stored in Azure Stack Key Vault
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/07/2018
ms.author: mabrigg
ms.openlocfilehash: 4239eb31afd4abc8b3555f0ee353f5d96716d623
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866808"
---
# <a name="create-a-virtual-machine-using-a-secure-password-stored-in-azure-stack-key-vault"></a><span data-ttu-id="00538-103">Create a virtual machine using a secure password stored in Azure Stack Key Vault</span><span class="sxs-lookup"><span data-stu-id="00538-103">Create a virtual machine using a secure password stored in Azure Stack Key Vault</span></span>

<span data-ttu-id="00538-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="00538-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="00538-105">This article steps through deploying a Windows Server virtual machine using a password stored in Azure Stack Key Vault.</span><span class="sxs-lookup"><span data-stu-id="00538-105">This article steps through deploying a Windows Server virtual machine using a password stored in Azure Stack Key Vault.</span></span> <span data-ttu-id="00538-106">Using a key vault password is more secure than passing a plain text password.</span><span class="sxs-lookup"><span data-stu-id="00538-106">Using a key vault password is more secure than passing a plain text password.</span></span>

## <a name="overview"></a><span data-ttu-id="00538-107">Overview</span><span class="sxs-lookup"><span data-stu-id="00538-107">Overview</span></span>

<span data-ttu-id="00538-108">You can store values such as a password as a secret in an Azure Stack key vault.</span><span class="sxs-lookup"><span data-stu-id="00538-108">You can store values such as a password as a secret in an Azure Stack key vault.</span></span> <span data-ttu-id="00538-109">After you create a secret, you can reference it in Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="00538-109">After you create a secret, you can reference it in Azure Resource Manager templates.</span></span> <span data-ttu-id="00538-110">Using secrets with Resource Manager provides the following benefits:</span><span class="sxs-lookup"><span data-stu-id="00538-110">Using secrets with Resource Manager provides the following benefits:</span></span>

* <span data-ttu-id="00538-111">You don’t have to manually enter secret each time you deploy a resource.</span><span class="sxs-lookup"><span data-stu-id="00538-111">You don’t have to manually enter secret each time you deploy a resource.</span></span>
* <span data-ttu-id="00538-112">You can specify which users or service principals can access a secret.</span><span class="sxs-lookup"><span data-stu-id="00538-112">You can specify which users or service principals can access a secret.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00538-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00538-113">Prerequisites</span></span>

* <span data-ttu-id="00538-114">You must subscribe to an offer that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="00538-114">You must subscribe to an offer that includes the Key Vault service.</span></span>
* [<span data-ttu-id="00538-115">Install PowerShell for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="00538-115">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="00538-116">Configure the Azure Stack user's PowerShell environment.</span><span class="sxs-lookup"><span data-stu-id="00538-116">Configure the Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="00538-117">The following steps describe the process required to create a virtual machine by retrieving the password stored in a Key Vault:</span><span class="sxs-lookup"><span data-stu-id="00538-117">The following steps describe the process required to create a virtual machine by retrieving the password stored in a Key Vault:</span></span>

1. <span data-ttu-id="00538-118">Create a Key Vault secret.</span><span class="sxs-lookup"><span data-stu-id="00538-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="00538-119">Update the azuredeploy.parameters.json file.</span><span class="sxs-lookup"><span data-stu-id="00538-119">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="00538-120">Deploy the template.</span><span class="sxs-lookup"><span data-stu-id="00538-120">Deploy the template.</span></span>

><span data-ttu-id="00538-121">[NOTE] You can use these steps from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span><span class="sxs-lookup"><span data-stu-id="00538-121">[NOTE] You can use these steps from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="00538-122">Create a Key Vault secret</span><span class="sxs-lookup"><span data-stu-id="00538-122">Create a Key Vault secret</span></span>

<span data-ttu-id="00538-123">The following script creates a key vault, and stores a password in the key vault as a secret.</span><span class="sxs-lookup"><span data-stu-id="00538-123">The following script creates a key vault, and stores a password in the key vault as a secret.</span></span> <span data-ttu-id="00538-124">Use the `-EnabledForDeployment` parameter when you're creating the key vault.</span><span class="sxs-lookup"><span data-stu-id="00538-124">Use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="00538-125">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="00538-125">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "MySecret"

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location
  -EnabledForTemplateDeployment

$secretValue = ConvertTo-SecureString -String '<Password for your virtual machine>' -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
  -SecretValue $secretValue

```

<span data-ttu-id="00538-126">When you run the previous script, the output includes the secret URI.</span><span class="sxs-lookup"><span data-stu-id="00538-126">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="00538-127">Make a note of this URI.</span><span class="sxs-lookup"><span data-stu-id="00538-127">Make a note of this URI.</span></span> <span data-ttu-id="00538-128">You have to reference it in the [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span><span class="sxs-lookup"><span data-stu-id="00538-128">You have to reference it in the [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span></span> <span data-ttu-id="00538-129">Download the [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) folder onto your development computer.</span><span class="sxs-lookup"><span data-stu-id="00538-129">Download the [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) folder onto your development computer.</span></span> <span data-ttu-id="00538-130">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span><span class="sxs-lookup"><span data-stu-id="00538-130">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="00538-131">Modify the `azuredeploy.parameters.json` file according to your environment values.</span><span class="sxs-lookup"><span data-stu-id="00538-131">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="00538-132">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span><span class="sxs-lookup"><span data-stu-id="00538-132">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="00538-133">The following file is an example of a parameter file:</span><span class="sxs-lookup"><span data-stu-id="00538-133">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="00538-134">Update the azuredeploy.parameters.json file</span><span class="sxs-lookup"><span data-stu-id="00538-134">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="00538-135">Update the azuredeploy.parameters.json file with the KeyVault URI, secretName, adminUsername of the virtual machine values as per your environment.</span><span class="sxs-lookup"><span data-stu-id="00538-135">Update the azuredeploy.parameters.json file with the KeyVault URI, secretName, adminUsername of the virtual machine values as per your environment.</span></span> <span data-ttu-id="00538-136">The following JSON file shows an example of the template parameters file:</span><span class="sxs-lookup"><span data-stu-id="00538-136">The following JSON file shows an example of the template parameters file:</span></span>

```json
{
    "$schema":  "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion":  "1.0.0.0",
    "parameters":  {
       "adminUsername":  {
         "value":  "demouser"
          },
         "adminPassword":  {
           "reference":  {
              "keyVault":  {
                "id":  "/subscriptions/xxxxxx/resourceGroups/RgKvPwd/providers/Microsoft.KeyVault/vaults/KvPwd"
                },
              "secretName":  "MySecret"
           }
         },
       "dnsLabelPrefix":  {
          "value":  "mydns123456"
        },
        "windowsOSVersion":  {
          "value":  "2016-Datacenter"
        }
    }
}

```

## <a name="template-deployment"></a><span data-ttu-id="00538-137">Template deployment</span><span class="sxs-lookup"><span data-stu-id="00538-137">Template deployment</span></span>

<span data-ttu-id="00538-138">Now deploy the template by using the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="00538-138">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

<span data-ttu-id="00538-139">When the template is deployed successfully, it results in the following output:</span><span class="sxs-lookup"><span data-stu-id="00538-139">When the template is deployed successfully, it results in the following output:</span></span>

![Deployment output](media/azure-stack-kv-deploy-vm-with-secret/deployment-output.png)

## <a name="next-steps"></a><span data-ttu-id="00538-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="00538-141">Next steps</span></span>

[<span data-ttu-id="00538-142">Deploy a sample app with Key Vault</span><span class="sxs-lookup"><span data-stu-id="00538-142">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="00538-143">Deploy a VM with a Key Vault certificate</span><span class="sxs-lookup"><span data-stu-id="00538-143">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)
