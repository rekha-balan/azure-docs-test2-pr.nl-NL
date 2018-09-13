---
title: Use Azure Key Vault with Managed Applications | Microsoft Docs
description: Shows how to use access secrets in Azure Key Vault when deploying Managed Applications
services: managed-applications
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.date: 07/11/2018
ms.author: tomfitz
ms.openlocfilehash: f091ba44a3170dcc4141829f2f4105d6e7993cdf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869828"
---
# <a name="access-key-vault-secret-when-deploying-azure-managed-applications"></a><span data-ttu-id="a5d90-103">Access Key Vault secret when deploying Azure Managed Applications</span><span class="sxs-lookup"><span data-stu-id="a5d90-103">Access Key Vault secret when deploying Azure Managed Applications</span></span>

<span data-ttu-id="a5d90-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5d90-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="a5d90-105">To access the Key Vault when deploying Managed Applications, you must grant access to the **Appliance Resource Provider** service principal.</span><span class="sxs-lookup"><span data-stu-id="a5d90-105">To access the Key Vault when deploying Managed Applications, you must grant access to the **Appliance Resource Provider** service principal.</span></span> <span data-ttu-id="a5d90-106">This article describes how to configure the Key Vault to work with Managed Applications.</span><span class="sxs-lookup"><span data-stu-id="a5d90-106">This article describes how to configure the Key Vault to work with Managed Applications.</span></span>

## <a name="enable-template-deployment"></a><span data-ttu-id="a5d90-107">Enable template deployment</span><span class="sxs-lookup"><span data-stu-id="a5d90-107">Enable template deployment</span></span>

1. <span data-ttu-id="a5d90-108">In the portal, select your Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a5d90-108">In the portal, select your Key Vault.</span></span>

1. <span data-ttu-id="a5d90-109">Select **Access policies**.</span><span class="sxs-lookup"><span data-stu-id="a5d90-109">Select **Access policies**.</span></span>   

   ![Select access policies](./media/key-vault-access/select-access-policies.png)

1. <span data-ttu-id="a5d90-111">Select **Click to show advanced access policies**.</span><span class="sxs-lookup"><span data-stu-id="a5d90-111">Select **Click to show advanced access policies**.</span></span>

   ![Show advanced access policies](./media/key-vault-access/advanced.png)

1. <span data-ttu-id="a5d90-113">Select **Enable access to Azure Resource Manager for template deployment**.</span><span class="sxs-lookup"><span data-stu-id="a5d90-113">Select **Enable access to Azure Resource Manager for template deployment**.</span></span> <span data-ttu-id="a5d90-114">Then, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5d90-114">Then, select **Save**.</span></span>

   ![Enable template deployment](./media/key-vault-access/enable-template.png)

## <a name="add-service-as-contributor"></a><span data-ttu-id="a5d90-116">Add service as contributor</span><span class="sxs-lookup"><span data-stu-id="a5d90-116">Add service as contributor</span></span>

1. <span data-ttu-id="a5d90-117">Select **Access control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="a5d90-117">Select **Access control (IAM)**.</span></span>

   ![Select access control](./media/key-vault-access/access-control.png)

1. <span data-ttu-id="a5d90-119">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="a5d90-119">Select **Add**.</span></span>

   ![Select add](./media/key-vault-access/add-access-control.png)

1. <span data-ttu-id="a5d90-121">Select **Contributor** for the role.</span><span class="sxs-lookup"><span data-stu-id="a5d90-121">Select **Contributor** for the role.</span></span> <span data-ttu-id="a5d90-122">Search for **Appliance Resource Provider** and select it from the available options.</span><span class="sxs-lookup"><span data-stu-id="a5d90-122">Search for **Appliance Resource Provider** and select it from the available options.</span></span>

   ![Search for provider](./media/key-vault-access/search-provider.png)

1. <span data-ttu-id="a5d90-124">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5d90-124">Select **Save**.</span></span>

## <a name="reference-key-vault-secret"></a><span data-ttu-id="a5d90-125">Reference Key Vault secret</span><span class="sxs-lookup"><span data-stu-id="a5d90-125">Reference Key Vault secret</span></span>

<span data-ttu-id="a5d90-126">To pass a secret from a Key Vault to a template in your Managed Application, you must use a [linked template](../azure-resource-manager/resource-group-linked-templates.md) and reference the Key Vault in the parameters for the linked template.</span><span class="sxs-lookup"><span data-stu-id="a5d90-126">To pass a secret from a Key Vault to a template in your Managed Application, you must use a [linked template](../azure-resource-manager/resource-group-linked-templates.md) and reference the Key Vault in the parameters for the linked template.</span></span> <span data-ttu-id="a5d90-127">Provide the resource ID of the Key Vault and the name of the secret.</span><span class="sxs-lookup"><span data-stu-id="a5d90-127">Provide the resource ID of the Key Vault and the name of the secret.</span></span>

```json
"resources": [{
  "apiVersion": "2015-01-01",
  "name": "linkedTemplate",
  "type": "Microsoft.Resources/deployments",
  "properties": {
    "mode": "incremental",
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/keyvaultparameter/sqlserver.json",
      "contentVersion": "1.0.0.0"
    },
    "parameters": {
      "adminPassword": {
        "reference": {
          "keyVault": {
            "id": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.KeyVault/vaults/<key-vault-name>"
          },
          "secretName": "<secret-name>"
        }
      },
      "adminLogin": { "value": "[parameters('adminLogin')]" },
      "sqlServerName": {"value": "[parameters('sqlServerName')]"}
    }
  }
}],
```

## <a name="next-steps"></a><span data-ttu-id="a5d90-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5d90-128">Next steps</span></span>

<span data-ttu-id="a5d90-129">You've configured your Key Vault to be accessible during deployment of a Managed Application.</span><span class="sxs-lookup"><span data-stu-id="a5d90-129">You've configured your Key Vault to be accessible during deployment of a Managed Application.</span></span>

* <span data-ttu-id="a5d90-130">For information about passing a value from a Key Vault as a template parameter, see [Use Azure Key Vault to pass secure parameter value during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="a5d90-130">For information about passing a value from a Key Vault as a template parameter, see [Use Azure Key Vault to pass secure parameter value during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>
* <span data-ttu-id="a5d90-131">For managed application examples, see [Sample projects for Azure managed applications](sample-projects.md).</span><span class="sxs-lookup"><span data-stu-id="a5d90-131">For managed application examples, see [Sample projects for Azure managed applications](sample-projects.md).</span></span>
* <span data-ttu-id="a5d90-132">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5d90-132">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>