---
title: Securely saving secret application settings for a web application | Microsoft Docs
description: How to securely save secret application settings such as Azure credentials or third party API keys using ASP.NET core Key Vault Provider, User Secret, or .NET 4.7.1 configuration builders
services: visualstudio
documentationcenter: ''
author: cawa
manager: paulyuk
editor: ''
ms.assetid: ''
ms.service: ''
ms.workload: web, azure
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: conceptual
ms.date: 11/09/2017
ms.author: cawa
ms.openlocfilehash: 753c48665bb3b0e59928b114860e89a9b7d10eae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869757"
---
# <a name="securely-save-secret-application-settings-for-a-web-application"></a><span data-ttu-id="7da5e-103">Securely save secret application settings for a web application</span><span class="sxs-lookup"><span data-stu-id="7da5e-103">Securely save secret application settings for a web application</span></span>

## <a name="overview"></a><span data-ttu-id="7da5e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7da5e-104">Overview</span></span>
<span data-ttu-id="7da5e-105">This article describes how to securely save secret application configuration settings for Azure applications.</span><span class="sxs-lookup"><span data-stu-id="7da5e-105">This article describes how to securely save secret application configuration settings for Azure applications.</span></span>

<span data-ttu-id="7da5e-106">Traditionally all web application configuration settings are saved in configuration files such as Web.config. This practice leads to checking in secret settings such as Cloud credentials to public source control systems like Github.</span><span class="sxs-lookup"><span data-stu-id="7da5e-106">Traditionally all web application configuration settings are saved in configuration files such as Web.config. This practice leads to checking in secret settings such as Cloud credentials to public source control systems like Github.</span></span> <span data-ttu-id="7da5e-107">Meanwhile, it could be hard to follow security best practice because of the overhead required to change source code and reconfigure development settings.</span><span class="sxs-lookup"><span data-stu-id="7da5e-107">Meanwhile, it could be hard to follow security best practice because of the overhead required to change source code and reconfigure development settings.</span></span>

<span data-ttu-id="7da5e-108">To make sure development process is secure, tooling and framework libraries are created to save application secret settings securely with minimal or no source code change.</span><span class="sxs-lookup"><span data-stu-id="7da5e-108">To make sure development process is secure, tooling and framework libraries are created to save application secret settings securely with minimal or no source code change.</span></span>

## <a name="aspnet-and-net-core-applications"></a><span data-ttu-id="7da5e-109">ASP.NET and .NET core applications</span><span class="sxs-lookup"><span data-stu-id="7da5e-109">ASP.NET and .NET core applications</span></span>

### <a name="save-secret-settings-in-user-secret-store-that-is-outside-of-source-control-folder"></a><span data-ttu-id="7da5e-110">Save secret settings in User Secret store that is outside of source control folder</span><span class="sxs-lookup"><span data-stu-id="7da5e-110">Save secret settings in User Secret store that is outside of source control folder</span></span>
<span data-ttu-id="7da5e-111">If you are doing a quick prototype or you don't have internet access, start with moving your secret settings outside of source control folder to User Secret store.</span><span class="sxs-lookup"><span data-stu-id="7da5e-111">If you are doing a quick prototype or you don't have internet access, start with moving your secret settings outside of source control folder to User Secret store.</span></span> <span data-ttu-id="7da5e-112">User Secret store is a file saved under user profiler folder, so secrets are not checked in to source control.</span><span class="sxs-lookup"><span data-stu-id="7da5e-112">User Secret store is a file saved under user profiler folder, so secrets are not checked in to source control.</span></span> <span data-ttu-id="7da5e-113">The following diagram demonstrates how [User Secret](https://docs.microsoft.com/aspnet/core/security/app-secrets?tabs=visual-studio#SecretManager) works.</span><span class="sxs-lookup"><span data-stu-id="7da5e-113">The following diagram demonstrates how [User Secret](https://docs.microsoft.com/aspnet/core/security/app-secrets?tabs=visual-studio#SecretManager) works.</span></span>

![User Secret keeps secret settings outside of source control](./media/vs-secure-secret-appsettings/aspnetcore-usersecret.PNG)

<span data-ttu-id="7da5e-115">If you are running .NET core console application, use Key Vault to save your secret securely.</span><span class="sxs-lookup"><span data-stu-id="7da5e-115">If you are running .NET core console application, use Key Vault to save your secret securely.</span></span>

### <a name="save-secret-settings-in-azure-key-vault"></a><span data-ttu-id="7da5e-116">Save secret settings in Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="7da5e-116">Save secret settings in Azure Key Vault</span></span>
<span data-ttu-id="7da5e-117">If you are developing a project and need to share source code securely, use [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="7da5e-117">If you are developing a project and need to share source code securely, use [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span></span>

1. <span data-ttu-id="7da5e-118">Create a Key Vault in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7da5e-118">Create a Key Vault in your Azure subscription.</span></span> <span data-ttu-id="7da5e-119">Fill out all required fields on the UI and click *Create* on the bottom of the blade</span><span class="sxs-lookup"><span data-stu-id="7da5e-119">Fill out all required fields on the UI and click *Create* on the bottom of the blade</span></span>

    ![Create Azure Key Vault](./media/vs-secure-secret-appsettings/create-keyvault.PNG)

2. <span data-ttu-id="7da5e-121">Grant you and your team members access to the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7da5e-121">Grant you and your team members access to the Key Vault.</span></span> <span data-ttu-id="7da5e-122">If you have a large team, you can create an [Azure Active Directory group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal) and add that security group access to the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7da5e-122">If you have a large team, you can create an [Azure Active Directory group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal) and add that security group access to the Key Vault.</span></span> <span data-ttu-id="7da5e-123">In the *Secret Permissions* dropdown, check *Get* and *List* under *Secret Management Operations*.</span><span class="sxs-lookup"><span data-stu-id="7da5e-123">In the *Secret Permissions* dropdown, check *Get* and *List* under *Secret Management Operations*.</span></span>

    ![Add Key Vault access policy](./media/vs-secure-secret-appsettings/add-keyvault-access-policy.png)

3. <span data-ttu-id="7da5e-125">Add your secret to Key Vault on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7da5e-125">Add your secret to Key Vault on Azure portal.</span></span> <span data-ttu-id="7da5e-126">For nested configuration settings, replace ':' with '--' so the Key Vault secret name is valid.</span><span class="sxs-lookup"><span data-stu-id="7da5e-126">For nested configuration settings, replace ':' with '--' so the Key Vault secret name is valid.</span></span> <span data-ttu-id="7da5e-127">':' is not allowed to be in the name of a Key Vault secret.</span><span class="sxs-lookup"><span data-stu-id="7da5e-127">':' is not allowed to be in the name of a Key Vault secret.</span></span>

    ![Add Key Vault secret](./media/vs-secure-secret-appsettings/add-keyvault-secret.png)

4. <span data-ttu-id="7da5e-129">Install the [Azure Services Authentication extension for Visual Studio](https://go.microsoft.com/fwlink/?linkid=862354).</span><span class="sxs-lookup"><span data-stu-id="7da5e-129">Install the [Azure Services Authentication extension for Visual Studio](https://go.microsoft.com/fwlink/?linkid=862354).</span></span> <span data-ttu-id="7da5e-130">Through this extension, app can access Key Vault using the Visual Studio sign-in identity.</span><span class="sxs-lookup"><span data-stu-id="7da5e-130">Through this extension, app can access Key Vault using the Visual Studio sign-in identity.</span></span>

5. <span data-ttu-id="7da5e-131">Add the following NuGet packages to your project:</span><span class="sxs-lookup"><span data-stu-id="7da5e-131">Add the following NuGet packages to your project:</span></span>

    ```
    Microsoft.Azure.Services.AppAuthentication
    ```
6. <span data-ttu-id="7da5e-132">Add the following code to Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="7da5e-132">Add the following code to Program.cs file:</span></span>

    ```csharp
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
                    })
                    .UseStartup<Startup>()
                    .Build();

        private static string GetKeyVaultEndpoint() => Environment.GetEnvironmentVariable("KEYVAULT_ENDPOINT");
    ```
7. <span data-ttu-id="7da5e-133">Add your Key Vault URL to launchsettings.json file.</span><span class="sxs-lookup"><span data-stu-id="7da5e-133">Add your Key Vault URL to launchsettings.json file.</span></span> <span data-ttu-id="7da5e-134">The environment variable name *KEYVAULT_ENDPOINT* is defined in the code you added in step 6.</span><span class="sxs-lookup"><span data-stu-id="7da5e-134">The environment variable name *KEYVAULT_ENDPOINT* is defined in the code you added in step 6.</span></span>

    ![Add Key Vault URL as a project environment variable](./media/vs-secure-secret-appsettings/add-keyvault-url.png)

8. <span data-ttu-id="7da5e-136">Start debugging the project.</span><span class="sxs-lookup"><span data-stu-id="7da5e-136">Start debugging the project.</span></span> <span data-ttu-id="7da5e-137">It should run successfully.</span><span class="sxs-lookup"><span data-stu-id="7da5e-137">It should run successfully.</span></span>

## <a name="aspnet-and-net-applications"></a><span data-ttu-id="7da5e-138">ASP.NET and .NET applications</span><span class="sxs-lookup"><span data-stu-id="7da5e-138">ASP.NET and .NET applications</span></span>

<span data-ttu-id="7da5e-139">.NET 4.7.1 supports Key Vault and Secret configuration builders, which ensures secrets can be moved outside of source control folder without code changes.</span><span class="sxs-lookup"><span data-stu-id="7da5e-139">.NET 4.7.1 supports Key Vault and Secret configuration builders, which ensures secrets can be moved outside of source control folder without code changes.</span></span>
<span data-ttu-id="7da5e-140">To proceed, [download .NET 4.7.1](https://www.microsoft.com/download/details.aspx?id=56115) and migrate your application if it's using an older version of .NET framework.</span><span class="sxs-lookup"><span data-stu-id="7da5e-140">To proceed, [download .NET 4.7.1](https://www.microsoft.com/download/details.aspx?id=56115) and migrate your application if it's using an older version of .NET framework.</span></span>

### <a name="save-secret-settings-in-a-secret-file-that-is-outside-of-source-control-folder"></a><span data-ttu-id="7da5e-141">Save secret settings in a secret file that is outside of source control folder</span><span class="sxs-lookup"><span data-stu-id="7da5e-141">Save secret settings in a secret file that is outside of source control folder</span></span>
<span data-ttu-id="7da5e-142">If you are writing a quick prototype and don't want to provision Azure resources, go with this option.</span><span class="sxs-lookup"><span data-stu-id="7da5e-142">If you are writing a quick prototype and don't want to provision Azure resources, go with this option.</span></span>

1. <span data-ttu-id="7da5e-143">Install the following NuGet package to your project</span><span class="sxs-lookup"><span data-stu-id="7da5e-143">Install the following NuGet package to your project</span></span>
    ```
    Microsoft.Configuration.ConfigurationBuilders.Basic.1.0.0-alpha1.nupkg
    ```

2. <span data-ttu-id="7da5e-144">Create a file that's similar to the follow.</span><span class="sxs-lookup"><span data-stu-id="7da5e-144">Create a file that's similar to the follow.</span></span> <span data-ttu-id="7da5e-145">Save it under a location outside of your project folder.</span><span class="sxs-lookup"><span data-stu-id="7da5e-145">Save it under a location outside of your project folder.</span></span>

    ```xml

       <root>
              <secrets ver="1.0">
                     <secret name="secret1" value="foo_one" />
                        <secret name="secret2" value="foo_two" />
                       </secrets>
      </root>
      ```

3. <span data-ttu-id="7da5e-146">Define the secret file to be a configuration builder in your Web.config file.</span><span class="sxs-lookup"><span data-stu-id="7da5e-146">Define the secret file to be a configuration builder in your Web.config file.</span></span> <span data-ttu-id="7da5e-147">Put this section before *appSettings* section.</span><span class="sxs-lookup"><span data-stu-id="7da5e-147">Put this section before *appSettings* section.</span></span>

    ```xml
    <configBuilders>
        <builders>
            <add name="Secrets"
                 secretsFile="C:\Users\AppData\MyWebApplication1\secret.xml" type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
                    Microsoft.Configuration.ConfigurationBuilders, Version=1.0.0.0, Culture=neutral" />
        </builders>
    </configBuilders>
    ```

4. <span data-ttu-id="7da5e-148">Specify appSettings section is using the secret configuration builder.</span><span class="sxs-lookup"><span data-stu-id="7da5e-148">Specify appSettings section is using the secret configuration builder.</span></span> <span data-ttu-id="7da5e-149">Make sure there is any entry for the secret setting with a dummy value.</span><span class="sxs-lookup"><span data-stu-id="7da5e-149">Make sure there is any entry for the secret setting with a dummy value.</span></span>

    ```xml
        <appSettings configBuilders="Secrets">
            <add key="webpages:Version" value="3.0.0.0" />
            <add key="webpages:Enabled" value="false" />
            <add key="ClientValidationEnabled" value="true" />
            <add key="UnobtrusiveJavaScriptEnabled" value="true" />
            <add key="secret" value="" />
        </appSettings>
    ```

5. <span data-ttu-id="7da5e-150">Debug your app.</span><span class="sxs-lookup"><span data-stu-id="7da5e-150">Debug your app.</span></span> <span data-ttu-id="7da5e-151">It should run successfully.</span><span class="sxs-lookup"><span data-stu-id="7da5e-151">It should run successfully.</span></span>

### <a name="save-secret-settings-in-an-azure-key-vault"></a><span data-ttu-id="7da5e-152">Save secret settings in an Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="7da5e-152">Save secret settings in an Azure Key Vault</span></span>
<span data-ttu-id="7da5e-153">Follow instructions from ASP.NET core section to configure a Key Vault for your project.</span><span class="sxs-lookup"><span data-stu-id="7da5e-153">Follow instructions from ASP.NET core section to configure a Key Vault for your project.</span></span>

1. <span data-ttu-id="7da5e-154">Install the following NuGet package to your project</span><span class="sxs-lookup"><span data-stu-id="7da5e-154">Install the following NuGet package to your project</span></span>
```
Microsoft.Configuration.ConfigurationBuilders.UserSecrets.1.0.0-preview2.nupkg
```

2. <span data-ttu-id="7da5e-155">Define Key Vault configuration builder in Web.config. Put this section before *appSettings* section.</span><span class="sxs-lookup"><span data-stu-id="7da5e-155">Define Key Vault configuration builder in Web.config. Put this section before *appSettings* section.</span></span> <span data-ttu-id="7da5e-156">Replace *vaultName* to be the Key Vault name if your Key Vault is in public Azure, or full URI if you are using Sovereign cloud.</span><span class="sxs-lookup"><span data-stu-id="7da5e-156">Replace *vaultName* to be the Key Vault name if your Key Vault is in public Azure, or full URI if you are using Sovereign cloud.</span></span>

    ```xml
    <configSections>
        <section name="configBuilders" type="System.Configuration.ConfigurationBuildersSection, System.Configuration, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" restartOnExternalChanges="false" requirePermission="false" />
    </configSections>
    <configBuilders>
        <builders>
            <add name="AzureKeyVault" vaultName="Test911" type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder, ConfigurationBuilders, Version=1.0.0.0, Culture=neutral" />
        </builders>
    </configBuilders>
    ```
3.  <span data-ttu-id="7da5e-157">Specify appSettings section is using the Key Vault configuration builder.</span><span class="sxs-lookup"><span data-stu-id="7da5e-157">Specify appSettings section is using the Key Vault configuration builder.</span></span> <span data-ttu-id="7da5e-158">Make sure there is any entry for the secret setting with a dummy value.</span><span class="sxs-lookup"><span data-stu-id="7da5e-158">Make sure there is any entry for the secret setting with a dummy value.</span></span>

    ```xml
    <appSettings configBuilders="AzureKeyVault">
        <add key="webpages:Version" value="3.0.0.0" />
        <add key="webpages:Enabled" value="false" />
        <add key="ClientValidationEnabled" value="true" />
        <add key="UnobtrusiveJavaScriptEnabled" value="true" />
        <add key="secret" value="" />
    </appSettings>
    ```

4. <span data-ttu-id="7da5e-159">Start debugging the project.</span><span class="sxs-lookup"><span data-stu-id="7da5e-159">Start debugging the project.</span></span> <span data-ttu-id="7da5e-160">It should run successfully.</span><span class="sxs-lookup"><span data-stu-id="7da5e-160">It should run successfully.</span></span>
