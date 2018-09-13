---
title: Troubleshoot Azure RBAC | Microsoft Docs
description: Get help with issues or questions about Role Based Access Control resources.
services: azure-portal
documentationcenter: na
author: kgremban
manager: femila
editor: ''
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: kgremban
ms.openlocfilehash: acab331c63dc8ccc06a57c5fe3ba67d22ab42c5c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554656"
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="3e57e-103">Role-Based Access Control troubleshooting</span><span class="sxs-lookup"><span data-stu-id="3e57e-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="3e57e-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span><span class="sxs-lookup"><span data-stu-id="3e57e-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="3e57e-105">These three roles cover all resource types:</span><span class="sxs-lookup"><span data-stu-id="3e57e-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="3e57e-106">Owner</span><span class="sxs-lookup"><span data-stu-id="3e57e-106">Owner</span></span>  
* <span data-ttu-id="3e57e-107">Contributor</span><span class="sxs-lookup"><span data-stu-id="3e57e-107">Contributor</span></span>  
* <span data-ttu-id="3e57e-108">Reader</span><span class="sxs-lookup"><span data-stu-id="3e57e-108">Reader</span></span>  

<span data-ttu-id="3e57e-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span><span class="sxs-lookup"><span data-stu-id="3e57e-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="3e57e-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span><span class="sxs-lookup"><span data-stu-id="3e57e-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="3e57e-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span><span class="sxs-lookup"><span data-stu-id="3e57e-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="3e57e-112">App service workloads</span><span class="sxs-lookup"><span data-stu-id="3e57e-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="3e57e-113">Write access capabilities</span><span class="sxs-lookup"><span data-stu-id="3e57e-113">Write access capabilities</span></span>
<span data-ttu-id="3e57e-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span><span class="sxs-lookup"><span data-stu-id="3e57e-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="3e57e-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span><span class="sxs-lookup"><span data-stu-id="3e57e-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="3e57e-116">Commands (like start, stop, etc.)</span><span class="sxs-lookup"><span data-stu-id="3e57e-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="3e57e-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span><span class="sxs-lookup"><span data-stu-id="3e57e-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="3e57e-118">Accessing publishing credentials and other secrets like app settings and connection strings</span><span class="sxs-lookup"><span data-stu-id="3e57e-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="3e57e-119">Streaming logs</span><span class="sxs-lookup"><span data-stu-id="3e57e-119">Streaming logs</span></span>
* <span data-ttu-id="3e57e-120">Diagnostic logs configuration</span><span class="sxs-lookup"><span data-stu-id="3e57e-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="3e57e-121">Console (command prompt)</span><span class="sxs-lookup"><span data-stu-id="3e57e-121">Console (command prompt)</span></span>
* <span data-ttu-id="3e57e-122">Active and recent deployments (for local git continuous deployment)</span><span class="sxs-lookup"><span data-stu-id="3e57e-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="3e57e-123">Estimated spend</span><span class="sxs-lookup"><span data-stu-id="3e57e-123">Estimated spend</span></span>
* <span data-ttu-id="3e57e-124">Web tests</span><span class="sxs-lookup"><span data-stu-id="3e57e-124">Web tests</span></span>
* <span data-ttu-id="3e57e-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span><span class="sxs-lookup"><span data-stu-id="3e57e-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="3e57e-126">If you can't access any of these tiles, you'll need to ask your administrator for Contributor access to the web app.</span><span class="sxs-lookup"><span data-stu-id="3e57e-126">If you can't access any of these tiles, you'll need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="3e57e-127">Dealing with related resources</span><span class="sxs-lookup"><span data-stu-id="3e57e-127">Dealing with related resources</span></span>
<span data-ttu-id="3e57e-128">Web apps are complicated by the presence of a few different resources that interplay.</span><span class="sxs-lookup"><span data-stu-id="3e57e-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="3e57e-129">Here is a typical resource group with a couple websites:</span><span class="sxs-lookup"><span data-stu-id="3e57e-129">Here is a typical resource group with a couple websites:</span></span>

![Web app resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="3e57e-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal will be disabled.</span><span class="sxs-lookup"><span data-stu-id="3e57e-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal will be disabled.</span></span>

<span data-ttu-id="3e57e-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span><span class="sxs-lookup"><span data-stu-id="3e57e-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="3e57e-133">Viewing the web app’s pricing tier (Free or Standard)</span><span class="sxs-lookup"><span data-stu-id="3e57e-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="3e57e-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span><span class="sxs-lookup"><span data-stu-id="3e57e-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="3e57e-135">Quotas (storage, bandwidth, CPU)</span><span class="sxs-lookup"><span data-stu-id="3e57e-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="3e57e-136">These items require **write** access to the whole **Resource group** that contains your website:</span><span class="sxs-lookup"><span data-stu-id="3e57e-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="3e57e-137">SSL Certificates and bindings (This is because SSL certificates can be shared between sites in the same resource group and geo-location)</span><span class="sxs-lookup"><span data-stu-id="3e57e-137">SSL Certificates and bindings (This is because SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="3e57e-138">Alert rules</span><span class="sxs-lookup"><span data-stu-id="3e57e-138">Alert rules</span></span>  
* <span data-ttu-id="3e57e-139">Autoscale settings</span><span class="sxs-lookup"><span data-stu-id="3e57e-139">Autoscale settings</span></span>  
* <span data-ttu-id="3e57e-140">Application insights components</span><span class="sxs-lookup"><span data-stu-id="3e57e-140">Application insights components</span></span>  
* <span data-ttu-id="3e57e-141">Web tests</span><span class="sxs-lookup"><span data-stu-id="3e57e-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="3e57e-142">Virtual machine workloads</span><span class="sxs-lookup"><span data-stu-id="3e57e-142">Virtual machine workloads</span></span>
<span data-ttu-id="3e57e-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="3e57e-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="3e57e-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span><span class="sxs-lookup"><span data-stu-id="3e57e-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="3e57e-145">These items require **write** access to the **Virtual machine**:</span><span class="sxs-lookup"><span data-stu-id="3e57e-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="3e57e-146">Endpoints</span><span class="sxs-lookup"><span data-stu-id="3e57e-146">Endpoints</span></span>  
* <span data-ttu-id="3e57e-147">IP addresses</span><span class="sxs-lookup"><span data-stu-id="3e57e-147">IP addresses</span></span>  
* <span data-ttu-id="3e57e-148">Disks</span><span class="sxs-lookup"><span data-stu-id="3e57e-148">Disks</span></span>  
* <span data-ttu-id="3e57e-149">Extensions</span><span class="sxs-lookup"><span data-stu-id="3e57e-149">Extensions</span></span>  

<span data-ttu-id="3e57e-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span><span class="sxs-lookup"><span data-stu-id="3e57e-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="3e57e-151">Availability set</span><span class="sxs-lookup"><span data-stu-id="3e57e-151">Availability set</span></span>  
* <span data-ttu-id="3e57e-152">Load balanced set</span><span class="sxs-lookup"><span data-stu-id="3e57e-152">Load balanced set</span></span>  
* <span data-ttu-id="3e57e-153">Alert rules</span><span class="sxs-lookup"><span data-stu-id="3e57e-153">Alert rules</span></span>  

<span data-ttu-id="3e57e-154">If you can't access any of these tiles, youneed to ask your administrator for Contributor access to the Resource group.</span><span class="sxs-lookup"><span data-stu-id="3e57e-154">If you can't access any of these tiles, youneed to ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="3e57e-155">See more</span><span class="sxs-lookup"><span data-stu-id="3e57e-155">See more</span></span>
* <span data-ttu-id="3e57e-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3e57e-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="3e57e-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span><span class="sxs-lookup"><span data-stu-id="3e57e-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="3e57e-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span><span class="sxs-lookup"><span data-stu-id="3e57e-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="3e57e-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span><span class="sxs-lookup"><span data-stu-id="3e57e-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>


