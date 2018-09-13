---
title: 'Azure Active Directory B2C: LinkedIn configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with LinkedIn accounts in your applications that are secured by Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 7a3127d0354314e695dc368d6ddc7d6231f558fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671471"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="e3489-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span><span class="sxs-lookup"><span data-stu-id="e3489-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="e3489-104">Create a LinkedIn application</span><span class="sxs-lookup"><span data-stu-id="e3489-104">Create a LinkedIn application</span></span>
<span data-ttu-id="e3489-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="e3489-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="e3489-106">You need a LinkedIn account to do this.</span><span class="sxs-lookup"><span data-stu-id="e3489-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="e3489-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="e3489-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="e3489-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span><span class="sxs-lookup"><span data-stu-id="e3489-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="e3489-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span><span class="sxs-lookup"><span data-stu-id="e3489-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - New app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="e3489-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span><span class="sxs-lookup"><span data-stu-id="e3489-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="e3489-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="e3489-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - Register app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="e3489-114">Copy the values of **Client ID** and **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="e3489-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="e3489-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="e3489-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e3489-116">**Client Secret** is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="e3489-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="e3489-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="e3489-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="e3489-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="e3489-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="e3489-119">Click **Add**, and then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="e3489-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="e3489-120">The **{tenant}** value is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e3489-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - Setup app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="e3489-122">Configure LinkedIn as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="e3489-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="e3489-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e3489-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="e3489-124">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="e3489-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="e3489-125">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="e3489-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="e3489-126">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="e3489-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="e3489-127">For example, enter "LI".</span><span class="sxs-lookup"><span data-stu-id="e3489-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="e3489-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3489-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="e3489-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e3489-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="e3489-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span><span class="sxs-lookup"><span data-stu-id="e3489-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>




