---
title: Managed Service Identity in App Service and Azure Functions | Microsoft Docs
description: Conceptual reference and setup guide for Managed Service Identity support in Azure App Service and Azure Functions
services: app-service
author: mattchenderson
manager: cfowler
editor: ''
ms.service: app-service
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/25/2018
ms.author: mahender
ms.openlocfilehash: c7a819f987de41ba7705d21bb6de95475cd3f9c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870714"
---
# <a name="how-to-use-azure-managed-service-identity-in-app-service-and-azure-functions"></a><span data-ttu-id="e126c-103">How to use Azure Managed Service Identity in App Service and Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e126c-103">How to use Azure Managed Service Identity in App Service and Azure Functions</span></span>

> [!NOTE] 
> <span data-ttu-id="e126c-104">App Service on Linux and Web App for Containers do not currently support Managed Service Identity.</span><span class="sxs-lookup"><span data-stu-id="e126c-104">App Service on Linux and Web App for Containers do not currently support Managed Service Identity.</span></span>

> [!Important] 
> <span data-ttu-id="e126c-105">Managed Service Identity for App Service and Azure Functions will not behave as expected if your app is migrated across subscriptions/tenants.</span><span class="sxs-lookup"><span data-stu-id="e126c-105">Managed Service Identity for App Service and Azure Functions will not behave as expected if your app is migrated across subscriptions/tenants.</span></span> <span data-ttu-id="e126c-106">The app will need to obtain a new identity, which can be done by disabling and re-enabling the feature.</span><span class="sxs-lookup"><span data-stu-id="e126c-106">The app will need to obtain a new identity, which can be done by disabling and re-enabling the feature.</span></span> <span data-ttu-id="e126c-107">See [Removing an identity](#remove) below.</span><span class="sxs-lookup"><span data-stu-id="e126c-107">See [Removing an identity](#remove) below.</span></span> <span data-ttu-id="e126c-108">Downstream resources will also need to have access policies updated to use the new identity.</span><span class="sxs-lookup"><span data-stu-id="e126c-108">Downstream resources will also need to have access policies updated to use the new identity.</span></span>

<span data-ttu-id="e126c-109">This topic shows you how to create a managed app identity for App Service and Azure Functions applications and how to use it to access other resources.</span><span class="sxs-lookup"><span data-stu-id="e126c-109">This topic shows you how to create a managed app identity for App Service and Azure Functions applications and how to use it to access other resources.</span></span> <span data-ttu-id="e126c-110">A managed service identity from Azure Active Directory allows your app to easily access other AAD-protected resources such as Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e126c-110">A managed service identity from Azure Active Directory allows your app to easily access other AAD-protected resources such as Azure Key Vault.</span></span> <span data-ttu-id="e126c-111">The identity is managed by the Azure platform and does not require you to provision or rotate any secrets.</span><span class="sxs-lookup"><span data-stu-id="e126c-111">The identity is managed by the Azure platform and does not require you to provision or rotate any secrets.</span></span> <span data-ttu-id="e126c-112">For more about Managed Service Identity, see the [Managed Service Identity overview](../active-directory/managed-identities-azure-resources/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e126c-112">For more about Managed Service Identity, see the [Managed Service Identity overview](../active-directory/managed-identities-azure-resources/overview.md).</span></span>

## <a name="creating-an-app-with-an-identity"></a><span data-ttu-id="e126c-113">Creating an app with an identity</span><span class="sxs-lookup"><span data-stu-id="e126c-113">Creating an app with an identity</span></span>

<span data-ttu-id="e126c-114">Creating an app with an identity requires an additional property to be set on the application.</span><span class="sxs-lookup"><span data-stu-id="e126c-114">Creating an app with an identity requires an additional property to be set on the application.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="e126c-115">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e126c-115">Using the Azure portal</span></span>

<span data-ttu-id="e126c-116">To set up a managed service identity in the portal, you will first create an application as normal and then enable the feature.</span><span class="sxs-lookup"><span data-stu-id="e126c-116">To set up a managed service identity in the portal, you will first create an application as normal and then enable the feature.</span></span>

1. <span data-ttu-id="e126c-117">Create an app in the portal as you normally would.</span><span class="sxs-lookup"><span data-stu-id="e126c-117">Create an app in the portal as you normally would.</span></span> <span data-ttu-id="e126c-118">Navigate to it in the portal.</span><span class="sxs-lookup"><span data-stu-id="e126c-118">Navigate to it in the portal.</span></span>

2. <span data-ttu-id="e126c-119">If using a function app, navigate to **Platform features**.</span><span class="sxs-lookup"><span data-stu-id="e126c-119">If using a function app, navigate to **Platform features**.</span></span> <span data-ttu-id="e126c-120">For other app types, scroll down to the **Settings** group in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="e126c-120">For other app types, scroll down to the **Settings** group in the left navigation.</span></span>

3. <span data-ttu-id="e126c-121">Select **Managed service identity**.</span><span class="sxs-lookup"><span data-stu-id="e126c-121">Select **Managed service identity**.</span></span>

4. <span data-ttu-id="e126c-122">Switch **Register with Azure Active Directory** to **On**.</span><span class="sxs-lookup"><span data-stu-id="e126c-122">Switch **Register with Azure Active Directory** to **On**.</span></span> <span data-ttu-id="e126c-123">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e126c-123">Click **Save**.</span></span>

![Managed Service Identity in App Service](media/app-service-managed-service-identity/msi-blade.png)

### <a name="using-the-azure-cli"></a><span data-ttu-id="e126c-125">Using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e126c-125">Using the Azure CLI</span></span>

<span data-ttu-id="e126c-126">To set up a managed service identity using the Azure CLI, you will need to use the `az webapp identity assign` command against an existing application.</span><span class="sxs-lookup"><span data-stu-id="e126c-126">To set up a managed service identity using the Azure CLI, you will need to use the `az webapp identity assign` command against an existing application.</span></span> <span data-ttu-id="e126c-127">You have three options for running the examples in this section:</span><span class="sxs-lookup"><span data-stu-id="e126c-127">You have three options for running the examples in this section:</span></span>

- <span data-ttu-id="e126c-128">Use [Azure Cloud Shell](../cloud-shell/overview.md) from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e126c-128">Use [Azure Cloud Shell](../cloud-shell/overview.md) from the Azure portal.</span></span>
- <span data-ttu-id="e126c-129">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block below.</span><span class="sxs-lookup"><span data-stu-id="e126c-129">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block below.</span></span>
- <span data-ttu-id="e126c-130">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.31 or later) if you prefer to use a local CLI console.</span><span class="sxs-lookup"><span data-stu-id="e126c-130">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.31 or later) if you prefer to use a local CLI console.</span></span> 

<span data-ttu-id="e126c-131">The following steps will walk you through creating a web app and assigning it an identity using the CLI:</span><span class="sxs-lookup"><span data-stu-id="e126c-131">The following steps will walk you through creating a web app and assigning it an identity using the CLI:</span></span>

1. <span data-ttu-id="e126c-132">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span><span class="sxs-lookup"><span data-stu-id="e126c-132">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span></span> <span data-ttu-id="e126c-133">Use an account that is associated with the Azure subscription under which you would like to deploy the application:</span><span class="sxs-lookup"><span data-stu-id="e126c-133">Use an account that is associated with the Azure subscription under which you would like to deploy the application:</span></span>

    ```azurecli-interactive
    az login
    ```
2. <span data-ttu-id="e126c-134">Create a web application using the CLI.</span><span class="sxs-lookup"><span data-stu-id="e126c-134">Create a web application using the CLI.</span></span> <span data-ttu-id="e126c-135">For more examples of how to use the CLI with App Service, see [App Service CLI samples](../app-service/app-service-cli-samples.md):</span><span class="sxs-lookup"><span data-stu-id="e126c-135">For more examples of how to use the CLI with App Service, see [App Service CLI samples](../app-service/app-service-cli-samples.md):</span></span>

    ```azurecli-interactive
    az group create --name myResourceGroup --location westus
    az appservice plan create --name myPlan --resource-group myResourceGroup --sku S1
    az webapp create --name myApp --resource-group myResourceGroup --plan myPlan
    ```

3. <span data-ttu-id="e126c-136">Run the `identity assign` command to create the identity for this application:</span><span class="sxs-lookup"><span data-stu-id="e126c-136">Run the `identity assign` command to create the identity for this application:</span></span>

    ```azurecli-interactive
    az webapp identity assign --name myApp --resource-group myResourceGroup
    ```

### <a name="using-azure-powershell"></a><span data-ttu-id="e126c-137">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e126c-137">Using Azure PowerShell</span></span>

<span data-ttu-id="e126c-138">The following steps will walk you through creating a web app and assigning it an identity using Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e126c-138">The following steps will walk you through creating a web app and assigning it an identity using Azure PowerShell:</span></span>

1. <span data-ttu-id="e126c-139">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="e126c-139">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

2. <span data-ttu-id="e126c-140">Create a web application using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e126c-140">Create a web application using Azure PowerShell.</span></span> <span data-ttu-id="e126c-141">For more examples of how to use Azure PowerShell with App Service, see [App Service PowerShell samples](../app-service/app-service-powershell-samples.md):</span><span class="sxs-lookup"><span data-stu-id="e126c-141">For more examples of how to use Azure PowerShell with App Service, see [App Service PowerShell samples](../app-service/app-service-powershell-samples.md):</span></span>

    ```azurepowershell-interactive
    # Create a resource group.
    New-AzureRmResourceGroup -Name myResourceGroup -Location $location
    
    # Create an App Service plan in Free tier.
    New-AzureRmAppServicePlan -Name $webappname -Location $location -ResourceGroupName myResourceGroup -Tier Free
    
    # Create a web app.
    New-AzureRmWebApp -Name $webappname -Location $location -AppServicePlan $webappname -ResourceGroupName myResourceGroup
    ```

3. <span data-ttu-id="e126c-142">Run the `identity assign` command to create the identity for this application:</span><span class="sxs-lookup"><span data-stu-id="e126c-142">Run the `identity assign` command to create the identity for this application:</span></span>

    ```azurepowershell-interactive
    Set-AzureRmWebApp -AssignIdentity $true -Name $webappname -ResourceGroupName myResourceGroup 
    ```

### <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="e126c-143">Using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="e126c-143">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="e126c-144">An Azure Resource Manager template can be used to automate deployment of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e126c-144">An Azure Resource Manager template can be used to automate deployment of your Azure resources.</span></span> <span data-ttu-id="e126c-145">To learn more about deploying to App Service and Functions, see [Automating resource deployment in App Service](../app-service/app-service-deploy-complex-application-predictably.md) and [Automating resource deployment in Azure Functions](../azure-functions/functions-infrastructure-as-code.md).</span><span class="sxs-lookup"><span data-stu-id="e126c-145">To learn more about deploying to App Service and Functions, see [Automating resource deployment in App Service](../app-service/app-service-deploy-complex-application-predictably.md) and [Automating resource deployment in Azure Functions](../azure-functions/functions-infrastructure-as-code.md).</span></span>

<span data-ttu-id="e126c-146">Any resource of type `Microsoft.Web/sites` can be created with an identity by including the following property in the resource definition:</span><span class="sxs-lookup"><span data-stu-id="e126c-146">Any resource of type `Microsoft.Web/sites` can be created with an identity by including the following property in the resource definition:</span></span>
```json
"identity": {
    "type": "SystemAssigned"
}    
```

<span data-ttu-id="e126c-147">This tells Azure to create and manage the identity for your application.</span><span class="sxs-lookup"><span data-stu-id="e126c-147">This tells Azure to create and manage the identity for your application.</span></span>

<span data-ttu-id="e126c-148">For example, a web app might look like the following:</span><span class="sxs-lookup"><span data-stu-id="e126c-148">For example, a web app might look like the following:</span></span>
```json
{
    "apiVersion": "2016-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('appName')]",
    "location": "[resourceGroup().location]",
    "identity": {
        "type": "SystemAssigned"
    },
    "properties": {
        "name": "[variables('appName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "hostingEnvironment": "",
        "clientAffinityEnabled": false,
        "alwaysOn": true
    },
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
    ]
}
```

<span data-ttu-id="e126c-149">When the site is created, it has the following additional properties:</span><span class="sxs-lookup"><span data-stu-id="e126c-149">When the site is created, it has the following additional properties:</span></span>
```json
"identity": {
    "tenantId": "<TENANTID>",
    "principalId": "<PRINCIPALID>"
}
```

<span data-ttu-id="e126c-150">Where `<TENANTID>` and `<PRINCIPALID>` are replaced with GUIDs.</span><span class="sxs-lookup"><span data-stu-id="e126c-150">Where `<TENANTID>` and `<PRINCIPALID>` are replaced with GUIDs.</span></span> <span data-ttu-id="e126c-151">The tenantId property identifies what AAD tenant the identity belongs to.</span><span class="sxs-lookup"><span data-stu-id="e126c-151">The tenantId property identifies what AAD tenant the identity belongs to.</span></span> <span data-ttu-id="e126c-152">The principalId is a unique identifier for the application's new identity.</span><span class="sxs-lookup"><span data-stu-id="e126c-152">The principalId is a unique identifier for the application's new identity.</span></span> <span data-ttu-id="e126c-153">Within AAD, the service principal has the same name that you gave to your App Service or Azure Functions instance.</span><span class="sxs-lookup"><span data-stu-id="e126c-153">Within AAD, the service principal has the same name that you gave to your App Service or Azure Functions instance.</span></span>

## <a name="obtaining-tokens-for-azure-resources"></a><span data-ttu-id="e126c-154">Obtaining tokens for Azure resources</span><span class="sxs-lookup"><span data-stu-id="e126c-154">Obtaining tokens for Azure resources</span></span>

<span data-ttu-id="e126c-155">An app can use its identity to get tokens to other resources protected by AAD, such as Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e126c-155">An app can use its identity to get tokens to other resources protected by AAD, such as Azure Key Vault.</span></span> <span data-ttu-id="e126c-156">These tokens represent the application accessing the resource, and not any specific user of the application.</span><span class="sxs-lookup"><span data-stu-id="e126c-156">These tokens represent the application accessing the resource, and not any specific user of the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e126c-157">You may need to configure the target resource to allow access from your application.</span><span class="sxs-lookup"><span data-stu-id="e126c-157">You may need to configure the target resource to allow access from your application.</span></span> <span data-ttu-id="e126c-158">For example, if you request a token to Key Vault, you need to make sure you have added an access policy that includes your application's identity.</span><span class="sxs-lookup"><span data-stu-id="e126c-158">For example, if you request a token to Key Vault, you need to make sure you have added an access policy that includes your application's identity.</span></span> <span data-ttu-id="e126c-159">Otherwise, your calls to Key Vault will be rejected, even if they include the token.</span><span class="sxs-lookup"><span data-stu-id="e126c-159">Otherwise, your calls to Key Vault will be rejected, even if they include the token.</span></span> <span data-ttu-id="e126c-160">To learn more about which resources support Managed Service Identity tokens, see [Azure services that support Azure AD authentication](../active-directory/managed-identities-azure-resources/services-support-msi.md#azure-services-that-support-azure-ad-authentication).</span><span class="sxs-lookup"><span data-stu-id="e126c-160">To learn more about which resources support Managed Service Identity tokens, see [Azure services that support Azure AD authentication](../active-directory/managed-identities-azure-resources/services-support-msi.md#azure-services-that-support-azure-ad-authentication).</span></span>

<span data-ttu-id="e126c-161">There is a simple REST protocol for obtaining a token in App Service and Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e126c-161">There is a simple REST protocol for obtaining a token in App Service and Azure Functions.</span></span> <span data-ttu-id="e126c-162">For .NET applications, the Microsoft.Azure.Services.AppAuthentication library provides an abstraction over this protocol and supports a local development experience.</span><span class="sxs-lookup"><span data-stu-id="e126c-162">For .NET applications, the Microsoft.Azure.Services.AppAuthentication library provides an abstraction over this protocol and supports a local development experience.</span></span>

### <a name="asal"></a><span data-ttu-id="e126c-163">Using the Microsoft.Azure.Services.AppAuthentication library for .NET</span><span class="sxs-lookup"><span data-stu-id="e126c-163">Using the Microsoft.Azure.Services.AppAuthentication library for .NET</span></span>

<span data-ttu-id="e126c-164">For .NET applications and functions, the simplest way to work with a managed service identity is through the Microsoft.Azure.Services.AppAuthentication package.</span><span class="sxs-lookup"><span data-stu-id="e126c-164">For .NET applications and functions, the simplest way to work with a managed service identity is through the Microsoft.Azure.Services.AppAuthentication package.</span></span> <span data-ttu-id="e126c-165">This library will also allow you to test your code locally on your development machine, using your user account from Visual Studio, the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest), or Active Directory Integrated Authentication.</span><span class="sxs-lookup"><span data-stu-id="e126c-165">This library will also allow you to test your code locally on your development machine, using your user account from Visual Studio, the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest), or Active Directory Integrated Authentication.</span></span> <span data-ttu-id="e126c-166">For more on local development options with this library, see the [Microsoft.Azure.Services.AppAuthentication reference].</span><span class="sxs-lookup"><span data-stu-id="e126c-166">For more on local development options with this library, see the [Microsoft.Azure.Services.AppAuthentication reference].</span></span> <span data-ttu-id="e126c-167">This section shows you how to get started with the library in your code.</span><span class="sxs-lookup"><span data-stu-id="e126c-167">This section shows you how to get started with the library in your code.</span></span>

1. <span data-ttu-id="e126c-168">Add references to the [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) and [Microsoft.Azure.KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet packages to your application.</span><span class="sxs-lookup"><span data-stu-id="e126c-168">Add references to the [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) and [Microsoft.Azure.KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet packages to your application.</span></span>

2.  <span data-ttu-id="e126c-169">Add the following code to your application:</span><span class="sxs-lookup"><span data-stu-id="e126c-169">Add the following code to your application:</span></span>

```csharp
using Microsoft.Azure.Services.AppAuthentication;
using Microsoft.Azure.KeyVault;
// ...
var azureServiceTokenProvider = new AzureServiceTokenProvider();
string accessToken = await azureServiceTokenProvider.GetAccessTokenAsync("https://management.azure.com/");
// OR
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(azureServiceTokenProvider.KeyVaultTokenCallback));
```

<span data-ttu-id="e126c-170">To learn more about Microsoft.Azure.Services.AppAuthentication and the operations it exposes, see the [Microsoft.Azure.Services.AppAuthentication reference] and the [App Service and KeyVault with MSI .NET sample](https://github.com/Azure-Samples/app-service-msi-keyvault-dotnet).</span><span class="sxs-lookup"><span data-stu-id="e126c-170">To learn more about Microsoft.Azure.Services.AppAuthentication and the operations it exposes, see the [Microsoft.Azure.Services.AppAuthentication reference] and the [App Service and KeyVault with MSI .NET sample](https://github.com/Azure-Samples/app-service-msi-keyvault-dotnet).</span></span>

### <a name="using-the-rest-protocol"></a><span data-ttu-id="e126c-171">Using the REST protocol</span><span class="sxs-lookup"><span data-stu-id="e126c-171">Using the REST protocol</span></span>

<span data-ttu-id="e126c-172">An app with a managed service identity has two environment variables defined:</span><span class="sxs-lookup"><span data-stu-id="e126c-172">An app with a managed service identity has two environment variables defined:</span></span>
- <span data-ttu-id="e126c-173">MSI_ENDPOINT</span><span class="sxs-lookup"><span data-stu-id="e126c-173">MSI_ENDPOINT</span></span>
- <span data-ttu-id="e126c-174">MSI_SECRET</span><span class="sxs-lookup"><span data-stu-id="e126c-174">MSI_SECRET</span></span>

<span data-ttu-id="e126c-175">The **MSI_ENDPOINT** is a local URL from which your app can request tokens.</span><span class="sxs-lookup"><span data-stu-id="e126c-175">The **MSI_ENDPOINT** is a local URL from which your app can request tokens.</span></span> <span data-ttu-id="e126c-176">To get a token for a resource, make an HTTP GET request to this endpoint, including the following parameters:</span><span class="sxs-lookup"><span data-stu-id="e126c-176">To get a token for a resource, make an HTTP GET request to this endpoint, including the following parameters:</span></span>

> [!div class="mx-tdBreakAll"]
> |<span data-ttu-id="e126c-177">Parameter name</span><span class="sxs-lookup"><span data-stu-id="e126c-177">Parameter name</span></span>|<span data-ttu-id="e126c-178">In</span><span class="sxs-lookup"><span data-stu-id="e126c-178">In</span></span>|<span data-ttu-id="e126c-179">Description</span><span class="sxs-lookup"><span data-stu-id="e126c-179">Description</span></span>|
> |-----|-----|-----|
> |<span data-ttu-id="e126c-180">resource</span><span class="sxs-lookup"><span data-stu-id="e126c-180">resource</span></span>|<span data-ttu-id="e126c-181">Query</span><span class="sxs-lookup"><span data-stu-id="e126c-181">Query</span></span>|<span data-ttu-id="e126c-182">The AAD resource URI of the resource for which a token should be obtained.</span><span class="sxs-lookup"><span data-stu-id="e126c-182">The AAD resource URI of the resource for which a token should be obtained.</span></span>|
> |<span data-ttu-id="e126c-183">api-version</span><span class="sxs-lookup"><span data-stu-id="e126c-183">api-version</span></span>|<span data-ttu-id="e126c-184">Query</span><span class="sxs-lookup"><span data-stu-id="e126c-184">Query</span></span>|<span data-ttu-id="e126c-185">The version of the token API to be used.</span><span class="sxs-lookup"><span data-stu-id="e126c-185">The version of the token API to be used.</span></span> <span data-ttu-id="e126c-186">"2017-09-01" is currently the only version supported.</span><span class="sxs-lookup"><span data-stu-id="e126c-186">"2017-09-01" is currently the only version supported.</span></span>|
> |<span data-ttu-id="e126c-187">secret</span><span class="sxs-lookup"><span data-stu-id="e126c-187">secret</span></span>|<span data-ttu-id="e126c-188">Header</span><span class="sxs-lookup"><span data-stu-id="e126c-188">Header</span></span>|<span data-ttu-id="e126c-189">The value of the MSI_SECRET environment variable.</span><span class="sxs-lookup"><span data-stu-id="e126c-189">The value of the MSI_SECRET environment variable.</span></span>|


<span data-ttu-id="e126c-190">A successful 200 OK response includes a JSON body with the following properties:</span><span class="sxs-lookup"><span data-stu-id="e126c-190">A successful 200 OK response includes a JSON body with the following properties:</span></span>

> [!div class="mx-tdBreakAll"]
> |<span data-ttu-id="e126c-191">Property name</span><span class="sxs-lookup"><span data-stu-id="e126c-191">Property name</span></span>|<span data-ttu-id="e126c-192">Description</span><span class="sxs-lookup"><span data-stu-id="e126c-192">Description</span></span>|
> |-------------|----------|
> |<span data-ttu-id="e126c-193">access_token</span><span class="sxs-lookup"><span data-stu-id="e126c-193">access_token</span></span>|<span data-ttu-id="e126c-194">The requested access token.</span><span class="sxs-lookup"><span data-stu-id="e126c-194">The requested access token.</span></span> <span data-ttu-id="e126c-195">The calling web service can use this token to authenticate to the receiving web service.</span><span class="sxs-lookup"><span data-stu-id="e126c-195">The calling web service can use this token to authenticate to the receiving web service.</span></span>|
> |<span data-ttu-id="e126c-196">expires_on</span><span class="sxs-lookup"><span data-stu-id="e126c-196">expires_on</span></span>|<span data-ttu-id="e126c-197">The time when the access token expires.</span><span class="sxs-lookup"><span data-stu-id="e126c-197">The time when the access token expires.</span></span> <span data-ttu-id="e126c-198">The date is represented as the number of seconds from 1970-01-01T0:0:0Z UTC until the expiration time.</span><span class="sxs-lookup"><span data-stu-id="e126c-198">The date is represented as the number of seconds from 1970-01-01T0:0:0Z UTC until the expiration time.</span></span> <span data-ttu-id="e126c-199">This value is used to determine the lifetime of cached tokens.</span><span class="sxs-lookup"><span data-stu-id="e126c-199">This value is used to determine the lifetime of cached tokens.</span></span>|
> |<span data-ttu-id="e126c-200">resource</span><span class="sxs-lookup"><span data-stu-id="e126c-200">resource</span></span>|<span data-ttu-id="e126c-201">The App ID URI of the receiving web service.</span><span class="sxs-lookup"><span data-stu-id="e126c-201">The App ID URI of the receiving web service.</span></span>|
> |<span data-ttu-id="e126c-202">token_type</span><span class="sxs-lookup"><span data-stu-id="e126c-202">token_type</span></span>|<span data-ttu-id="e126c-203">Indicates the token type value.</span><span class="sxs-lookup"><span data-stu-id="e126c-203">Indicates the token type value.</span></span> <span data-ttu-id="e126c-204">The only type that Azure AD supports is Bearer.</span><span class="sxs-lookup"><span data-stu-id="e126c-204">The only type that Azure AD supports is Bearer.</span></span> <span data-ttu-id="e126c-205">For more information about bearer tokens, see [The OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt).</span><span class="sxs-lookup"><span data-stu-id="e126c-205">For more information about bearer tokens, see [The OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt).</span></span>|


<span data-ttu-id="e126c-206">This response is the same as the [response for the AAD service-to-service access token request](../active-directory/develop/v1-oauth2-client-creds-grant-flow.md#service-to-service-access-token-response).</span><span class="sxs-lookup"><span data-stu-id="e126c-206">This response is the same as the [response for the AAD service-to-service access token request](../active-directory/develop/v1-oauth2-client-creds-grant-flow.md#service-to-service-access-token-response).</span></span>

> [!NOTE] 
> <span data-ttu-id="e126c-207">Environment variables are set up when the process first starts, so after enabling Managed Service Identity for your application you may need to restart your application, or redeploy its code, before `MSI_ENDPOINT` and `MSI_SECRET` are available to your code.</span><span class="sxs-lookup"><span data-stu-id="e126c-207">Environment variables are set up when the process first starts, so after enabling Managed Service Identity for your application you may need to restart your application, or redeploy its code, before `MSI_ENDPOINT` and `MSI_SECRET` are available to your code.</span></span>

### <a name="rest-protocol-examples"></a><span data-ttu-id="e126c-208">REST protocol examples</span><span class="sxs-lookup"><span data-stu-id="e126c-208">REST protocol examples</span></span>
<span data-ttu-id="e126c-209">An example request might look like the following:</span><span class="sxs-lookup"><span data-stu-id="e126c-209">An example request might look like the following:</span></span>
```
GET /MSI/token?resource=https://vault.azure.net&api-version=2017-09-01 HTTP/1.1
Host: localhost:4141
Secret: 853b9a84-5bfa-4b22-a3f3-0b9a43d9ad8a
```
<span data-ttu-id="e126c-210">And a sample response might look like the following:</span><span class="sxs-lookup"><span data-stu-id="e126c-210">And a sample response might look like the following:</span></span>
```
HTTP/1.1 200 OK
Content-Type: application/json
 
{
    "access_token": "eyJ0eXAi…",
    "expires_on": "09/14/2017 00:00:00 PM +00:00",
    "resource": "https://vault.azure.net",
    "token_type": "Bearer"
}
```

### <a name="code-examples"></a><span data-ttu-id="e126c-211">Code examples</span><span class="sxs-lookup"><span data-stu-id="e126c-211">Code examples</span></span>
<a name="token-csharp"></a><span data-ttu-id="e126c-212">To make this request in C#:</span><span class="sxs-lookup"><span data-stu-id="e126c-212">To make this request in C#:</span></span>
```csharp
public static async Task<HttpResponseMessage> GetToken(string resource, string apiversion)  {
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Add("Secret", Environment.GetEnvironmentVariable("MSI_SECRET"));
    return await client.GetAsync(String.Format("{0}/?resource={1}&api-version={2}", Environment.GetEnvironmentVariable("MSI_ENDPOINT"), resource, apiversion));
}
```
> [!TIP]
> <span data-ttu-id="e126c-213">For .NET languages, you can also use [Microsoft.Azure.Services.AppAuthentication](#asal) instead of crafting this request yourself.</span><span class="sxs-lookup"><span data-stu-id="e126c-213">For .NET languages, you can also use [Microsoft.Azure.Services.AppAuthentication](#asal) instead of crafting this request yourself.</span></span>

<a name="token-js"></a><span data-ttu-id="e126c-214">In Node.JS:</span><span class="sxs-lookup"><span data-stu-id="e126c-214">In Node.JS:</span></span>
```javascript
const rp = require('request-promise');
const getToken = function(resource, apiver, cb) {
    var options = {
        uri: `${process.env["MSI_ENDPOINT"]}/?resource=${resource}&api-version=${apiver}`,
        headers: {
            'Secret': process.env["MSI_SECRET"]
        }
    };
    rp(options)
        .then(cb);
}
```

<a name="token-powershell"></a><span data-ttu-id="e126c-215">In PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e126c-215">In PowerShell:</span></span>
```powershell
$apiVersion = "2017-09-01"
$resourceURI = "https://<AAD-resource-URI-for-resource-to-obtain-token>"
$tokenAuthURI = $env:MSI_ENDPOINT + "?resource=$resourceURI&api-version=$apiVersion"
$tokenResponse = Invoke-RestMethod -Method Get -Headers @{"Secret"="$env:MSI_SECRET"} -Uri $tokenAuthURI
$accessToken = $tokenResponse.access_token
```

## <a name="remove"></a><span data-ttu-id="e126c-216">Removing an identity</span><span class="sxs-lookup"><span data-stu-id="e126c-216">Removing an identity</span></span>

<span data-ttu-id="e126c-217">An identity can be removed by disabling the feature using the portal, PowerShell, or CLI in the same way that it was created.</span><span class="sxs-lookup"><span data-stu-id="e126c-217">An identity can be removed by disabling the feature using the portal, PowerShell, or CLI in the same way that it was created.</span></span> <span data-ttu-id="e126c-218">In the REST/ARM template protocol, this is done by setting the type to "None":</span><span class="sxs-lookup"><span data-stu-id="e126c-218">In the REST/ARM template protocol, this is done by setting the type to "None":</span></span>

```json
"identity": {
    "type": "None"
}    
```

<span data-ttu-id="e126c-219">Removing the identity in this way will also delete the principal from AAD.</span><span class="sxs-lookup"><span data-stu-id="e126c-219">Removing the identity in this way will also delete the principal from AAD.</span></span> <span data-ttu-id="e126c-220">System-assigned Identities are automatically removed from AAD when the app resource is deleted.</span><span class="sxs-lookup"><span data-stu-id="e126c-220">System-assigned Identities are automatically removed from AAD when the app resource is deleted.</span></span>

> [!NOTE] 
> <span data-ttu-id="e126c-221">There is also an application setting that can be set, WEBSITE_DISABLE_MSI, which just disables the local token service.</span><span class="sxs-lookup"><span data-stu-id="e126c-221">There is also an application setting that can be set, WEBSITE_DISABLE_MSI, which just disables the local token service.</span></span> <span data-ttu-id="e126c-222">However, it leaves the identity in place, and tooling will still show MSI as "on" or "enabled."</span><span class="sxs-lookup"><span data-stu-id="e126c-222">However, it leaves the identity in place, and tooling will still show MSI as "on" or "enabled."</span></span> <span data-ttu-id="e126c-223">As a result, use of this setting is not recommmended.</span><span class="sxs-lookup"><span data-stu-id="e126c-223">As a result, use of this setting is not recommmended.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e126c-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="e126c-224">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e126c-225">Access SQL Database securely using managed service identity</span><span class="sxs-lookup"><span data-stu-id="e126c-225">Access SQL Database securely using managed service identity</span></span>](app-service-web-tutorial-connect-msi.md)

[Microsoft.Azure.Services.AppAuthentication reference]: https://go.microsoft.com/fwlink/p/?linkid=862452
