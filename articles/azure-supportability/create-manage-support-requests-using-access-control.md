---
title: Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests | Microsoft Docs
description: Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 5a1845d294678db76c8cc380f4a19491d49c040d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563091"
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="418d4-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span><span class="sxs-lookup"><span data-stu-id="418d4-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="418d4-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span><span class="sxs-lookup"><span data-stu-id="418d4-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="418d4-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span><span class="sxs-lookup"><span data-stu-id="418d4-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="418d4-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span><span class="sxs-lookup"><span data-stu-id="418d4-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="418d4-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span><span class="sxs-lookup"><span data-stu-id="418d4-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="418d4-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span><span class="sxs-lookup"><span data-stu-id="418d4-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![Subscription error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="418d4-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/\* at the Subscription scope to be able to create and manage support requests.</span><span class="sxs-lookup"><span data-stu-id="418d4-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/\* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="418d4-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="418d4-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="418d4-112">Getting Started</span><span class="sxs-lookup"><span data-stu-id="418d4-112">Getting Started</span></span>

<span data-ttu-id="418d4-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span><span class="sxs-lookup"><span data-stu-id="418d4-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="418d4-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span><span class="sxs-lookup"><span data-stu-id="418d4-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="418d4-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span><span class="sxs-lookup"><span data-stu-id="418d4-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="418d4-116">To create a custom role for support request management, the role must have the action Microsoft.Support/\*</span><span class="sxs-lookup"><span data-stu-id="418d4-116">To create a custom role for support request management, the role must have the action Microsoft.Support/\*</span></span>

<span data-ttu-id="418d4-117">Here’s an example of a custom role you can use to create and manage support requests.</span><span class="sxs-lookup"><span data-stu-id="418d4-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="418d4-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span><span class="sxs-lookup"><span data-stu-id="418d4-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="418d4-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span><span class="sxs-lookup"><span data-stu-id="418d4-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="418d4-120">Create and manage support requests in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="418d4-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="418d4-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span><span class="sxs-lookup"><span data-stu-id="418d4-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="418d4-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span><span class="sxs-lookup"><span data-stu-id="418d4-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="418d4-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span><span class="sxs-lookup"><span data-stu-id="418d4-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="418d4-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span><span class="sxs-lookup"><span data-stu-id="418d4-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="418d4-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span><span class="sxs-lookup"><span data-stu-id="418d4-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![Add role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="418d4-127">Click "Add" under the "Users" blade.</span><span class="sxs-lookup"><span data-stu-id="418d4-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="418d4-128">Select the custom role "Support Request Contributor" from the list of roles</span><span class="sxs-lookup"><span data-stu-id="418d4-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![Add support contributor role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="418d4-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span><span class="sxs-lookup"><span data-stu-id="418d4-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="418d4-131">Click "Select"</span><span class="sxs-lookup"><span data-stu-id="418d4-131">Click "Select"</span></span>

    ![Add users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="418d4-133">Click "Ok" to proceed</span><span class="sxs-lookup"><span data-stu-id="418d4-133">Click "Ok" to proceed</span></span>

    ![Add access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="418d4-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span><span class="sxs-lookup"><span data-stu-id="418d4-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![User added](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="418d4-137">When Joe logs in the portal, he sees the subscription to which he was added.</span><span class="sxs-lookup"><span data-stu-id="418d4-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="418d4-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span><span class="sxs-lookup"><span data-stu-id="418d4-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![New support request](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="418d4-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="418d4-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="418d4-141">Remove support request access in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="418d4-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="418d4-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span><span class="sxs-lookup"><span data-stu-id="418d4-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="418d4-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span><span class="sxs-lookup"><span data-stu-id="418d4-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="418d4-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span><span class="sxs-lookup"><span data-stu-id="418d4-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![Remove support request access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="418d4-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span><span class="sxs-lookup"><span data-stu-id="418d4-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![Subscription error-2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="418d4-148">Joe cannot see any support requests when he clicks "All support requests"</span><span class="sxs-lookup"><span data-stu-id="418d4-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![case details view-2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-supportability/media/create-manage-support-requests-using-access-control/case-details-view-2.png)











