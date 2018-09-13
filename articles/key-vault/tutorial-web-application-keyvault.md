---
title: Configure an Azure web application to read a secret from Key vault tutorial | Microsoft Docs
description: Tutorial Configure an ASP.Net core application to read a secret from Key vault
services: key-vault
documentationcenter: ''
author: barclayn
manager: mbaldwin
ms.assetid: 0e57f5c7-6f5a-46b7-a18a-043da8ca0d83
ms.service: key-vault
ms.workload: identity
ms.topic: tutorial
ms.date: 09/05/2018
ms.author: barclayn
ms.custom: mvc
ms.openlocfilehash: c9cf31fc7c9b404c541b2140f6b2489c0eec4281
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857457"
---
# <a name="tutorial-configure-an-azure-web-application-to-read-a-secret-from-key-vault"></a><span data-ttu-id="9b24b-103">Tutorial: Configure an Azure web application to read a secret from Key Vault</span><span class="sxs-lookup"><span data-stu-id="9b24b-103">Tutorial: Configure an Azure web application to read a secret from Key Vault</span></span>

<span data-ttu-id="9b24b-104">In this tutorial, you go over the necessary steps for getting an Azure web application to read information from Key vault using managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9b24b-104">In this tutorial, you go over the necessary steps for getting an Azure web application to read information from Key vault using managed identities for Azure resources.</span></span> <span data-ttu-id="9b24b-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="9b24b-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9b24b-106">Create a Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-106">Create a Key Vault.</span></span>
> * <span data-ttu-id="9b24b-107">Store a secret in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-107">Store a secret in Key Vault.</span></span>
> * <span data-ttu-id="9b24b-108">Create an Azure web Application.</span><span class="sxs-lookup"><span data-stu-id="9b24b-108">Create an Azure web Application.</span></span>
> * <span data-ttu-id="9b24b-109">Enable a managed identity for the web application.</span><span class="sxs-lookup"><span data-stu-id="9b24b-109">Enable a managed identity for the web application.</span></span>
> * <span data-ttu-id="9b24b-110">Grant the required permissions for the application to read data from Key vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-110">Grant the required permissions for the application to read data from Key vault.</span></span>

<span data-ttu-id="9b24b-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9b24b-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9b24b-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="9b24b-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9b24b-113">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="9b24b-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="9b24b-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9b24b-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="9b24b-115">To log in to the Azure using the CLI, you can type:</span><span class="sxs-lookup"><span data-stu-id="9b24b-115">To log in to the Azure using the CLI, you can type:</span></span>

```azurecli
az login
```

## <a name="create-resource-group"></a><span data-ttu-id="9b24b-116">Create resource group</span><span class="sxs-lookup"><span data-stu-id="9b24b-116">Create resource group</span></span>

<span data-ttu-id="9b24b-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="9b24b-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="9b24b-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="9b24b-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="9b24b-119">The following example creates a resource group named *ContosoResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="9b24b-119">The following example creates a resource group named *ContosoResourceGroup* in the *eastus* location.</span></span>

```azurecli
# To list locations: az account list-locations --output table
az group create --name "ContosoResourceGroup" --location "East US"
```

<span data-ttu-id="9b24b-120">The resource group you just created is used throughout this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9b24b-120">The resource group you just created is used throughout this tutorial.</span></span>

## <a name="create-an-azure-key-vault"></a><span data-ttu-id="9b24b-121">Create an Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9b24b-121">Create an Azure Key Vault</span></span>

<span data-ttu-id="9b24b-122">Next you create a Key Vault in the resource group created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9b24b-122">Next you create a Key Vault in the resource group created in the previous step.</span></span> <span data-ttu-id="9b24b-123">Although “ContosoKeyVault” is used as the name for the Key Vault throughout this tutorial, you have to use a unique name.</span><span class="sxs-lookup"><span data-stu-id="9b24b-123">Although “ContosoKeyVault” is used as the name for the Key Vault throughout this tutorial, you have to use a unique name.</span></span> <span data-ttu-id="9b24b-124">Provide the following information:</span><span class="sxs-lookup"><span data-stu-id="9b24b-124">Provide the following information:</span></span>

* <span data-ttu-id="9b24b-125">Vault name **ContosoKeyVault**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-125">Vault name **ContosoKeyVault**.</span></span>
* <span data-ttu-id="9b24b-126">Resource group name **ContosoResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-126">Resource group name **ContosoResourceGroup**.</span></span>
* <span data-ttu-id="9b24b-127">The location **East US**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-127">The location **East US**.</span></span>

```azurecli
az keyvault create --name "ContosoKeyVault" --resource-group "ContosoResourceGroup" --location "East US"
```

<span data-ttu-id="9b24b-128">The output of this command shows properties of the newly created Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-128">The output of this command shows properties of the newly created Key Vault.</span></span> <span data-ttu-id="9b24b-129">Take note of the two properties listed below:</span><span class="sxs-lookup"><span data-stu-id="9b24b-129">Take note of the two properties listed below:</span></span>

* <span data-ttu-id="9b24b-130">**Vault Name**: In the example, this is **ContosoKeyVault**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-130">**Vault Name**: In the example, this is **ContosoKeyVault**.</span></span> <span data-ttu-id="9b24b-131">You will use the name of your Key Vault for all Key Vault commands.</span><span class="sxs-lookup"><span data-stu-id="9b24b-131">You will use the name of your Key Vault for all Key Vault commands.</span></span>
* <span data-ttu-id="9b24b-132">**Vault URI**: In the example, this is https://<YourKeyVaultName>.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="9b24b-132">**Vault URI**: In the example, this is https://<YourKeyVaultName>.vault.azure.net/.</span></span> <span data-ttu-id="9b24b-133">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="9b24b-133">Applications that use your vault through its REST API must use this URI.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9b24b-134">If you get the error Parameter 'vault_name' must conform to the following pattern: '^[a-zA-Z0-9-]{3,24}$' The -name param value was not unique or did not conform to a string composed of alpha-numeric characters from 3 to 24 long.</span><span class="sxs-lookup"><span data-stu-id="9b24b-134">If you get the error Parameter 'vault_name' must conform to the following pattern: '^[a-zA-Z0-9-]{3,24}$' The -name param value was not unique or did not conform to a string composed of alpha-numeric characters from 3 to 24 long.</span></span>

<span data-ttu-id="9b24b-135">At this point, your Azure account is the only one authorized to perform any operations on this new vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-135">At this point, your Azure account is the only one authorized to perform any operations on this new vault.</span></span>

## <a name="add-a-secret-to-key-vault"></a><span data-ttu-id="9b24b-136">Add a secret to key vault</span><span class="sxs-lookup"><span data-stu-id="9b24b-136">Add a secret to key vault</span></span>

<span data-ttu-id="9b24b-137">We're adding a secret to help illustrate how this works.</span><span class="sxs-lookup"><span data-stu-id="9b24b-137">We're adding a secret to help illustrate how this works.</span></span> <span data-ttu-id="9b24b-138">You could be storing a SQL connection string or any other information that you need to keep securely but make available to your application.</span><span class="sxs-lookup"><span data-stu-id="9b24b-138">You could be storing a SQL connection string or any other information that you need to keep securely but make available to your application.</span></span> <span data-ttu-id="9b24b-139">In this tutorial, the password will be called **AppSecret** and will store the value of **MySecret** in it.</span><span class="sxs-lookup"><span data-stu-id="9b24b-139">In this tutorial, the password will be called **AppSecret** and will store the value of **MySecret** in it.</span></span>

<span data-ttu-id="9b24b-140">Type the commands below to create a secret in Key Vault called **AppSecret** that will store the value **MySecret**:</span><span class="sxs-lookup"><span data-stu-id="9b24b-140">Type the commands below to create a secret in Key Vault called **AppSecret** that will store the value **MySecret**:</span></span>

```azurecli
az keyvault secret set --vault-name "ContosoKeyVault" --name "AppSecret" --value "MySecret"
```

<span data-ttu-id="9b24b-141">To view the value contained in the secret as plain text:</span><span class="sxs-lookup"><span data-stu-id="9b24b-141">To view the value contained in the secret as plain text:</span></span>

```azurecli
az keyvault secret show --name "AppSecret" --vault-name "ContosoKeyVault"
```

<span data-ttu-id="9b24b-142">This command shows the secret information including the URI.</span><span class="sxs-lookup"><span data-stu-id="9b24b-142">This command shows the secret information including the URI.</span></span> <span data-ttu-id="9b24b-143">After completing these steps, you should have a URI to a secret in an Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-143">After completing these steps, you should have a URI to a secret in an Azure Key Vault.</span></span> <span data-ttu-id="9b24b-144">Make note of this information.</span><span class="sxs-lookup"><span data-stu-id="9b24b-144">Make note of this information.</span></span> <span data-ttu-id="9b24b-145">You need it in a later step.</span><span class="sxs-lookup"><span data-stu-id="9b24b-145">You need it in a later step.</span></span>

## <a name="create-a-web-app"></a><span data-ttu-id="9b24b-146">Create a web app</span><span class="sxs-lookup"><span data-stu-id="9b24b-146">Create a web app</span></span>

<span data-ttu-id="9b24b-147">In this section you create an ASP.NET MVC application and deploy it in Azure as a Web App.</span><span class="sxs-lookup"><span data-stu-id="9b24b-147">In this section you create an ASP.NET MVC application and deploy it in Azure as a Web App.</span></span> <span data-ttu-id="9b24b-148">For more information about Azure Web Apps, see [Web Apps overview](../app-service/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b24b-148">For more information about Azure Web Apps, see [Web Apps overview](../app-service/app-service-web-overview.md).</span></span>

1. <span data-ttu-id="9b24b-149">In Visual Studio, create a project by selecting **File > New > Project**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-149">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

2. <span data-ttu-id="9b24b-150">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Core Web Application**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-150">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Core Web Application**.</span></span>

3. <span data-ttu-id="9b24b-151">Name the application **WebKeyVault**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-151">Name the application **WebKeyVault**, and then select **OK**.</span></span>
   >[!IMPORTANT]
   > <span data-ttu-id="9b24b-152">You must name the app WebKeyVault so the code you copy and paste will match the namespace.</span><span class="sxs-lookup"><span data-stu-id="9b24b-152">You must name the app WebKeyVault so the code you copy and paste will match the namespace.</span></span> <span data-ttu-id="9b24b-153">If you named the site anything else you will need to modify the code to match the site name.</span><span class="sxs-lookup"><span data-stu-id="9b24b-153">If you named the site anything else you will need to modify the code to match the site name.</span></span>

    ![New ASP.NET Project dialog box](media/tutorial-web-application-keyvault/aspnet-dialog.png)

4. <span data-ttu-id="9b24b-155">You can deploy any type of ASP.NET Core web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="9b24b-155">You can deploy any type of ASP.NET Core web app to Azure.</span></span> <span data-ttu-id="9b24b-156">For this tutorial, select the **Web Application** template, and make sure authentication is set to **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-156">For this tutorial, select the **Web Application** template, and make sure authentication is set to **No Authentication**.</span></span>

    ![ASPNET no authentication dialog box](media/tutorial-web-application-keyvault/aspnet-noauth.png)

5. <span data-ttu-id="9b24b-158">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-158">Select **OK**.</span></span>

6. <span data-ttu-id="9b24b-159">Once the ASP.NET Core project is created, the ASP.NET Core welcome page is displayed, providing numerous links to resources to help you get started.</span><span class="sxs-lookup"><span data-stu-id="9b24b-159">Once the ASP.NET Core project is created, the ASP.NET Core welcome page is displayed, providing numerous links to resources to help you get started.</span></span>

7. <span data-ttu-id="9b24b-160">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span><span class="sxs-lookup"><span data-stu-id="9b24b-160">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

## <a name="modify-the-web-app"></a><span data-ttu-id="9b24b-161">Modify the web app</span><span class="sxs-lookup"><span data-stu-id="9b24b-161">Modify the web app</span></span>

<span data-ttu-id="9b24b-162">There are two NuGet packages that your web application needs to have installed.</span><span class="sxs-lookup"><span data-stu-id="9b24b-162">There are two NuGet packages that your web application needs to have installed.</span></span> <span data-ttu-id="9b24b-163">To install them, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9b24b-163">To install them, follow the steps below:</span></span>

1. <span data-ttu-id="9b24b-164">In solution explorer right-click on your website name.</span><span class="sxs-lookup"><span data-stu-id="9b24b-164">In solution explorer right-click on your website name.</span></span>
2. <span data-ttu-id="9b24b-165">Select **Manage NuGet packages for solution...**</span><span class="sxs-lookup"><span data-stu-id="9b24b-165">Select **Manage NuGet packages for solution...**</span></span>
3. <span data-ttu-id="9b24b-166">Select the check box next to the search box.</span><span class="sxs-lookup"><span data-stu-id="9b24b-166">Select the check box next to the search box.</span></span> <span data-ttu-id="9b24b-167">**Include prerelease**</span><span class="sxs-lookup"><span data-stu-id="9b24b-167">**Include prerelease**</span></span>
4. <span data-ttu-id="9b24b-168">Search for the two NuGet packages listed below and accept for them to be added to your solution:</span><span class="sxs-lookup"><span data-stu-id="9b24b-168">Search for the two NuGet packages listed below and accept for them to be added to your solution:</span></span>

    * <span data-ttu-id="9b24b-169">[Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) - makes it easy to fetch access tokens for Service-to-Azure-Service authentication scenarios.</span><span class="sxs-lookup"><span data-stu-id="9b24b-169">[Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) - makes it easy to fetch access tokens for Service-to-Azure-Service authentication scenarios.</span></span> 
    * <span data-ttu-id="9b24b-170">[Microsoft.Azure.KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) - contains methods for interacting with Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-170">[Microsoft.Azure.KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) - contains methods for interacting with Key Vault.</span></span>

5. <span data-ttu-id="9b24b-171">Use the Solution Explorer to open `Program.cs` and replace the contents of the Program.cs file with the following code.</span><span class="sxs-lookup"><span data-stu-id="9b24b-171">Use the Solution Explorer to open `Program.cs` and replace the contents of the Program.cs file with the following code.</span></span> <span data-ttu-id="9b24b-172">Substitute ```<YourKeyVaultName>``` with the name of your key vault:</span><span class="sxs-lookup"><span data-stu-id="9b24b-172">Substitute ```<YourKeyVaultName>``` with the name of your key vault:</span></span>

    ```csharp
    
    using Microsoft.AspNetCore;
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.Azure.KeyVault;
    using Microsoft.Azure.Services.AppAuthentication;
    using Microsoft.Extensions.Configuration;
    using Microsoft.Extensions.Configuration.AzureKeyVault;
    
    namespace WebKeyVault
    {
       public class Program
       {
           public static void Main(string[] args)
           {
               BuildWebHost(args).Run();
           }

           public static IWebHost BuildWebHost(string[] args) =>
           WebHost.CreateDefaultBuilder(args)
               .ConfigureAppConfiguration((ctx, builder) =>
               {
                   var keyVaultEndpoint = GetKeyVaultEndpoint();
                   if (!string.IsNullOrEmpty(keyVaultEndpoint))
                   {
                       var azureServiceTokenProvider = new AzureServiceTokenProvider();
                       var keyVaultClient = new KeyVaultClient(
                           new KeyVaultClient.AuthenticationCallback(
                               azureServiceTokenProvider.KeyVaultTokenCallback));
                       builder.AddAzureKeyVault(
                           keyVaultEndpoint, keyVaultClient, new DefaultKeyVaultSecretManager());
                   }
               }
            ).UseStartup<Startup>()
             .Build();

           private static string GetKeyVaultEndpoint() => "https://<YourKeyVaultName>.vault.azure.net";
         }
    }
    ```

6. <span data-ttu-id="9b24b-173">Use Solution Explorer to navigate to the **Pages** section and open `About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9b24b-173">Use Solution Explorer to navigate to the **Pages** section and open `About.cshtml`.</span></span> <span data-ttu-id="9b24b-174">Replace the contents of **About.cshtml.cs** with the code below:</span><span class="sxs-lookup"><span data-stu-id="9b24b-174">Replace the contents of **About.cshtml.cs** with the code below:</span></span>

    ```csharp
    
    using Microsoft.AspNetCore.Mvc.RazorPages;
    using Microsoft.Extensions.Configuration;
    
    namespace WebKeyVault.Pages
    {
        public class AboutModel : PageModel
        {
            public AboutModel(IConfiguration configuration)
            {
                _configuration = configuration;
            }
    
            private readonly IConfiguration _configuration = null;
            public string Message { get; set; }
    
            public void OnGet()
            {
                Message = "My key val = " +  _configuration["AppSecret"];
            }
        }
    }
    
    ```

7. <span data-ttu-id="9b24b-175">From the main menu, choose **Debug** > **Start without Debugging**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-175">From the main menu, choose **Debug** > **Start without Debugging**.</span></span> <span data-ttu-id="9b24b-176">When the browser appears, navigate to the **About** page.</span><span class="sxs-lookup"><span data-stu-id="9b24b-176">When the browser appears, navigate to the **About** page.</span></span> <span data-ttu-id="9b24b-177">The value for the AppSecret is displayed.</span><span class="sxs-lookup"><span data-stu-id="9b24b-177">The value for the AppSecret is displayed.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9b24b-178">If you get a HTTP Error 502.5 - Process Failure message</span><span class="sxs-lookup"><span data-stu-id="9b24b-178">If you get a HTTP Error 502.5 - Process Failure message</span></span>
> > <span data-ttu-id="9b24b-179">then verify the name of the Key Vault specified in `Program.cs`</span><span class="sxs-lookup"><span data-stu-id="9b24b-179">then verify the name of the Key Vault specified in `Program.cs`</span></span>

## <a name="publish-the-web-application-to-azure"></a><span data-ttu-id="9b24b-180">Publish the web application to Azure</span><span class="sxs-lookup"><span data-stu-id="9b24b-180">Publish the web application to Azure</span></span>

1. <span data-ttu-id="9b24b-181">Above the editor, select **WebKeyVault**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-181">Above the editor, select **WebKeyVault**.</span></span>
2. <span data-ttu-id="9b24b-182">Select **Publish** then **Start**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-182">Select **Publish** then **Start**.</span></span>
3. <span data-ttu-id="9b24b-183">Create a new **App Service**, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-183">Create a new **App Service**, select **Publish**.</span></span>
4. <span data-ttu-id="9b24b-184">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-184">Select **Create**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9b24b-185">A browser window opens and you will see a 502.5 - Process Failure message.</span><span class="sxs-lookup"><span data-stu-id="9b24b-185">A browser window opens and you will see a 502.5 - Process Failure message.</span></span> <span data-ttu-id="9b24b-186">This is expected.</span><span class="sxs-lookup"><span data-stu-id="9b24b-186">This is expected.</span></span> <span data-ttu-id="9b24b-187">You will need to grant the application identity rights to read secrets from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-187">You will need to grant the application identity rights to read secrets from Key Vault.</span></span>

## <a name="enable-a-managed-identity-for-the-web-app"></a><span data-ttu-id="9b24b-188">Enable a managed identity for the web app</span><span class="sxs-lookup"><span data-stu-id="9b24b-188">Enable a managed identity for the web app</span></span>

<span data-ttu-id="9b24b-189">Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Key Vault to retrieve them.</span><span class="sxs-lookup"><span data-stu-id="9b24b-189">Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Key Vault to retrieve them.</span></span> <span data-ttu-id="9b24b-190">[Managed identities for Azure resources overview](../active-directory/managed-identities-azure-resources/overview.md) makes solving this problem simpler, by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b24b-190">[Managed identities for Azure resources overview](../active-directory/managed-identities-azure-resources/overview.md) makes solving this problem simpler, by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9b24b-191">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="9b24b-191">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span></span>

1. <span data-ttu-id="9b24b-192">Return to the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b24b-192">Return to the Azure CLI</span></span>
2. <span data-ttu-id="9b24b-193">Run the assign-identity command to create the identity for this application:</span><span class="sxs-lookup"><span data-stu-id="9b24b-193">Run the assign-identity command to create the identity for this application:</span></span>

```azurecli
az webapp identity assign --name "WebKeyVault" --resource-group "ContosoResourcegroup"
```

>[!NOTE]
><span data-ttu-id="9b24b-194">This command is the equivalent of going to the portal and switching the **Identity / System assigned** setting to **On** in the web application properties.</span><span class="sxs-lookup"><span data-stu-id="9b24b-194">This command is the equivalent of going to the portal and switching the **Identity / System assigned** setting to **On** in the web application properties.</span></span>

## <a name="grant-rights-to-the-application-identity"></a><span data-ttu-id="9b24b-195">Grant rights to the application identity</span><span class="sxs-lookup"><span data-stu-id="9b24b-195">Grant rights to the application identity</span></span>

<span data-ttu-id="9b24b-196">Using the Azure portal, go to the Key Vault's access policies, and grant yourself Secret Management access to the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-196">Using the Azure portal, go to the Key Vault's access policies, and grant yourself Secret Management access to the Key Vault.</span></span> <span data-ttu-id="9b24b-197">This will allow you to run the application on your local development machine.</span><span class="sxs-lookup"><span data-stu-id="9b24b-197">This will allow you to run the application on your local development machine.</span></span>

1. <span data-ttu-id="9b24b-198">Search for your Key Vault in the **Search Resources** dialog box in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9b24b-198">Search for your Key Vault in the **Search Resources** dialog box in the Azure portal.</span></span>
2. <span data-ttu-id="9b24b-199">Select **Access policies**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-199">Select **Access policies**.</span></span>
3. <span data-ttu-id="9b24b-200">Select **Add New**, in the **Secret permissions** section select **Get** and **List**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-200">Select **Add New**, in the **Secret permissions** section select **Get** and **List**.</span></span>
4. <span data-ttu-id="9b24b-201">Select **Select Principal**, and add the application identity.</span><span class="sxs-lookup"><span data-stu-id="9b24b-201">Select **Select Principal**, and add the application identity.</span></span> <span data-ttu-id="9b24b-202">It will have the same name as the application.</span><span class="sxs-lookup"><span data-stu-id="9b24b-202">It will have the same name as the application.</span></span>
5. <span data-ttu-id="9b24b-203">Choose **Ok**.</span><span class="sxs-lookup"><span data-stu-id="9b24b-203">Choose **Ok**.</span></span>

<span data-ttu-id="9b24b-204">Now your account in Azure and the application identity have rights to read information from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-204">Now your account in Azure and the application identity have rights to read information from Key Vault.</span></span> <span data-ttu-id="9b24b-205">When you refresh the page, you should see the landing page of the site.</span><span class="sxs-lookup"><span data-stu-id="9b24b-205">When you refresh the page, you should see the landing page of the site.</span></span> <span data-ttu-id="9b24b-206">If you select **About**, you see the value you stored in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9b24b-206">If you select **About**, you see the value you stored in Key Vault.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9b24b-207">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9b24b-207">Clean up resources</span></span>

<span data-ttu-id="9b24b-208">To delete a resource group and all its resources, use the **az group delete** command.</span><span class="sxs-lookup"><span data-stu-id="9b24b-208">To delete a resource group and all its resources, use the **az group delete** command.</span></span>

  ```azurecli
  az group delete -n "ContosoResourceGroup"
  ```

## <a name="next-steps"></a><span data-ttu-id="9b24b-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b24b-209">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9b24b-210">Azure Key Vault Developer's Guide</span><span class="sxs-lookup"><span data-stu-id="9b24b-210">Azure Key Vault Developer's Guide</span></span>](key-vault-developers-guide.md)