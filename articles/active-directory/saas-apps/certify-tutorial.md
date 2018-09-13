---
title: 'Tutorial: Azure Active Directory integration with Certify | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Certify.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 68f1863ed8a901a93a1fe0626671a429adc96e61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870358"
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="cfd3c-103">Tutorial: Azure Active Directory integration with Certify</span><span class="sxs-lookup"><span data-stu-id="cfd3c-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="cfd3c-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfd3c-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfd3c-105">Integrating Certify with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cfd3c-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cfd3c-106">You can control in Azure AD who has access to Certify</span><span class="sxs-lookup"><span data-stu-id="cfd3c-106">You can control in Azure AD who has access to Certify</span></span>
- <span data-ttu-id="cfd3c-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cfd3c-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfd3c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cfd3c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cfd3c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cfd3c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfd3c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cfd3c-110">Prerequisites</span></span>

<span data-ttu-id="cfd3c-111">To configure Azure AD integration with Certify, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cfd3c-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

- <span data-ttu-id="cfd3c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cfd3c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfd3c-113">A Certify single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cfd3c-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfd3c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfd3c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cfd3c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfd3c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfd3c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfd3c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfd3c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cfd3c-118">Scenario description</span></span>
<span data-ttu-id="cfd3c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfd3c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cfd3c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfd3c-121">Adding Certify from the gallery</span><span class="sxs-lookup"><span data-stu-id="cfd3c-121">Adding Certify from the gallery</span></span>
1. <span data-ttu-id="cfd3c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfd3c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-the-gallery"></a><span data-ttu-id="cfd3c-123">Adding Certify from the gallery</span><span class="sxs-lookup"><span data-stu-id="cfd3c-123">Adding Certify from the gallery</span></span>
<span data-ttu-id="cfd3c-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cfd3c-125">**To add Certify from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cfd3c-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd3c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cfd3c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cfd3c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cfd3c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cfd3c-133">In the search box, type **Certify**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-133">In the search box, type **Certify**.</span></span>

    ![Creating an Azure AD test user](./media/certify-tutorial/tutorial_certify_search.png)

1. <span data-ttu-id="cfd3c-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfd3c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfd3c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfd3c-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cfd3c-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfd3c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span></span> <span data-ttu-id="cfd3c-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>

<span data-ttu-id="cfd3c-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cfd3c-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cfd3c-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cfd3c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cfd3c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cfd3c-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cfd3c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cfd3c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfd3c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfd3c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfd3c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="cfd3c-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cfd3c-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd3c-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cfd3c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/certify-tutorial/tutorial_certify_samlbase.png)

1. <span data-ttu-id="cfd3c-155">On the **Certify Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cfd3c-155">On the **Certify Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="cfd3c-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="cfd3c-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span></span>

1. <span data-ttu-id="cfd3c-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/certify-tutorial/tutorial_certify_certificate.png) 

1. <span data-ttu-id="cfd3c-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/certify-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cfd3c-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cfd3c-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="cfd3c-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/certify-tutorial/tutorial_certify_configure.png) 

1. <span data-ttu-id="cfd3c-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="cfd3c-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="cfd3c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cfd3c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cfd3c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cfd3c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cfd3c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfd3c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfd3c-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cfd3c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfd3c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cfd3c-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cfd3c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd3c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/certify-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cfd3c-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/certify-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cfd3c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/certify-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cfd3c-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cfd3c-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfd3c-182">a.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-182">a.</span></span> <span data-ttu-id="cfd3c-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfd3c-184">b.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-184">b.</span></span> <span data-ttu-id="cfd3c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfd3c-186">c.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-186">c.</span></span> <span data-ttu-id="cfd3c-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cfd3c-188">d.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-188">d.</span></span> <span data-ttu-id="cfd3c-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="cfd3c-190">Creating a Certify test user</span><span class="sxs-lookup"><span data-stu-id="cfd3c-190">Creating a Certify test user</span></span>

<span data-ttu-id="cfd3c-191">The objective of this section is to create a user called Britta Simon in Certify.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-191">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="cfd3c-192">Certify supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cfd3c-193">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-193">There is no action item for you in this section.</span></span> <span data-ttu-id="cfd3c-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="cfd3c-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="cfd3c-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cfd3c-196">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cfd3c-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cfd3c-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span></span>

![Assign User][200] 

<span data-ttu-id="cfd3c-199">**To assign Britta Simon to Certify, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cfd3c-199">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd3c-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cfd3c-202">In the applications list, select **Certify**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-202">In the applications list, select **Certify**.</span></span>

    ![Configure Single Sign-On](./media/certify-tutorial/tutorial_certify_app.png) 

1. <span data-ttu-id="cfd3c-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cfd3c-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-206">Click **Add** button.</span></span> <span data-ttu-id="cfd3c-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cfd3c-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cfd3c-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cfd3c-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfd3c-212">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfd3c-212">Testing single sign-on</span></span>

<span data-ttu-id="cfd3c-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="cfd3c-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span><span class="sxs-lookup"><span data-stu-id="cfd3c-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfd3c-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cfd3c-215">Additional resources</span></span>

* [<span data-ttu-id="cfd3c-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfd3c-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cfd3c-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cfd3c-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/certify-tutorial/tutorial_general_01.png
[2]: ./media/certify-tutorial/tutorial_general_02.png
[3]: ./media/certify-tutorial/tutorial_general_03.png
[4]: ./media/certify-tutorial/tutorial_general_04.png

[100]: ./media/certify-tutorial/tutorial_general_100.png

[200]: ./media/certify-tutorial/tutorial_general_200.png
[201]: ./media/certify-tutorial/tutorial_general_201.png
[202]: ./media/certify-tutorial/tutorial_general_202.png
[203]: ./media/certify-tutorial/tutorial_general_203.png

