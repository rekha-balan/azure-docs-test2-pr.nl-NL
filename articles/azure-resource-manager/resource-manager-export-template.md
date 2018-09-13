---
title: Export Azure Resource Manager template | Microsoft Docs
description: Use Azure Resource Manage to export a template from an existing resource group.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/26/2018
ms.author: tomfitz
ms.openlocfilehash: 3e1dd8ad49ceb126a14070ed641146d91419640a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773896"
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="754e5-103">Export an Azure Resource Manager template from existing resources</span><span class="sxs-lookup"><span data-stu-id="754e5-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="754e5-104">In this article, you learn how to export a Resource Manager template from existing resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="754e5-104">In this article, you learn how to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="754e5-105">You can use that generated template to gain a better understanding of template syntax.</span><span class="sxs-lookup"><span data-stu-id="754e5-105">You can use that generated template to gain a better understanding of template syntax.</span></span>

<span data-ttu-id="754e5-106">There are two ways to export a template:</span><span class="sxs-lookup"><span data-stu-id="754e5-106">There are two ways to export a template:</span></span>

* <span data-ttu-id="754e5-107">You can export the **actual template used for deployment**.</span><span class="sxs-lookup"><span data-stu-id="754e5-107">You can export the **actual template used for deployment**.</span></span> <span data-ttu-id="754e5-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span><span class="sxs-lookup"><span data-stu-id="754e5-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="754e5-109">This approach is helpful when you deployed resources through the portal, and want to see the template to create those resources.</span><span class="sxs-lookup"><span data-stu-id="754e5-109">This approach is helpful when you deployed resources through the portal, and want to see the template to create those resources.</span></span> <span data-ttu-id="754e5-110">This template is readily usable.</span><span class="sxs-lookup"><span data-stu-id="754e5-110">This template is readily usable.</span></span> 
* <span data-ttu-id="754e5-111">You can export a **generated template that represents the current state of the resource group**.</span><span class="sxs-lookup"><span data-stu-id="754e5-111">You can export a **generated template that represents the current state of the resource group**.</span></span> <span data-ttu-id="754e5-112">The exported template isn't based on any template that you used for deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-112">The exported template isn't based on any template that you used for deployment.</span></span> <span data-ttu-id="754e5-113">Instead, it creates a template that is a "snapshot" or "backup" of the resource group.</span><span class="sxs-lookup"><span data-stu-id="754e5-113">Instead, it creates a template that is a "snapshot" or "backup" of the resource group.</span></span> <span data-ttu-id="754e5-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span><span class="sxs-lookup"><span data-stu-id="754e5-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="754e5-115">Use this option to redeploy resources to the same resource group.</span><span class="sxs-lookup"><span data-stu-id="754e5-115">Use this option to redeploy resources to the same resource group.</span></span> <span data-ttu-id="754e5-116">To use this template for another resource group, you may have to significantly modify it.</span><span class="sxs-lookup"><span data-stu-id="754e5-116">To use this template for another resource group, you may have to significantly modify it.</span></span>

<span data-ttu-id="754e5-117">This article shows both approaches through the portal.</span><span class="sxs-lookup"><span data-stu-id="754e5-117">This article shows both approaches through the portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="754e5-118">Deploy resources</span><span class="sxs-lookup"><span data-stu-id="754e5-118">Deploy resources</span></span>
<span data-ttu-id="754e5-119">Let's start by deploying resources to Azure that you can use for exporting as a template.</span><span class="sxs-lookup"><span data-stu-id="754e5-119">Let's start by deploying resources to Azure that you can use for exporting as a template.</span></span> <span data-ttu-id="754e5-120">If you already have a resource group in your subscription that you want to export to a template, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="754e5-120">If you already have a resource group in your subscription that you want to export to a template, you can skip this section.</span></span> <span data-ttu-id="754e5-121">The rest of this article assumes you've deployed the web app and SQL database solution shown in this section.</span><span class="sxs-lookup"><span data-stu-id="754e5-121">The rest of this article assumes you've deployed the web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="754e5-122">If you use a different solution, your experience might be a little different, but the steps to export a template are the same.</span><span class="sxs-lookup"><span data-stu-id="754e5-122">If you use a different solution, your experience might be a little different, but the steps to export a template are the same.</span></span> 

1. <span data-ttu-id="754e5-123">In the [Azure portal](https://portal.azure.com), select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="754e5-123">In the [Azure portal](https://portal.azure.com), select **Create a resource**.</span></span>
   
      ![Select new](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="754e5-125">Search for **web app + SQL** and select it from the available options.</span><span class="sxs-lookup"><span data-stu-id="754e5-125">Search for **web app + SQL** and select it from the available options.</span></span>
   
      ![Search web app and SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="754e5-127">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="754e5-127">Select **Create**.</span></span>

      ![Select create](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="754e5-129">Provide the required values for the web app and SQL database.</span><span class="sxs-lookup"><span data-stu-id="754e5-129">Provide the required values for the web app and SQL database.</span></span> <span data-ttu-id="754e5-130">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="754e5-130">Select **Create**.</span></span>

      ![Provide web and SQL value](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="754e5-132">The deployment may take a minute.</span><span class="sxs-lookup"><span data-stu-id="754e5-132">The deployment may take a minute.</span></span> <span data-ttu-id="754e5-133">After the deployment finishes, your subscription contains the solution.</span><span class="sxs-lookup"><span data-stu-id="754e5-133">After the deployment finishes, your subscription contains the solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="754e5-134">View template from deployment history</span><span class="sxs-lookup"><span data-stu-id="754e5-134">View template from deployment history</span></span>
1. <span data-ttu-id="754e5-135">Go to the resource group for your new resource group.</span><span class="sxs-lookup"><span data-stu-id="754e5-135">Go to the resource group for your new resource group.</span></span> <span data-ttu-id="754e5-136">Notice that the portal shows the result of the last deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-136">Notice that the portal shows the result of the last deployment.</span></span> <span data-ttu-id="754e5-137">Select this link.</span><span class="sxs-lookup"><span data-stu-id="754e5-137">Select this link.</span></span>
   
      ![Resource group](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="754e5-139">You see a history of deployments for the group.</span><span class="sxs-lookup"><span data-stu-id="754e5-139">You see a history of deployments for the group.</span></span> <span data-ttu-id="754e5-140">In your case, the portal probably lists only one deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-140">In your case, the portal probably lists only one deployment.</span></span> <span data-ttu-id="754e5-141">Select this deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-141">Select this deployment.</span></span>
   
     ![Last deployment](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="754e5-143">The portal displays a summary of the deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-143">The portal displays a summary of the deployment.</span></span> <span data-ttu-id="754e5-144">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span><span class="sxs-lookup"><span data-stu-id="754e5-144">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span></span> <span data-ttu-id="754e5-145">To see the template that you used for the deployment, select **View template**.</span><span class="sxs-lookup"><span data-stu-id="754e5-145">To see the template that you used for the deployment, select **View template**.</span></span>
   
     ![View deployment summary](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="754e5-147">Resource Manager retrieves the following seven files for you:</span><span class="sxs-lookup"><span data-stu-id="754e5-147">Resource Manager retrieves the following seven files for you:</span></span>
   
   1. <span data-ttu-id="754e5-148">**Template** - The template that defines the infrastructure for your solution.</span><span class="sxs-lookup"><span data-stu-id="754e5-148">**Template** - The template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="754e5-149">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span><span class="sxs-lookup"><span data-stu-id="754e5-149">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="754e5-150">**Parameters** - A parameter file that you can use to pass in values during deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-150">**Parameters** - A parameter file that you can use to pass in values during deployment.</span></span> <span data-ttu-id="754e5-151">It contains the values that you provided during the first deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-151">It contains the values that you provided during the first deployment.</span></span> <span data-ttu-id="754e5-152">You can change any of these values when you redeploy the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-152">You can change any of these values when you redeploy the template.</span></span>
   3. <span data-ttu-id="754e5-153">**CLI** - An Azure CLI script file that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-153">**CLI** - An Azure CLI script file that you can use to deploy the template.</span></span>
   4. <span data-ttu-id="754e5-154">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-154">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span></span>
   5. <span data-ttu-id="754e5-155">**.NET** - A .NET class that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-155">**.NET** - A .NET class that you can use to deploy the template.</span></span>
   6. <span data-ttu-id="754e5-156">**Ruby** - A Ruby class that you can use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-156">**Ruby** - A Ruby class that you can use to deploy the template.</span></span>
      
      <span data-ttu-id="754e5-157">By default, the portal displays the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-157">By default, the portal displays the template.</span></span>
      
       ![View template](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="754e5-159">This template is the actual template used to create your web app and SQL database.</span><span class="sxs-lookup"><span data-stu-id="754e5-159">This template is the actual template used to create your web app and SQL database.</span></span> <span data-ttu-id="754e5-160">Notice it contains parameters that enable you to provide different values during deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-160">Notice it contains parameters that enable you to provide different values during deployment.</span></span> <span data-ttu-id="754e5-161">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="754e5-161">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-the-template-from-resource-group"></a><span data-ttu-id="754e5-162">Export the template from resource group</span><span class="sxs-lookup"><span data-stu-id="754e5-162">Export the template from resource group</span></span>
<span data-ttu-id="754e5-163">If you've manually changed your resources or added resources in multiple deployments, retrieving a template from the deployment history doesn't reflect the current state of the resource group.</span><span class="sxs-lookup"><span data-stu-id="754e5-163">If you've manually changed your resources or added resources in multiple deployments, retrieving a template from the deployment history doesn't reflect the current state of the resource group.</span></span> <span data-ttu-id="754e5-164">This section shows you how to export a template that reflects the current state of the resource group.</span><span class="sxs-lookup"><span data-stu-id="754e5-164">This section shows you how to export a template that reflects the current state of the resource group.</span></span> <span data-ttu-id="754e5-165">It is intended as a snapshot of the resource group, which you can use to redeploy to the same resource group.</span><span class="sxs-lookup"><span data-stu-id="754e5-165">It is intended as a snapshot of the resource group, which you can use to redeploy to the same resource group.</span></span> <span data-ttu-id="754e5-166">To use the exported template for other solutions, you must significantly modify it.</span><span class="sxs-lookup"><span data-stu-id="754e5-166">To use the exported template for other solutions, you must significantly modify it.</span></span>

> [!NOTE]
> <span data-ttu-id="754e5-167">You can't export a template for a resource group that has more than 200 resources.</span><span class="sxs-lookup"><span data-stu-id="754e5-167">You can't export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="754e5-168">To view the template for a resource group, select **Automation script**.</span><span class="sxs-lookup"><span data-stu-id="754e5-168">To view the template for a resource group, select **Automation script**.</span></span>
   
      ![Export resource group](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="754e5-170">Resource Manager evaluates the resources in the resource group, and generates a template for those resources.</span><span class="sxs-lookup"><span data-stu-id="754e5-170">Resource Manager evaluates the resources in the resource group, and generates a template for those resources.</span></span> <span data-ttu-id="754e5-171">Not all resource types support the export template function.</span><span class="sxs-lookup"><span data-stu-id="754e5-171">Not all resource types support the export template function.</span></span> <span data-ttu-id="754e5-172">You may see an error stating that there is a problem with the export.</span><span class="sxs-lookup"><span data-stu-id="754e5-172">You may see an error stating that there is a problem with the export.</span></span> <span data-ttu-id="754e5-173">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span><span class="sxs-lookup"><span data-stu-id="754e5-173">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="754e5-174">You again see the six files that you can use to redeploy the solution.</span><span class="sxs-lookup"><span data-stu-id="754e5-174">You again see the six files that you can use to redeploy the solution.</span></span> <span data-ttu-id="754e5-175">However, this time the template is a little different.</span><span class="sxs-lookup"><span data-stu-id="754e5-175">However, this time the template is a little different.</span></span> <span data-ttu-id="754e5-176">Notice that the generated template contains fewer parameters than the template in previous section.</span><span class="sxs-lookup"><span data-stu-id="754e5-176">Notice that the generated template contains fewer parameters than the template in previous section.</span></span> <span data-ttu-id="754e5-177">Also, many of the values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span><span class="sxs-lookup"><span data-stu-id="754e5-177">Also, many of the values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="754e5-178">Before reusing this template, you might want to edit the template to make better use of parameters.</span><span class="sxs-lookup"><span data-stu-id="754e5-178">Before reusing this template, you might want to edit the template to make better use of parameters.</span></span> 
   
3. <span data-ttu-id="754e5-179">You have a couple of options for continuing to work with this template.</span><span class="sxs-lookup"><span data-stu-id="754e5-179">You have a couple of options for continuing to work with this template.</span></span> <span data-ttu-id="754e5-180">You can either download the template and work on it locally with a JSON editor.</span><span class="sxs-lookup"><span data-stu-id="754e5-180">You can either download the template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="754e5-181">Or, you can save the template to your library and work on it through the portal.</span><span class="sxs-lookup"><span data-stu-id="754e5-181">Or, you can save the template to your library and work on it through the portal.</span></span>
   
     <span data-ttu-id="754e5-182">If you're comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span><span class="sxs-lookup"><span data-stu-id="754e5-182">If you're comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span></span> <span data-ttu-id="754e5-183">To work locally, select **Download**.</span><span class="sxs-lookup"><span data-stu-id="754e5-183">To work locally, select **Download**.</span></span>
   
      ![Download template](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="754e5-185">If you aren't set up with a JSON editor, you might prefer editing the template through the portal.</span><span class="sxs-lookup"><span data-stu-id="754e5-185">If you aren't set up with a JSON editor, you might prefer editing the template through the portal.</span></span> <span data-ttu-id="754e5-186">The rest of this article assumes you've saved the template to your library in the portal.</span><span class="sxs-lookup"><span data-stu-id="754e5-186">The rest of this article assumes you've saved the template to your library in the portal.</span></span> <span data-ttu-id="754e5-187">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span><span class="sxs-lookup"><span data-stu-id="754e5-187">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span></span> <span data-ttu-id="754e5-188">To work through the portal, select **Add to library**.</span><span class="sxs-lookup"><span data-stu-id="754e5-188">To work through the portal, select **Add to library**.</span></span>
   
      ![Add to library](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="754e5-190">When adding a template to the library, you give the template a name and description.</span><span class="sxs-lookup"><span data-stu-id="754e5-190">When adding a template to the library, you give the template a name and description.</span></span> <span data-ttu-id="754e5-191">Then, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="754e5-191">Then, select **Save**.</span></span>
   
     ![Set template values](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="754e5-193">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span><span class="sxs-lookup"><span data-stu-id="754e5-193">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span></span>
   
      ![Find templates](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="754e5-195">Select the template with the name you saved.</span><span class="sxs-lookup"><span data-stu-id="754e5-195">Select the template with the name you saved.</span></span>
   
      ![Select template](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-the-template"></a><span data-ttu-id="754e5-197">Customize the template</span><span class="sxs-lookup"><span data-stu-id="754e5-197">Customize the template</span></span>
<span data-ttu-id="754e5-198">The exported template works fine if you want to create the same web app and SQL database for every deployment.</span><span class="sxs-lookup"><span data-stu-id="754e5-198">The exported template works fine if you want to create the same web app and SQL database for every deployment.</span></span> <span data-ttu-id="754e5-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span><span class="sxs-lookup"><span data-stu-id="754e5-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="754e5-200">This article shows you how to add parameters for the database administrator name and password.</span><span class="sxs-lookup"><span data-stu-id="754e5-200">This article shows you how to add parameters for the database administrator name and password.</span></span> <span data-ttu-id="754e5-201">You can use this same approach to add more flexibility for other values in the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-201">You can use this same approach to add more flexibility for other values in the template.</span></span>

1. <span data-ttu-id="754e5-202">To customize the template, select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="754e5-202">To customize the template, select **Edit**.</span></span>
   
     ![Show template](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="754e5-204">Select the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-204">Select the template.</span></span>
   
     ![Edit template](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="754e5-206">To pass values that you might want to specify during deployment, add the following two parameters to the **parameters** section in the template:</span><span class="sxs-lookup"><span data-stu-id="754e5-206">To pass values that you might want to specify during deployment, add the following two parameters to the **parameters** section in the template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="754e5-207">To use the new parameters, replace the SQL server definition in the **resources** section.</span><span class="sxs-lookup"><span data-stu-id="754e5-207">To use the new parameters, replace the SQL server definition in the **resources** section.</span></span> <span data-ttu-id="754e5-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span><span class="sxs-lookup"><span data-stu-id="754e5-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="754e5-209">Select **OK** when you're done editing the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-209">Select **OK** when you're done editing the template.</span></span>
7. <span data-ttu-id="754e5-210">Select **Save** to save the changes to the template.</span><span class="sxs-lookup"><span data-stu-id="754e5-210">Select **Save** to save the changes to the template.</span></span>
   
     ![Save template](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="754e5-212">To redeploy the updated template, select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="754e5-212">To redeploy the updated template, select **Deploy**.</span></span>
   
     ![Deploy template](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="754e5-214">Provide parameter values, and select a resource group to deploy the resources to.</span><span class="sxs-lookup"><span data-stu-id="754e5-214">Provide parameter values, and select a resource group to deploy the resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="754e5-215">Fix export issues</span><span class="sxs-lookup"><span data-stu-id="754e5-215">Fix export issues</span></span>
<span data-ttu-id="754e5-216">Not all resource types support the export template function.</span><span class="sxs-lookup"><span data-stu-id="754e5-216">Not all resource types support the export template function.</span></span> <span data-ttu-id="754e5-217">You only see export issues when exporting from a resource group rather than from your deployment history.</span><span class="sxs-lookup"><span data-stu-id="754e5-217">You only see export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="754e5-218">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span><span class="sxs-lookup"><span data-stu-id="754e5-218">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span></span> <span data-ttu-id="754e5-219">Only export from a resource group when you have made changes to the resource group that aren't defined in a single template.</span><span class="sxs-lookup"><span data-stu-id="754e5-219">Only export from a resource group when you have made changes to the resource group that aren't defined in a single template.</span></span>

<span data-ttu-id="754e5-220">To resolve export issues, manually add the missing resources back into your template.</span><span class="sxs-lookup"><span data-stu-id="754e5-220">To resolve export issues, manually add the missing resources back into your template.</span></span> <span data-ttu-id="754e5-221">The error message includes the resource types that can't be exported.</span><span class="sxs-lookup"><span data-stu-id="754e5-221">The error message includes the resource types that can't be exported.</span></span> <span data-ttu-id="754e5-222">Find that resource type in [Template reference](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="754e5-222">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="754e5-223">For example, to manually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="754e5-223">For example, to manually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span> <span data-ttu-id="754e5-224">The template reference gives you the JSON to add the resource to your template.</span><span class="sxs-lookup"><span data-stu-id="754e5-224">The template reference gives you the JSON to add the resource to your template.</span></span>

<span data-ttu-id="754e5-225">After getting the JSON format for the resource, you need to get the resource values.</span><span class="sxs-lookup"><span data-stu-id="754e5-225">After getting the JSON format for the resource, you need to get the resource values.</span></span> <span data-ttu-id="754e5-226">You can see the values for the resource by using the GET operation in the REST API for the resource type.</span><span class="sxs-lookup"><span data-stu-id="754e5-226">You can see the values for the resource by using the GET operation in the REST API for the resource type.</span></span> <span data-ttu-id="754e5-227">For example, to get the values for your virtual network gateway, see [Virtual Network Gateways - Get](/rest/api/network-gateway/virtualnetworkgateways/get).</span><span class="sxs-lookup"><span data-stu-id="754e5-227">For example, to get the values for your virtual network gateway, see [Virtual Network Gateways - Get](/rest/api/network-gateway/virtualnetworkgateways/get).</span></span>

## <a name="next-steps"></a><span data-ttu-id="754e5-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="754e5-228">Next steps</span></span>

* <span data-ttu-id="754e5-229">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="754e5-229">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="754e5-230">To see how to export a template through PowerShell, see [Export Azure Resource Manager templates with PowerShell](resource-manager-export-template-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="754e5-230">To see how to export a template through PowerShell, see [Export Azure Resource Manager templates with PowerShell](resource-manager-export-template-powershell.md).</span></span>
* <span data-ttu-id="754e5-231">To see how to export a template through Azure CLI, see [Export Azure Resource Manager templates with Azure CLI](resource-manager-export-template-cli.md).</span><span class="sxs-lookup"><span data-stu-id="754e5-231">To see how to export a template through Azure CLI, see [Export Azure Resource Manager templates with Azure CLI](resource-manager-export-template-cli.md).</span></span>

