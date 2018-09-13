---
title: Continuous deployment for Azure Functions | Microsoft Docs
description: Use continuous deployment facilities of Azure App Service to publish your Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: f385bffcb7567a7dd57821a4b32403b1005e745d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551139"
---
# <a name="continuous-deployment-for-azure-functions"></a>Continuous deployment for Azure Functions
Azure Functions makes it easy to configure continuous deployment for your function app. Functions uses Azure App Service integration with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS) to enable a continuous deployment workflow where Azure pulls updates to your functions code when they are published to one of these services. If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).

Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated. It also lets you maintain source control on your functions code. The following deployment sources are currently supported:

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* [Git local repo](../app-service-web/app-service-deploy-local-git.md)
* Git external repo
* [GitHub]
* Mercurial external repo
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

Deployments are configured on a per-function-app basis. After continuous deployment is enabled, access to function code in the portal is set to *read-only*.

## <a name="continuous-deployment-requirements"></a>Continuous deployment requirements

You must have your deployment source configured and your functions code in the deployment source before you set-up continuous deployment. In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function. This folder structure is essentially your site code. 

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Set up continuous deployment
Use the following procedure to configure continuous deployment for an existing function app:

1. In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Configure continuous integration** > **Setup**.
   
    ![Setup continuous deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/setup-deployment.png)
   
    ![Setup continuous deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/setup-deployment-1.png)
   
    You can also get to the Deployments blade from the Functions quickstart by clicking **Start from source control**.
2. In the **Deployment source** blade, click **Choose source**, then fill-in the information for your chosen deployment source and click **OK**.
   
    ![Choose deployment source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/choose-deployment-source.png)

After continuous deployment is configured, all changes files in your deployment source are copied to the function app and a full site deployment is triggered. The site is redeployed when files in the source are updated.

## <a name="deployment-options"></a>Deployment options

The following are some typical deployment scenarios:

- [Create a staging deployment](#staging)
- [Move existing functions to continuous deployment](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Create a staging deployment

Function Apps doesn't yet support deployment slots. However, you can still manage separate staging and production deployments by using continuous integration.

The process to configure and work with a staging deployment looks generally like this:

1. Create two function apps in your subscription, one for the production code and one for staging. 

2. Create a deployment source, if you don't already have one. This example uses [GitHub].

3. For your production function app, complete the above steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repo.
   
    ![Choose deployment branch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/choose-deployment-branch.png)

4. Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo. If your deployment source doesn't support branching, use a different folder.

5. Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.

6. After testing, merge changes from the staging branch into the master branch. This will trigger deployment to the production function app. If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a>Move existing functions to continuous deployment
When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above. You can do this in the App Service settings for your function app. After your files are downloaded, you can upload them to your chosen continuous deployment source.

> [!NOTE]
> After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.

- [How to: Configure deployment credentials](#credentials)
- [How to: Download files using FTP](#downftp)
- [How to: download files using the local Git repository](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>How to: Configure deployment credentials
Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site, which you can do from the portal. Credentials are set at the Function app level.

1. In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Go to App Service settings** > **Deployment credentials**.
   
    ![Set local deployment credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Type in a username and password, then click **Save**. You can now use these credentials to access your function app from FTP or the built-in Git repo.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>How to: Download files using FTP

1. In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Go to App Service settings** > **Properties** and copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.  

    **FTP/Deployment User** must be entered as displayed in the portal, including the app name, in order to provide proper context for the FTP server.
   
    ![Get your deployment information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/get-deployment-credentials.png)

2. From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-the-local-git-repository"></a>How to: download files using the local Git repository

1. In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Configure continuous integration** > **Setup**.

2. In the Deployments blade, click **Choose source**, **Local Git repository**, then click **OK**.

3. Click **Go to App Service settings** > **Properties** and note the value of Git URL. 
   
    ![Setup continuous deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Clone the repo on your local machine using a Git-aware command line or your favorite Git tool. The Git clone command looks like the following:
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Fetch files from your function app to the clone on your local computer, as in the following example:
   
        git pull origin master
   
    If requested, supply the username and password for your function app deployment.  

[GitHub]: https://github.com/







