---
title: Azure App Service plans in-depth overview | Microsoft Docs
description: Learn how App Service plans for Azure App Service work, and how they benefit your management experience.
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: ''
author: btardif
manager: erikre
editor: ''
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: eae59562bfb2892da2c37fce1d108b32c2ebfbcf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552305"
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Azure App Service plans in-depth overview
App Service plans represent the collection of physical resources used to host your apps.

App Service plans define:

- Region (West US, East US, etc.)
- Scale count (one, two, three instances, etc.)
- Instance size (Small, Medium, Large)
- SKU (Free, Shared, Basic, Standard, Premium)

Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.  Apps in the same subscription, region, and resource group can share an App Service plan. 

All applications assigned to an **App Service plan** share the resources defined by it. This sharing saves money when hosting multiple apps in a single App Service plan.

Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way. 

If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.

For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances. Apps also have access to the standard service tier features. Plan instances on which apps are running are fully managed and highly available. 

> [!IMPORTANT]
> The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.

This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.

## <a name="apps-and-app-service-plans"></a>Apps and App Service plans
An app in App Service can be associated with only one App Service plan at any given time.

Both apps and plans are contained in a **resource group**. A resource group serves as the lifecycle boundary for every resource that's within it. You can use resource groups to manage all the pieces of an application together.

Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources. 

For example, you can separate resources among dev, test, and production environments. Having separate environments for production and dev/test lets you isolate resources. In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.

When you have multiple plans in a single resource group, you can also define an application that spans geographical regions. 

For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan. In such a situation, all the copies of the app are then contained in a single resource group. Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Create an App Service plan or use existing one
When you create an app, you should consider creating a resource group. On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.

Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one. This decision is more a question of capacity and expected load.

We recommend isolating your app into a new App Service plan when:

- App is resource-intensive. 
- App has different scaling factors from the other apps hosted in an existing plan.
- App needs resource in a different geographical region.

This way you can allocate a new set of resources for your app and gain greater control of your apps.

## <a name="create-an-app-service-plan"></a>Create an App Service plan
> [!TIP]
> If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)
 

You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.

In the [Azure portal](https://portal.azure.com), click **New** > 
**Web + mobile**, and then select **Web App** or other App Service app kind.
![Create an app in the Azure portal.][createWebApp]

You can then select or create the App Service plan for the new app.

 ![Create an App Service plan.][createASP]

To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**. Click **Pricing tier**, and then select an appropriate pricing tier for the service. Select **View all** to view more pricing options, such as **Free** and **Shared**. After you have selected the pricing tier, click the **Select** button.

## <a name="move-an-app-to-a-different-app-service-plan"></a>Move an app to a different App Service plan
You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com). You can move apps between plans as long as the plans are in the same resource group and geographical region.

To move an app to another plan:

- Navigate to the app that you want to move. 
- In the **Menu**, look for the **App Service Plan** section.
- Select **Change App Service plan** to start the process.

**Change App Service plan** opens the **App Service plan** selector. At this point, you can pick an existing plan to move this app into. 

> [!IMPORTANT]
> Only valid plans (in the same resource group and geographical location) are shown.

![App Service plan selector.][change]

Each plan has its own pricing tier. For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.

## <a name="clone-an-app-to-a-different-app-service-plan"></a>Clone an app to a different App Service plan
If you want to move the app to a different region, one alternative is app cloning. Cloning makes a copy of your app in a new or existing App Service plan in any region.

You can find **Clone App** in the **Development Tools** section of the menu.

> [!IMPORTANT]
> Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Scale an App Service plan
There are three ways to scale a plan:

* **Change the plan’s pricing tier**. A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.
* **Change the plan’s instance size**. As an example, a plan in the Basic tier that uses small instances can be changed to use large instances. All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.
* **Change the plan’s instance count**. For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances. A Premium plan can be scaled out to 20 instances (subject to availability). All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.

You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan. Changes apply to the App Service plan and affect all apps that it hosts.

 ![Set values to scale up an app.][pricingtier]

## <a name="app-service-plan-cleanup"></a>App Service plan cleanup
> [!IMPORTANT]
>**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.

To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.

## <a name="summary"></a>Summary
App Service plans represent a set of features and capacity that you can share across your apps. App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization. This way, if you want to save money on your testing environment, you can share a plan across multiple apps. You can also maximize throughput for your production environment by scaling it across multiple regions and plans.

## <a name="whats-changed"></a>What's changed
* For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png




