---
title: Configure Azure Function App Settings | Microsoft Docs
description: Learn how to configure Azure function app settings.
services: ''
documentationcenter: .net
author: rachelappel
manager: erikre
editor: ''
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: rachelap
ms.openlocfilehash: a54d298132d47e9ecf83e9e263a92d088ffc2e9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553390"
---
# <a name="how-to-configure-azure-function-app-settings"></a>How to configure Azure Function app settings
## <a name="settings-overview"></a>Settings overview
You can manage Azure Function Apps settings by clicking the **Function App Settings** link in the bottom-left corner of the portal. Azure function app settings apply to all functions in the app.

1. Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.
2. Click **Function App Settings** in the bottom-left corner of the portal. This action reveals several configuration options to choose from. 

![Azure Function App settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="develop"></a>Develop
### <a name="app-service-editor"></a>App Service Editor
The App Service Editor is an advanced in-portal editor that you can use to modify Json configuration files and code files alike. Choosing this option launches a separate browser tab with a basic editor. This enables you to integrate with GitHub, run and debug code, and modify function app settings.

![The App Service Editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="application-settings"></a>Application settings
Manage environment variables, Framework versions, remote debugging, app settings, connection strings, default docs, etc. These settings are specific to your Function App. 

To configure app settings, click the **Configure App Settings** link. 

![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="dev-console"></a>Dev console
You can execute DOS style commands with the Azure functions in-portal console. Common commands include directory and file creation and navigation, as well as executing batch files and scripts. 

> [!NOTE]
> You can upload scripts, but first you must configure an FTP client in the Azure Function's **Advanced Settings**.
> 
> 

To open the In-portal console, click **Open dev console**.

![Configure function app memory size](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

> [!NOTE]
> Working in a console with ASCII art like that makes you look cool.
> 
> 

## <a name="deploy"></a>Deploy
### <a name="continuous-integration"></a>Continuous integration
You can integrate your Function App with GitHub, Visual Studio Team Services, and more.

1. Click the  **Configure continuous integration** link. This  opens a **Deployments** pane with options.
2. Click **Setup** in the **Deployments** pane to reveal a **Deployment Source** pane with one option: Click **Choose Source** to show available sources. 
3. Choose any of the deployment sources available: Visual Studio Team Services, OneDrive, Local Git Repository, GitHub, Bitbucket, DropBox, or an External Repository by clicking it. 
   
    ![Configure Function App's CI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-ci.png)
4. Enter your credentials and information as prompted by the various deployment sources. The credentials and information requested may be slightly different depending on what source you have chosen. 

Once you have setup CI, connected code you push to the configured source is automatically deployed to this function app.

### <a name="kudu"></a>Kudu
Kudu allows you to access advanced administrative features of a Function App.

To open Kudu, click **Go to Kudu**. This action opens an entirely new browser window with the Kudu web admin.

> [!NOTE]
> You can alternatively launch **Kudu** by inserting "scm" into your function's URL, as shown here: ```https://<YourFunctionName>.scm.azurewebsites.net/```
> 
> 

From the Kudu webpage, you can view and manage system information, app settings, environment variables, HTTP headers, server variables, and more.

![Configure Kudu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)

## <a name="manage-app-service-settings"></a>Manage: App Service settings
Manage your function app like any other App Service instance. This option gives you access to all the previously discussed settings, plus several more.  

To open advanced settings, click the **Advanced Settings** link. 

![Configure App Service Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-settings.png)

For details on how to configure each App Service setting, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).

## <a name="manage-cors"></a>Manage: CORS
Normally, for security reasons, calls to your hosts (domains) from external sources, such as Ajax calls from a browser, are not allowed. Otherwise, malicious code could be sent to and executed on the backend. The safest route then is to blacklist all sources of code, except for a few of your own trusted ones. You can configure which sources you accept calls from in Azure functions by configuring Cross-Origin Resource Sharing (CORS). CORS allows you to list domains that are the source of JavaScript that can call functions in your Azure Function App. 

1. To configure CORS, click the **Configure CORS** link. 
2. Enter the domains that you want to whitelist.

![Configure Function App's CORS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

## <a name="manage-authenticationauthorization"></a>Manage: Authentication/authorization
For functions that use an HTTP trigger, you can require calls to be authenticated.

1. To configure authentication click the **Configure authentication** link.
2. Toggle the **App Service Authentication** button to **On**.

![Configure Function App's CI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)

Most authentication providers ask for an API Key/Client ID and a Secret; however, both the Microsoft Account and Facebook options also allow you to define scopes (specific authorization credentials). Active Directory has several express or advanced configuration settings you can set.

For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).

## <a name="manage-api-definition"></a>Manage: API definition
Allow clients to more easily consume your HTTP-triggered functions.

1. To set up an API, click **Configure API metadata**. 
2. Enter the URL that points to a Swagger json file.

![Configure Function App's API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)

For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).

## <a name="daily-usage-quota"></a>Daily Usage Quota

Azure Functions enables you to predictably limit platform usage by setting a daily spending quota. Once the daily spending quota is reached the Function App is stopped. A Function App stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota. The unit of the spending quota is the unit of billing: GB-s (gigabyte-seconds), please refer to the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on the billing model. 

![Configure function app memory size](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-quota.png)

## <a name="next-steps"></a>Next steps
[!INCLUDE [Getting Started Note](../../includes/functions-get-help.md)]












