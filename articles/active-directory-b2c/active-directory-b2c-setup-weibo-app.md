---
title: Set up sign-up and sign-in with a Weibo account using Azure Active Directory B2C | Microsoft Docs
description: Provide sign-up and sign-in to customers with Weibo accounts in your applications using Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/09/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 06a79250bac977fc4ade7853594c5307bb11d983
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804653"
---
# <a name="set-up-sign-up-and-sign-in-with-a-weibo-account-using-azure-active-directory-b2c"></a><span data-ttu-id="4f76c-103">Set up sign-up and sign-in with a Weibo account using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="4f76c-103">Set up sign-up and sign-in with a Weibo account using Azure Active Directory B2C</span></span>

> [!NOTE]
> <span data-ttu-id="4f76c-104">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="4f76c-104">This feature is in preview.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="4f76c-105">Create a Weibo application</span><span class="sxs-lookup"><span data-stu-id="4f76c-105">Create a Weibo application</span></span>

<span data-ttu-id="4f76c-106">To use a Weibo account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span><span class="sxs-lookup"><span data-stu-id="4f76c-106">To use a Weibo account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span></span> <span data-ttu-id="4f76c-107">If you don’t already have a Weibo account, you can get it at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="4f76c-107">If you don’t already have a Weibo account, you can get it at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

1. <span data-ttu-id="4f76c-108">Sign in to the [Weibo developer portal](http://open.weibo.com/) with your Weibo account credentials.</span><span class="sxs-lookup"><span data-stu-id="4f76c-108">Sign in to the [Weibo developer portal](http://open.weibo.com/) with your Weibo account credentials.</span></span>
2. <span data-ttu-id="4f76c-109">After signing in, select your display name in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="4f76c-109">After signing in, select your display name in the top-right corner.</span></span>
3. <span data-ttu-id="4f76c-110">In the dropdown, select **编辑开发者信息** (edit developer information).</span><span class="sxs-lookup"><span data-stu-id="4f76c-110">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="4f76c-111">Enter the required information and select **提交** (submit).</span><span class="sxs-lookup"><span data-stu-id="4f76c-111">Enter the required information and select **提交** (submit).</span></span>
5. <span data-ttu-id="4f76c-112">Complete the email verification process.</span><span class="sxs-lookup"><span data-stu-id="4f76c-112">Complete the email verification process.</span></span>
6. <span data-ttu-id="4f76c-113">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="4f76c-113">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="4f76c-114">Enter the required information and select **提交** (submit).</span><span class="sxs-lookup"><span data-stu-id="4f76c-114">Enter the required information and select **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="4f76c-115">Register a Weibo application</span><span class="sxs-lookup"><span data-stu-id="4f76c-115">Register a Weibo application</span></span>

1. <span data-ttu-id="4f76c-116">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="4f76c-116">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="4f76c-117">Enter the necessary application information.</span><span class="sxs-lookup"><span data-stu-id="4f76c-117">Enter the necessary application information.</span></span>
3. <span data-ttu-id="4f76c-118">Select **创建** (create).</span><span class="sxs-lookup"><span data-stu-id="4f76c-118">Select **创建** (create).</span></span>
4. <span data-ttu-id="4f76c-119">Copy the values of **App Key** and **App Secret**.</span><span class="sxs-lookup"><span data-stu-id="4f76c-119">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="4f76c-120">You need both of these to add the identity provider to your tenant.</span><span class="sxs-lookup"><span data-stu-id="4f76c-120">You need both of these to add the identity provider to your tenant.</span></span>
5. <span data-ttu-id="4f76c-121">Upload the required photos and enter the necessary information.</span><span class="sxs-lookup"><span data-stu-id="4f76c-121">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="4f76c-122">Select **保存以上信息** (save).</span><span class="sxs-lookup"><span data-stu-id="4f76c-122">Select **保存以上信息** (save).</span></span>
7. <span data-ttu-id="4f76c-123">Select **高级信息** (advanced information).</span><span class="sxs-lookup"><span data-stu-id="4f76c-123">Select **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="4f76c-124">Select **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span><span class="sxs-lookup"><span data-stu-id="4f76c-124">Select **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="4f76c-125">Enter `https://{tenant_name}.b2clogin.com/te/{tenant_name}.onmicrosoft.com/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span><span class="sxs-lookup"><span data-stu-id="4f76c-125">Enter `https://{tenant_name}.b2clogin.com/te/{tenant_name}.onmicrosoft.com/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="4f76c-126">For example, if your `tenant_name` is contoso, set the URL to be `https://contoso.b2clogin.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="4f76c-126">For example, if your `tenant_name` is contoso, set the URL to be `https://contoso.b2clogin.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="4f76c-127">Select **提交** (submit).</span><span class="sxs-lookup"><span data-stu-id="4f76c-127">Select **提交** (submit).</span></span>  

## <a name="configure-a-weibo-account-as-an-identity-provider"></a><span data-ttu-id="4f76c-128">Configure a Weibo account as an identity provider</span><span class="sxs-lookup"><span data-stu-id="4f76c-128">Configure a Weibo account as an identity provider</span></span>

1. <span data-ttu-id="4f76c-129">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="4f76c-129">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="4f76c-130">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4f76c-130">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="4f76c-131">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f76c-131">Select your subscription information, and then select **Switch Directory**.</span></span> 

    ![Switch to your Azure AD B2C tenant](./media/active-directory-b2c-setup-weibo-app/switch-directories.png)

    <span data-ttu-id="4f76c-133">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="4f76c-133">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-setup-weibo-app/select-directory.png)

3. <span data-ttu-id="4f76c-135">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="4f76c-135">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span>
4. <span data-ttu-id="4f76c-136">Select **Identity providers**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="4f76c-136">Select **Identity providers**, and then select **Add**.</span></span>
5. <span data-ttu-id="4f76c-137">Provide a **Name**.</span><span class="sxs-lookup"><span data-stu-id="4f76c-137">Provide a **Name**.</span></span> <span data-ttu-id="4f76c-138">For example, enter *Weibo*.</span><span class="sxs-lookup"><span data-stu-id="4f76c-138">For example, enter *Weibo*.</span></span>
6. <span data-ttu-id="4f76c-139">Select **Identity provider type**, select **Weibo (Preview)**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f76c-139">Select **Identity provider type**, select **Weibo (Preview)**, and click **OK**.</span></span>
7. <span data-ttu-id="4f76c-140">Select **Set up this identity provider** and enter the App Key that you recorded earlier as the **Client ID** and enter the App Secret that you recorded as the **Client secret** of the Weibo application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="4f76c-140">Select **Set up this identity provider** and enter the App Key that you recorded earlier as the **Client ID** and enter the App Secret that you recorded as the **Client secret** of the Weibo application that you created earlier.</span></span>
8. <span data-ttu-id="4f76c-141">Click **OK** and then click **Create** to save your Weibo configuration.</span><span class="sxs-lookup"><span data-stu-id="4f76c-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>
