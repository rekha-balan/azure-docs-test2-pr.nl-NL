---
title: Configure SaaS apps for B2B collaboration in Azure Active Directory | Microsoft Docs
description: Code and PowerShell samples for Azure Active Directory B2B collaboration
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 05/23/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 409cce16d256c408aaa245b97d17171669a2cf41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871246"
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="23407-103">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="23407-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="23407-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23407-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="23407-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="23407-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="23407-106">Before you look at app-specific instructions, here are some rules of thumb:</span><span class="sxs-lookup"><span data-stu-id="23407-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="23407-107">For most of the apps, user setup needs to happen manually.</span><span class="sxs-lookup"><span data-stu-id="23407-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="23407-108">That is, users must be created manually in the app as well.</span><span class="sxs-lookup"><span data-stu-id="23407-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="23407-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span><span class="sxs-lookup"><span data-stu-id="23407-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="23407-110">Users must be sure to accept each invitation.</span><span class="sxs-lookup"><span data-stu-id="23407-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="23407-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="23407-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="23407-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="23407-112">Dropbox Business</span></span>

<span data-ttu-id="23407-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span><span class="sxs-lookup"><span data-stu-id="23407-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="23407-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23407-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="23407-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="23407-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![The "Add" button on the Enterprise applications page](media/configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="23407-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span><span class="sxs-lookup"><span data-stu-id="23407-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Search for "dropbox" on the Add an application page](media/configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="23407-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span><span class="sxs-lookup"><span data-stu-id="23407-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="23407-120">(It's set as UPN by default.)</span><span class="sxs-lookup"><span data-stu-id="23407-120">(It's set as UPN by default.)</span></span>

  ![Configuring single sign-on for the app](media/configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="23407-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span><span class="sxs-lookup"><span data-stu-id="23407-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Downloading the certificate for Dropbox configuration](media/configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="23407-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span><span class="sxs-lookup"><span data-stu-id="23407-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![The Dropbox sign-in page](media/configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="23407-126">On the menu, select **Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="23407-126">On the menu, select **Admin Console**.</span></span>

  ![The "Admin Console" link on the Dropbox menu](media/configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="23407-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="23407-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![The "More" link in the collapsed Authentication dialog box](media/configure-saas-apps/dropbox-auth-01.png)

  ![The "Sign in URL" in the expanded Authentication dialog box](media/configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="23407-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="23407-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configuring automatic user provisioning in the Azure portal](media/configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="23407-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span><span class="sxs-lookup"><span data-stu-id="23407-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="23407-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span><span class="sxs-lookup"><span data-stu-id="23407-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="23407-135">Box</span><span class="sxs-lookup"><span data-stu-id="23407-135">Box</span></span>
<span data-ttu-id="23407-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="23407-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="23407-137">In this procedure, you upload metadata to Box.com.</span><span class="sxs-lookup"><span data-stu-id="23407-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="23407-138">Add the Box app from the enterprise apps.</span><span class="sxs-lookup"><span data-stu-id="23407-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="23407-139">Configure single sign-on in the following order:</span><span class="sxs-lookup"><span data-stu-id="23407-139">Configure single sign-on in the following order:</span></span>

  ![Configure Box single sign-on](media/configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="23407-141">a.</span><span class="sxs-lookup"><span data-stu-id="23407-141">a.</span></span> <span data-ttu-id="23407-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23407-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="23407-143">This URL is the URL of your Box.com tenant.</span><span class="sxs-lookup"><span data-stu-id="23407-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="23407-144">It should follow the naming convention *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="23407-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="23407-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span><span class="sxs-lookup"><span data-stu-id="23407-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="23407-146">b.</span><span class="sxs-lookup"><span data-stu-id="23407-146">b.</span></span> <span data-ttu-id="23407-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span><span class="sxs-lookup"><span data-stu-id="23407-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="23407-148">c.</span><span class="sxs-lookup"><span data-stu-id="23407-148">c.</span></span> <span data-ttu-id="23407-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="23407-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="23407-150">d.</span><span class="sxs-lookup"><span data-stu-id="23407-150">d.</span></span> <span data-ttu-id="23407-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span><span class="sxs-lookup"><span data-stu-id="23407-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="23407-152">e.</span><span class="sxs-lookup"><span data-stu-id="23407-152">e.</span></span> <span data-ttu-id="23407-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span><span class="sxs-lookup"><span data-stu-id="23407-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="23407-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="23407-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Authorize Azure AD to connect to Box](media/configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="23407-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span><span class="sxs-lookup"><span data-stu-id="23407-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23407-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="23407-157">Next steps</span></span>

<span data-ttu-id="23407-158">See the following articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="23407-158">See the following articles on Azure AD B2B collaboration:</span></span>

- [<span data-ttu-id="23407-159">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="23407-159">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
- [<span data-ttu-id="23407-160">Dynamic groups and B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="23407-160">Dynamic groups and B2B collaboration</span></span>](use-dynamic-groups.md)
- [<span data-ttu-id="23407-161">B2B collaboration user claims mapping</span><span class="sxs-lookup"><span data-stu-id="23407-161">B2B collaboration user claims mapping</span></span>](claims-mapping.md)
- [<span data-ttu-id="23407-162">Office 365 external sharing</span><span class="sxs-lookup"><span data-stu-id="23407-162">Office 365 external sharing</span></span>](o365-external-user.md)

