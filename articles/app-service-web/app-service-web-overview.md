---
title: Web Apps overview | Microsoft Docs
description: Learn how Azure App Service helps you develop and host web applications
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/04/2017
ms.author: cephalin
ms.openlocfilehash: 2a1e1004a4dab48aed75740a24ff5556242eaa67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554543"
---
# <a name="web-apps-overview"></a>Web Apps overview
*App Service Web Apps* is a fully managed compute platform that is optimized for hosting websites and web applications. This [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) offering of Microsoft Azure lets you focus on your business logic while Azure takes care of the infrastructure to run and scale your apps.

The following 5-minute video introduces Azure App Service Web Apps.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>What is a web app in App Service?
In App Service, a *web app* is the compute resources that Azure provides for hosting a website or web application.  

The compute resources may be on shared or dedicated virtual machines (VMs), depending on the pricing tier that you choose. Your application code runs in a managed VM that is isolated from other customers.

Your code can be in any language or framework that is supported by [Azure App Service](../app-service/app-service-value-prop-what-is.md), such as ASP.NET, Node.js, Java, PHP, or Python. You can also run scripts that use [PowerShell and other scripting languages](web-sites-create-web-jobs.md#acceptablefiles) in a web app.

For examples of typical application scenarios that you can use Web Apps for, see [Web app scenarios](https://azure.microsoft.com/documentation/scenarios/web-app/) and the **Scenarios and recommendations** section of [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Why use Web Apps?
Here are some key features of App Service that apply to Web Apps:

* **Multiple languages and frameworks** - App Service has first-class support for ASP.NET, Node.js, Java, PHP, and Python. You can also run [PowerShell and other scripts or executables](web-sites-create-web-jobs.md) on App Service VMs.
* **DevOps optimization** - Set up [continuous integration and deployment](app-service-continuous-deployment.md) with Visual Studio Team Services, GitHub, or BitBucket. Promote updates through [test and staging environments](web-sites-staged-publishing.md). Perform [A/B testing](app-service-web-test-in-production-get-start.md). Manage your apps in App Service by using [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [cross-platform command-line interface (CLI)](../cli-install-nodejs.md).
* **Global scale with high availability** - Scale [up](web-sites-scale.md) or [out](../monitoring-and-diagnostics/insights-how-to-scale.md) manually or automatically. Host your apps anywhere in Microsoft's global datacenter infrastructure, and the App Service [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promises high availability.
* **Connections to SaaS platforms and on-premises data** - Choose from more than 50 [connectors](../connectors/apis-list.md) for enterprise systems (such as SAP, Siebel, and Oracle), SaaS services (such as Salesforce and Office 365), and internet services (such as Facebook and Twitter). Access on-premises data using [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Azure Virtual Networks](web-sites-integrate-with-vnet.md).
* **Security and compliance** - App Service is [ISO, SOC, and PCI compliant](https://www.microsoft.com/TrustCenter/).
* **Application templates** - Choose from an extensive list of application templates in the [Azure Marketplace](https://azure.microsoft.com/marketplace/) that let you use a wizard to install popular open-source software such as WordPress, Joomla, and Drupal.
* **Visual Studio integration** - Dedicated tools in Visual Studio streamline the work of creating, deploying, and debugging.

In addition, a web app can take advantage of features offered by [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (such as CORS support) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (such as push notifications). For more information about app types in App Service, see [Azure App Service overview](../app-service/app-service-value-prop-what-is.md).

Besides Web Apps in App Service, Azure offers other services that can be used for hosting websites and web applications. For most scenarios, Web Apps is the best choice.  For microservice architecture, consider [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric), and if you need more control over the VMs that your code runs on, consider [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/). For more information about how to choose between these Azure services, see [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Getting started
To get started by deploying sample code to a new web app in App Service, follow one of the tutorials in the following dropdown box. You'll need a free Azure account.

> [!div class="op_single_selector"]
> * [Deploy your first ASP.NET web app to Azure in 5 minutes](app-service-web-get-started-dotnet.md)
> * [Deploy your first PHP web app to Azure in 5 minutes](app-service-web-get-started-php.md)
> * [Deploy your first Node.js web app to Azure in 5 minutes](app-service-web-get-started-nodejs.md)
> * [Deploy your first Java web app to Azure in 5 minutes](app-service-web-get-started-java.md)
> * [Deploy your first Python web app to Azure in 5 minutes](app-service-web-get-started-python.md)
> * [Deploy your first HTML site to Azure in 5 minutes](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account. Create a starter app and play with it for up to an hour--no credit card required, no commitments.
> 
> 
