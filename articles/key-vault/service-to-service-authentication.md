---
title: Service-to-service authentication to Azure Key Vault using .NET
description: Use the Microsoft.Azure.Services.AppAuthentication library to authenticate to Azure Key Vault using .NET.
keywords: azure key-vault authentication local credentials
author: bryanla
manager: mbaldwin
services: key-vault
ms.author: bryanla
ms.date: 09/05/2018
ms.topic: conceptual
ms.prod: ''
ms.service: key-vault
ms.technology: ''
ms.assetid: 4be434c4-0c99-4800-b775-c9713c973ee9
ms.openlocfilehash: d9fc845316d6e785d8215ac738b893ebc080d911
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855631"
---
# <a name="service-to-service-authentication-to-azure-key-vault-using-net"></a><span data-ttu-id="e01ea-104">Service-to-service authentication to Azure Key Vault using .NET</span><span class="sxs-lookup"><span data-stu-id="e01ea-104">Service-to-service authentication to Azure Key Vault using .NET</span></span>

<span data-ttu-id="e01ea-105">To authenticate to Azure Key Vault, you need an Azure Active Directory (AD) credential, either a shared secret or a certificate.</span><span class="sxs-lookup"><span data-stu-id="e01ea-105">To authenticate to Azure Key Vault, you need an Azure Active Directory (AD) credential, either a shared secret or a certificate.</span></span> <span data-ttu-id="e01ea-106">Managing such credentials can be difficult and it's tempting to bundle credentials into an app by including them in source or configuration files.</span><span class="sxs-lookup"><span data-stu-id="e01ea-106">Managing such credentials can be difficult and it's tempting to bundle credentials into an app by including them in source or configuration files.</span></span>

<span data-ttu-id="e01ea-107">The `Microsoft.Azure.Services.AppAuthentication` for .NET library simplifies this problem.</span><span class="sxs-lookup"><span data-stu-id="e01ea-107">The `Microsoft.Azure.Services.AppAuthentication` for .NET library simplifies this problem.</span></span> <span data-ttu-id="e01ea-108">It uses the developer's credentials to authenticate during local development.</span><span class="sxs-lookup"><span data-stu-id="e01ea-108">It uses the developer's credentials to authenticate during local development.</span></span> <span data-ttu-id="e01ea-109">When the solution is later deployed to Azure, the library automatically switches to application credentials.</span><span class="sxs-lookup"><span data-stu-id="e01ea-109">When the solution is later deployed to Azure, the library automatically switches to application credentials.</span></span>  

<span data-ttu-id="e01ea-110">Using developer credentials during local development is more secure because you do not need to create Azure AD credentials or share credentials between developers.</span><span class="sxs-lookup"><span data-stu-id="e01ea-110">Using developer credentials during local development is more secure because you do not need to create Azure AD credentials or share credentials between developers.</span></span>

<span data-ttu-id="e01ea-111">The `Microsoft.Azure.Services.AppAuthentication` library manages authentication automatically, which in turn allows you to focus on your solution, rather than your credentials.</span><span class="sxs-lookup"><span data-stu-id="e01ea-111">The `Microsoft.Azure.Services.AppAuthentication` library manages authentication automatically, which in turn allows you to focus on your solution, rather than your credentials.</span></span>

<span data-ttu-id="e01ea-112">The `Microsoft.Azure.Services.AppAuthentication` library supports local development with Microsoft Visual Studio, Azure CLI, or Azure AD Integrated Authentication.</span><span class="sxs-lookup"><span data-stu-id="e01ea-112">The `Microsoft.Azure.Services.AppAuthentication` library supports local development with Microsoft Visual Studio, Azure CLI, or Azure AD Integrated Authentication.</span></span> <span data-ttu-id="e01ea-113">When deployed to Azure App Services or an Azure Virtual Machine (VM), the library automatically uses [managed identities for Azure services](/azure/active-directory/msi-overview).</span><span class="sxs-lookup"><span data-stu-id="e01ea-113">When deployed to Azure App Services or an Azure Virtual Machine (VM), the library automatically uses [managed identities for Azure services](/azure/active-directory/msi-overview).</span></span> <span data-ttu-id="e01ea-114">No code or configuration changes are required.</span><span class="sxs-lookup"><span data-stu-id="e01ea-114">No code or configuration changes are required.</span></span> <span data-ttu-id="e01ea-115">The library also supports direct use of Azure AD [client credentials](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal) when a managed identity is not available, or when the developer's security context cannot be determined during local development.</span><span class="sxs-lookup"><span data-stu-id="e01ea-115">The library also supports direct use of Azure AD [client credentials](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal) when a managed identity is not available, or when the developer's security context cannot be determined during local development.</span></span>

<a name="asal"></a>
## <a name="using-the-library"></a><span data-ttu-id="e01ea-116">Using the library</span><span class="sxs-lookup"><span data-stu-id="e01ea-116">Using the library</span></span>

<span data-ttu-id="e01ea-117">For .NET applications, the simplest way to work with a managed identity is through the `Microsoft.Azure.Services.AppAuthentication` package.</span><span class="sxs-lookup"><span data-stu-id="e01ea-117">For .NET applications, the simplest way to work with a managed identity is through the `Microsoft.Azure.Services.AppAuthentication` package.</span></span> <span data-ttu-id="e01ea-118">Here's how to get started:</span><span class="sxs-lookup"><span data-stu-id="e01ea-118">Here's how to get started:</span></span>

1. <span data-ttu-id="e01ea-119">Add a reference to the [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) NuGet package to your application.</span><span class="sxs-lookup"><span data-stu-id="e01ea-119">Add a reference to the [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) NuGet package to your application.</span></span>

2. <span data-ttu-id="e01ea-120">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="e01ea-120">Add the following code:</span></span>

    ``` csharp
    using Microsoft.Azure.Services.AppAuthentication;
    using Microsoft.Azure.KeyVault;

    // ...

    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(
    azureServiceTokenProvider.KeyVaultTokenCallback));

    // or

    var azureServiceTokenProvider = new AzureServiceTokenProvider();
    string accessToken = await azureServiceTokenProvider.GetAccessTokenAsync(
       "https://management.azure.com/").ConfigureAwait(false);
    ```

<span data-ttu-id="e01ea-121">The `AzureServiceTokenProvider` class caches the token in memory and retrieves it from Azure AD just before expiration.</span><span class="sxs-lookup"><span data-stu-id="e01ea-121">The `AzureServiceTokenProvider` class caches the token in memory and retrieves it from Azure AD just before expiration.</span></span> <span data-ttu-id="e01ea-122">Consequently, you no longer have to check the expiration before calling the `GetAccessTokenAsync` method.</span><span class="sxs-lookup"><span data-stu-id="e01ea-122">Consequently, you no longer have to check the expiration before calling the `GetAccessTokenAsync` method.</span></span> <span data-ttu-id="e01ea-123">Just call the method when you want to use the token.</span><span class="sxs-lookup"><span data-stu-id="e01ea-123">Just call the method when you want to use the token.</span></span> 

<span data-ttu-id="e01ea-124">The `GetAccessTokenAsync` method requires a resource identifier.</span><span class="sxs-lookup"><span data-stu-id="e01ea-124">The `GetAccessTokenAsync` method requires a resource identifier.</span></span> <span data-ttu-id="e01ea-125">To learn more, see [which Azure services support managed identities for Azure resources](https://docs.microsoft.com/azure/active-directory/msi-overview#which-azure-services-support-managed-service-identity).</span><span class="sxs-lookup"><span data-stu-id="e01ea-125">To learn more, see [which Azure services support managed identities for Azure resources](https://docs.microsoft.com/azure/active-directory/msi-overview#which-azure-services-support-managed-service-identity).</span></span>


<a name="samples"></a>
## <a name="samples"></a><span data-ttu-id="e01ea-126">Samples</span><span class="sxs-lookup"><span data-stu-id="e01ea-126">Samples</span></span>

<span data-ttu-id="e01ea-127">The following samples show the `Microsoft.Azure.Services.AppAuthentication` library in action:</span><span class="sxs-lookup"><span data-stu-id="e01ea-127">The following samples show the `Microsoft.Azure.Services.AppAuthentication` library in action:</span></span>

1. [<span data-ttu-id="e01ea-128">Use a managed identity to retrieve a secret from Azure Key Vault at runtime</span><span class="sxs-lookup"><span data-stu-id="e01ea-128">Use a managed identity to retrieve a secret from Azure Key Vault at runtime</span></span>](https://github.com/Azure-Samples/app-service-msi-keyvault-dotnet)

2. <span data-ttu-id="e01ea-129">[Programmatically deploy an Azure Resource Manager template from an Azure VM with a managed identity](https://github.com/Azure-Samples/windowsvm-msi-arm-dotnet).</span><span class="sxs-lookup"><span data-stu-id="e01ea-129">[Programmatically deploy an Azure Resource Manager template from an Azure VM with a managed identity](https://github.com/Azure-Samples/windowsvm-msi-arm-dotnet).</span></span>

3. <span data-ttu-id="e01ea-130">[Use .NET Core sample and a managed identity to call Azure services from an Azure Linux VM](https://github.com/Azure-Samples/linuxvm-msi-keyvault-arm-dotnet/).</span><span class="sxs-lookup"><span data-stu-id="e01ea-130">[Use .NET Core sample and a managed identity to call Azure services from an Azure Linux VM](https://github.com/Azure-Samples/linuxvm-msi-keyvault-arm-dotnet/).</span></span>


<a name="local"></a>
## <a name="local-development-authentication"></a><span data-ttu-id="e01ea-131">Local development authentication</span><span class="sxs-lookup"><span data-stu-id="e01ea-131">Local development authentication</span></span>

<span data-ttu-id="e01ea-132">For local development, there are two primary authentication scenarios:</span><span class="sxs-lookup"><span data-stu-id="e01ea-132">For local development, there are two primary authentication scenarios:</span></span>

- [<span data-ttu-id="e01ea-133">Authenticating to Azure services</span><span class="sxs-lookup"><span data-stu-id="e01ea-133">Authenticating to Azure services</span></span>](#authenticating-to-azure-services)
- [<span data-ttu-id="e01ea-134">Authenticating to custom services</span><span class="sxs-lookup"><span data-stu-id="e01ea-134">Authenticating to custom services</span></span>](#authenticating-to-custom-services)

<span data-ttu-id="e01ea-135">Here, you learn the requirements for each scenario and supported tools.</span><span class="sxs-lookup"><span data-stu-id="e01ea-135">Here, you learn the requirements for each scenario and supported tools.</span></span>


### <a name="authenticating-to-azure-services"></a><span data-ttu-id="e01ea-136">Authenticating to Azure Services</span><span class="sxs-lookup"><span data-stu-id="e01ea-136">Authenticating to Azure Services</span></span>

<span data-ttu-id="e01ea-137">Local machines do not support managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e01ea-137">Local machines do not support managed identities for Azure resources.</span></span>  <span data-ttu-id="e01ea-138">As a result, the `Microsoft.Azure.Services.AppAuthentication` library uses your developer credentials to run in your local development environment.</span><span class="sxs-lookup"><span data-stu-id="e01ea-138">As a result, the `Microsoft.Azure.Services.AppAuthentication` library uses your developer credentials to run in your local development environment.</span></span> <span data-ttu-id="e01ea-139">When the solution is deployed to Azure, the library uses a managed identity to switch to an OAuth 2.0 client credential grant flow.</span><span class="sxs-lookup"><span data-stu-id="e01ea-139">When the solution is deployed to Azure, the library uses a managed identity to switch to an OAuth 2.0 client credential grant flow.</span></span>  <span data-ttu-id="e01ea-140">This means you can test the same code locally and remotely without worry.</span><span class="sxs-lookup"><span data-stu-id="e01ea-140">This means you can test the same code locally and remotely without worry.</span></span>

<span data-ttu-id="e01ea-141">For local development, `AzureServiceTokenProvider` fetches tokens using **Visual Studio**, **Azure command-line interface** (CLI), or **Azure AD Integrated Authentication**.</span><span class="sxs-lookup"><span data-stu-id="e01ea-141">For local development, `AzureServiceTokenProvider` fetches tokens using **Visual Studio**, **Azure command-line interface** (CLI), or **Azure AD Integrated Authentication**.</span></span> <span data-ttu-id="e01ea-142">Each option is tried sequentially and the library uses the first option that succeeds.</span><span class="sxs-lookup"><span data-stu-id="e01ea-142">Each option is tried sequentially and the library uses the first option that succeeds.</span></span> <span data-ttu-id="e01ea-143">If no option works, an `AzureServiceTokenProviderException` exception is thrown with detailed information.</span><span class="sxs-lookup"><span data-stu-id="e01ea-143">If no option works, an `AzureServiceTokenProviderException` exception is thrown with detailed information.</span></span>

### <a name="authenticating-with-visual-studio"></a><span data-ttu-id="e01ea-144">Authenticating with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e01ea-144">Authenticating with Visual Studio</span></span>

<span data-ttu-id="e01ea-145">To use Visual Studio, verify:</span><span class="sxs-lookup"><span data-stu-id="e01ea-145">To use Visual Studio, verify:</span></span>

1. <span data-ttu-id="e01ea-146">You've installed [Visual Studio 2017 v15.5](https://blogs.msdn.microsoft.com/visualstudio/2017/10/11/visual-studio-2017-version-15-5-preview/) or later.</span><span class="sxs-lookup"><span data-stu-id="e01ea-146">You've installed [Visual Studio 2017 v15.5](https://blogs.msdn.microsoft.com/visualstudio/2017/10/11/visual-studio-2017-version-15-5-preview/) or later.</span></span>

2. <span data-ttu-id="e01ea-147">The [App Authentication extension for Visual Studio](https://go.microsoft.com/fwlink/?linkid=862354) is installed.</span><span class="sxs-lookup"><span data-stu-id="e01ea-147">The [App Authentication extension for Visual Studio](https://go.microsoft.com/fwlink/?linkid=862354) is installed.</span></span>
 
3. <span data-ttu-id="e01ea-148">You signed in to Visual Studio and have selected an account to use for local development.</span><span class="sxs-lookup"><span data-stu-id="e01ea-148">You signed in to Visual Studio and have selected an account to use for local development.</span></span> <span data-ttu-id="e01ea-149">Use **Tools**&nbsp;>&nbsp;**Options**&nbsp;>&nbsp;**Azure Service Authentication** to choose a local development account.</span><span class="sxs-lookup"><span data-stu-id="e01ea-149">Use **Tools**&nbsp;>&nbsp;**Options**&nbsp;>&nbsp;**Azure Service Authentication** to choose a local development account.</span></span> 

<span data-ttu-id="e01ea-150">If you run into problems using Visual Studio, such as errors regarding the token provider file, carefully review these steps.</span><span class="sxs-lookup"><span data-stu-id="e01ea-150">If you run into problems using Visual Studio, such as errors regarding the token provider file, carefully review these steps.</span></span> 

<span data-ttu-id="e01ea-151">It may also be necessary to reauthenticate your developer token.</span><span class="sxs-lookup"><span data-stu-id="e01ea-151">It may also be necessary to reauthenticate your developer token.</span></span>  <span data-ttu-id="e01ea-152">To do so, go to **Tools**&nbsp;>&nbsp;**Options**>**Azure&nbsp;Service&nbsp;Authentication** and look for a **Re-authenticate** link under the selected account.</span><span class="sxs-lookup"><span data-stu-id="e01ea-152">To do so, go to **Tools**&nbsp;>&nbsp;**Options**>**Azure&nbsp;Service&nbsp;Authentication** and look for a **Re-authenticate** link under the selected account.</span></span>  <span data-ttu-id="e01ea-153">Select it to authenticate.</span><span class="sxs-lookup"><span data-stu-id="e01ea-153">Select it to authenticate.</span></span> 

### <a name="authenticating-with-azure-cli"></a><span data-ttu-id="e01ea-154">Authenticating with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e01ea-154">Authenticating with Azure CLI</span></span>

<span data-ttu-id="e01ea-155">To use Azure CLI for local development:</span><span class="sxs-lookup"><span data-stu-id="e01ea-155">To use Azure CLI for local development:</span></span>

1. <span data-ttu-id="e01ea-156">Install [Azure CLI v2.0.12](/cli/azure/install-azure-cli) or later.</span><span class="sxs-lookup"><span data-stu-id="e01ea-156">Install [Azure CLI v2.0.12](/cli/azure/install-azure-cli) or later.</span></span> <span data-ttu-id="e01ea-157">Upgrade earlier versions.</span><span class="sxs-lookup"><span data-stu-id="e01ea-157">Upgrade earlier versions.</span></span> 

2. <span data-ttu-id="e01ea-158">Use **az login** to sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="e01ea-158">Use **az login** to sign in to Azure.</span></span>

<span data-ttu-id="e01ea-159">Use `az account get-access-token` to verify access.</span><span class="sxs-lookup"><span data-stu-id="e01ea-159">Use `az account get-access-token` to verify access.</span></span>  <span data-ttu-id="e01ea-160">If you receive an error, verify that Step 1 completed successfully.</span><span class="sxs-lookup"><span data-stu-id="e01ea-160">If you receive an error, verify that Step 1 completed successfully.</span></span> 

<span data-ttu-id="e01ea-161">If Azure CLI is not installed to the default directory, you may receive an error reporting that `AzureServiceTokenProvider` cannot find the path for Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e01ea-161">If Azure CLI is not installed to the default directory, you may receive an error reporting that `AzureServiceTokenProvider` cannot find the path for Azure CLI.</span></span>  <span data-ttu-id="e01ea-162">Use the **AzureCLIPath**environment variable to define the Azure CLI installation folder.</span><span class="sxs-lookup"><span data-stu-id="e01ea-162">Use the **AzureCLIPath**environment variable to define the Azure CLI installation folder.</span></span> <span data-ttu-id="e01ea-163">`AzureServiceTokenProvider` adds the directory specified in the **AzureCLIPath** environment variable to the **Path** environment variable when necessary.</span><span class="sxs-lookup"><span data-stu-id="e01ea-163">`AzureServiceTokenProvider` adds the directory specified in the **AzureCLIPath** environment variable to the **Path** environment variable when necessary.</span></span>

<span data-ttu-id="e01ea-164">If you are signed in to Azure CLI using multiple accounts or your account has access to multiple subscriptions, you need to specify the specific subscription to be used.</span><span class="sxs-lookup"><span data-stu-id="e01ea-164">If you are signed in to Azure CLI using multiple accounts or your account has access to multiple subscriptions, you need to specify the specific subscription to be used.</span></span>  <span data-ttu-id="e01ea-165">To do so, use:</span><span class="sxs-lookup"><span data-stu-id="e01ea-165">To do so, use:</span></span>

```
az account set --subscription <subscription-id>
```

<span data-ttu-id="e01ea-166">This command generates output only on failure.</span><span class="sxs-lookup"><span data-stu-id="e01ea-166">This command generates output only on failure.</span></span>  <span data-ttu-id="e01ea-167">To verify the current account settings, use:</span><span class="sxs-lookup"><span data-stu-id="e01ea-167">To verify the current account settings, use:</span></span>

```
az account list
```

### <a name="authenticating-with-azure-ad-integrate-authentication"></a><span data-ttu-id="e01ea-168">Authenticating with Azure AD Integrate authentication</span><span class="sxs-lookup"><span data-stu-id="e01ea-168">Authenticating with Azure AD Integrate authentication</span></span>

<span data-ttu-id="e01ea-169">To use Azure AD authentication, verify that:</span><span class="sxs-lookup"><span data-stu-id="e01ea-169">To use Azure AD authentication, verify that:</span></span>

- <span data-ttu-id="e01ea-170">Your on-premises active directory [syncs to Azure AD](/azure/active-directory/connect/active-directory-aadconnect).</span><span class="sxs-lookup"><span data-stu-id="e01ea-170">Your on-premises active directory [syncs to Azure AD](/azure/active-directory/connect/active-directory-aadconnect).</span></span>

- <span data-ttu-id="e01ea-171">Your code is running on a domain-joined machine.</span><span class="sxs-lookup"><span data-stu-id="e01ea-171">Your code is running on a domain-joined machine.</span></span>


### <a name="authenticating-to-custom-services"></a><span data-ttu-id="e01ea-172">Authenticating to custom services</span><span class="sxs-lookup"><span data-stu-id="e01ea-172">Authenticating to custom services</span></span>

<span data-ttu-id="e01ea-173">When a service calls Azure services, the previous steps work because Azure services allow access to both users and applications.</span><span class="sxs-lookup"><span data-stu-id="e01ea-173">When a service calls Azure services, the previous steps work because Azure services allow access to both users and applications.</span></span>  

<span data-ttu-id="e01ea-174">When creating a service that calls a custom service, use Azure AD client credentials for local development authentication.</span><span class="sxs-lookup"><span data-stu-id="e01ea-174">When creating a service that calls a custom service, use Azure AD client credentials for local development authentication.</span></span>  <span data-ttu-id="e01ea-175">There are two options:</span><span class="sxs-lookup"><span data-stu-id="e01ea-175">There are two options:</span></span> 

1.  <span data-ttu-id="e01ea-176">Use a service principal to sign into Azure:</span><span class="sxs-lookup"><span data-stu-id="e01ea-176">Use a service principal to sign into Azure:</span></span>

    1.  <span data-ttu-id="e01ea-177">[Create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e01ea-177">[Create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>

    2.  <span data-ttu-id="e01ea-178">Use Azure CLI to sign in:</span><span class="sxs-lookup"><span data-stu-id="e01ea-178">Use Azure CLI to sign in:</span></span>

        ```
        az login --service-principal -u <principal-id> --password <password>
           --tenant <tenant-id> --allow-no-subscriptions
        ```

        <span data-ttu-id="e01ea-179">Because the service principal may not have access to a subscription, use the `--allow-no-subscriptions` argument.</span><span class="sxs-lookup"><span data-stu-id="e01ea-179">Because the service principal may not have access to a subscription, use the `--allow-no-subscriptions` argument.</span></span>

2.  <span data-ttu-id="e01ea-180">Use environment variables to specify service principal details.</span><span class="sxs-lookup"><span data-stu-id="e01ea-180">Use environment variables to specify service principal details.</span></span>  <span data-ttu-id="e01ea-181">For details, see [Running the application using a service principal](#running-the-application-using-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="e01ea-181">For details, see [Running the application using a service principal](#running-the-application-using-a-service-principal).</span></span>

<span data-ttu-id="e01ea-182">Once you've signed in to Azure, `AzureServiceTokenProvider` uses the service principal to retrieve a token for local development.</span><span class="sxs-lookup"><span data-stu-id="e01ea-182">Once you've signed in to Azure, `AzureServiceTokenProvider` uses the service principal to retrieve a token for local development.</span></span>

<span data-ttu-id="e01ea-183">This applies only to local development.</span><span class="sxs-lookup"><span data-stu-id="e01ea-183">This applies only to local development.</span></span> <span data-ttu-id="e01ea-184">When your solution is deployed to Azure, the library switches to a managed identity for authentication.</span><span class="sxs-lookup"><span data-stu-id="e01ea-184">When your solution is deployed to Azure, the library switches to a managed identity for authentication.</span></span>

<a name="msi"></a>
## <a name="running-the-application-using-managed-identity"></a><span data-ttu-id="e01ea-185">Running the application using managed identity</span><span class="sxs-lookup"><span data-stu-id="e01ea-185">Running the application using managed identity</span></span> 

<span data-ttu-id="e01ea-186">When you run your code on an Azure App Service or an Azure VM with a managed identity enabled, the library automatically uses the managed identity.</span><span class="sxs-lookup"><span data-stu-id="e01ea-186">When you run your code on an Azure App Service or an Azure VM with a managed identity enabled, the library automatically uses the managed identity.</span></span> <span data-ttu-id="e01ea-187">No code changes are required.</span><span class="sxs-lookup"><span data-stu-id="e01ea-187">No code changes are required.</span></span> 


<a name="sp"></a>
## <a name="running-the-application-using-a-service-principal"></a><span data-ttu-id="e01ea-188">Running the application using a Service Principal</span><span class="sxs-lookup"><span data-stu-id="e01ea-188">Running the application using a Service Principal</span></span> 

<span data-ttu-id="e01ea-189">It may be necessary to create an Azure AD Client credential to authenticate.</span><span class="sxs-lookup"><span data-stu-id="e01ea-189">It may be necessary to create an Azure AD Client credential to authenticate.</span></span> <span data-ttu-id="e01ea-190">Common examples include:</span><span class="sxs-lookup"><span data-stu-id="e01ea-190">Common examples include:</span></span>

1. <span data-ttu-id="e01ea-191">Your code runs on a local development environment, but not under the developer's identity.</span><span class="sxs-lookup"><span data-stu-id="e01ea-191">Your code runs on a local development environment, but not under the developer's identity.</span></span>  <span data-ttu-id="e01ea-192">Service Fabric, for example, uses the [NetworkService account](/azure/service-fabric/service-fabric-application-secret-management) for local development.</span><span class="sxs-lookup"><span data-stu-id="e01ea-192">Service Fabric, for example, uses the [NetworkService account](/azure/service-fabric/service-fabric-application-secret-management) for local development.</span></span>
 
2. <span data-ttu-id="e01ea-193">Your code runs on a local development environment and you authenticate to a custom service, so you can't use your developer identity.</span><span class="sxs-lookup"><span data-stu-id="e01ea-193">Your code runs on a local development environment and you authenticate to a custom service, so you can't use your developer identity.</span></span> 
 
3. <span data-ttu-id="e01ea-194">Your code is running on an Azure compute resource that does not yet support managed identities for Azure resources, such as Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="e01ea-194">Your code is running on an Azure compute resource that does not yet support managed identities for Azure resources, such as Azure Batch.</span></span>

<span data-ttu-id="e01ea-195">To use a certificate to sign into Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e01ea-195">To use a certificate to sign into Azure AD:</span></span>

1. <span data-ttu-id="e01ea-196">Create a [service principal certificate](/azure/azure-resource-manager/resource-group-authenticate-service-principal).</span><span class="sxs-lookup"><span data-stu-id="e01ea-196">Create a [service principal certificate](/azure/azure-resource-manager/resource-group-authenticate-service-principal).</span></span> 

2. <span data-ttu-id="e01ea-197">Deploy the certificate to either the _LocalMachine_ or _CurrentUser_ store.</span><span class="sxs-lookup"><span data-stu-id="e01ea-197">Deploy the certificate to either the _LocalMachine_ or _CurrentUser_ store.</span></span> 

3. <span data-ttu-id="e01ea-198">Set an environment variable named **AzureServicesAuthConnectionString** to:</span><span class="sxs-lookup"><span data-stu-id="e01ea-198">Set an environment variable named **AzureServicesAuthConnectionString** to:</span></span>

    ```
    RunAs=App;AppId={AppId};TenantId={TenantId};CertificateThumbprint={Thumbprint};
          CertificateStoreLocation={LocalMachine or CurrentUser}
    ```
 
    <span data-ttu-id="e01ea-199">Replace _{AppId}_, _{TenantId}_, and _{Thumbprint}_ with values generated in Step 1.</span><span class="sxs-lookup"><span data-stu-id="e01ea-199">Replace _{AppId}_, _{TenantId}_, and _{Thumbprint}_ with values generated in Step 1.</span></span>

    <span data-ttu-id="e01ea-200">**CertificateStoreLocation** must be either _CurrentUser_ or _LocalMachine_, based on your deployment plan.</span><span class="sxs-lookup"><span data-stu-id="e01ea-200">**CertificateStoreLocation** must be either _CurrentUser_ or _LocalMachine_, based on your deployment plan.</span></span>

4. <span data-ttu-id="e01ea-201">Run the application.</span><span class="sxs-lookup"><span data-stu-id="e01ea-201">Run the application.</span></span> 

<span data-ttu-id="e01ea-202">To sign in using an Azure AD shared secret credential:</span><span class="sxs-lookup"><span data-stu-id="e01ea-202">To sign in using an Azure AD shared secret credential:</span></span>

1. <span data-ttu-id="e01ea-203">Create a [service principal with a password](/azure/azure-resource-manager/resource-group-authenticate-service-principal) and grant it access to the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e01ea-203">Create a [service principal with a password](/azure/azure-resource-manager/resource-group-authenticate-service-principal) and grant it access to the Key Vault.</span></span> 

2. <span data-ttu-id="e01ea-204">Set an environment variable named **AzureServicesAuthConnectionString** to:</span><span class="sxs-lookup"><span data-stu-id="e01ea-204">Set an environment variable named **AzureServicesAuthConnectionString** to:</span></span>

    ```
    RunAs=App;AppId={AppId};TenantId={TenantId};AppKey={ClientSecret} 
    ```

    <span data-ttu-id="e01ea-205">Replace _{AppId}_, _{TenantId}_, and _{ClientSecret}_ with values generated in Step 1.</span><span class="sxs-lookup"><span data-stu-id="e01ea-205">Replace _{AppId}_, _{TenantId}_, and _{ClientSecret}_ with values generated in Step 1.</span></span>

3. <span data-ttu-id="e01ea-206">Run the application.</span><span class="sxs-lookup"><span data-stu-id="e01ea-206">Run the application.</span></span> 

<span data-ttu-id="e01ea-207">Once everything's set up correctly, no further code changes are necessary.</span><span class="sxs-lookup"><span data-stu-id="e01ea-207">Once everything's set up correctly, no further code changes are necessary.</span></span>  <span data-ttu-id="e01ea-208">`AzureServiceTokenProvider` uses the environment variable and the certificate to authenticate to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e01ea-208">`AzureServiceTokenProvider` uses the environment variable and the certificate to authenticate to Azure AD.</span></span> 

<a name="connectionstrings"></a>
## <a name="connection-string-support"></a><span data-ttu-id="e01ea-209">Connection String Support</span><span class="sxs-lookup"><span data-stu-id="e01ea-209">Connection String Support</span></span>

<span data-ttu-id="e01ea-210">By default, `AzureServiceTokenProvider` uses multiple methods to retrieve a token.</span><span class="sxs-lookup"><span data-stu-id="e01ea-210">By default, `AzureServiceTokenProvider` uses multiple methods to retrieve a token.</span></span> 

<span data-ttu-id="e01ea-211">To control the process, use a connection string passed to the `AzureServiceTokenProvider` constructor or specified in the *AzureServicesAuthConnectionString* environment variable.</span><span class="sxs-lookup"><span data-stu-id="e01ea-211">To control the process, use a connection string passed to the `AzureServiceTokenProvider` constructor or specified in the *AzureServicesAuthConnectionString* environment variable.</span></span> 

<span data-ttu-id="e01ea-212">The following options are supported:</span><span class="sxs-lookup"><span data-stu-id="e01ea-212">The following options are supported:</span></span>

| <span data-ttu-id="e01ea-213">Connection&nbsp;string&nbsp;option</span><span class="sxs-lookup"><span data-stu-id="e01ea-213">Connection&nbsp;string&nbsp;option</span></span> | <span data-ttu-id="e01ea-214">Scenario</span><span class="sxs-lookup"><span data-stu-id="e01ea-214">Scenario</span></span> | <span data-ttu-id="e01ea-215">Comments</span><span class="sxs-lookup"><span data-stu-id="e01ea-215">Comments</span></span>|
|:--------------------------------|:------------------------|:----------------------------|
| `RunAs=Developer; DeveloperTool=AzureCli` | <span data-ttu-id="e01ea-216">Local development</span><span class="sxs-lookup"><span data-stu-id="e01ea-216">Local development</span></span> | <span data-ttu-id="e01ea-217">AzureServiceTokenProvider uses AzureCli to get token.</span><span class="sxs-lookup"><span data-stu-id="e01ea-217">AzureServiceTokenProvider uses AzureCli to get token.</span></span> |
| `RunAs=Developer; DeveloperTool=VisualStudio` | <span data-ttu-id="e01ea-218">Local development</span><span class="sxs-lookup"><span data-stu-id="e01ea-218">Local development</span></span> | <span data-ttu-id="e01ea-219">AzureServiceTokenProvider uses Visual Studio to get token.</span><span class="sxs-lookup"><span data-stu-id="e01ea-219">AzureServiceTokenProvider uses Visual Studio to get token.</span></span> |
| `RunAs=CurrentUser;` | <span data-ttu-id="e01ea-220">Local development</span><span class="sxs-lookup"><span data-stu-id="e01ea-220">Local development</span></span> | <span data-ttu-id="e01ea-221">AzureServiceTokenProvider uses Azure AD Integrated Authentication to get token.</span><span class="sxs-lookup"><span data-stu-id="e01ea-221">AzureServiceTokenProvider uses Azure AD Integrated Authentication to get token.</span></span> |
| `RunAs=App;` | <span data-ttu-id="e01ea-222">managed identities for Azure resources</span><span class="sxs-lookup"><span data-stu-id="e01ea-222">managed identities for Azure resources</span></span> | <span data-ttu-id="e01ea-223">AzureServiceTokenProvider uses a managed identity to get token.</span><span class="sxs-lookup"><span data-stu-id="e01ea-223">AzureServiceTokenProvider uses a managed identity to get token.</span></span> |
| `RunAs=App;AppId={AppId};TenantId={TenantId};CertificateThumbprint`<br>`   ={Thumbprint};CertificateStoreLocation={LocalMachine or CurrentUser}`  | <span data-ttu-id="e01ea-224">Service principal</span><span class="sxs-lookup"><span data-stu-id="e01ea-224">Service principal</span></span> | <span data-ttu-id="e01ea-225">`AzureServiceTokenProvider` uses certificate to get token from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e01ea-225">`AzureServiceTokenProvider` uses certificate to get token from Azure AD.</span></span> |
| `RunAs=App;AppId={AppId};TenantId={TenantId};`<br>`   CertificateSubjectName={Subject};CertificateStoreLocation=`<br>`   {LocalMachine or CurrentUser}` | <span data-ttu-id="e01ea-226">Service principal</span><span class="sxs-lookup"><span data-stu-id="e01ea-226">Service principal</span></span> | <span data-ttu-id="e01ea-227">`AzureServiceTokenProvider` uses certificate to get token from Azure AD</span><span class="sxs-lookup"><span data-stu-id="e01ea-227">`AzureServiceTokenProvider` uses certificate to get token from Azure AD</span></span>|
| `RunAs=App;AppId={AppId};TenantId={TenantId};AppKey={ClientSecret}` | <span data-ttu-id="e01ea-228">Service principal</span><span class="sxs-lookup"><span data-stu-id="e01ea-228">Service principal</span></span> |<span data-ttu-id="e01ea-229">`AzureServiceTokenProvider` uses secret to get token from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e01ea-229">`AzureServiceTokenProvider` uses secret to get token from Azure AD.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e01ea-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="e01ea-230">Next steps</span></span>

- <span data-ttu-id="e01ea-231">Learn more about [managed identities for Azure resources](/azure/app-service/app-service-managed-service-identity).</span><span class="sxs-lookup"><span data-stu-id="e01ea-231">Learn more about [managed identities for Azure resources](/azure/app-service/app-service-managed-service-identity).</span></span>

- <span data-ttu-id="e01ea-232">Learn different ways to [authenticate and authorize apps](/azure/app-service/app-service-authentication-overview).</span><span class="sxs-lookup"><span data-stu-id="e01ea-232">Learn different ways to [authenticate and authorize apps](/azure/app-service/app-service-authentication-overview).</span></span>

- <span data-ttu-id="e01ea-233">Learn more about Azure AD [authentication scenarios](/azure/active-directory/develop/active-directory-authentication-scenarios#web-browser-to-web-application).</span><span class="sxs-lookup"><span data-stu-id="e01ea-233">Learn more about Azure AD [authentication scenarios](/azure/active-directory/develop/active-directory-authentication-scenarios#web-browser-to-web-application).</span></span>
