---
title: Unexpected error when performing consent to an application | Microsoft Docs
description: Discusses errors that can occur during the process of consenting to an application and what you can do about them
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 70413d3467b2f9d5591e6138ed1a7347db58264b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858114"
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a><span data-ttu-id="144c2-103">Unexpected error when performing consent to an application</span><span class="sxs-lookup"><span data-stu-id="144c2-103">Unexpected error when performing consent to an application</span></span>

<span data-ttu-id="144c2-104">This article discusses errors that can occur during the process of consenting to an application.</span><span class="sxs-lookup"><span data-stu-id="144c2-104">This article discusses errors that can occur during the process of consenting to an application.</span></span> <span data-ttu-id="144c2-105">If you are troubleshooting unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="144c2-105">If you are troubleshooting unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="144c2-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span><span class="sxs-lookup"><span data-stu-id="144c2-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span></span> <span data-ttu-id="144c2-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span><span class="sxs-lookup"><span data-stu-id="144c2-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span></span> <span data-ttu-id="144c2-108">A consent prompt is displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span><span class="sxs-lookup"><span data-stu-id="144c2-108">A consent prompt is displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span></span>

<span data-ttu-id="144c2-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span><span class="sxs-lookup"><span data-stu-id="144c2-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span></span> <span data-ttu-id="144c2-110">If these conditions are not met, the following errors can occur.</span><span class="sxs-lookup"><span data-stu-id="144c2-110">If these conditions are not met, the following errors can occur.</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="144c2-111">Requesting not authorized permissions error</span><span class="sxs-lookup"><span data-stu-id="144c2-111">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="144c2-112">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span><span class="sxs-lookup"><span data-stu-id="144c2-112">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span></span> <span data-ttu-id="144c2-113">Contact an administrator, who can consent to this application on your behalf.</span><span class="sxs-lookup"><span data-stu-id="144c2-113">Contact an administrator, who can consent to this application on your behalf.</span></span>

<span data-ttu-id="144c2-114">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span><span class="sxs-lookup"><span data-stu-id="144c2-114">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="144c2-115">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span><span class="sxs-lookup"><span data-stu-id="144c2-115">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="144c2-116">Policy prevents granting permissions error</span><span class="sxs-lookup"><span data-stu-id="144c2-116">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="144c2-117">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span><span class="sxs-lookup"><span data-stu-id="144c2-117">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span></span> <span data-ttu-id="144c2-118">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span><span class="sxs-lookup"><span data-stu-id="144c2-118">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span></span>

<span data-ttu-id="144c2-119">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span><span class="sxs-lookup"><span data-stu-id="144c2-119">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span></span> <span data-ttu-id="144c2-120">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span><span class="sxs-lookup"><span data-stu-id="144c2-120">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="144c2-121">Intermittent problem error</span><span class="sxs-lookup"><span data-stu-id="144c2-121">Intermittent problem error</span></span>
* <span data-ttu-id="144c2-122">**AADSTS90090:** It looks like the sign-in process encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="144c2-122">**AADSTS90090:** It looks like the sign-in process encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="144c2-123">try again later.</span><span class="sxs-lookup"><span data-stu-id="144c2-123">try again later.</span></span>

<span data-ttu-id="144c2-124">This error indicates that an intermittent service side issue has occurred.</span><span class="sxs-lookup"><span data-stu-id="144c2-124">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="144c2-125">It can be resolved by attempting to consent to the application again.</span><span class="sxs-lookup"><span data-stu-id="144c2-125">It can be resolved by attempting to consent to the application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="144c2-126">Resource not available error</span><span class="sxs-lookup"><span data-stu-id="144c2-126">Resource not available error</span></span>
* <span data-ttu-id="144c2-127">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span><span class="sxs-lookup"><span data-stu-id="144c2-127">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="144c2-128">Contact the application developer.</span><span class="sxs-lookup"><span data-stu-id="144c2-128">Contact the application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="144c2-129">Resource not available in tenant error</span><span class="sxs-lookup"><span data-stu-id="144c2-129">Resource not available in tenant error</span></span>
* <span data-ttu-id="144c2-130">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="144c2-130">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="144c2-131">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="144c2-131">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="144c2-132">Permissions mismatch error</span><span class="sxs-lookup"><span data-stu-id="144c2-132">Permissions mismatch error</span></span>
* <span data-ttu-id="144c2-133">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="144c2-133">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="144c2-134">This request failed because it does not match how the app was pre-configured during app registration.</span><span class="sxs-lookup"><span data-stu-id="144c2-134">This request failed because it does not match how the app was pre-configured during app registration.</span></span> <span data-ttu-id="144c2-135">Contact the app vendor.\*\*</span><span class="sxs-lookup"><span data-stu-id="144c2-135">Contact the app vendor.\*\*</span></span>

<span data-ttu-id="144c2-136">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span><span class="sxs-lookup"><span data-stu-id="144c2-136">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span></span> <span data-ttu-id="144c2-137">This situation can occur for several reasons:</span><span class="sxs-lookup"><span data-stu-id="144c2-137">This situation can occur for several reasons:</span></span>

-   <span data-ttu-id="144c2-138">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span><span class="sxs-lookup"><span data-stu-id="144c2-138">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span></span> <span data-ttu-id="144c2-139">In this case, the application developer must update the configuration of the client application to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="144c2-139">In this case, the application developer must update the configuration of the client application to resolve this issue.</span></span>

-   <span data-ttu-id="144c2-140">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span><span class="sxs-lookup"><span data-stu-id="144c2-140">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span></span> <span data-ttu-id="144c2-141">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span><span class="sxs-lookup"><span data-stu-id="144c2-141">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span></span> <span data-ttu-id="144c2-142">The Service Principal can be provisioned in a number of ways, depending on the type of application, including:</span><span class="sxs-lookup"><span data-stu-id="144c2-142">The Service Principal can be provisioned in a number of ways, depending on the type of application, including:</span></span>

    -   <span data-ttu-id="144c2-143">Acquiring a subscription for the resource application (Microsoft published applications)</span><span class="sxs-lookup"><span data-stu-id="144c2-143">Acquiring a subscription for the resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="144c2-144">Consenting to the resource application</span><span class="sxs-lookup"><span data-stu-id="144c2-144">Consenting to the resource application</span></span>

    -   <span data-ttu-id="144c2-145">Granting the application permissions via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="144c2-145">Granting the application permissions via the Azure portal</span></span>

    -   <span data-ttu-id="144c2-146">Adding the application from the Azure AD Application Gallery</span><span class="sxs-lookup"><span data-stu-id="144c2-146">Adding the application from the Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="144c2-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="144c2-147">Next steps</span></span> 

[<span data-ttu-id="144c2-148">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span><span class="sxs-lookup"><span data-stu-id="144c2-148">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="144c2-149">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span><span class="sxs-lookup"><span data-stu-id="144c2-149">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


