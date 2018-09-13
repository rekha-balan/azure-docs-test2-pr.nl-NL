---
title: Advanced certificate signing options in the SAML token for pre-integrated apps in Azure Active Directory | Microsoft Docs
description: Learn how to use advanced certificate signing options in the SAML token for pre-integrated apps in Azure Active Directory
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/07/2017
ms.author: barbkess
ms.reviewer: jeedes
ms.custom: aaddev
ms.openlocfilehash: c7f2892586dd78f3e4b102deb8c51b9979ed07e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869332"
---
# <a name="advanced-certificate-signing-options-in-the-saml-token-for-gallery-apps-in-azure-active-directory"></a><span data-ttu-id="3920c-103">Advanced certificate signing options in the SAML token for gallery apps in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3920c-103">Advanced certificate signing options in the SAML token for gallery apps in Azure Active Directory</span></span>
<span data-ttu-id="3920c-104">Today Azure Active Directory (Azure AD) supports thousands of pre-integrated applications in the Azure Active Directory App Gallery.</span><span class="sxs-lookup"><span data-stu-id="3920c-104">Today Azure Active Directory (Azure AD) supports thousands of pre-integrated applications in the Azure Active Directory App Gallery.</span></span> <span data-ttu-id="3920c-105">This number includes more than 500 applications that support single sign-on by using the SAML 2.0 protocol.</span><span class="sxs-lookup"><span data-stu-id="3920c-105">This number includes more than 500 applications that support single sign-on by using the SAML 2.0 protocol.</span></span> <span data-ttu-id="3920c-106">When a user authenticates to an application through Azure AD by using SAML, Azure AD sends a token to the application (via an HTTP POST).</span><span class="sxs-lookup"><span data-stu-id="3920c-106">When a user authenticates to an application through Azure AD by using SAML, Azure AD sends a token to the application (via an HTTP POST).</span></span> <span data-ttu-id="3920c-107">Then, the application validates and uses the token to log in the user instead of prompting for a username and password.</span><span class="sxs-lookup"><span data-stu-id="3920c-107">Then, the application validates and uses the token to log in the user instead of prompting for a username and password.</span></span> <span data-ttu-id="3920c-108">These SAML tokens are signed with the unique certificate that's generated in Azure AD and by specific standard algorithms.</span><span class="sxs-lookup"><span data-stu-id="3920c-108">These SAML tokens are signed with the unique certificate that's generated in Azure AD and by specific standard algorithms.</span></span>

<span data-ttu-id="3920c-109">Azure AD uses some of the default settings for the gallery applications.</span><span class="sxs-lookup"><span data-stu-id="3920c-109">Azure AD uses some of the default settings for the gallery applications.</span></span> <span data-ttu-id="3920c-110">The default values are set up based on the application's requirements.</span><span class="sxs-lookup"><span data-stu-id="3920c-110">The default values are set up based on the application's requirements.</span></span>

<span data-ttu-id="3920c-111">Azure AD supports advanced certificate signing settings.</span><span class="sxs-lookup"><span data-stu-id="3920c-111">Azure AD supports advanced certificate signing settings.</span></span> <span data-ttu-id="3920c-112">To select these options, first select the **Show advanced certificate signing settings** check box:</span><span class="sxs-lookup"><span data-stu-id="3920c-112">To select these options, first select the **Show advanced certificate signing settings** check box:</span></span>

![Show advanced certificate signing settings](./media/certificate-signing-options/saml-advance-certificate.png)

<span data-ttu-id="3920c-114">After you select this check box, you can set up certificate signing options and the certificate signing algorithm.</span><span class="sxs-lookup"><span data-stu-id="3920c-114">After you select this check box, you can set up certificate signing options and the certificate signing algorithm.</span></span>

## <a name="certificate-signing-options"></a><span data-ttu-id="3920c-115">Certificate signing options</span><span class="sxs-lookup"><span data-stu-id="3920c-115">Certificate signing options</span></span>

<span data-ttu-id="3920c-116">Azure AD supports three certificate signing options:</span><span class="sxs-lookup"><span data-stu-id="3920c-116">Azure AD supports three certificate signing options:</span></span>

* <span data-ttu-id="3920c-117">**Sign SAML assertion**.</span><span class="sxs-lookup"><span data-stu-id="3920c-117">**Sign SAML assertion**.</span></span> <span data-ttu-id="3920c-118">This default option is set for most of the gallery applications.</span><span class="sxs-lookup"><span data-stu-id="3920c-118">This default option is set for most of the gallery applications.</span></span> <span data-ttu-id="3920c-119">If this option is selected, Azure AD as an IdP signs the SAML assertion and certificate with the X509 certificate of the application.</span><span class="sxs-lookup"><span data-stu-id="3920c-119">If this option is selected, Azure AD as an IdP signs the SAML assertion and certificate with the X509 certificate of the application.</span></span> <span data-ttu-id="3920c-120">Also, it uses the signing algorithm, which is selected in the **Signing Algorithm** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="3920c-120">Also, it uses the signing algorithm, which is selected in the **Signing Algorithm** drop-down list.</span></span>

* <span data-ttu-id="3920c-121">**Sign SAML response**.</span><span class="sxs-lookup"><span data-stu-id="3920c-121">**Sign SAML response**.</span></span> <span data-ttu-id="3920c-122">If this option is selected, Azure AD as an IdP signs the SAML response with the X509 certificate of the application.</span><span class="sxs-lookup"><span data-stu-id="3920c-122">If this option is selected, Azure AD as an IdP signs the SAML response with the X509 certificate of the application.</span></span> <span data-ttu-id="3920c-123">Also, it uses the signing algorithm, which is selected in the **Signing Algorithm** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="3920c-123">Also, it uses the signing algorithm, which is selected in the **Signing Algorithm** drop-down list.</span></span>

* <span data-ttu-id="3920c-124">**Sign SAML response and assertion**.</span><span class="sxs-lookup"><span data-stu-id="3920c-124">**Sign SAML response and assertion**.</span></span> <span data-ttu-id="3920c-125">If this option is selected, Azure AD as an IdP signs the entire SAML token with the X509 certificate of the application.</span><span class="sxs-lookup"><span data-stu-id="3920c-125">If this option is selected, Azure AD as an IdP signs the entire SAML token with the X509 certificate of the application.</span></span> <span data-ttu-id="3920c-126">Also, it uses the signing algorithm, which is selected in the **Signing Algorithm** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="3920c-126">Also, it uses the signing algorithm, which is selected in the **Signing Algorithm** drop-down list.</span></span>

    ![Certificate signing options](./media/certificate-signing-options/saml-signing-options.png)

## <a name="certificate-signing-algorithms"></a><span data-ttu-id="3920c-128">Certificate signing algorithms</span><span class="sxs-lookup"><span data-stu-id="3920c-128">Certificate signing algorithms</span></span>

<span data-ttu-id="3920c-129">Azure AD supports two signing algorithms to sign the SAML response:</span><span class="sxs-lookup"><span data-stu-id="3920c-129">Azure AD supports two signing algorithms to sign the SAML response:</span></span>

* <span data-ttu-id="3920c-130">**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="3920c-130">**SHA-256**.</span></span> <span data-ttu-id="3920c-131">Azure AD uses this default algorithm to sign the SAML response.</span><span class="sxs-lookup"><span data-stu-id="3920c-131">Azure AD uses this default algorithm to sign the SAML response.</span></span> <span data-ttu-id="3920c-132">It's the newest algorithm and is treated as more secure than SHA-1.</span><span class="sxs-lookup"><span data-stu-id="3920c-132">It's the newest algorithm and is treated as more secure than SHA-1.</span></span> <span data-ttu-id="3920c-133">Most of the applications support the SHA-256 algorithm.</span><span class="sxs-lookup"><span data-stu-id="3920c-133">Most of the applications support the SHA-256 algorithm.</span></span> <span data-ttu-id="3920c-134">If an application supports only SHA-1 as the signing algorithm, you can change it.</span><span class="sxs-lookup"><span data-stu-id="3920c-134">If an application supports only SHA-1 as the signing algorithm, you can change it.</span></span> <span data-ttu-id="3920c-135">Otherwise, we recommend that you use the SHA-256 algorithm for signing the SAML response.</span><span class="sxs-lookup"><span data-stu-id="3920c-135">Otherwise, we recommend that you use the SHA-256 algorithm for signing the SAML response.</span></span>

    ![SHA-256 certificate signing algorithm](./media/certificate-signing-options/saml-signing-algo-sha256.png)

* <span data-ttu-id="3920c-137">**SHA-1**.</span><span class="sxs-lookup"><span data-stu-id="3920c-137">**SHA-1**.</span></span> <span data-ttu-id="3920c-138">This is the older algorithm, and it's treated as less secure than SH-256.</span><span class="sxs-lookup"><span data-stu-id="3920c-138">This is the older algorithm, and it's treated as less secure than SH-256.</span></span> <span data-ttu-id="3920c-139">If an application supports only this signing algorithm, you can select this option in the **Signing Algorithm** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="3920c-139">If an application supports only this signing algorithm, you can select this option in the **Signing Algorithm** drop-down list.</span></span> <span data-ttu-id="3920c-140">Azure AD then signs the SAML response with the SHA-1 algorithm.</span><span class="sxs-lookup"><span data-stu-id="3920c-140">Azure AD then signs the SAML response with the SHA-1 algorithm.</span></span>

    ![SHA-1 certificate signing algorithm](./media/certificate-signing-options/saml-signing-algo-sha1.png)

## <a name="next-steps"></a><span data-ttu-id="3920c-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="3920c-142">Next steps</span></span>
* [<span data-ttu-id="3920c-143">Article index for application management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3920c-143">Article index for application management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="3920c-144">Configure single sign-on to applications that are not in the Azure Active Directory App Gallery</span><span class="sxs-lookup"><span data-stu-id="3920c-144">Configure single sign-on to applications that are not in the Azure Active Directory App Gallery</span></span>](configure-federated-single-sign-on-non-gallery-applications.md)
* [<span data-ttu-id="3920c-145">Troubleshoot SAML-based single sign-on</span><span class="sxs-lookup"><span data-stu-id="3920c-145">Troubleshoot SAML-based single sign-on</span></span>](../develop/howto-v1-debug-saml-sso-issues.md)


