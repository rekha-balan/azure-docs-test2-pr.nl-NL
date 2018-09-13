---
title: 'Tutorial: Azure Active Directory Integration with Rally Software | Microsoft Docs'
description: Learn how to use Rally Software with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4ab9b9f78a697bead8599d259c4aad78840594a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563246"
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="7445e-103">Tutorial: Azure Active Directory Integration with Rally Software</span><span class="sxs-lookup"><span data-stu-id="7445e-103">Tutorial: Azure Active Directory Integration with Rally Software</span></span>
<span data-ttu-id="7445e-104">The objective of this tutorial is to show the integration of Azure and Rally Software.</span><span class="sxs-lookup"><span data-stu-id="7445e-104">The objective of this tutorial is to show the integration of Azure and Rally Software.</span></span>  

<span data-ttu-id="7445e-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="7445e-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="7445e-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7445e-106">A valid Azure subscription</span></span>
* <span data-ttu-id="7445e-107">A Rally Software tenant</span><span class="sxs-lookup"><span data-stu-id="7445e-107">A Rally Software tenant</span></span>

<span data-ttu-id="7445e-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7445e-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="7445e-109">Enabling the application integration for Rally Software</span><span class="sxs-lookup"><span data-stu-id="7445e-109">Enabling the application integration for Rally Software</span></span>
2. <span data-ttu-id="7445e-110">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="7445e-110">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="7445e-111">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="7445e-111">Configuring user provisioning</span></span>
4. <span data-ttu-id="7445e-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="7445e-112">Assigning users</span></span>

<span data-ttu-id="7445e-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769525.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="7445e-113">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769525.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-rally-software"></a><span data-ttu-id="7445e-114">Enable the application integration for Rally Software</span><span class="sxs-lookup"><span data-stu-id="7445e-114">Enable the application integration for Rally Software</span></span>
<span data-ttu-id="7445e-115">The objective of this section is to outline how to enable the application integration for Rally Software.</span><span class="sxs-lookup"><span data-stu-id="7445e-115">The objective of this section is to outline how to enable the application integration for Rally Software.</span></span>

<span data-ttu-id="7445e-116">**To enable the application integration for Rally Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7445e-116">**To enable the application integration for Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="7445e-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7445e-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="7445e-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="7445e-118">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="7445e-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7445e-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7445e-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7445e-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="7445e-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="7445e-121">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="7445e-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7445e-122">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="7445e-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="7445e-123">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="7445e-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7445e-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="7445e-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="7445e-125">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="7445e-126">In the **search box**, type **rally**.</span><span class="sxs-lookup"><span data-stu-id="7445e-126">In the **search box**, type **rally**.</span></span>
   
    <span data-ttu-id="7445e-127">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769526.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="7445e-127">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769526.png "Application gallery")</span></span>

7. <span data-ttu-id="7445e-128">In the results pane, select **Rally Software**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7445e-128">In the results pane, select **Rally Software**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="7445e-129">![Rally Software](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769527.png "Rally Software")</span><span class="sxs-lookup"><span data-stu-id="7445e-129">![Rally Software](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769527.png "Rally Software")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="7445e-130">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="7445e-130">Configure single sign-on</span></span>

<span data-ttu-id="7445e-131">The objective of this section is to outline how to enable users to authenticate to Rally Software with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="7445e-131">The objective of this section is to outline how to enable users to authenticate to Rally Software with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="7445e-132">As part of this procedure, you are required to upload a certificate to Rally Software.</span><span class="sxs-lookup"><span data-stu-id="7445e-132">As part of this procedure, you are required to upload a certificate to Rally Software.</span></span>

<span data-ttu-id="7445e-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7445e-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="7445e-134">In the Azure classic portal, on the **Rally Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="7445e-134">In the Azure classic portal, on the **Rally Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="7445e-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749323.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="7445e-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="7445e-136">On the **How would you like users to sign on to Rally** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7445e-136">On the **How would you like users to sign on to Rally** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="7445e-137">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769528.png "Microsoft Azure AD Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7445e-137">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769528.png "Microsoft Azure AD Single Sign-On")</span></span>

3. <span data-ttu-id="7445e-138">On the **Configure App URL** page, in the **Rally Software Tenant URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.rally.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7445e-138">On the **Configure App URL** page, in the **Rally Software Tenant URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.rally.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="7445e-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769529.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="7445e-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769529.png "Configure App URL")</span></span>

4. <span data-ttu-id="7445e-140">On the **Configure single sign-on at Rally** page, click Download metadata, and then save it on your computer.</span><span class="sxs-lookup"><span data-stu-id="7445e-140">On the **Configure single sign-on at Rally** page, click Download metadata, and then save it on your computer.</span></span>
   
    <span data-ttu-id="7445e-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769530.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="7445e-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769530.png "Configure single sign-on")</span></span>

5. <span data-ttu-id="7445e-142">Log in to your **Rally Software** tenant.</span><span class="sxs-lookup"><span data-stu-id="7445e-142">Log in to your **Rally Software** tenant.</span></span>

6. <span data-ttu-id="7445e-143">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="7445e-143">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="7445e-144">![Subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769531.png "Subscription")</span><span class="sxs-lookup"><span data-stu-id="7445e-144">![Subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769531.png "Subscription")</span></span>

7. <span data-ttu-id="7445e-145">Click the **Action** button In the tool bar on the top at the right side and then select **Edit Subscription**.</span><span class="sxs-lookup"><span data-stu-id="7445e-145">Click the **Action** button In the tool bar on the top at the right side and then select **Edit Subscription**.</span></span>

8. <span data-ttu-id="7445e-146">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span><span class="sxs-lookup"><span data-stu-id="7445e-146">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="7445e-147">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769542.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="7445e-147">![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769542.png "Authentication")</span></span>
   
  1. <span data-ttu-id="7445e-148">Select **Rally or SSO authentication** from Authentication dropdown.</span><span class="sxs-lookup"><span data-stu-id="7445e-148">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>
  2. <span data-ttu-id="7445e-149">In the Azure classic portal, on the **Configure single sign-on at Rally Software** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="7445e-149">In the Azure classic portal, on the **Configure single sign-on at Rally Software** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>
  3. <span data-ttu-id="7445e-150">In the Azure classic portal, on the **Configure single sign-on at Rally Software** dialog page, copy the **Remote Logout URL** value.</span><span class="sxs-lookup"><span data-stu-id="7445e-150">In the Azure classic portal, on the **Configure single sign-on at Rally Software** dialog page, copy the **Remote Logout URL** value.</span></span>

9. <span data-ttu-id="7445e-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="7445e-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="7445e-152">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769547.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="7445e-152">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769547.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="7445e-153">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="7445e-153">Configure user provisioning</span></span>

<span data-ttu-id="7445e-154">For AAD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span><span class="sxs-lookup"><span data-stu-id="7445e-154">For AAD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="7445e-155">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7445e-155">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7445e-156">Log in to your Rally Software tenant.</span><span class="sxs-lookup"><span data-stu-id="7445e-156">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="7445e-157">Go to **Setup \> USERS**, and then click **+ Add New**.</span><span class="sxs-lookup"><span data-stu-id="7445e-157">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="7445e-158">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC781039.png "Users")</span><span class="sxs-lookup"><span data-stu-id="7445e-158">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC781039.png "Users")</span></span>

3. <span data-ttu-id="7445e-159">Type the name in the New User textbox, and then click **Add with Details**.</span><span class="sxs-lookup"><span data-stu-id="7445e-159">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="7445e-160">In the **Create User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7445e-160">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="7445e-161">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC781040.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="7445e-161">![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC781040.png "Create User")</span></span>
   
   1. <span data-ttu-id="7445e-162">In the **User Name** textbox, type the name of the Azure AD user you want to provision.</span><span class="sxs-lookup"><span data-stu-id="7445e-162">In the **User Name** textbox, type the name of the Azure AD user you want to provision.</span></span>
   2. <span data-ttu-id="7445e-163">In the **Email Address** textbox, type the email address of the Azure AD user you want to provision.</span><span class="sxs-lookup"><span data-stu-id="7445e-163">In the **Email Address** textbox, type the email address of the Azure AD user you want to provision.</span></span>
   3. <span data-ttu-id="7445e-164">Click **Save & Close**.</span><span class="sxs-lookup"><span data-stu-id="7445e-164">Click **Save & Close**.</span></span>

>[!NOTE]
><span data-ttu-id="7445e-165">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7445e-165">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="7445e-166">Assign users</span><span class="sxs-lookup"><span data-stu-id="7445e-166">Assign users</span></span>
<span data-ttu-id="7445e-167">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="7445e-167">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="7445e-168">**To assign users to Rally Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7445e-168">**To assign users to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="7445e-169">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="7445e-169">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="7445e-170">On the **Rally Software** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="7445e-170">On the **Rally Software** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="7445e-171">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769548.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="7445e-171">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769548.png "Assign users")</span></span>

3. <span data-ttu-id="7445e-172">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="7445e-172">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="7445e-173">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="7445e-173">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="7445e-174">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7445e-174">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="7445e-175">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7445e-175">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>



















