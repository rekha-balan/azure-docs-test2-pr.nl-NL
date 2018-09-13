---
title: Azure portal dashboard access | Microsoft Docs
description: This article explains how to share access to a dashboard in the Azure portal.
services: azure-portal
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: 3589bc63569aedadea71f38f88307041c0fa07fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553060"
---
# <a name="sharing-azure-dashboards"></a><span data-ttu-id="8fca9-103">Sharing Azure dashboards</span><span class="sxs-lookup"><span data-stu-id="8fca9-103">Sharing Azure dashboards</span></span>
<span data-ttu-id="8fca9-104">After configuring a dashboard, you can publish it and share it with other users in your organization.</span><span class="sxs-lookup"><span data-stu-id="8fca9-104">After configuring a dashboard, you can publish it and share it with other users in your organization.</span></span> <span data-ttu-id="8fca9-105">You permit others to access your dashboard by using Azure [Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8fca9-105">You permit others to access your dashboard by using Azure [Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="8fca9-106">You assign a user or group of users to a role, and that role defines whether those users can view or modify the published dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-106">You assign a user or group of users to a role, and that role defines whether those users can view or modify the published dashboard.</span></span> 

<span data-ttu-id="8fca9-107">All published dashboards are implemented as Azure resources, which means they exist as manageable items within your subscription and are contained in a resource group.</span><span class="sxs-lookup"><span data-stu-id="8fca9-107">All published dashboards are implemented as Azure resources, which means they exist as manageable items within your subscription and are contained in a resource group.</span></span>  <span data-ttu-id="8fca9-108">From an access control perspective, dashboards are no different than other resources, such as a virtual machine or a storage account.</span><span class="sxs-lookup"><span data-stu-id="8fca9-108">From an access control perspective, dashboards are no different than other resources, such as a virtual machine or a storage account.</span></span>

> [!TIP]
> <span data-ttu-id="8fca9-109">Individual tiles on the dashboard enforce their own access control requirements based on the resources they display.</span><span class="sxs-lookup"><span data-stu-id="8fca9-109">Individual tiles on the dashboard enforce their own access control requirements based on the resources they display.</span></span>  <span data-ttu-id="8fca9-110">Therefore, you can design a dashboard that is shared broadly while still protecting the data on individual tiles.</span><span class="sxs-lookup"><span data-stu-id="8fca9-110">Therefore, you can design a dashboard that is shared broadly while still protecting the data on individual tiles.</span></span>
> 
> 

## <a name="understanding-access-control-for-dashboards"></a><span data-ttu-id="8fca9-111">Understanding access control for dashboards</span><span class="sxs-lookup"><span data-stu-id="8fca9-111">Understanding access control for dashboards</span></span>
<span data-ttu-id="8fca9-112">With role-based access control, you can assign users to roles at three different levels of scope:</span><span class="sxs-lookup"><span data-stu-id="8fca9-112">With role-based access control, you can assign users to roles at three different levels of scope:</span></span>

* <span data-ttu-id="8fca9-113">subscription</span><span class="sxs-lookup"><span data-stu-id="8fca9-113">subscription</span></span>
* <span data-ttu-id="8fca9-114">resource group</span><span class="sxs-lookup"><span data-stu-id="8fca9-114">resource group</span></span>
* <span data-ttu-id="8fca9-115">resource</span><span class="sxs-lookup"><span data-stu-id="8fca9-115">resource</span></span>

<span data-ttu-id="8fca9-116">The permissions you assign are inherited from subscription down to the resource.</span><span class="sxs-lookup"><span data-stu-id="8fca9-116">The permissions you assign are inherited from subscription down to the resource.</span></span> <span data-ttu-id="8fca9-117">The published dashboard is a resource.</span><span class="sxs-lookup"><span data-stu-id="8fca9-117">The published dashboard is a resource.</span></span> <span data-ttu-id="8fca9-118">Therefore, you may already have users assigned to roles for the subscription which also work for the published dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-118">Therefore, you may already have users assigned to roles for the subscription which also work for the published dashboard.</span></span> 

<span data-ttu-id="8fca9-119">Here is an example.</span><span class="sxs-lookup"><span data-stu-id="8fca9-119">Here is an example.</span></span>  <span data-ttu-id="8fca9-120">Let's say you have an Azure subscription and various members of your team have been assigned the roles of **owner**, **contributor**, or **reader** for the subscription.</span><span class="sxs-lookup"><span data-stu-id="8fca9-120">Let's say you have an Azure subscription and various members of your team have been assigned the roles of **owner**, **contributor**, or **reader** for the subscription.</span></span> <span data-ttu-id="8fca9-121">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within the subscription.</span><span class="sxs-lookup"><span data-stu-id="8fca9-121">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within the subscription.</span></span>  <span data-ttu-id="8fca9-122">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span><span class="sxs-lookup"><span data-stu-id="8fca9-122">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="8fca9-123">Users with reader access are able to make local edits to a published dashboard (such as, when troubleshooting an issue), but are not able to publish those changes back to the server.</span><span class="sxs-lookup"><span data-stu-id="8fca9-123">Users with reader access are able to make local edits to a published dashboard (such as, when troubleshooting an issue), but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="8fca9-124">They will have the option to make a private copy of the dashboard for themselves</span><span class="sxs-lookup"><span data-stu-id="8fca9-124">They will have the option to make a private copy of the dashboard for themselves</span></span>

<span data-ttu-id="8fca9-125">However, you could also assign permissions to the resource group that contains several dashboards or to an individual dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-125">However, you could also assign permissions to the resource group that contains several dashboards or to an individual dashboard.</span></span> <span data-ttu-id="8fca9-126">For example, you may decide that a group of users should have limited permissions across the subscription but greater access to a particular dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-126">For example, you may decide that a group of users should have limited permissions across the subscription but greater access to a particular dashboard.</span></span> <span data-ttu-id="8fca9-127">You assign those users to a role for that dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-127">You assign those users to a role for that dashboard.</span></span> 

## <a name="publish-dashboard"></a><span data-ttu-id="8fca9-128">Publish dashboard</span><span class="sxs-lookup"><span data-stu-id="8fca9-128">Publish dashboard</span></span>
<span data-ttu-id="8fca9-129">Let's suppose you have finished configuring a dashboard that you want to share with a group of users in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8fca9-129">Let's suppose you have finished configuring a dashboard that you want to share with a group of users in your subscription.</span></span> <span data-ttu-id="8fca9-130">The steps below depict a customized group called Storage Managers, but you can name your group whatever you would like.</span><span class="sxs-lookup"><span data-stu-id="8fca9-130">The steps below depict a customized group called Storage Managers, but you can name your group whatever you would like.</span></span> <span data-ttu-id="8fca9-131">For information about creating an Active Directory group and adding users to that group, see [Managing groups in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8fca9-131">For information about creating an Active Directory group and adding users to that group, see [Managing groups in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span></span>

1. <span data-ttu-id="8fca9-132">In the dashboard, select **Share**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-132">In the dashboard, select **Share**.</span></span>
   
     ![select share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboard-share-access/select-share.png)
2. <span data-ttu-id="8fca9-134">Before assigning access, you must publish the dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-134">Before assigning access, you must publish the dashboard.</span></span> <span data-ttu-id="8fca9-135">By default, the dashboard will be published to a resource group named **dashboards**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-135">By default, the dashboard will be published to a resource group named **dashboards**.</span></span> <span data-ttu-id="8fca9-136">Select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-136">Select **Publish**.</span></span>
   
     ![publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboard-share-access/publish.png)

<span data-ttu-id="8fca9-138">Your dashboard is now published.</span><span class="sxs-lookup"><span data-stu-id="8fca9-138">Your dashboard is now published.</span></span> <span data-ttu-id="8fca9-139">If the permissions inherited from the subscription are suitable, you do not need to do anything more.</span><span class="sxs-lookup"><span data-stu-id="8fca9-139">If the permissions inherited from the subscription are suitable, you do not need to do anything more.</span></span> <span data-ttu-id="8fca9-140">Other users in your organization will be able to access and modify the dashboard based on their subscription level role.</span><span class="sxs-lookup"><span data-stu-id="8fca9-140">Other users in your organization will be able to access and modify the dashboard based on their subscription level role.</span></span> <span data-ttu-id="8fca9-141">However, for this tutorial, let's assign a group of users to a role for that dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-141">However, for this tutorial, let's assign a group of users to a role for that dashboard.</span></span>

## <a name="assign-access-to-a-dashboard"></a><span data-ttu-id="8fca9-142">Assign access to a dashboard</span><span class="sxs-lookup"><span data-stu-id="8fca9-142">Assign access to a dashboard</span></span>
1. <span data-ttu-id="8fca9-143">After publishing the dashboard, select **Manage users**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-143">After publishing the dashboard, select **Manage users**.</span></span>
   
     ![manage users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboard-share-access/manage-users.png)
2. <span data-ttu-id="8fca9-145">You will see a list of existing users that are already assigned a role for this dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fca9-145">You will see a list of existing users that are already assigned a role for this dashboard.</span></span> <span data-ttu-id="8fca9-146">Your list of existing users will be different than the image below.</span><span class="sxs-lookup"><span data-stu-id="8fca9-146">Your list of existing users will be different than the image below.</span></span> <span data-ttu-id="8fca9-147">Most likely, the assignments are inherited from the subscription.</span><span class="sxs-lookup"><span data-stu-id="8fca9-147">Most likely, the assignments are inherited from the subscription.</span></span> <span data-ttu-id="8fca9-148">To add a new user or group, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-148">To add a new user or group, select **Add**.</span></span>
   
     ![add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboard-share-access/existing-users.png)
3. <span data-ttu-id="8fca9-150">Select the role that represents the permissions you would like to grant.</span><span class="sxs-lookup"><span data-stu-id="8fca9-150">Select the role that represents the permissions you would like to grant.</span></span> <span data-ttu-id="8fca9-151">For this example, select **Contributor**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-151">For this example, select **Contributor**.</span></span>
   
     ![select role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboard-share-access/select-role.png)
4. <span data-ttu-id="8fca9-153">Select the user or group that you wish to assign to the role.</span><span class="sxs-lookup"><span data-stu-id="8fca9-153">Select the user or group that you wish to assign to the role.</span></span> <span data-ttu-id="8fca9-154">If you do not see the user or group you are looking for in the list, use the search box.</span><span class="sxs-lookup"><span data-stu-id="8fca9-154">If you do not see the user or group you are looking for in the list, use the search box.</span></span> <span data-ttu-id="8fca9-155">Your list of available groups will depend on the groups you have created in your Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8fca9-155">Your list of available groups will depend on the groups you have created in your Active Directory.</span></span>
   
     ![select user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboard-share-access/select-user.png) 
5. <span data-ttu-id="8fca9-157">When you have finished adding users or groups, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-157">When you have finished adding users or groups, select **OK**.</span></span> 
6. <span data-ttu-id="8fca9-158">The new assignment is added to the list of users.</span><span class="sxs-lookup"><span data-stu-id="8fca9-158">The new assignment is added to the list of users.</span></span> <span data-ttu-id="8fca9-159">Notice that its **Access** is listed as **Assigned** rather than **Inherited**.</span><span class="sxs-lookup"><span data-stu-id="8fca9-159">Notice that its **Access** is listed as **Assigned** rather than **Inherited**.</span></span>
   
     ![assigned roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a><span data-ttu-id="8fca9-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fca9-161">Next steps</span></span>
* <span data-ttu-id="8fca9-162">For a list of roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="8fca9-162">For a list of roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="8fca9-163">To learn about managing resources, see [Manage Azure resources through portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8fca9-163">To learn about managing resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>








