---
title: 'Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tangoe Command Premium Mobile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 2a477d8e10b9be4aa90cc80341c787facaabc520
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867636"
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="56ac9-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="56ac9-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="56ac9-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56ac9-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56ac9-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="56ac9-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56ac9-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="56ac9-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="56ac9-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="56ac9-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56ac9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="56ac9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="56ac9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="56ac9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56ac9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="56ac9-110">Prerequisites</span></span>

<span data-ttu-id="56ac9-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="56ac9-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="56ac9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="56ac9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56ac9-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="56ac9-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56ac9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="56ac9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56ac9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="56ac9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56ac9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="56ac9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56ac9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56ac9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56ac9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="56ac9-118">Scenario description</span></span>
<span data-ttu-id="56ac9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="56ac9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56ac9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="56ac9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56ac9-121">Add Tangoe Command Premium Mobile from the gallery</span><span class="sxs-lookup"><span data-stu-id="56ac9-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
1. <span data-ttu-id="56ac9-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56ac9-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="56ac9-123">Add Tangoe Command Premium Mobile from the gallery</span><span class="sxs-lookup"><span data-stu-id="56ac9-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="56ac9-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="56ac9-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56ac9-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56ac9-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56ac9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="56ac9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="56ac9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56ac9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="56ac9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="56ac9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="56ac9-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="56ac9-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="56ac9-134">Add Tangoe Command Premium Mobile from gallery</span><span class="sxs-lookup"><span data-stu-id="56ac9-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="56ac9-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56ac9-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="56ac9-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56ac9-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56ac9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56ac9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="56ac9-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span><span class="sxs-lookup"><span data-stu-id="56ac9-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="56ac9-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="56ac9-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56ac9-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="56ac9-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56ac9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="56ac9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="56ac9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56ac9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="56ac9-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="56ac9-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="56ac9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="56ac9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="56ac9-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="56ac9-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="56ac9-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56ac9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="56ac9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span><span class="sxs-lookup"><span data-stu-id="56ac9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="56ac9-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56ac9-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="56ac9-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="56ac9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="56ac9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML-based Sign-on](./media/tangoe-tutorial/tutorial_tangoe_samlbase.png)

1. <span data-ttu-id="56ac9-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56ac9-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![Tangoe Command Premium Mobile Domain and URLs](./media/tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="56ac9-155">a.</span><span class="sxs-lookup"><span data-stu-id="56ac9-155">a.</span></span> <span data-ttu-id="56ac9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="56ac9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="56ac9-157">b.</span><span class="sxs-lookup"><span data-stu-id="56ac9-157">b.</span></span> <span data-ttu-id="56ac9-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="56ac9-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56ac9-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="56ac9-159">These values are not real.</span></span> <span data-ttu-id="56ac9-160">Update these values with the actual  Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="56ac9-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="56ac9-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="56ac9-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-us/) to get these values.</span></span> 

1. <span data-ttu-id="56ac9-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="56ac9-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![SAML Signing Certificate section](./media/tangoe-tutorial/tutorial_tangoe_certificate.png) 

1. <span data-ttu-id="56ac9-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="56ac9-164">Click **Save** button.</span></span>

    ![Save button](./media/tangoe-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="56ac9-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="56ac9-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="56ac9-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="56ac9-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Tangoe Command Premium Mobile Configuration section](./media/tangoe-tutorial/tutorial_tangoe_configure.png) 

1. <span data-ttu-id="56ac9-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-us/) and provide the following:</span><span class="sxs-lookup"><span data-stu-id="56ac9-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-us/) and provide the following:</span></span>

   - <span data-ttu-id="56ac9-170">The downloaded metadata file</span><span class="sxs-lookup"><span data-stu-id="56ac9-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="56ac9-171">The **SAML Entity ID**</span><span class="sxs-lookup"><span data-stu-id="56ac9-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="56ac9-172">The **SAML Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="56ac9-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="56ac9-173">The **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="56ac9-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="56ac9-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="56ac9-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56ac9-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="56ac9-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56ac9-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56ac9-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="56ac9-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="56ac9-177">Create an Azure AD test user</span></span>
<span data-ttu-id="56ac9-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56ac9-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="56ac9-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56ac9-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56ac9-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="56ac9-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tangoe-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="56ac9-183">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Users and groups -> All users](./media/tangoe-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="56ac9-185">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="56ac9-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add user](./media/tangoe-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="56ac9-187">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56ac9-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![User dialog page](./media/tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56ac9-189">a.</span><span class="sxs-lookup"><span data-stu-id="56ac9-189">a.</span></span> <span data-ttu-id="56ac9-190">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56ac9-191">b.</span><span class="sxs-lookup"><span data-stu-id="56ac9-191">b.</span></span> <span data-ttu-id="56ac9-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56ac9-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56ac9-193">c.</span><span class="sxs-lookup"><span data-stu-id="56ac9-193">c.</span></span> <span data-ttu-id="56ac9-194">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="56ac9-195">d.</span><span class="sxs-lookup"><span data-stu-id="56ac9-195">d.</span></span> <span data-ttu-id="56ac9-196">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="56ac9-197">Create a Tangoe Command Premium Mobile test user</span><span class="sxs-lookup"><span data-stu-id="56ac9-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="56ac9-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="56ac9-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="56ac9-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="56ac9-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="56ac9-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-us/) to provision all these users into the application.</span><span class="sxs-lookup"><span data-stu-id="56ac9-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="56ac9-201">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="56ac9-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="56ac9-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="56ac9-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![Assign User][200] 

<span data-ttu-id="56ac9-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56ac9-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="56ac9-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="56ac9-207">In the applications list, select **Tangoe Command Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile in app list](./media/tangoe-tutorial/tutorial_tangoe_app.png) 

1. <span data-ttu-id="56ac9-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="56ac9-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="56ac9-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="56ac9-211">Click **Add** button.</span></span> <span data-ttu-id="56ac9-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="56ac9-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="56ac9-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="56ac9-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="56ac9-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="56ac9-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="56ac9-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="56ac9-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="56ac9-217">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="56ac9-217">Test single sign-on</span></span>

<span data-ttu-id="56ac9-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="56ac9-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="56ac9-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span><span class="sxs-lookup"><span data-stu-id="56ac9-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="56ac9-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="56ac9-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="56ac9-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="56ac9-221">Additional resources</span></span>

* [<span data-ttu-id="56ac9-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56ac9-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="56ac9-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56ac9-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/tangoe-tutorial/tutorial_general_01.png
[2]: ./media/tangoe-tutorial/tutorial_general_02.png
[3]: ./media/tangoe-tutorial/tutorial_general_03.png
[4]: ./media/tangoe-tutorial/tutorial_general_04.png

[100]: ./media/tangoe-tutorial/tutorial_general_100.png

[200]: ./media/tangoe-tutorial/tutorial_general_200.png
[201]: ./media/tangoe-tutorial/tutorial_general_201.png
[202]: ./media/tangoe-tutorial/tutorial_general_202.png
[203]: ./media/tangoe-tutorial/tutorial_general_203.png

