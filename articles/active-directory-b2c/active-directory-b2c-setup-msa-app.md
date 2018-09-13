---
title: Set up sign-up and sign-in with a Microsoft account using Azure Active Directory B2C | Microsoft Docs
description: Provide sign-up and sign-in to customers with Microsoft accounts in your applications using Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/05/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 338c2a197cb50091c3b272e0ce590341ffda1d7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828724"
---
# <a name="set-up-sign-up-and-sign-in-with-a-microsoft-account-using-azure-active-directory-b2c"></a><span data-ttu-id="c8184-103">Set up sign-up and sign-in with a Microsoft account using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="c8184-103">Set up sign-up and sign-in with a Microsoft account using Azure Active Directory B2C</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="c8184-104">Create a Microsoft account application</span><span class="sxs-lookup"><span data-stu-id="c8184-104">Create a Microsoft account application</span></span>

<span data-ttu-id="c8184-105">To use a Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span><span class="sxs-lookup"><span data-stu-id="c8184-105">To use a Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span></span> <span data-ttu-id="c8184-106">If you don’t already have a Microsoft account, you can get it at [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="c8184-106">If you don’t already have a Microsoft account, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="c8184-107">Sign in to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) with your Microsoft account credentials.</span><span class="sxs-lookup"><span data-stu-id="c8184-107">Sign in to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="c8184-108">In the upper-right corner, select **Add an app**.</span><span class="sxs-lookup"><span data-stu-id="c8184-108">In the upper-right corner, select **Add an app**.</span></span>
3. <span data-ttu-id="c8184-109">Provide a **Name** for your application and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c8184-109">Provide a **Name** for your application and click **Create**.</span></span>
4. <span data-ttu-id="c8184-110">On the registration page, copy the value of **Application Id**. You use it to configure your Microsoft account as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="c8184-110">On the registration page, copy the value of **Application Id**. You use it to configure your Microsoft account as an identity provider in your tenant.</span></span>
5. <span data-ttu-id="c8184-111">Select **Add platform**, and then and choose **Web**.</span><span class="sxs-lookup"><span data-stu-id="c8184-111">Select **Add platform**, and then and choose **Web**.</span></span>
6. <span data-ttu-id="c8184-112">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in **Redirect URLs**.</span><span class="sxs-lookup"><span data-stu-id="c8184-112">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in **Redirect URLs**.</span></span> <span data-ttu-id="c8184-113">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span><span class="sxs-lookup"><span data-stu-id="c8184-113">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span></span>
7. <span data-ttu-id="c8184-114">Select **Generate New Password** under **Application Secrets**.</span><span class="sxs-lookup"><span data-stu-id="c8184-114">Select **Generate New Password** under **Application Secrets**.</span></span> <span data-ttu-id="c8184-115">Copy the new password displayed on screen.</span><span class="sxs-lookup"><span data-stu-id="c8184-115">Copy the new password displayed on screen.</span></span> <span data-ttu-id="c8184-116">You need it to configure a Microsoft account as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="c8184-116">You need it to configure a Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="c8184-117">This password is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="c8184-117">This password is an important security credential.</span></span>

## <a name="configure-a-microsoft-account-as-an-identity-provider"></a><span data-ttu-id="c8184-118">Configure a Microsoft account as an identity provider</span><span class="sxs-lookup"><span data-stu-id="c8184-118">Configure a Microsoft account as an identity provider</span></span>

1. <span data-ttu-id="c8184-119">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="c8184-119">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="c8184-120">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c8184-120">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="c8184-121">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8184-121">Select your subscription information, and then select **Switch Directory**.</span></span> 

    ![Switch to your Azure AD B2C tenant](./media/active-directory-b2c-setup-msa-app/switch-directories.png)

    <span data-ttu-id="c8184-123">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="c8184-123">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-setup-msa-app/select-directory.png)

3. <span data-ttu-id="c8184-125">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="c8184-125">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span>
4. <span data-ttu-id="c8184-126">Select **Identity providers**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c8184-126">Select **Identity providers**, and then select **Add**.</span></span>
5. <span data-ttu-id="c8184-127">Provide a **Name**.</span><span class="sxs-lookup"><span data-stu-id="c8184-127">Provide a **Name**.</span></span> <span data-ttu-id="c8184-128">For example, enter *MSA*.</span><span class="sxs-lookup"><span data-stu-id="c8184-128">For example, enter *MSA*.</span></span>
6. <span data-ttu-id="c8184-129">Select **Identity provider type**, select **Microsoft Account**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8184-129">Select **Identity provider type**, select **Microsoft Account**, and click **OK**.</span></span>
7. <span data-ttu-id="c8184-130">Select **Set up this identity provider** and enter the Application Id that you recorded earlier as the **Client ID** and enter the password that you recorded as the **Client secret** of the Microsoft account application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="c8184-130">Select **Set up this identity provider** and enter the Application Id that you recorded earlier as the **Client ID** and enter the password that you recorded as the **Client secret** of the Microsoft account application that you created earlier.</span></span>
8. <span data-ttu-id="c8184-131">Click **OK** and then click **Create** to save your Microsoft account configuration.</span><span class="sxs-lookup"><span data-stu-id="c8184-131">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

