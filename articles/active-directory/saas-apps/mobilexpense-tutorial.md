---
title: 'Tutorial: Azure Active Directory integration with Mobile Xpense | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mobile Xpense.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jeedes
ms.openlocfilehash: fd35cb67d0555919a1340c428bac042b67239469
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856066"
---
# <a name="tutorial-azure-active-directory-integration-with-mobile-xpense"></a><span data-ttu-id="06acf-103">Tutorial: Azure Active Directory integration with Mobile Xpense</span><span class="sxs-lookup"><span data-stu-id="06acf-103">Tutorial: Azure Active Directory integration with Mobile Xpense</span></span>

<span data-ttu-id="06acf-104">In this tutorial, you learn how to integrate Mobile Xpense with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06acf-104">In this tutorial, you learn how to integrate Mobile Xpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06acf-105">Integrating Mobile Xpense with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="06acf-105">Integrating Mobile Xpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="06acf-106">You can control in Azure AD who has access to Mobile Xpense.</span><span class="sxs-lookup"><span data-stu-id="06acf-106">You can control in Azure AD who has access to Mobile Xpense.</span></span>
- <span data-ttu-id="06acf-107">You can enable your users to automatically get signed-on to Mobile Xpense (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="06acf-107">You can enable your users to automatically get signed-on to Mobile Xpense (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="06acf-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="06acf-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="06acf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="06acf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06acf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="06acf-110">Prerequisites</span></span>

<span data-ttu-id="06acf-111">To configure Azure AD integration with Mobile Xpense, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="06acf-111">To configure Azure AD integration with Mobile Xpense, you need the following items:</span></span>

- <span data-ttu-id="06acf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="06acf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06acf-113">A Mobile Xpense single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="06acf-113">A Mobile Xpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06acf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="06acf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06acf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="06acf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06acf-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="06acf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06acf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06acf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06acf-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="06acf-118">Scenario description</span></span>
<span data-ttu-id="06acf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="06acf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06acf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="06acf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06acf-121">Adding Mobile Xpense from the gallery</span><span class="sxs-lookup"><span data-stu-id="06acf-121">Adding Mobile Xpense from the gallery</span></span>
1. <span data-ttu-id="06acf-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="06acf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobile-xpense-from-the-gallery"></a><span data-ttu-id="06acf-123">Adding Mobile Xpense from the gallery</span><span class="sxs-lookup"><span data-stu-id="06acf-123">Adding Mobile Xpense from the gallery</span></span>
<span data-ttu-id="06acf-124">To configure the integration of Mobile Xpense into Azure AD, you need to add Mobile Xpense from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="06acf-124">To configure the integration of Mobile Xpense into Azure AD, you need to add Mobile Xpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="06acf-125">**To add Mobile Xpense from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06acf-125">**To add Mobile Xpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="06acf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="06acf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="06acf-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="06acf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="06acf-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="06acf-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="06acf-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="06acf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="06acf-133">In the search box, type **Mobile Xpense**, select **Mobile Xpense** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="06acf-133">In the search box, type **Mobile Xpense**, select **Mobile Xpense** from result panel then click **Add** button to add the application.</span></span>

    ![Mobile Xpense in the results list](./media/mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="06acf-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="06acf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="06acf-136">In this section, you configure and test Azure AD single sign-on with Mobile Xpense based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="06acf-136">In this section, you configure and test Azure AD single sign-on with Mobile Xpense based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="06acf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mobile Xpense is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06acf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mobile Xpense is to a user in Azure AD.</span></span> <span data-ttu-id="06acf-138">In other words, a link relationship between an Azure AD user and the related user in Mobile Xpense needs to be established.</span><span class="sxs-lookup"><span data-stu-id="06acf-138">In other words, a link relationship between an Azure AD user and the related user in Mobile Xpense needs to be established.</span></span>

<span data-ttu-id="06acf-139">In Mobile Xpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="06acf-139">In Mobile Xpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="06acf-140">To configure and test Azure AD single sign-on with Mobile Xpense, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="06acf-140">To configure and test Azure AD single sign-on with Mobile Xpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="06acf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="06acf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="06acf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06acf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="06acf-143">**[Create a Mobile Xpense test user](#create-a-mobile-xpense-test-user)** - to have a counterpart of Britta Simon in Mobile Xpense that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="06acf-143">**[Create a Mobile Xpense test user](#create-a-mobile-xpense-test-user)** - to have a counterpart of Britta Simon in Mobile Xpense that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="06acf-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="06acf-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="06acf-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="06acf-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="06acf-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="06acf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="06acf-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mobile Xpense application.</span><span class="sxs-lookup"><span data-stu-id="06acf-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mobile Xpense application.</span></span>

<span data-ttu-id="06acf-148">**To configure Azure AD single sign-on with Mobile Xpense, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06acf-148">**To configure Azure AD single sign-on with Mobile Xpense, perform the following steps:**</span></span>

1. <span data-ttu-id="06acf-149">In the Azure portal, on the **Mobile Xpense** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="06acf-149">In the Azure portal, on the **Mobile Xpense** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="06acf-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="06acf-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

1. <span data-ttu-id="06acf-153">On the **Mobile Xpense Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="06acf-153">On the **Mobile Xpense Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Mobile Xpense Domain and URLs single sign-on information](./media/mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="06acf-155">a.</span><span class="sxs-lookup"><span data-stu-id="06acf-155">a.</span></span> <span data-ttu-id="06acf-156">In the **Identifier** textbox, type a URL: `https://mobilexpense.com/ServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="06acf-156">In the **Identifier** textbox, type a URL: `https://mobilexpense.com/ServiceProvider`</span></span>

    <span data-ttu-id="06acf-157">b.</span><span class="sxs-lookup"><span data-stu-id="06acf-157">b.</span></span> <span data-ttu-id="06acf-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub-domain>.mobilexpense.com/NET/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="06acf-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub-domain>.mobilexpense.com/NET/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

1. <span data-ttu-id="06acf-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="06acf-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Mobile Xpense Domain and URLs single sign-on information](./media/mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

    <span data-ttu-id="06acf-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="06acf-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.mobilexpense.com/<customername>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="06acf-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="06acf-162">These values are not real.</span></span> <span data-ttu-id="06acf-163">Update these values with the actual Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="06acf-163">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="06acf-164">Contact [Mobile Xpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="06acf-164">Contact [Mobile Xpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

1. <span data-ttu-id="06acf-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="06acf-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

1. <span data-ttu-id="06acf-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="06acf-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/mobilexpense-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="06acf-169">To configure single sign-on on **Mobile Xpense** side, you need to send the downloaded **Metadata XML** to [Mobile Xpense support team](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="06acf-169">To configure single sign-on on **Mobile Xpense** side, you need to send the downloaded **Metadata XML** to [Mobile Xpense support team](http://www.mobilexpense.net/contact).</span></span> <span data-ttu-id="06acf-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="06acf-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="06acf-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="06acf-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="06acf-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="06acf-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="06acf-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06acf-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="06acf-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="06acf-174">Create an Azure AD test user</span></span>

<span data-ttu-id="06acf-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06acf-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="06acf-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06acf-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="06acf-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="06acf-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/mobilexpense-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="06acf-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="06acf-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/mobilexpense-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="06acf-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="06acf-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/mobilexpense-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="06acf-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="06acf-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/mobilexpense-tutorial/create_aaduser_04.png)

    <span data-ttu-id="06acf-186">a.</span><span class="sxs-lookup"><span data-stu-id="06acf-186">a.</span></span> <span data-ttu-id="06acf-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06acf-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06acf-188">b.</span><span class="sxs-lookup"><span data-stu-id="06acf-188">b.</span></span> <span data-ttu-id="06acf-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06acf-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="06acf-190">c.</span><span class="sxs-lookup"><span data-stu-id="06acf-190">c.</span></span> <span data-ttu-id="06acf-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="06acf-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="06acf-192">d.</span><span class="sxs-lookup"><span data-stu-id="06acf-192">d.</span></span> <span data-ttu-id="06acf-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="06acf-193">Click **Create**.</span></span>
 
### <a name="create-a-mobile-xpense-test-user"></a><span data-ttu-id="06acf-194">Create a Mobile Xpense test user</span><span class="sxs-lookup"><span data-stu-id="06acf-194">Create a Mobile Xpense test user</span></span>

<span data-ttu-id="06acf-195">In this section, you create a user called Britta Simon in MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="06acf-195">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="06acf-196">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span><span class="sxs-lookup"><span data-stu-id="06acf-196">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="06acf-197">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="06acf-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="06acf-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="06acf-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="06acf-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mobile Xpense.</span><span class="sxs-lookup"><span data-stu-id="06acf-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mobile Xpense.</span></span>

![Assign the user role][200] 

<span data-ttu-id="06acf-201">**To assign Britta Simon to Mobile Xpense, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06acf-201">**To assign Britta Simon to Mobile Xpense, perform the following steps:**</span></span>

1. <span data-ttu-id="06acf-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="06acf-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="06acf-204">In the applications list, select **Mobile Xpense**.</span><span class="sxs-lookup"><span data-stu-id="06acf-204">In the applications list, select **Mobile Xpense**.</span></span>

    ![The Mobile Xpense link in the Applications list](./media/mobilexpense-tutorial/tutorial_mobilexpense_app.png)  

1. <span data-ttu-id="06acf-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="06acf-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="06acf-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="06acf-208">Click **Add** button.</span></span> <span data-ttu-id="06acf-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="06acf-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="06acf-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="06acf-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="06acf-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="06acf-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="06acf-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="06acf-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="06acf-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="06acf-214">Test single sign-on</span></span>

<span data-ttu-id="06acf-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="06acf-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="06acf-216">When you click the Mobile Xpense tile in the Access Panel, you should get automatically signed-on to your Mobile Xpense application.</span><span class="sxs-lookup"><span data-stu-id="06acf-216">When you click the Mobile Xpense tile in the Access Panel, you should get automatically signed-on to your Mobile Xpense application.</span></span>
<span data-ttu-id="06acf-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06acf-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06acf-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="06acf-218">Additional resources</span></span>

* [<span data-ttu-id="06acf-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06acf-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="06acf-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="06acf-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/mobilexpense-tutorial/tutorial_general_203.png
