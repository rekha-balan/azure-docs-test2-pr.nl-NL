---
title: Enable subscription management in your tenant - Azure | Microsoft Docs
description: Learn how to enable enable subscription management in your tenant when using Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 03/27/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 89bb6fd48c58b7672b7a2251a172cc169093d368
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857901"
---
# <a name="enable-subscription-management-in-your-tenant"></a><span data-ttu-id="85233-103">Enable subscription management in your tenant</span><span class="sxs-lookup"><span data-stu-id="85233-103">Enable subscription management in your tenant</span></span>

<span data-ttu-id="85233-104">As a global administrator of your directory, you might not have default access to all subscription resources in your tenant.</span><span class="sxs-lookup"><span data-stu-id="85233-104">As a global administrator of your directory, you might not have default access to all subscription resources in your tenant.</span></span> <span data-ttu-id="85233-105">This article outlines the steps to give yourself access to all subscriptions in your tenant.</span><span class="sxs-lookup"><span data-stu-id="85233-105">This article outlines the steps to give yourself access to all subscriptions in your tenant.</span></span> <span data-ttu-id="85233-106">It also provides a recommended approach to remaining compliant with any security controls your organization requires after you receive access.</span><span class="sxs-lookup"><span data-stu-id="85233-106">It also provides a recommended approach to remaining compliant with any security controls your organization requires after you receive access.</span></span>

## <a name="who-can-enable-management-of-subscriptions-in-my-directory"></a><span data-ttu-id="85233-107">Who can enable management of subscriptions in my directory?</span><span class="sxs-lookup"><span data-stu-id="85233-107">Who can enable management of subscriptions in my directory?</span></span>

<span data-ttu-id="85233-108">Each user assigned to the global administrator role must follow the steps below to enable subscription management.</span><span class="sxs-lookup"><span data-stu-id="85233-108">Each user assigned to the global administrator role must follow the steps below to enable subscription management.</span></span> <span data-ttu-id="85233-109">After you have enabled subscription management for yourself, you can add other global administrators who might need resource access as well.</span><span class="sxs-lookup"><span data-stu-id="85233-109">After you have enabled subscription management for yourself, you can add other global administrators who might need resource access as well.</span></span> <span data-ttu-id="85233-110">There is no directory setting that enables access for all members of the global administrator role.</span><span class="sxs-lookup"><span data-stu-id="85233-110">There is no directory setting that enables access for all members of the global administrator role.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="85233-111">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="85233-111">Sign in to the Azure portal</span></span>

<span data-ttu-id="85233-112">Sign in to the Azure portal with an account that is an eligible or active member of the global administrator role.</span><span class="sxs-lookup"><span data-stu-id="85233-112">Sign in to the Azure portal with an account that is an eligible or active member of the global administrator role.</span></span> <span data-ttu-id="85233-113">If the account is an eligible global administrator, you must first activate the role before moving on to the next step.</span><span class="sxs-lookup"><span data-stu-id="85233-113">If the account is an eligible global administrator, you must first activate the role before moving on to the next step.</span></span>

## <a name="access-the-azure-active-directory-admin-center"></a><span data-ttu-id="85233-114">Access the Azure Active Directory admin center</span><span class="sxs-lookup"><span data-stu-id="85233-114">Access the Azure Active Directory admin center</span></span>

<span data-ttu-id="85233-115">Now that you are signed in to the Azure portal as a global administrator, you can edit settings that provide access to Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="85233-115">Now that you are signed in to the Azure portal as a global administrator, you can edit settings that provide access to Azure subscriptions.</span></span> <span data-ttu-id="85233-116">Browse to the Azure Active Directory (Azure AD) admin center, and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="85233-116">Browse to the Azure Active Directory (Azure AD) admin center, and select **Properties**.</span></span>

![Screenshot of Azure AD admin center, with Properties highlighted](media/azure-pim-resource-rbac/aad_properties.png)

<span data-ttu-id="85233-118">In the list of properties, under **Global admin can manage Azure subscriptions**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="85233-118">In the list of properties, under **Global admin can manage Azure subscriptions**, select **Yes**.</span></span>

![Screenshot of Properties page, with toggle set to Yes](media/azure-pim-resource-rbac/aad_properties_save.png)

<span data-ttu-id="85233-120">Now your account is automatically added to the user access administrator role for every subscription resource in the tenant.</span><span class="sxs-lookup"><span data-stu-id="85233-120">Now your account is automatically added to the user access administrator role for every subscription resource in the tenant.</span></span>

## <a name="browse-to-azure-ad-pim"></a><span data-ttu-id="85233-121">Browse to Azure AD PIM</span><span class="sxs-lookup"><span data-stu-id="85233-121">Browse to Azure AD PIM</span></span>

 <span data-ttu-id="85233-122">From here, go to Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="85233-122">From here, go to Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="85233-123">Under **Manage**, select **Azure resources**.</span><span class="sxs-lookup"><span data-stu-id="85233-123">Under **Manage**, select **Azure resources**.</span></span>

![Screenshot of PIM, with Azure resources highlighted](media/azure-pim-resource-rbac/aadpim_manage_azure_resources.png)

## <a name="manage-and-discover-resources"></a><span data-ttu-id="85233-125">Manage and discover resources</span><span class="sxs-lookup"><span data-stu-id="85233-125">Manage and discover resources</span></span>

<span data-ttu-id="85233-126">If your organization is already using Azure AD PIM to protect administrators in Azure AD, you can see a list of subscriptions when the blade loads.</span><span class="sxs-lookup"><span data-stu-id="85233-126">If your organization is already using Azure AD PIM to protect administrators in Azure AD, you can see a list of subscriptions when the blade loads.</span></span>

![Screenshot of PIM, with list of subscriptions shown in blade](media/azure-pim-resource-rbac/aadpim_manage_azure_resource_some_there.png)

> [!NOTE]
> <span data-ttu-id="85233-128">If you do not see any resources, confirm that:</span><span class="sxs-lookup"><span data-stu-id="85233-128">If you do not see any resources, confirm that:</span></span>
>- <span data-ttu-id="85233-129">Your global administrator role is not expired.</span><span class="sxs-lookup"><span data-stu-id="85233-129">Your global administrator role is not expired.</span></span> 
>- <span data-ttu-id="85233-130">Your organization has an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="85233-130">Your organization has an Azure subscription.</span></span>

![Screenshot of PIM, with empty resource list](media/azure-pim-resource-rbac/aadpim_rbac_empty_resource_list.png)

## <a name="configure-assignments"></a><span data-ttu-id="85233-132">Configure assignments</span><span class="sxs-lookup"><span data-stu-id="85233-132">Configure assignments</span></span>

<span data-ttu-id="85233-133">Select a subscription from the list, and assign yourself (or a group you are a member of) as an eligible owner of the resource.</span><span class="sxs-lookup"><span data-stu-id="85233-133">Select a subscription from the list, and assign yourself (or a group you are a member of) as an eligible owner of the resource.</span></span> 
<span data-ttu-id="85233-134">[Read more about assigning roles](pim-resource-roles-assign-roles.md).</span><span class="sxs-lookup"><span data-stu-id="85233-134">[Read more about assigning roles](pim-resource-roles-assign-roles.md).</span></span>

<span data-ttu-id="85233-135">Repeat this process for each resource before proceeding to the next step.</span><span class="sxs-lookup"><span data-stu-id="85233-135">Repeat this process for each resource before proceeding to the next step.</span></span>

## <a name="clean-up-standing-access"></a><span data-ttu-id="85233-136">Clean up standing access</span><span class="sxs-lookup"><span data-stu-id="85233-136">Clean up standing access</span></span>

<span data-ttu-id="85233-137">Now that you have eligible assignments for the important subscriptions in your organization, you can clean up standing access by disabling the option in directory properties.</span><span class="sxs-lookup"><span data-stu-id="85233-137">Now that you have eligible assignments for the important subscriptions in your organization, you can clean up standing access by disabling the option in directory properties.</span></span>

![Screenshot of Properties page, with toggle set to No](media/azure-pim-resource-rbac/aad_properties_no.png)

## <a name="next-steps"></a><span data-ttu-id="85233-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="85233-139">Next steps</span></span>

- [<span data-ttu-id="85233-140">Discover Azure resources to manage in PIM</span><span class="sxs-lookup"><span data-stu-id="85233-140">Discover Azure resources to manage in PIM</span></span>](pim-resource-roles-discover-resources.md)
- [<span data-ttu-id="85233-141">Configure Azure resource role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="85233-141">Configure Azure resource role settings in PIM</span></span>](pim-resource-roles-configure-role-settings.md)
