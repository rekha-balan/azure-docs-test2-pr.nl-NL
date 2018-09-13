---
title: 'Tutorial: Azure Active Directory integration with Skilljar | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Skilljar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c572f556-98a3-48e6-8e4c-e634b7a2ba70
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 6a0463640f9a7194632a65cdb10653a520fcc0c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867218"
---
# <a name="tutorial-azure-active-directory-integration-with-skilljar"></a><span data-ttu-id="ae665-103">Tutorial: Azure Active Directory integration with Skilljar</span><span class="sxs-lookup"><span data-stu-id="ae665-103">Tutorial: Azure Active Directory integration with Skilljar</span></span>

<span data-ttu-id="ae665-104">In this tutorial, you learn how to integrate Skilljar with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae665-104">In this tutorial, you learn how to integrate Skilljar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae665-105">Integrating Skilljar with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ae665-105">Integrating Skilljar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae665-106">You can control in Azure AD who has access to Skilljar</span><span class="sxs-lookup"><span data-stu-id="ae665-106">You can control in Azure AD who has access to Skilljar</span></span>
- <span data-ttu-id="ae665-107">You can enable your users to automatically get signed-on to Skilljar (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ae665-107">You can enable your users to automatically get signed-on to Skilljar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae665-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ae665-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae665-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ae665-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae665-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae665-110">Prerequisites</span></span>

<span data-ttu-id="ae665-111">To configure Azure AD integration with Skilljar, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ae665-111">To configure Azure AD integration with Skilljar, you need the following items:</span></span>

- <span data-ttu-id="ae665-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ae665-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae665-113">A Skilljar single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ae665-113">A Skilljar single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae665-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ae665-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae665-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ae665-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae665-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ae665-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae665-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae665-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae665-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ae665-118">Scenario description</span></span>
<span data-ttu-id="ae665-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ae665-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae665-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae665-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae665-121">Adding Skilljar from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae665-121">Adding Skilljar from the gallery</span></span>
1. <span data-ttu-id="ae665-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae665-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skilljar-from-the-gallery"></a><span data-ttu-id="ae665-123">Adding Skilljar from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae665-123">Adding Skilljar from the gallery</span></span>
<span data-ttu-id="ae665-124">To configure the integration of Skilljar into Azure AD, you need to add Skilljar from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ae665-124">To configure the integration of Skilljar into Azure AD, you need to add Skilljar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae665-125">**To add Skilljar from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae665-125">**To add Skilljar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae665-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ae665-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="ae665-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ae665-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae665-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae665-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="ae665-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ae665-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="ae665-133">In the search box, type **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="ae665-133">In the search box, type **Skilljar**.</span></span>

    ![Creating an Azure AD test user](./media/skilljar-tutorial/tutorial_skilljar_search.png)

1. <span data-ttu-id="ae665-135">In the results panel, select **Skilljar**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ae665-135">In the results panel, select **Skilljar**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/skilljar-tutorial/tutorial_skilljar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae665-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae665-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae665-138">In this section, you configure and test Azure AD single sign-on with Skilljar based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae665-138">In this section, you configure and test Azure AD single sign-on with Skilljar based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae665-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skilljar is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae665-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skilljar is to a user in Azure AD.</span></span> <span data-ttu-id="ae665-140">In other words, a link relationship between an Azure AD user and the related user in Skilljar needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ae665-140">In other words, a link relationship between an Azure AD user and the related user in Skilljar needs to be established.</span></span>

<span data-ttu-id="ae665-141">In Skilljar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ae665-141">In Skilljar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae665-142">To configure and test Azure AD single sign-on with Skilljar, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae665-142">To configure and test Azure AD single sign-on with Skilljar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae665-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ae665-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ae665-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae665-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ae665-145">**[Creating a Skilljar test user](#creating-a-skilljar-test-user)** - to have a counterpart of Britta Simon in Skilljar that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ae665-145">**[Creating a Skilljar test user](#creating-a-skilljar-test-user)** - to have a counterpart of Britta Simon in Skilljar that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ae665-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae665-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ae665-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ae665-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae665-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae665-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae665-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skilljar application.</span><span class="sxs-lookup"><span data-stu-id="ae665-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skilljar application.</span></span>

<span data-ttu-id="ae665-150">**To configure Azure AD single sign-on with Skilljar, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae665-150">**To configure Azure AD single sign-on with Skilljar, perform the following steps:**</span></span>

1. <span data-ttu-id="ae665-151">In the Azure portal, on the **Skilljar** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ae665-151">In the Azure portal, on the **Skilljar** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="ae665-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae665-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/skilljar-tutorial/tutorial_skilljar_samlbase.png)

1. <span data-ttu-id="ae665-155">On the **Skilljar Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae665-155">On the **Skilljar Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/skilljar-tutorial/tutorial_skilljar_url.png)

    <span data-ttu-id="ae665-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae665-157">a.</span></span> <span data-ttu-id="ae665-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="ae665-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span></span>

    <span data-ttu-id="ae665-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae665-159">b.</span></span> <span data-ttu-id="ae665-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="ae665-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae665-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ae665-161">These values are not real.</span></span> <span data-ttu-id="ae665-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="ae665-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ae665-163">Contact [Skilljar Client support team](http://support.skilljar.com/hc/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ae665-163">Contact [Skilljar Client support team](http://support.skilljar.com/hc/) to get these values.</span></span> 
 
1. <span data-ttu-id="ae665-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ae665-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/skilljar-tutorial/tutorial_skilljar_certificate.png) 

1. <span data-ttu-id="ae665-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ae665-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/skilljar-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ae665-168">To configure single sign-on on **Skilljar** side, you need to send the downloaded **Metadata XML**, and **Name Identifier Format Value - urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** to [Skilljar support team](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="ae665-168">To configure single sign-on on **Skilljar** side, you need to send the downloaded **Metadata XML**, and **Name Identifier Format Value - urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** to [Skilljar support team](http://support.skilljar.com/hc/).</span></span> <span data-ttu-id="ae665-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="ae665-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ae665-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="ae665-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae665-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="ae665-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae665-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae665-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae665-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae665-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae665-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae665-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ae665-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae665-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae665-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ae665-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/skilljar-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="ae665-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ae665-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/skilljar-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="ae665-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ae665-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/skilljar-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="ae665-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae665-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/skilljar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae665-185">a.</span><span class="sxs-lookup"><span data-stu-id="ae665-185">a.</span></span> <span data-ttu-id="ae665-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae665-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae665-187">b.</span><span class="sxs-lookup"><span data-stu-id="ae665-187">b.</span></span> <span data-ttu-id="ae665-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae665-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae665-189">c.</span><span class="sxs-lookup"><span data-stu-id="ae665-189">c.</span></span> <span data-ttu-id="ae665-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ae665-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae665-191">d.</span><span class="sxs-lookup"><span data-stu-id="ae665-191">d.</span></span> <span data-ttu-id="ae665-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae665-192">Click **Create**.</span></span>
 
### <a name="creating-a-skilljar-test-user"></a><span data-ttu-id="ae665-193">Creating a Skilljar test user</span><span class="sxs-lookup"><span data-stu-id="ae665-193">Creating a Skilljar test user</span></span>

<span data-ttu-id="ae665-194">The objective of this section is to create a user called Britta Simon in Skilljar.</span><span class="sxs-lookup"><span data-stu-id="ae665-194">The objective of this section is to create a user called Britta Simon in Skilljar.</span></span> <span data-ttu-id="ae665-195">Skilljar supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="ae665-195">Skilljar supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ae665-196">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="ae665-196">There is no action item for you in this section.</span></span> <span data-ttu-id="ae665-197">A new user is created during an attempt to access Skilljar if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="ae665-197">A new user is created during an attempt to access Skilljar if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="ae665-198">If you need to create a user manually, you need to contact the [Skilljar support team](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="ae665-198">If you need to create a user manually, you need to contact the [Skilljar support team](http://support.skilljar.com/hc/).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae665-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae665-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae665-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skilljar.</span><span class="sxs-lookup"><span data-stu-id="ae665-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skilljar.</span></span>

![Assign User][200] 

<span data-ttu-id="ae665-202">**To assign Britta Simon to Skilljar, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae665-202">**To assign Britta Simon to Skilljar, perform the following steps:**</span></span>

1. <span data-ttu-id="ae665-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae665-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ae665-205">In the applications list, select **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="ae665-205">In the applications list, select **Skilljar**.</span></span>

    ![Configure Single Sign-On](./media/skilljar-tutorial/tutorial_skilljar_app.png) 

1. <span data-ttu-id="ae665-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ae665-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="ae665-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ae665-209">Click **Add** button.</span></span> <span data-ttu-id="ae665-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae665-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="ae665-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ae665-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ae665-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae665-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ae665-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae665-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae665-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae665-215">Testing single sign-on</span></span>

<span data-ttu-id="ae665-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ae665-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="ae665-217">When you click the Skilljar tile in the Access Panel, you should get automatically signed-on to your Skilljar application.</span><span class="sxs-lookup"><span data-stu-id="ae665-217">When you click the Skilljar tile in the Access Panel, you should get automatically signed-on to your Skilljar application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae665-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ae665-218">Additional resources</span></span>

* [<span data-ttu-id="ae665-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae665-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ae665-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae665-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skilljar-tutorial/tutorial_general_01.png
[2]: ./media/skilljar-tutorial/tutorial_general_02.png
[3]: ./media/skilljar-tutorial/tutorial_general_03.png
[4]: ./media/skilljar-tutorial/tutorial_general_04.png

[100]: ./media/skilljar-tutorial/tutorial_general_100.png

[200]: ./media/skilljar-tutorial/tutorial_general_200.png
[201]: ./media/skilljar-tutorial/tutorial_general_201.png
[202]: ./media/skilljar-tutorial/tutorial_general_202.png
[203]: ./media/skilljar-tutorial/tutorial_general_203.png

