---
title: Key Vault secret with Resource Manager template | Microsoft Docs
description: Shows how to pass a secret from a key vault as a parameter during deployment.
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: tomfitz
ms.openlocfilehash: 61dbe6861ba0458c5a25834c6fd745e028c9f53c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563891"
---
# <a name="use-key-vault-to-pass-secure-parameter-value-during-deployment"></a><span data-ttu-id="6fce3-103">Use Key Vault to pass secure parameter value during deployment</span><span class="sxs-lookup"><span data-stu-id="6fce3-103">Use Key Vault to pass secure parameter value during deployment</span></span>

<span data-ttu-id="6fce3-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6fce3-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="6fce3-105">You retrieve the value by referencing the key vault and secret in your parameter file.</span><span class="sxs-lookup"><span data-stu-id="6fce3-105">You retrieve the value by referencing the key vault and secret in your parameter file.</span></span> <span data-ttu-id="6fce3-106">The value is never exposed because you only reference its key vault ID.</span><span class="sxs-lookup"><span data-stu-id="6fce3-106">The value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="6fce3-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span><span class="sxs-lookup"><span data-stu-id="6fce3-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span></span> <span data-ttu-id="6fce3-108">The key vault can exist in a different subscription than the resource group you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="6fce3-108">The key vault can exist in a different subscription than the resource group you are deploying to.</span></span> <span data-ttu-id="6fce3-109">When referencing the key vault, you include the subscription ID.</span><span class="sxs-lookup"><span data-stu-id="6fce3-109">When referencing the key vault, you include the subscription ID.</span></span>

<span data-ttu-id="6fce3-110">This topic shows you how to create a key vault and secret, configure access to the secret for a Resource Manager template, and pass the secret as a parameter.</span><span class="sxs-lookup"><span data-stu-id="6fce3-110">This topic shows you how to create a key vault and secret, configure access to the secret for a Resource Manager template, and pass the secret as a parameter.</span></span> <span data-ttu-id="6fce3-111">If you already have a key vault and secret, but need to check template and user access, go to the [Enable access to the secret](#enable-access-to-the-secret) section.</span><span class="sxs-lookup"><span data-stu-id="6fce3-111">If you already have a key vault and secret, but need to check template and user access, go to the [Enable access to the secret](#enable-access-to-the-secret) section.</span></span> <span data-ttu-id="6fce3-112">If you already have the key vault and secret, and are sure it is configured for template and user access, go to the [Reference a secret with static id](#reference-a-secret-with-static-id) section.</span><span class="sxs-lookup"><span data-stu-id="6fce3-112">If you already have the key vault and secret, and are sure it is configured for template and user access, go to the [Reference a secret with static id](#reference-a-secret-with-static-id) section.</span></span> 

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="6fce3-113">Deploy a key vault and secret</span><span class="sxs-lookup"><span data-stu-id="6fce3-113">Deploy a key vault and secret</span></span>

<span data-ttu-id="6fce3-114">You can deploy a key vault and secret through a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="6fce3-114">You can deploy a key vault and secret through a Resource Manager template.</span></span> <span data-ttu-id="6fce3-115">For an example, see [Key vault template](resource-manager-template-keyvault.md) and [Key vault secret template](resource-manager-template-keyvault-secret.md).</span><span class="sxs-lookup"><span data-stu-id="6fce3-115">For an example, see [Key vault template](resource-manager-template-keyvault.md) and [Key vault secret template](resource-manager-template-keyvault-secret.md).</span></span> <span data-ttu-id="6fce3-116">When creating the key vault, set the **enabledForTemplateDeployment** property to **true** so it can be referenced from other Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="6fce3-116">When creating the key vault, set the **enabledForTemplateDeployment** property to **true** so it can be referenced from other Resource Manager templates.</span></span> 

<span data-ttu-id="6fce3-117">Or, you can create the key vault and secret through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6fce3-117">Or, you can create the key vault and secret through the Azure portal.</span></span> 

1. <span data-ttu-id="6fce3-118">Select **New** -> **Security + Identity** -> **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-118">Select **New** -> **Security + Identity** -> **Key Vault**.</span></span>

   ![create new key vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/new-key-vault.png)

2. <span data-ttu-id="6fce3-120">Provide values for the key vault.</span><span class="sxs-lookup"><span data-stu-id="6fce3-120">Provide values for the key vault.</span></span> <span data-ttu-id="6fce3-121">You can ignore the **Access policies** and **Advanced access policy** settings for now.</span><span class="sxs-lookup"><span data-stu-id="6fce3-121">You can ignore the **Access policies** and **Advanced access policy** settings for now.</span></span> <span data-ttu-id="6fce3-122">Those settings are covered in the section.</span><span class="sxs-lookup"><span data-stu-id="6fce3-122">Those settings are covered in the section.</span></span> <span data-ttu-id="6fce3-123">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-123">Select **Create**.</span></span>

   ![set key vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/create-key-vault.png)

3. <span data-ttu-id="6fce3-125">You now have a key vault.</span><span class="sxs-lookup"><span data-stu-id="6fce3-125">You now have a key vault.</span></span> <span data-ttu-id="6fce3-126">Select that key vault.</span><span class="sxs-lookup"><span data-stu-id="6fce3-126">Select that key vault.</span></span>

4. <span data-ttu-id="6fce3-127">In the key vault blade, select **Secrets**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-127">In the key vault blade, select **Secrets**.</span></span>

   ![select secrets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/select-secret.png)

5. <span data-ttu-id="6fce3-129">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-129">Select **Add**.</span></span>

   ![select add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/add-secret.png)

6. <span data-ttu-id="6fce3-131">Select **Manual** for upload options.</span><span class="sxs-lookup"><span data-stu-id="6fce3-131">Select **Manual** for upload options.</span></span> <span data-ttu-id="6fce3-132">Provide a name and value for secret.</span><span class="sxs-lookup"><span data-stu-id="6fce3-132">Provide a name and value for secret.</span></span> <span data-ttu-id="6fce3-133">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-133">Select **Create**.</span></span>

   ![provide secret](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/provide-secret.png)

<span data-ttu-id="6fce3-135">You have created your key vault and secret.</span><span class="sxs-lookup"><span data-stu-id="6fce3-135">You have created your key vault and secret.</span></span>

## <a name="enable-access-to-the-secret"></a><span data-ttu-id="6fce3-136">Enable access to the secret</span><span class="sxs-lookup"><span data-stu-id="6fce3-136">Enable access to the secret</span></span>

<span data-ttu-id="6fce3-137">Whether you are using a new key vault or an existing one, ensure that the user deploying the template can access the secret.</span><span class="sxs-lookup"><span data-stu-id="6fce3-137">Whether you are using a new key vault or an existing one, ensure that the user deploying the template can access the secret.</span></span> <span data-ttu-id="6fce3-138">The user deploying a template that references a secret must have the `Microsoft.KeyVault/vaults/deploy/action` permission for the key vault.</span><span class="sxs-lookup"><span data-stu-id="6fce3-138">The user deploying a template that references a secret must have the `Microsoft.KeyVault/vaults/deploy/action` permission for the key vault.</span></span> <span data-ttu-id="6fce3-139">The [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span><span class="sxs-lookup"><span data-stu-id="6fce3-139">The [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="6fce3-140">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add the user to that role.</span><span class="sxs-lookup"><span data-stu-id="6fce3-140">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add the user to that role.</span></span> <span data-ttu-id="6fce3-141">Also, you must grant Resource Manager the ability to access the key vault during deployment.</span><span class="sxs-lookup"><span data-stu-id="6fce3-141">Also, you must grant Resource Manager the ability to access the key vault during deployment.</span></span>

<span data-ttu-id="6fce3-142">You can check or perform these steps through the portal.</span><span class="sxs-lookup"><span data-stu-id="6fce3-142">You can check or perform these steps through the portal.</span></span>

1. <span data-ttu-id="6fce3-143">Select **Access control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-143">Select **Access control (IAM)**.</span></span>

   ![select access control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/select-access-control.png)

2. <span data-ttu-id="6fce3-145">If the account you intend to use for deploying templates is not already an Owner or Contributor (or added to a custom role that grants `Microsoft.KeyVault/vaults/deploy/action` permission), select **Add**</span><span class="sxs-lookup"><span data-stu-id="6fce3-145">If the account you intend to use for deploying templates is not already an Owner or Contributor (or added to a custom role that grants `Microsoft.KeyVault/vaults/deploy/action` permission), select **Add**</span></span>

   ![add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/add-user.png)

3. <span data-ttu-id="6fce3-147">Select the Contributor or Owner role, and search for the identity to assign to that role.</span><span class="sxs-lookup"><span data-stu-id="6fce3-147">Select the Contributor or Owner role, and search for the identity to assign to that role.</span></span> <span data-ttu-id="6fce3-148">Select **Okay** to complete adding the identity to the role.</span><span class="sxs-lookup"><span data-stu-id="6fce3-148">Select **Okay** to complete adding the identity to the role.</span></span>

   ![add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/search-user.png)

4. <span data-ttu-id="6fce3-150">To enable access from a template during deployment, select **Advanced access control**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-150">To enable access from a template during deployment, select **Advanced access control**.</span></span> <span data-ttu-id="6fce3-151">Select the option **Enable access to Azure Resource Manager for template deployment**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-151">Select the option **Enable access to Azure Resource Manager for template deployment**.</span></span>

   ![enable template access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-keyvault-parameter/select-template-access.png)

## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="6fce3-153">Reference a secret with static id</span><span class="sxs-lookup"><span data-stu-id="6fce3-153">Reference a secret with static id</span></span>

<span data-ttu-id="6fce3-154">You reference the secret from within a **parameters file (not the template)** that passes values to your template.</span><span class="sxs-lookup"><span data-stu-id="6fce3-154">You reference the secret from within a **parameters file (not the template)** that passes values to your template.</span></span> <span data-ttu-id="6fce3-155">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span><span class="sxs-lookup"><span data-stu-id="6fce3-155">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span></span> <span data-ttu-id="6fce3-156">In the following example, the key vault secret must already exist, and you provide a static value for its resource ID.</span><span class="sxs-lookup"><span data-stu-id="6fce3-156">In the following example, the key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "sqlsvrAdminLoginPassword": {
        "reference": {
          "keyVault": {
            "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
          },
          "secretName": "adminPassword"
        }
      },
      "sqlsvrAdminLogin": {
        "value": "exampleadmin"
      }
    }
}
```

<span data-ttu-id="6fce3-157">In the template, the parameter that accepts the secret should be a **securestring**.</span><span class="sxs-lookup"><span data-stu-id="6fce3-157">In the template, the parameter that accepts the secret should be a **securestring**.</span></span> <span data-ttu-id="6fce3-158">The following example shows the relevant sections of a template that deploys a SQL server that requires an administrator password.</span><span class="sxs-lookup"><span data-stu-id="6fce3-158">The following example shows the relevant sections of a template that deploys a SQL server that requires an administrator password.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "sqlsvrAdminLogin": {
            "type": "string",
            "minLength": 4
        },
        "sqlsvrAdminLoginPassword": {
            "type": "securestring"
        },
        ...
    },
    "resources": [
        {
          "name": "[variables('sqlsvrName')]",
          "type": "Microsoft.Sql/servers",
          "location": "[resourceGroup().location]",
          "apiVersion": "2014-04-01-preview",
          "properties": {
              "administratorLogin": "[parameters('sqlsvrAdminLogin')]",
              "administratorLoginPassword": "[parameters('sqlsvrAdminLoginPassword')]"
          },
          ...
        }
    ],
    "variables": {
        "sqlsvrName": "[concat('sqlsvr', uniqueString(resourceGroup().id))]"
    },
    "outputs": { }
}
```



## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="6fce3-159">Reference a secret with dynamic id</span><span class="sxs-lookup"><span data-stu-id="6fce3-159">Reference a secret with dynamic id</span></span>

<span data-ttu-id="6fce3-160">The previous section showed how to pass a static resource ID for the key vault secret.</span><span class="sxs-lookup"><span data-stu-id="6fce3-160">The previous section showed how to pass a static resource ID for the key vault secret.</span></span> <span data-ttu-id="6fce3-161">However, in some scenarios, you need to reference a key vault secret that varies based on the current deployment.</span><span class="sxs-lookup"><span data-stu-id="6fce3-161">However, in some scenarios, you need to reference a key vault secret that varies based on the current deployment.</span></span> <span data-ttu-id="6fce3-162">In that case, you cannot hard-code the resource ID in the parameters file.</span><span class="sxs-lookup"><span data-stu-id="6fce3-162">In that case, you cannot hard-code the resource ID in the parameters file.</span></span> <span data-ttu-id="6fce3-163">Unfortunately, you cannot dynamically generate the resource ID in the parameters file because template expressions are not permitted in the parameters file.</span><span class="sxs-lookup"><span data-stu-id="6fce3-163">Unfortunately, you cannot dynamically generate the resource ID in the parameters file because template expressions are not permitted in the parameters file.</span></span>

<span data-ttu-id="6fce3-164">To dynamically generate the resource ID for a key vault secret, you must move the resource that needs the secret into a nested template.</span><span class="sxs-lookup"><span data-stu-id="6fce3-164">To dynamically generate the resource ID for a key vault secret, you must move the resource that needs the secret into a nested template.</span></span> <span data-ttu-id="6fce3-165">In your master template, you add the nested template and pass in a parameter that contains the dynamically generated resource ID.</span><span class="sxs-lookup"><span data-stu-id="6fce3-165">In your master template, you add the nested template and pass in a parameter that contains the dynamically generated resource ID.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a><span data-ttu-id="6fce3-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="6fce3-166">Next steps</span></span>
* <span data-ttu-id="6fce3-167">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6fce3-167">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="6fce3-168">For information about using a key vault with a Virtual Machine, see [Security considerations for Azure Resource Manager](best-practices-resource-manager-security.md).</span><span class="sxs-lookup"><span data-stu-id="6fce3-168">For information about using a key vault with a Virtual Machine, see [Security considerations for Azure Resource Manager](best-practices-resource-manager-security.md).</span></span>
* <span data-ttu-id="6fce3-169">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="6fce3-169">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>










