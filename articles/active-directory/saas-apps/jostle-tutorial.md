---
title: 'Tutorial: Azure Active Directory integration with Jostle | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jostle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: b988d908b995b1144837c8642a8864a87e2fc61a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868383"
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="f8655-103">Tutorial: Azure Active Directory integration with Jostle</span><span class="sxs-lookup"><span data-stu-id="f8655-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="f8655-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8655-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8655-105">Integrating Jostle with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f8655-105">Integrating Jostle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f8655-106">You can control in Azure AD who has access to Jostle</span><span class="sxs-lookup"><span data-stu-id="f8655-106">You can control in Azure AD who has access to Jostle</span></span>
- <span data-ttu-id="f8655-107">You can enable your users to automatically get signed-on to Jostle (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f8655-107">You can enable your users to automatically get signed-on to Jostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8655-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f8655-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f8655-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f8655-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8655-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f8655-110">Prerequisites</span></span>

<span data-ttu-id="f8655-111">To configure Azure AD integration with Jostle, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f8655-111">To configure Azure AD integration with Jostle, you need the following items:</span></span>

- <span data-ttu-id="f8655-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f8655-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8655-113">A Jostle single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f8655-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8655-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f8655-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8655-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f8655-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8655-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f8655-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8655-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8655-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8655-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f8655-118">Scenario description</span></span>
<span data-ttu-id="f8655-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f8655-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="f8655-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f8655-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8655-121">Adding Jostle from the gallery</span><span class="sxs-lookup"><span data-stu-id="f8655-121">Adding Jostle from the gallery</span></span>
1. <span data-ttu-id="f8655-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8655-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-the-gallery"></a><span data-ttu-id="f8655-123">Adding Jostle from the gallery</span><span class="sxs-lookup"><span data-stu-id="f8655-123">Adding Jostle from the gallery</span></span>
<span data-ttu-id="f8655-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f8655-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f8655-125">**To add Jostle from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8655-125">**To add Jostle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f8655-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f8655-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![Active Directory][1]

1. <span data-ttu-id="f8655-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f8655-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f8655-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f8655-129">Then go to **All applications**.</span></span>

    ![Applications][2]

1. <span data-ttu-id="f8655-131">Click **Add** at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="f8655-131">Click **Add** at the top of the window.</span></span>

    ![add_01](./media/jostle-tutorial/add_01.png)

1. <span data-ttu-id="f8655-133">In the search box under **Add an application** type **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="f8655-133">In the search box under **Add an application** type **Jostle**.</span></span>

    ![add_02](./media/jostle-tutorial/add_02.png)

1. <span data-ttu-id="f8655-135">In the results panel, select **Jostle**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f8655-135">In the results panel, select **Jostle**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8655-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8655-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8655-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f8655-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f8655-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8655-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span></span> <span data-ttu-id="f8655-140">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f8655-140">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span></span>

<span data-ttu-id="f8655-141">In Jostle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f8655-141">In Jostle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f8655-142">To configure and test Azure AD single sign-on with Jostle, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f8655-142">To configure and test Azure AD single sign-on with Jostle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f8655-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f8655-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f8655-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8655-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f8655-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f8655-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f8655-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8655-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f8655-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f8655-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8655-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8655-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8655-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jostle application.</span><span class="sxs-lookup"><span data-stu-id="f8655-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="f8655-150">**To configure Azure AD single sign-on with Jostle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8655-150">**To configure Azure AD single sign-on with Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="f8655-151">In the Azure portal, on the **Jostle** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f8655-151">In the Azure portal, on the **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f8655-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8655-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/jostle-tutorial/tutorial_jostle_samlbase.png)

1. <span data-ttu-id="f8655-155">On the **Jostle Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8655-155">On the **Jostle Domain and URLs** section, perform the following steps:</span></span>

    ![url_01](./media/jostle-tutorial/url_01.png)

    <span data-ttu-id="f8655-157">a.</span><span class="sxs-lookup"><span data-stu-id="f8655-157">a.</span></span> <span data-ttu-id="f8655-158">In the **Sign-on URL** textbox, enter: `https://login-prod.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="f8655-158">In the **Sign-on URL** textbox, enter: `https://login-prod.jostle.us`</span></span>

    <span data-ttu-id="f8655-159">b.</span><span class="sxs-lookup"><span data-stu-id="f8655-159">b.</span></span> <span data-ttu-id="f8655-160">In the **Identifier** textbox, enter: `https://jostle.us`</span><span class="sxs-lookup"><span data-stu-id="f8655-160">In the **Identifier** textbox, enter: `https://jostle.us`</span></span>

    <span data-ttu-id="f8655-161">c.</span><span class="sxs-lookup"><span data-stu-id="f8655-161">c.</span></span> <span data-ttu-id="f8655-162">Check the box next to **Show advanced URL settings**</span><span class="sxs-lookup"><span data-stu-id="f8655-162">Check the box next to **Show advanced URL settings**</span></span>

    <span data-ttu-id="f8655-163">d.</span><span class="sxs-lookup"><span data-stu-id="f8655-163">d.</span></span> <span data-ttu-id="f8655-164">In the **Reply URL** textbox, enter: `https://login-prod.jostle.us/saml/SSO/alias/newjostle.us`</span><span class="sxs-lookup"><span data-stu-id="f8655-164">In the **Reply URL** textbox, enter: `https://login-prod.jostle.us/saml/SSO/alias/newjostle.us`</span></span>

1. <span data-ttu-id="f8655-165">On the **User Attributes** section, for the **User Identifier** field, enter: `user.userprincipalname`</span><span class="sxs-lookup"><span data-stu-id="f8655-165">On the **User Attributes** section, for the **User Identifier** field, enter: `user.userprincipalname`</span></span>

    ![url_02](./media/jostle-tutorial/url_02.png)

1. <span data-ttu-id="f8655-167">Click **Save** at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="f8655-167">Click **Save** at the top of the window.</span></span>

1. <span data-ttu-id="f8655-168">Go to **SAML Signing Certificate** and verify that it's set to **Active**.</span><span class="sxs-lookup"><span data-stu-id="f8655-168">Go to **SAML Signing Certificate** and verify that it's set to **Active**.</span></span> <span data-ttu-id="f8655-169">Then click **Metadata XML** to download the metadata file.</span><span class="sxs-lookup"><span data-stu-id="f8655-169">Then click **Metadata XML** to download the metadata file.</span></span>

    ![url_03](./media/jostle-tutorial/url_03.png)

1. <span data-ttu-id="f8655-171">To configure single sign-on on Jostle's side, you need to send the downloaded metadata XML to [Jostle support team](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="f8655-171">To configure single sign-on on Jostle's side, you need to send the downloaded metadata XML to [Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="f8655-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f8655-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f8655-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f8655-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f8655-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f8655-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f8655-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8655-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8655-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f8655-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8655-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8655-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f8655-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8655-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f8655-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f8655-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/jostle-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="f8655-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f8655-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/jostle-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="f8655-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f8655-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/jostle-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="f8655-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8655-186">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/jostle-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f8655-188">a.</span><span class="sxs-lookup"><span data-stu-id="f8655-188">a.</span></span> <span data-ttu-id="f8655-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8655-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8655-190">b.</span><span class="sxs-lookup"><span data-stu-id="f8655-190">b.</span></span> <span data-ttu-id="f8655-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8655-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8655-192">c.</span><span class="sxs-lookup"><span data-stu-id="f8655-192">c.</span></span> <span data-ttu-id="f8655-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f8655-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f8655-194">d.</span><span class="sxs-lookup"><span data-stu-id="f8655-194">d.</span></span> <span data-ttu-id="f8655-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8655-195">Click **Create**.</span></span>

### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="f8655-196">Creating a Jostle test user</span><span class="sxs-lookup"><span data-stu-id="f8655-196">Creating a Jostle test user</span></span>

<span data-ttu-id="f8655-197">In this section, you create a user called Britta Simon in Jostle.</span><span class="sxs-lookup"><span data-stu-id="f8655-197">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="f8655-198">If you don't know how to add Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) to add the test user and enable SSO.</span><span class="sxs-lookup"><span data-stu-id="f8655-198">If you don't know how to add Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) to add the test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="f8655-199">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="f8655-199">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f8655-200">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f8655-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f8655-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jostle.</span><span class="sxs-lookup"><span data-stu-id="f8655-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jostle.</span></span>

![Assign User][200]

<span data-ttu-id="f8655-203">**To assign Britta Simon to Jostle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8655-203">**To assign Britta Simon to Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="f8655-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f8655-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="f8655-206">In the applications list, select **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="f8655-206">In the applications list, select **Jostle**.</span></span>

    ![Configure Single Sign-On](./media/jostle-tutorial/tutorial_jostle_app.png)

1. <span data-ttu-id="f8655-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f8655-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

1. <span data-ttu-id="f8655-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f8655-210">Click **Add** button.</span></span> <span data-ttu-id="f8655-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8655-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f8655-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f8655-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f8655-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8655-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f8655-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8655-215">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="f8655-216">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8655-216">Testing single sign-on</span></span>

<span data-ttu-id="f8655-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f8655-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f8655-218">When you click the Jostle tile in the Access Panel, you should get automatically login page of Jostle application.</span><span class="sxs-lookup"><span data-stu-id="f8655-218">When you click the Jostle tile in the Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="f8655-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8655-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8655-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f8655-220">Additional resources</span></span>

* [<span data-ttu-id="f8655-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8655-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f8655-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8655-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/jostle-tutorial/tutorial_general_01.png
[2]: ./media/jostle-tutorial/tutorial_general_02.png
[3]: ./media/jostle-tutorial/tutorial_general_03.png
[4]: ./media/jostle-tutorial/tutorial_general_04.png

[100]: ./media/jostle-tutorial/tutorial_general_100.png

[200]: ./media/jostle-tutorial/tutorial_general_200.png
[201]: ./media/jostle-tutorial/tutorial_general_201.png
[202]: ./media/jostle-tutorial/tutorial_general_202.png
[203]: ./media/jostle-tutorial/tutorial_general_203.png
