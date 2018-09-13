---
title: 'Azure Active Directory B2C: QQ configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with QQ accounts in your applications that are secured by Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: ''
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 2079e7e461800928c2253665d755f3d506b88fcc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550075"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="6bf20-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span><span class="sxs-lookup"><span data-stu-id="6bf20-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="6bf20-104">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="6bf20-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="6bf20-105">Create a QQ application</span><span class="sxs-lookup"><span data-stu-id="6bf20-105">Create a QQ application</span></span>

<span data-ttu-id="6bf20-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="6bf20-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="6bf20-107">You need a QQ account to do this.</span><span class="sxs-lookup"><span data-stu-id="6bf20-107">You need a QQ account to do this.</span></span> <span data-ttu-id="6bf20-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="6bf20-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="6bf20-109">Register for the QQ developer program</span><span class="sxs-lookup"><span data-stu-id="6bf20-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="6bf20-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span><span class="sxs-lookup"><span data-stu-id="6bf20-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="6bf20-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span><span class="sxs-lookup"><span data-stu-id="6bf20-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="6bf20-112">In the menu, select **个人** (individual developer).</span><span class="sxs-lookup"><span data-stu-id="6bf20-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="6bf20-113">Enter the required information into the form and click **下一步** (next step).</span><span class="sxs-lookup"><span data-stu-id="6bf20-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="6bf20-114">Complete the email verification process.</span><span class="sxs-lookup"><span data-stu-id="6bf20-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="6bf20-115">You will need to wait a few days to be approved after registering as a developer.</span><span class="sxs-lookup"><span data-stu-id="6bf20-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="6bf20-116">Register a QQ application</span><span class="sxs-lookup"><span data-stu-id="6bf20-116">Register a QQ application</span></span>

1. <span data-ttu-id="6bf20-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="6bf20-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="6bf20-118">Click on **应用管理** (app management).</span><span class="sxs-lookup"><span data-stu-id="6bf20-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="6bf20-119">Click on **创建应用** (create app).</span><span class="sxs-lookup"><span data-stu-id="6bf20-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="6bf20-120">Enter the necessary app information.</span><span class="sxs-lookup"><span data-stu-id="6bf20-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="6bf20-121">Click on **创建应用** (create app).</span><span class="sxs-lookup"><span data-stu-id="6bf20-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="6bf20-122">Enter the required information.</span><span class="sxs-lookup"><span data-stu-id="6bf20-122">Enter the required information.</span></span>
7. <span data-ttu-id="6bf20-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="6bf20-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="6bf20-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="6bf20-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="6bf20-125">Click on **创建应用** (create app).</span><span class="sxs-lookup"><span data-stu-id="6bf20-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="6bf20-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span><span class="sxs-lookup"><span data-stu-id="6bf20-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="6bf20-127">Click on **查看** (view) next to the app you just created.</span><span class="sxs-lookup"><span data-stu-id="6bf20-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="6bf20-128">Click on **修改** (edit).</span><span class="sxs-lookup"><span data-stu-id="6bf20-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="6bf20-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span><span class="sxs-lookup"><span data-stu-id="6bf20-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="6bf20-130">Configure QQ as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="6bf20-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="6bf20-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6bf20-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="6bf20-132">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="6bf20-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="6bf20-133">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="6bf20-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="6bf20-134">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="6bf20-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="6bf20-135">For example, enter "QQ".</span><span class="sxs-lookup"><span data-stu-id="6bf20-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="6bf20-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bf20-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="6bf20-137">Click **Set up this identity provider**</span><span class="sxs-lookup"><span data-stu-id="6bf20-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="6bf20-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span><span class="sxs-lookup"><span data-stu-id="6bf20-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="6bf20-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="6bf20-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="6bf20-140">Click **OK** and then click **Create** to save your QQ configuration.</span><span class="sxs-lookup"><span data-stu-id="6bf20-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

