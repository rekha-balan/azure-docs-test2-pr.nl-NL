---
title: Using Ruby in Azure App Service Web Apps on Linux | Microsoft Docs
description: Using Ruby in Azure App Service Web Apps on Linux.
keywords: azure app service, web app, faq, linux, oss, ruby
services: app-service
documentationCenter: ''
authors: aelnably
manager: erikre
editor: ''
ms.assetid: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: e77b5abe10582262dd50000a605843eebe00ac4b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661459"
---
# <a name="using-ruby-in-web-apps-on-linux"></a>Using Ruby in Web Apps on Linux #

With the latest update to our backend, we introduced support for Ruby v.2.3. By setting the configuration of your Linux web app, you can change the application stack.

## <a name="using-the-azure-portal"></a>Using the Azure portal ##

From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:

![Start creating a web app on the Azure portal][1]

Next, the **Create blade** opens as shown in the following image:

![The Create blade][2]

1. Give your web app a name.
2. Choose an existing resource group or create a new one. (See available regions in the [limitations section](app-service-linux-intro.md).)
3. Choose an existing Azure App Service plan or create a new one. (See App Service plan notes in the [limitations section](app-service-linux-intro.md).)
4. Choose the Ruby from the Built-in Runtime stacks.

After your Ruby web app gets created, you can deploy to it using Git or FTP.

## <a name="next-steps"></a>Next steps
* [What is App Service on Linux?](app-service-linux-intro.md)
* [Creating Web Apps in App Service on Linux](app-service-linux-how-to-create-a-web-app.md)
* [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md)
* [Azure App Service Web Apps on Linux FAQ](app-service-linux-faq.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-ruby/New-Linux.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-ruby/Ruby-UX.png

