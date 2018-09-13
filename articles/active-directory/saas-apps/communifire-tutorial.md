---
title: 'Tutorial: Azure Active Directory integration with Communifire | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Communifire.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: de2a164d-2115-43e7-a9ed-e54f483f4aeb
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: jeedes
ms.openlocfilehash: 590d8fe0e974587effc7d8a3c59546b5684b146c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967532"
---
# <a name="tutorial-azure-active-directory-integration-with-communifire"></a><span data-ttu-id="f4765-103">Tutorial: Azure Active Directory integration with Communifire</span><span class="sxs-lookup"><span data-stu-id="f4765-103">Tutorial: Azure Active Directory integration with Communifire</span></span>

<span data-ttu-id="f4765-104">In this tutorial, you learn how to integrate Communifire with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4765-104">In this tutorial, you learn how to integrate Communifire with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4765-105">Integrating Communifire with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f4765-105">Integrating Communifire with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f4765-106">You can control in Azure AD who has access to Communifire.</span><span class="sxs-lookup"><span data-stu-id="f4765-106">You can control in Azure AD who has access to Communifire.</span></span>
- <span data-ttu-id="f4765-107">You can enable your users to automatically get signed-on to Communifire (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="f4765-107">You can enable your users to automatically get signed-on to Communifire (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f4765-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4765-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f4765-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f4765-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4765-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4765-110">Prerequisites</span></span>

<span data-ttu-id="f4765-111">To configure Azure AD integration with Communifire, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f4765-111">To configure Azure AD integration with Communifire, you need the following items:</span></span>

- <span data-ttu-id="f4765-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f4765-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4765-113">A Communifire single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f4765-113">A Communifire single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4765-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f4765-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4765-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f4765-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4765-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f4765-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4765-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4765-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4765-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f4765-118">Scenario description</span></span>
<span data-ttu-id="f4765-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f4765-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4765-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f4765-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4765-121">Adding Communifire from the gallery</span><span class="sxs-lookup"><span data-stu-id="f4765-121">Adding Communifire from the gallery</span></span>
1. <span data-ttu-id="f4765-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f4765-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-communifire-from-the-gallery"></a><span data-ttu-id="f4765-123">Adding Communifire from the gallery</span><span class="sxs-lookup"><span data-stu-id="f4765-123">Adding Communifire from the gallery</span></span>
<span data-ttu-id="f4765-124">To configure the integration of Communifire into Azure AD, you need to add Communifire from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f4765-124">To configure the integration of Communifire into Azure AD, you need to add Communifire from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f4765-125">**To add Communifire from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f4765-125">**To add Communifire from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f4765-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f4765-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="f4765-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f4765-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f4765-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f4765-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="f4765-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f4765-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="f4765-133">In the search box, type **Communifire**, select **Communifire** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f4765-133">In the search box, type **Communifire**, select **Communifire** from result panel then click **Add** button to add the application.</span></span>

    ![Communifire in the results list](./media/communifire-tutorial/tutorial_communifire_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f4765-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f4765-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f4765-136">In this section, you configure and test Azure AD single sign-on with Communifire based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f4765-136">In this section, you configure and test Azure AD single sign-on with Communifire based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4765-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Communifire is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4765-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Communifire is to a user in Azure AD.</span></span> <span data-ttu-id="f4765-138">In other words, a link relationship between an Azure AD user and the related user in Communifire needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f4765-138">In other words, a link relationship between an Azure AD user and the related user in Communifire needs to be established.</span></span>

<span data-ttu-id="f4765-139">In Communifire, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f4765-139">In Communifire, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f4765-140">To configure and test Azure AD single sign-on with Communifire, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f4765-140">To configure and test Azure AD single sign-on with Communifire, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f4765-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f4765-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f4765-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4765-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f4765-143">**[Create a Communifire test user](#create-a-communifire-test-user)** - to have a counterpart of Britta Simon in Communifire that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f4765-143">**[Create a Communifire test user](#create-a-communifire-test-user)** - to have a counterpart of Britta Simon in Communifire that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f4765-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f4765-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f4765-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f4765-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f4765-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f4765-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f4765-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Communifire application.</span><span class="sxs-lookup"><span data-stu-id="f4765-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Communifire application.</span></span>

<span data-ttu-id="f4765-148">**To configure Azure AD single sign-on with Communifire, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f4765-148">**To configure Azure AD single sign-on with Communifire, perform the following steps:**</span></span>

1. <span data-ttu-id="f4765-149">In the Azure portal, on the **Communifire** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f4765-149">In the Azure portal, on the **Communifire** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="f4765-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f4765-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/communifire-tutorial/tutorial_communifire_samlbase.png)

1. <span data-ttu-id="f4765-153">On the **Communifire Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f4765-153">On the **Communifire Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Communifire Domain and URLs single sign-on information](./media/communifire-tutorial/tutorial_communifire_url.png)

    <span data-ttu-id="f4765-155">a.</span><span class="sxs-lookup"><span data-stu-id="f4765-155">a.</span></span> <span data-ttu-id="f4765-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.communifire.com`</span><span class="sxs-lookup"><span data-stu-id="f4765-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.communifire.com`</span></span>

    <span data-ttu-id="f4765-157">b.</span><span class="sxs-lookup"><span data-stu-id="f4765-157">b.</span></span> <span data-ttu-id="f4765-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.communifire.com/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="f4765-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.communifire.com/SAML/AssertionConsumerService.aspx`</span></span>

1. <span data-ttu-id="f4765-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f4765-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Communifire Domain and URLs single sign-on information](./media/communifire-tutorial/tutorial_communifire_url1.png)

    <span data-ttu-id="f4765-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.communifire.com/login`</span><span class="sxs-lookup"><span data-stu-id="f4765-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.communifire.com/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f4765-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f4765-162">These values are not real.</span></span> <span data-ttu-id="f4765-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="f4765-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f4765-164">Contact [Communifire Client support team](https://my.axerosolutions.com/spaces/77/communifire-support/help/welcome) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f4765-164">Contact [Communifire Client support team](https://my.axerosolutions.com/spaces/77/communifire-support/help/welcome) to get these values.</span></span> 

1. <span data-ttu-id="f4765-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f4765-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/communifire-tutorial/tutorial_communifire_certificate.png) 

1.  <span data-ttu-id="f4765-167">Check **Show advanced certificate Signing settings** and select **Signing Option** as **Sign SAML response and assertion**.</span><span class="sxs-lookup"><span data-stu-id="f4765-167">Check **Show advanced certificate Signing settings** and select **Signing Option** as **Sign SAML response and assertion**.</span></span>

    ![The Certificate option](./media/communifire-tutorial/tutorial_communifire_certificateoption.png) 

1. <span data-ttu-id="f4765-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f4765-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/communifire-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="f4765-171">To configure single sign-on on **Communifire** side, you need to send the downloaded **Metadata XML** to [Communifire support team](https://my.axerosolutions.com/spaces/77/communifire-support/help/welcome).</span><span class="sxs-lookup"><span data-stu-id="f4765-171">To configure single sign-on on **Communifire** side, you need to send the downloaded **Metadata XML** to [Communifire support team](https://my.axerosolutions.com/spaces/77/communifire-support/help/welcome).</span></span> <span data-ttu-id="f4765-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f4765-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f4765-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f4765-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f4765-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f4765-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f4765-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4765-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f4765-176">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f4765-176">Create an Azure AD test user</span></span>

<span data-ttu-id="f4765-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4765-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="f4765-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f4765-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f4765-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f4765-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/communifire-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="f4765-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f4765-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/communifire-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="f4765-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f4765-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/communifire-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="f4765-186">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f4765-186">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/communifire-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f4765-188">a.</span><span class="sxs-lookup"><span data-stu-id="f4765-188">a.</span></span> <span data-ttu-id="f4765-189">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4765-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4765-190">b.</span><span class="sxs-lookup"><span data-stu-id="f4765-190">b.</span></span> <span data-ttu-id="f4765-191">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4765-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f4765-192">c.</span><span class="sxs-lookup"><span data-stu-id="f4765-192">c.</span></span> <span data-ttu-id="f4765-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="f4765-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f4765-194">d.</span><span class="sxs-lookup"><span data-stu-id="f4765-194">d.</span></span> <span data-ttu-id="f4765-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f4765-195">Click **Create**.</span></span>
 
### <a name="create-a-communifire-test-user"></a><span data-ttu-id="f4765-196">Create a Communifire test user</span><span class="sxs-lookup"><span data-stu-id="f4765-196">Create a Communifire test user</span></span>

<span data-ttu-id="f4765-197">The objective of this section is to create a user called Britta Simon in Communifire.</span><span class="sxs-lookup"><span data-stu-id="f4765-197">The objective of this section is to create a user called Britta Simon in Communifire.</span></span> <span data-ttu-id="f4765-198">Communifire supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="f4765-198">Communifire supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f4765-199">A new user is created after saving the profile details during an attempt to access Communifire if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="f4765-199">A new user is created after saving the profile details during an attempt to access Communifire if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="f4765-200">If you need to create a user manually, Contact [Communifire support team](https://my.axerosolutions.com/spaces/77/communifire-support/help/welcome).</span><span class="sxs-lookup"><span data-stu-id="f4765-200">If you need to create a user manually, Contact [Communifire support team](https://my.axerosolutions.com/spaces/77/communifire-support/help/welcome).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f4765-201">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f4765-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="f4765-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Communifire.</span><span class="sxs-lookup"><span data-stu-id="f4765-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Communifire.</span></span>

![Assign the user role][200] 

<span data-ttu-id="f4765-204">**To assign Britta Simon to Communifire, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f4765-204">**To assign Britta Simon to Communifire, perform the following steps:**</span></span>

1. <span data-ttu-id="f4765-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f4765-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f4765-207">In the applications list, select **Communifire**.</span><span class="sxs-lookup"><span data-stu-id="f4765-207">In the applications list, select **Communifire**.</span></span>

    ![The Communifire link in the Applications list](./media/communifire-tutorial/tutorial_communifire_app.png)  

1. <span data-ttu-id="f4765-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f4765-209">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="f4765-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f4765-211">Click **Add** button.</span></span> <span data-ttu-id="f4765-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f4765-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="f4765-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f4765-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f4765-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f4765-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f4765-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f4765-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f4765-217">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f4765-217">Test single sign-on</span></span>

<span data-ttu-id="f4765-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f4765-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f4765-219">When you click the Communifire tile in the Access Panel, you should get automatically signed-on to your Communifire application.</span><span class="sxs-lookup"><span data-stu-id="f4765-219">When you click the Communifire tile in the Access Panel, you should get automatically signed-on to your Communifire application.</span></span>
<span data-ttu-id="f4765-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4765-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f4765-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f4765-221">Additional resources</span></span>

* [<span data-ttu-id="f4765-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4765-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f4765-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4765-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/communifire-tutorial/tutorial_general_01.png
[2]: ./media/communifire-tutorial/tutorial_general_02.png
[3]: ./media/communifire-tutorial/tutorial_general_03.png
[4]: ./media/communifire-tutorial/tutorial_general_04.png

[100]: ./media/communifire-tutorial/tutorial_general_100.png

[200]: ./media/communifire-tutorial/tutorial_general_200.png
[201]: ./media/communifire-tutorial/tutorial_general_201.png
[202]: ./media/communifire-tutorial/tutorial_general_202.png
[203]: ./media/communifire-tutorial/tutorial_general_203.png

