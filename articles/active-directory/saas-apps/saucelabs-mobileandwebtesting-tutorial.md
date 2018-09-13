---
title: 'Tutorial: Azure Active Directory integration with Sauce Labs - Mobile and Web Testing | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Sauce Labs - Mobile and Web Testing.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3142d947-70e5-4345-8a30-b92d8715fac9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2018
ms.author: jeedes
ms.openlocfilehash: 55d84256f408e80600308ede22dbaa903b070d90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867460"
---
# <a name="tutorial-azure-active-directory-integration-with-sauce-labs---mobile-and-web-testing"></a><span data-ttu-id="b1d2e-103">Tutorial: Azure Active Directory integration with Sauce Labs - Mobile and Web Testing</span><span class="sxs-lookup"><span data-stu-id="b1d2e-103">Tutorial: Azure Active Directory integration with Sauce Labs - Mobile and Web Testing</span></span>

<span data-ttu-id="b1d2e-104">In this tutorial, you learn how to integrate Sauce Labs - Mobile and Web Testing with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1d2e-104">In this tutorial, you learn how to integrate Sauce Labs - Mobile and Web Testing with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1d2e-105">Integrating Sauce Labs - Mobile and Web Testing with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b1d2e-105">Integrating Sauce Labs - Mobile and Web Testing with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b1d2e-106">You can control in Azure AD who has access to Sauce Labs - Mobile and Web Testing.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-106">You can control in Azure AD who has access to Sauce Labs - Mobile and Web Testing.</span></span>
- <span data-ttu-id="b1d2e-107">You can enable your users to automatically get signed-on to Sauce Labs - Mobile and Web Testing (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-107">You can enable your users to automatically get signed-on to Sauce Labs - Mobile and Web Testing (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b1d2e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b1d2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1d2e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1d2e-110">Prerequisites</span></span>

<span data-ttu-id="b1d2e-111">To configure Azure AD integration with Sauce Labs - Mobile and Web Testing, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b1d2e-111">To configure Azure AD integration with Sauce Labs - Mobile and Web Testing, you need the following items:</span></span>

- <span data-ttu-id="b1d2e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b1d2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1d2e-113">A Sauce Labs - Mobile and Web Testing single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b1d2e-113">A Sauce Labs - Mobile and Web Testing single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1d2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1d2e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b1d2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1d2e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1d2e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1d2e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1d2e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b1d2e-118">Scenario description</span></span>
<span data-ttu-id="b1d2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1d2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b1d2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1d2e-121">Adding Sauce Labs - Mobile and Web Testing from the gallery</span><span class="sxs-lookup"><span data-stu-id="b1d2e-121">Adding Sauce Labs - Mobile and Web Testing from the gallery</span></span>
2. <span data-ttu-id="b1d2e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b1d2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sauce-labs---mobile-and-web-testing-from-the-gallery"></a><span data-ttu-id="b1d2e-123">Adding Sauce Labs - Mobile and Web Testing from the gallery</span><span class="sxs-lookup"><span data-stu-id="b1d2e-123">Adding Sauce Labs - Mobile and Web Testing from the gallery</span></span>
<span data-ttu-id="b1d2e-124">To configure the integration of Sauce Labs - Mobile and Web Testing into Azure AD, you need to add Sauce Labs - Mobile and Web Testing from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-124">To configure the integration of Sauce Labs - Mobile and Web Testing into Azure AD, you need to add Sauce Labs - Mobile and Web Testing from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b1d2e-125">**To add Sauce Labs - Mobile and Web Testing from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b1d2e-125">**To add Sauce Labs - Mobile and Web Testing from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b1d2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="b1d2e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b1d2e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="b1d2e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="b1d2e-133">In the search box, type **Sauce Labs - Mobile and Web Testing**, select **Sauce Labs - Mobile and Web Testing** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-133">In the search box, type **Sauce Labs - Mobile and Web Testing**, select **Sauce Labs - Mobile and Web Testing** from result panel then click **Add** button to add the application.</span></span>

    ![Sauce Labs - Mobile and Web Testing in the results list](./media/saucelabs-mobileandwebtesting-tutorial/tutorial_saucelabs_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b1d2e-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b1d2e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b1d2e-136">In this section, you configure and test Azure AD single sign-on with Sauce Labs - Mobile and Web Testing based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b1d2e-136">In this section, you configure and test Azure AD single sign-on with Sauce Labs - Mobile and Web Testing based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1d2e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Sauce Labs - Mobile and Web Testing is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Sauce Labs - Mobile and Web Testing is to a user in Azure AD.</span></span> <span data-ttu-id="b1d2e-138">In other words, a link relationship between an Azure AD user and the related user in Sauce Labs - Mobile and Web Testing needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-138">In other words, a link relationship between an Azure AD user and the related user in Sauce Labs - Mobile and Web Testing needs to be established.</span></span>

<span data-ttu-id="b1d2e-139">To configure and test Azure AD single sign-on with Sauce Labs - Mobile and Web Testing, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b1d2e-139">To configure and test Azure AD single sign-on with Sauce Labs - Mobile and Web Testing, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b1d2e-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b1d2e-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1d2e-142">**[Create a Sauce Labs - Mobile and Web Testing test user](#create-a-sauce-labs---mobile-and-web-testing-test-user)** - to have a counterpart of Britta Simon in Sauce Labs - Mobile and Web Testing that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-142">**[Create a Sauce Labs - Mobile and Web Testing test user](#create-a-sauce-labs---mobile-and-web-testing-test-user)** - to have a counterpart of Britta Simon in Sauce Labs - Mobile and Web Testing that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1d2e-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1d2e-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b1d2e-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b1d2e-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b1d2e-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sauce Labs - Mobile and Web Testing application.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sauce Labs - Mobile and Web Testing application.</span></span>

<span data-ttu-id="b1d2e-147">**To configure Azure AD single sign-on with Sauce Labs - Mobile and Web Testing, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b1d2e-147">**To configure Azure AD single sign-on with Sauce Labs - Mobile and Web Testing, perform the following steps:**</span></span>

1. <span data-ttu-id="b1d2e-148">In the Azure portal, on the **Sauce Labs - Mobile and Web Testing** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-148">In the Azure portal, on the **Sauce Labs - Mobile and Web Testing** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="b1d2e-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/saucelabs-mobileandwebtesting-tutorial/tutorial_saucelabs_samlbase.png)

3. <span data-ttu-id="b1d2e-152">On the **Sauce Labs - Mobile and Web Testing Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-152">On the **Sauce Labs - Mobile and Web Testing Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Sauce Labs - Mobile and Web Testing Domain and URLs single sign-on information](./media/saucelabs-mobileandwebtesting-tutorial/tutorial_saucelabs_url.png)

4. <span data-ttu-id="b1d2e-154">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-154">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/saucelabs-mobileandwebtesting-tutorial/tutorial_saucelabs_certificate.png)

5. <span data-ttu-id="b1d2e-156">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-156">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1d2e-158">In a different web browser window, sign in to your Sauce Labs - Mobile and Web Testing company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-158">In a different web browser window, sign in to your Sauce Labs - Mobile and Web Testing company site as an administrator.</span></span>

7. <span data-ttu-id="b1d2e-159">Click on the **User icon** and select **Team Management** tab.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-159">Click on the **User icon** and select **Team Management** tab.</span></span>

    ![Configure Single Sign-On](./media/saucelabs-mobileandwebtesting-tutorial/configure1.png)

8. <span data-ttu-id="b1d2e-161">Enter your **Domain name** in the textbox.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-161">Enter your **Domain name** in the textbox.</span></span>

    ![Configure Single Sign-On](./media/saucelabs-mobileandwebtesting-tutorial/configure2.png)

9. <span data-ttu-id="b1d2e-163">Click **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-163">Click **Configure** tab.</span></span>

    ![Configure Single Sign-On](./media/saucelabs-mobileandwebtesting-tutorial/configure3.png)

10. <span data-ttu-id="b1d2e-165">In the **Configure Single Sign On** section, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-165">In the **Configure Single Sign On** section, perform the following steps.</span></span>

    ![Configure Single Sign-On](./media/saucelabs-mobileandwebtesting-tutorial/configure4.png)

    <span data-ttu-id="b1d2e-167">a.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-167">a.</span></span> <span data-ttu-id="b1d2e-168">Click **Browse** and upload the downloaded metadata file from the Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-168">Click **Browse** and upload the downloaded metadata file from the Azure AD.</span></span>

    <span data-ttu-id="b1d2e-169">b.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-169">b.</span></span> <span data-ttu-id="b1d2e-170">Select the **ALLOW JUST-IN-TIME PROVISIONING** checkbox.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-170">Select the **ALLOW JUST-IN-TIME PROVISIONING** checkbox.</span></span>

    <span data-ttu-id="b1d2e-171">c.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-171">c.</span></span> <span data-ttu-id="b1d2e-172">Clcik **Save**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-172">Clcik **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b1d2e-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b1d2e-173">Create an Azure AD test user</span></span>

<span data-ttu-id="b1d2e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b1d2e-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b1d2e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b1d2e-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/saucelabs-mobileandwebtesting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b1d2e-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/saucelabs-mobileandwebtesting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b1d2e-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/saucelabs-mobileandwebtesting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b1d2e-183">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b1d2e-183">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/saucelabs-mobileandwebtesting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b1d2e-185">a.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-185">a.</span></span> <span data-ttu-id="b1d2e-186">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1d2e-187">b.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-187">b.</span></span> <span data-ttu-id="b1d2e-188">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b1d2e-189">c.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-189">c.</span></span> <span data-ttu-id="b1d2e-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b1d2e-191">d.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-191">d.</span></span> <span data-ttu-id="b1d2e-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-192">Click **Create**.</span></span>
  
### <a name="create-a-sauce-labs---mobile-and-web-testing-test-user"></a><span data-ttu-id="b1d2e-193">Create a Sauce Labs - Mobile and Web Testing test user</span><span class="sxs-lookup"><span data-stu-id="b1d2e-193">Create a Sauce Labs - Mobile and Web Testing test user</span></span>

<span data-ttu-id="b1d2e-194">The objective of this section is to create a user called Britta Simon in Sauce Labs - Mobile and Web Testing.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-194">The objective of this section is to create a user called Britta Simon in Sauce Labs - Mobile and Web Testing.</span></span> <span data-ttu-id="b1d2e-195">Sauce Labs - Mobile and Web Testing supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-195">Sauce Labs - Mobile and Web Testing supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="b1d2e-196">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-196">There is no action item for you in this section.</span></span> <span data-ttu-id="b1d2e-197">A new user is created during an attempt to access Sauce Labs - Mobile and Web Testing if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-197">A new user is created during an attempt to access Sauce Labs - Mobile and Web Testing if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="b1d2e-198">If you need to create a user manually, contact [Sauce Labs - Mobile and Web Testing support team](mailto:support@saucelabs.com).</span><span class="sxs-lookup"><span data-stu-id="b1d2e-198">If you need to create a user manually, contact [Sauce Labs - Mobile and Web Testing support team](mailto:support@saucelabs.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b1d2e-199">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b1d2e-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="b1d2e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sauce Labs - Mobile and Web Testing.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sauce Labs - Mobile and Web Testing.</span></span>

![Assign the user role][200]

<span data-ttu-id="b1d2e-202">**To assign Britta Simon to Sauce Labs - Mobile and Web Testing, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b1d2e-202">**To assign Britta Simon to Sauce Labs - Mobile and Web Testing, perform the following steps:**</span></span>

1. <span data-ttu-id="b1d2e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="b1d2e-205">In the applications list, select **Sauce Labs - Mobile and Web Testing**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-205">In the applications list, select **Sauce Labs - Mobile and Web Testing**.</span></span>

    ![The Sauce Labs - Mobile and Web Testing link in the Applications list](./media/saucelabs-mobileandwebtesting-tutorial/tutorial_saucelabs_app.png)  

3. <span data-ttu-id="b1d2e-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-207">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="b1d2e-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-209">Click **Add** button.</span></span> <span data-ttu-id="b1d2e-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="b1d2e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b1d2e-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1d2e-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="b1d2e-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b1d2e-215">Test single sign-on</span></span>

<span data-ttu-id="b1d2e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b1d2e-217">When you click the Sauce Labs - Mobile and Web Testing tile in the Access Panel, you should get automatically signed-on to your Sauce Labs - Mobile and Web Testing application.</span><span class="sxs-lookup"><span data-stu-id="b1d2e-217">When you click the Sauce Labs - Mobile and Web Testing tile in the Access Panel, you should get automatically signed-on to your Sauce Labs - Mobile and Web Testing application.</span></span>
<span data-ttu-id="b1d2e-218">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2e-218">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1d2e-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b1d2e-219">Additional resources</span></span>

* [<span data-ttu-id="b1d2e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1d2e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b1d2e-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1d2e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_01.png
[2]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_02.png
[3]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_03.png
[4]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_04.png

[100]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_100.png

[200]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_200.png
[201]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_201.png
[202]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_202.png
[203]: ./media/saucelabs-mobileandwebtesting-tutorial/tutorial_general_203.png