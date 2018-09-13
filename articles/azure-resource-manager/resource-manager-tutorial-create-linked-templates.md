---
title: Create linked Azure Resource Manager templates | Microsoft Docs
description: Learn how to create linked Azure Resource Manager templates for creating virtual machine
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
ms.openlocfilehash: 1fc4b439ebff03be1f21321861045ccdbbbd178e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966401"
---
# <a name="tutorial-create-linked-azure-resource-manager-templates"></a><span data-ttu-id="5b504-103">Tutorial: create linked Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="5b504-103">Tutorial: create linked Azure Resource Manager templates</span></span>

<span data-ttu-id="5b504-104">Learn how to create linked Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="5b504-104">Learn how to create linked Azure Resource Manager templates.</span></span> <span data-ttu-id="5b504-105">Using linked templates, you can have one template call another template.</span><span class="sxs-lookup"><span data-stu-id="5b504-105">Using linked templates, you can have one template call another template.</span></span> <span data-ttu-id="5b504-106">It is great for modularizing templates.</span><span class="sxs-lookup"><span data-stu-id="5b504-106">It is great for modularizing templates.</span></span> <span data-ttu-id="5b504-107">In this tutorial, you use the same template used in [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md), which creates a virtual machine, a virtual network, and other dependent resource including a storage account.</span><span class="sxs-lookup"><span data-stu-id="5b504-107">In this tutorial, you use the same template used in [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md), which creates a virtual machine, a virtual network, and other dependent resource including a storage account.</span></span> <span data-ttu-id="5b504-108">You separate the storage account resource to a linked template.</span><span class="sxs-lookup"><span data-stu-id="5b504-108">You separate the storage account resource to a linked template.</span></span>

<span data-ttu-id="5b504-109">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="5b504-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5b504-110">Open a quickstart template</span><span class="sxs-lookup"><span data-stu-id="5b504-110">Open a quickstart template</span></span>
> * <span data-ttu-id="5b504-111">Create the linked template</span><span class="sxs-lookup"><span data-stu-id="5b504-111">Create the linked template</span></span>
> * <span data-ttu-id="5b504-112">Upload the linked template</span><span class="sxs-lookup"><span data-stu-id="5b504-112">Upload the linked template</span></span>
> * <span data-ttu-id="5b504-113">Link to the linked template</span><span class="sxs-lookup"><span data-stu-id="5b504-113">Link to the linked template</span></span>
> * <span data-ttu-id="5b504-114">Configure dependency</span><span class="sxs-lookup"><span data-stu-id="5b504-114">Configure dependency</span></span>
> * <span data-ttu-id="5b504-115">Get values from linked template</span><span class="sxs-lookup"><span data-stu-id="5b504-115">Get values from linked template</span></span>
> * <span data-ttu-id="5b504-116">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="5b504-116">Deploy the template</span></span>

<span data-ttu-id="5b504-117">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="5b504-117">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b504-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5b504-118">Prerequisites</span></span>

<span data-ttu-id="5b504-119">To complete this article, you need:</span><span class="sxs-lookup"><span data-stu-id="5b504-119">To complete this article, you need:</span></span>

* <span data-ttu-id="5b504-120">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="5b504-120">[Visual Studio Code](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="5b504-121">Resource Manager Tools extension.</span><span class="sxs-lookup"><span data-stu-id="5b504-121">Resource Manager Tools extension.</span></span>  <span data-ttu-id="5b504-122">See [Install the extension ](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="5b504-122">See [Install the extension ](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).</span></span>
* <span data-ttu-id="5b504-123">Complete [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md).</span><span class="sxs-lookup"><span data-stu-id="5b504-123">Complete [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md).</span></span>

## <a name="open-a-quickstart-template"></a><span data-ttu-id="5b504-124">Open a Quickstart template</span><span class="sxs-lookup"><span data-stu-id="5b504-124">Open a Quickstart template</span></span>

<span data-ttu-id="5b504-125">Azure QuickStart Templates is a repository for Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="5b504-125">Azure QuickStart Templates is a repository for Resource Manager templates.</span></span> <span data-ttu-id="5b504-126">Instead of creating a template from scratch, you can find a sample template and customize it.</span><span class="sxs-lookup"><span data-stu-id="5b504-126">Instead of creating a template from scratch, you can find a sample template and customize it.</span></span> <span data-ttu-id="5b504-127">The template used in this tutorial is called [Deploy a simple Windows VM](https://azure.microsoft.com/resources/templates/101-vm-simple-windows/).</span><span class="sxs-lookup"><span data-stu-id="5b504-127">The template used in this tutorial is called [Deploy a simple Windows VM](https://azure.microsoft.com/resources/templates/101-vm-simple-windows/).</span></span> <span data-ttu-id="5b504-128">This is the same template used in [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md).</span><span class="sxs-lookup"><span data-stu-id="5b504-128">This is the same template used in [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md).</span></span> <span data-ttu-id="5b504-129">You save two copies of the same template to be used as:</span><span class="sxs-lookup"><span data-stu-id="5b504-129">You save two copies of the same template to be used as:</span></span>

- <span data-ttu-id="5b504-130">**The main template**: create all the resources except the storage account.</span><span class="sxs-lookup"><span data-stu-id="5b504-130">**The main template**: create all the resources except the storage account.</span></span>
- <span data-ttu-id="5b504-131">**The linked template**: create the storage account.</span><span class="sxs-lookup"><span data-stu-id="5b504-131">**The linked template**: create the storage account.</span></span>

1. <span data-ttu-id="5b504-132">From Visual Studio Code, select **File**>**Open File**.</span><span class="sxs-lookup"><span data-stu-id="5b504-132">From Visual Studio Code, select **File**>**Open File**.</span></span>
2. <span data-ttu-id="5b504-133">In **File name**, paste the following URL:</span><span class="sxs-lookup"><span data-stu-id="5b504-133">In **File name**, paste the following URL:</span></span>

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json
    ```
3. <span data-ttu-id="5b504-134">Select **Open** to open the file.</span><span class="sxs-lookup"><span data-stu-id="5b504-134">Select **Open** to open the file.</span></span>
4. <span data-ttu-id="5b504-135">Select **File**>**Save As** to save a copy of the file to your local computer with the name **azuredeploy.json**.</span><span class="sxs-lookup"><span data-stu-id="5b504-135">Select **File**>**Save As** to save a copy of the file to your local computer with the name **azuredeploy.json**.</span></span>
5. <span data-ttu-id="5b504-136">Select **File**>**Save As** to create another copy of the file with the name **linkedTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="5b504-136">Select **File**>**Save As** to create another copy of the file with the name **linkedTemplate.json**.</span></span>

## <a name="create-the-linked-template"></a><span data-ttu-id="5b504-137">Create the linked template</span><span class="sxs-lookup"><span data-stu-id="5b504-137">Create the linked template</span></span>

<span data-ttu-id="5b504-138">The linked template creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="5b504-138">The linked template creates a storage account.</span></span> <span data-ttu-id="5b504-139">The linked template is almost identical to the standalone template that creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="5b504-139">The linked template is almost identical to the standalone template that creates a storage account.</span></span> <span data-ttu-id="5b504-140">In this tutorial, the linked template needs to pass a value back to the main template.</span><span class="sxs-lookup"><span data-stu-id="5b504-140">In this tutorial, the linked template needs to pass a value back to the main template.</span></span> <span data-ttu-id="5b504-141">This value is defined in the `outputs` element.</span><span class="sxs-lookup"><span data-stu-id="5b504-141">This value is defined in the `outputs` element.</span></span>

1. <span data-ttu-id="5b504-142">Open linkedTemplate.json in Visual Studio Code if it is not opened.</span><span class="sxs-lookup"><span data-stu-id="5b504-142">Open linkedTemplate.json in Visual Studio Code if it is not opened.</span></span>
2. <span data-ttu-id="5b504-143">Make the following changes:</span><span class="sxs-lookup"><span data-stu-id="5b504-143">Make the following changes:</span></span>

    - <span data-ttu-id="5b504-144">Remove all the resources except the storage account.</span><span class="sxs-lookup"><span data-stu-id="5b504-144">Remove all the resources except the storage account.</span></span> <span data-ttu-id="5b504-145">You remove a total of four resources.</span><span class="sxs-lookup"><span data-stu-id="5b504-145">You remove a total of four resources.</span></span>
    - <span data-ttu-id="5b504-146">Update the **outputs** element, so it looks like:</span><span class="sxs-lookup"><span data-stu-id="5b504-146">Update the **outputs** element, so it looks like:</span></span>

        ```json
        "outputs": {
            "storageUri": {
                "type": "string",
                "value": "[reference(parameters('storageAccountName')).primaryEndpoints.blob]"
              }
        }
        ```
        <span data-ttu-id="5b504-147">**storageUri** is required by the virtual machine resource definition in the main template.</span><span class="sxs-lookup"><span data-stu-id="5b504-147">**storageUri** is required by the virtual machine resource definition in the main template.</span></span>  <span data-ttu-id="5b504-148">You pass the value back to the main template as an output value.</span><span class="sxs-lookup"><span data-stu-id="5b504-148">You pass the value back to the main template as an output value.</span></span>
    - <span data-ttu-id="5b504-149">Remove the parameters that are never used.</span><span class="sxs-lookup"><span data-stu-id="5b504-149">Remove the parameters that are never used.</span></span> <span data-ttu-id="5b504-150">These parameters have a green wave line underneath them.</span><span class="sxs-lookup"><span data-stu-id="5b504-150">These parameters have a green wave line underneath them.</span></span> <span data-ttu-id="5b504-151">You shall only have one parameter left called **location**.</span><span class="sxs-lookup"><span data-stu-id="5b504-151">You shall only have one parameter left called **location**.</span></span>
    - <span data-ttu-id="5b504-152">Remove the **variables** element.</span><span class="sxs-lookup"><span data-stu-id="5b504-152">Remove the **variables** element.</span></span> <span data-ttu-id="5b504-153">They are no needed in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b504-153">They are no needed in this tutorial.</span></span>
    - <span data-ttu-id="5b504-154">Add a parameter called **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="5b504-154">Add a parameter called **storageAccountName**.</span></span> <span data-ttu-id="5b504-155">The storage account name is passed from the main template to the linked template as a parameter.</span><span class="sxs-lookup"><span data-stu-id="5b504-155">The storage account name is passed from the main template to the linked template as a parameter.</span></span>

    <span data-ttu-id="5b504-156">When you are done, the template shall look like:</span><span class="sxs-lookup"><span data-stu-id="5b504-156">When you are done, the template shall look like:</span></span>

    ```json
    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
          "storageAccountName":{
            "type": "string",
            "metadata": {
              "description": "Azure Storage account name."
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
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2016-01-01",
            "location": "[parameters('location')]",
            "sku": {
              "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
          }
        ],
        "outputs": {
            "storageUri": {
                "type": "string",
                "value": "[reference(parameters('storageAccountName')).primaryEndpoints.blob]"
              }
        }
    }
    ```
3. <span data-ttu-id="5b504-157">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="5b504-157">Save the changes.</span></span>

## <a name="upload-the-linked-template"></a><span data-ttu-id="5b504-158">Upload the linked template</span><span class="sxs-lookup"><span data-stu-id="5b504-158">Upload the linked template</span></span>

<span data-ttu-id="5b504-159">The templates need to be accessible from where you run the deployment.</span><span class="sxs-lookup"><span data-stu-id="5b504-159">The templates need to be accessible from where you run the deployment.</span></span> <span data-ttu-id="5b504-160">This location could be an Azure storage account, Github, or Dropbox.</span><span class="sxs-lookup"><span data-stu-id="5b504-160">This location could be an Azure storage account, Github, or Dropbox.</span></span> <span data-ttu-id="5b504-161">If your templates contain sensitive information, make sure you protect access to them.</span><span class="sxs-lookup"><span data-stu-id="5b504-161">If your templates contain sensitive information, make sure you protect access to them.</span></span> <span data-ttu-id="5b504-162">In this tutorial, you use the Cloud shell deployment method as you used in [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md).</span><span class="sxs-lookup"><span data-stu-id="5b504-162">In this tutorial, you use the Cloud shell deployment method as you used in [Tutorial: create multiple resource instances using Resource Manager templates](./resource-manager-tutorial-create-multiple-instances.md).</span></span> <span data-ttu-id="5b504-163">The main template (azuredeploy.json) is uploaded to the shell.</span><span class="sxs-lookup"><span data-stu-id="5b504-163">The main template (azuredeploy.json) is uploaded to the shell.</span></span> <span data-ttu-id="5b504-164">The linked template (linkedTemplate.json) must be shared somewhere.</span><span class="sxs-lookup"><span data-stu-id="5b504-164">The linked template (linkedTemplate.json) must be shared somewhere.</span></span>  <span data-ttu-id="5b504-165">To reduce the tasks of this tutorial, the linked template defined in the previous section has been uploaded to [an Azure storage account](https://armtutorials.blob.core.windows.net/linkedtemplates/linkedStorageAccount.json).</span><span class="sxs-lookup"><span data-stu-id="5b504-165">To reduce the tasks of this tutorial, the linked template defined in the previous section has been uploaded to [an Azure storage account](https://armtutorials.blob.core.windows.net/linkedtemplates/linkedStorageAccount.json).</span></span>

## <a name="call-the-linked-template"></a><span data-ttu-id="5b504-166">Call the linked template</span><span class="sxs-lookup"><span data-stu-id="5b504-166">Call the linked template</span></span>

<span data-ttu-id="5b504-167">The main template is called azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="5b504-167">The main template is called azuredeploy.json.</span></span>

1. <span data-ttu-id="5b504-168">Open azuredeploy.json in Visual Studio Code if it is not opened.</span><span class="sxs-lookup"><span data-stu-id="5b504-168">Open azuredeploy.json in Visual Studio Code if it is not opened.</span></span>
2. <span data-ttu-id="5b504-169">Delete the storage account resource definition from the template.</span><span class="sxs-lookup"><span data-stu-id="5b504-169">Delete the storage account resource definition from the template.</span></span>
3. <span data-ttu-id="5b504-170">Add the following json snippet to the place where you had the storage account definition:</span><span class="sxs-lookup"><span data-stu-id="5b504-170">Add the following json snippet to the place where you had the storage account definition:</span></span>

    ```json
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri":"https://armtutorials.blob.core.windows.net/linkedtemplates/linkedStorageAccount.json"
          },
          "parameters": {
              "storageAccountName":{"value": "[variables('storageAccountName')]"},
              "location":{"value": "[parameters('location')]"}
          }
      }
    },
    ```

    <span data-ttu-id="5b504-171">Pay attention to these details:</span><span class="sxs-lookup"><span data-stu-id="5b504-171">Pay attention to these details:</span></span>

    - <span data-ttu-id="5b504-172">A `Microsoft.Resources/deployments` resource in the main template is used to link to another template.</span><span class="sxs-lookup"><span data-stu-id="5b504-172">A `Microsoft.Resources/deployments` resource in the main template is used to link to another template.</span></span>
    - <span data-ttu-id="5b504-173">The `deployments` resource has a name called `linkedTemplate`.</span><span class="sxs-lookup"><span data-stu-id="5b504-173">The `deployments` resource has a name called `linkedTemplate`.</span></span> <span data-ttu-id="5b504-174">This name is used for [configuring dependency](#configure-dependency).</span><span class="sxs-lookup"><span data-stu-id="5b504-174">This name is used for [configuring dependency](#configure-dependency).</span></span>  
    - <span data-ttu-id="5b504-175">You can only use [Incremental](./deployment-modes.md) deployment mode when calling linked templates.</span><span class="sxs-lookup"><span data-stu-id="5b504-175">You can only use [Incremental](./deployment-modes.md) deployment mode when calling linked templates.</span></span>
    - <span data-ttu-id="5b504-176">`templateLink/uri` contains the linked template URI.</span><span class="sxs-lookup"><span data-stu-id="5b504-176">`templateLink/uri` contains the linked template URI.</span></span> <span data-ttu-id="5b504-177">The linked template has been uploaded to a shared storage account.</span><span class="sxs-lookup"><span data-stu-id="5b504-177">The linked template has been uploaded to a shared storage account.</span></span> <span data-ttu-id="5b504-178">You can update the URI if you upload the template another location on the Internet.</span><span class="sxs-lookup"><span data-stu-id="5b504-178">You can update the URI if you upload the template another location on the Internet.</span></span>
    - <span data-ttu-id="5b504-179">Use `parameters` to pass values from the main template to the linked template.</span><span class="sxs-lookup"><span data-stu-id="5b504-179">Use `parameters` to pass values from the main template to the linked template.</span></span>
4. <span data-ttu-id="5b504-180">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="5b504-180">Save the changes.</span></span>

## <a name="configure-dependency"></a><span data-ttu-id="5b504-181">Configure dependency</span><span class="sxs-lookup"><span data-stu-id="5b504-181">Configure dependency</span></span>

<span data-ttu-id="5b504-182">Recall from [Tutorial: create multiple resource instances using Resource Manager template](./resource-manager-tutorial-create-multiple-instances.md), the virtual machine resource depends on the storage account:</span><span class="sxs-lookup"><span data-stu-id="5b504-182">Recall from [Tutorial: create multiple resource instances using Resource Manager template](./resource-manager-tutorial-create-multiple-instances.md), the virtual machine resource depends on the storage account:</span></span>

![Azure Resource Manager templates dependency diagram](./media/resource-manager-tutorial-create-linked-templates/resource-manager-template-visual-studio-code-dependency-diagram.png)

<span data-ttu-id="5b504-184">Because the storage account is defined in the linked template now, you must update the following two elements of the `Microsoft.Compute/virtualMachines` resource.</span><span class="sxs-lookup"><span data-stu-id="5b504-184">Because the storage account is defined in the linked template now, you must update the following two elements of the `Microsoft.Compute/virtualMachines` resource.</span></span>

- <span data-ttu-id="5b504-185">Reconfigure the `dependOn` element.</span><span class="sxs-lookup"><span data-stu-id="5b504-185">Reconfigure the `dependOn` element.</span></span> <span data-ttu-id="5b504-186">The storage account definition is moved to the linked template.</span><span class="sxs-lookup"><span data-stu-id="5b504-186">The storage account definition is moved to the linked template.</span></span>
- <span data-ttu-id="5b504-187">Reconfigure the `properties/diagnosticsProfile/bootDiagnostics/storageUri` element.</span><span class="sxs-lookup"><span data-stu-id="5b504-187">Reconfigure the `properties/diagnosticsProfile/bootDiagnostics/storageUri` element.</span></span> <span data-ttu-id="5b504-188">In [Create the linked template](#create-the-linked-template), you added an output value:</span><span class="sxs-lookup"><span data-stu-id="5b504-188">In [Create the linked template](#create-the-linked-template), you added an output value:</span></span>

    ```json
    "outputs": {
        "storageUri": {
            "type": "string",
            "value": "[reference(parameters('storageAccountName')).primaryEndpoints.blob]"
            }
    }
    ```
    <span data-ttu-id="5b504-189">This value is required by the main template.</span><span class="sxs-lookup"><span data-stu-id="5b504-189">This value is required by the main template.</span></span>

1. <span data-ttu-id="5b504-190">Open azuredeploy.json in Visual Studio Code if it is not opened.</span><span class="sxs-lookup"><span data-stu-id="5b504-190">Open azuredeploy.json in Visual Studio Code if it is not opened.</span></span>
2. <span data-ttu-id="5b504-191">Expand the virtual machine resource definition, update **dependsOn** as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="5b504-191">Expand the virtual machine resource definition, update **dependsOn** as shown in the following screenshot:</span></span>

    ![<span data-ttu-id="5b504-192">Azure Resource Manager linked templates configure dependency</span><span class="sxs-lookup"><span data-stu-id="5b504-192">Azure Resource Manager linked templates configure dependency</span></span> ](./media/resource-manager-tutorial-create-linked-templates/resource-manager-template-linked-templates-configure-dependency.png)
    
    <span data-ttu-id="5b504-193">"linkedTemplate" is the name of the deployments resource.</span><span class="sxs-lookup"><span data-stu-id="5b504-193">"linkedTemplate" is the name of the deployments resource.</span></span>  
3. <span data-ttu-id="5b504-194">update **properties/diagnosticsProfile/bootDiagnostics/storageUri** as shown in the previous screenshot.</span><span class="sxs-lookup"><span data-stu-id="5b504-194">update **properties/diagnosticsProfile/bootDiagnostics/storageUri** as shown in the previous screenshot.</span></span>

<span data-ttu-id="5b504-195">For more information, see [Use linked and nested templates when deploying Azure resources](./resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="5b504-195">For more information, see [Use linked and nested templates when deploying Azure resources](./resource-group-linked-templates.md)</span></span>

## <a name="deploy-the-template"></a><span data-ttu-id="5b504-196">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="5b504-196">Deploy the template</span></span>

<span data-ttu-id="5b504-197">Refer to the [Deploy the template](./resource-manager-tutorial-create-multiple-instances.md#deploy-the-template) section for the deployment procedure.</span><span class="sxs-lookup"><span data-stu-id="5b504-197">Refer to the [Deploy the template](./resource-manager-tutorial-create-multiple-instances.md#deploy-the-template) section for the deployment procedure.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="5b504-198">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="5b504-198">Clean up resources</span></span>

<span data-ttu-id="5b504-199">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="5b504-199">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

1. <span data-ttu-id="5b504-200">From the Azure portal, select **Resource group** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="5b504-200">From the Azure portal, select **Resource group** from the left menu.</span></span>
2. <span data-ttu-id="5b504-201">Enter the resource group name in the **Filter by name** field.</span><span class="sxs-lookup"><span data-stu-id="5b504-201">Enter the resource group name in the **Filter by name** field.</span></span>
3. <span data-ttu-id="5b504-202">Select the resource group name.</span><span class="sxs-lookup"><span data-stu-id="5b504-202">Select the resource group name.</span></span>  <span data-ttu-id="5b504-203">You shall see a total of six resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="5b504-203">You shall see a total of six resources in the resource group.</span></span>
4. <span data-ttu-id="5b504-204">Select **Delete resource group** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="5b504-204">Select **Delete resource group** from the top menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b504-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b504-205">Next steps</span></span>

<span data-ttu-id="5b504-206">In this tutorial, you develop and deploy a template to create a virtual machine, a virtual network, and the dependent resources.</span><span class="sxs-lookup"><span data-stu-id="5b504-206">In this tutorial, you develop and deploy a template to create a virtual machine, a virtual network, and the dependent resources.</span></span> <span data-ttu-id="5b504-207">To learn more about templates, see [Understand the structure and syntax of Azure Resource Manager Templates](./resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5b504-207">To learn more about templates, see [Understand the structure and syntax of Azure Resource Manager Templates](./resource-group-authoring-templates.md).</span></span>
