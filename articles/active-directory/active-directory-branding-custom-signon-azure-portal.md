---
title: Customize your sign-in page in the Azure Active Directory preview | Microsoft Docs
description: Learn how to add a company branding to the Azure sign-in page
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 4f8f6c0a810847d9348fb935982daec560bd89f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553746"
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory-preview"></a><span data-ttu-id="2e813-103">Add company branding to your sign-in page in the Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="2e813-103">Add company branding to your sign-in page in the Azure Active Directory preview</span></span>
<span data-ttu-id="2e813-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span><span class="sxs-lookup"><span data-stu-id="2e813-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="2e813-105">Azure Active Directory preview provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span><span class="sxs-lookup"><span data-stu-id="2e813-105">Azure Active Directory preview provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> [<span data-ttu-id="2e813-106">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="2e813-106">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="2e813-107">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span><span class="sxs-lookup"><span data-stu-id="2e813-107">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="2e813-108">You interact with this page to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="2e813-108">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="2e813-109">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span><span class="sxs-lookup"><span data-stu-id="2e813-109">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="2e813-110">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span><span class="sxs-lookup"><span data-stu-id="2e813-110">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Office 365 sign-in page before customization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="2e813-112">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span><span class="sxs-lookup"><span data-stu-id="2e813-112">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Office 365 sign-in page after customization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="2e813-114">Customizing the sign-in page</span><span class="sxs-lookup"><span data-stu-id="2e813-114">Customizing the sign-in page</span></span>
<span data-ttu-id="2e813-115">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="2e813-115">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="2e813-116">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span><span class="sxs-lookup"><span data-stu-id="2e813-116">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="2e813-117">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="2e813-117">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="2e813-118">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span><span class="sxs-lookup"><span data-stu-id="2e813-118">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="2e813-119">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span><span class="sxs-lookup"><span data-stu-id="2e813-119">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="2e813-120">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span><span class="sxs-lookup"><span data-stu-id="2e813-120">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="2e813-121">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e813-121">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="2e813-122">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e813-122">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="2e813-123">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span><span class="sxs-lookup"><span data-stu-id="2e813-123">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="2e813-124">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span><span class="sxs-lookup"><span data-stu-id="2e813-124">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Keep me signed-in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="2e813-126">It does not effect session lifetime.</span><span class="sxs-lookup"><span data-stu-id="2e813-126">It does not effect session lifetime.</span></span> <span data-ttu-id="2e813-127">You can hide the checkbox on the Azure Active Directory sign-in page.</span><span class="sxs-lookup"><span data-stu-id="2e813-127">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="2e813-128">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span><span class="sxs-lookup"><span data-stu-id="2e813-128">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Keep me signed-in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="2e813-130">To hide the checkbox, configure this setting to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="2e813-130">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="2e813-131">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span><span class="sxs-lookup"><span data-stu-id="2e813-131">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="2e813-132">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span><span class="sxs-lookup"><span data-stu-id="2e813-132">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="2e813-133">**To add company branding to your directory:**</span><span class="sxs-lookup"><span data-stu-id="2e813-133">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="2e813-134">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="2e813-134">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="2e813-135">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="2e813-135">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="2e813-137">On the **Users and groups** blade, select **Company branding**.</span><span class="sxs-lookup"><span data-stu-id="2e813-137">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="2e813-138">On the **Users and groups - Company branding** blade, select the **Edit** command.</span><span class="sxs-lookup"><span data-stu-id="2e813-138">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Edit custom branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="2e813-140">Modify the elements you want to customize.</span><span class="sxs-lookup"><span data-stu-id="2e813-140">Modify the elements you want to customize.</span></span> <span data-ttu-id="2e813-141">All elements are optional.</span><span class="sxs-lookup"><span data-stu-id="2e813-141">All elements are optional.</span></span>
6. <span data-ttu-id="2e813-142">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2e813-142">Click **Save**.</span></span>

<span data-ttu-id="2e813-143">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span><span class="sxs-lookup"><span data-stu-id="2e813-143">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e813-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="2e813-144">Next steps</span></span>
[<span data-ttu-id="2e813-145">Add language-specific company branding</span><span class="sxs-lookup"><span data-stu-id="2e813-145">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)






