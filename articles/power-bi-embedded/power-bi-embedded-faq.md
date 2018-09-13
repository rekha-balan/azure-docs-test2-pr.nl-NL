---
title: FAQ
description: Power BI Embedded FAQ
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: 1475ed4f-fc84-4865-b243-e8a47d8bda59
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: be485debb4d8a2d1f64e1752bc204f1634d53c97
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551552"
---
# <a name="power-bi-embedded-faq"></a>Power BI Embedded FAQ
## <a name="whats-your-most-recent-announcement-about-power-bi-embedded"></a>What's your most recent announcement about Power BI Embedded?
Microsoft Power BI Embedded Service is now generally available with standard GA SLA. To learn more about this release, see [What's new](power-bi-embedded-whats-new.md).

## <a name="what-is-microsoft-power-bi-embedded"></a>What is Microsoft Power BI Embedded?
Microsoft Power BI Embedded is now generally available. Power BI Embedded is an Azure service that allows Application developers to embed stunning, fully interactive reports and visualizations in customer facing apps without the time and expense of having to build your own controls from the ground-up. We now have Power BI Embedded available with SLA in 9 data centers worldwide. We have also enhanced functionalities in the service like support for data security via row-level security (RLS) in Power BI Embedded for advanced filtering. We have also simplified and updated the Power BI Embedded pricing model. To learn more, see [Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/).  

## <a name="who-would-want-to-use-microsoft-power-bi-embedded-and-why"></a>Who would want to use Microsoft Power BI Embedded, and why?
Microsoft Power BI Embedded is for Application developers that want to offer stunning and interactive data visualization experiences for their users across any of their devices without having to build it themselves. With Power BI Embedded, developers can deliver always-up-to-date views with Direct Query. Developers can also programmatically deploy and manage automate Power BI with the Azure ARM APIs and Power BI APIs. As with all things Power BI, the embedded service automatically scales to meet the usage and needs of your application. The Power BI Embedded service features a Pay-as-you-go consumption based pricing model.

## <a name="how-does-power-bi-embedded-relate-to-the-power-bi-service"></a>How does Power BI Embedded relate to the Power BI service?
The Power BI Embedded and the Power BI service are separate offerings. Power BI Embedded features a consumption-based billing model, is deployed through the Azure portal and is designed to enable ISVs to embed data visualizations in applications for their customers to use. The Power BI service is billed and deployed through the O365 portal and is a standalone general purpose BI offering primarily targeted at enterprise internal use. To learn more about the Power BI service, see [www.powerbi.com](https://powerbi.microsoft.com).

## <a name="how-does-power-bi-embedded-improve-my-app"></a>How does Power BI Embedded improve my app?
Applications are significantly more powerful when you can leverage stunning, interactive data visualizations to inform user decisions directly in your application. Power BI Embedded lets you enhance your app with interactive, always up-to-date, rich data visualizations so that you can increase the utility of your app, user satisfaction and loyalty, and deliver contextual analytics with ease on any device.

## <a name="are-there-any-rules-or-restrictions-about-how-i-can-use-power-bi-embedded-in-my-app"></a>Are there any rules or restrictions about how I can use Power BI Embedded in my app?
Power BI Embedded is intended for your applications that are provided for third party use. If you want to use the Power BI Embedded service to create an internal business application, each of your internal users will need a Power BI Pro USL, and your organization will be charged for their consumption of the Power BI Embedded service in addition to their Power BI Pro USL fees. To avoid incurring both Power BI Pro USL fees and Power BI Embedded consumption costs for internal applications, the Power BI service offers its own content embedding capabilities outside of Power BI Embedded for no additional cost to Power BI USL holders (dev.powerbi.com).

## <a name="can-power-bi-embedded-be-used-to-create-internal-applications"></a>Can Power BI Embedded be used to create internal applications?
No, Power BI Embedded is only intended for use by external users and should not be used within internal business applications. In order to embed Power BI content for use in internal business applications, you should use the Power BI service, and all users consuming that content must have a valid Power BI Free or Power BI Pro user subscription license. More information on how to integrate internal applications with the Power BI service is available at  [https://dev.powerbi.com](https://dev.powerbi.com).

## <a name="is-this-service-available-globally"></a>Is this service available globally?
The Power BI Embedded service is available in most data centers now. You can always check the latest availability [here](https://azure.microsoft.com/status/).

## <a name="what-is-the-available-sla-for-the-service"></a>What is the available SLA for the service?
Power BI Embedded with Azure standard SLA. See [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/) for more information.

## <a name="how-is-this-service-priced"></a>How is this service priced?
See [Power BI Embedded Pricing](http://go.microsoft.com/fwlink/?LinkId=760527) for pricing information.

## <a name="what-is-a-report-session-and-how-is-it-billed"></a>What is a report session and how is it billed?
A session is a set of interactions between an end user and a Power BI Embedded report. Each time a Power BI Embedded report is displayed to a user, a session is initiated and the subscription holder will be charged for a session. Sessions are billed at a flat rate, independent of the number of visual elements in a report or how frequently the report content is refreshed. A session ends when either the user closes the report, or the session times out after one hour.

## <a name="do-you-offer-any-tools-or-guidance-to-help-me-estimate-how-many-renderssession-i-should-expect-how-will-i-know-how-many-renders-have-been-completed"></a>Do you offer any tools or guidance to help me estimate how many renders/session I should expect? How will I know how many renders have been completed?
The Azure Portal will provide billing details on how many renders / report sessions have been performed against your subscription.

## <a name="do-i-need-a-power-bi-subscription-in-order-to-develop-applications-with-power-bi-embedded-how-do-i-get-started"></a>Do I need a Power BI subscription in order to develop applications with Power BI Embedded? How do I get started?
As the application developer, you do not need to have a Power BI subscription in order to create the reports and visualizations you wish to use in your application. You will need a Microsoft Azure subscription and the free Power BI Desktop application.

Please see our service documentation for details on how to use the Power BI Embedded service.

## <a name="i-have-an-azure-subscription-can-i-use-power-bi-embedded-using-my-existing-subscription"></a>I have an Azure subscription. Can I use Power BI Embedded using my existing subscription?
Yes. You can use your existing Azure subscription to provision and use the Microsoft Power BI Embedded service.

## <a name="does-my-application-end-user-need-a-power-bi-license"></a>Does my application end-user need a Power BI license?
No. Your application’s end-users are not required to buy or the Power BI subscription separately in order to access the in-app data visualizations. In the power BI Embedded model you, as the application provider, will be billed for the service through the Azure consumption meter. Please refer to the [Pricing and licensing page](http://go.microsoft.com/fwlink/?LinkId=760527).

## <a name="how-does-user-authentication-work-with-power-bi-embedded"></a>How does user authentication work with Power BI Embedded?
The Power BI Embedded service uses App Tokens for authentication and authorization instead of explicit end-user authentication. In the App Token model, your application manages authentication and authorization for your end-users. Then, when necessary, your app creates

and sends the App Tokens which tells our service to render the requested report. This design does not require your app to use Azure AD for user authentication and authorization, although you can do this. You can learn more about App Tokens [here](power-bi-embedded-app-token-flow.md). We also introduced row-level security feature (RLS) in Power BI Embedded for advanced security filtering scenarios.

## <a name="what-data-sources-are-currently-supported-with-power-bi-embedded"></a>What data sources are currently supported with Power BI Embedded?
We are going to support access to cloud data sources that use basic credentials via Direct Query. This means that sources such as Azure SQL DB and Azure SQL DW are supported right now. We will add support for other data sources and access types in the coming months. For more information, see [Connect to a data source](power-bi-embedded-connect-datasource.md).

## <a name="how-does-the-tenancy-model-work-for-power-bi-embedded"></a>How does the tenancy model work for Power BI Embedded?
In the Power BI Embedded model, there is no explicit requirement to have your customers in Azure AD tenants. You can elect to require Azure AD for your customers, or not. As a result, the architecture of your application and infrastructure is what will determine the tenancy model required for Power BI Embedded.

Developers/employees working on or building your application will need to have an AAD user account when they are to manage your Azure Subscription and Workspace Collections via the Azure Portal. Programmatic APIs to enable developers to import reports, modify connection strings and get embed URLs leverage App Tokens for authentication instead, and as a result do not require an AAD. Details on how to use our APIs and Azure Portal can be found at [Power BI Embedded documentation ](https://azure.microsoft.com/documentation/services/power-bi-embedded/) on Azure.com.

## <a name="where-can-i-learn-more"></a>Where can I learn more?
You can visit the [Power BI Embedded documentation page](http://go.microsoft.com/fwlink/?LinkId=760526). You can stay up-to-date about this service by visiting the [Power BI developer blog](http://blogs.msdn.com/powerbidev) or by visiting the Power BI developer center at dev.powerbi.com. You can also ask questions at [Stackoverflow](http://stackoverflow.com/questions/tagged/powerbi).

## <a name="how-do-i-get-started"></a>How do I get started?
You can get started for free now! If you have an Azure subscription, you can now provision Power BI Embedded from the Azure portal directly.  You can also create you [free Azure account](https://azure.microsoft.com/free/). Once you've provisioned the Power BI Embedded service, you can easily use Power BI REST APIs directly, or use the developer SDK available on [GitHub](http://go.microsoft.com/fwlink/?LinkID=746472). Samples are provided on how to leverage the developer SDK.

## <a name="see-also"></a>See also

[What is Microsoft Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)
[Get started with Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
[Get started with sample](power-bi-embedded-get-started-sample.md)   
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
More questions? [Try the Power BI Community](http://community.powerbi.com/)

