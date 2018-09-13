---
title: Unexpected error when performing consent to an application | Microsoft Docs
description: Discusses errors that can occur during the process of consenting to an application and what you can do about them
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: fa76215ee95643ed468cc8c9eb973b9f9dae3f1c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549497"
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a><span data-ttu-id="2b737-103">Unexpected error when performing consent to an application</span><span class="sxs-lookup"><span data-stu-id="2b737-103">Unexpected error when performing consent to an application</span></span>

<span data-ttu-id="2b737-104">This article discusses errors that can occur during the process of consenting to an application.</span><span class="sxs-lookup"><span data-stu-id="2b737-104">This article discusses errors that can occur during the process of consenting to an application.</span></span> <span data-ttu-id="2b737-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="2b737-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="2b737-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span><span class="sxs-lookup"><span data-stu-id="2b737-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span></span> <span data-ttu-id="2b737-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span><span class="sxs-lookup"><span data-stu-id="2b737-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span></span> 

<span data-ttu-id="2b737-108">This results in a consent prompt being displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span><span class="sxs-lookup"><span data-stu-id="2b737-108">This results in a consent prompt being displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span></span>

<span data-ttu-id="2b737-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span><span class="sxs-lookup"><span data-stu-id="2b737-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span></span> <span data-ttu-id="2b737-110">If these conditions are not met, various errors can occur.</span><span class="sxs-lookup"><span data-stu-id="2b737-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="2b737-111">These include:</span><span class="sxs-lookup"><span data-stu-id="2b737-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="2b737-112">Requesting not authorized permissions error</span><span class="sxs-lookup"><span data-stu-id="2b737-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="2b737-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span><span class="sxs-lookup"><span data-stu-id="2b737-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span></span> <span data-ttu-id="2b737-114">Contact an administrator, who can consent to this application on your behalf.</span><span class="sxs-lookup"><span data-stu-id="2b737-114">Contact an administrator, who can consent to this application on your behalf.</span></span>

<span data-ttu-id="2b737-115">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span><span class="sxs-lookup"><span data-stu-id="2b737-115">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="2b737-116">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span><span class="sxs-lookup"><span data-stu-id="2b737-116">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="2b737-117">Policy prevents granting permissions error</span><span class="sxs-lookup"><span data-stu-id="2b737-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="2b737-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span><span class="sxs-lookup"><span data-stu-id="2b737-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span></span> <span data-ttu-id="2b737-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span><span class="sxs-lookup"><span data-stu-id="2b737-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span></span>

<span data-ttu-id="2b737-120">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span><span class="sxs-lookup"><span data-stu-id="2b737-120">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span></span> <span data-ttu-id="2b737-121">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span><span class="sxs-lookup"><span data-stu-id="2b737-121">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="2b737-122">Intermittent problem error</span><span class="sxs-lookup"><span data-stu-id="2b737-122">Intermittent problem error</span></span>
* <span data-ttu-id="2b737-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="2b737-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="2b737-124">try again later.</span><span class="sxs-lookup"><span data-stu-id="2b737-124">try again later.</span></span>

<span data-ttu-id="2b737-125">This error indicates that an intermittent service side issue has occurred.</span><span class="sxs-lookup"><span data-stu-id="2b737-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="2b737-126">It can be resolved by attempting to consent to the application again.</span><span class="sxs-lookup"><span data-stu-id="2b737-126">It can be resolved by attempting to consent to the application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="2b737-127">Resource not available error</span><span class="sxs-lookup"><span data-stu-id="2b737-127">Resource not available error</span></span>
* <span data-ttu-id="2b737-128">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span><span class="sxs-lookup"><span data-stu-id="2b737-128">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="2b737-129">Contact the application developer.</span><span class="sxs-lookup"><span data-stu-id="2b737-129">Contact the application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="2b737-130">Resource not available in tenant error</span><span class="sxs-lookup"><span data-stu-id="2b737-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="2b737-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="2b737-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="2b737-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="2b737-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="2b737-133">Permissions mismatch error</span><span class="sxs-lookup"><span data-stu-id="2b737-133">Permissions mismatch error</span></span>
* <span data-ttu-id="2b737-134">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="2b737-134">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="2b737-135">This request failed because it does not match how the app was pre-configured during app registration.</span><span class="sxs-lookup"><span data-stu-id="2b737-135">This request failed because it does not match how the app was pre-configured during app registration.</span></span> <span data-ttu-id="2b737-136">Contact the app vendor.\*\*</span><span class="sxs-lookup"><span data-stu-id="2b737-136">Contact the app vendor.\*\*</span></span>

<span data-ttu-id="2b737-137">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span><span class="sxs-lookup"><span data-stu-id="2b737-137">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span></span> <span data-ttu-id="2b737-138">This can occur for several reasons:</span><span class="sxs-lookup"><span data-stu-id="2b737-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="2b737-139">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span><span class="sxs-lookup"><span data-stu-id="2b737-139">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span></span> <span data-ttu-id="2b737-140">In this case, the application developer must update the configuration of the client application to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="2b737-140">In this case, the application developer must update the configuration of the client application to resolve this issue.</span></span>

-   <span data-ttu-id="2b737-141">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span><span class="sxs-lookup"><span data-stu-id="2b737-141">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span></span> <span data-ttu-id="2b737-142">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span><span class="sxs-lookup"><span data-stu-id="2b737-142">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span></span> <span data-ttu-id="2b737-143">This can happen in an number of ways, depending on the type of application, including:</span><span class="sxs-lookup"><span data-stu-id="2b737-143">This can happen in an number of ways, depending on the type of application, including:</span></span>

    -   <span data-ttu-id="2b737-144">Acquiring a subscription for the resource application (Microsoft published applications)</span><span class="sxs-lookup"><span data-stu-id="2b737-144">Acquiring a subscription for the resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="2b737-145">Consenting to the resource application</span><span class="sxs-lookup"><span data-stu-id="2b737-145">Consenting to the resource application</span></span>

    -   <span data-ttu-id="2b737-146">Granting the application permissions via the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2b737-146">Granting the application permissions via the Azure Portal</span></span>

    -   <span data-ttu-id="2b737-147">Adding the application from the Azure AD Application Gallery</span><span class="sxs-lookup"><span data-stu-id="2b737-147">Adding the application from the Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b737-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b737-148">Next steps</span></span> 

[<span data-ttu-id="2b737-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span><span class="sxs-lookup"><span data-stu-id="2b737-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="2b737-150">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span><span class="sxs-lookup"><span data-stu-id="2b737-150">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


