---
title: 'Tutorial: Azure Active Directory integration with Workteam | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workteam.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 41df17a1-ba69-414f-8ec3-11079b030df6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2018
ms.author: jeedes
ms.openlocfilehash: 8d6ca6395e4f5e1aca361c56e21afc4e6bd1fc0c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866300"
---
# <a name="tutorial-azure-active-directory-integration-with-workteam"></a><span data-ttu-id="85aa3-103">Tutorial: Azure Active Directory integration with Workteam</span><span class="sxs-lookup"><span data-stu-id="85aa3-103">Tutorial: Azure Active Directory integration with Workteam</span></span>

<span data-ttu-id="85aa3-104">In this tutorial, you learn how to integrate Workteam with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85aa3-104">In this tutorial, you learn how to integrate Workteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85aa3-105">Integrating Workteam with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="85aa3-105">Integrating Workteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="85aa3-106">You can control in Azure AD who has access to Workteam.</span><span class="sxs-lookup"><span data-stu-id="85aa3-106">You can control in Azure AD who has access to Workteam.</span></span>
- <span data-ttu-id="85aa3-107">You can enable your users to automatically get signed-on to Workteam (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="85aa3-107">You can enable your users to automatically get signed-on to Workteam (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="85aa3-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85aa3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="85aa3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="85aa3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85aa3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="85aa3-110">Prerequisites</span></span>

<span data-ttu-id="85aa3-111">To configure Azure AD integration with Workteam, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="85aa3-111">To configure Azure AD integration with Workteam, you need the following items:</span></span>

- <span data-ttu-id="85aa3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="85aa3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85aa3-113">A Workteam single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="85aa3-113">A Workteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85aa3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="85aa3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85aa3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="85aa3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85aa3-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="85aa3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85aa3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85aa3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85aa3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="85aa3-118">Scenario description</span></span>
<span data-ttu-id="85aa3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="85aa3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85aa3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="85aa3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85aa3-121">Adding Workteam from the gallery</span><span class="sxs-lookup"><span data-stu-id="85aa3-121">Adding Workteam from the gallery</span></span>
2. <span data-ttu-id="85aa3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="85aa3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workteam-from-the-gallery"></a><span data-ttu-id="85aa3-123">Adding Workteam from the gallery</span><span class="sxs-lookup"><span data-stu-id="85aa3-123">Adding Workteam from the gallery</span></span>
<span data-ttu-id="85aa3-124">To configure the integration of Workteam into Azure AD, you need to add Workteam from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="85aa3-124">To configure the integration of Workteam into Azure AD, you need to add Workteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="85aa3-125">**To add Workteam from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85aa3-125">**To add Workteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="85aa3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="85aa3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="85aa3-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="85aa3-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="85aa3-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="85aa3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="85aa3-133">In the search box, type **Workteam**, select **Workteam** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="85aa3-133">In the search box, type **Workteam**, select **Workteam** from result panel then click **Add** button to add the application.</span></span>

    ![Workteam in the results list](./media/workteam-tutorial/tutorial_workteam_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="85aa3-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="85aa3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="85aa3-136">In this section, you configure and test Azure AD single sign-on with Workteam based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85aa3-136">In this section, you configure and test Azure AD single sign-on with Workteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85aa3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workteam is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85aa3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workteam is to a user in Azure AD.</span></span> <span data-ttu-id="85aa3-138">In other words, a link relationship between an Azure AD user and the related user in Workteam needs to be established.</span><span class="sxs-lookup"><span data-stu-id="85aa3-138">In other words, a link relationship between an Azure AD user and the related user in Workteam needs to be established.</span></span>

<span data-ttu-id="85aa3-139">To configure and test Azure AD single sign-on with Workteam, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="85aa3-139">To configure and test Azure AD single sign-on with Workteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="85aa3-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="85aa3-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="85aa3-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85aa3-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85aa3-142">**[Create a Workteam test user](#create-a-workteam-test-user)** - to have a counterpart of Britta Simon in Workteam that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="85aa3-142">**[Create a Workteam test user](#create-a-workteam-test-user)** - to have a counterpart of Britta Simon in Workteam that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="85aa3-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="85aa3-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85aa3-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="85aa3-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="85aa3-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="85aa3-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="85aa3-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workteam application.</span><span class="sxs-lookup"><span data-stu-id="85aa3-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workteam application.</span></span>

<span data-ttu-id="85aa3-147">**To configure Azure AD single sign-on with Workteam, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85aa3-147">**To configure Azure AD single sign-on with Workteam, perform the following steps:**</span></span>

1. <span data-ttu-id="85aa3-148">In the Azure portal, on the **Workteam** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-148">In the Azure portal, on the **Workteam** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="85aa3-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="85aa3-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/workteam-tutorial/tutorial_workteam_samlbase.png)

3. <span data-ttu-id="85aa3-152">On the **Workteam Domain and URLs** section, the user does not have to perform any steps as the application is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa3-152">On the **Workteam Domain and URLs** section, the user does not have to perform any steps as the application is already pre-integrated with Azure.</span></span>

    ![Workteam Domain and URLs single sign-on information](./media/workteam-tutorial/tutorial_workteam_url.png)

4. <span data-ttu-id="85aa3-154">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="85aa3-154">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Workteam Domain and URLs single sign-on information](./media/workteam-tutorial/tutorial_workteam_url1.png)

    <span data-ttu-id="85aa3-156">In the **Sign-on URL** textbox, type a URL: `https://app.workte.am`</span><span class="sxs-lookup"><span data-stu-id="85aa3-156">In the **Sign-on URL** textbox, type a URL: `https://app.workte.am`</span></span>
     
5. <span data-ttu-id="85aa3-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="85aa3-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/workteam-tutorial/tutorial_workteam_certificate.png) 

6. <span data-ttu-id="85aa3-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="85aa3-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/workteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="85aa3-161">On the **Workteam Configuration** section, click **Configure Workteam** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="85aa3-161">On the **Workteam Configuration** section, click **Configure Workteam** to open **Configure sign-on** window.</span></span> <span data-ttu-id="85aa3-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="85aa3-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Workteam Configuration](./media/workteam-tutorial/tutorial_workteam_configure.png) 

8. <span data-ttu-id="85aa3-164">In a different web browser window, log in to Workteam as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="85aa3-164">In a different web browser window, log in to Workteam as a Security Administrator.</span></span>

9. <span data-ttu-id="85aa3-165">In the top right corner click on **profile logo** and then click on **Organization settings**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-165">In the top right corner click on **profile logo** and then click on **Organization settings**.</span></span> 

    ![Workteam settings](./media/workteam-tutorial/tutorial_workteam_settings.png)

10. <span data-ttu-id="85aa3-167">Under **AUTHENTICATION** section, click on **Settings logo**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-167">Under **AUTHENTICATION** section, click on **Settings logo**.</span></span>

     ![Workteam azure](./media/workteam-tutorial/tutorial_workteam_azure.png)

11. <span data-ttu-id="85aa3-169">On the **SAML Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="85aa3-169">On the **SAML Settings** page, perform the following steps:</span></span>

     ![Workteam saml](./media/workteam-tutorial/tutorial_workteam_saml.png)

    <span data-ttu-id="85aa3-171">a.</span><span class="sxs-lookup"><span data-stu-id="85aa3-171">a.</span></span> <span data-ttu-id="85aa3-172">Select **SAML IdP** as **AD Azure**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-172">Select **SAML IdP** as **AD Azure**.</span></span>

    <span data-ttu-id="85aa3-173">b.</span><span class="sxs-lookup"><span data-stu-id="85aa3-173">b.</span></span> <span data-ttu-id="85aa3-174">In the **SAML Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85aa3-174">In the **SAML Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="85aa3-175">c.</span><span class="sxs-lookup"><span data-stu-id="85aa3-175">c.</span></span> <span data-ttu-id="85aa3-176">In the **SAML Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85aa3-176">In the **SAML Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="85aa3-177">d.</span><span class="sxs-lookup"><span data-stu-id="85aa3-177">d.</span></span> <span data-ttu-id="85aa3-178">In Notepad, open the **base-64 encoded certificate** that you downloaded from the Azure portal, copy its content, and then paste it into the **SAML Signing Certificate (Base64)** box.</span><span class="sxs-lookup"><span data-stu-id="85aa3-178">In Notepad, open the **base-64 encoded certificate** that you downloaded from the Azure portal, copy its content, and then paste it into the **SAML Signing Certificate (Base64)** box.</span></span>

    <span data-ttu-id="85aa3-179">e.</span><span class="sxs-lookup"><span data-stu-id="85aa3-179">e.</span></span> <span data-ttu-id="85aa3-180">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-180">Click **OK**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="85aa3-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="85aa3-181">Create an Azure AD test user</span></span>

<span data-ttu-id="85aa3-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85aa3-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="85aa3-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85aa3-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="85aa3-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="85aa3-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/workteam-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="85aa3-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/workteam-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="85aa3-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="85aa3-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/workteam-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="85aa3-191">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="85aa3-191">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/workteam-tutorial/create_aaduser_04.png)

    <span data-ttu-id="85aa3-193">a.</span><span class="sxs-lookup"><span data-stu-id="85aa3-193">a.</span></span> <span data-ttu-id="85aa3-194">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-194">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85aa3-195">b.</span><span class="sxs-lookup"><span data-stu-id="85aa3-195">b.</span></span> <span data-ttu-id="85aa3-196">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85aa3-196">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="85aa3-197">c.</span><span class="sxs-lookup"><span data-stu-id="85aa3-197">c.</span></span> <span data-ttu-id="85aa3-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="85aa3-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="85aa3-199">d.</span><span class="sxs-lookup"><span data-stu-id="85aa3-199">d.</span></span> <span data-ttu-id="85aa3-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-200">Click **Create**.</span></span>
 
### <a name="create-a-workteam-test-user"></a><span data-ttu-id="85aa3-201">Create a Workteam test user</span><span class="sxs-lookup"><span data-stu-id="85aa3-201">Create a Workteam test user</span></span>

<span data-ttu-id="85aa3-202">To enable Azure AD users to login to Workteam, they must be provisioned into Workteam.</span><span class="sxs-lookup"><span data-stu-id="85aa3-202">To enable Azure AD users to login to Workteam, they must be provisioned into Workteam.</span></span> <span data-ttu-id="85aa3-203">In Workteam, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="85aa3-203">In Workteam, provisioning is a manual task.</span></span>

<span data-ttu-id="85aa3-204">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85aa3-204">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="85aa3-205">Login to Workteam as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="85aa3-205">Login to Workteam as a Security Administrator.</span></span>

2. <span data-ttu-id="85aa3-206">On the top middle of the **Organization settings** page, click **USERS** and then click **NEW USER**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-206">On the top middle of the **Organization settings** page, click **USERS** and then click **NEW USER**.</span></span>

    ![Workteam user](./media/workteam-tutorial/tutorial_workteam_user.png)

3. <span data-ttu-id="85aa3-208">On the **New employee** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="85aa3-208">On the **New employee** page, perform the following steps:</span></span>

    ![Workteam newuser](./media/workteam-tutorial/tutorial_workteam_newuser.png)

    <span data-ttu-id="85aa3-210">a.</span><span class="sxs-lookup"><span data-stu-id="85aa3-210">a.</span></span> <span data-ttu-id="85aa3-211">In the **Name** text box, enter the first name of user like **Brittasimon**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-211">In the **Name** text box, enter the first name of user like **Brittasimon**.</span></span>

    <span data-ttu-id="85aa3-212">b.</span><span class="sxs-lookup"><span data-stu-id="85aa3-212">b.</span></span> <span data-ttu-id="85aa3-213">In **Email** text box, enter the email of user like **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-213">In **Email** text box, enter the email of user like **Brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="85aa3-214">c.</span><span class="sxs-lookup"><span data-stu-id="85aa3-214">c.</span></span> <span data-ttu-id="85aa3-215">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-215">Click **OK**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="85aa3-216">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="85aa3-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="85aa3-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workteam.</span><span class="sxs-lookup"><span data-stu-id="85aa3-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workteam.</span></span>

![Assign the user role][200] 

<span data-ttu-id="85aa3-219">**To assign Britta Simon to Workteam, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85aa3-219">**To assign Britta Simon to Workteam, perform the following steps:**</span></span>

1. <span data-ttu-id="85aa3-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="85aa3-222">In the applications list, select **Workteam**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-222">In the applications list, select **Workteam**.</span></span>

    ![The Workteam link in the Applications list](./media/workteam-tutorial/tutorial_workteam_app.png)  

3. <span data-ttu-id="85aa3-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="85aa3-224">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="85aa3-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="85aa3-226">Click **Add** button.</span></span> <span data-ttu-id="85aa3-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="85aa3-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="85aa3-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="85aa3-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="85aa3-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="85aa3-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85aa3-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="85aa3-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="85aa3-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="85aa3-232">Test single sign-on</span></span>

<span data-ttu-id="85aa3-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="85aa3-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="85aa3-234">When you click the Workteam tile in the Access Panel, you should get automatically signed-on to your Workteam application.</span><span class="sxs-lookup"><span data-stu-id="85aa3-234">When you click the Workteam tile in the Access Panel, you should get automatically signed-on to your Workteam application.</span></span>
<span data-ttu-id="85aa3-235">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85aa3-235">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="85aa3-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="85aa3-236">Additional resources</span></span>

* [<span data-ttu-id="85aa3-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85aa3-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="85aa3-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85aa3-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/workteam-tutorial/tutorial_general_01.png
[2]: ./media/workteam-tutorial/tutorial_general_02.png
[3]: ./media/workteam-tutorial/tutorial_general_03.png
[4]: ./media/workteam-tutorial/tutorial_general_04.png

[100]: ./media/workteam-tutorial/tutorial_general_100.png

[200]: ./media/workteam-tutorial/tutorial_general_200.png
[201]: ./media/workteam-tutorial/tutorial_general_201.png
[202]: ./media/workteam-tutorial/tutorial_general_202.png
[203]: ./media/workteam-tutorial/tutorial_general_203.png

