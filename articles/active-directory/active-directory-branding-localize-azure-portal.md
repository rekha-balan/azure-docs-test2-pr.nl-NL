---
title: Add language-specific company branding to your sign-in page in the Azure Active Directory preview | Microsoft Docs
description: Learn how to add a language specific company branding pictures and text to an Azure sign-in page
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: curtand
ms.openlocfilehash: 3e9b3dbd56b430117be95614d62644ef8fcb266a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540652"
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory-preview"></a><span data-ttu-id="b01bf-103">Add language-specific company branding to your sign-in page in the Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="b01bf-103">Add language-specific company branding to your sign-in page in the Azure Active Directory preview</span></span>
<span data-ttu-id="b01bf-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span><span class="sxs-lookup"><span data-stu-id="b01bf-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="b01bf-105">Azure Active Directory preview provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span><span class="sxs-lookup"><span data-stu-id="b01bf-105">Azure Active Directory preview provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> [<span data-ttu-id="b01bf-106">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="b01bf-106">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="b01bf-107">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span><span class="sxs-lookup"><span data-stu-id="b01bf-107">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="b01bf-108">You interact with this page to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="b01bf-108">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="b01bf-109">Customizing the sign-in page for another language</span><span class="sxs-lookup"><span data-stu-id="b01bf-109">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="b01bf-110">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b01bf-110">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="b01bf-111">You can configure one sign-in page per directory with a default set of customizable elements.</span><span class="sxs-lookup"><span data-stu-id="b01bf-111">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="b01bf-112">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span><span class="sxs-lookup"><span data-stu-id="b01bf-112">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="b01bf-113">You can also mix and match various elements.</span><span class="sxs-lookup"><span data-stu-id="b01bf-113">You can also mix and match various elements.</span></span> <span data-ttu-id="b01bf-114">For example, you could:</span><span class="sxs-lookup"><span data-stu-id="b01bf-114">For example, you could:</span></span>

* <span data-ttu-id="b01bf-115">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span><span class="sxs-lookup"><span data-stu-id="b01bf-115">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="b01bf-116">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span><span class="sxs-lookup"><span data-stu-id="b01bf-116">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="b01bf-117">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span><span class="sxs-lookup"><span data-stu-id="b01bf-117">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="b01bf-118">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span><span class="sxs-lookup"><span data-stu-id="b01bf-118">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="b01bf-119">**To add company branding to your directory:**</span><span class="sxs-lookup"><span data-stu-id="b01bf-119">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="b01bf-120">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="b01bf-120">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="b01bf-121">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b01bf-121">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="b01bf-123">On the **Users and groups** blade, select **Company branding**.</span><span class="sxs-lookup"><span data-stu-id="b01bf-123">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="b01bf-124">On the **Users and groups - Company branding** blade, select the **Add language** command.</span><span class="sxs-lookup"><span data-stu-id="b01bf-124">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Add language-specific branding elements](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="b01bf-126">Modify the elements you want to customize.</span><span class="sxs-lookup"><span data-stu-id="b01bf-126">Modify the elements you want to customize.</span></span> <span data-ttu-id="b01bf-127">All elements are optional.</span><span class="sxs-lookup"><span data-stu-id="b01bf-127">All elements are optional.</span></span>
6. <span data-ttu-id="b01bf-128">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b01bf-128">Click **Save**.</span></span>

<span data-ttu-id="b01bf-129">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span><span class="sxs-lookup"><span data-stu-id="b01bf-129">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b01bf-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="b01bf-130">Next steps</span></span>
[<span data-ttu-id="b01bf-131">Add company branding to your sign-in page</span><span class="sxs-lookup"><span data-stu-id="b01bf-131">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)


