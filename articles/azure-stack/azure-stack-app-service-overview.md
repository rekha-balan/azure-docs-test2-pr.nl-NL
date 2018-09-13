---
title: App Service Overview - Azure Stack | Microsoft Docs
description: Overview of App Service on Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9e6ff610f33a2e4cbd4f3c39074f8809f156ec4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551770"
---
# <a name="app-service-on-azure-stack-overview"></a>App Service on Azure Stack Overview

App Service on Azure Stack is the Azure offering brought to Azure Stack. The App Service on Azure Stack installer will create the following set of role instances:
*  Controller;
*  Management (Two instances will be created);
*  Front-End;
*  Publisher;
*  Worker (in Shared mode)

In addition, the App Service on Azure Stack installer will create a file server.
    
## <a name="whats-new-in-technical-preview-3-of-app-service-on-azure-stack"></a>What's New in Technical Preview 3 of App Service on Azure Stack?
![App Service in the Azure Stack Portal][1]

Technical Preview 3 of App Service on Azure Stack, builds on top of the second preview and brings a preview of Azure Functions to Azure Stack.  Azure Functions is an event-based serverless compute experience to accelerate your development.  New improvements to the stability of the service, updates to the Tenant Portal experience along with updates to the installer experience to give more configuration options.

## <a name="limitations-of-the-technical-preview"></a>Limitations of the Technical Preview

There is no support for the App Service on Azure Stack preview releases, although we do monitor the Azure Stack MSDN Forum. Don't put production workloads on this preview release. There is also no upgrade between App Service on Azure Stack preview releases. The primary purposes of these preview releases are to show what we are providing and to obtain feedback. 

## <a name="what-is-an-app-service-plan"></a>What is an App Service Plan?

The App Service resource provider uses the same code that Azure App Service uses. As a result, some common concepts are worth describing. In App Service, the pricing container for applications is called the App Service plan. It represents the set of dedicated virtual machines used to hold your apps. Within a given subscription, you can have multiple App Service plans. 

In Azure, there are shared and dedicated workers. A shared worker supports high-density multitenant app hosting and there is only one set of shared workers. Dedicated servers are only used by one tenant and come in three sizes: small, medium, and large. The needs of on-premises customers can't always be described by using those terms. In App Service on Azure Stack, resource provider administrators can define the worker tiers they want to make available.  Therefore having multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs. Using those worker tier definitions, they can then define their own pricing SKUs.

## <a name="portal-features"></a>Portal Features

App Service on Azure Stack uses the same UI that Azure App Service uses, as is true with the back end. Some features are disabled and aren't yet functional in Azure Stack, because Azure-specific expectations or services that those features require aren't yet available in Azure Stack. 

## <a name="next-steps"></a>Next steps

- [Before you get started with App Service on Azure Stack](azure-stack-app-service-before-you-get-started.md)
- [Install the App Service Resource Provider](azure-stack-app-service-deploy.md)

You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-overview/AppService_Portal.png

