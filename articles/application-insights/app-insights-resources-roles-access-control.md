---
title: Resources, roles and access control in Azure Application Insights | Microsoft Docs
description: Owners, contributors and readers of your organization's insights.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: awills
ms.openlocfilehash: 36fab7f23837fc85a724578caacc51c10e911b17
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551507"
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="aa63c-103">Resources, roles, and access control in Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa63c-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="aa63c-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="aa63c-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa63c-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span><span class="sxs-lookup"><span data-stu-id="aa63c-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="aa63c-106">Assign the **Application Insights component contributor** role.</span><span class="sxs-lookup"><span data-stu-id="aa63c-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="aa63c-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span><span class="sxs-lookup"><span data-stu-id="aa63c-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="aa63c-108">[Learn more](#access).</span><span class="sxs-lookup"><span data-stu-id="aa63c-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="aa63c-109">Resources, groups and subscriptions</span><span class="sxs-lookup"><span data-stu-id="aa63c-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="aa63c-110">First, some definitions:</span><span class="sxs-lookup"><span data-stu-id="aa63c-110">First, some definitions:</span></span>

* <span data-ttu-id="aa63c-111">**Resource** - An instance of a Microsoft Azure service.</span><span class="sxs-lookup"><span data-stu-id="aa63c-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="aa63c-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span><span class="sxs-lookup"><span data-stu-id="aa63c-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="aa63c-113">Other types of Azure resources include web apps, databases, and VMs.</span><span class="sxs-lookup"><span data-stu-id="aa63c-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="aa63c-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span><span class="sxs-lookup"><span data-stu-id="aa63c-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="aa63c-115">To find a resource, type part of its name in the filter field.</span><span class="sxs-lookup"><span data-stu-id="aa63c-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![List of Azure resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="aa63c-117">[**Resource group**][group] - Every resource belongs to one group.</span><span class="sxs-lookup"><span data-stu-id="aa63c-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="aa63c-118">A group is a convenient way to manage related resources, particularly for access control.</span><span class="sxs-lookup"><span data-stu-id="aa63c-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="aa63c-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span><span class="sxs-lookup"><span data-stu-id="aa63c-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![Choose Browse, Resource groups, then choose a group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="aa63c-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="aa63c-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="aa63c-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span><span class="sxs-lookup"><span data-stu-id="aa63c-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="aa63c-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span><span class="sxs-lookup"><span data-stu-id="aa63c-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <a name="access"></a> <span data-ttu-id="aa63c-124">Control access in the resource group</span><span class="sxs-lookup"><span data-stu-id="aa63c-124">Control access in the resource group</span></span>
<span data-ttu-id="aa63c-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span><span class="sxs-lookup"><span data-stu-id="aa63c-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="aa63c-126">They are attached to the same [resource group](#resource-group) as your application.</span><span class="sxs-lookup"><span data-stu-id="aa63c-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="aa63c-127">You might also have put other Azure services in there, such as websites or storage.</span><span class="sxs-lookup"><span data-stu-id="aa63c-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Resources in Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="aa63c-129">To control access to these resources it's therefore recommended to:</span><span class="sxs-lookup"><span data-stu-id="aa63c-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="aa63c-130">Control access at the **resource group or subscription** level.</span><span class="sxs-lookup"><span data-stu-id="aa63c-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="aa63c-131">Assign the **Application Insights Component contributor** role to users.</span><span class="sxs-lookup"><span data-stu-id="aa63c-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="aa63c-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span><span class="sxs-lookup"><span data-stu-id="aa63c-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="aa63c-133">To provide access to another user</span><span class="sxs-lookup"><span data-stu-id="aa63c-133">To provide access to another user</span></span>
<span data-ttu-id="aa63c-134">You must have Owner rights to the subscription or the resource group.</span><span class="sxs-lookup"><span data-stu-id="aa63c-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="aa63c-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="aa63c-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="aa63c-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa63c-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="aa63c-137">Navigate to the resource group</span><span class="sxs-lookup"><span data-stu-id="aa63c-137">Navigate to the resource group</span></span>
<span data-ttu-id="aa63c-138">Add the user there.</span><span class="sxs-lookup"><span data-stu-id="aa63c-138">Add the user there.</span></span>

![In your application's resource blade, open Essentials, open the resource group, and there select Settings/Users.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="aa63c-141">Or you could go up another level and add the user to the Subscription.</span><span class="sxs-lookup"><span data-stu-id="aa63c-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="aa63c-142">Select a role</span><span class="sxs-lookup"><span data-stu-id="aa63c-142">Select a role</span></span>
![Select a role for the new user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="aa63c-144">Role</span><span class="sxs-lookup"><span data-stu-id="aa63c-144">Role</span></span> | <span data-ttu-id="aa63c-145">In the resource group</span><span class="sxs-lookup"><span data-stu-id="aa63c-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="aa63c-146">Owner</span><span class="sxs-lookup"><span data-stu-id="aa63c-146">Owner</span></span> |<span data-ttu-id="aa63c-147">Can change anything, including user access</span><span class="sxs-lookup"><span data-stu-id="aa63c-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="aa63c-148">Contributor</span><span class="sxs-lookup"><span data-stu-id="aa63c-148">Contributor</span></span> |<span data-ttu-id="aa63c-149">Can edit anything, including all resources</span><span class="sxs-lookup"><span data-stu-id="aa63c-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="aa63c-150">Application Insights Component contributor</span><span class="sxs-lookup"><span data-stu-id="aa63c-150">Application Insights Component contributor</span></span> |<span data-ttu-id="aa63c-151">Can edit Application Insights resources, web tests and alerts</span><span class="sxs-lookup"><span data-stu-id="aa63c-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="aa63c-152">Reader</span><span class="sxs-lookup"><span data-stu-id="aa63c-152">Reader</span></span> |<span data-ttu-id="aa63c-153">Can view but not change anything</span><span class="sxs-lookup"><span data-stu-id="aa63c-153">Can view but not change anything</span></span> |

<span data-ttu-id="aa63c-154">'Editing' includes creating, deleting and updating:</span><span class="sxs-lookup"><span data-stu-id="aa63c-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="aa63c-155">Resources</span><span class="sxs-lookup"><span data-stu-id="aa63c-155">Resources</span></span>
* <span data-ttu-id="aa63c-156">Web tests</span><span class="sxs-lookup"><span data-stu-id="aa63c-156">Web tests</span></span>
* <span data-ttu-id="aa63c-157">Alerts</span><span class="sxs-lookup"><span data-stu-id="aa63c-157">Alerts</span></span>
* <span data-ttu-id="aa63c-158">Continuous export</span><span class="sxs-lookup"><span data-stu-id="aa63c-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="aa63c-159">Select the user</span><span class="sxs-lookup"><span data-stu-id="aa63c-159">Select the user</span></span>

<span data-ttu-id="aa63c-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="aa63c-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="aa63c-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span><span class="sxs-lookup"><span data-stu-id="aa63c-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="aa63c-162">Related content</span><span class="sxs-lookup"><span data-stu-id="aa63c-162">Related content</span></span>

* [<span data-ttu-id="aa63c-163">Role based access control in Azure</span><span class="sxs-lookup"><span data-stu-id="aa63c-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md





