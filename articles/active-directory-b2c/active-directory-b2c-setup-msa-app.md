---
title: 'Azure Active Directory B2C: Microsoft account configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with Microsoft accounts in your applications that are secured by Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: f52e7434722aaa496c3ebc2f24ceb2f12464b03b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556139"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="22a9c-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span><span class="sxs-lookup"><span data-stu-id="22a9c-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="22a9c-104">Create a Microsoft account application</span><span class="sxs-lookup"><span data-stu-id="22a9c-104">Create a Microsoft account application</span></span>
<span data-ttu-id="22a9c-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="22a9c-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="22a9c-106">You need a Microsoft account to do this.</span><span class="sxs-lookup"><span data-stu-id="22a9c-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="22a9c-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="22a9c-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="22a9c-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span><span class="sxs-lookup"><span data-stu-id="22a9c-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="22a9c-109">Click **Add an app**.</span><span class="sxs-lookup"><span data-stu-id="22a9c-109">Click **Add an app**.</span></span>
   
    ![Microsoft account - Add a new app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="22a9c-111">Provide a **Name** for your application and click **Create application**.</span><span class="sxs-lookup"><span data-stu-id="22a9c-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft account - App name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="22a9c-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="22a9c-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft account - Application Id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="22a9c-115">Click on **Add platform** and choose **Web**.</span><span class="sxs-lookup"><span data-stu-id="22a9c-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft account - Add platform](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft account - Web](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="22a9c-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span><span class="sxs-lookup"><span data-stu-id="22a9c-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="22a9c-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="22a9c-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft account - Redirect URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="22a9c-121">Click on **Generate New Password** under the **Application Secrets** section.</span><span class="sxs-lookup"><span data-stu-id="22a9c-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="22a9c-122">Copy the new password displayed on screen.</span><span class="sxs-lookup"><span data-stu-id="22a9c-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="22a9c-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="22a9c-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="22a9c-124">This password is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="22a9c-124">This password is an important security credential.</span></span>
   
    ![Microsoft account - Generate new password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft account - New password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="22a9c-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span><span class="sxs-lookup"><span data-stu-id="22a9c-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="22a9c-128">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="22a9c-128">Click **Save**.</span></span>
   
    ![Microsoft account - Live SDK support](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="22a9c-130">Configure Microsoft account as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="22a9c-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="22a9c-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="22a9c-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="22a9c-132">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="22a9c-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="22a9c-133">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="22a9c-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="22a9c-134">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="22a9c-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="22a9c-135">For example, enter "MSA".</span><span class="sxs-lookup"><span data-stu-id="22a9c-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="22a9c-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="22a9c-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="22a9c-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="22a9c-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="22a9c-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span><span class="sxs-lookup"><span data-stu-id="22a9c-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>










