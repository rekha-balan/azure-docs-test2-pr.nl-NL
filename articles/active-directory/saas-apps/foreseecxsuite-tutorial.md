---
title: 'Tutorial: Azure Active Directory integration with ForeSee CX Suite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ForeSee CX Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5f4b7830-6186-4d17-b77b-504d4192bfde
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2018
ms.author: jeedes
ms.openlocfilehash: b288bcbe14050c0f764f348d5e20186570e32866
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866533"
---
# <a name="tutorial-azure-active-directory-integration-with-foresee-cx-suite"></a><span data-ttu-id="112ee-103">Tutorial: Azure Active Directory integration with ForeSee CX Suite</span><span class="sxs-lookup"><span data-stu-id="112ee-103">Tutorial: Azure Active Directory integration with ForeSee CX Suite</span></span>

<span data-ttu-id="112ee-104">In this tutorial, you learn how to integrate ForeSee CX Suite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="112ee-104">In this tutorial, you learn how to integrate ForeSee CX Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="112ee-105">Integrating ForeSee CX Suite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="112ee-105">Integrating ForeSee CX Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="112ee-106">You can control in Azure AD who has access to ForeSee CX Suite.</span><span class="sxs-lookup"><span data-stu-id="112ee-106">You can control in Azure AD who has access to ForeSee CX Suite.</span></span>
- <span data-ttu-id="112ee-107">You can enable your users to automatically get signed-on to ForeSee CX Suite (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="112ee-107">You can enable your users to automatically get signed-on to ForeSee CX Suite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="112ee-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="112ee-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="112ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="112ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="112ee-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="112ee-110">Prerequisites</span></span>

<span data-ttu-id="112ee-111">To configure Azure AD integration with ForeSee CX Suite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="112ee-111">To configure Azure AD integration with ForeSee CX Suite, you need the following items:</span></span>

- <span data-ttu-id="112ee-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="112ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="112ee-113">A ForeSee CX Suite single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="112ee-113">A ForeSee CX Suite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="112ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="112ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="112ee-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="112ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="112ee-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="112ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="112ee-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="112ee-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="112ee-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="112ee-118">Scenario description</span></span>
<span data-ttu-id="112ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="112ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="112ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="112ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="112ee-121">Adding ForeSee CX Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="112ee-121">Adding ForeSee CX Suite from the gallery</span></span>
1. <span data-ttu-id="112ee-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="112ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-foresee-cx-suite-from-the-gallery"></a><span data-ttu-id="112ee-123">Adding ForeSee CX Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="112ee-123">Adding ForeSee CX Suite from the gallery</span></span>
<span data-ttu-id="112ee-124">To configure the integration of ForeSee CX Suite into Azure AD, you need to add ForeSee CX Suite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="112ee-124">To configure the integration of ForeSee CX Suite into Azure AD, you need to add ForeSee CX Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="112ee-125">**To add ForeSee CX Suite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="112ee-125">**To add ForeSee CX Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="112ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="112ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="112ee-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="112ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="112ee-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="112ee-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="112ee-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="112ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="112ee-133">In the search box, type **ForeSee CX Suite**, select **ForeSee CX Suite** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="112ee-133">In the search box, type **ForeSee CX Suite**, select **ForeSee CX Suite** from result panel then click **Add** button to add the application.</span></span>

    ![ForeSee CX Suite in the results list](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="112ee-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="112ee-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="112ee-136">In this section, you configure and test Azure AD single sign-on with ForeSee CX Suite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="112ee-136">In this section, you configure and test Azure AD single sign-on with ForeSee CX Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="112ee-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ForeSee CX Suite is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="112ee-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ForeSee CX Suite is to a user in Azure AD.</span></span> <span data-ttu-id="112ee-138">In other words, a link relationship between an Azure AD user and the related user in ForeSee CX Suite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="112ee-138">In other words, a link relationship between an Azure AD user and the related user in ForeSee CX Suite needs to be established.</span></span>

<span data-ttu-id="112ee-139">To configure and test Azure AD single sign-on with ForeSee CX Suite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="112ee-139">To configure and test Azure AD single sign-on with ForeSee CX Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="112ee-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="112ee-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="112ee-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="112ee-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="112ee-142">**[Create a ForeSee CX Suite test user](#create-a-foresee-cx-suite-test-user)** - to have a counterpart of Britta Simon in ForeSee CX Suite that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="112ee-142">**[Create a ForeSee CX Suite test user](#create-a-foresee-cx-suite-test-user)** - to have a counterpart of Britta Simon in ForeSee CX Suite that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="112ee-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="112ee-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="112ee-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="112ee-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="112ee-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="112ee-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="112ee-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ForeSee CX Suite application.</span><span class="sxs-lookup"><span data-stu-id="112ee-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ForeSee CX Suite application.</span></span>

<span data-ttu-id="112ee-147">**To configure Azure AD single sign-on with ForeSee CX Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="112ee-147">**To configure Azure AD single sign-on with ForeSee CX Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="112ee-148">In the Azure portal, on the **ForeSee CX Suite** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="112ee-148">In the Azure portal, on the **ForeSee CX Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="112ee-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="112ee-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_samlbase.png)

1. <span data-ttu-id="112ee-152">On the **ForeSee CX Suite Domain and URLs** section, if you have **Service Provider metadata file**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="112ee-152">On the **ForeSee CX Suite Domain and URLs** section, if you have **Service Provider metadata file**, perform the following steps:</span></span>

    ![ForeSee CX Suite Domain and URLs single sign-on information](./media/foreseecxsuite-tutorial/upload.png)

    <span data-ttu-id="112ee-154">a.</span><span class="sxs-lookup"><span data-stu-id="112ee-154">a.</span></span> <span data-ttu-id="112ee-155">Click **Upload metadata file**.</span><span class="sxs-lookup"><span data-stu-id="112ee-155">Click **Upload metadata file**.</span></span>

    ![ForeSee CX Suite Domain and URLs single sign-on information](./media/foreseecxsuite-tutorial/tutorial_foreseen_uploadconfig.png)

    <span data-ttu-id="112ee-157">b.</span><span class="sxs-lookup"><span data-stu-id="112ee-157">b.</span></span> <span data-ttu-id="112ee-158">Click on **folder logo** to select the metadata file and click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="112ee-158">Click on **folder logo** to select the metadata file and click **Upload**.</span></span>

    <span data-ttu-id="112ee-159">c.</span><span class="sxs-lookup"><span data-stu-id="112ee-159">c.</span></span> <span data-ttu-id="112ee-160">After successfull completion of uploading **Service Provider metadata file** the **Identifier** value get auto populated in **ForeSee CX Suite Domain and URLs** section textbox as shown below:</span><span class="sxs-lookup"><span data-stu-id="112ee-160">After successfull completion of uploading **Service Provider metadata file** the **Identifier** value get auto populated in **ForeSee CX Suite Domain and URLs** section textbox as shown below:</span></span>

    ![ForeSee CX Suite Domain and URLs single sign-on information](./media/foreseecxsuite-tutorial/urlupload.png)

1. <span data-ttu-id="112ee-162">If you dont have **Service Provider metadata file**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="112ee-162">If you dont have **Service Provider metadata file**, perform the following steps:</span></span>

    ![ForeSee CX Suite Domain and URLs single sign-on information](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_url.png)

    <span data-ttu-id="112ee-164">a.</span><span class="sxs-lookup"><span data-stu-id="112ee-164">a.</span></span> <span data-ttu-id="112ee-165">In the **Sign-on URL** textbox, type the URL: `https://cxsuite.foresee.com/`</span><span class="sxs-lookup"><span data-stu-id="112ee-165">In the **Sign-on URL** textbox, type the URL: `https://cxsuite.foresee.com/`</span></span>

    <span data-ttu-id="112ee-166">b.</span><span class="sxs-lookup"><span data-stu-id="112ee-166">b.</span></span> <span data-ttu-id="112ee-167">In the **Identifier** textbox, type a URL using the following pattern: `https://www.okta.com/saml2/service-provider/<UniqueID>`</span><span class="sxs-lookup"><span data-stu-id="112ee-167">In the **Identifier** textbox, type a URL using the following pattern: `https://www.okta.com/saml2/service-provider/<UniqueID>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="112ee-168">The Identifier value is not real.</span><span class="sxs-lookup"><span data-stu-id="112ee-168">The Identifier value is not real.</span></span> <span data-ttu-id="112ee-169">Update this value with the actual Identifier.</span><span class="sxs-lookup"><span data-stu-id="112ee-169">Update this value with the actual Identifier.</span></span> <span data-ttu-id="112ee-170">Contact [ForeSee CX Suite Client support team](mailto:support@foresee.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="112ee-170">Contact [ForeSee CX Suite Client support team](mailto:support@foresee.com) to get this value.</span></span>

1. <span data-ttu-id="112ee-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="112ee-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_certificate.png)

1. <span data-ttu-id="112ee-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="112ee-173">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/foreseecxsuite-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="112ee-175">To configure single sign-on on **ForeSee CX Suite** side, you need to send the downloaded **Metadata XML** to [ForeSee CX Suite support team](mailto:support@foresee.com).</span><span class="sxs-lookup"><span data-stu-id="112ee-175">To configure single sign-on on **ForeSee CX Suite** side, you need to send the downloaded **Metadata XML** to [ForeSee CX Suite support team](mailto:support@foresee.com).</span></span> <span data-ttu-id="112ee-176">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="112ee-176">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="112ee-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="112ee-177">Create an Azure AD test user</span></span>

<span data-ttu-id="112ee-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="112ee-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="112ee-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="112ee-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="112ee-181">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="112ee-181">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/foreseecxsuite-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="112ee-183">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="112ee-183">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/foreseecxsuite-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="112ee-185">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="112ee-185">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/foreseecxsuite-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="112ee-187">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="112ee-187">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/foreseecxsuite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="112ee-189">a.</span><span class="sxs-lookup"><span data-stu-id="112ee-189">a.</span></span> <span data-ttu-id="112ee-190">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="112ee-190">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="112ee-191">b.</span><span class="sxs-lookup"><span data-stu-id="112ee-191">b.</span></span> <span data-ttu-id="112ee-192">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="112ee-192">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="112ee-193">c.</span><span class="sxs-lookup"><span data-stu-id="112ee-193">c.</span></span> <span data-ttu-id="112ee-194">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="112ee-194">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="112ee-195">d.</span><span class="sxs-lookup"><span data-stu-id="112ee-195">d.</span></span> <span data-ttu-id="112ee-196">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="112ee-196">Click **Create**.</span></span>

### <a name="create-a-foresee-cx-suite-test-user"></a><span data-ttu-id="112ee-197">Create a ForeSee CX Suite test user</span><span class="sxs-lookup"><span data-stu-id="112ee-197">Create a ForeSee CX Suite test user</span></span>

<span data-ttu-id="112ee-198">In this section, you create a user called Britta Simon in ForeSee CX Suite.</span><span class="sxs-lookup"><span data-stu-id="112ee-198">In this section, you create a user called Britta Simon in ForeSee CX Suite.</span></span> <span data-ttu-id="112ee-199">Work with [ForeSee CX Suite support team](mailto:support@foresee.com) to add the users or the domain which is needed to be whitelisted in the ForeSee CX Suite platform.</span><span class="sxs-lookup"><span data-stu-id="112ee-199">Work with [ForeSee CX Suite support team](mailto:support@foresee.com) to add the users or the domain which is needed to be whitelisted in the ForeSee CX Suite platform.</span></span> <span data-ttu-id="112ee-200">If the domain is added by the team, users will get automatically provisioned to the ForeSee CX Suite platform.</span><span class="sxs-lookup"><span data-stu-id="112ee-200">If the domain is added by the team, users will get automatically provisioned to the ForeSee CX Suite platform.</span></span> <span data-ttu-id="112ee-201">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="112ee-201">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="112ee-202">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="112ee-202">Assign the Azure AD test user</span></span>

<span data-ttu-id="112ee-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ForeSee CX Suite.</span><span class="sxs-lookup"><span data-stu-id="112ee-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ForeSee CX Suite.</span></span>

![Assign the user role][200]

<span data-ttu-id="112ee-205">**To assign Britta Simon to ForeSee CX Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="112ee-205">**To assign Britta Simon to ForeSee CX Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="112ee-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="112ee-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="112ee-208">In the applications list, select **ForeSee CX Suite**.</span><span class="sxs-lookup"><span data-stu-id="112ee-208">In the applications list, select **ForeSee CX Suite**.</span></span>

    ![The ForeSee CX Suite link in the Applications list](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_app.png)

1. <span data-ttu-id="112ee-210">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="112ee-210">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="112ee-212">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="112ee-212">Click **Add** button.</span></span> <span data-ttu-id="112ee-213">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="112ee-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="112ee-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="112ee-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="112ee-216">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="112ee-216">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="112ee-217">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="112ee-217">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="112ee-218">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="112ee-218">Test single sign-on</span></span>

<span data-ttu-id="112ee-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="112ee-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="112ee-220">When you click the ForeSee CX Suite tile in the Access Panel, you should get automatically signed-on to your ForeSee CX Suite application.</span><span class="sxs-lookup"><span data-stu-id="112ee-220">When you click the ForeSee CX Suite tile in the Access Panel, you should get automatically signed-on to your ForeSee CX Suite application.</span></span>
<span data-ttu-id="112ee-221">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="112ee-221">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="112ee-222">Additional resources</span><span class="sxs-lookup"><span data-stu-id="112ee-222">Additional resources</span></span>

* [<span data-ttu-id="112ee-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="112ee-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="112ee-224">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="112ee-224">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/foreseecxsuite-tutorial/tutorial_general_01.png
[2]: ./media/foreseecxsuite-tutorial/tutorial_general_02.png
[3]: ./media/foreseecxsuite-tutorial/tutorial_general_03.png
[4]: ./media/foreseecxsuite-tutorial/tutorial_general_04.png

[100]: ./media/foreseecxsuite-tutorial/tutorial_general_100.png

[200]: ./media/foreseecxsuite-tutorial/tutorial_general_200.png
[201]: ./media/foreseecxsuite-tutorial/tutorial_general_201.png
[202]: ./media/foreseecxsuite-tutorial/tutorial_general_202.png
[203]: ./media/foreseecxsuite-tutorial/tutorial_general_203.png

