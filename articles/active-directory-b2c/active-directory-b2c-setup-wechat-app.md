---
title: 'Azure Active Directory B2C: WeChat configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with WeChat accounts in your applications that are secured by Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: ''
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 3195ce5830a3bcd862c524b4133d45626a6ab270
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661562"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="f27a6-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span><span class="sxs-lookup"><span data-stu-id="f27a6-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="f27a6-104">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="f27a6-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="f27a6-105">Create a WeChat application</span><span class="sxs-lookup"><span data-stu-id="f27a6-105">Create a WeChat application</span></span>

<span data-ttu-id="f27a6-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="f27a6-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="f27a6-107">You need a WeChat account to do this.</span><span class="sxs-lookup"><span data-stu-id="f27a6-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="f27a6-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span><span class="sxs-lookup"><span data-stu-id="f27a6-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="f27a6-109">After that, get your account registered with the WeChat developer program.</span><span class="sxs-lookup"><span data-stu-id="f27a6-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="f27a6-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="f27a6-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="f27a6-111">Register a WeChat application</span><span class="sxs-lookup"><span data-stu-id="f27a6-111">Register a WeChat application</span></span>

1. <span data-ttu-id="f27a6-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span><span class="sxs-lookup"><span data-stu-id="f27a6-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="f27a6-113">Click on **管理中心** (management center).</span><span class="sxs-lookup"><span data-stu-id="f27a6-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="f27a6-114">Follow the necessary steps to register a new application.</span><span class="sxs-lookup"><span data-stu-id="f27a6-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="f27a6-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f27a6-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="f27a6-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f27a6-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="f27a6-117">Find and copy the **APP ID** and **APP KEY**.</span><span class="sxs-lookup"><span data-stu-id="f27a6-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="f27a6-118">You will need these later.</span><span class="sxs-lookup"><span data-stu-id="f27a6-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f27a6-119">Configure WeChat as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="f27a6-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f27a6-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f27a6-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="f27a6-121">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="f27a6-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f27a6-122">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="f27a6-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="f27a6-123">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="f27a6-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="f27a6-124">For example, enter "WeChat".</span><span class="sxs-lookup"><span data-stu-id="f27a6-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="f27a6-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f27a6-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="f27a6-126">Click **Set up this identity provider**</span><span class="sxs-lookup"><span data-stu-id="f27a6-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="f27a6-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span><span class="sxs-lookup"><span data-stu-id="f27a6-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="f27a6-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="f27a6-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="f27a6-129">Click **OK** and then click **Create** to save your WeChat configuration.</span><span class="sxs-lookup"><span data-stu-id="f27a6-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

