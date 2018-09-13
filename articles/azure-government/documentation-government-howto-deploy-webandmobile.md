---
title: Deploy to Azure App Services using Visual Studio 2015 | Microsoft Docs
description: This article describes how to deploy a Web App, API App or Mobile App to Azure Government using Visual Studio 2015 and Azure SDK.
services: azure-government
cloud: gov
documentationcenter: ''
author: sdubeymsft
manager: zakramer
ms.assetid: 8f9a3700-b9ee-43b7-b64d-2e6c3b57d4c0
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 01/03/2016
ms.author: sdubeymsft
ms.openlocfilehash: 7b332230e534a3b1ba8ae73c695b7aa69d662a85
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550596"
---
# <a name="deploy-to-azure-app-services-using-visual-studio-2015"></a>Deploy to Azure App Services using Visual Studio 2015
This article describes how to deploy an Azure App Services app (API App, Web App, Mobile App) to Azure Government using Visual Studio 2015.

## <a name="prerequisites"></a>Prerequisites
* See [Visual Studio prerequisites] (../app-service-api/app-service-api-dotnet-get-started.md#prerequisites) to install and configure Visual Studio 2015 and Azure SDK.
* Follow [these instructions] (documentation-government-manage-subscriptions.md) to configure Visual Studio to connect to Azure Government account.

## <a name="open-app-project-in-visual-studio"></a>Open App project in Visual Studio
* Open existing app solution\project in Visual Studio, create a project by following [these instructions] (../app-service-web/app-service-web-get-started-dotnet.md), or download sample app by following [these steps] (../app-service-api/app-service-api-dotnet-get-started.md#download-the-sample-application).
* Run the app in Visual Studio to make sure it works locally.

## <a name="deploy-to-azure-government"></a>Deploy to Azure Government
* Once **Visual Studio is configured to connect to Azure Government account** (already done in prerequisites section), instructions to deploy to app services are exactly same as for Azure Public.
* To deploy the app, follow [these steps] (../app-service-api/app-service-api-dotnet-get-started.md#a-idcreateapiappa-create-an-api-app-in-azure-and-deploy-code-to-it).

### <a name="references"></a>References
* [Deploy an ASP.NET web app to Azure App Service, using Visual Studio] (../app-service-web/app-service-web-get-started-dotnet.md)
* For other ways to deploy, see [Deploy your app to Azure App Service] (../app-service-web/web-sites-deploy.md)
* For general App Service documentation, see [App Service - API Apps Documentation] (../app-service-api/index.md)

## <a name="next-steps"></a>Next steps
For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).
