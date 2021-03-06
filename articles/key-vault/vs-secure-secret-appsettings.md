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
# <a name="securely-save-secret-application-settings-for-a-web-application"></a>Securely save secret application settings for a web application

## <a name="overview"></a>Overview
This article describes how to securely save secret application configuration settings for Azure applications.

Traditionally all web application configuration settings are saved in configuration files such as Web.config. This practice leads to checking in secret settings such as Cloud credentials to public source control systems like Github. Meanwhile, it could be hard to follow security best practice because of the overhead required to change source code and reconfigure development settings.

To make sure development process is secure, tooling and framework libraries are created to save application secret settings securely with minimal or no source code change.

## <a name="aspnet-and-net-core-applications"></a>ASP.NET and .NET core applications

### <a name="save-secret-settings-in-user-secret-store-that-is-outside-of-source-control-folder"></a>Save secret settings in User Secret store that is outside of source control folder
If you are doing a quick prototype or you don't have internet access, start with moving your secret settings outside of source control folder to User Secret store. User Secret store is a file saved under user profiler folder, so secrets are not checked in to source control. The following diagram demonstrates how [User Secret](https://docs.microsoft.com/aspnet/core/security/app-secrets?tabs=visual-studio#SecretManager) works.

![User Secret keeps secret settings outside of source control](./media/vs-secure-secret-appsettings/aspnetcore-usersecret.PNG)

If you are running .NET core console application, use Key Vault to save your secret securely.

### <a name="save-secret-settings-in-azure-key-vault"></a>Save secret settings in Azure Key Vault
If you are developing a project and need to share source code securely, use [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

1. Create a Key Vault in your Azure subscription. Fill out all required fields on the UI and click *Create* on the bottom of the blade

    ![Create Azure Key Vault](./media/vs-secure-secret-appsettings/create-keyvault.PNG)

2. Grant you and your team members access to the Key Vault. If you have a large team, you can create an [Azure Active Directory group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal) and add that security group access to the Key Vault. In the *Secret Permissions* dropdown, check *Get* and *List* under *Secret Management Operations*.

    ![Add Key Vault access policy](./media/vs-secure-secret-appsettings/add-keyvault-access-policy.png)

3. Add your secret to Key Vault on Azure portal. For nested configuration settings, replace ':' with '--' so the Key Vault secret name is valid. ':' is not allowed to be in the name of a Key Vault secret.

    ![Add Key Vault secret](./media/vs-secure-secret-appsettings/add-keyvault-secret.png)

4. Install the [Azure Services Authentication extension for Visual Studio](https://go.microsoft.com/fwlink/?linkid=862354). Through this extension, app can access Key Vault using the Visual Studio sign-in identity.

5. Add the following NuGet packages to your project:

    ```
    Microsoft.Azure.Services.AppAuthentication
    ```
6. Add the following code to Program.cs file:

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
7. Add your Key Vault URL to launchsettings.json file. The environment variable name *KEYVAULT_ENDPOINT* is defined in the code you added in step 6.

    ![Add Key Vault URL as a project environment variable](./media/vs-secure-secret-appsettings/add-keyvault-url.png)

8. Start debugging the project. It should run successfully.

## <a name="aspnet-and-net-applications"></a>ASP.NET and .NET applications

.NET 4.7.1 supports Key Vault and Secret configuration builders, which ensures secrets can be moved outside of source control folder without code changes.
To proceed, [download .NET 4.7.1](https://www.microsoft.com/download/details.aspx?id=56115) and migrate your application if it's using an older version of .NET framework.

### <a name="save-secret-settings-in-a-secret-file-that-is-outside-of-source-control-folder"></a>Save secret settings in a secret file that is outside of source control folder
If you are writing a quick prototype and don't want to provision Azure resources, go with this option.

1. Install the following NuGet package to your project
    ```
    Microsoft.Configuration.ConfigurationBuilders.Basic.1.0.0-alpha1.nupkg
    ```

2. Create a file that's similar to the follow. Save it under a location outside of your project folder.

    ```xml

       <root>
              <secrets ver="1.0">
                     <secret name="secret1" value="foo_one" />
                        <secret name="secret2" value="foo_two" />
                       </secrets>
      </root>
      ```

3. Define the secret file to be a configuration builder in your Web.config file. Put this section before *appSettings* section.

    ```xml
    <configBuilders>
        <builders>
            <add name="Secrets"
                 secretsFile="C:\Users\AppData\MyWebApplication1\secret.xml" type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
                    Microsoft.Configuration.ConfigurationBuilders, Version=1.0.0.0, Culture=neutral" />
        </builders>
    </configBuilders>
    ```

4. Specify appSettings section is using the secret configuration builder. Make sure there is any entry for the secret setting with a dummy value.

    ```xml
        <appSettings configBuilders="Secrets">
            <add key="webpages:Version" value="3.0.0.0" />
            <add key="webpages:Enabled" value="false" />
            <add key="ClientValidationEnabled" value="true" />
            <add key="UnobtrusiveJavaScriptEnabled" value="true" />
            <add key="secret" value="" />
        </appSettings>
    ```

5. Debug your app. It should run successfully.

### <a name="save-secret-settings-in-an-azure-key-vault"></a>Save secret settings in an Azure Key Vault
Follow instructions from ASP.NET core section to configure a Key Vault for your project.

1. Install the following NuGet package to your project
```
Microsoft.Configuration.ConfigurationBuilders.UserSecrets.1.0.0-preview2.nupkg
```

2. Define Key Vault configuration builder in Web.config. Put this section before *appSettings* section. Replace *vaultName* to be the Key Vault name if your Key Vault is in public Azure, or full URI if you are using Sovereign cloud.

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
3.  Specify appSettings section is using the Key Vault configuration builder. Make sure there is any entry for the secret setting with a dummy value.

    ```xml
    <appSettings configBuilders="AzureKeyVault">
        <add key="webpages:Version" value="3.0.0.0" />
        <add key="webpages:Enabled" value="false" />
        <add key="ClientValidationEnabled" value="true" />
        <add key="UnobtrusiveJavaScriptEnabled" value="true" />
        <add key="secret" value="" />
    </appSettings>
    ```

4. Start debugging the project. It should run successfully.
