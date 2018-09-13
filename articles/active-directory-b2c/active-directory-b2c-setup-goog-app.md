---
title: Set up sign-up and sign-in with a Google account using Azure Active Directory B2C | Microsoft Docs
description: Provide sign-up and sign-in to customers with Google accounts in your applications using Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/06/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 477bd6047da639dcf21592a7ec0c1b80844e031e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828126"
---
# <a name="set-up-sign-up-and-sign-in-with-a-google-account-using-azure-active-directory-b2c"></a><span data-ttu-id="d8cf9-103">Set up sign-up and sign-in with a Google account using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d8cf9-103">Set up sign-up and sign-in with a Google account using Azure Active Directory B2C</span></span>

## <a name="create-a-google-application"></a><span data-ttu-id="d8cf9-104">Create a Google application</span><span class="sxs-lookup"><span data-stu-id="d8cf9-104">Create a Google application</span></span>

<span data-ttu-id="d8cf9-105">To use a Google account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-105">To use a Google account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span></span> <span data-ttu-id="d8cf9-106">If you don’t already have a Google account you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="d8cf9-106">If you don’t already have a Google account you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="d8cf9-107">Sign in to the [Google Developers Console](https://console.developers.google.com/) with your Google account credentials.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-107">Sign in to the [Google Developers Console](https://console.developers.google.com/) with your Google account credentials.</span></span>
2. <span data-ttu-id="d8cf9-108">Select **Create project**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-108">Select **Create project**, and then click **Create**.</span></span> <span data-ttu-id="d8cf9-109">If you have created projects before, select the project list, and then select **New Project**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-109">If you have created projects before, select the project list, and then select **New Project**.</span></span>
3. <span data-ttu-id="d8cf9-110">Enter a **Project name**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-110">Enter a **Project name**, and then click **Create**.</span></span>
3. <span data-ttu-id="d8cf9-111">Select **Credentials** in the left menu, and then select **Create credentials** > **Oauth client ID**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-111">Select **Credentials** in the left menu, and then select **Create credentials** > **Oauth client ID**.</span></span>
4. <span data-ttu-id="d8cf9-112">Select **Configure consent screen**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-112">Select **Configure consent screen**.</span></span>
5. <span data-ttu-id="d8cf9-113">Select or specify a valid **Email address**, provide a **Product name shown to users**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-113">Select or specify a valid **Email address**, provide a **Product name shown to users**, and click **Save**.</span></span>
6. <span data-ttu-id="d8cf9-114">Under **Application type**, select **Web application**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-114">Under **Application type**, select **Web application**.</span></span>
7. <span data-ttu-id="d8cf9-115">Enter a **Name** for your application, enter `https://{tenant}.b2clogin.com` in **Authorized JavaScript origins**, and `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in **Authorized redirect URIs**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-115">Enter a **Name** for your application, enter `https://{tenant}.b2clogin.com` in **Authorized JavaScript origins**, and `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in **Authorized redirect URIs**.</span></span> <span data-ttu-id="d8cf9-116">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span><span class="sxs-lookup"><span data-stu-id="d8cf9-116">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span></span>
8. <span data-ttu-id="d8cf9-117">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-117">Click **Create**.</span></span>
9. <span data-ttu-id="d8cf9-118">Copy the values of **Client ID** and **Client secret**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-118">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="d8cf9-119">You will need both of them to configure Google as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-119">You will need both of them to configure Google as an identity provider in your tenant.</span></span> <span data-ttu-id="d8cf9-120">**Client secret** is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-120">**Client secret** is an important security credential.</span></span>

## <a name="configure-a-google-account-as-an-identity-provider"></a><span data-ttu-id="d8cf9-121">Configure a Google account as an identity provider</span><span class="sxs-lookup"><span data-stu-id="d8cf9-121">Configure a Google account as an identity provider</span></span>

1. <span data-ttu-id="d8cf9-122">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-122">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="d8cf9-123">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-123">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="d8cf9-124">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-124">Select your subscription information, and then select **Switch Directory**.</span></span> 

    ![Switch to your Azure AD B2C tenant](./media/active-directory-b2c-setup-fb-app/switch-directories.png)

    <span data-ttu-id="d8cf9-126">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-126">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-setup-fb-app/select-directory.png)

3. <span data-ttu-id="d8cf9-128">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-128">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span>
4. <span data-ttu-id="d8cf9-129">Select **Identity providers**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-129">Select **Identity providers**, and then select **Add**.</span></span>
5. <span data-ttu-id="d8cf9-130">Enter a **Name**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-130">Enter a **Name**.</span></span> <span data-ttu-id="d8cf9-131">For example, enter *Google*.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-131">For example, enter *Google*.</span></span>
6. <span data-ttu-id="d8cf9-132">Select **Identity provider type**, select **Google**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-132">Select **Identity provider type**, select **Google**, and click **OK**.</span></span>
7. <span data-ttu-id="d8cf9-133">Select **Set up this identity provider** and enter the Client ID that you recorded earlier as the **Client ID** and enter the Client Secret that you recorded as the **Client secret** of the Google application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-133">Select **Set up this identity provider** and enter the Client ID that you recorded earlier as the **Client ID** and enter the Client Secret that you recorded as the **Client secret** of the Google application that you created earlier.</span></span>
8. <span data-ttu-id="d8cf9-134">Click **OK** and then click **Create** to save your Google configuration.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-134">Click **OK** and then click **Create** to save your Google configuration.</span></span>

