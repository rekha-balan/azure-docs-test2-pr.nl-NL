---
title: Create an Azure Resource Manager template for deploying an encrypted storage account | Microsoft Docs
description: Use Visual Studio Code to create a template for deploying an encrypted storage account.
services: azure-resource-manager
documentationcenter: ''
author: mumian
manager: dougeby
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/07/2018
ms.topic: tutorial
ms.author: jgao
ms.openlocfilehash: aec2db760fcde27bfd61d3b49ae9805861c64d94
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871120"
---
# <a name="tutorial-create-an-azure-resource-manager-template-for-deploying-an-encrypted-storage-account"></a><span data-ttu-id="0a374-103">Tutorial: create an Azure Resource Manager template for deploying an encrypted storage account</span><span class="sxs-lookup"><span data-stu-id="0a374-103">Tutorial: create an Azure Resource Manager template for deploying an encrypted storage account</span></span>

<span data-ttu-id="0a374-104">Learn how to find information to complete an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="0a374-104">Learn how to find information to complete an Azure Resource Manager template.</span></span>

<span data-ttu-id="0a374-105">In this tutorial, you use a base template from Azure Quickstart templates to create an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="0a374-105">In this tutorial, you use a base template from Azure Quickstart templates to create an Azure Storage account.</span></span>  <span data-ttu-id="0a374-106">Using template reference documentation, you customize the base template to create an encrypted storage account.</span><span class="sxs-lookup"><span data-stu-id="0a374-106">Using template reference documentation, you customize the base template to create an encrypted storage account.</span></span>

<span data-ttu-id="0a374-107">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="0a374-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a374-108">Open a Quickstart template</span><span class="sxs-lookup"><span data-stu-id="0a374-108">Open a Quickstart template</span></span>
> * <span data-ttu-id="0a374-109">Understand the template</span><span class="sxs-lookup"><span data-stu-id="0a374-109">Understand the template</span></span>
> * <span data-ttu-id="0a374-110">Edit the template</span><span class="sxs-lookup"><span data-stu-id="0a374-110">Edit the template</span></span>
> * <span data-ttu-id="0a374-111">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="0a374-111">Deploy the template</span></span>

<span data-ttu-id="0a374-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="0a374-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a374-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a374-113">Prerequisites</span></span>

<span data-ttu-id="0a374-114">To complete this article, you need:</span><span class="sxs-lookup"><span data-stu-id="0a374-114">To complete this article, you need:</span></span>

* <span data-ttu-id="0a374-115">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="0a374-115">[Visual Studio Code](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="0a374-116">Resource Manager Tools extension.</span><span class="sxs-lookup"><span data-stu-id="0a374-116">Resource Manager Tools extension.</span></span> <span data-ttu-id="0a374-117">To install, see [Install the Resource Manager Tools extension](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="0a374-117">To install, see [Install the Resource Manager Tools extension](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).</span></span>

## <a name="open-a-quickstart-template"></a><span data-ttu-id="0a374-118">Open a Quickstart template</span><span class="sxs-lookup"><span data-stu-id="0a374-118">Open a Quickstart template</span></span>

<span data-ttu-id="0a374-119">The template used in this quickstart is called [Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/).</span><span class="sxs-lookup"><span data-stu-id="0a374-119">The template used in this quickstart is called [Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/).</span></span> <span data-ttu-id="0a374-120">The template defines an Azure Storage account resource.</span><span class="sxs-lookup"><span data-stu-id="0a374-120">The template defines an Azure Storage account resource.</span></span>

1. <span data-ttu-id="0a374-121">From Visual Studio Code, select **File**>**Open File**.</span><span class="sxs-lookup"><span data-stu-id="0a374-121">From Visual Studio Code, select **File**>**Open File**.</span></span>
2. <span data-ttu-id="0a374-122">In **File name**, paste the following URL:</span><span class="sxs-lookup"><span data-stu-id="0a374-122">In **File name**, paste the following URL:</span></span>

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
    ```
3. <span data-ttu-id="0a374-123">Select **Open** to open the file.</span><span class="sxs-lookup"><span data-stu-id="0a374-123">Select **Open** to open the file.</span></span>
4. <span data-ttu-id="0a374-124">Select **File**>**Save As** to save the file as **azuredeploy.json** to your local computer.</span><span class="sxs-lookup"><span data-stu-id="0a374-124">Select **File**>**Save As** to save the file as **azuredeploy.json** to your local computer.</span></span>

## <a name="understand-the-format"></a><span data-ttu-id="0a374-125">Understand the format</span><span class="sxs-lookup"><span data-stu-id="0a374-125">Understand the format</span></span>

<span data-ttu-id="0a374-126">From VS Code, collapse the template to the root level.</span><span class="sxs-lookup"><span data-stu-id="0a374-126">From VS Code, collapse the template to the root level.</span></span> <span data-ttu-id="0a374-127">You have the simplest structure with the following elements:</span><span class="sxs-lookup"><span data-stu-id="0a374-127">You have the simplest structure with the following elements:</span></span>

![Resource Manager template simplest structure](./media/resource-manager-tutorial-create-encrypted-storage-accounts/resource-manager-template-simplest-structure.png)

* <span data-ttu-id="0a374-129">**$schema**: specify the location of the JSON schema file that describes the version of the template language.</span><span class="sxs-lookup"><span data-stu-id="0a374-129">**$schema**: specify the location of the JSON schema file that describes the version of the template language.</span></span>
* <span data-ttu-id="0a374-130">**contentVersion**: specify any value for this element to document significant changes in your template.</span><span class="sxs-lookup"><span data-stu-id="0a374-130">**contentVersion**: specify any value for this element to document significant changes in your template.</span></span>
* <span data-ttu-id="0a374-131">**parameters**: specify the values that are provided when deployment is executed to customize resource deployment.</span><span class="sxs-lookup"><span data-stu-id="0a374-131">**parameters**: specify the values that are provided when deployment is executed to customize resource deployment.</span></span>
* <span data-ttu-id="0a374-132">**variables**: specify the values that are used as JSON fragments in the template to simplify template language expressions.</span><span class="sxs-lookup"><span data-stu-id="0a374-132">**variables**: specify the values that are used as JSON fragments in the template to simplify template language expressions.</span></span>
* <span data-ttu-id="0a374-133">**resources**: specify the resource types that are deployed or updated in a resource group.</span><span class="sxs-lookup"><span data-stu-id="0a374-133">**resources**: specify the resource types that are deployed or updated in a resource group.</span></span>
* <span data-ttu-id="0a374-134">**outputs**: specify the values that are returned after deployment.</span><span class="sxs-lookup"><span data-stu-id="0a374-134">**outputs**: specify the values that are returned after deployment.</span></span>

## <a name="use-parameters-in-template"></a><span data-ttu-id="0a374-135">Use parameters in template</span><span class="sxs-lookup"><span data-stu-id="0a374-135">Use parameters in template</span></span>

<span data-ttu-id="0a374-136">Parameters enable you to customize the deployment by providing values that are tailored for a particular environment.</span><span class="sxs-lookup"><span data-stu-id="0a374-136">Parameters enable you to customize the deployment by providing values that are tailored for a particular environment.</span></span> <span data-ttu-id="0a374-137">You use the parameters defined in the template when setting values for the storage account.</span><span class="sxs-lookup"><span data-stu-id="0a374-137">You use the parameters defined in the template when setting values for the storage account.</span></span>

![Resource Manager template parameters](./media/resource-manager-tutorial-create-encrypted-storage-accounts/resource-manager-template-parameters.png)

<span data-ttu-id="0a374-139">In this template, two parameters are defined.</span><span class="sxs-lookup"><span data-stu-id="0a374-139">In this template, two parameters are defined.</span></span> <span data-ttu-id="0a374-140">Notice a template function is used in location.defaultValue:</span><span class="sxs-lookup"><span data-stu-id="0a374-140">Notice a template function is used in location.defaultValue:</span></span>

```json
"defaultValue": "[resourceGroup().location]",
```

<span data-ttu-id="0a374-141">The resourceGroup() function returns an object that represents the current resource group.</span><span class="sxs-lookup"><span data-stu-id="0a374-141">The resourceGroup() function returns an object that represents the current resource group.</span></span> <span data-ttu-id="0a374-142">For a list of template functions, see [Azure Resource Manager template functions](./resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="0a374-142">For a list of template functions, see [Azure Resource Manager template functions](./resource-group-template-functions.md).</span></span>

<span data-ttu-id="0a374-143">To use the parameters defined in the template:</span><span class="sxs-lookup"><span data-stu-id="0a374-143">To use the parameters defined in the template:</span></span>

```json
"location": "[parameters('location')]",
"name": "[parameters('storageAccountType')]"
```

## <a name="use-variables-in-template"></a><span data-ttu-id="0a374-144">Use variables in template</span><span class="sxs-lookup"><span data-stu-id="0a374-144">Use variables in template</span></span>

<span data-ttu-id="0a374-145">Variables allow you to construct values that can be used throughout your template.</span><span class="sxs-lookup"><span data-stu-id="0a374-145">Variables allow you to construct values that can be used throughout your template.</span></span> <span data-ttu-id="0a374-146">Variables help reducing the complexity of the templates.</span><span class="sxs-lookup"><span data-stu-id="0a374-146">Variables help reducing the complexity of the templates.</span></span>

![Resource Manager template variables](./media/resource-manager-tutorial-create-encrypted-storage-accounts/resource-manager-template-variables.png)

<span data-ttu-id="0a374-148">This template defines one variable *storageAccountName*.</span><span class="sxs-lookup"><span data-stu-id="0a374-148">This template defines one variable *storageAccountName*.</span></span> <span data-ttu-id="0a374-149">In the definition, two template functions are used:</span><span class="sxs-lookup"><span data-stu-id="0a374-149">In the definition, two template functions are used:</span></span>

- <span data-ttu-id="0a374-150">**concat()**: concatenates strings.</span><span class="sxs-lookup"><span data-stu-id="0a374-150">**concat()**: concatenates strings.</span></span> <span data-ttu-id="0a374-151">For more information, see [concat](./resource-group-template-functions-string.md#concat).</span><span class="sxs-lookup"><span data-stu-id="0a374-151">For more information, see [concat](./resource-group-template-functions-string.md#concat).</span></span>
- <span data-ttu-id="0a374-152">**uniqueString()**: creates a deterministic hash string based on the values provided as parameters.</span><span class="sxs-lookup"><span data-stu-id="0a374-152">**uniqueString()**: creates a deterministic hash string based on the values provided as parameters.</span></span> <span data-ttu-id="0a374-153">Each Azure storage account must have a unique name across of all Azure.</span><span class="sxs-lookup"><span data-stu-id="0a374-153">Each Azure storage account must have a unique name across of all Azure.</span></span> <span data-ttu-id="0a374-154">This function provides a unique string.</span><span class="sxs-lookup"><span data-stu-id="0a374-154">This function provides a unique string.</span></span> <span data-ttu-id="0a374-155">For more string functions, see [String functions](./resource-group-template-functions-string.md).</span><span class="sxs-lookup"><span data-stu-id="0a374-155">For more string functions, see [String functions](./resource-group-template-functions-string.md).</span></span>

<span data-ttu-id="0a374-156">To use the variable defined in the template:</span><span class="sxs-lookup"><span data-stu-id="0a374-156">To use the variable defined in the template:</span></span>

```json
"name": "[variables('storageAccountName')]"
```

## <a name="edit-the-template"></a><span data-ttu-id="0a374-157">Edit the template</span><span class="sxs-lookup"><span data-stu-id="0a374-157">Edit the template</span></span>

<span data-ttu-id="0a374-158">The goal of this tutorial is to define a template to create an encrypted storage account.</span><span class="sxs-lookup"><span data-stu-id="0a374-158">The goal of this tutorial is to define a template to create an encrypted storage account.</span></span>  <span data-ttu-id="0a374-159">The sample template only creates a basic unencrypted storage account.</span><span class="sxs-lookup"><span data-stu-id="0a374-159">The sample template only creates a basic unencrypted storage account.</span></span> <span data-ttu-id="0a374-160">To find the encryption-related configuration, you can use the template reference of Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="0a374-160">To find the encryption-related configuration, you can use the template reference of Azure Storage account.</span></span>

1. <span data-ttu-id="0a374-161">Browse to [Azure Templates](https://docs.microsoft.com/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="0a374-161">Browse to [Azure Templates](https://docs.microsoft.com/azure/templates/).</span></span>
2. <span data-ttu-id="0a374-162">In **Filter by title**, enter **storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="0a374-162">In **Filter by title**, enter **storage accounts**.</span></span>
3. <span data-ttu-id="0a374-163">Select **Reference/Template reference/Storage/Storage Accounts** as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0a374-163">Select **Reference/Template reference/Storage/Storage Accounts** as shown in the following screenshot:</span></span>

    ![Resource Manager template reference storage account](./media/resource-manager-tutorial-create-encrypted-storage-accounts/resource-manager-template-resources-reference-storage-accounts.png)

    <span data-ttu-id="0a374-165">resource-manager-template-resources-reference-storage-accounts</span><span class="sxs-lookup"><span data-stu-id="0a374-165">resource-manager-template-resources-reference-storage-accounts</span></span>
1. <span data-ttu-id="0a374-166">Explore the encryption-related information.</span><span class="sxs-lookup"><span data-stu-id="0a374-166">Explore the encryption-related information.</span></span>  
1. <span data-ttu-id="0a374-167">Inside the properties element of the storage account resource definition, add the following json:</span><span class="sxs-lookup"><span data-stu-id="0a374-167">Inside the properties element of the storage account resource definition, add the following json:</span></span>

    ```json
    "encryption": {
        "keySource": "Microsoft.Storage",
        "services": {
            "blob": {
                "enabled": true
            }
        }
    }
    ```
    <span data-ttu-id="0a374-168">This part enables the encryption function of the blob storage service.</span><span class="sxs-lookup"><span data-stu-id="0a374-168">This part enables the encryption function of the blob storage service.</span></span>

<span data-ttu-id="0a374-169">From Visual Studio Code, modify the template so that the final resources element looks like:</span><span class="sxs-lookup"><span data-stu-id="0a374-169">From Visual Studio Code, modify the template so that the final resources element looks like:</span></span>

![Resource Manager template encrypted storage account resources](./media/resource-manager-tutorial-create-encrypted-storage-accounts/resource-manager-template-encrypted-storage-resources.png)

## <a name="deploy-the-template"></a><span data-ttu-id="0a374-171">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="0a374-171">Deploy the template</span></span>

<span data-ttu-id="0a374-172">Refer to the [Deploy the template](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#deploy-the-template) section in the Visual Studio Code quickstart for the deployment procedure.</span><span class="sxs-lookup"><span data-stu-id="0a374-172">Refer to the [Deploy the template](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#deploy-the-template) section in the Visual Studio Code quickstart for the deployment procedure.</span></span>

<span data-ttu-id="0a374-173">The following screenshot shows the CLI command for listing the newly created storage account, which indicates encryption has been enabled for the blob storage.</span><span class="sxs-lookup"><span data-stu-id="0a374-173">The following screenshot shows the CLI command for listing the newly created storage account, which indicates encryption has been enabled for the blob storage.</span></span>

![Azure Resource Manager encrypted storage account](./media/resource-manager-tutorial-create-encrypted-storage-accounts/resource-manager-template-encrypted-storage-account.png)

## <a name="clean-up-resources"></a><span data-ttu-id="0a374-175">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0a374-175">Clean up resources</span></span>

<span data-ttu-id="0a374-176">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="0a374-176">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

1. <span data-ttu-id="0a374-177">From the Azure portal, select **Resource group** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="0a374-177">From the Azure portal, select **Resource group** from the left menu.</span></span>
2. <span data-ttu-id="0a374-178">Enter the resource group name in the **Filter by name** field.</span><span class="sxs-lookup"><span data-stu-id="0a374-178">Enter the resource group name in the **Filter by name** field.</span></span>
3. <span data-ttu-id="0a374-179">Select the resource group name.</span><span class="sxs-lookup"><span data-stu-id="0a374-179">Select the resource group name.</span></span>  <span data-ttu-id="0a374-180">You shall see a total of six resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="0a374-180">You shall see a total of six resources in the resource group.</span></span>
4. <span data-ttu-id="0a374-181">Select **Delete resource group** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="0a374-181">Select **Delete resource group** from the top menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a374-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a374-182">Next steps</span></span>

<span data-ttu-id="0a374-183">In this tutorial, you learned how to use template reference to customize an existing template.</span><span class="sxs-lookup"><span data-stu-id="0a374-183">In this tutorial, you learned how to use template reference to customize an existing template.</span></span> <span data-ttu-id="0a374-184">In the next tutorial, you learn how to use resource iteration to create multiple storage accounts.</span><span class="sxs-lookup"><span data-stu-id="0a374-184">In the next tutorial, you learn how to use resource iteration to create multiple storage accounts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a374-185">Create multiple instances</span><span class="sxs-lookup"><span data-stu-id="0a374-185">Create multiple instances</span></span>](./resource-manager-tutorial-create-multiple-instances.md)
