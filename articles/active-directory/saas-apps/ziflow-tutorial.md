---
title: 'Tutorial: Azure Active Directory integration with Ziflow | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Ziflow.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 84e60fa4-36fb-49c4-a642-95538c78f926
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2018
ms.author: jeedes
ms.openlocfilehash: 460a52f240f6b3723f93e81a11a8cd1ccc6c30c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868864"
---
# <a name="tutorial-azure-active-directory-integration-with-ziflow"></a><span data-ttu-id="5076a-103">Tutorial: Azure Active Directory integration with Ziflow</span><span class="sxs-lookup"><span data-stu-id="5076a-103">Tutorial: Azure Active Directory integration with Ziflow</span></span>

<span data-ttu-id="5076a-104">In this tutorial, you learn how to integrate Ziflow with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5076a-104">In this tutorial, you learn how to integrate Ziflow with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5076a-105">Integrating Ziflow with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5076a-105">Integrating Ziflow with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5076a-106">You can control in Azure AD who has access to Ziflow.</span><span class="sxs-lookup"><span data-stu-id="5076a-106">You can control in Azure AD who has access to Ziflow.</span></span>
- <span data-ttu-id="5076a-107">You can enable your users to automatically get signed-on to Ziflow (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="5076a-107">You can enable your users to automatically get signed-on to Ziflow (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5076a-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5076a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5076a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="5076a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5076a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5076a-110">Prerequisites</span></span>

<span data-ttu-id="5076a-111">To configure Azure AD integration with Ziflow, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5076a-111">To configure Azure AD integration with Ziflow, you need the following items:</span></span>

- <span data-ttu-id="5076a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5076a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5076a-113">A Ziflow single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5076a-113">A Ziflow single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5076a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5076a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5076a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5076a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5076a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="5076a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5076a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5076a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5076a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5076a-118">Scenario description</span></span>
<span data-ttu-id="5076a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5076a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5076a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5076a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5076a-121">Adding Ziflow from the gallery</span><span class="sxs-lookup"><span data-stu-id="5076a-121">Adding Ziflow from the gallery</span></span>
2. <span data-ttu-id="5076a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5076a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ziflow-from-the-gallery"></a><span data-ttu-id="5076a-123">Adding Ziflow from the gallery</span><span class="sxs-lookup"><span data-stu-id="5076a-123">Adding Ziflow from the gallery</span></span>
<span data-ttu-id="5076a-124">To configure the integration of Ziflow into Azure AD, you need to add Ziflow from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5076a-124">To configure the integration of Ziflow into Azure AD, you need to add Ziflow from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5076a-125">**To add Ziflow from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5076a-125">**To add Ziflow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5076a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5076a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="5076a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5076a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5076a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5076a-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="5076a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="5076a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="5076a-133">In the search box, type **Ziflow**, select **Ziflow** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5076a-133">In the search box, type **Ziflow**, select **Ziflow** from result panel then click **Add** button to add the application.</span></span>

    ![Ziflow in the results list](./media/ziflow-tutorial/tutorial_ziflow_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5076a-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5076a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5076a-136">In this section, you configure and test Azure AD single sign-on with Ziflow based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5076a-136">In this section, you configure and test Azure AD single sign-on with Ziflow based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5076a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ziflow is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5076a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ziflow is to a user in Azure AD.</span></span> <span data-ttu-id="5076a-138">In other words, a link relationship between an Azure AD user and the related user in Ziflow needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5076a-138">In other words, a link relationship between an Azure AD user and the related user in Ziflow needs to be established.</span></span>

<span data-ttu-id="5076a-139">To configure and test Azure AD single sign-on with Ziflow, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5076a-139">To configure and test Azure AD single sign-on with Ziflow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5076a-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5076a-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5076a-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5076a-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5076a-142">**[Create a Ziflow test user](#create-a-ziflow-test-user)** - to have a counterpart of Britta Simon in Ziflow that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="5076a-142">**[Create a Ziflow test user](#create-a-ziflow-test-user)** - to have a counterpart of Britta Simon in Ziflow that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5076a-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5076a-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5076a-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5076a-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5076a-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5076a-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5076a-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ziflow application.</span><span class="sxs-lookup"><span data-stu-id="5076a-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ziflow application.</span></span>

<span data-ttu-id="5076a-147">**To configure Azure AD single sign-on with Ziflow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5076a-147">**To configure Azure AD single sign-on with Ziflow, perform the following steps:**</span></span>

1. <span data-ttu-id="5076a-148">In the Azure portal, on the **Ziflow** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5076a-148">In the Azure portal, on the **Ziflow** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="5076a-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5076a-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/ziflow-tutorial/tutorial_ziflow_samlbase.png)

3. <span data-ttu-id="5076a-152">On the **Ziflow Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5076a-152">On the **Ziflow Domain and URLs** section, perform the following steps:</span></span>

    ![Ziflow Domain and URLs single sign-on information](./media/ziflow-tutorial/tutorial_ziflow_url.png)

    <span data-ttu-id="5076a-154">a.</span><span class="sxs-lookup"><span data-stu-id="5076a-154">a.</span></span> <span data-ttu-id="5076a-155">In the **Sign on URL** textbox, type a URL using the following pattern: `https://ziflow-production.auth0.com/login/callback?connection=<UniqueID>`</span><span class="sxs-lookup"><span data-stu-id="5076a-155">In the **Sign on URL** textbox, type a URL using the following pattern: `https://ziflow-production.auth0.com/login/callback?connection=<UniqueID>`</span></span>

    <span data-ttu-id="5076a-156">b.</span><span class="sxs-lookup"><span data-stu-id="5076a-156">b.</span></span> <span data-ttu-id="5076a-157">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:ziflow-production:<UniqueID>`</span><span class="sxs-lookup"><span data-stu-id="5076a-157">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:ziflow-production:<UniqueID>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="5076a-158">The preceding values are not real.</span><span class="sxs-lookup"><span data-stu-id="5076a-158">The preceding values are not real.</span></span> <span data-ttu-id="5076a-159">You will update the unique ID value in the Identifier and Sign on URL with  actual value, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="5076a-159">You will update the unique ID value in the Identifier and Sign on URL with  actual value, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="5076a-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5076a-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/ziflow-tutorial/tutorial_ziflow_certificate.png) 

5. <span data-ttu-id="5076a-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5076a-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/ziflow-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5076a-164">On the **Ziflow Configuration** section, click **Configure Ziflow** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="5076a-164">On the **Ziflow Configuration** section, click **Configure Ziflow** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5076a-165">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="5076a-165">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Ziflow Configuration](./media/ziflow-tutorial/tutorial_ziflow_configure.png) 

7. <span data-ttu-id="5076a-167">In a different web browser window, login to Ziflow as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="5076a-167">In a different web browser window, login to Ziflow as a Security Administrator.</span></span>

8. <span data-ttu-id="5076a-168">Click on Avatar in the top right corner, and then click **Manage account**.</span><span class="sxs-lookup"><span data-stu-id="5076a-168">Click on Avatar in the top right corner, and then click **Manage account**.</span></span>

    ![Ziflow Configuration Manage](./media/ziflow-tutorial/tutorial_ziflow_manage.png)

9. <span data-ttu-id="5076a-170">In the top left, click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5076a-170">In the top left, click **Single Sign-On**.</span></span>

    ![Ziflow Configuration Sign](./media/ziflow-tutorial/tutorial_ziflow_signon.png)

10. <span data-ttu-id="5076a-172">On the **Single Sign-On** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5076a-172">On the **Single Sign-On** page, perform the following steps:</span></span>

    ![Ziflow Configuration Single](./media/ziflow-tutorial/tutorial_ziflow_page.png)

    <span data-ttu-id="5076a-174">a.</span><span class="sxs-lookup"><span data-stu-id="5076a-174">a.</span></span> <span data-ttu-id="5076a-175">Select **Type** as **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="5076a-175">Select **Type** as **SAML2.0**.</span></span>

    <span data-ttu-id="5076a-176">b.</span><span class="sxs-lookup"><span data-stu-id="5076a-176">b.</span></span> <span data-ttu-id="5076a-177">In the **Sign In URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5076a-177">In the **Sign In URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="5076a-178">c.</span><span class="sxs-lookup"><span data-stu-id="5076a-178">c.</span></span> <span data-ttu-id="5076a-179">Upload the base-64 encoded certificate that you have downloaded from the Azure portal, into the **X509 Signing Certificate**.</span><span class="sxs-lookup"><span data-stu-id="5076a-179">Upload the base-64 encoded certificate that you have downloaded from the Azure portal, into the **X509 Signing Certificate**.</span></span>

    <span data-ttu-id="5076a-180">d.</span><span class="sxs-lookup"><span data-stu-id="5076a-180">d.</span></span> <span data-ttu-id="5076a-181">In the **Sign Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5076a-181">In the **Sign Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="5076a-182">e.</span><span class="sxs-lookup"><span data-stu-id="5076a-182">e.</span></span> <span data-ttu-id="5076a-183">From the **Configuration Settings for your Identifier Provider** section, copy the highlighted unique ID value and append it with the Identifier and Sign on URL in the **Ziflow Domain and URLs section** on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5076a-183">From the **Configuration Settings for your Identifier Provider** section, copy the highlighted unique ID value and append it with the Identifier and Sign on URL in the **Ziflow Domain and URLs section** on Azure portal.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5076a-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5076a-184">Create an Azure AD test user</span></span>

<span data-ttu-id="5076a-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5076a-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="5076a-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5076a-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5076a-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="5076a-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/ziflow-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5076a-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5076a-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/ziflow-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5076a-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="5076a-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/ziflow-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5076a-194">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5076a-194">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/ziflow-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5076a-196">a.</span><span class="sxs-lookup"><span data-stu-id="5076a-196">a.</span></span> <span data-ttu-id="5076a-197">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5076a-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5076a-198">b.</span><span class="sxs-lookup"><span data-stu-id="5076a-198">b.</span></span> <span data-ttu-id="5076a-199">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5076a-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5076a-200">c.</span><span class="sxs-lookup"><span data-stu-id="5076a-200">c.</span></span> <span data-ttu-id="5076a-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="5076a-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5076a-202">d.</span><span class="sxs-lookup"><span data-stu-id="5076a-202">d.</span></span> <span data-ttu-id="5076a-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5076a-203">Click **Create**.</span></span>
  
### <a name="create-a-ziflow-test-user"></a><span data-ttu-id="5076a-204">Create a Ziflow test user</span><span class="sxs-lookup"><span data-stu-id="5076a-204">Create a Ziflow test user</span></span>

<span data-ttu-id="5076a-205">To enable Azure AD users to log in to Ziflow, they must be provisioned into Ziflow.</span><span class="sxs-lookup"><span data-stu-id="5076a-205">To enable Azure AD users to log in to Ziflow, they must be provisioned into Ziflow.</span></span> <span data-ttu-id="5076a-206">In Ziflow, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="5076a-206">In Ziflow, provisioning is a manual task.</span></span>

<span data-ttu-id="5076a-207">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5076a-207">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="5076a-208">Log in to Ziflow as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="5076a-208">Log in to Ziflow as a Security Administrator.</span></span>

2. <span data-ttu-id="5076a-209">Navigate to **People** on the top.</span><span class="sxs-lookup"><span data-stu-id="5076a-209">Navigate to **People** on the top.</span></span>

    ![Ziflow Configuration people](./media/ziflow-tutorial/tutorial_ziflow_people.png)

3. <span data-ttu-id="5076a-211">Click **Add** and then click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="5076a-211">Click **Add** and then click **Add user**.</span></span>

    ![Ziflow Configuration adding user](./media/ziflow-tutorial/tutorial_ziflow_add.png)

4. <span data-ttu-id="5076a-213">On the **Add a user** popup, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5076a-213">On the **Add a user** popup, perform the following steps:</span></span>

    ![Ziflow Configuration adding user](./media/ziflow-tutorial/tutorial_ziflow_adduser.png)

    <span data-ttu-id="5076a-215">a.</span><span class="sxs-lookup"><span data-stu-id="5076a-215">a.</span></span> <span data-ttu-id="5076a-216">In **Email** text box, enter the email of user like brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5076a-216">In **Email** text box, enter the email of user like brittasimon@contoso.com.</span></span>

    <span data-ttu-id="5076a-217">b.</span><span class="sxs-lookup"><span data-stu-id="5076a-217">b.</span></span> <span data-ttu-id="5076a-218">In **First name** text box, enter the first name of user like Britta.</span><span class="sxs-lookup"><span data-stu-id="5076a-218">In **First name** text box, enter the first name of user like Britta.</span></span>

    <span data-ttu-id="5076a-219">c.</span><span class="sxs-lookup"><span data-stu-id="5076a-219">c.</span></span> <span data-ttu-id="5076a-220">In **Last name** text box, enter the last name of user like Simon.</span><span class="sxs-lookup"><span data-stu-id="5076a-220">In **Last name** text box, enter the last name of user like Simon.</span></span>

    <span data-ttu-id="5076a-221">d.</span><span class="sxs-lookup"><span data-stu-id="5076a-221">d.</span></span> <span data-ttu-id="5076a-222">Select your Ziflow role.</span><span class="sxs-lookup"><span data-stu-id="5076a-222">Select your Ziflow role.</span></span>

    <span data-ttu-id="5076a-223">e.</span><span class="sxs-lookup"><span data-stu-id="5076a-223">e.</span></span> <span data-ttu-id="5076a-224">Click **Add 1 user**.</span><span class="sxs-lookup"><span data-stu-id="5076a-224">Click **Add 1 user**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5076a-225">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="5076a-225">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5076a-226">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5076a-226">Assign the Azure AD test user</span></span>

<span data-ttu-id="5076a-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ziflow.</span><span class="sxs-lookup"><span data-stu-id="5076a-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ziflow.</span></span>

![Assign the user role][200] 

<span data-ttu-id="5076a-229">**To assign Britta Simon to Ziflow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5076a-229">**To assign Britta Simon to Ziflow, perform the following steps:**</span></span>

1. <span data-ttu-id="5076a-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5076a-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="5076a-232">In the applications list, select **Ziflow**.</span><span class="sxs-lookup"><span data-stu-id="5076a-232">In the applications list, select **Ziflow**.</span></span>

    ![The Ziflow link in the Applications list](./media/ziflow-tutorial/tutorial_ziflow_app.png)  

3. <span data-ttu-id="5076a-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5076a-234">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="5076a-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5076a-236">Click **Add** button.</span></span> <span data-ttu-id="5076a-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5076a-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="5076a-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5076a-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5076a-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5076a-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5076a-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5076a-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5076a-242">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="5076a-242">Test single sign-on</span></span>

<span data-ttu-id="5076a-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5076a-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5076a-244">When you click the Ziflow tile in the Access Panel, you should get automatically signed-on to your Ziflow application.</span><span class="sxs-lookup"><span data-stu-id="5076a-244">When you click the Ziflow tile in the Access Panel, you should get automatically signed-on to your Ziflow application.</span></span>
<span data-ttu-id="5076a-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5076a-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5076a-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5076a-246">Additional resources</span></span>

* [<span data-ttu-id="5076a-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5076a-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="5076a-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5076a-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ziflow-tutorial/tutorial_general_01.png
[2]: ./media/ziflow-tutorial/tutorial_general_02.png
[3]: ./media/ziflow-tutorial/tutorial_general_03.png
[4]: ./media/ziflow-tutorial/tutorial_general_04.png

[100]: ./media/ziflow-tutorial/tutorial_general_100.png

[200]: ./media/ziflow-tutorial/tutorial_general_200.png
[201]: ./media/ziflow-tutorial/tutorial_general_201.png
[202]: ./media/ziflow-tutorial/tutorial_general_202.png
[203]: ./media/ziflow-tutorial/tutorial_general_203.png

