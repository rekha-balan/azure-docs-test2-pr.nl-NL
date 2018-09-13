---
title: Create a Cordova app on Azure App Service Mobile Apps | Microsoft Docs
description: Follow this tutorial to get started with using Azure mobile app backends for Apache Cordova development
services: app-service\mobile
documentationcenter: javascript
author: conceptdev
manager: crdun
editor: ''
tags: ''
keywords: cordova,javascript,mobile,client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: crdun
ms.openlocfilehash: 223e9e35fcab347f9b5b8db01a9fd667b9f5d55d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814527"
---
# <a name="create-an-apache-cordova-app"></a>Create an Apache Cordova app
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Overview
This tutorial shows you how to add a cloud-based backend service to an Apache Cordova mobile app by using an Azure mobile app backend.  You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.

Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using the Mobile Apps feature in Azure App Service.

## <a name="prerequisites"></a>Prerequisites
To complete this tutorial, you need the following prerequisites:

* A PC with [Visual Studio Community 2017] or newer.
* [Visual Studio Tools for Apache Cordova].
* An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).

You may also bypass Visual Studio and use the Apache Cordova command line directly.  Using the command line is useful when completing the tutorial on a Mac computer.  Compiling Apache Cordova client applications using the command line is not covered by this tutorial.

## <a name="create-an-azure-mobile-app-backend"></a>Create an Azure mobile app backend
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Watch a video showing similar steps](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-the-server-project"></a>Configure the server project
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-apache-cordova-app"></a>Download and run the Apache Cordova app
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Next Steps
Now that you completed this quick start tutorial, move on to one of the following tutorials:

* [Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) to your Apache Cordova app.
* [Add Authentication](app-service-mobile-cordova-get-started-users.md) to your Apache Cordova app.
* [Add Push Notifications](app-service-mobile-cordova-get-started-push.md) to your Apache Cordova app.

Learn more about key concepts with Azure App Service.

* [Offline Data]
* [Authentication]
* [Push Notifications]

Learn how to use the SDKs.

* [Apache Cordova SDK]
* [ASP.NET Server SDK]
* [Node.js Server SDK]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Offline Data]: app-service-mobile-offline-data-sync.md
[Authentication]: app-service-mobile-auth.md
[Push Notifications]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
