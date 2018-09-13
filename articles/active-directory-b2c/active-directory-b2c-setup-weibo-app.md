---
title: 'Azure Active Directory B2C: Weibo configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with Weibo accounts in your applications that are secured by Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: ''
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: b6fdb9311ca2be3752c4ef74c91fe7abe9a91210
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548718"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="74065-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span><span class="sxs-lookup"><span data-stu-id="74065-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="74065-104">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="74065-104">This feature is in preview.</span></span> <span data-ttu-id="74065-105">Do not use this identity provider in your production environment.</span><span class="sxs-lookup"><span data-stu-id="74065-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="74065-106">Create a Weibo application</span><span class="sxs-lookup"><span data-stu-id="74065-106">Create a Weibo application</span></span>

<span data-ttu-id="74065-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="74065-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="74065-108">You need a Weibo account to do this.</span><span class="sxs-lookup"><span data-stu-id="74065-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="74065-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="74065-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="74065-110">Register for the Weibo developer program</span><span class="sxs-lookup"><span data-stu-id="74065-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="74065-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span><span class="sxs-lookup"><span data-stu-id="74065-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="74065-112">After signing in, click on your display name in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="74065-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="74065-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span><span class="sxs-lookup"><span data-stu-id="74065-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="74065-114">Enter the required information into the form and click **提交** (submit).</span><span class="sxs-lookup"><span data-stu-id="74065-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="74065-115">Complete the email verification process.</span><span class="sxs-lookup"><span data-stu-id="74065-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="74065-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="74065-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="74065-117">Enter the required information into the form and click **提交** (submit).</span><span class="sxs-lookup"><span data-stu-id="74065-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="74065-118">Register a Weibo application</span><span class="sxs-lookup"><span data-stu-id="74065-118">Register a Weibo application</span></span>

1. <span data-ttu-id="74065-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="74065-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="74065-120">Enter the necessary application information.</span><span class="sxs-lookup"><span data-stu-id="74065-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="74065-121">Click **创建** (create).</span><span class="sxs-lookup"><span data-stu-id="74065-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="74065-122">Copy the values of **App Key** and **App Secret**.</span><span class="sxs-lookup"><span data-stu-id="74065-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="74065-123">You will need this later.</span><span class="sxs-lookup"><span data-stu-id="74065-123">You will need this later.</span></span>
5. <span data-ttu-id="74065-124">Upload the required photos and enter the necessary information.</span><span class="sxs-lookup"><span data-stu-id="74065-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="74065-125">Click **保存以上信息** (save).</span><span class="sxs-lookup"><span data-stu-id="74065-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="74065-126">Click **高级信息** (advanced information).</span><span class="sxs-lookup"><span data-stu-id="74065-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="74065-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span><span class="sxs-lookup"><span data-stu-id="74065-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="74065-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span><span class="sxs-lookup"><span data-stu-id="74065-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="74065-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="74065-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="74065-130">Click **提交** (submit).</span><span class="sxs-lookup"><span data-stu-id="74065-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="74065-131">Configure Weibo as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="74065-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="74065-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="74065-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="74065-133">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="74065-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="74065-134">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="74065-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="74065-135">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="74065-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="74065-136">For example, enter "Weibo".</span><span class="sxs-lookup"><span data-stu-id="74065-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="74065-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="74065-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="74065-138">Click **Set up this identity provider**</span><span class="sxs-lookup"><span data-stu-id="74065-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="74065-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span><span class="sxs-lookup"><span data-stu-id="74065-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="74065-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="74065-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="74065-141">Click **OK** and then click **Create** to save your Weibo configuration.</span><span class="sxs-lookup"><span data-stu-id="74065-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

