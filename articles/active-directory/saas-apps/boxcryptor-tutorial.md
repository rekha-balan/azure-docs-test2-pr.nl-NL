---
title: 'Tutorial: Azure Active Directory integration with Boxcryptor | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Boxcryptor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c46aa523-b58c-4a95-a800-db2e5e01c542
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2018
ms.author: jeedes
ms.openlocfilehash: ec9ebb5673a5bca9c5eda2b08baa1a825edcefe4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856914"
---
# <a name="tutorial-azure-active-directory-integration-with-boxcryptor"></a><span data-ttu-id="14748-103">Tutorial: Azure Active Directory integration with Boxcryptor</span><span class="sxs-lookup"><span data-stu-id="14748-103">Tutorial: Azure Active Directory integration with Boxcryptor</span></span>

<span data-ttu-id="14748-104">In this tutorial, you learn how to integrate Boxcryptor with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14748-104">In this tutorial, you learn how to integrate Boxcryptor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14748-105">Integrating Boxcryptor with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="14748-105">Integrating Boxcryptor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="14748-106">You can control in Azure AD who has access to Boxcryptor.</span><span class="sxs-lookup"><span data-stu-id="14748-106">You can control in Azure AD who has access to Boxcryptor.</span></span>
- <span data-ttu-id="14748-107">You can enable your users to automatically get signed-on to Boxcryptor (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="14748-107">You can enable your users to automatically get signed-on to Boxcryptor (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="14748-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="14748-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="14748-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="14748-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14748-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="14748-110">Prerequisites</span></span>

<span data-ttu-id="14748-111">To configure Azure AD integration with Boxcryptor, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="14748-111">To configure Azure AD integration with Boxcryptor, you need the following items:</span></span>

- <span data-ttu-id="14748-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="14748-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14748-113">A Boxcryptor single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="14748-113">A Boxcryptor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14748-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="14748-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14748-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="14748-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14748-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="14748-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14748-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14748-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14748-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="14748-118">Scenario description</span></span>
<span data-ttu-id="14748-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="14748-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14748-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="14748-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14748-121">Adding Boxcryptor from the gallery</span><span class="sxs-lookup"><span data-stu-id="14748-121">Adding Boxcryptor from the gallery</span></span>
1. <span data-ttu-id="14748-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="14748-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boxcryptor-from-the-gallery"></a><span data-ttu-id="14748-123">Adding Boxcryptor from the gallery</span><span class="sxs-lookup"><span data-stu-id="14748-123">Adding Boxcryptor from the gallery</span></span>
<span data-ttu-id="14748-124">To configure the integration of Boxcryptor into Azure AD, you need to add Boxcryptor from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="14748-124">To configure the integration of Boxcryptor into Azure AD, you need to add Boxcryptor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="14748-125">**To add Boxcryptor from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14748-125">**To add Boxcryptor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="14748-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="14748-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="14748-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="14748-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="14748-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="14748-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="14748-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="14748-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="14748-133">In the search box, type **Boxcryptor**, select **Boxcryptor** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="14748-133">In the search box, type **Boxcryptor**, select **Boxcryptor** from result panel then click **Add** button to add the application.</span></span>

    ![Boxcryptor in the results list](./media/boxcryptor-tutorial/tutorial_boxcryptor_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="14748-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="14748-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="14748-136">In this section, you configure and test Azure AD single sign-on with Boxcryptor based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="14748-136">In this section, you configure and test Azure AD single sign-on with Boxcryptor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="14748-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Boxcryptor is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14748-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Boxcryptor is to a user in Azure AD.</span></span> <span data-ttu-id="14748-138">In other words, a link relationship between an Azure AD user and the related user in Boxcryptor needs to be established.</span><span class="sxs-lookup"><span data-stu-id="14748-138">In other words, a link relationship between an Azure AD user and the related user in Boxcryptor needs to be established.</span></span>

<span data-ttu-id="14748-139">To configure and test Azure AD single sign-on with Boxcryptor, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="14748-139">To configure and test Azure AD single sign-on with Boxcryptor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="14748-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="14748-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="14748-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14748-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="14748-142">**[Create a Boxcryptor test user](#create-a-boxcryptor-test-user)** - to have a counterpart of Britta Simon in Boxcryptor that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="14748-142">**[Create a Boxcryptor test user](#create-a-boxcryptor-test-user)** - to have a counterpart of Britta Simon in Boxcryptor that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="14748-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="14748-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="14748-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="14748-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="14748-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="14748-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="14748-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boxcryptor application.</span><span class="sxs-lookup"><span data-stu-id="14748-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boxcryptor application.</span></span>

<span data-ttu-id="14748-147">**To configure Azure AD single sign-on with Boxcryptor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14748-147">**To configure Azure AD single sign-on with Boxcryptor, perform the following steps:**</span></span>

1. <span data-ttu-id="14748-148">In the Azure portal, on the **Boxcryptor** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="14748-148">In the Azure portal, on the **Boxcryptor** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="14748-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="14748-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/boxcryptor-tutorial/tutorial_boxcryptor_samlbase.png)

1. <span data-ttu-id="14748-152">On the **Boxcryptor Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="14748-152">On the **Boxcryptor Domain and URLs** section, perform the following steps:</span></span>

    ![Boxcryptor Domain and URLs single sign-on information](./media/boxcryptor-tutorial/tutorial_boxcryptor_url.png)

    <span data-ttu-id="14748-154">a.</span><span class="sxs-lookup"><span data-stu-id="14748-154">a.</span></span> <span data-ttu-id="14748-155">In the **Sign-on URL** textbox, type a URL: `https://www.boxcryptor.com/app`</span><span class="sxs-lookup"><span data-stu-id="14748-155">In the **Sign-on URL** textbox, type a URL: `https://www.boxcryptor.com/app`</span></span>

    <span data-ttu-id="14748-156">b.</span><span class="sxs-lookup"><span data-stu-id="14748-156">b.</span></span> <span data-ttu-id="14748-157">In the **Identifier** textbox, type a value: `boxcryptor`</span><span class="sxs-lookup"><span data-stu-id="14748-157">In the **Identifier** textbox, type a value: `boxcryptor`</span></span>

1. <span data-ttu-id="14748-158">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="14748-158">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/boxcryptor-tutorial/tutorial_boxcryptor_certificate.png) 

1. <span data-ttu-id="14748-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="14748-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/boxcryptor-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="14748-162">On the **Boxcryptor Configuration** section, click **Configure Boxcryptor** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="14748-162">On the **Boxcryptor Configuration** section, click **Configure Boxcryptor** to open **Configure sign-on** window.</span></span> <span data-ttu-id="14748-163">Copy the **SAML Single Sign-On Service URL** and **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="14748-163">Copy the **SAML Single Sign-On Service URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Andromeda SCM Configuration](./media/boxcryptor-tutorial/tutorial_boxcryptor_configure.png)

1. <span data-ttu-id="14748-165">To configure single sign-on on **Boxcryptor** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Boxcryptor support team](mailto:support@boxcryptor.com).</span><span class="sxs-lookup"><span data-stu-id="14748-165">To configure single sign-on on **Boxcryptor** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Boxcryptor support team](mailto:support@boxcryptor.com).</span></span> <span data-ttu-id="14748-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="14748-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="14748-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="14748-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="14748-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="14748-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="14748-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14748-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="14748-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="14748-170">Create an Azure AD test user</span></span>

<span data-ttu-id="14748-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14748-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="14748-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14748-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="14748-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="14748-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/boxcryptor-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="14748-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="14748-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/boxcryptor-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="14748-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="14748-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/boxcryptor-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="14748-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="14748-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/boxcryptor-tutorial/create_aaduser_04.png)

    <span data-ttu-id="14748-182">a.</span><span class="sxs-lookup"><span data-stu-id="14748-182">a.</span></span> <span data-ttu-id="14748-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14748-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14748-184">b.</span><span class="sxs-lookup"><span data-stu-id="14748-184">b.</span></span> <span data-ttu-id="14748-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14748-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="14748-186">c.</span><span class="sxs-lookup"><span data-stu-id="14748-186">c.</span></span> <span data-ttu-id="14748-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="14748-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="14748-188">d.</span><span class="sxs-lookup"><span data-stu-id="14748-188">d.</span></span> <span data-ttu-id="14748-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="14748-189">Click **Create**.</span></span>
 
### <a name="create-a-boxcryptor-test-user"></a><span data-ttu-id="14748-190">Create a Boxcryptor test user</span><span class="sxs-lookup"><span data-stu-id="14748-190">Create a Boxcryptor test user</span></span>

<span data-ttu-id="14748-191">In this section, you create a user called Britta Simon in Boxcryptor.</span><span class="sxs-lookup"><span data-stu-id="14748-191">In this section, you create a user called Britta Simon in Boxcryptor.</span></span> <span data-ttu-id="14748-192">Work with [Boxcryptor support team](mailto:support@boxcryptor.com) to add the users or the domain which is needed to be whitelisted in the Boxcryptor platform.</span><span class="sxs-lookup"><span data-stu-id="14748-192">Work with [Boxcryptor support team](mailto:support@boxcryptor.com) to add the users or the domain which is needed to be whitelisted in the Boxcryptor platform.</span></span> <span data-ttu-id="14748-193">If the domain is added by the team, users will get automatically provisioned to the Boxcryptor platform.</span><span class="sxs-lookup"><span data-stu-id="14748-193">If the domain is added by the team, users will get automatically provisioned to the Boxcryptor platform.</span></span> <span data-ttu-id="14748-194">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="14748-194">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="14748-195">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="14748-195">Assign the Azure AD test user</span></span>

<span data-ttu-id="14748-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boxcryptor.</span><span class="sxs-lookup"><span data-stu-id="14748-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boxcryptor.</span></span>

![Assign the user role][200] 

<span data-ttu-id="14748-198">**To assign Britta Simon to Boxcryptor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14748-198">**To assign Britta Simon to Boxcryptor, perform the following steps:**</span></span>

1. <span data-ttu-id="14748-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="14748-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="14748-201">In the applications list, select **Boxcryptor**.</span><span class="sxs-lookup"><span data-stu-id="14748-201">In the applications list, select **Boxcryptor**.</span></span>

    ![The Boxcryptor link in the Applications list](./media/boxcryptor-tutorial/tutorial_boxcryptor_app.png)  

1. <span data-ttu-id="14748-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="14748-203">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="14748-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="14748-205">Click **Add** button.</span></span> <span data-ttu-id="14748-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="14748-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="14748-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="14748-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="14748-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="14748-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="14748-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="14748-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="14748-211">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="14748-211">Test single sign-on</span></span>

<span data-ttu-id="14748-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="14748-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="14748-213">When you click the Boxcryptor tile in the Access Panel, you should get automatically signed-on to your Boxcryptor application.</span><span class="sxs-lookup"><span data-stu-id="14748-213">When you click the Boxcryptor tile in the Access Panel, you should get automatically signed-on to your Boxcryptor application.</span></span>
<span data-ttu-id="14748-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="14748-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="14748-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="14748-215">Additional resources</span></span>

* [<span data-ttu-id="14748-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14748-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="14748-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14748-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/boxcryptor-tutorial/tutorial_general_01.png
[2]: ./media/boxcryptor-tutorial/tutorial_general_02.png
[3]: ./media/boxcryptor-tutorial/tutorial_general_03.png
[4]: ./media/boxcryptor-tutorial/tutorial_general_04.png

[100]: ./media/boxcryptor-tutorial/tutorial_general_100.png

[200]: ./media/boxcryptor-tutorial/tutorial_general_200.png
[201]: ./media/boxcryptor-tutorial/tutorial_general_201.png
[202]: ./media/boxcryptor-tutorial/tutorial_general_202.png
[203]: ./media/boxcryptor-tutorial/tutorial_general_203.png

