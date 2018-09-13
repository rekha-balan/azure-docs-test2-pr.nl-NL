---
title: Manage a web app in Azure App Service
description: Links to resources for managing a web app in Azure App Service.
services: app-service\web
documentationcenter: ''
author: erikre
manager: erikre
editor: ''
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: b5d00cf094a813c7a14a3fd5b4a5d73b5e2de49e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563690"
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Manage a web app in Azure App Service
This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Management includes all of the tasks that keep your web app running smoothly. 

Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.

Many web app management tasks can be performed in the Azure Portal.

## <a name="before-you-deploy-your-web-app-to-production"></a>Before you deploy your web app to production
### <a name="choose-a-tier"></a>Choose a tier
Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium. For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/). 

* [App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.
* You can always [switch tiers](web-sites-scale.md) after you create your web app.

### <a name="configuration"></a>Configuration
Use the [Azure Portal](https://portal.azure.com/) to set various configuration options. For details, see [Configure web apps in Azure App Service](web-sites-configure.md). Here is a quick checklist:

* Select **runtime versions** for .NET, PHP, Java, or Python, if needed.
* Enable **WebSockets** if your web app uses the WebSocket protocol. (This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)
* Are you running continuous web jobs? If so, enable **Always On**.
* Set the **default document**, such as index.html.

In addition to these basic configuration settings, you may want to configure the following:

* **Secure Socket Layer (SSL)** encryption. To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it. See [Enable HTTPS for a web app in Azure App Service](web-sites-configure-ssl-certificate.md).
* **Custom domain name.** Your web app automatically has a subdomain under azurewebsites.net. You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](web-sites-custom-domain-name.md).

Language-specific configuration:

* **PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).
* **Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>While your web app is running
While your web app is running, you want to make sure it is available, and that it scales to meet user traffic. You may also need to troubleshoot errors.

### <a name="monitoring"></a>Monitoring
* Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.
* [Scale your web app](web-sites-scale.md) in response to traffic. Depending on your tier, you can scale the number of VMs and/or the size of the VM instances. In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.  

### <a name="backups"></a>Backups
* Set [automatic backups](web-sites-backup.md) of your web app. Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.

### <a name="troubleshooting"></a>Troubleshooting
* If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud. 
* Outside of Visual Studio, there are various ways to collect diagnostic logs. See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).
* For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Restoring Data
* [Restore](web-sites-restore.md) a web app that was previously backed up.

## <a name="when-you-update-your-web-app"></a>When you update your web app
If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).

Consider using [staged deployment](web-sites-staged-publishing.md). This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment. 

If you use Visual Studio Team Services, you can set up continuous deployment from source control:

* [Using Team Foundation Version Control (TFVC)](../cloud-services/cloud-services-continuous-delivery-use-vso.md) 
* [Using Git](../cloud-services/cloud-services-continuous-delivery-use-vso-git.md)

<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


