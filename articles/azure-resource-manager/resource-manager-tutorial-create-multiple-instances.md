---
title: Create multiple resource instances using Azure Resource Manager   | Microsoft Docs
description: Learn how to create an Azure Resource Manager template to create multiple Azure resource instances.
services: azure-resource-manager
documentationcenter: ''
author: mumian
manager: dougeby
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/10/2018
ms.topic: tutorial
ms.author: jgao
ms.openlocfilehash: 25729a355ad24527a0a40ee66ac6c9a44d710959
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969471"
---
# <a name="tutorial-create-multiple-resource-instances-using-resource-manager-templates"></a><span data-ttu-id="38da2-103">Tutorial: create multiple resource instances using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="38da2-103">Tutorial: create multiple resource instances using Resource Manager templates</span></span>

<span data-ttu-id="38da2-104">Learn how to iterate in your Azure Resource Manager template to create multiple instances of an Azure resource.</span><span class="sxs-lookup"><span data-stu-id="38da2-104">Learn how to iterate in your Azure Resource Manager template to create multiple instances of an Azure resource.</span></span> <span data-ttu-id="38da2-105">In the last tutorial, you modified an existing template to create an encrypted Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="38da2-105">In the last tutorial, you modified an existing template to create an encrypted Azure Storage account.</span></span> <span data-ttu-id="38da2-106">In this tutorial,  you modify the same template to create three storage account instances.</span><span class="sxs-lookup"><span data-stu-id="38da2-106">In this tutorial,  you modify the same template to create three storage account instances.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38da2-107">Open a quickstart template</span><span class="sxs-lookup"><span data-stu-id="38da2-107">Open a quickstart template</span></span>
> * <span data-ttu-id="38da2-108">Edit the template</span><span class="sxs-lookup"><span data-stu-id="38da2-108">Edit the template</span></span>
> * <span data-ttu-id="38da2-109">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="38da2-109">Deploy the template</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38da2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="38da2-110">Prerequisites</span></span>

<span data-ttu-id="38da2-111">To complete this article, you need:</span><span class="sxs-lookup"><span data-stu-id="38da2-111">To complete this article, you need:</span></span>

* <span data-ttu-id="38da2-112">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="38da2-112">[Visual Studio Code](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="38da2-113">Resource Manager Tools extension.</span><span class="sxs-lookup"><span data-stu-id="38da2-113">Resource Manager Tools extension.</span></span> <span data-ttu-id="38da2-114">To install, see [Install the Resource Manager Tools extension](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="38da2-114">To install, see [Install the Resource Manager Tools extension](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).</span></span>

## <a name="open-a-quickstart-template"></a><span data-ttu-id="38da2-115">Open a Quickstart template</span><span class="sxs-lookup"><span data-stu-id="38da2-115">Open a Quickstart template</span></span>

<span data-ttu-id="38da2-116">The template used in this quickstart is called [Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/).</span><span class="sxs-lookup"><span data-stu-id="38da2-116">The template used in this quickstart is called [Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/).</span></span> <span data-ttu-id="38da2-117">The template defines an Azure Storage account resource.</span><span class="sxs-lookup"><span data-stu-id="38da2-117">The template defines an Azure Storage account resource.</span></span>

1. <span data-ttu-id="38da2-118">From Visual Studio Code, select **File**>**Open File**.</span><span class="sxs-lookup"><span data-stu-id="38da2-118">From Visual Studio Code, select **File**>**Open File**.</span></span>
2. <span data-ttu-id="38da2-119">In **File name**, paste the following URL:</span><span class="sxs-lookup"><span data-stu-id="38da2-119">In **File name**, paste the following URL:</span></span>

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
    ```
3. <span data-ttu-id="38da2-120">Select **Open** to open the file.</span><span class="sxs-lookup"><span data-stu-id="38da2-120">Select **Open** to open the file.</span></span>
4. <span data-ttu-id="38da2-121">Select **File**>**Save As** to save the file as **azuredeploy.json** to your local computer.</span><span class="sxs-lookup"><span data-stu-id="38da2-121">Select **File**>**Save As** to save the file as **azuredeploy.json** to your local computer.</span></span>

## <a name="edit-the-template"></a><span data-ttu-id="38da2-122">Edit the template</span><span class="sxs-lookup"><span data-stu-id="38da2-122">Edit the template</span></span>

<span data-ttu-id="38da2-123">The goal of this tutorial is to use resource iteration to create three storage accounts.</span><span class="sxs-lookup"><span data-stu-id="38da2-123">The goal of this tutorial is to use resource iteration to create three storage accounts.</span></span>  <span data-ttu-id="38da2-124">The sample template only creates one storage account.</span><span class="sxs-lookup"><span data-stu-id="38da2-124">The sample template only creates one storage account.</span></span> 

<span data-ttu-id="38da2-125">From Visual Studio Code, make the following four changes:</span><span class="sxs-lookup"><span data-stu-id="38da2-125">From Visual Studio Code, make the following four changes:</span></span>

![Azure Resource Manager create multiple instances](./media/resource-manager-tutorial-create-multiple-instances/resource-manager-template-create-multiple-instances.png)

1. <span data-ttu-id="38da2-127">Add a `copy` element to the storage account resource definition.</span><span class="sxs-lookup"><span data-stu-id="38da2-127">Add a `copy` element to the storage account resource definition.</span></span> <span data-ttu-id="38da2-128">In the copy element, you specify the number of iterations and a name for this loop.</span><span class="sxs-lookup"><span data-stu-id="38da2-128">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="38da2-129">The count value must be a positive integer and can't exceed 800.</span><span class="sxs-lookup"><span data-stu-id="38da2-129">The count value must be a positive integer and can't exceed 800.</span></span>
2. <span data-ttu-id="38da2-130">The `copyIndex()` function returns the current iteration in the loop.</span><span class="sxs-lookup"><span data-stu-id="38da2-130">The `copyIndex()` function returns the current iteration in the loop.</span></span> <span data-ttu-id="38da2-131">`copyIndex()` is zero-based.</span><span class="sxs-lookup"><span data-stu-id="38da2-131">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="38da2-132">To offset the index value, you can pass a value in the copyIndex() function.</span><span class="sxs-lookup"><span data-stu-id="38da2-132">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="38da2-133">For example, *copyIndex(1)*.</span><span class="sxs-lookup"><span data-stu-id="38da2-133">For example, *copyIndex(1)*.</span></span>
3. <span data-ttu-id="38da2-134">Delete the **variables** element, because it is not used anymore.</span><span class="sxs-lookup"><span data-stu-id="38da2-134">Delete the **variables** element, because it is not used anymore.</span></span>
4. <span data-ttu-id="38da2-135">Delete the **outputs** element.</span><span class="sxs-lookup"><span data-stu-id="38da2-135">Delete the **outputs** element.</span></span>

<span data-ttu-id="38da2-136">The completed template looks like:</span><span class="sxs-lookup"><span data-stu-id="38da2-136">The completed template looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for all resources."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
      "apiVersion": "2018-02-01",
      "location": "[parameters('location')]",
      "sku": {
        "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage",
      "properties": {},
      "copy": {
        "name": "storagecopy",
        "count": 3
      }
    }
  ]
}
```

<span data-ttu-id="38da2-137">For more information about creating multiple instances, see [Deploy multiple instances of a resource or property in Azure Resource Manager Templates](./resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="38da2-137">For more information about creating multiple instances, see [Deploy multiple instances of a resource or property in Azure Resource Manager Templates](./resource-group-create-multiple.md)</span></span>

## <a name="deploy-the-template"></a><span data-ttu-id="38da2-138">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="38da2-138">Deploy the template</span></span>

<span data-ttu-id="38da2-139">Refer to the [Deploy the template](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#deploy-the-template) section in the Visual Studio Code quickstart for the deployment procedure.</span><span class="sxs-lookup"><span data-stu-id="38da2-139">Refer to the [Deploy the template](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#deploy-the-template) section in the Visual Studio Code quickstart for the deployment procedure.</span></span>

<span data-ttu-id="38da2-140">To list all three storage accounts, omit the --name parameter:</span><span class="sxs-lookup"><span data-stu-id="38da2-140">To list all three storage accounts, omit the --name parameter:</span></span>

# <a name="clitabcli"></a>[<span data-ttu-id="38da2-141">CLI</span><span class="sxs-lookup"><span data-stu-id="38da2-141">CLI</span></span>](#tab/CLI)
```cli
az storage account list --resource-group <ResourceGroupName>
```

# <a name="powershelltabpowershell"></a>[<span data-ttu-id="38da2-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38da2-142">PowerShell</span></span>](#tab/PowerShell)

```powershell
Get-AzureRmStorageAccount -ResourceGroupName <ResourceGroupName>
```

---

<span data-ttu-id="38da2-143">Compare the storage account names with the name definition in the template.</span><span class="sxs-lookup"><span data-stu-id="38da2-143">Compare the storage account names with the name definition in the template.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="38da2-144">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="38da2-144">Clean up resources</span></span>

<span data-ttu-id="38da2-145">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="38da2-145">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

1. <span data-ttu-id="38da2-146">From the Azure portal, select **Resource group** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="38da2-146">From the Azure portal, select **Resource group** from the left menu.</span></span>
2. <span data-ttu-id="38da2-147">Enter the resource group name in the **Filter by name** field.</span><span class="sxs-lookup"><span data-stu-id="38da2-147">Enter the resource group name in the **Filter by name** field.</span></span>
3. <span data-ttu-id="38da2-148">Select the resource group name.</span><span class="sxs-lookup"><span data-stu-id="38da2-148">Select the resource group name.</span></span>  <span data-ttu-id="38da2-149">You shall see a total of six resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="38da2-149">You shall see a total of six resources in the resource group.</span></span>
4. <span data-ttu-id="38da2-150">Select **Delete resource group** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="38da2-150">Select **Delete resource group** from the top menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38da2-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="38da2-151">Next steps</span></span>

<span data-ttu-id="38da2-152">In this tutorial, you learned how to create multiple storage account instances.</span><span class="sxs-lookup"><span data-stu-id="38da2-152">In this tutorial, you learned how to create multiple storage account instances.</span></span> <span data-ttu-id="38da2-153">So far, you have created one storage account or multiple storage account instances.</span><span class="sxs-lookup"><span data-stu-id="38da2-153">So far, you have created one storage account or multiple storage account instances.</span></span> <span data-ttu-id="38da2-154">In the next tutorial, you develop a template with multiple resources and multiple resource types.</span><span class="sxs-lookup"><span data-stu-id="38da2-154">In the next tutorial, you develop a template with multiple resources and multiple resource types.</span></span> <span data-ttu-id="38da2-155">Some of the resources have dependent resources.</span><span class="sxs-lookup"><span data-stu-id="38da2-155">Some of the resources have dependent resources.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38da2-156">Create dependent resources</span><span class="sxs-lookup"><span data-stu-id="38da2-156">Create dependent resources</span></span>](./resource-manager-tutorial-create-templates-with-dependent-resources.md)
