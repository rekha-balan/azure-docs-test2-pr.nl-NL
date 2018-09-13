---
title: Configure SaaS apps for B2B collaboration in Azure Active Directory | Microsoft Docs
description: Code and PowerShell samples for Azure Active Directory B2B collaboration
services: active-directory
documentationcenter: ''
author: sasubram
manager: femila
editor: ''
tags: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 02/06/2017
ms.author: sasubram
ms.openlocfilehash: 686221fbacc182d60d9b839d0b943e3ef30d0861
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563122"
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="82840-103">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="82840-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="82840-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82840-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="82840-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="82840-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="82840-106">Before you look at app-specific instructions, here are some rules of thumb:</span><span class="sxs-lookup"><span data-stu-id="82840-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="82840-107">For most of the apps, user setup needs to happen manually.</span><span class="sxs-lookup"><span data-stu-id="82840-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="82840-108">That is, users must be created manually in the app as well.</span><span class="sxs-lookup"><span data-stu-id="82840-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="82840-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span><span class="sxs-lookup"><span data-stu-id="82840-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="82840-110">Users must be sure to accept each invitation.</span><span class="sxs-lookup"><span data-stu-id="82840-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="82840-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="82840-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="82840-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="82840-112">Dropbox Business</span></span>

<span data-ttu-id="82840-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span><span class="sxs-lookup"><span data-stu-id="82840-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="82840-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82840-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="82840-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="82840-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![The "Add" button on the Enterprise applications page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="82840-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span><span class="sxs-lookup"><span data-stu-id="82840-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Search for "dropbox" on the Add an application page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="82840-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span><span class="sxs-lookup"><span data-stu-id="82840-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="82840-120">(It's set as UPN by default.)</span><span class="sxs-lookup"><span data-stu-id="82840-120">(It's set as UPN by default.)</span></span>

  ![Configuring single sign-on for the app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="82840-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span><span class="sxs-lookup"><span data-stu-id="82840-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Downloading the certificate for Dropbox configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="82840-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span><span class="sxs-lookup"><span data-stu-id="82840-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![The Dropbox sign-in page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="82840-126">On the menu, select **Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="82840-126">On the menu, select **Admin Console**.</span></span>

  ![The "Admin Console" link on the Dropbox menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="82840-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="82840-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![The "More" link in the collapsed Authentication dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![The "Sign in URL" in the expanded Authentication dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="82840-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="82840-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configuring automatic user provisioning in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="82840-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span><span class="sxs-lookup"><span data-stu-id="82840-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="82840-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span><span class="sxs-lookup"><span data-stu-id="82840-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="82840-135">Box</span><span class="sxs-lookup"><span data-stu-id="82840-135">Box</span></span>
<span data-ttu-id="82840-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="82840-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="82840-137">In this procedure, you upload metadata to Box.com.</span><span class="sxs-lookup"><span data-stu-id="82840-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="82840-138">Add the Box app from the enterprise apps.</span><span class="sxs-lookup"><span data-stu-id="82840-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="82840-139">Configure single sign-on by doing the following:</span><span class="sxs-lookup"><span data-stu-id="82840-139">Configure single sign-on by doing the following:</span></span>

  ![Configure Box single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="82840-141">a.</span><span class="sxs-lookup"><span data-stu-id="82840-141">a.</span></span> <span data-ttu-id="82840-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="82840-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="82840-143">This URL is the URL of your Box.com tenant.</span><span class="sxs-lookup"><span data-stu-id="82840-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="82840-144">It should follow the naming convention *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="82840-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="82840-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span><span class="sxs-lookup"><span data-stu-id="82840-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="82840-146">b.</span><span class="sxs-lookup"><span data-stu-id="82840-146">b.</span></span> <span data-ttu-id="82840-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span><span class="sxs-lookup"><span data-stu-id="82840-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="82840-148">c.</span><span class="sxs-lookup"><span data-stu-id="82840-148">c.</span></span> <span data-ttu-id="82840-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="82840-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="82840-150">d.</span><span class="sxs-lookup"><span data-stu-id="82840-150">d.</span></span> <span data-ttu-id="82840-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span><span class="sxs-lookup"><span data-stu-id="82840-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="82840-152">e.</span><span class="sxs-lookup"><span data-stu-id="82840-152">e.</span></span> <span data-ttu-id="82840-153">Forward the metadata file to the Box support team, which will configure single sign-on for you.</span><span class="sxs-lookup"><span data-stu-id="82840-153">Forward the metadata file to the Box support team, which will configure single sign-on for you.</span></span>

3. <span data-ttu-id="82840-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="82840-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Authorize Azure AD to connect to Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="82840-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span><span class="sxs-lookup"><span data-stu-id="82840-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82840-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="82840-157">Next steps</span></span>

<span data-ttu-id="82840-158">See the following articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="82840-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="82840-159">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="82840-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="82840-160">B2B collaboration user properties</span><span class="sxs-lookup"><span data-stu-id="82840-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="82840-161">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="82840-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="82840-162">Delegate B2B collaboration invitations</span><span class="sxs-lookup"><span data-stu-id="82840-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="82840-163">Dynamic groups and B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="82840-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="82840-164">B2B collaboration code and PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="82840-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="82840-165">B2B collaboration user tokens</span><span class="sxs-lookup"><span data-stu-id="82840-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="82840-166">B2B collaboration user claims mapping</span><span class="sxs-lookup"><span data-stu-id="82840-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="82840-167">Office 365 external sharing</span><span class="sxs-lookup"><span data-stu-id="82840-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="82840-168">B2B collaboration current limitations</span><span class="sxs-lookup"><span data-stu-id="82840-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)











