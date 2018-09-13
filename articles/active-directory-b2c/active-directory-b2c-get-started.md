---
title: 'Azure Active Directory B2C: Create an Azure Active Directory B2C tenant | Microsoft Docs'
description: A topic on how to create an Azure Active Directory B2C tenant
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 59fe4a8ef49e906a2ba10a648807407bdcaa2667
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555088"
---
# <a name="azure-active-directory-b2c-create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="0fb8a-103">Azure Active Directory B2C: Create an Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="0fb8a-103">Azure Active Directory B2C: Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="0fb8a-104">To start using Microsoft Azure Active Directory (Azure AD) B2C, follow the four steps outlined in this article.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-104">To start using Microsoft Azure Active Directory (Azure AD) B2C, follow the four steps outlined in this article.</span></span>

## <a name="step-1-sign-up-for-an-azure-subscription"></a><span data-ttu-id="0fb8a-105">Step 1: Sign up for an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0fb8a-105">Step 1: Sign up for an Azure subscription</span></span>
<span data-ttu-id="0fb8a-106">If you already have an Azure subscription, skip this step.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-106">If you already have an Azure subscription, skip this step.</span></span> <span data-ttu-id="0fb8a-107">If not, sign up for an [Azure subscription](../active-directory/sign-up-organization.md) and get access to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-107">If not, sign up for an [Azure subscription](../active-directory/sign-up-organization.md) and get access to Azure AD B2C.</span></span>

## <a name="step-2-create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="0fb8a-108">Step 2: Create an Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="0fb8a-108">Step 2: Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="0fb8a-109">Use the following steps to create a new Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-109">Use the following steps to create a new Azure AD B2C tenant.</span></span> <span data-ttu-id="0fb8a-110">Currently B2C features can't be turned on in your existing tenants.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-110">Currently B2C features can't be turned on in your existing tenants.</span></span>

1. <span data-ttu-id="0fb8a-111">Sign in to the [Azure portal](https://portal.azure.com/) as the Subscription Administrator.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-111">Sign in to the [Azure portal](https://portal.azure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="0fb8a-112">This is the same work or school account or the same Microsoft account that you used to sign up for Azure.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-112">This is the same work or school account or the same Microsoft account that you used to sign up for Azure.</span></span>
2. <span data-ttu-id="0fb8a-113">Click **New**(or the + button if collapsed) and in the **Search the marketplace** field enter "Azure Active Directory B2C".</span><span class="sxs-lookup"><span data-stu-id="0fb8a-113">Click **New**(or the + button if collapsed) and in the **Search the marketplace** field enter "Azure Active Directory B2C".</span></span>
   
    ![Screen shot of finding the Azure AD B2C option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-get-started/find-azure-ad-b2c.png)
3. <span data-ttu-id="0fb8a-115">In the result, click on **Azure Active Directory B2C**</span><span class="sxs-lookup"><span data-stu-id="0fb8a-115">In the result, click on **Azure Active Directory B2C**</span></span>

    ![Screen shot of result for Azure Active Directory B2C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-get-started/find-azure-ad-b2c-result.png)
4. <span data-ttu-id="0fb8a-117">You'll be shown a page with the details on B2C.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-117">You'll be shown a page with the details on B2C.</span></span>  <span data-ttu-id="0fb8a-118">Click **Create** at the bottom to start configuring your new Azure Active Directory B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-118">Click **Create** at the bottom to start configuring your new Azure Active Directory B2C tenant.</span></span>
5. <span data-ttu-id="0fb8a-119">Click **Create a new Azure AD B2C Tenant**.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-119">Click **Create a new Azure AD B2C Tenant**.</span></span>
6. <span data-ttu-id="0fb8a-120">Choose the **Organization name, Domain name, and Country or Region** for your tenant.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-120">Choose the **Organization name, Domain name, and Country or Region** for your tenant.</span></span>

    ![Screen shot of the form for creating a new tenant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-get-started/create-new-b2c-tenant.png)
7. <span data-ttu-id="0fb8a-122">Click **Create** to create your tenant.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-122">Click **Create** to create your tenant.</span></span>  <span data-ttu-id="0fb8a-123">This may take a few minutes, you will be alerted in your notifications when it is complete.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-123">This may take a few minutes, you will be alerted in your notifications when it is complete.</span></span>

8. <span data-ttu-id="0fb8a-124">Your tenant is now created and will appear in the Active Directory extension.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-124">Your tenant is now created and will appear in the Active Directory extension.</span></span> <span data-ttu-id="0fb8a-125">You are also made a Global Administrator of the tenant.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-125">You are also made a Global Administrator of the tenant.</span></span> <span data-ttu-id="0fb8a-126">You can add other Global Administrators as required.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-126">You can add other Global Administrators as required.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0fb8a-127">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="0fb8a-127">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="0fb8a-128">Note that there are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-128">Note that there are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="0fb8a-129">You have to create a B2C tenant with a different domain name.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-129">You have to create a B2C tenant with a different domain name.</span></span>
   > 
   > 

## <a name="step-3-navigate-to-the-b2c-features-blade-on-the-azure-portal"></a><span data-ttu-id="0fb8a-130">Step 3: Navigate to the B2C features blade on the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0fb8a-130">Step 3: Navigate to the B2C features blade on the Azure portal</span></span>
1. <span data-ttu-id="0fb8a-131">Expand **More services** below the navigation bar on the left side.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-131">Expand **More services** below the navigation bar on the left side.</span></span>
2. <span data-ttu-id="0fb8a-132">Search for **Azure AD B2C** and click on the result (You can favorite this for easy access in the future).</span><span class="sxs-lookup"><span data-stu-id="0fb8a-132">Search for **Azure AD B2C** and click on the result (You can favorite this for easy access in the future).</span></span>

    ![Screen shot of searching in the navigation pane for Azure AD B2C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-get-started/navigate-to-azure-ad-b2c.png)

3. <span data-ttu-id="0fb8a-134">The Azure portal with the B2C features blade showing will open in a new browser tab or window.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-134">The Azure portal with the B2C features blade showing will open in a new browser tab or window.</span></span>
   
4. <span data-ttu-id="0fb8a-135">Pin this blade to your Startboard for easy access.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-135">Pin this blade to your Startboard for easy access.</span></span> <span data-ttu-id="0fb8a-136">(The Pin tool is in the upper-right corner of the features blade.)</span><span class="sxs-lookup"><span data-stu-id="0fb8a-136">(The Pin tool is in the upper-right corner of the features blade.)</span></span>
   
    ![Screen shot of the B2C features blade and pin button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-get-started/b2c-pin-tenant.png)

## <a name="step-4-link-your-azure-ad-b2c-tenant-to-your-azure-subscription"></a><span data-ttu-id="0fb8a-138">Step 4: Link your Azure AD B2C tenant to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0fb8a-138">Step 4: Link your Azure AD B2C tenant to your Azure subscription</span></span>
<span data-ttu-id="0fb8a-139">If you are planning to use your B2C tenant for production apps, you will need to link your Azure AD B2C tenant to your Azure subscription to pay for usage charges.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-139">If you are planning to use your B2C tenant for production apps, you will need to link your Azure AD B2C tenant to your Azure subscription to pay for usage charges.</span></span> <span data-ttu-id="0fb8a-140">Read [this article](active-directory-b2c-how-to-enable-billing.md) to learn how to do this.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-140">Read [this article](active-directory-b2c-how-to-enable-billing.md) to learn how to do this.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0fb8a-141">If you don't link your Azure AD B2C tenant to your Azure subscription, you will see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") on the B2C features blade on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-141">If you don't link your Azure AD B2C tenant to your Azure subscription, you will see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") on the B2C features blade on the Azure portal.</span></span> <span data-ttu-id="0fb8a-142">It is important that you take this step before you ship your apps into production.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-142">It is important that you take this step before you ship your apps into production.</span></span>
   > 
   > 

## <a name="easy-access-to-the-b2c-features-blade-on-the-azure-portal"></a><span data-ttu-id="0fb8a-143">Easy access to the B2C features blade on the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0fb8a-143">Easy access to the B2C features blade on the Azure portal</span></span>
<span data-ttu-id="0fb8a-144">To improve discoverability, we've added a shortcut to the B2C features blade on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-144">To improve discoverability, we've added a shortcut to the B2C features blade on the Azure portal.</span></span>

1. <span data-ttu-id="0fb8a-145">Sign into the Azure portal as the Global Administrator of your B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-145">Sign into the Azure portal as the Global Administrator of your B2C tenant.</span></span> <span data-ttu-id="0fb8a-146">If you are already signed into a different tenant, switch tenants (on the top-right corner).</span><span class="sxs-lookup"><span data-stu-id="0fb8a-146">If you are already signed into a different tenant, switch tenants (on the top-right corner).</span></span>
2. <span data-ttu-id="0fb8a-147">Click **Browse** on the left hand navigation.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-147">Click **Browse** on the left hand navigation.</span></span>
3. <span data-ttu-id="0fb8a-148">Click **Azure AD B2C** to access the B2C features blade.</span><span class="sxs-lookup"><span data-stu-id="0fb8a-148">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Screen shot of Browse to B2C features blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-get-started/b2c-browse.png)

## <a name="next-steps"></a><span data-ttu-id="0fb8a-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fb8a-150">Next steps</span></span>
<span data-ttu-id="0fb8a-151">Learn how to register an application with Azure AD B2C and to build a Quick Start application by reading [Azure Active Directory B2C: Register your application](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="0fb8a-151">Learn how to register an application with Azure AD B2C and to build a Quick Start application by reading [Azure Active Directory B2C: Register your application](active-directory-b2c-app-registration.md).</span></span>







