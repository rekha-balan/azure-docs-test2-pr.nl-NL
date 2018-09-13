---
title: 'Tutorial: Azure Active Directory integration with LINE WORKS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LINE WORKS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jeedes
ms.openlocfilehash: 907cec2784b4ad22555f6b29efb6d670ce7d48d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856003"
---
# <a name="tutorial-azure-active-directory-integration-with-line-works"></a><span data-ttu-id="14313-103">Tutorial: Azure Active Directory integration with LINE WORKS</span><span class="sxs-lookup"><span data-stu-id="14313-103">Tutorial: Azure Active Directory integration with LINE WORKS</span></span>

<span data-ttu-id="14313-104">In this tutorial, you learn how to integrate LINE WORKS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14313-104">In this tutorial, you learn how to integrate LINE WORKS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14313-105">Integrating LINE WORKS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="14313-105">Integrating LINE WORKS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="14313-106">You can control in Azure AD who has access to LINE WORKS.</span><span class="sxs-lookup"><span data-stu-id="14313-106">You can control in Azure AD who has access to LINE WORKS.</span></span>
- <span data-ttu-id="14313-107">You can enable your users to automatically get signed-on to LINE WORKS (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="14313-107">You can enable your users to automatically get signed-on to LINE WORKS (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="14313-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="14313-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="14313-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="14313-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14313-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="14313-110">Prerequisites</span></span>

<span data-ttu-id="14313-111">To configure Azure AD integration with LINE WORKS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="14313-111">To configure Azure AD integration with LINE WORKS, you need the following items:</span></span>

- <span data-ttu-id="14313-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="14313-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14313-113">A LINE WORKS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="14313-113">A LINE WORKS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14313-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="14313-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14313-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="14313-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14313-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="14313-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14313-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14313-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14313-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="14313-118">Scenario description</span></span>
<span data-ttu-id="14313-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="14313-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14313-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="14313-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14313-121">Adding LINE WORKS from the gallery</span><span class="sxs-lookup"><span data-stu-id="14313-121">Adding LINE WORKS from the gallery</span></span>
1. <span data-ttu-id="14313-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="14313-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-line-works-from-the-gallery"></a><span data-ttu-id="14313-123">Adding LINE WORKS from the gallery</span><span class="sxs-lookup"><span data-stu-id="14313-123">Adding LINE WORKS from the gallery</span></span>
<span data-ttu-id="14313-124">To configure the integration of LINE WORKS into Azure AD, you need to add LINE WORKS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="14313-124">To configure the integration of LINE WORKS into Azure AD, you need to add LINE WORKS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="14313-125">**To add LINE WORKS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14313-125">**To add LINE WORKS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="14313-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="14313-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="14313-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="14313-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="14313-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="14313-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="14313-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="14313-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="14313-133">In the search box, type **LINE WORKS**, select **LINE WORKS** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="14313-133">In the search box, type **LINE WORKS**, select **LINE WORKS** from result panel then click **Add** button to add the application.</span></span>

    ![LINE WORKS in the results list](./media/worksmobile-tutorial/tutorial_lineworks_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="14313-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="14313-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="14313-136">In this section, you configure and test Azure AD single sign-on with LINE WORKS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="14313-136">In this section, you configure and test Azure AD single sign-on with LINE WORKS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="14313-137">For single sign-on to work, Azure AD needs to know what the counterpart user in LINE WORKS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14313-137">For single sign-on to work, Azure AD needs to know what the counterpart user in LINE WORKS is to a user in Azure AD.</span></span> <span data-ttu-id="14313-138">In other words, a link relationship between an Azure AD user and the related user in LINE WORKS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="14313-138">In other words, a link relationship between an Azure AD user and the related user in LINE WORKS needs to be established.</span></span>

<span data-ttu-id="14313-139">In LINE WORKS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="14313-139">In LINE WORKS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="14313-140">To configure and test Azure AD single sign-on with LINE WORKS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="14313-140">To configure and test Azure AD single sign-on with LINE WORKS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="14313-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="14313-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="14313-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14313-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="14313-143">**[Create a LINE WORKS test user](#create-a-line-works-test-user)** - to have a counterpart of Britta Simon in LINE WORKS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="14313-143">**[Create a LINE WORKS test user](#create-a-line-works-test-user)** - to have a counterpart of Britta Simon in LINE WORKS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="14313-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="14313-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="14313-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="14313-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="14313-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="14313-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="14313-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LINE WORKS application.</span><span class="sxs-lookup"><span data-stu-id="14313-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LINE WORKS application.</span></span>

<span data-ttu-id="14313-148">**To configure Azure AD single sign-on with LINE WORKS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14313-148">**To configure Azure AD single sign-on with LINE WORKS, perform the following steps:**</span></span>

1. <span data-ttu-id="14313-149">In the Azure portal, on the **LINE WORKS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="14313-149">In the Azure portal, on the **LINE WORKS** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="14313-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="14313-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/worksmobile-tutorial/tutorial_lineworks_samlbase.png)

1. <span data-ttu-id="14313-153">On the **LINE WORKS Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="14313-153">On the **LINE WORKS Domain and URLs** section, perform the following steps:</span></span>

    ![LINE WORKS Domain and URLs single sign-on information](./media/worksmobile-tutorial/tutorial_lineworks_url.png)

    <span data-ttu-id="14313-155">a.</span><span class="sxs-lookup"><span data-stu-id="14313-155">a.</span></span> <span data-ttu-id="14313-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://auth.worksmobile.com/d/login/{domain}/?userId={ID@domain}`</span><span class="sxs-lookup"><span data-stu-id="14313-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://auth.worksmobile.com/d/login/{domain}/?userId={ID@domain}`</span></span>

    <span data-ttu-id="14313-157">b.</span><span class="sxs-lookup"><span data-stu-id="14313-157">b.</span></span> <span data-ttu-id="14313-158">In the **Identifier** textbox, type the value: `worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="14313-158">In the **Identifier** textbox, type the value: `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14313-159">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="14313-159">This value is not real.</span></span> <span data-ttu-id="14313-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="14313-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="14313-161">Contact [LINE WORKS Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="14313-161">Contact [LINE WORKS Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span>

1. <span data-ttu-id="14313-162">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="14313-162">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/worksmobile-tutorial/tutorial_lineworks_certificate.png) 

1. <span data-ttu-id="14313-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="14313-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/worksmobile-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="14313-166">On the **LINE WORKS Configuration** section, click **Configure LINE WORKS** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="14313-166">On the **LINE WORKS Configuration** section, click **Configure LINE WORKS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="14313-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="14313-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![LINE WORKS Configuration](./media/worksmobile-tutorial/tutorial_lineworks_configure.png) 

1. <span data-ttu-id="14313-169">To configure single sign-on on **LINE WORKS** side, you need to send the downloaded **Certificate file, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [LINE WORKS support team](mailto:dl_ssoinfo@worksmobile.com).</span><span class="sxs-lookup"><span data-stu-id="14313-169">To configure single sign-on on **LINE WORKS** side, you need to send the downloaded **Certificate file, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [LINE WORKS support team](mailto:dl_ssoinfo@worksmobile.com).</span></span> <span data-ttu-id="14313-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="14313-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="14313-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="14313-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="14313-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="14313-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="14313-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14313-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="14313-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="14313-174">Create an Azure AD test user</span></span>

<span data-ttu-id="14313-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14313-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="14313-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14313-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="14313-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="14313-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/worksmobile-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="14313-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="14313-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/worksmobile-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="14313-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="14313-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/worksmobile-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="14313-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="14313-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/worksmobile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="14313-186">a.</span><span class="sxs-lookup"><span data-stu-id="14313-186">a.</span></span> <span data-ttu-id="14313-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14313-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14313-188">b.</span><span class="sxs-lookup"><span data-stu-id="14313-188">b.</span></span> <span data-ttu-id="14313-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14313-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="14313-190">c.</span><span class="sxs-lookup"><span data-stu-id="14313-190">c.</span></span> <span data-ttu-id="14313-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="14313-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="14313-192">d.</span><span class="sxs-lookup"><span data-stu-id="14313-192">d.</span></span> <span data-ttu-id="14313-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="14313-193">Click **Create**.</span></span>
 
### <a name="create-a-line-works-test-user"></a><span data-ttu-id="14313-194">Create a LINE WORKS test user</span><span class="sxs-lookup"><span data-stu-id="14313-194">Create a LINE WORKS test user</span></span>

<span data-ttu-id="14313-195">In this section, you create a user called Britta Simon in LINE WORKS.</span><span class="sxs-lookup"><span data-stu-id="14313-195">In this section, you create a user called Britta Simon in LINE WORKS.</span></span> <span data-ttu-id="14313-196">Please work with [LINE WORKS support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the LINE WORKS platform.</span><span class="sxs-lookup"><span data-stu-id="14313-196">Please work with [LINE WORKS support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the LINE WORKS platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="14313-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="14313-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="14313-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LINE WORKS.</span><span class="sxs-lookup"><span data-stu-id="14313-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LINE WORKS.</span></span>

![Assign the user role][200] 

<span data-ttu-id="14313-200">**To assign Britta Simon to LINE WORKS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="14313-200">**To assign Britta Simon to LINE WORKS, perform the following steps:**</span></span>

1. <span data-ttu-id="14313-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="14313-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="14313-203">In the applications list, select **LINE WORKS**.</span><span class="sxs-lookup"><span data-stu-id="14313-203">In the applications list, select **LINE WORKS**.</span></span>

    ![The LINE WORKS link in the Applications list](./media/worksmobile-tutorial/tutorial_lineworks_app.png)  

1. <span data-ttu-id="14313-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="14313-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="14313-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="14313-207">Click **Add** button.</span></span> <span data-ttu-id="14313-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="14313-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="14313-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="14313-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="14313-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="14313-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="14313-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="14313-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="14313-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="14313-213">Test single sign-on</span></span>

<span data-ttu-id="14313-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="14313-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="14313-215">When you click the LINE WORKS tile in the Access Panel, you should get automatically signed-on to your LINE WORKS application.</span><span class="sxs-lookup"><span data-stu-id="14313-215">When you click the LINE WORKS tile in the Access Panel, you should get automatically signed-on to your LINE WORKS application.</span></span>
<span data-ttu-id="14313-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="14313-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="14313-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="14313-217">Additional resources</span></span>

* [<span data-ttu-id="14313-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14313-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="14313-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14313-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/lineworks-tutorial/tutorial_general_01.png
[2]: ./media/lineworks-tutorial/tutorial_general_02.png
[3]: ./media/lineworks-tutorial/tutorial_general_03.png
[4]: ./media/lineworks-tutorial/tutorial_general_04.png

[100]: ./media/lineworks-tutorial/tutorial_general_100.png

[200]: ./media/lineworks-tutorial/tutorial_general_200.png
[201]: ./media/lineworks-tutorial/tutorial_general_201.png
[202]: ./media/lineworks-tutorial/tutorial_general_202.png
[203]: ./media/lineworks-tutorial/tutorial_general_203.png
