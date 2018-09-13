---
title: 'Azure Active Directory B2C: Google+ configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with Google+ accounts in your applications that are secured by Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 2330dd7bebb1713fa2663ba5dcd5901d92a2cdc2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549250"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="b3aa3-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span><span class="sxs-lookup"><span data-stu-id="b3aa3-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="b3aa3-104">Create a Google+ application</span><span class="sxs-lookup"><span data-stu-id="b3aa3-104">Create a Google+ application</span></span>
<span data-ttu-id="b3aa3-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="b3aa3-106">You need a Google+ account to do this.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="b3aa3-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="b3aa3-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="b3aa3-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="b3aa3-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - Get started](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - New project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="b3aa3-112">Click **API Manager** and then click **Credentials** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="b3aa3-113">Click the **OAuth consent screen** tab at the top.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+ - Credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="b3aa3-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - OAuth consent screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="b3aa3-117">Click **New credentials** and then choose **OAuth client ID**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - OAuth consent screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="b3aa3-119">Under **Application type**, select **Web application**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - OAuth consent screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="b3aa3-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="b3aa3-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b3aa3-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="b3aa3-123">The **{tenant}** value is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="b3aa3-124">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-124">Click **Create**.</span></span>
   
    ![Google+ - Create client ID](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="b3aa3-126">Copy the values of **Client ID** and **Client secret**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="b3aa3-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="b3aa3-128">**Client secret** is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - Client secret](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b3aa3-130">Configure Google+ as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="b3aa3-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b3aa3-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="b3aa3-132">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b3aa3-133">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="b3aa3-134">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="b3aa3-135">For example, enter "G+".</span><span class="sxs-lookup"><span data-stu-id="b3aa3-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="b3aa3-136">Click **Identity provider type**, select **Google**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="b3aa3-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="b3aa3-138">Click **OK** and then click **Create** to save your Google+ configuration.</span><span class="sxs-lookup"><span data-stu-id="b3aa3-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>









