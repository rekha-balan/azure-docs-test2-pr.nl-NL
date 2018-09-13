---
title: Quickstart- Set and retrieve a secret from Azure Key Vault using a Node Web App | Microsoft Docs
description: Quickstart- Set and retrieve a secret from Azure Key Vault using a Node Web App
services: key-vault
documentationcenter: ''
author: prashanthyv
manager: sumedhb
ms.service: key-vault
ms.workload: identity
ms.topic: quickstart
ms.date: 09/05/2018
ms.author: barclayn
ms.custom: mvc
ms.openlocfilehash: 3185e313f20a9398b12e24e4da293f95afb1a62f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867473"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault-using-a-node-web-app"></a><span data-ttu-id="5243d-103">Quickstart: Set and retrieve a secret from Azure Key Vault using a Node Web App</span><span class="sxs-lookup"><span data-stu-id="5243d-103">Quickstart: Set and retrieve a secret from Azure Key Vault using a Node Web App</span></span> 

<span data-ttu-id="5243d-104">This quickstart shows you how to store a secret in Key Vault and how to retrieve it using a Web app.</span><span class="sxs-lookup"><span data-stu-id="5243d-104">This quickstart shows you how to store a secret in Key Vault and how to retrieve it using a Web app.</span></span> <span data-ttu-id="5243d-105">To see the secret value you would have to run this on Azure.</span><span class="sxs-lookup"><span data-stu-id="5243d-105">To see the secret value you would have to run this on Azure.</span></span> <span data-ttu-id="5243d-106">The quickstart uses Node.js and managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="5243d-106">The quickstart uses Node.js and managed identities for Azure resources.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5243d-107">Create a Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5243d-107">Create a Key Vault.</span></span>
> * <span data-ttu-id="5243d-108">Store a secret in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5243d-108">Store a secret in Key Vault.</span></span>
> * <span data-ttu-id="5243d-109">Retrieve a secret from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5243d-109">Retrieve a secret from Key Vault.</span></span>
> * <span data-ttu-id="5243d-110">Create an Azure Web Application.</span><span class="sxs-lookup"><span data-stu-id="5243d-110">Create an Azure Web Application.</span></span>
> * <span data-ttu-id="5243d-111">Enable a [managed identity](https://docs.microsoft.com/azure/active-directory/managed-service-identity/overview) for the web app.</span><span class="sxs-lookup"><span data-stu-id="5243d-111">Enable a [managed identity](https://docs.microsoft.com/azure/active-directory/managed-service-identity/overview) for the web app.</span></span>
> * <span data-ttu-id="5243d-112">Grant the required permissions for the web application to read data from Key vault.</span><span class="sxs-lookup"><span data-stu-id="5243d-112">Grant the required permissions for the web application to read data from Key vault.</span></span>

<span data-ttu-id="5243d-113">Before you proceed make sure that you are familiar with the [basic concepts](key-vault-whatis.md#basic-concepts).</span><span class="sxs-lookup"><span data-stu-id="5243d-113">Before you proceed make sure that you are familiar with the [basic concepts](key-vault-whatis.md#basic-concepts).</span></span>

>[!NOTE]
<span data-ttu-id="5243d-114">To understand why the below tutorial is the best practice we need to understand a few concepts.</span><span class="sxs-lookup"><span data-stu-id="5243d-114">To understand why the below tutorial is the best practice we need to understand a few concepts.</span></span> <span data-ttu-id="5243d-115">Key Vault is a central repository to store secrets programmatically.</span><span class="sxs-lookup"><span data-stu-id="5243d-115">Key Vault is a central repository to store secrets programmatically.</span></span> <span data-ttu-id="5243d-116">But to do so applications / users need to first authenticate to Key Vault i.e. present a secret.</span><span class="sxs-lookup"><span data-stu-id="5243d-116">But to do so applications / users need to first authenticate to Key Vault i.e. present a secret.</span></span> <span data-ttu-id="5243d-117">To follow security best practices this first secret needs to be rotated periodically as well.</span><span class="sxs-lookup"><span data-stu-id="5243d-117">To follow security best practices this first secret needs to be rotated periodically as well.</span></span> <span data-ttu-id="5243d-118">But with [managed identites for Azure resources](../active-directory/managed-identities-azure-resources/overview.md) applications that run in Azure are given an identity which is automatically managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="5243d-118">But with [managed identites for Azure resources](../active-directory/managed-identities-azure-resources/overview.md) applications that run in Azure are given an identity which is automatically managed by Azure.</span></span> <span data-ttu-id="5243d-119">This helps solve the **Secret Introduction Problem** where users / applications can follow best practices and not have to worry about rotating the first secret</span><span class="sxs-lookup"><span data-stu-id="5243d-119">This helps solve the **Secret Introduction Problem** where users / applications can follow best practices and not have to worry about rotating the first secret</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5243d-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5243d-120">Prerequisites</span></span>

* [<span data-ttu-id="5243d-121">Node JS</span><span class="sxs-lookup"><span data-stu-id="5243d-121">Node JS</span></span>](https://nodejs.org/en/)
* [<span data-ttu-id="5243d-122">Git</span><span class="sxs-lookup"><span data-stu-id="5243d-122">Git</span></span>](https://www.git-scm.com/)
* <span data-ttu-id="5243d-123">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) 2.0.4 or later</span><span class="sxs-lookup"><span data-stu-id="5243d-123">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) 2.0.4 or later</span></span>
* <span data-ttu-id="5243d-124">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5243d-124">An Azure subscription.</span></span> <span data-ttu-id="5243d-125">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="5243d-125">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="login-to-azure"></a><span data-ttu-id="5243d-126">Login to Azure</span><span class="sxs-lookup"><span data-stu-id="5243d-126">Login to Azure</span></span>

<span data-ttu-id="5243d-127">To log in to Azure using the CLI, you can type:</span><span class="sxs-lookup"><span data-stu-id="5243d-127">To log in to Azure using the CLI, you can type:</span></span>

```azurecli
az login
```

## <a name="create-resource-group"></a><span data-ttu-id="5243d-128">Create resource group</span><span class="sxs-lookup"><span data-stu-id="5243d-128">Create resource group</span></span>

<span data-ttu-id="5243d-129">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="5243d-129">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="5243d-130">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="5243d-130">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="5243d-131">Please select a Resource Group name and fill in the placeholder.</span><span class="sxs-lookup"><span data-stu-id="5243d-131">Please select a Resource Group name and fill in the placeholder.</span></span>
<span data-ttu-id="5243d-132">The following example creates a resource group named *<YourResourceGroupName>* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="5243d-132">The following example creates a resource group named *<YourResourceGroupName>* in the *eastus* location.</span></span>

```azurecli
# To list locations: az account list-locations --output table
az group create --name "<YourResourceGroupName>" --location "East US"
```

<span data-ttu-id="5243d-133">The resource group you just created is used throughout this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5243d-133">The resource group you just created is used throughout this tutorial.</span></span>

## <a name="create-an-azure-key-vault"></a><span data-ttu-id="5243d-134">Create an Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5243d-134">Create an Azure Key Vault</span></span>

<span data-ttu-id="5243d-135">Next you create a Key Vault using the resource group created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="5243d-135">Next you create a Key Vault using the resource group created in the previous step.</span></span> <span data-ttu-id="5243d-136">Although “ContosoKeyVault” is used as the name for the Key Vault throughout this article, you have to use a unique name.</span><span class="sxs-lookup"><span data-stu-id="5243d-136">Although “ContosoKeyVault” is used as the name for the Key Vault throughout this article, you have to use a unique name.</span></span> <span data-ttu-id="5243d-137">Provide the following information:</span><span class="sxs-lookup"><span data-stu-id="5243d-137">Provide the following information:</span></span>

* <span data-ttu-id="5243d-138">Vault name - **Select a Key Vault Name here**.</span><span class="sxs-lookup"><span data-stu-id="5243d-138">Vault name - **Select a Key Vault Name here**.</span></span>
* <span data-ttu-id="5243d-139">Resource group name - **Select a Resource Group Name here**.</span><span class="sxs-lookup"><span data-stu-id="5243d-139">Resource group name - **Select a Resource Group Name here**.</span></span>
* <span data-ttu-id="5243d-140">The location - **East US**.</span><span class="sxs-lookup"><span data-stu-id="5243d-140">The location - **East US**.</span></span>

```azurecli
az keyvault create --name "<YourKeyVaultName>" --resource-group "<YourResourceGroupName>" --location "East US"
```

<span data-ttu-id="5243d-141">At this point, your Azure account is the only one authorized to perform any operations on this new vault.</span><span class="sxs-lookup"><span data-stu-id="5243d-141">At this point, your Azure account is the only one authorized to perform any operations on this new vault.</span></span>

## <a name="add-a-secret-to-key-vault"></a><span data-ttu-id="5243d-142">Add a secret to key vault</span><span class="sxs-lookup"><span data-stu-id="5243d-142">Add a secret to key vault</span></span>

<span data-ttu-id="5243d-143">We're adding a secret to help illustrate how this works.</span><span class="sxs-lookup"><span data-stu-id="5243d-143">We're adding a secret to help illustrate how this works.</span></span> <span data-ttu-id="5243d-144">You could be storing a SQL connection string or any other information that you need to keep securely but make available to your application.</span><span class="sxs-lookup"><span data-stu-id="5243d-144">You could be storing a SQL connection string or any other information that you need to keep securely but make available to your application.</span></span> <span data-ttu-id="5243d-145">In this tutorial, the password will be called **AppSecret** and will store the value of **MySecret** in it.</span><span class="sxs-lookup"><span data-stu-id="5243d-145">In this tutorial, the password will be called **AppSecret** and will store the value of **MySecret** in it.</span></span>

<span data-ttu-id="5243d-146">Type the commands below to create a secret in Key Vault called **AppSecret** that will store the value **MySecret**:</span><span class="sxs-lookup"><span data-stu-id="5243d-146">Type the commands below to create a secret in Key Vault called **AppSecret** that will store the value **MySecret**:</span></span>

```azurecli
az keyvault secret set --vault-name "<YourKeyVaultName>" --name "AppSecret" --value "MySecret"
```

<span data-ttu-id="5243d-147">To view the value contained in the secret as plain text:</span><span class="sxs-lookup"><span data-stu-id="5243d-147">To view the value contained in the secret as plain text:</span></span>

```azurecli
az keyvault secret show --name "AppSecret" --vault-name "<YourKeyVaultName>"
```

<span data-ttu-id="5243d-148">This command shows the secret information including the URI.</span><span class="sxs-lookup"><span data-stu-id="5243d-148">This command shows the secret information including the URI.</span></span> <span data-ttu-id="5243d-149">After completing these steps, you should have a URI to a secret in an Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5243d-149">After completing these steps, you should have a URI to a secret in an Azure Key Vault.</span></span> <span data-ttu-id="5243d-150">Write this information down.</span><span class="sxs-lookup"><span data-stu-id="5243d-150">Write this information down.</span></span> <span data-ttu-id="5243d-151">You need it in a later step.</span><span class="sxs-lookup"><span data-stu-id="5243d-151">You need it in a later step.</span></span>

## <a name="clone-the-repo"></a><span data-ttu-id="5243d-152">Clone the Repo</span><span class="sxs-lookup"><span data-stu-id="5243d-152">Clone the Repo</span></span>

<span data-ttu-id="5243d-153">Clone the repo in order to make a local copy for you to edit the source by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5243d-153">Clone the repo in order to make a local copy for you to edit the source by running the following command:</span></span>

```
git clone https://github.com/Azure-Samples/key-vault-node-quickstart.git
```

## <a name="install-dependencies"></a><span data-ttu-id="5243d-154">Install dependencies</span><span class="sxs-lookup"><span data-stu-id="5243d-154">Install dependencies</span></span>

<span data-ttu-id="5243d-155">Here we install the dependencies.</span><span class="sxs-lookup"><span data-stu-id="5243d-155">Here we install the dependencies.</span></span> <span data-ttu-id="5243d-156">Run the following commands cd key-vault-node-quickstart npm install</span><span class="sxs-lookup"><span data-stu-id="5243d-156">Run the following commands cd key-vault-node-quickstart npm install</span></span>

<span data-ttu-id="5243d-157">This project used 2 node modules:</span><span class="sxs-lookup"><span data-stu-id="5243d-157">This project used 2 node modules:</span></span>

* [<span data-ttu-id="5243d-158">ms-rest-azure</span><span class="sxs-lookup"><span data-stu-id="5243d-158">ms-rest-azure</span></span>](https://www.npmjs.com/package/ms-rest-azure) 
* [<span data-ttu-id="5243d-159">azure-keyvault</span><span class="sxs-lookup"><span data-stu-id="5243d-159">azure-keyvault</span></span>](https://www.npmjs.com/package/azure-keyvault)

## <a name="publish-the-web-application-to-azure"></a><span data-ttu-id="5243d-160">Publish the web application to Azure</span><span class="sxs-lookup"><span data-stu-id="5243d-160">Publish the web application to Azure</span></span>

<span data-ttu-id="5243d-161">Below are the few steps we need to do</span><span class="sxs-lookup"><span data-stu-id="5243d-161">Below are the few steps we need to do</span></span>

- <span data-ttu-id="5243d-162">The 1st step is to create a [Azure App Service](https://azure.microsoft.com/services/app-service/) Plan.</span><span class="sxs-lookup"><span data-stu-id="5243d-162">The 1st step is to create a [Azure App Service](https://azure.microsoft.com/services/app-service/) Plan.</span></span> <span data-ttu-id="5243d-163">You can store multiple web apps in this plan.</span><span class="sxs-lookup"><span data-stu-id="5243d-163">You can store multiple web apps in this plan.</span></span>

    ```
    az appservice plan create --name myAppServicePlan --resource-group myResourceGroup
    ```
- <span data-ttu-id="5243d-164">Next we create a web app.</span><span class="sxs-lookup"><span data-stu-id="5243d-164">Next we create a web app.</span></span> <span data-ttu-id="5243d-165">In the following example, replace <app_name> with a globally unique app name (valid characters are a-z, 0-9, and -).</span><span class="sxs-lookup"><span data-stu-id="5243d-165">In the following example, replace <app_name> with a globally unique app name (valid characters are a-z, 0-9, and -).</span></span> <span data-ttu-id="5243d-166">The runtime is set to NODE|6.9.</span><span class="sxs-lookup"><span data-stu-id="5243d-166">The runtime is set to NODE|6.9.</span></span> <span data-ttu-id="5243d-167">To see all supported runtimes, run az webapp list-runtimes</span><span class="sxs-lookup"><span data-stu-id="5243d-167">To see all supported runtimes, run az webapp list-runtimes</span></span>
    ```
    # Bash
    az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "NODE|6.9" --deployment-local-git
    ```
    <span data-ttu-id="5243d-168">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="5243d-168">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>
    ```
    {
      "availabilityState": "Normal",
      "clientAffinityEnabled": true,
      "clientCertEnabled": false,
      "cloningInfo": null,
      "containerSize": 0,
      "dailyMemoryTimeQuota": 0,
      "defaultHostName": "<app_name>.azurewebsites.net",
      "enabled": true,
      "deploymentLocalGitUrl": "https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git"
      < JSON data removed for brevity. >
    }
    ```
    <span data-ttu-id="5243d-169">Browse to your newly created web app and you should see a functioning web app.</span><span class="sxs-lookup"><span data-stu-id="5243d-169">Browse to your newly created web app and you should see a functioning web app.</span></span> <span data-ttu-id="5243d-170">Replace <app_name> with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="5243d-170">Replace <app_name> with a unique app name.</span></span>

    ```
    http://<app name>.azurewebsites.net
    ```
    <span data-ttu-id="5243d-171">The above command also creates a Git-enabled app which allows you to deploy to azure from your local git.</span><span class="sxs-lookup"><span data-stu-id="5243d-171">The above command also creates a Git-enabled app which allows you to deploy to azure from your local git.</span></span> 
    <span data-ttu-id="5243d-172">Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'</span><span class="sxs-lookup"><span data-stu-id="5243d-172">Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'</span></span>

- <span data-ttu-id="5243d-173">Create a deployment user After the previous command is completed you can add add an Azure remote to your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="5243d-173">Create a deployment user After the previous command is completed you can add add an Azure remote to your local Git repository.</span></span> <span data-ttu-id="5243d-174">Replace <url> with the URL of the Git remote that you got from Enable Git for your app.</span><span class="sxs-lookup"><span data-stu-id="5243d-174">Replace <url> with the URL of the Git remote that you got from Enable Git for your app.</span></span>

    ```
    git remote add azure <url>
    ```

## <a name="enable-a-managed-identity-for-the-web-app"></a><span data-ttu-id="5243d-175">Enable a managed identity for the web app</span><span class="sxs-lookup"><span data-stu-id="5243d-175">Enable a managed identity for the web app</span></span>

<span data-ttu-id="5243d-176">Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Key Vault to retrieve them.</span><span class="sxs-lookup"><span data-stu-id="5243d-176">Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Key Vault to retrieve them.</span></span> <span data-ttu-id="5243d-177">[Managed identities for Azure resources overview](../active-directory/managed-identities-azure-resources/overview.md) makes solving this problem simpler, by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5243d-177">[Managed identities for Azure resources overview](../active-directory/managed-identities-azure-resources/overview.md) makes solving this problem simpler, by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5243d-178">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="5243d-178">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span></span>

<span data-ttu-id="5243d-179">Run the assign-identity command to create the identity for this application:</span><span class="sxs-lookup"><span data-stu-id="5243d-179">Run the assign-identity command to create the identity for this application:</span></span>

```azurecli
az webapp identity assign --name <app_name> --resource-group "<YourResourceGroupName>"
```

<span data-ttu-id="5243d-180">This command is the equivalent of going to the portal and switching the **Identity / System assigned** setting to **On** in the web application properties.</span><span class="sxs-lookup"><span data-stu-id="5243d-180">This command is the equivalent of going to the portal and switching the **Identity / System assigned** setting to **On** in the web application properties.</span></span>

### <a name="assign-permissions-to-your-application-to-read-secrets-from-key-vault"></a><span data-ttu-id="5243d-181">Assign permissions to your application to read secrets from Key Vault</span><span class="sxs-lookup"><span data-stu-id="5243d-181">Assign permissions to your application to read secrets from Key Vault</span></span>

<span data-ttu-id="5243d-182">Write down or copy the output of the command above.</span><span class="sxs-lookup"><span data-stu-id="5243d-182">Write down or copy the output of the command above.</span></span> <span data-ttu-id="5243d-183">It should be in the format:</span><span class="sxs-lookup"><span data-stu-id="5243d-183">It should be in the format:</span></span>
        
        {
          "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          "type": "SystemAssigned"
        }
        
<span data-ttu-id="5243d-184">Then, run this command using the name of your Key Vault and the value of PrincipalId copied from above:</span><span class="sxs-lookup"><span data-stu-id="5243d-184">Then, run this command using the name of your Key Vault and the value of PrincipalId copied from above:</span></span>

```azurecli
az keyvault set-policy --name '<YourKeyVaultName>' --object-id <PrincipalId> --secret-permissions get
```

## <a name="deploy-the-node-app-to-azure-and-retrieve-the-secret-value"></a><span data-ttu-id="5243d-185">Deploy the Node App to Azure and retrieve the secret value</span><span class="sxs-lookup"><span data-stu-id="5243d-185">Deploy the Node App to Azure and retrieve the secret value</span></span>

<span data-ttu-id="5243d-186">Now that everything is set.</span><span class="sxs-lookup"><span data-stu-id="5243d-186">Now that everything is set.</span></span> <span data-ttu-id="5243d-187">Run the following command to deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="5243d-187">Run the following command to deploy the app to Azure</span></span>

```
git push azure master
```

<span data-ttu-id="5243d-188">After this when you browse https://<app_name>.azurewebsites.net you can see the secret value.</span><span class="sxs-lookup"><span data-stu-id="5243d-188">After this when you browse https://<app_name>.azurewebsites.net you can see the secret value.</span></span>
<span data-ttu-id="5243d-189">Make sure that you replaced the name <YourKeyVaultName> with your vault name</span><span class="sxs-lookup"><span data-stu-id="5243d-189">Make sure that you replaced the name <YourKeyVaultName> with your vault name</span></span>

## <a name="next-steps"></a><span data-ttu-id="5243d-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="5243d-190">Next steps</span></span>

* [<span data-ttu-id="5243d-191">Azure Key Vault Home Page</span><span class="sxs-lookup"><span data-stu-id="5243d-191">Azure Key Vault Home Page</span></span>](https://azure.microsoft.com/services/key-vault/)
* [<span data-ttu-id="5243d-192">Azure Key Vault Documentation</span><span class="sxs-lookup"><span data-stu-id="5243d-192">Azure Key Vault Documentation</span></span>](https://docs.microsoft.com/azure/key-vault/)
* [<span data-ttu-id="5243d-193">Azure SDK For Node</span><span class="sxs-lookup"><span data-stu-id="5243d-193">Azure SDK For Node</span></span>](https://docs.microsoft.com/javascript/api/overview/azure/key-vault)
* [<span data-ttu-id="5243d-194">Azure REST API Reference</span><span class="sxs-lookup"><span data-stu-id="5243d-194">Azure REST API Reference</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
