---
title: Web App Cloning using Azure Portal
description: Learn how to clone your Web Apps to new Web Apps using Azure Portal.
services: app-service\web
documentationcenter: ''
author: ahmedelnably
manager: stefsch
editor: ''
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: ef40367c8a75a5af6881ac5a60ddeec508b2af94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552629"
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Azure App Service App Cloning Using Azure Portal
The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region. This will enable customers to deploy a number of apps across different regions quickly and easily.

App cloning is currently only supported for premium tier app service plans. The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Cloning an existing App
The web app must be running in the **Premium** mode in order for you to create a clone for the web app.

1. In the [Azure Portal](https://portal.azure.com/), open your web app's blade.
2. Click **Tools**. Then, in the **Tools** blade, click **Clone App**.
   
    ![][1]
   
   > [!NOTE]
   > If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning. At this point, you have the option to select **Upgrade**.
   > 
   > 
3. In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan. Also the user will be able to choose whether to clone a number of source web app settings or not.
   
    ![][2]
4. After clicking **create** the platform will start working on creating a clone of the source web app.

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a>Cloning an existing App to an App Service Environment
In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.

## <a name="current-restrictions"></a>Current Restrictions
This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:

* Azure Traffic Manager settings are not cloned
* Auto scale settings are not cloned
* Backup schedule settings are not cloned
* VNET settings are not cloned
* App Insights are not automatically set up on the destination web app
* Easy Auth settings are not cloned
* Kudu Extension are not cloned
* TiP rules are not cloned
* Database content are not cloned

### <a name="references"></a>References
* [Web App Cloning using PowerShell](app-service-web-app-cloning.md)
* [Back up a web app in Azure App Service](web-sites-backup.md)
* [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md)
* [Create a web app in an App Service Environment](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Introduction to App Service Environment](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-cloning-portal/CloneSettings.png


