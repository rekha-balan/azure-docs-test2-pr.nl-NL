---
title: View tenant applications - Azure Active Directory | Microsoft Docs
description: Use the Azure portal to view the applications in your Azure Active Directory (Azure AD) tenant.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/25/2018
ms.author: barbkess
ms.reviewer: arvinh
ms.custom: it-pro
ms.openlocfilehash: bedd83426ecb24681fcfa292a049b8d4a3271d6a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857045"
---
# <a name="view-your-azure-active-directory-tenant-applications"></a><span data-ttu-id="fbd02-103">View your Azure Active Directory tenant applications</span><span class="sxs-lookup"><span data-stu-id="fbd02-103">View your Azure Active Directory tenant applications</span></span>

<span data-ttu-id="fbd02-104">This quickstart uses the Azure portal to view the applications in your Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="fbd02-104">This quickstart uses the Azure portal to view the applications in your Azure Active Directory (Azure AD) tenant.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fbd02-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="fbd02-105">Before you begin</span></span>

<span data-ttu-id="fbd02-106">To see results, you need to have at least one application in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fbd02-106">To see results, you need to have at least one application in your Azure AD tenant.</span></span> <span data-ttu-id="fbd02-107">To add an application, see the [Add an application](add-application-portal.md) quickstart.</span><span class="sxs-lookup"><span data-stu-id="fbd02-107">To add an application, see the [Add an application](add-application-portal.md) quickstart.</span></span>

<span data-ttu-id="fbd02-108">Sign in to the [Azure portal](https://portal.azure.com) as a global admin for your Azure AD tenant, a cloud application admin, or an application admin.</span><span class="sxs-lookup"><span data-stu-id="fbd02-108">Sign in to the [Azure portal](https://portal.azure.com) as a global admin for your Azure AD tenant, a cloud application admin, or an application admin.</span></span>

## <a name="find-the-list-of-tenant-applications"></a><span data-ttu-id="fbd02-109">Find the list of tenant applications</span><span class="sxs-lookup"><span data-stu-id="fbd02-109">Find the list of tenant applications</span></span>

<span data-ttu-id="fbd02-110">Your Azure AD tenant applications are viewable in the **Enterprise apps** section of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fbd02-110">Your Azure AD tenant applications are viewable in the **Enterprise apps** section of the Azure portal.</span></span>

<span data-ttu-id="fbd02-111">To find your tenant applications:</span><span class="sxs-lookup"><span data-stu-id="fbd02-111">To find your tenant applications:</span></span>

1. <span data-ttu-id="fbd02-112">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-112">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="fbd02-113">In the Azure Active Directory blade, click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-113">In the Azure Active Directory blade, click **Enterprise applications**.</span></span> 

3. <span data-ttu-id="fbd02-114">From the **Application Type** drop-down menu, select **All Applications**, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-114">From the **Application Type** drop-down menu, select **All Applications**, and click **Apply**.</span></span> <span data-ttu-id="fbd02-115">A random sample of your tenant applications appears.</span><span class="sxs-lookup"><span data-stu-id="fbd02-115">A random sample of your tenant applications appears.</span></span>

    ![Enterprise apps](media/view-applications-portal/open-enterprise-apps.png)
   
4. <span data-ttu-id="fbd02-117">To view more applications, click **Show more** at the bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="fbd02-117">To view more applications, click **Show more** at the bottom of the list.</span></span> <span data-ttu-id="fbd02-118">Depending on the number of applications in your tenant, it might be easier to [search for a particular application](#search-for-a-tenant-application), instead of scrolling through the list.</span><span class="sxs-lookup"><span data-stu-id="fbd02-118">Depending on the number of applications in your tenant, it might be easier to [search for a particular application](#search-for-a-tenant-application), instead of scrolling through the list.</span></span>

## <a name="select-viewing-options"></a><span data-ttu-id="fbd02-119">Select viewing options</span><span class="sxs-lookup"><span data-stu-id="fbd02-119">Select viewing options</span></span>

<span data-ttu-id="fbd02-120">In this section, select the options according to what you are looking for.</span><span class="sxs-lookup"><span data-stu-id="fbd02-120">In this section, select the options according to what you are looking for.</span></span>

1. <span data-ttu-id="fbd02-121">You can view the applications according to options for **Application Type**, **Application Status**, and **Application visibility**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-121">You can view the applications according to options for **Application Type**, **Application Status**, and **Application visibility**.</span></span> 

    ![Options for searching](media/view-applications-portal/search-options.png)

2. <span data-ttu-id="fbd02-123">Under **Application Type**, choose one of these options:</span><span class="sxs-lookup"><span data-stu-id="fbd02-123">Under **Application Type**, choose one of these options:</span></span>

    - <span data-ttu-id="fbd02-124">**Enterprise Applications** shows non-Microsoft applications.</span><span class="sxs-lookup"><span data-stu-id="fbd02-124">**Enterprise Applications** shows non-Microsoft applications.</span></span>
    - <span data-ttu-id="fbd02-125">**Microsoft Applications** shows Microsoft applications.</span><span class="sxs-lookup"><span data-stu-id="fbd02-125">**Microsoft Applications** shows Microsoft applications.</span></span>
    - <span data-ttu-id="fbd02-126">**All Applications** shows both non-Microsoft and Microsoft applications.</span><span class="sxs-lookup"><span data-stu-id="fbd02-126">**All Applications** shows both non-Microsoft and Microsoft applications.</span></span>

3. <span data-ttu-id="fbd02-127">Under **Application Status**, choose **Any**, **Disabled**, or **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-127">Under **Application Status**, choose **Any**, **Disabled**, or **Enabled**.</span></span> <span data-ttu-id="fbd02-128">The **Any** option includes both disabled and enabled applications.</span><span class="sxs-lookup"><span data-stu-id="fbd02-128">The **Any** option includes both disabled and enabled applications.</span></span>

4. <span data-ttu-id="fbd02-129">Under **Application Visibility**, choose **Any**, or **Hidden**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-129">Under **Application Visibility**, choose **Any**, or **Hidden**.</span></span> <span data-ttu-id="fbd02-130">The **Hidden** option shows applications that are in the tenant, but are not visible to users.</span><span class="sxs-lookup"><span data-stu-id="fbd02-130">The **Hidden** option shows applications that are in the tenant, but are not visible to users.</span></span>

5. <span data-ttu-id="fbd02-131">After choosing the options you want, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-131">After choosing the options you want, click **Apply**.</span></span>
 

## <a name="search-for-a-tenant-application"></a><span data-ttu-id="fbd02-132">Search for a tenant application</span><span class="sxs-lookup"><span data-stu-id="fbd02-132">Search for a tenant application</span></span>

<span data-ttu-id="fbd02-133">To search for an particular application:</span><span class="sxs-lookup"><span data-stu-id="fbd02-133">To search for an particular application:</span></span>

1. <span data-ttu-id="fbd02-134">In the **Application Type** menu, select **All applications**, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-134">In the **Application Type** menu, select **All applications**, and click **Apply**.</span></span>

2. <span data-ttu-id="fbd02-135">Enter the name of the application you want to find.</span><span class="sxs-lookup"><span data-stu-id="fbd02-135">Enter the name of the application you want to find.</span></span> <span data-ttu-id="fbd02-136">If the application has been added to your Azure AD tenant, it will appear in the search results.</span><span class="sxs-lookup"><span data-stu-id="fbd02-136">If the application has been added to your Azure AD tenant, it will appear in the search results.</span></span> <span data-ttu-id="fbd02-137">This example shows that GitHub has not been added to the tenant applications.</span><span class="sxs-lookup"><span data-stu-id="fbd02-137">This example shows that GitHub has not been added to the tenant applications.</span></span>

    ![Search for an application](media/view-applications-portal/search-for-tenant-application.png)

3. <span data-ttu-id="fbd02-139">Try entering the first few letters of an application name.</span><span class="sxs-lookup"><span data-stu-id="fbd02-139">Try entering the first few letters of an application name.</span></span>  <span data-ttu-id="fbd02-140">This example shows all the applications that start with **Sales**.</span><span class="sxs-lookup"><span data-stu-id="fbd02-140">This example shows all the applications that start with **Sales**.</span></span>

    ![Search with a prefix](media/view-applications-portal/search-by-prefix.png)

## <a name="next-steps"></a><span data-ttu-id="fbd02-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbd02-142">Next steps</span></span>

<span data-ttu-id="fbd02-143">In this quickstart, you learned how to view the applications in your Azure AD tenant, and how to filter the list of applications by application type, status, and visibility.</span><span class="sxs-lookup"><span data-stu-id="fbd02-143">In this quickstart, you learned how to view the applications in your Azure AD tenant, and how to filter the list of applications by application type, status, and visibility.</span></span> <span data-ttu-id="fbd02-144">You also learned how to search for a particular application.</span><span class="sxs-lookup"><span data-stu-id="fbd02-144">You also learned how to search for a particular application.</span></span>

<span data-ttu-id="fbd02-145">Now that you have found the application you were looking for, you can continue to [Add more applications to your tenant](add-application-portal.md), or click the application to view or edit properties and configuration options.</span><span class="sxs-lookup"><span data-stu-id="fbd02-145">Now that you have found the application you were looking for, you can continue to [Add more applications to your tenant](add-application-portal.md), or click the application to view or edit properties and configuration options.</span></span> <span data-ttu-id="fbd02-146">For example, you could configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbd02-146">For example, you could configure single sign-on.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbd02-147">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="fbd02-147">Configure single sign-on</span></span>](configure-single-sign-on-portal.md)


