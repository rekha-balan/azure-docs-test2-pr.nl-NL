---
title: Guidance on deploying Azure web apps by using templates | Microsoft Docs
description: Recommendations for creating Azure Resource Manager templates to deploy web apps.
services: app-service
documentationcenter: app-service
author: tfitzmac
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2018
ms.author: tomfitz
ms.openlocfilehash: c2f600d86965e1115d4be1370da8f7c8e1b67f05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870854"
---
# <a name="guidance-on-deploying-web-apps-by-using-azure-resource-manager-templates"></a><span data-ttu-id="724cb-103">Guidance on deploying web apps by using Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="724cb-103">Guidance on deploying web apps by using Azure Resource Manager templates</span></span>

<span data-ttu-id="724cb-104">This article provides recommendations for creating Azure Resource Manager templates to deploy Azure App Service solutions.</span><span class="sxs-lookup"><span data-stu-id="724cb-104">This article provides recommendations for creating Azure Resource Manager templates to deploy Azure App Service solutions.</span></span> <span data-ttu-id="724cb-105">These recommendations can help you avoid common problems.</span><span class="sxs-lookup"><span data-stu-id="724cb-105">These recommendations can help you avoid common problems.</span></span>

## <a name="define-dependencies"></a><span data-ttu-id="724cb-106">Define dependencies</span><span class="sxs-lookup"><span data-stu-id="724cb-106">Define dependencies</span></span>

<span data-ttu-id="724cb-107">Defining dependencies for web apps requires an understanding of how the resources within a web app interact.</span><span class="sxs-lookup"><span data-stu-id="724cb-107">Defining dependencies for web apps requires an understanding of how the resources within a web app interact.</span></span> <span data-ttu-id="724cb-108">If you specify dependencies in an incorrect order, you might cause deployment errors or create a race condition that stalls the deployment.</span><span class="sxs-lookup"><span data-stu-id="724cb-108">If you specify dependencies in an incorrect order, you might cause deployment errors or create a race condition that stalls the deployment.</span></span>

> [!WARNING]
> <span data-ttu-id="724cb-109">If you include an MSDeploy site extension in your template, you must set any configuration resources as dependent on the MSDeploy resource.</span><span class="sxs-lookup"><span data-stu-id="724cb-109">If you include an MSDeploy site extension in your template, you must set any configuration resources as dependent on the MSDeploy resource.</span></span> <span data-ttu-id="724cb-110">Configuration changes cause the site to restart asynchronously.</span><span class="sxs-lookup"><span data-stu-id="724cb-110">Configuration changes cause the site to restart asynchronously.</span></span> <span data-ttu-id="724cb-111">By making the configuration resources dependent on MSDeploy, you ensure that MSDeploy finishes before the site restarts.</span><span class="sxs-lookup"><span data-stu-id="724cb-111">By making the configuration resources dependent on MSDeploy, you ensure that MSDeploy finishes before the site restarts.</span></span> <span data-ttu-id="724cb-112">Without these dependencies, the site might restart during the deployment process of MSDeploy.</span><span class="sxs-lookup"><span data-stu-id="724cb-112">Without these dependencies, the site might restart during the deployment process of MSDeploy.</span></span> <span data-ttu-id="724cb-113">For an example template, see [WordPress Template with Web Deploy Dependency](https://github.com/davidebbo/AzureWebsitesSamples/blob/master/ARMTemplates/WordpressTemplateWebDeployDependency.json).</span><span class="sxs-lookup"><span data-stu-id="724cb-113">For an example template, see [WordPress Template with Web Deploy Dependency](https://github.com/davidebbo/AzureWebsitesSamples/blob/master/ARMTemplates/WordpressTemplateWebDeployDependency.json).</span></span>

<span data-ttu-id="724cb-114">The following image shows the dependency order for various App Service resources:</span><span class="sxs-lookup"><span data-stu-id="724cb-114">The following image shows the dependency order for various App Service resources:</span></span>

![Web app dependencies](media/web-sites-rm-template-guidance/web-dependencies.png)

<span data-ttu-id="724cb-116">You deploy resources in the following order:</span><span class="sxs-lookup"><span data-stu-id="724cb-116">You deploy resources in the following order:</span></span>

<span data-ttu-id="724cb-117">**Tier 1**</span><span class="sxs-lookup"><span data-stu-id="724cb-117">**Tier 1**</span></span>
* <span data-ttu-id="724cb-118">App Service plan.</span><span class="sxs-lookup"><span data-stu-id="724cb-118">App Service plan.</span></span>
* <span data-ttu-id="724cb-119">Any other related resources, like databases or storage accounts.</span><span class="sxs-lookup"><span data-stu-id="724cb-119">Any other related resources, like databases or storage accounts.</span></span>

<span data-ttu-id="724cb-120">**Tier 2**</span><span class="sxs-lookup"><span data-stu-id="724cb-120">**Tier 2**</span></span>
* <span data-ttu-id="724cb-121">Web app--depends on the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="724cb-121">Web app--depends on the App Service plan.</span></span>
* <span data-ttu-id="724cb-122">Azure Application Insights instance that targets the server farm--depends on the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="724cb-122">Azure Application Insights instance that targets the server farm--depends on the App Service plan.</span></span>

<span data-ttu-id="724cb-123">**Tier 3**</span><span class="sxs-lookup"><span data-stu-id="724cb-123">**Tier 3**</span></span>
* <span data-ttu-id="724cb-124">Source control--depends on the web app.</span><span class="sxs-lookup"><span data-stu-id="724cb-124">Source control--depends on the web app.</span></span>
* <span data-ttu-id="724cb-125">MSDeploy site extension--depends on the web app.</span><span class="sxs-lookup"><span data-stu-id="724cb-125">MSDeploy site extension--depends on the web app.</span></span>
* <span data-ttu-id="724cb-126">Application Insights instance that targets the server farm--depends on the web app.</span><span class="sxs-lookup"><span data-stu-id="724cb-126">Application Insights instance that targets the server farm--depends on the web app.</span></span>

<span data-ttu-id="724cb-127">**Tier 4**</span><span class="sxs-lookup"><span data-stu-id="724cb-127">**Tier 4**</span></span>
* <span data-ttu-id="724cb-128">App Service certificate--depends on source control or MSDeploy if either is present.</span><span class="sxs-lookup"><span data-stu-id="724cb-128">App Service certificate--depends on source control or MSDeploy if either is present.</span></span> <span data-ttu-id="724cb-129">Otherwise, it depends on the web app.</span><span class="sxs-lookup"><span data-stu-id="724cb-129">Otherwise, it depends on the web app.</span></span>
* <span data-ttu-id="724cb-130">Configuration settings (connection strings, web.config values, app settings)--depends on source control or MSDeploy if either is present.</span><span class="sxs-lookup"><span data-stu-id="724cb-130">Configuration settings (connection strings, web.config values, app settings)--depends on source control or MSDeploy if either is present.</span></span> <span data-ttu-id="724cb-131">Otherwise, it depends on the web app.</span><span class="sxs-lookup"><span data-stu-id="724cb-131">Otherwise, it depends on the web app.</span></span>

<span data-ttu-id="724cb-132">**Tier 5**</span><span class="sxs-lookup"><span data-stu-id="724cb-132">**Tier 5**</span></span>
* <span data-ttu-id="724cb-133">Host name bindings--depends on the certificate if present.</span><span class="sxs-lookup"><span data-stu-id="724cb-133">Host name bindings--depends on the certificate if present.</span></span> <span data-ttu-id="724cb-134">Otherwise, it depends on a higher-level resource.</span><span class="sxs-lookup"><span data-stu-id="724cb-134">Otherwise, it depends on a higher-level resource.</span></span>
* <span data-ttu-id="724cb-135">Site extensions--depends on configuration settings if present.</span><span class="sxs-lookup"><span data-stu-id="724cb-135">Site extensions--depends on configuration settings if present.</span></span> <span data-ttu-id="724cb-136">Otherwise, it depends on a higher-level resource.</span><span class="sxs-lookup"><span data-stu-id="724cb-136">Otherwise, it depends on a higher-level resource.</span></span>

<span data-ttu-id="724cb-137">Typically, your solution includes only some of these resources and tiers.</span><span class="sxs-lookup"><span data-stu-id="724cb-137">Typically, your solution includes only some of these resources and tiers.</span></span> <span data-ttu-id="724cb-138">For missing tiers, map lower resources to the next-higher tier.</span><span class="sxs-lookup"><span data-stu-id="724cb-138">For missing tiers, map lower resources to the next-higher tier.</span></span>

<span data-ttu-id="724cb-139">The following example shows part of a template.</span><span class="sxs-lookup"><span data-stu-id="724cb-139">The following example shows part of a template.</span></span> <span data-ttu-id="724cb-140">The value of the connection string configuration depends on the MSDeploy extension.</span><span class="sxs-lookup"><span data-stu-id="724cb-140">The value of the connection string configuration depends on the MSDeploy extension.</span></span> <span data-ttu-id="724cb-141">The MSDeploy extension depends on the web app and database.</span><span class="sxs-lookup"><span data-stu-id="724cb-141">The MSDeploy extension depends on the web app and database.</span></span> 

```json
{
    "name": "[parameters('appName')]",
    "type": "Microsoft.Web/Sites",
    ...
    "resources": [
      {
          "name": "MSDeploy",
          "type": "Extensions",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', parameters('appName'))]",
            "[concat('Microsoft.Sql/servers/', parameters('dbServerName'), '/databases/', parameters('dbName'))]",
          ],
          ...
      },
      {
          "name": "connectionstrings",
          "type": "config",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', parameters('appName'), '/Extensions/MSDeploy')]"
          ],
          ...
      }
    ]
}
```

<span data-ttu-id="724cb-142">For a ready-to-run sample that uses the code above, see [Template: Build a simple Umbraco Web App](https://github.com/Azure/azure-quickstart-templates/tree/master/umbraco-webapp-simple).</span><span class="sxs-lookup"><span data-stu-id="724cb-142">For a ready-to-run sample that uses the code above, see [Template: Build a simple Umbraco Web App](https://github.com/Azure/azure-quickstart-templates/tree/master/umbraco-webapp-simple).</span></span>

## <a name="find-information-about-msdeploy-errors"></a><span data-ttu-id="724cb-143">Find information about MSDeploy errors</span><span class="sxs-lookup"><span data-stu-id="724cb-143">Find information about MSDeploy errors</span></span>

<span data-ttu-id="724cb-144">If your Resource Manager template uses MSDeploy, the deployment error messages can be difficult to understand.</span><span class="sxs-lookup"><span data-stu-id="724cb-144">If your Resource Manager template uses MSDeploy, the deployment error messages can be difficult to understand.</span></span> <span data-ttu-id="724cb-145">To get more information after a failed deployment, try the following steps:</span><span class="sxs-lookup"><span data-stu-id="724cb-145">To get more information after a failed deployment, try the following steps:</span></span>

1. <span data-ttu-id="724cb-146">Go to the site's [Kudu console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="724cb-146">Go to the site's [Kudu console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span>
2. <span data-ttu-id="724cb-147">Browse to the folder at D:\home\LogFiles\SiteExtensions\MSDeploy.</span><span class="sxs-lookup"><span data-stu-id="724cb-147">Browse to the folder at D:\home\LogFiles\SiteExtensions\MSDeploy.</span></span>
3. <span data-ttu-id="724cb-148">Look for the appManagerStatus.xml and appManagerLog.xml files.</span><span class="sxs-lookup"><span data-stu-id="724cb-148">Look for the appManagerStatus.xml and appManagerLog.xml files.</span></span> <span data-ttu-id="724cb-149">The first file logs the status.</span><span class="sxs-lookup"><span data-stu-id="724cb-149">The first file logs the status.</span></span> <span data-ttu-id="724cb-150">The second file logs information about the error.</span><span class="sxs-lookup"><span data-stu-id="724cb-150">The second file logs information about the error.</span></span> <span data-ttu-id="724cb-151">If the error isn't clear to you, you can include it when you're asking for help on the forum.</span><span class="sxs-lookup"><span data-stu-id="724cb-151">If the error isn't clear to you, you can include it when you're asking for help on the forum.</span></span>

## <a name="choose-a-unique-web-app-name"></a><span data-ttu-id="724cb-152">Choose a unique web app name</span><span class="sxs-lookup"><span data-stu-id="724cb-152">Choose a unique web app name</span></span>

<span data-ttu-id="724cb-153">The name for your web app must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="724cb-153">The name for your web app must be globally unique.</span></span> <span data-ttu-id="724cb-154">You can use a naming convention that's likely to be unique, or you can use the [uniqueString function](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) to assist with generating a unique name.</span><span class="sxs-lookup"><span data-stu-id="724cb-154">You can use a naming convention that's likely to be unique, or you can use the [uniqueString function](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) to assist with generating a unique name.</span></span>

```json
{
  "apiVersion": "2016-08-01",
  "name": "[concat(parameters('siteNamePrefix'), uniqueString(resourceGroup().id))]",
  "type": "Microsoft.Web/sites",
  ...
}
```

## <a name="deploy-web-app-certificate-from-key-vault"></a><span data-ttu-id="724cb-155">Deploy web app certificate from Key Vault</span><span class="sxs-lookup"><span data-stu-id="724cb-155">Deploy web app certificate from Key Vault</span></span>

<span data-ttu-id="724cb-156">If your template includes a [Microsoft.Web/certificates](/azure/templates/microsoft.web/certificates) resource for SSL binding, and the certificate is stored in a Key Vault, you must make sure the App Service identity can access the certificate.</span><span class="sxs-lookup"><span data-stu-id="724cb-156">If your template includes a [Microsoft.Web/certificates](/azure/templates/microsoft.web/certificates) resource for SSL binding, and the certificate is stored in a Key Vault, you must make sure the App Service identity can access the certificate.</span></span>

<span data-ttu-id="724cb-157">In global Azure, the App Service service principal has the ID of **abfa0a7c-a6b6-4736-8310-5855508787cd**.</span><span class="sxs-lookup"><span data-stu-id="724cb-157">In global Azure, the App Service service principal has the ID of **abfa0a7c-a6b6-4736-8310-5855508787cd**.</span></span> <span data-ttu-id="724cb-158">To grant access to Key Vault for the App Service service principal, use:</span><span class="sxs-lookup"><span data-stu-id="724cb-158">To grant access to Key Vault for the App Service service principal, use:</span></span>

```azurepowershell-interactive
Set-AzureRmKeyVaultAccessPolicy `
  -VaultName KEY_VAULT_NAME `
  -ServicePrincipalName abfa0a7c-a6b6-4736-8310-5855508787cd `
  -PermissionsToSecrets get `
  -PermissionsToCertificates get
```

<span data-ttu-id="724cb-159">In Azure Government, the App Service service principal has the ID of **6a02c803-dafd-4136-b4c3-5a6f318b4714**.</span><span class="sxs-lookup"><span data-stu-id="724cb-159">In Azure Government, the App Service service principal has the ID of **6a02c803-dafd-4136-b4c3-5a6f318b4714**.</span></span> <span data-ttu-id="724cb-160">Use that ID in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="724cb-160">Use that ID in the preceding example.</span></span>

<span data-ttu-id="724cb-161">In your Key Vault, select **Certificates** and **Generate/Import** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="724cb-161">In your Key Vault, select **Certificates** and **Generate/Import** to upload the certificate.</span></span>

![Import certificate](media/web-sites-rm-template-guidance/import-certificate.png)

<span data-ttu-id="724cb-163">In your template, provide the name of the certificate for the `keyVaultSecretName`.</span><span class="sxs-lookup"><span data-stu-id="724cb-163">In your template, provide the name of the certificate for the `keyVaultSecretName`.</span></span>

<span data-ttu-id="724cb-164">For an example template, see [Deploy a Web App certificate from Key Vault secret and use it for creating SSL binding](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-certificate-from-key-vault).</span><span class="sxs-lookup"><span data-stu-id="724cb-164">For an example template, see [Deploy a Web App certificate from Key Vault secret and use it for creating SSL binding](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-certificate-from-key-vault).</span></span>

## <a name="next-steps"></a><span data-ttu-id="724cb-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="724cb-165">Next steps</span></span>

* <span data-ttu-id="724cb-166">For a tutorial on deploying web apps with a template, see [Provision and deploy microservices predictably in Azure](app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="724cb-166">For a tutorial on deploying web apps with a template, see [Provision and deploy microservices predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>