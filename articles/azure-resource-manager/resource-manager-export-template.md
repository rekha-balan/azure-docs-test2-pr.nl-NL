---
title: Export Azure Resource Manager template | Microsoft Docs
description: Use Azure Resource Manage to export a template from an existing resource group.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: 90d89175a8be32ee0a2f144ce073021599bf9e39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549417"
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="806ed-103">Export an Azure Resource Manager template from existing resources</span><span class="sxs-lookup"><span data-stu-id="806ed-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="806ed-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="806ed-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="806ed-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span><span class="sxs-lookup"><span data-stu-id="806ed-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="806ed-106">It is important to note that there are two different ways to export a template:</span><span class="sxs-lookup"><span data-stu-id="806ed-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="806ed-107">You can export the actual template that you used for a deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="806ed-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span><span class="sxs-lookup"><span data-stu-id="806ed-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="806ed-109">This approach is helpful when you have deployed resources through the portal.</span><span class="sxs-lookup"><span data-stu-id="806ed-109">This approach is helpful when you have deployed resources through the portal.</span></span> <span data-ttu-id="806ed-110">Now, you want to see how to construct the template to create those resources.</span><span class="sxs-lookup"><span data-stu-id="806ed-110">Now, you want to see how to construct the template to create those resources.</span></span>
* <span data-ttu-id="806ed-111">You can export a template that represents the current state of the resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-111">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="806ed-112">The exported template is not based on any template that you used for deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-112">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="806ed-113">Instead, it creates a template that is a snapshot of the resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-113">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="806ed-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span><span class="sxs-lookup"><span data-stu-id="806ed-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="806ed-115">This approach is useful when you have modified the resource group through the portal or scripts.</span><span class="sxs-lookup"><span data-stu-id="806ed-115">This approach is useful when you have modified the resource group through the portal or scripts.</span></span> <span data-ttu-id="806ed-116">Now, you need to capture the resource group as a template.</span><span class="sxs-lookup"><span data-stu-id="806ed-116">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="806ed-117">This topic shows both approaches.</span><span class="sxs-lookup"><span data-stu-id="806ed-117">This topic shows both approaches.</span></span>

<span data-ttu-id="806ed-118">In this tutorial, you sign in to the Azure portal, create a storage account, and export the template for that storage account.</span><span class="sxs-lookup"><span data-stu-id="806ed-118">In this tutorial, you sign in to the Azure portal, create a storage account, and export the template for that storage account.</span></span> <span data-ttu-id="806ed-119">You add a virtual network to modify the resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-119">You add a virtual network to modify the resource group.</span></span> <span data-ttu-id="806ed-120">Finally, you export a new template that represents its current state.</span><span class="sxs-lookup"><span data-stu-id="806ed-120">Finally, you export a new template that represents its current state.</span></span> <span data-ttu-id="806ed-121">Although this article focuses on a simplified infrastructure, you could use these same steps to export a template for a more complicated solution.</span><span class="sxs-lookup"><span data-stu-id="806ed-121">Although this article focuses on a simplified infrastructure, you could use these same steps to export a template for a more complicated solution.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="806ed-122">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="806ed-122">Create a storage account</span></span>
1. <span data-ttu-id="806ed-123">In the [Azure portal](https://portal.azure.com), select **New** > **Storage** > **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="806ed-123">In the [Azure portal](https://portal.azure.com), select **New** > **Storage** > **Storage account**.</span></span>
   
      ![create storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/create-storage.png)
2. <span data-ttu-id="806ed-125">Create a storage account with the name **storage**, your initials, and the date.</span><span class="sxs-lookup"><span data-stu-id="806ed-125">Create a storage account with the name **storage**, your initials, and the date.</span></span> <span data-ttu-id="806ed-126">The storage account name must be unique across Azure.</span><span class="sxs-lookup"><span data-stu-id="806ed-126">The storage account name must be unique across Azure.</span></span> <span data-ttu-id="806ed-127">If the name is already in use, you see an error message indicating the name is in use.</span><span class="sxs-lookup"><span data-stu-id="806ed-127">If the name is already in use, you see an error message indicating the name is in use.</span></span> <span data-ttu-id="806ed-128">Try a variation.</span><span class="sxs-lookup"><span data-stu-id="806ed-128">Try a variation.</span></span> <span data-ttu-id="806ed-129">For resource group, select **Create new** and name it **ExportGroup**.</span><span class="sxs-lookup"><span data-stu-id="806ed-129">For resource group, select **Create new** and name it **ExportGroup**.</span></span> <span data-ttu-id="806ed-130">You can use the default values for the other properties.</span><span class="sxs-lookup"><span data-stu-id="806ed-130">You can use the default values for the other properties.</span></span> <span data-ttu-id="806ed-131">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="806ed-131">Select **Create**.</span></span>
   
      ![provide values for storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/provide-storage-values.png)

<span data-ttu-id="806ed-133">The deployment may take a minute.</span><span class="sxs-lookup"><span data-stu-id="806ed-133">The deployment may take a minute.</span></span> <span data-ttu-id="806ed-134">After the deployment finishes, your subscription contains the storage account.</span><span class="sxs-lookup"><span data-stu-id="806ed-134">After the deployment finishes, your subscription contains the storage account.</span></span>

## <a name="view-a-template-from-deployment-history"></a><span data-ttu-id="806ed-135">View a template from deployment history</span><span class="sxs-lookup"><span data-stu-id="806ed-135">View a template from deployment history</span></span>
1. <span data-ttu-id="806ed-136">Go to the resource group blade for your new resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-136">Go to the resource group blade for your new resource group.</span></span> <span data-ttu-id="806ed-137">Notice that the blade shows the result of the last deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-137">Notice that the blade shows the result of the last deployment.</span></span> <span data-ttu-id="806ed-138">Select this link.</span><span class="sxs-lookup"><span data-stu-id="806ed-138">Select this link.</span></span>
   
      ![resource group blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/resource-group-blade.png)
2. <span data-ttu-id="806ed-140">You see a history of deployments for the group.</span><span class="sxs-lookup"><span data-stu-id="806ed-140">You see a history of deployments for the group.</span></span> <span data-ttu-id="806ed-141">In your case, the blade probably lists only one deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-141">In your case, the blade probably lists only one deployment.</span></span> <span data-ttu-id="806ed-142">Select this deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-142">Select this deployment.</span></span>
   
     ![last deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/last-deployment.png)
3. <span data-ttu-id="806ed-144">The blade displays a summary of the deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-144">The blade displays a summary of the deployment.</span></span> <span data-ttu-id="806ed-145">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span><span class="sxs-lookup"><span data-stu-id="806ed-145">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span></span> <span data-ttu-id="806ed-146">To see the template that you used for the deployment, select **View template**.</span><span class="sxs-lookup"><span data-stu-id="806ed-146">To see the template that you used for the deployment, select **View template**.</span></span>
   
     ![view deployment summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/deployment-summary.png)
4. <span data-ttu-id="806ed-148">Resource Manager retrieves the following seven files for you:</span><span class="sxs-lookup"><span data-stu-id="806ed-148">Resource Manager retrieves the following seven files for you:</span></span>
   
   1. <span data-ttu-id="806ed-149">**Template** - The template that defines the infrastructure for your solution.</span><span class="sxs-lookup"><span data-stu-id="806ed-149">**Template** - The template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="806ed-150">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span><span class="sxs-lookup"><span data-stu-id="806ed-150">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="806ed-151">**Parameters** - A parameter file that you can use to pass in values during deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-151">**Parameters** - A parameter file that you can use to pass in values during deployment.</span></span> <span data-ttu-id="806ed-152">It contains the values that you provided during the first deployment, but you can change any of these values when you redeploy the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-152">It contains the values that you provided during the first deployment, but you can change any of these values when you redeploy the template.</span></span>
   3. <span data-ttu-id="806ed-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   3. <span data-ttu-id="806ed-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   4. <span data-ttu-id="806ed-155">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-155">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span></span>
   5. <span data-ttu-id="806ed-156">**.NET** - A .NET class that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-156">**.NET** - A .NET class that you can use to deploy the template.</span></span>
   6. <span data-ttu-id="806ed-157">**Ruby** - A Ruby class that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-157">**Ruby** - A Ruby class that you can use to deploy the template.</span></span>
      
      <span data-ttu-id="806ed-158">The files are available through links across the blade.</span><span class="sxs-lookup"><span data-stu-id="806ed-158">The files are available through links across the blade.</span></span> <span data-ttu-id="806ed-159">By default, the blade displays the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-159">By default, the blade displays the template.</span></span>
      
       ![view template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/view-template.png)
      
      <span data-ttu-id="806ed-161">Let's pay particular attention to the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-161">Let's pay particular attention to the template.</span></span> <span data-ttu-id="806ed-162">Your template should look similar to:</span><span class="sxs-lookup"><span data-stu-id="806ed-162">Your template should look similar to:</span></span>
      
      ```json
      {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
          "name": {
            "type": "String"
          },
          "accountType": {
            "type": "String"
          },
          "location": {
            "type": "String"
          },
          "encryptionEnabled": {
            "defaultValue": false,
            "type": "Bool"
          }
        },
        "resources": [
          {
            "type": "Microsoft.Storage/storageAccounts",
            "sku": {
              "name": "[parameters('accountType')]"
            },
            "kind": "Storage",
            "name": "[parameters('name')]",
            "apiVersion": "2016-01-01",
            "location": "[parameters('location')]",
            "properties": {
              "encryption": {
                "services": {
                  "blob": {
                    "enabled": "[parameters('encryptionEnabled')]"
                  }
                },
                "keySource": "Microsoft.Storage"
              }
            }
          }
        ]
      }
      ```

<span data-ttu-id="806ed-163">This template is the actual template used to create your storage account.</span><span class="sxs-lookup"><span data-stu-id="806ed-163">This template is the actual template used to create your storage account.</span></span> <span data-ttu-id="806ed-164">Notice it contains parameters that enable you to deploy different types of storage accounts.</span><span class="sxs-lookup"><span data-stu-id="806ed-164">Notice it contains parameters that enable you to deploy different types of storage accounts.</span></span> <span data-ttu-id="806ed-165">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="806ed-165">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span> <span data-ttu-id="806ed-166">For the complete list of the functions you can use in a template, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="806ed-166">For the complete list of the functions you can use in a template, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span>

## <a name="add-a-virtual-network"></a><span data-ttu-id="806ed-167">Add a virtual network</span><span class="sxs-lookup"><span data-stu-id="806ed-167">Add a virtual network</span></span>
<span data-ttu-id="806ed-168">The template that you downloaded in the previous section represented the infrastructure for that original deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-168">The template that you downloaded in the previous section represented the infrastructure for that original deployment.</span></span> <span data-ttu-id="806ed-169">However, it will not account for any changes you make after the deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-169">However, it will not account for any changes you make after the deployment.</span></span>
<span data-ttu-id="806ed-170">To illustrate this issue, let's modify the resource group by adding a virtual network through the portal.</span><span class="sxs-lookup"><span data-stu-id="806ed-170">To illustrate this issue, let's modify the resource group by adding a virtual network through the portal.</span></span>

1. <span data-ttu-id="806ed-171">In the resource group blade, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="806ed-171">In the resource group blade, select **Add**.</span></span>
   
      ![add resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/add-resource.png)
2. <span data-ttu-id="806ed-173">Select **Virtual network** from the available resources.</span><span class="sxs-lookup"><span data-stu-id="806ed-173">Select **Virtual network** from the available resources.</span></span>
   
      ![select virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/select-vnet.png)
3. <span data-ttu-id="806ed-175">Name your virtual network **VNET**, and use the default values for the other properties.</span><span class="sxs-lookup"><span data-stu-id="806ed-175">Name your virtual network **VNET**, and use the default values for the other properties.</span></span> <span data-ttu-id="806ed-176">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="806ed-176">Select **Create**.</span></span>
   
      ![set alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/create-vnet.png)
4. <span data-ttu-id="806ed-178">After the virtual network has successfully deployed to your resource group, look again at the deployment history.</span><span class="sxs-lookup"><span data-stu-id="806ed-178">After the virtual network has successfully deployed to your resource group, look again at the deployment history.</span></span> <span data-ttu-id="806ed-179">You now see two deployments.</span><span class="sxs-lookup"><span data-stu-id="806ed-179">You now see two deployments.</span></span> <span data-ttu-id="806ed-180">If you do not see the second deployment, you may need to close your resource group blade and reopen it.</span><span class="sxs-lookup"><span data-stu-id="806ed-180">If you do not see the second deployment, you may need to close your resource group blade and reopen it.</span></span> <span data-ttu-id="806ed-181">Select the more recent deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-181">Select the more recent deployment.</span></span>
   
      ![deployment history](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/deployment-history.png)
5. <span data-ttu-id="806ed-183">View the template for that deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-183">View the template for that deployment.</span></span> <span data-ttu-id="806ed-184">Notice that it defines only the virtual network.</span><span class="sxs-lookup"><span data-stu-id="806ed-184">Notice that it defines only the virtual network.</span></span> <span data-ttu-id="806ed-185">It does not include the storage account you deployed earlier.</span><span class="sxs-lookup"><span data-stu-id="806ed-185">It does not include the storage account you deployed earlier.</span></span> <span data-ttu-id="806ed-186">You no longer have a template that represents all the resources in your resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-186">You no longer have a template that represents all the resources in your resource group.</span></span>

## <a name="export-the-template-from-resource-group"></a><span data-ttu-id="806ed-187">Export the template from resource group</span><span class="sxs-lookup"><span data-stu-id="806ed-187">Export the template from resource group</span></span>
<span data-ttu-id="806ed-188">To get the current state of your resource group, export a template that shows a snapshot of the resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-188">To get the current state of your resource group, export a template that shows a snapshot of the resource group.</span></span>  

> [!NOTE]
> <span data-ttu-id="806ed-189">You cannot export a template for a resource group that has more than 200 resources.</span><span class="sxs-lookup"><span data-stu-id="806ed-189">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="806ed-190">To view the template for a resource group, select **Automation script**.</span><span class="sxs-lookup"><span data-stu-id="806ed-190">To view the template for a resource group, select **Automation script**.</span></span>
   
      ![export resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/export-resource-group.png)
   
     <span data-ttu-id="806ed-192">Not all resource types support the export template function.</span><span class="sxs-lookup"><span data-stu-id="806ed-192">Not all resource types support the export template function.</span></span> <span data-ttu-id="806ed-193">If your resource group only contains the storage account and virtual network shown in this article, you do not see an error.</span><span class="sxs-lookup"><span data-stu-id="806ed-193">If your resource group only contains the storage account and virtual network shown in this article, you do not see an error.</span></span> <span data-ttu-id="806ed-194">However, if you have created other resource types, you may see an error stating that there is a problem with the export.</span><span class="sxs-lookup"><span data-stu-id="806ed-194">However, if you have created other resource types, you may see an error stating that there is a problem with the export.</span></span> <span data-ttu-id="806ed-195">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span><span class="sxs-lookup"><span data-stu-id="806ed-195">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="806ed-196">You again see the six files that you can use to redeploy the solution, but this time the template is a little different.</span><span class="sxs-lookup"><span data-stu-id="806ed-196">You again see the six files that you can use to redeploy the solution, but this time the template is a little different.</span></span> <span data-ttu-id="806ed-197">This template has only two parameters: one for the storage account name, and one for the virtual network name.</span><span class="sxs-lookup"><span data-stu-id="806ed-197">This template has only two parameters: one for the storage account name, and one for the virtual network name.</span></span>

   ```json
   "parameters": {
     "virtualNetworks_VNET_name": {
       "defaultValue": "VNET",
       "type": "String"
     },
     "storageAccounts_storagetf05092016_name": {
       "defaultValue": "storagetf05092016",
       "type": "String"
     }
   },
   ```
   
   <span data-ttu-id="806ed-198">Resource Manager did not retrieve the templates that you used during deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-198">Resource Manager did not retrieve the templates that you used during deployment.</span></span> <span data-ttu-id="806ed-199">Instead, it generated a new template that's based on the current configuration of the resources.</span><span class="sxs-lookup"><span data-stu-id="806ed-199">Instead, it generated a new template that's based on the current configuration of the resources.</span></span> <span data-ttu-id="806ed-200">For example, the template sets the storage account location and replication value to:</span><span class="sxs-lookup"><span data-stu-id="806ed-200">For example, the template sets the storage account location and replication value to:</span></span>

   ```json 
   "location": "northeurope",
   "tags": {},
   "properties": {
     "accountType": "Standard_RAGRS"
   },
   ```
3. <span data-ttu-id="806ed-201">You have a couple of options for continuing to work with this template.</span><span class="sxs-lookup"><span data-stu-id="806ed-201">You have a couple of options for continuing to work with this template.</span></span> <span data-ttu-id="806ed-202">You can either download the template and work on it locally with a JSON editor.</span><span class="sxs-lookup"><span data-stu-id="806ed-202">You can either download the template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="806ed-203">Or, you can save the template to your library and work on it through the portal.</span><span class="sxs-lookup"><span data-stu-id="806ed-203">Or, you can save the template to your library and work on it through the portal.</span></span>
   
     <span data-ttu-id="806ed-204">If you are comfortable using a JSON editor like [VS Code](resource-manager-vs-code.md) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span><span class="sxs-lookup"><span data-stu-id="806ed-204">If you are comfortable using a JSON editor like [VS Code](resource-manager-vs-code.md) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span></span> <span data-ttu-id="806ed-205">If you are not set up with a JSON editor, you might prefer editing the template through the portal.</span><span class="sxs-lookup"><span data-stu-id="806ed-205">If you are not set up with a JSON editor, you might prefer editing the template through the portal.</span></span> <span data-ttu-id="806ed-206">The remainder of this topic assumes you have saved the template to your library in the portal.</span><span class="sxs-lookup"><span data-stu-id="806ed-206">The remainder of this topic assumes you have saved the template to your library in the portal.</span></span> <span data-ttu-id="806ed-207">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span><span class="sxs-lookup"><span data-stu-id="806ed-207">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span></span>
   
     <span data-ttu-id="806ed-208">To work locally, select **Download**.</span><span class="sxs-lookup"><span data-stu-id="806ed-208">To work locally, select **Download**.</span></span>
   
      ![download template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="806ed-210">To work through the portal, select **Add to library**.</span><span class="sxs-lookup"><span data-stu-id="806ed-210">To work through the portal, select **Add to library**.</span></span>
   
      ![add to library](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="806ed-212">When adding a template to the library, give the template a name and description.</span><span class="sxs-lookup"><span data-stu-id="806ed-212">When adding a template to the library, give the template a name and description.</span></span> <span data-ttu-id="806ed-213">Then, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="806ed-213">Then, select **Save**.</span></span>
   
     ![set template values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/set-template-values.png)
4. <span data-ttu-id="806ed-215">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span><span class="sxs-lookup"><span data-stu-id="806ed-215">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span></span>
   
      ![find templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="806ed-217">Select the template with the name you saved.</span><span class="sxs-lookup"><span data-stu-id="806ed-217">Select the template with the name you saved.</span></span>
   
      ![select template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/select-library-template.png)

## <a name="customize-the-template"></a><span data-ttu-id="806ed-219">Customize the template</span><span class="sxs-lookup"><span data-stu-id="806ed-219">Customize the template</span></span>
<span data-ttu-id="806ed-220">The exported template works fine if you want to create the same storage account and virtual network for every deployment.</span><span class="sxs-lookup"><span data-stu-id="806ed-220">The exported template works fine if you want to create the same storage account and virtual network for every deployment.</span></span> <span data-ttu-id="806ed-221">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span><span class="sxs-lookup"><span data-stu-id="806ed-221">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="806ed-222">For example, during deployment, you might want to specify the type of storage account to create or the values to use for the virtual network address prefix and subnet prefix.</span><span class="sxs-lookup"><span data-stu-id="806ed-222">For example, during deployment, you might want to specify the type of storage account to create or the values to use for the virtual network address prefix and subnet prefix.</span></span>

<span data-ttu-id="806ed-223">In this section, you add parameters to the exported template so that you can reuse the template when you deploy these resources to other environments.</span><span class="sxs-lookup"><span data-stu-id="806ed-223">In this section, you add parameters to the exported template so that you can reuse the template when you deploy these resources to other environments.</span></span> <span data-ttu-id="806ed-224">You also add some features to your template to decrease the likelihood of encountering an error when you deploy your template.</span><span class="sxs-lookup"><span data-stu-id="806ed-224">You also add some features to your template to decrease the likelihood of encountering an error when you deploy your template.</span></span> <span data-ttu-id="806ed-225">You no longer have to guess a unique name for your storage account.</span><span class="sxs-lookup"><span data-stu-id="806ed-225">You no longer have to guess a unique name for your storage account.</span></span> <span data-ttu-id="806ed-226">Instead, the template creates a unique name.</span><span class="sxs-lookup"><span data-stu-id="806ed-226">Instead, the template creates a unique name.</span></span> <span data-ttu-id="806ed-227">You restrict the values that can be specified for the storage account type to only valid options.</span><span class="sxs-lookup"><span data-stu-id="806ed-227">You restrict the values that can be specified for the storage account type to only valid options.</span></span>

1. <span data-ttu-id="806ed-228">To customize the template, select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="806ed-228">To customize the template, select **Edit**.</span></span>
   
     ![show template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/show-template.png)
2. <span data-ttu-id="806ed-230">Select the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-230">Select the template.</span></span>
   
     ![edit template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/edit-template.png)
3. <span data-ttu-id="806ed-232">To be able to pass the values that you might want to specify during deployment, replace the **parameters** section with new parameter definitions.</span><span class="sxs-lookup"><span data-stu-id="806ed-232">To be able to pass the values that you might want to specify during deployment, replace the **parameters** section with new parameter definitions.</span></span> <span data-ttu-id="806ed-233">Notice the values of **allowedValues** for **storageAccount_accountType**.</span><span class="sxs-lookup"><span data-stu-id="806ed-233">Notice the values of **allowedValues** for **storageAccount_accountType**.</span></span> <span data-ttu-id="806ed-234">If you accidentally provide an invalid value, that error is recognized before the deployment starts.</span><span class="sxs-lookup"><span data-stu-id="806ed-234">If you accidentally provide an invalid value, that error is recognized before the deployment starts.</span></span> <span data-ttu-id="806ed-235">Also, notice that you are providing only a prefix for the storage account name, and the prefix is limited to 11 characters.</span><span class="sxs-lookup"><span data-stu-id="806ed-235">Also, notice that you are providing only a prefix for the storage account name, and the prefix is limited to 11 characters.</span></span> <span data-ttu-id="806ed-236">When you limit the prefix to 11 characters, you ensure that the complete name does not exceed the maximum number of characters for a storage account.</span><span class="sxs-lookup"><span data-stu-id="806ed-236">When you limit the prefix to 11 characters, you ensure that the complete name does not exceed the maximum number of characters for a storage account.</span></span> <span data-ttu-id="806ed-237">The prefix enables you to apply a naming convention to your storage accounts.</span><span class="sxs-lookup"><span data-stu-id="806ed-237">The prefix enables you to apply a naming convention to your storage accounts.</span></span> <span data-ttu-id="806ed-238">You will see how to create a unique name in the next step.</span><span class="sxs-lookup"><span data-stu-id="806ed-238">You will see how to create a unique name in the next step.</span></span>

   ```json
   "parameters": {
     "storageAccount_prefix": {
       "type": "string",
       "maxLength": 11
     },
     "storageAccount_accountType": {
       "defaultValue": "Standard_RAGRS",
       "type": "string",
       "allowedValues": [
         "Standard_LRS",
         "Standard_ZRS",
         "Standard_GRS",
         "Standard_RAGRS",
         "Premium_LRS"
       ]
     },
     "virtualNetwork_name": {
       "type": "string"
     },
     "addressPrefix": {
       "defaultValue": "10.0.0.0/16",
       "type": "string"
     },
     "subnetName": {
       "defaultValue": "subnet-1",
       "type": "string"
     },
     "subnetAddressPrefix": {
       "defaultValue": "10.0.0.0/24",
       "type": "string"
     }
   },
   ```

4. <span data-ttu-id="806ed-239">The **variables** section of your template is currently empty.</span><span class="sxs-lookup"><span data-stu-id="806ed-239">The **variables** section of your template is currently empty.</span></span> <span data-ttu-id="806ed-240">In the **variables** section, you create values that simplify the syntax for the rest of your template.</span><span class="sxs-lookup"><span data-stu-id="806ed-240">In the **variables** section, you create values that simplify the syntax for the rest of your template.</span></span> <span data-ttu-id="806ed-241">Replace this section with a new variable definition.</span><span class="sxs-lookup"><span data-stu-id="806ed-241">Replace this section with a new variable definition.</span></span> <span data-ttu-id="806ed-242">The **storageAccount_name** variable concatenates the prefix from the parameter to a unique string that is generated based on the identifier of the resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-242">The **storageAccount_name** variable concatenates the prefix from the parameter to a unique string that is generated based on the identifier of the resource group.</span></span> <span data-ttu-id="806ed-243">You no longer have to guess a unique name when providing a parameter value.</span><span class="sxs-lookup"><span data-stu-id="806ed-243">You no longer have to guess a unique name when providing a parameter value.</span></span>

   ```json
   "variables": {
     "storageAccount_name": "[concat(parameters('storageAccount_prefix'), uniqueString(resourceGroup().id))]"
   },
   ```

5. <span data-ttu-id="806ed-244">To use the parameters and variable in the resource definitions, replace the **resources** section with new resource definitions.</span><span class="sxs-lookup"><span data-stu-id="806ed-244">To use the parameters and variable in the resource definitions, replace the **resources** section with new resource definitions.</span></span> <span data-ttu-id="806ed-245">Notice that little has changed in the resource definitions other than the value that's assigned to the resource property.</span><span class="sxs-lookup"><span data-stu-id="806ed-245">Notice that little has changed in the resource definitions other than the value that's assigned to the resource property.</span></span> <span data-ttu-id="806ed-246">The properties are the same as the properties from the exported template.</span><span class="sxs-lookup"><span data-stu-id="806ed-246">The properties are the same as the properties from the exported template.</span></span> <span data-ttu-id="806ed-247">You are simply assigning properties to parameter values instead of hard-coded values.</span><span class="sxs-lookup"><span data-stu-id="806ed-247">You are simply assigning properties to parameter values instead of hard-coded values.</span></span> <span data-ttu-id="806ed-248">The location of the resources is set to use the same location as the resource group through the **resourceGroup().location** expression.</span><span class="sxs-lookup"><span data-stu-id="806ed-248">The location of the resources is set to use the same location as the resource group through the **resourceGroup().location** expression.</span></span> <span data-ttu-id="806ed-249">The variable that you created for the storage account name is referenced through the **variables** expression.</span><span class="sxs-lookup"><span data-stu-id="806ed-249">The variable that you created for the storage account name is referenced through the **variables** expression.</span></span>

   ```json
   "resources": [
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "[parameters('virtualNetwork_name')]",
       "apiVersion": "2015-06-15",
       "location": "[resourceGroup().location]",
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "[parameters('addressPrefix')]"
           ]
         },
         "subnets": [
           {
             "name": "[parameters('subnetName')]",
             "properties": {
               "addressPrefix": "[parameters('subnetAddressPrefix')]"
             }
           }
         ]
       },
       "dependsOn": []
     },
     {
       "type": "Microsoft.Storage/storageAccounts",
       "name": "[variables('storageAccount_name')]",
       "apiVersion": "2015-06-15",
       "location": "[resourceGroup().location]",
       "tags": {},
       "properties": {
         "accountType": "[parameters('storageAccount_accountType')]"
       },
       "dependsOn": []
     }
   ]
   ```

6. <span data-ttu-id="806ed-250">Select **OK** when you are done editing the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-250">Select **OK** when you are done editing the template.</span></span>
7. <span data-ttu-id="806ed-251">Select **Save** to save the changes to the template.</span><span class="sxs-lookup"><span data-stu-id="806ed-251">Select **Save** to save the changes to the template.</span></span>
   
     ![save template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="806ed-253">To deploy the updated template, select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="806ed-253">To deploy the updated template, select **Deploy**.</span></span>
   
     ![deploy template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/deploy-template.png)
9. <span data-ttu-id="806ed-255">Provide parameter values, and select a new resource group to deploy the resources to.</span><span class="sxs-lookup"><span data-stu-id="806ed-255">Provide parameter values, and select a new resource group to deploy the resources to.</span></span>

## <a name="update-the-downloaded-parameters-file"></a><span data-ttu-id="806ed-256">Update the downloaded parameters file</span><span class="sxs-lookup"><span data-stu-id="806ed-256">Update the downloaded parameters file</span></span>
<span data-ttu-id="806ed-257">If you are working with the downloaded files (rather than the portal library), you need to update the downloaded parameter file.</span><span class="sxs-lookup"><span data-stu-id="806ed-257">If you are working with the downloaded files (rather than the portal library), you need to update the downloaded parameter file.</span></span> <span data-ttu-id="806ed-258">It no longer matches the parameters in your template.</span><span class="sxs-lookup"><span data-stu-id="806ed-258">It no longer matches the parameters in your template.</span></span> <span data-ttu-id="806ed-259">You do not have to use a parameter file, but it can simplify the process when you redeploy an environment.</span><span class="sxs-lookup"><span data-stu-id="806ed-259">You do not have to use a parameter file, but it can simplify the process when you redeploy an environment.</span></span> <span data-ttu-id="806ed-260">You use the default values that are defined in the template for many of the parameters so that your parameter file only needs two values.</span><span class="sxs-lookup"><span data-stu-id="806ed-260">You use the default values that are defined in the template for many of the parameters so that your parameter file only needs two values.</span></span>

<span data-ttu-id="806ed-261">Replace the contents of the parameters.json file with:</span><span class="sxs-lookup"><span data-stu-id="806ed-261">Replace the contents of the parameters.json file with:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccount_prefix": {
      "value": "storage"
    },
    "virtualNetwork_name": {
      "value": "VNET"
    }
  }
}
```

<span data-ttu-id="806ed-262">The updated parameter file provides values only for parameters that do not have a default value.</span><span class="sxs-lookup"><span data-stu-id="806ed-262">The updated parameter file provides values only for parameters that do not have a default value.</span></span> <span data-ttu-id="806ed-263">You can provide values for the other parameters when you want a value that is different from the default value.</span><span class="sxs-lookup"><span data-stu-id="806ed-263">You can provide values for the other parameters when you want a value that is different from the default value.</span></span>

## <a name="fix-export-issues"></a><span data-ttu-id="806ed-264">Fix export issues</span><span class="sxs-lookup"><span data-stu-id="806ed-264">Fix export issues</span></span>
<span data-ttu-id="806ed-265">Not all resource types support the export template function.</span><span class="sxs-lookup"><span data-stu-id="806ed-265">Not all resource types support the export template function.</span></span> <span data-ttu-id="806ed-266">Resource Manager specifically does not export some resource types to prevent exposing sensitive data.</span><span class="sxs-lookup"><span data-stu-id="806ed-266">Resource Manager specifically does not export some resource types to prevent exposing sensitive data.</span></span> <span data-ttu-id="806ed-267">For example, if you have a connection string in your site config, you probably do not want it explicitly displayed in an exported template.</span><span class="sxs-lookup"><span data-stu-id="806ed-267">For example, if you have a connection string in your site config, you probably do not want it explicitly displayed in an exported template.</span></span> <span data-ttu-id="806ed-268">To resolve this issue, manually add the missing resources back into your template.</span><span class="sxs-lookup"><span data-stu-id="806ed-268">To resolve this issue, manually add the missing resources back into your template.</span></span>

> [!NOTE]
> <span data-ttu-id="806ed-269">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span><span class="sxs-lookup"><span data-stu-id="806ed-269">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="806ed-270">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span><span class="sxs-lookup"><span data-stu-id="806ed-270">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span></span> <span data-ttu-id="806ed-271">Only export from a resource group when you have made changes to the resource group that are not defined in a single template.</span><span class="sxs-lookup"><span data-stu-id="806ed-271">Only export from a resource group when you have made changes to the resource group that are not defined in a single template.</span></span>
> 
> 

<span data-ttu-id="806ed-272">For example, if you export a template for a resource group that contains a web app, SQL Database, and connection string in the site config, you see the following message:</span><span class="sxs-lookup"><span data-stu-id="806ed-272">For example, if you export a template for a resource group that contains a web app, SQL Database, and connection string in the site config, you see the following message:</span></span>

![show error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/show-error.png)

<span data-ttu-id="806ed-274">Selecting the message shows you exactly which resource types were not exported.</span><span class="sxs-lookup"><span data-stu-id="806ed-274">Selecting the message shows you exactly which resource types were not exported.</span></span> 

![show error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-export-template/show-error-details.png)

<span data-ttu-id="806ed-276">This topic shows common fixes.</span><span class="sxs-lookup"><span data-stu-id="806ed-276">This topic shows common fixes.</span></span>

### <a name="connection-string"></a><span data-ttu-id="806ed-277">Connection string</span><span class="sxs-lookup"><span data-stu-id="806ed-277">Connection string</span></span>
<span data-ttu-id="806ed-278">In the web sites resource, add a definition for the connection string to the database:</span><span class="sxs-lookup"><span data-stu-id="806ed-278">In the web sites resource, add a definition for the connection string to the database:</span></span>

```json
{
  "type": "Microsoft.Web/sites",
  ...
  "resources": [
    {
      "apiVersion": "2015-08-01",
      "type": "config",
      "name": "connectionstrings",
      "dependsOn": [
          "[concat('Microsoft.Web/Sites/', parameters('<site-name>'))]"
      ],
      "properties": {
          "DefaultConnection": {
            "value": "[concat('Data Source=tcp:', reference(concat('Microsoft.Sql/servers/', parameters('<database-server-name>'))).fullyQualifiedDomainName, ',1433;Initial Catalog=', parameters('<database-name>'), ';User Id=', parameters('<admin-login>'), '@', parameters('<database-server-name>'), ';Password=', parameters('<admin-password>'), ';')]",
              "type": "SQLServer"
          }
      }
    }
  ]
}
```    

### <a name="web-site-extension"></a><span data-ttu-id="806ed-279">Web site extension</span><span class="sxs-lookup"><span data-stu-id="806ed-279">Web site extension</span></span>
<span data-ttu-id="806ed-280">In the web site resource, add a definition for the code to install:</span><span class="sxs-lookup"><span data-stu-id="806ed-280">In the web site resource, add a definition for the code to install:</span></span>

```json
{
  "type": "Microsoft.Web/sites",
  ...
  "resources": [
    {
      "name": "MSDeploy",
      "type": "extensions",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [
        "[concat('Microsoft.Web/sites/', parameters('<site-name>'))]"
      ],
      "properties": {
        "packageUri": "[concat(parameters('<artifacts-location>'), '/', parameters('<package-folder>'), '/', parameters('<package-file-name>'), parameters('<sas-token>'))]",
        "dbType": "None",
        "connectionString": "",
        "setParameters": {
          "IIS Web Application Name": "[parameters('<site-name>')]"
        }
      }
    }
  ]
}
```

### <a name="virtual-machine-extension"></a><span data-ttu-id="806ed-281">Virtual machine extension</span><span class="sxs-lookup"><span data-stu-id="806ed-281">Virtual machine extension</span></span>
<span data-ttu-id="806ed-282">For examples of virtual machine extensions, see [Azure Windows VM Extension Configuration Samples](../virtual-machines/windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="806ed-282">For examples of virtual machine extensions, see [Azure Windows VM Extension Configuration Samples](../virtual-machines/windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="virtual-network-gateway"></a><span data-ttu-id="806ed-283">Virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="806ed-283">Virtual network gateway</span></span>
<span data-ttu-id="806ed-284">Add a virtual network gateway resource type.</span><span class="sxs-lookup"><span data-stu-id="806ed-284">Add a virtual network gateway resource type.</span></span>

```json
{
  "type": "Microsoft.Network/virtualNetworkGateways",
  "name": "[parameters('<gateway-name>')]",
  "apiVersion": "2015-06-15",
  "location": "[resourceGroup().location]",
  "properties": {
    "gatewayType": "[parameters('<gateway-type>')]",
    "ipConfigurations": [
      {
        "name": "default",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[resourceId('Microsoft.Network/virtualNetworks/subnets', parameters('<vnet-name>'), parameters('<new-subnet-name>'))]"
          },
          "publicIpAddress": {
            "id": "[resourceId('Microsoft.Network/publicIPAddresses', parameters('<new-public-ip-address-Name>'))]"
          }
        }
      }
    ],
    "enableBgp": false,
    "vpnType": "[parameters('<vpn-type>')]"
  },
  "dependsOn": [
    "Microsoft.Network/virtualNetworks/codegroup4/subnets/GatewaySubnet",
    "[concat('Microsoft.Network/publicIPAddresses/', parameters('<new-public-ip-address-Name>'))]"
  ]
},
```

### <a name="local-network-gateway"></a><span data-ttu-id="806ed-285">Local network gateway</span><span class="sxs-lookup"><span data-stu-id="806ed-285">Local network gateway</span></span>
<span data-ttu-id="806ed-286">Add a local network gateway resource type.</span><span class="sxs-lookup"><span data-stu-id="806ed-286">Add a local network gateway resource type.</span></span>

```json
{
    "type": "Microsoft.Network/localNetworkGateways",
    "name": "[parameters('<local-network-gateway-name>')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
      "localNetworkAddressSpace": {
        "addressPrefixes": "[parameters('<address-prefixes>')]"
      }
    }
}
```

### <a name="connection"></a><span data-ttu-id="806ed-287">Connection</span><span class="sxs-lookup"><span data-stu-id="806ed-287">Connection</span></span>
<span data-ttu-id="806ed-288">Add a connection resource type.</span><span class="sxs-lookup"><span data-stu-id="806ed-288">Add a connection resource type.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "name": "[parameters('<connection-name>')]",
    "type": "Microsoft.Network/connections",
    "location": "[resourceGroup().location]",
    "properties": {
        "virtualNetworkGateway1": {
        "id": "[resourceId('Microsoft.Network/virtualNetworkGateways', parameters('<gateway-name>'))]"
      },
      "localNetworkGateway2": {
        "id": "[resourceId('Microsoft.Network/localNetworkGateways', parameters('<local-gateway-name>'))]"
      },
      "connectionType": "IPsec",
      "routingWeight": 10,
      "sharedKey": "[parameters('<shared-key>')]"
    }
},
```


## <a name="next-steps"></a><span data-ttu-id="806ed-289">Next steps</span><span class="sxs-lookup"><span data-stu-id="806ed-289">Next steps</span></span>
<span data-ttu-id="806ed-290">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="806ed-290">Congratulations!</span></span> <span data-ttu-id="806ed-291">You have learned how to export a template from resources that you created in the portal.</span><span class="sxs-lookup"><span data-stu-id="806ed-291">You have learned how to export a template from resources that you created in the portal.</span></span>

* <span data-ttu-id="806ed-292">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="806ed-292">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="806ed-293">To see how to export a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="806ed-293">To see how to export a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="806ed-294">To see how to export a template through Azure CLI, see [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="806ed-294">To see how to export a template through Azure CLI, see [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>























