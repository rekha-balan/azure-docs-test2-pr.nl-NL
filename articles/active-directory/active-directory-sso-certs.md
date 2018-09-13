---
title: How to Manage Federation Certificates in Azure AD | Microsoft Docs
description: Learn how to customize the expiration date for your federation certificates, and how to renew certificates that will soon expire.
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: asmalser
ms.openlocfilehash: de533f5b9a83c34951003718aaa6e5bdffffae28
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670335"
---
# <a name="managing-certificates-for-federated-single-sign-on-in-azure-active-directory"></a><span data-ttu-id="2c824-103">Managing Certificates for Federated Single Sign-On in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c824-103">Managing Certificates for Federated Single Sign-On in Azure Active Directory</span></span>
<span data-ttu-id="2c824-104">This article covers common questions related to the certificates that Azure Active Directory creates in order to establish federated single sign-on (SSO) to your SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="2c824-104">This article covers common questions related to the certificates that Azure Active Directory creates in order to establish federated single sign-on (SSO) to your SaaS applications.</span></span>

<span data-ttu-id="2c824-105">This article is only relevant to apps that are configured to use **Azure AD Single Sign-On**, as shown in the example below:</span><span class="sxs-lookup"><span data-stu-id="2c824-105">This article is only relevant to apps that are configured to use **Azure AD Single Sign-On**, as shown in the example below:</span></span>

![Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/fed-sso.PNG)

## <a name="how-to-customize-the-expiration-date-for-your-federation-certificate"></a><span data-ttu-id="2c824-107">How to Customize the Expiration Date for your Federation Certificate</span><span class="sxs-lookup"><span data-stu-id="2c824-107">How to Customize the Expiration Date for your Federation Certificate</span></span>
<span data-ttu-id="2c824-108">By default, certificates are set to expire after two years.</span><span class="sxs-lookup"><span data-stu-id="2c824-108">By default, certificates are set to expire after two years.</span></span> <span data-ttu-id="2c824-109">You can choose a different expiration date for your certificate by following the steps below.</span><span class="sxs-lookup"><span data-stu-id="2c824-109">You can choose a different expiration date for your certificate by following the steps below.</span></span> <span data-ttu-id="2c824-110">The included screenshots use Salesforce for the sake of example, but these steps can apply to any federated SaaS app.</span><span class="sxs-lookup"><span data-stu-id="2c824-110">The included screenshots use Salesforce for the sake of example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="2c824-111">In Azure Active Directory, on the Quick Start page for your application, click on **Configure single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2c824-111">In Azure Active Directory, on the Quick Start page for your application, click on **Configure single sign-on**.</span></span>
   
    ![Open the SSO configuration wizard.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/config-sso.png)
2. <span data-ttu-id="2c824-113">Select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2c824-113">Select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
3. <span data-ttu-id="2c824-114">Type in the **Sign-On URL** of your application, and select the checkbox for **Configure the certificate used for federated single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2c824-114">Type in the **Sign-On URL** of your application, and select the checkbox for **Configure the certificate used for federated single sign-on**.</span></span> <span data-ttu-id="2c824-115">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2c824-115">Then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/new-app-config-sso.PNG)
4. <span data-ttu-id="2c824-117">On the next page, select **Generate a new certificate**, and select how long you'd like the certificate to be valid for.</span><span class="sxs-lookup"><span data-stu-id="2c824-117">On the next page, select **Generate a new certificate**, and select how long you'd like the certificate to be valid for.</span></span> <span data-ttu-id="2c824-118">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2c824-118">Then click **Next**.</span></span>
   
    ![Generate a new certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/new-app-config-cert.PNG)
5. <span data-ttu-id="2c824-120">Next, click on **Download certificate**.</span><span class="sxs-lookup"><span data-stu-id="2c824-120">Next, click on **Download certificate**.</span></span> <span data-ttu-id="2c824-121">To learn how to upload the certificate to your particular SaaS app, click **View configuration instructions**.</span><span class="sxs-lookup"><span data-stu-id="2c824-121">To learn how to upload the certificate to your particular SaaS app, click **View configuration instructions**.</span></span>
   
    ![Download then upload the certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/new-app-config-app.PNG)
6. <span data-ttu-id="2c824-123">The certificate won't be enabled until you select the confirmation checkbox at the bottom of the dialog and then press submit.</span><span class="sxs-lookup"><span data-stu-id="2c824-123">The certificate won't be enabled until you select the confirmation checkbox at the bottom of the dialog and then press submit.</span></span>

## <a name="how-to-renew-a-certificate-that-will-soon-expire"></a><span data-ttu-id="2c824-124">How to Renew a Certificate that will Soon Expire</span><span class="sxs-lookup"><span data-stu-id="2c824-124">How to Renew a Certificate that will Soon Expire</span></span>
<span data-ttu-id="2c824-125">The renewal steps shown below should ideally result in no significant downtime for your users.</span><span class="sxs-lookup"><span data-stu-id="2c824-125">The renewal steps shown below should ideally result in no significant downtime for your users.</span></span> <span data-ttu-id="2c824-126">The screenshots used in this section feature Salesforce as an example, but these steps can apply to any federated SaaS app.</span><span class="sxs-lookup"><span data-stu-id="2c824-126">The screenshots used in this section feature Salesforce as an example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="2c824-127">In Azure Active Directory, on the Quick Start page for your application, click on **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2c824-127">In Azure Active Directory, on the Quick Start page for your application, click on **Configure Single Sign-On**.</span></span>
   
    ![Open the SSO configuration wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/renew-sso-button.PNG)
2. <span data-ttu-id="2c824-129">On the first page of the dialog, **Azure AD Single Sign-On** should already be selected, so click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2c824-129">On the first page of the dialog, **Azure AD Single Sign-On** should already be selected, so click **Next**.</span></span>
3. <span data-ttu-id="2c824-130">On the second page, select the checkbox for **Configure the certificate used for federated single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2c824-130">On the second page, select the checkbox for **Configure the certificate used for federated single sign-on**.</span></span> <span data-ttu-id="2c824-131">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2c824-131">Then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/renew-config-sso.PNG)
4. <span data-ttu-id="2c824-133">On the next page, select **Generate a new certificate**, and select how long you'd like the new certificate to be valid for.</span><span class="sxs-lookup"><span data-stu-id="2c824-133">On the next page, select **Generate a new certificate**, and select how long you'd like the new certificate to be valid for.</span></span> <span data-ttu-id="2c824-134">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2c824-134">Then click **Next**.</span></span>
   
    ![Generate a new certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/new-app-config-cert.PNG)
5. <span data-ttu-id="2c824-136">Click on **Download certificate**.</span><span class="sxs-lookup"><span data-stu-id="2c824-136">Click on **Download certificate**.</span></span> <span data-ttu-id="2c824-137">To successfully renew your certificate, you must perform the following two steps:</span><span class="sxs-lookup"><span data-stu-id="2c824-137">To successfully renew your certificate, you must perform the following two steps:</span></span>
   
   * <span data-ttu-id="2c824-138">Upload the new certificate to the SaaS app's single sign-on configuration screen.</span><span class="sxs-lookup"><span data-stu-id="2c824-138">Upload the new certificate to the SaaS app's single sign-on configuration screen.</span></span> <span data-ttu-id="2c824-139">To learn how to do this for your particular SaaS app, click **View configuration instructions**.</span><span class="sxs-lookup"><span data-stu-id="2c824-139">To learn how to do this for your particular SaaS app, click **View configuration instructions**.</span></span>
   * <span data-ttu-id="2c824-140">In Azure AD, Select the confirmation checkbox at the bottom of the dialog to enable the new certificate, and then click **Next** to submit.</span><span class="sxs-lookup"><span data-stu-id="2c824-140">In Azure AD, Select the confirmation checkbox at the bottom of the dialog to enable the new certificate, and then click **Next** to submit.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="2c824-141">Single sign-on to the app will be disabled the moment either one of these two steps is completed, but it will be enabled again once the second step is completed.</span><span class="sxs-lookup"><span data-stu-id="2c824-141">Single sign-on to the app will be disabled the moment either one of these two steps is completed, but it will be enabled again once the second step is completed.</span></span> <span data-ttu-id="2c824-142">Therefore, to minimize downtime, please prepare to accomplish both steps within a short amount of time from each other.</span><span class="sxs-lookup"><span data-stu-id="2c824-142">Therefore, to minimize downtime, please prepare to accomplish both steps within a short amount of time from each other.</span></span>
     > 
     > 
     
     ![Download then upload the certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-sso-certs/renew-config-app.PNG)

## <a name="related-articles"></a><span data-ttu-id="2c824-144">Related Articles</span><span class="sxs-lookup"><span data-stu-id="2c824-144">Related Articles</span></span>
* [<span data-ttu-id="2c824-145">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c824-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="2c824-146">Application access and single sign-on with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c824-146">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2c824-147">Troubleshooting SAML-Based Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2c824-147">Troubleshooting SAML-Based Single Sign-On</span></span>](active-directory-saml-debugging.md)










