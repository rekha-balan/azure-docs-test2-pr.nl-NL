---
title: 'Tutorial: Azure Active Directory integration with Amplitude | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Amplitude.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 496c9ffa-c833-41fa-8d17-2dc3044954d1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2018
ms.author: jeedes
ms.openlocfilehash: a2815b60799f98071915a0f06908fd92ff3fb2f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869998"
---
# <a name="tutorial-azure-active-directory-integration-with-amplitude"></a><span data-ttu-id="99919-103">Tutorial: Azure Active Directory integration with Amplitude</span><span class="sxs-lookup"><span data-stu-id="99919-103">Tutorial: Azure Active Directory integration with Amplitude</span></span>

<span data-ttu-id="99919-104">In this tutorial, you learn how to integrate Amplitude with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99919-104">In this tutorial, you learn how to integrate Amplitude with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99919-105">Integrating Amplitude with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="99919-105">Integrating Amplitude with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="99919-106">You can control in Azure AD who has access to Amplitude.</span><span class="sxs-lookup"><span data-stu-id="99919-106">You can control in Azure AD who has access to Amplitude.</span></span>
- <span data-ttu-id="99919-107">You can enable your users to automatically get signed-on to Amplitude (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="99919-107">You can enable your users to automatically get signed-on to Amplitude (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="99919-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="99919-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="99919-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="99919-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99919-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99919-110">Prerequisites</span></span>

<span data-ttu-id="99919-111">To configure Azure AD integration with Amplitude, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="99919-111">To configure Azure AD integration with Amplitude, you need the following items:</span></span>

- <span data-ttu-id="99919-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="99919-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99919-113">An Amplitude single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="99919-113">An Amplitude single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="99919-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="99919-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="99919-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="99919-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99919-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="99919-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="99919-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99919-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99919-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="99919-118">Scenario description</span></span>
<span data-ttu-id="99919-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="99919-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="99919-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="99919-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99919-121">Adding Amplitude from the gallery</span><span class="sxs-lookup"><span data-stu-id="99919-121">Adding Amplitude from the gallery</span></span>
2. <span data-ttu-id="99919-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99919-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amplitude-from-the-gallery"></a><span data-ttu-id="99919-123">Adding Amplitude from the gallery</span><span class="sxs-lookup"><span data-stu-id="99919-123">Adding Amplitude from the gallery</span></span>
<span data-ttu-id="99919-124">To configure the integration of Amplitude into Azure AD, you need to add Amplitude from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="99919-124">To configure the integration of Amplitude into Azure AD, you need to add Amplitude from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99919-125">**To add Amplitude from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99919-125">**To add Amplitude from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99919-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="99919-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="99919-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="99919-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="99919-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="99919-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="99919-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="99919-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="99919-133">In the search box, type **Amplitude**, select **Amplitude** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="99919-133">In the search box, type **Amplitude**, select **Amplitude** from result panel then click **Add** button to add the application.</span></span>

    ![Amplitude in the results list](./media/amplitude-tutorial/tutorial_amplitude_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="99919-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99919-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="99919-136">In this section, you configure and test Azure AD single sign-on with Amplitude based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99919-136">In this section, you configure and test Azure AD single sign-on with Amplitude based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99919-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Amplitude is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99919-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Amplitude is to a user in Azure AD.</span></span> <span data-ttu-id="99919-138">In other words, a link relationship between an Azure AD user and the related user in Amplitude needs to be established.</span><span class="sxs-lookup"><span data-stu-id="99919-138">In other words, a link relationship between an Azure AD user and the related user in Amplitude needs to be established.</span></span>

<span data-ttu-id="99919-139">To configure and test Azure AD single sign-on with Amplitude, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="99919-139">To configure and test Azure AD single sign-on with Amplitude, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99919-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="99919-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99919-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99919-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99919-142">**[Create an Amplitude test user](#create-an-amplitude-test-user)** - to have a counterpart of Britta Simon in Amplitude that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="99919-142">**[Create an Amplitude test user](#create-an-amplitude-test-user)** - to have a counterpart of Britta Simon in Amplitude that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="99919-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="99919-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99919-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="99919-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="99919-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99919-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="99919-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amplitude application.</span><span class="sxs-lookup"><span data-stu-id="99919-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amplitude application.</span></span>

<span data-ttu-id="99919-147">**To configure Azure AD single sign-on with Amplitude, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99919-147">**To configure Azure AD single sign-on with Amplitude, perform the following steps:**</span></span>

1. <span data-ttu-id="99919-148">In the Azure portal, on the **Amplitude** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="99919-148">In the Azure portal, on the **Amplitude** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="99919-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="99919-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/amplitude-tutorial/tutorial_amplitude_samlbase.png)

3. <span data-ttu-id="99919-152">On the **Amplitude Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="99919-152">On the **Amplitude Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Amplitude Domain and URLs single sign-on information](./media/amplitude-tutorial/tutorial_amplitude_url.png)

    <span data-ttu-id="99919-154">a.</span><span class="sxs-lookup"><span data-stu-id="99919-154">a.</span></span> <span data-ttu-id="99919-155">In the **Identifier** textbox, type the URL: `https://amplitude.com/saml/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="99919-155">In the **Identifier** textbox, type the URL: `https://amplitude.com/saml/sso/metadata`</span></span>

    <span data-ttu-id="99919-156">b.</span><span class="sxs-lookup"><span data-stu-id="99919-156">b.</span></span> <span data-ttu-id="99919-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://analytics.amplitude.com/saml/sso/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="99919-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://analytics.amplitude.com/saml/sso/<uniqueid>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="99919-158">The Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="99919-158">The Reply URL value is not real.</span></span> <span data-ttu-id="99919-159">You will get the Reply URL value later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="99919-159">You will get the Reply URL value later in this tutorial.</span></span>

4. <span data-ttu-id="99919-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="99919-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Amplitude Domain and URLs single sign-on information](./media/amplitude-tutorial/tutorial_amplitude_url1.png)

    <span data-ttu-id="99919-162">In the **Sign-on URL** textbox, type the URL: `https://analytics.amplitude.com/sso`</span><span class="sxs-lookup"><span data-stu-id="99919-162">In the **Sign-on URL** textbox, type the URL: `https://analytics.amplitude.com/sso`</span></span>

5. <span data-ttu-id="99919-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="99919-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/amplitude-tutorial/tutorial_amplitude_certificate.png) 

6. <span data-ttu-id="99919-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="99919-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/amplitude-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="99919-167">Sign-on to your Amplitude company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="99919-167">Sign-on to your Amplitude company site as administrator.</span></span>

8. <span data-ttu-id="99919-168">Click on the **Plan Admin** from the left navigation bar.</span><span class="sxs-lookup"><span data-stu-id="99919-168">Click on the **Plan Admin** from the left navigation bar.</span></span>

    ![Configure Single Sign-On](./media/amplitude-tutorial/configure1.png)

9. <span data-ttu-id="99919-170">Select **Microsoft Azure Active Directory Metadata** from the **SSO Integration**.</span><span class="sxs-lookup"><span data-stu-id="99919-170">Select **Microsoft Azure Active Directory Metadata** from the **SSO Integration**.</span></span>

    ![Configure Single Sign-On](./media/amplitude-tutorial/configure2.png)

10. <span data-ttu-id="99919-172">On the **Set Up Single Sign-On** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99919-172">On the **Set Up Single Sign-On** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/amplitude-tutorial/configure3.png)

    <span data-ttu-id="99919-174">a.</span><span class="sxs-lookup"><span data-stu-id="99919-174">a.</span></span> <span data-ttu-id="99919-175">Open the downloaded **Metadata Xml** from Azure portal in notepad, paste the content into the **Microsoft Azure Active Directory Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="99919-175">Open the downloaded **Metadata Xml** from Azure portal in notepad, paste the content into the **Microsoft Azure Active Directory Metadata** textbox.</span></span>

    <span data-ttu-id="99919-176">b.</span><span class="sxs-lookup"><span data-stu-id="99919-176">b.</span></span> <span data-ttu-id="99919-177">Copy the **Reply URL (ACS)** value and paste it into the **Reply URL** textbox of Amplitude Domain and URLs section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="99919-177">Copy the **Reply URL (ACS)** value and paste it into the **Reply URL** textbox of Amplitude Domain and URLs section in the Azure portal.</span></span>

    <span data-ttu-id="99919-178">c.</span><span class="sxs-lookup"><span data-stu-id="99919-178">c.</span></span> <span data-ttu-id="99919-179">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="99919-179">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="99919-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="99919-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="99919-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="99919-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="99919-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="99919-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="99919-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99919-183">Create an Azure AD test user</span></span>

<span data-ttu-id="99919-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99919-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="99919-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99919-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99919-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="99919-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/amplitude-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="99919-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="99919-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/amplitude-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="99919-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="99919-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/amplitude-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="99919-193">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99919-193">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/amplitude-tutorial/create_aaduser_04.png)

    <span data-ttu-id="99919-195">a.</span><span class="sxs-lookup"><span data-stu-id="99919-195">a.</span></span> <span data-ttu-id="99919-196">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99919-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99919-197">b.</span><span class="sxs-lookup"><span data-stu-id="99919-197">b.</span></span> <span data-ttu-id="99919-198">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99919-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="99919-199">c.</span><span class="sxs-lookup"><span data-stu-id="99919-199">c.</span></span> <span data-ttu-id="99919-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="99919-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="99919-201">d.</span><span class="sxs-lookup"><span data-stu-id="99919-201">d.</span></span> <span data-ttu-id="99919-202">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="99919-202">Click **Create**.</span></span>
 
### <a name="create-an-amplitude-test-user"></a><span data-ttu-id="99919-203">Create an Amplitude test user</span><span class="sxs-lookup"><span data-stu-id="99919-203">Create an Amplitude test user</span></span>

<span data-ttu-id="99919-204">The objective of this section is to create a user called Britta Simon in Amplitude.</span><span class="sxs-lookup"><span data-stu-id="99919-204">The objective of this section is to create a user called Britta Simon in Amplitude.</span></span> <span data-ttu-id="99919-205">Amplitude supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="99919-205">Amplitude supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="99919-206">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="99919-206">There is no action item for you in this section.</span></span> <span data-ttu-id="99919-207">A new user is created during an attempt to access Amplitude if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="99919-207">A new user is created during an attempt to access Amplitude if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="99919-208">If you need to create a user manually, contact [Amplitude support team](https://amplitude.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="99919-208">If you need to create a user manually, contact [Amplitude support team](https://amplitude.zendesk.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="99919-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99919-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="99919-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Amplitude.</span><span class="sxs-lookup"><span data-stu-id="99919-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Amplitude.</span></span>

![Assign the user role][200] 

<span data-ttu-id="99919-212">**To assign Britta Simon to Amplitude, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99919-212">**To assign Britta Simon to Amplitude, perform the following steps:**</span></span>

1. <span data-ttu-id="99919-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="99919-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="99919-215">In the applications list, select **Amplitude**.</span><span class="sxs-lookup"><span data-stu-id="99919-215">In the applications list, select **Amplitude**.</span></span>

    ![The Amplitude link in the Applications list](./media/amplitude-tutorial/tutorial_amplitude_app.png)  

3. <span data-ttu-id="99919-217">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="99919-217">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="99919-219">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="99919-219">Click **Add** button.</span></span> <span data-ttu-id="99919-220">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="99919-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="99919-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="99919-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="99919-223">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="99919-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="99919-224">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="99919-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="99919-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="99919-225">Test single sign-on</span></span>

<span data-ttu-id="99919-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="99919-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="99919-227">When you click the Amplitude tile in the Access Panel, you should get automatically signed-on to your Amplitude application.</span><span class="sxs-lookup"><span data-stu-id="99919-227">When you click the Amplitude tile in the Access Panel, you should get automatically signed-on to your Amplitude application.</span></span>
<span data-ttu-id="99919-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="99919-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="99919-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="99919-229">Additional resources</span></span>

* [<span data-ttu-id="99919-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99919-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="99919-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99919-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/amplitude-tutorial/tutorial_general_01.png
[2]: ./media/amplitude-tutorial/tutorial_general_02.png
[3]: ./media/amplitude-tutorial/tutorial_general_03.png
[4]: ./media/amplitude-tutorial/tutorial_general_04.png

[100]: ./media/amplitude-tutorial/tutorial_general_100.png

[200]: ./media/amplitude-tutorial/tutorial_general_200.png
[201]: ./media/amplitude-tutorial/tutorial_general_201.png
[202]: ./media/amplitude-tutorial/tutorial_general_202.png
[203]: ./media/amplitude-tutorial/tutorial_general_203.png

