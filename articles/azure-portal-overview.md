---
title: Microsoft Azure portal overview
description: Learn how to use the Microsoft Azure portal.
services: ''
documentationcenter: ''
author: davidwrede
manager: erikre
editor: jimbe
ms.assetid: 53cb9df1-c96a-4f4e-b022-18336cd3d697
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/16/2015
ms.author: dwrede
ms.openlocfilehash: 8dc53c3128644ff4a53ed3de4ea281b8457fac01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564379"
---
# <a name="microsoft-azure-portal-overview"></a>Microsoft Azure portal overview
The Microsoft Azure portal is a central place where you can provision and manage your Azure resources.  This tutorial will familiarize you with the portal and show you how to use some of these key capabilities:

* A **comprehensive marketplace** that lets you browse through thousands of items from Microsoft and other vendors that can be purchased and/or provisioned.
* A **unified and scalable browse experience** that makes it easy to find the resources you care about and perform various management operations.
* **Consistent management pages** (or blades) that let you manage Azure’s wide variety of services through a consistent way of exposing settings, actions, billing information, health monitoring and usage data, and much more.
* A **personal experience** that lets you create a customized start screen that shows the information that you want to see whenever you log in.  You can also customize any of the management blades that contain tiles.
  
  ![Azure Portal UI Orientation][UIOrientation]

## <a name="before-you-get-started"></a>Before you get started
You will need a valid Azure subscription to go through this tutorial.  If you don’t have one, then [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/) today.  Once you have a subscription, you can access the portal at [https://portal.azure.com].

## <a name="how-to-create-a-resource"></a>How to create a resource
Azure has a marketplace with thousands of items that you can create from one place.  Let’s say you want to create a new Windows Server 2012 VM.  The +NEW hub is your entry point into a curated set of featured categories from the marketplace.  Each category has a small set of featured items along with a link to the full marketplace that shows all categories and search. To create that new Windows Server 2012 VM, perform the following actions:  

1. Windows Server 2012 is featured, so you can select it from the Compute category.  
2. Fill out some basic inputs on a form.
3. Click ‘Create’ and your VM will begin to provision immediately.

The notifications hub will alert you when your resource has been created and a management blade will open (you can always browse to resources later).

![Portal Categories][PortalCategories]

## <a name="how-to-find-your-resources"></a>How to find your resources
You can always pin frequently accessed resources to your startboard, but you might need to browse to something that you don’t frequently access.  The browse hub shown below is your way to get to all of your resources.  You can filter by subscription, choose/resize columns, and navigate to the management blades by clicking on individual items.

![Browse Hub][BrowseHub]

## <a name="how-to-manage-and-delegate-access-to-a-resource"></a>How to manage and delegate access to a resource
From this blade you can connect to the virtual machine using remote desktop, monitor key performance metrics, control access to this VM using role based access (RBAC), configure the VM, and perform other important management tasks.  Delegating access based on role is critical to managing at scale.  Click [here](active-directory/role-based-access-control-configure.md) to learn more about it. To delegate access to a resource, perform the following actions:

1. Browse to your resource.
2. Click ‘All settings’ in the Essentials section.
3. Click ‘Users’ in the settings list.
4. Click ‘Add’ in the command bar.
5. Choose a user and a role.

![Managing a Resource][ManageResource]

## <a name="how-to-get-help"></a>How to get help
If you ever have a problem, we’re here for you.  The portal has a help and support page that can point you in the right direction.  Depending on your [support plan](https://azure.microsoft.com/support/plans/), you can also create support tickets directly in the portal.  After creating a support ticket, you can manage the lifecycle of the ticket from within the portal. You can get to the help and support page by navigating to Browse -> Help + support.  

![Help and support][HelpSupport]

## <a name="summary"></a>Summary
Let’s review what you learned in this tutorial:

* You learned how to sign up, get a subscription, and browse to the portal
* You got oriented with the portal UI and learned how to create and browse resources
* You learned how to create a resource and browse resources
* You learned about the structure or management blades and how you can consistently manage different types of resources
* You learned how to customize the portal to bring the information you care about to the front and center
* You learned how to control access to resources using role based access (RBAC)
* You learned how to get help and support

The Microsoft Azure portal radically simplifies building and managing your applications in the cloud.  Take a look at the [management blog](https://azure.microsoft.com/blog/topics/management/) to keep up to date as we’re constantly [listening to feedback](https://feedback.azure.com/forums/223579-azure-preview-portal/) and making improvements.  [ScottGu’s blog](http://weblogs.asp.net/scottgu) is another great place to look for all Azure updates.

[UIOrientation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-portal-how-to-use/azure_portal_1.png
[PortalCategories]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-portal-how-to-use/azure_portal_2.png
[BrowseHub]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-portal-how-to-use/azure_portal_3.png
[ManageResource]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-portal-how-to-use/azure_portal_4.png
[CustomizeBlades]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-portal-how-to-use/azure_portal_5.png
[HelpSupport]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-portal-how-to-use/azure_portal_6.png






