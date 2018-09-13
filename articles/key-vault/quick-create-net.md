---
title: 'Quickstart: Set and retrieve a secret from Azure Key Vault by using a node web app | Microsoft Docs'
description: 'Quickstart: Set and retrieve a secret from Azure Key Vault by using a node web app'
services: key-vault
author: prashanthyv
manager: sumedhb
ms.service: key-vault
ms.topic: quickstart
ms.date: 09/05/2018
ms.author: barclayn
ms.custom: mvc
ms.openlocfilehash: e0d11f25c7c22100ae43f1fa5807093bf6701027
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966380"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault-by-using-a-net-web-app"></a><span data-ttu-id="db967-103">Quickstart: Set and retrieve a secret from Azure Key Vault by using a .NET web app</span><span class="sxs-lookup"><span data-stu-id="db967-103">Quickstart: Set and retrieve a secret from Azure Key Vault by using a .NET web app</span></span>

<span data-ttu-id="db967-104">In this quickstart, you follow the necessary steps for getting an Azure web application to read information from Azure Key Vault by using managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="db967-104">In this quickstart, you follow the necessary steps for getting an Azure web application to read information from Azure Key Vault by using managed identities for Azure resources.</span></span> <span data-ttu-id="db967-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="db967-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db967-106">Create a key vault.</span><span class="sxs-lookup"><span data-stu-id="db967-106">Create a key vault.</span></span>
> * <span data-ttu-id="db967-107">Store a secret in the key vault.</span><span class="sxs-lookup"><span data-stu-id="db967-107">Store a secret in the key vault.</span></span>
> * <span data-ttu-id="db967-108">Retrieve a secret from the key vault.</span><span class="sxs-lookup"><span data-stu-id="db967-108">Retrieve a secret from the key vault.</span></span>
> * <span data-ttu-id="db967-109">Create an Azure web application.</span><span class="sxs-lookup"><span data-stu-id="db967-109">Create an Azure web application.</span></span>
> * <span data-ttu-id="db967-110">Enable a [managed identity](../active-directory/managed-identities-azure-resources/overview.md) for the web app.</span><span class="sxs-lookup"><span data-stu-id="db967-110">Enable a [managed identity](../active-directory/managed-identities-azure-resources/overview.md) for the web app.</span></span>
> * <span data-ttu-id="db967-111">Grant the required permissions for the web application to read data from the key vault.</span><span class="sxs-lookup"><span data-stu-id="db967-111">Grant the required permissions for the web application to read data from the key vault.</span></span>

<span data-ttu-id="db967-112">Before we go any further, please read the [basic concepts](key-vault-whatis.md#basic-concepts).</span><span class="sxs-lookup"><span data-stu-id="db967-112">Before we go any further, please read the [basic concepts](key-vault-whatis.md#basic-concepts).</span></span>

>[!NOTE]
><span data-ttu-id="db967-113">Key Vault is a central repository to store secrets programmatically.</span><span class="sxs-lookup"><span data-stu-id="db967-113">Key Vault is a central repository to store secrets programmatically.</span></span> <span data-ttu-id="db967-114">But to do so, applications and users need to first authenticate to Key Vault--that is, present a secret.</span><span class="sxs-lookup"><span data-stu-id="db967-114">But to do so, applications and users need to first authenticate to Key Vault--that is, present a secret.</span></span> <span data-ttu-id="db967-115">To follow security best practices, this first secret needs to be rotated periodically.</span><span class="sxs-lookup"><span data-stu-id="db967-115">To follow security best practices, this first secret needs to be rotated periodically.</span></span> 
>
><span data-ttu-id="db967-116">With [managed identities for Azure resources](../active-directory/managed-identities-azure-resources/overview.md), applications that run in Azure are given an identity that Azure manages automatically.</span><span class="sxs-lookup"><span data-stu-id="db967-116">With [managed identities for Azure resources](../active-directory/managed-identities-azure-resources/overview.md), applications that run in Azure are given an identity that Azure manages automatically.</span></span> <span data-ttu-id="db967-117">This helps solve the *secret introduction problem* so that users and applications can follow best practices and not have to worry about rotating the first secret.</span><span class="sxs-lookup"><span data-stu-id="db967-117">This helps solve the *secret introduction problem* so that users and applications can follow best practices and not have to worry about rotating the first secret.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db967-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db967-118">Prerequisites</span></span>

* <span data-ttu-id="db967-119">On Windows:</span><span class="sxs-lookup"><span data-stu-id="db967-119">On Windows:</span></span>
  * <span data-ttu-id="db967-120">[Visual Studio 2017 version 15.7.3 or later](https://www.microsoft.com/net/download/windows) with the following workloads:</span><span class="sxs-lookup"><span data-stu-id="db967-120">[Visual Studio 2017 version 15.7.3 or later](https://www.microsoft.com/net/download/windows) with the following workloads:</span></span>
    * <span data-ttu-id="db967-121">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="db967-121">ASP.NET and web development</span></span>
    * <span data-ttu-id="db967-122">.NET Core cross-platform development</span><span class="sxs-lookup"><span data-stu-id="db967-122">.NET Core cross-platform development</span></span>
  * [<span data-ttu-id="db967-123">.NET Core 2.1 SDK or later</span><span class="sxs-lookup"><span data-stu-id="db967-123">.NET Core 2.1 SDK or later</span></span>](https://www.microsoft.com/net/download/windows)

* <span data-ttu-id="db967-124">On Mac:</span><span class="sxs-lookup"><span data-stu-id="db967-124">On Mac:</span></span>
  * <span data-ttu-id="db967-125">See [What’s New in Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/).</span><span class="sxs-lookup"><span data-stu-id="db967-125">See [What’s New in Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/).</span></span>

* <span data-ttu-id="db967-126">All platforms:</span><span class="sxs-lookup"><span data-stu-id="db967-126">All platforms:</span></span>
  * <span data-ttu-id="db967-127">Git ([download](https://git-scm.com/downloads)).</span><span class="sxs-lookup"><span data-stu-id="db967-127">Git ([download](https://git-scm.com/downloads)).</span></span>
  * <span data-ttu-id="db967-128">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="db967-128">An Azure subscription.</span></span> <span data-ttu-id="db967-129">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="db967-129">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
  * <span data-ttu-id="db967-130">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="db967-130">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) version 2.0.4 or later.</span></span> <span data-ttu-id="db967-131">This is available for Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="db967-131">This is available for Windows, Mac, and Linux.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="db967-132">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="db967-132">Log in to Azure</span></span>

<span data-ttu-id="db967-133">To log in to Azure by using the Azure CLI, enter:</span><span class="sxs-lookup"><span data-stu-id="db967-133">To log in to Azure by using the Azure CLI, enter:</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="db967-134">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="db967-134">Create a resource group</span></span>

<span data-ttu-id="db967-135">Create a resource group by using the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="db967-135">Create a resource group by using the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="db967-136">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="db967-136">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="db967-137">Select a resource group name and fill in the placeholder.</span><span class="sxs-lookup"><span data-stu-id="db967-137">Select a resource group name and fill in the placeholder.</span></span>
<span data-ttu-id="db967-138">The following example creates a resource group in the East US location:</span><span class="sxs-lookup"><span data-stu-id="db967-138">The following example creates a resource group in the East US location:</span></span>

```azurecli
# To list locations: az account list-locations --output table
az group create --name "<YourResourceGroupName>" --location "East US"
```

<span data-ttu-id="db967-139">The resource group that you just created is used throughout this article.</span><span class="sxs-lookup"><span data-stu-id="db967-139">The resource group that you just created is used throughout this article.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="db967-140">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="db967-140">Create a key vault</span></span>

<span data-ttu-id="db967-141">Next you create a key vault in the resource group that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="db967-141">Next you create a key vault in the resource group that you created in the previous step.</span></span> <span data-ttu-id="db967-142">Provide the following information:</span><span class="sxs-lookup"><span data-stu-id="db967-142">Provide the following information:</span></span>

* <span data-ttu-id="db967-143">Key vault name: The name must be a string of 3-24 characters and must contain only (0-9, a-z, A-Z, and -).</span><span class="sxs-lookup"><span data-stu-id="db967-143">Key vault name: The name must be a string of 3-24 characters and must contain only (0-9, a-z, A-Z, and -).</span></span>
* <span data-ttu-id="db967-144">Resource group name.</span><span class="sxs-lookup"><span data-stu-id="db967-144">Resource group name.</span></span>
* <span data-ttu-id="db967-145">Location: **East US**.</span><span class="sxs-lookup"><span data-stu-id="db967-145">Location: **East US**.</span></span>

```azurecli
az keyvault create --name "<YourKeyVaultName>" --resource-group "<YourResourceGroupName>" --location "East US"
```

<span data-ttu-id="db967-146">At this point, your Azure account is the only one that's authorized to perform any operations on this new vault.</span><span class="sxs-lookup"><span data-stu-id="db967-146">At this point, your Azure account is the only one that's authorized to perform any operations on this new vault.</span></span>

## <a name="add-a-secret-to-the-key-vault"></a><span data-ttu-id="db967-147">Add a secret to the key vault</span><span class="sxs-lookup"><span data-stu-id="db967-147">Add a secret to the key vault</span></span>

<span data-ttu-id="db967-148">We're adding a secret to help illustrate how this works.</span><span class="sxs-lookup"><span data-stu-id="db967-148">We're adding a secret to help illustrate how this works.</span></span> <span data-ttu-id="db967-149">You might be storing a SQL connection string or any other information that you need to keep securely but make available to your application.</span><span class="sxs-lookup"><span data-stu-id="db967-149">You might be storing a SQL connection string or any other information that you need to keep securely but make available to your application.</span></span>

<span data-ttu-id="db967-150">Type the following commands to create a secret in the key vault called **AppSecret**.</span><span class="sxs-lookup"><span data-stu-id="db967-150">Type the following commands to create a secret in the key vault called **AppSecret**.</span></span> <span data-ttu-id="db967-151">This secret will store the value **MySecret**.</span><span class="sxs-lookup"><span data-stu-id="db967-151">This secret will store the value **MySecret**.</span></span>

```azurecli
az keyvault secret set --vault-name "<YourKeyVaultName>" --name "AppSecret" --value "MySecret"
```

<span data-ttu-id="db967-152">To view the value contained in the secret as plain text:</span><span class="sxs-lookup"><span data-stu-id="db967-152">To view the value contained in the secret as plain text:</span></span>

```azurecli
az keyvault secret show --name "AppSecret" --vault-name "<YourKeyVaultName>"
```

<span data-ttu-id="db967-153">This command shows the secret information, including the URI.</span><span class="sxs-lookup"><span data-stu-id="db967-153">This command shows the secret information, including the URI.</span></span> <span data-ttu-id="db967-154">After you complete these steps, you should have a URI to a secret in a key vault.</span><span class="sxs-lookup"><span data-stu-id="db967-154">After you complete these steps, you should have a URI to a secret in a key vault.</span></span> <span data-ttu-id="db967-155">Make note of this information.</span><span class="sxs-lookup"><span data-stu-id="db967-155">Make note of this information.</span></span> <span data-ttu-id="db967-156">You'll need it in a later step.</span><span class="sxs-lookup"><span data-stu-id="db967-156">You'll need it in a later step.</span></span>

## <a name="clone-the-repo"></a><span data-ttu-id="db967-157">Clone the repo</span><span class="sxs-lookup"><span data-stu-id="db967-157">Clone the repo</span></span>

<span data-ttu-id="db967-158">Clone the repo to make a local copy where you can edit the source.</span><span class="sxs-lookup"><span data-stu-id="db967-158">Clone the repo to make a local copy where you can edit the source.</span></span> <span data-ttu-id="db967-159">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="db967-159">Run the following command:</span></span>

```
git clone https://github.com/Azure-Samples/key-vault-dotnet-core-quickstart.git
```

## <a name="open-and-edit-the-solution"></a><span data-ttu-id="db967-160">Open and edit the solution</span><span class="sxs-lookup"><span data-stu-id="db967-160">Open and edit the solution</span></span>

<span data-ttu-id="db967-161">Edit the program.cs file to run the sample with your specific key vault name:</span><span class="sxs-lookup"><span data-stu-id="db967-161">Edit the program.cs file to run the sample with your specific key vault name:</span></span>

1. <span data-ttu-id="db967-162">Browse to the folder key-vault-dotnet-core-quickstart.</span><span class="sxs-lookup"><span data-stu-id="db967-162">Browse to the folder key-vault-dotnet-core-quickstart.</span></span>
2. <span data-ttu-id="db967-163">Open the key-vault-dotnet-core-quickstart.sln file in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="db967-163">Open the key-vault-dotnet-core-quickstart.sln file in Visual Studio 2017.</span></span>
3. <span data-ttu-id="db967-164">Open the Program.cs file and update the placeholder *YourKeyVaultName* with the name of your key vault that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="db967-164">Open the Program.cs file and update the placeholder *YourKeyVaultName* with the name of your key vault that you created earlier.</span></span>

<span data-ttu-id="db967-165">This solution uses [AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) and [KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet libraries.</span><span class="sxs-lookup"><span data-stu-id="db967-165">This solution uses [AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) and [KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet libraries.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="db967-166">Run the app</span><span class="sxs-lookup"><span data-stu-id="db967-166">Run the app</span></span>

<span data-ttu-id="db967-167">From the main menu of Visual Studio 2017, select **Debug** > **Start** without debugging.</span><span class="sxs-lookup"><span data-stu-id="db967-167">From the main menu of Visual Studio 2017, select **Debug** > **Start** without debugging.</span></span> <span data-ttu-id="db967-168">When the browser appears, go to the **About** page.</span><span class="sxs-lookup"><span data-stu-id="db967-168">When the browser appears, go to the **About** page.</span></span> <span data-ttu-id="db967-169">The value for **AppSecret** is displayed.</span><span class="sxs-lookup"><span data-stu-id="db967-169">The value for **AppSecret** is displayed.</span></span>

## <a name="publish-the-web-application-to-azure"></a><span data-ttu-id="db967-170">Publish the web application to Azure</span><span class="sxs-lookup"><span data-stu-id="db967-170">Publish the web application to Azure</span></span>

<span data-ttu-id="db967-171">Publish this app to Azure to see it live as a web app, and to see that you can fetch the secret value:</span><span class="sxs-lookup"><span data-stu-id="db967-171">Publish this app to Azure to see it live as a web app, and to see that you can fetch the secret value:</span></span>

1. <span data-ttu-id="db967-172">In Visual Studio, select the **key-vault-dotnet-core-quickstart** project.</span><span class="sxs-lookup"><span data-stu-id="db967-172">In Visual Studio, select the **key-vault-dotnet-core-quickstart** project.</span></span>
2. <span data-ttu-id="db967-173">Select **Publish** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="db967-173">Select **Publish** > **Start**.</span></span>
3. <span data-ttu-id="db967-174">Create a new **App Service**, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="db967-174">Create a new **App Service**, and then select **Publish**.</span></span>
4. <span data-ttu-id="db967-175">Change the app name to **keyvaultdotnetcorequickstart**.</span><span class="sxs-lookup"><span data-stu-id="db967-175">Change the app name to **keyvaultdotnetcorequickstart**.</span></span>
5. <span data-ttu-id="db967-176">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="db967-176">Select **Create**.</span></span>

>[!VIDEO https://sec.ch9.ms/ch9/e93d/a6ac417f-2e63-4125-a37a-8f34bf0fe93d/KeyVault_high.mp4]

## <a name="enable-a-managed-identity-for-the-web-app"></a><span data-ttu-id="db967-177">Enable a managed identity for the web app</span><span class="sxs-lookup"><span data-stu-id="db967-177">Enable a managed identity for the web app</span></span>

<span data-ttu-id="db967-178">Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Key Vault to retrieve them.</span><span class="sxs-lookup"><span data-stu-id="db967-178">Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Key Vault to retrieve them.</span></span> <span data-ttu-id="db967-179">[Managed identities for Azure resources overview](../active-directory/managed-identities-azure-resources/overview.md) makes solving this problem simpler, by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="db967-179">[Managed identities for Azure resources overview](../active-directory/managed-identities-azure-resources/overview.md) makes solving this problem simpler, by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="db967-180">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="db967-180">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span></span>

1. <span data-ttu-id="db967-181">Return to the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="db967-181">Return to the Azure CLI.</span></span>
2. <span data-ttu-id="db967-182">Run the assign-identity command to create the identity for this application:</span><span class="sxs-lookup"><span data-stu-id="db967-182">Run the assign-identity command to create the identity for this application:</span></span>

   ```azurecli
   az webapp identity assign --name "keyvaultdotnetcorequickstart" --resource-group "<YourResourceGroupName>"
   ```

>[!NOTE]
><span data-ttu-id="db967-183">The command in this procedure is the equivalent of going to the portal and switching the **Identity / System assigned** setting to **On** in the web application properties.</span><span class="sxs-lookup"><span data-stu-id="db967-183">The command in this procedure is the equivalent of going to the portal and switching the **Identity / System assigned** setting to **On** in the web application properties.</span></span>

## <a name="assign-permissions-to-your-application-to-read-secrets-from-key-vault"></a><span data-ttu-id="db967-184">Assign permissions to your application to read secrets from Key Vault</span><span class="sxs-lookup"><span data-stu-id="db967-184">Assign permissions to your application to read secrets from Key Vault</span></span>

<span data-ttu-id="db967-185">Make a note of the output when you publish the application to Azure.</span><span class="sxs-lookup"><span data-stu-id="db967-185">Make a note of the output when you publish the application to Azure.</span></span> <span data-ttu-id="db967-186">It should be of the format:</span><span class="sxs-lookup"><span data-stu-id="db967-186">It should be of the format:</span></span>
        
        {
          "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          "type": "SystemAssigned"
        }
        
<span data-ttu-id="db967-187">Then, run this command by using the name of your key vault and the value of **PrincipalId**:</span><span class="sxs-lookup"><span data-stu-id="db967-187">Then, run this command by using the name of your key vault and the value of **PrincipalId**:</span></span>

```azurecli

az keyvault set-policy --name '<YourKeyVaultName>' --object-id <PrincipalId> --secret-permissions get

```

<span data-ttu-id="db967-188">Now when you run the application, you should see your secret value retrieved.</span><span class="sxs-lookup"><span data-stu-id="db967-188">Now when you run the application, you should see your secret value retrieved.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db967-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="db967-189">Next steps</span></span>

* [<span data-ttu-id="db967-190">Azure Key Vault home page</span><span class="sxs-lookup"><span data-stu-id="db967-190">Azure Key Vault home page</span></span>](https://azure.microsoft.com/services/key-vault/)
* [<span data-ttu-id="db967-191">Azure Key Vault documentation</span><span class="sxs-lookup"><span data-stu-id="db967-191">Azure Key Vault documentation</span></span>](https://docs.microsoft.com/azure/key-vault/)
* [<span data-ttu-id="db967-192">Azure SDK For .NET</span><span class="sxs-lookup"><span data-stu-id="db967-192">Azure SDK For .NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
* [<span data-ttu-id="db967-193">Azure REST API reference</span><span class="sxs-lookup"><span data-stu-id="db967-193">Azure REST API reference</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
