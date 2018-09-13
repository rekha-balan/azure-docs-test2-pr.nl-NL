---
title: Create an Azure web app running on Linux | Microsoft Docs
description: Web app creation workflow for App Service on Linux.
keywords: azure app service, web app, linux, oss
services: app-service
documentationcenter: ''
author: naziml
manager: erikre
editor: ''
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 66abb1d3d71b7338868e7b0ef86da67d9f12534b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549409"
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Create an Azure web app running on Linux
## <a name="use-the-azure-portal-to-create-your-web-app"></a>Use the Azure portal to create your web app
You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:

![Start creating a web app on the Azure portal][1]

Next, the **Create blade** opens as shown in the following image:

![The Create blade][2]

1. Give your web app a name.
2. Choose an existing resource group or create a new one. (See available regions in the [limitations section](app-service-linux-intro.md).)
3. Choose an existing Azure App Service plan or create a new one. (See App Service plan notes in the [limitations section](app-service-linux-intro.md).)
4. Choose the application stack that you intend to use. You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.

Once you have created the app, you can change the application stack from the application settings as shown in the following image:

![Application settings][3]

## <a name="deploy-your-web-app"></a>Deploy your web app
Choosing **deployment options** from the management portal gives you the option to use local a Git or GitHub repository to deploy your application. The rest of the instructions are similar to those for a non-Linux web app. You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.

You can also use FTP to upload your application to your site. You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:

![Diagnostics logs][4]

## <a name="next-steps"></a>Next steps
* [What is App Service on Linux?](app-service-linux-intro.md)
* [Using PM2 Configuration for Node.js in Web Apps on Linux](app-service-linux-using-nodejs-pm2.md)
* [Using Ruby in Azure App Service Web Apps on Linux](app-service-linux-using-ruby.md)
* [Azure App Service Web Apps on Linux FAQ](app-service-linux-faq.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png




