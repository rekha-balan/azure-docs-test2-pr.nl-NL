---
title: 'Tutorial: Azure Active Directory integration with Pantheon | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pantheon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 25f8b09f31bd9eecc454444312ea02182a71a77a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867379"
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="e64c1-103">Tutorial: Azure Active Directory integration with Pantheon</span><span class="sxs-lookup"><span data-stu-id="e64c1-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="e64c1-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e64c1-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e64c1-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e64c1-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e64c1-106">You can control in Azure AD who has access to Pantheon</span><span class="sxs-lookup"><span data-stu-id="e64c1-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="e64c1-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e64c1-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e64c1-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e64c1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e64c1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e64c1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e64c1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e64c1-110">Prerequisites</span></span>

<span data-ttu-id="e64c1-111">To configure Azure AD integration with Pantheon, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e64c1-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="e64c1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e64c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e64c1-113">A Pantheon single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e64c1-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e64c1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e64c1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e64c1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e64c1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e64c1-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e64c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e64c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e64c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e64c1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e64c1-118">Scenario description</span></span>
<span data-ttu-id="e64c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e64c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e64c1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e64c1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e64c1-121">Adding Pantheon from the gallery</span><span class="sxs-lookup"><span data-stu-id="e64c1-121">Adding Pantheon from the gallery</span></span>
1. <span data-ttu-id="e64c1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e64c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="e64c1-123">Adding Pantheon from the gallery</span><span class="sxs-lookup"><span data-stu-id="e64c1-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="e64c1-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e64c1-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e64c1-125">**To add Pantheon from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e64c1-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e64c1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="e64c1-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e64c1-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="e64c1-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e64c1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="e64c1-133">In the search box, type **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-133">In the search box, type **Pantheon**.</span></span>

    ![Creating an Azure AD test user](./media/pantheon-tutorial/tutorial_pantheon_search.png)

1. <span data-ttu-id="e64c1-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e64c1-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e64c1-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e64c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e64c1-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e64c1-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e64c1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e64c1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="e64c1-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e64c1-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="e64c1-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="e64c1-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e64c1-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e64c1-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e64c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e64c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e64c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e64c1-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e64c1-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e64c1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e64c1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e64c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e64c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e64c1-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e64c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e64c1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span><span class="sxs-lookup"><span data-stu-id="e64c1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="e64c1-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e64c1-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="e64c1-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="e64c1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e64c1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/pantheon-tutorial/tutorial_pantheon_samlbase.png)

1. <span data-ttu-id="e64c1-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e64c1-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="e64c1-157">a.</span><span class="sxs-lookup"><span data-stu-id="e64c1-157">a.</span></span> <span data-ttu-id="e64c1-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="e64c1-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="e64c1-159">b.</span><span class="sxs-lookup"><span data-stu-id="e64c1-159">b.</span></span> <span data-ttu-id="e64c1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="e64c1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e64c1-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="e64c1-161">These values are not real.</span></span> <span data-ttu-id="e64c1-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="e64c1-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e64c1-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e64c1-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

1. <span data-ttu-id="e64c1-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span><span class="sxs-lookup"><span data-stu-id="e64c1-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="e64c1-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span><span class="sxs-lookup"><span data-stu-id="e64c1-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="e64c1-166">But for successful integration you need to adjust this value to match with user’s email address.</span><span class="sxs-lookup"><span data-stu-id="e64c1-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="e64c1-167">The integration will only work after doing the correct mapping.</span><span class="sxs-lookup"><span data-stu-id="e64c1-167">The integration will only work after doing the correct mapping.</span></span>

    ![Configure Single Sign-On](./media/pantheon-tutorial/tutorial_attribute.png)    


1. <span data-ttu-id="e64c1-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e64c1-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/pantheon-tutorial/tutorial_pantheon_certificate.png)

1. <span data-ttu-id="e64c1-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e64c1-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/pantheon-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e64c1-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e64c1-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e64c1-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="e64c1-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/pantheon-tutorial/tutorial_pantheon_configure.png) 

1. <span data-ttu-id="e64c1-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="e64c1-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="e64c1-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span><span class="sxs-lookup"><span data-stu-id="e64c1-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="e64c1-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="e64c1-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="e64c1-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="e64c1-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e64c1-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e64c1-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e64c1-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e64c1-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e64c1-182">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e64c1-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="e64c1-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="e64c1-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e64c1-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e64c1-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/pantheon-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="e64c1-188">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/pantheon-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="e64c1-190">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="e64c1-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/pantheon-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="e64c1-192">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e64c1-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e64c1-194">a.</span><span class="sxs-lookup"><span data-stu-id="e64c1-194">a.</span></span> <span data-ttu-id="e64c1-195">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e64c1-196">b.</span><span class="sxs-lookup"><span data-stu-id="e64c1-196">b.</span></span> <span data-ttu-id="e64c1-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e64c1-198">c.</span><span class="sxs-lookup"><span data-stu-id="e64c1-198">c.</span></span> <span data-ttu-id="e64c1-199">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e64c1-200">d.</span><span class="sxs-lookup"><span data-stu-id="e64c1-200">d.</span></span> <span data-ttu-id="e64c1-201">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="e64c1-202">Creating a Pantheon test user</span><span class="sxs-lookup"><span data-stu-id="e64c1-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="e64c1-203">In this section, you create a user called Britta Simon in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="e64c1-204">Please follow the below steps to add the user in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="e64c1-205">For SSO to work user needs to be created first in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="e64c1-206">Login to Pantheon with admin credentials.</span><span class="sxs-lookup"><span data-stu-id="e64c1-206">Login to Pantheon with admin credentials.</span></span>

1. <span data-ttu-id="e64c1-207">Navigate to **Organization** dashboard page.</span><span class="sxs-lookup"><span data-stu-id="e64c1-207">Navigate to **Organization** dashboard page.</span></span>
 
1. <span data-ttu-id="e64c1-208">Click **People**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-208">Click **People**.</span></span>

1. <span data-ttu-id="e64c1-209">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-209">Click **Add user**.</span></span>

1. <span data-ttu-id="e64c1-210">Enter the user's email address.</span><span class="sxs-lookup"><span data-stu-id="e64c1-210">Enter the user's email address.</span></span>

1. <span data-ttu-id="e64c1-211">Choose the user's role.</span><span class="sxs-lookup"><span data-stu-id="e64c1-211">Choose the user's role.</span></span>

1. <span data-ttu-id="e64c1-212">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e64c1-213">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e64c1-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e64c1-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span><span class="sxs-lookup"><span data-stu-id="e64c1-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![Assign User][200] 

<span data-ttu-id="e64c1-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e64c1-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="e64c1-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e64c1-219">In the applications list, select **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-219">In the applications list, select **Pantheon**.</span></span>

    ![Configure Single Sign-On](./media/pantheon-tutorial/tutorial_pantheon_app.png) 

1. <span data-ttu-id="e64c1-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e64c1-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="e64c1-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e64c1-223">Click **Add** button.</span></span> <span data-ttu-id="e64c1-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e64c1-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="e64c1-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e64c1-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e64c1-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e64c1-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e64c1-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e64c1-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e64c1-229">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="e64c1-229">Testing single sign-on</span></span>

<span data-ttu-id="e64c1-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e64c1-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e64c1-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span><span class="sxs-lookup"><span data-stu-id="e64c1-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="e64c1-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e64c1-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e64c1-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e64c1-233">Additional resources</span></span>

* [<span data-ttu-id="e64c1-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e64c1-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e64c1-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e64c1-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/pantheon-tutorial/tutorial_general_01.png
[2]: ./media/pantheon-tutorial/tutorial_general_02.png
[3]: ./media/pantheon-tutorial/tutorial_general_03.png
[4]: ./media/pantheon-tutorial/tutorial_general_04.png

[100]: ./media/pantheon-tutorial/tutorial_general_100.png

[200]: ./media/pantheon-tutorial/tutorial_general_200.png
[201]: ./media/pantheon-tutorial/tutorial_general_201.png
[202]: ./media/pantheon-tutorial/tutorial_general_202.png
[203]: ./media/pantheon-tutorial/tutorial_general_203.png

