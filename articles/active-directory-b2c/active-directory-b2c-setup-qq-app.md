---
title: Set up sign-up and sign-in with a QQ account using Azure Active Directory B2C | Microsoft Docs
description: Provide sign-up and sign-in to customers with QQ accounts in your applications using Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/09/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 11bb5bf132103bed9e154a12c0e628177ca6a57a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809210"
---
# <a name="set-up-sign-up-and-sign-in-with-a-qq-account-using-azure-active-directory-b2c"></a><span data-ttu-id="8fd08-103">Set up sign-up and sign-in with a QQ account using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="8fd08-103">Set up sign-up and sign-in with a QQ account using Azure Active Directory B2C</span></span>

> [!NOTE]
> <span data-ttu-id="8fd08-104">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="8fd08-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="8fd08-105">Create a QQ application</span><span class="sxs-lookup"><span data-stu-id="8fd08-105">Create a QQ application</span></span>

<span data-ttu-id="8fd08-106">To use a QQ account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span><span class="sxs-lookup"><span data-stu-id="8fd08-106">To use a QQ account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span></span> <span data-ttu-id="8fd08-107">If you don’t already have a QQ account, you can get it at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="8fd08-107">If you don’t already have a QQ account, you can get it at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="8fd08-108">Register for the QQ developer program</span><span class="sxs-lookup"><span data-stu-id="8fd08-108">Register for the QQ developer program</span></span>

1. <span data-ttu-id="8fd08-109">Sign in to the [QQ developer portal](http://open.qq.com) with your QQ account credentials.</span><span class="sxs-lookup"><span data-stu-id="8fd08-109">Sign in to the [QQ developer portal](http://open.qq.com) with your QQ account credentials.</span></span>
2. <span data-ttu-id="8fd08-110">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span><span class="sxs-lookup"><span data-stu-id="8fd08-110">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="8fd08-111">Select **个人** (individual developer).</span><span class="sxs-lookup"><span data-stu-id="8fd08-111">Select **个人** (individual developer).</span></span>
4. <span data-ttu-id="8fd08-112">Enter the required information and select **下一步** (next step).</span><span class="sxs-lookup"><span data-stu-id="8fd08-112">Enter the required information and select **下一步** (next step).</span></span>
5. <span data-ttu-id="8fd08-113">Complete the email verification process.</span><span class="sxs-lookup"><span data-stu-id="8fd08-113">Complete the email verification process.</span></span> <span data-ttu-id="8fd08-114">You will need to wait a few days to be approved after registering as a developer.</span><span class="sxs-lookup"><span data-stu-id="8fd08-114">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="8fd08-115">Register a QQ application</span><span class="sxs-lookup"><span data-stu-id="8fd08-115">Register a QQ application</span></span>

1. <span data-ttu-id="8fd08-116">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="8fd08-116">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="8fd08-117">Select **应用管理** (app management).</span><span class="sxs-lookup"><span data-stu-id="8fd08-117">Select **应用管理** (app management).</span></span>
5. <span data-ttu-id="8fd08-118">Select **创建应用** (create app) and enter the required information.</span><span class="sxs-lookup"><span data-stu-id="8fd08-118">Select **创建应用** (create app) and enter the required information.</span></span>
7. <span data-ttu-id="8fd08-119">Enter `https://{tenant_name}.b2clogin.com/te/{tenant_name}.onmicrosoft.com/oauth2/authresp` in **授权回调域** (callback URL).</span><span class="sxs-lookup"><span data-stu-id="8fd08-119">Enter `https://{tenant_name}.b2clogin.com/te/{tenant_name}.onmicrosoft.com/oauth2/authresp` in **授权回调域** (callback URL).</span></span> <span data-ttu-id="8fd08-120">For example, if your `tenant_name` is contoso, set the URL to be `https://contoso.b2clogin.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="8fd08-120">For example, if your `tenant_name` is contoso, set the URL to be `https://contoso.b2clogin.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="8fd08-121">Select **创建应用** (create app).</span><span class="sxs-lookup"><span data-stu-id="8fd08-121">Select **创建应用** (create app).</span></span>
9. <span data-ttu-id="8fd08-122">On the confirmation page, select **应用管理** (app management) to return to the app management page.</span><span class="sxs-lookup"><span data-stu-id="8fd08-122">On the confirmation page, select **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="8fd08-123">Select **查看** (view) next to the app you created.</span><span class="sxs-lookup"><span data-stu-id="8fd08-123">Select **查看** (view) next to the app you created.</span></span>
11. <span data-ttu-id="8fd08-124">Select **修改** (edit).</span><span class="sxs-lookup"><span data-stu-id="8fd08-124">Select **修改** (edit).</span></span>
12. <span data-ttu-id="8fd08-125">Copy the **APP ID** and **APP KEY**.</span><span class="sxs-lookup"><span data-stu-id="8fd08-125">Copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="8fd08-126">You need both of these values to add the identity provider to your tenant.</span><span class="sxs-lookup"><span data-stu-id="8fd08-126">You need both of these values to add the identity provider to your tenant.</span></span>

## <a name="configure-qq-as-an-identity-provider"></a><span data-ttu-id="8fd08-127">Configure QQ as an identity provider</span><span class="sxs-lookup"><span data-stu-id="8fd08-127">Configure QQ as an identity provider</span></span>

1. <span data-ttu-id="8fd08-128">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="8fd08-128">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="8fd08-129">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8fd08-129">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="8fd08-130">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fd08-130">Select your subscription information, and then select **Switch Directory**.</span></span> 

    ![Switch to your Azure AD B2C tenant](./media/active-directory-b2c-setup-qq-app/switch-directories.png)

    <span data-ttu-id="8fd08-132">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="8fd08-132">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-setup-qq-app/select-directory.png)

3. <span data-ttu-id="8fd08-134">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="8fd08-134">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span>
4. <span data-ttu-id="8fd08-135">Select **Identity providers**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8fd08-135">Select **Identity providers**, and then select **Add**.</span></span>
5. <span data-ttu-id="8fd08-136">Provide a **Name**.</span><span class="sxs-lookup"><span data-stu-id="8fd08-136">Provide a **Name**.</span></span> <span data-ttu-id="8fd08-137">For example, enter *QQ*.</span><span class="sxs-lookup"><span data-stu-id="8fd08-137">For example, enter *QQ*.</span></span>
6. <span data-ttu-id="8fd08-138">Select **Identity provider type**, select **QQ (Preview)**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fd08-138">Select **Identity provider type**, select **QQ (Preview)**, and click **OK**.</span></span>
7. <span data-ttu-id="8fd08-139">Select **Set up this identity provider** and enter the APP ID that you recorded earlier as the **Client ID** and enter the APP Key that you recorded as the **Client secret** of the QQ application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="8fd08-139">Select **Set up this identity provider** and enter the APP ID that you recorded earlier as the **Client ID** and enter the APP Key that you recorded as the **Client secret** of the QQ application that you created earlier.</span></span>
8. <span data-ttu-id="8fd08-140">Click **OK** and then click **Create** to save your QQ configuration.</span><span class="sxs-lookup"><span data-stu-id="8fd08-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

