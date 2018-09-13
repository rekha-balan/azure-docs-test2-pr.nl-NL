---
title: 'Tutorial: Azure Active Directory integration with Skills Base | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Skills Base.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 237d90c4-8243-4f80-a305-b5ad9204159e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2018
ms.author: jeedes
ms.openlocfilehash: e11ba8ca9c4ad17b2ade909bb474ad2d1fcf4410
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866211"
---
# <a name="tutorial-azure-active-directory-integration-with-skills-base"></a><span data-ttu-id="7e648-103">Tutorial: Azure Active Directory integration with Skills Base</span><span class="sxs-lookup"><span data-stu-id="7e648-103">Tutorial: Azure Active Directory integration with Skills Base</span></span>

<span data-ttu-id="7e648-104">In this tutorial, you learn how to integrate Skills Base with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e648-104">In this tutorial, you learn how to integrate Skills Base with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e648-105">Integrating Skills Base with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7e648-105">Integrating Skills Base with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7e648-106">You can control in Azure AD who has access to Skills Base.</span><span class="sxs-lookup"><span data-stu-id="7e648-106">You can control in Azure AD who has access to Skills Base.</span></span>
- <span data-ttu-id="7e648-107">You can enable your users to automatically get signed-on to Skills Base (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7e648-107">You can enable your users to automatically get signed-on to Skills Base (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7e648-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7e648-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7e648-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7e648-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e648-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7e648-110">Prerequisites</span></span>

<span data-ttu-id="7e648-111">To configure Azure AD integration with Skills Base, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7e648-111">To configure Azure AD integration with Skills Base, you need the following items:</span></span>

- <span data-ttu-id="7e648-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7e648-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e648-113">A Skills Base single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7e648-113">A Skills Base single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e648-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7e648-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e648-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7e648-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e648-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7e648-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e648-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e648-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e648-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7e648-118">Scenario description</span></span>
<span data-ttu-id="7e648-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7e648-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e648-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7e648-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e648-121">Adding Skills Base from the gallery</span><span class="sxs-lookup"><span data-stu-id="7e648-121">Adding Skills Base from the gallery</span></span>
2. <span data-ttu-id="7e648-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e648-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skills-base-from-the-gallery"></a><span data-ttu-id="7e648-123">Adding Skills Base from the gallery</span><span class="sxs-lookup"><span data-stu-id="7e648-123">Adding Skills Base from the gallery</span></span>
<span data-ttu-id="7e648-124">To configure the integration of Skills Base into Azure AD, you need to add Skills Base from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7e648-124">To configure the integration of Skills Base into Azure AD, you need to add Skills Base from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7e648-125">**To add Skills Base from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e648-125">**To add Skills Base from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7e648-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7e648-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="7e648-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7e648-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7e648-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7e648-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="7e648-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7e648-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="7e648-133">In the search box, type **Skills Base**, select **Skills Base** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7e648-133">In the search box, type **Skills Base**, select **Skills Base** from result panel then click **Add** button to add the application.</span></span>

    ![Skills Base in the results list](./media/skillsbase-tutorial/tutorial_skillsbase_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7e648-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e648-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7e648-136">In this section, you configure and test Azure AD single sign-on with Skills Base based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7e648-136">In this section, you configure and test Azure AD single sign-on with Skills Base based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7e648-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skills Base is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e648-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skills Base is to a user in Azure AD.</span></span> <span data-ttu-id="7e648-138">In other words, a link relationship between an Azure AD user and the related user in Skills Base needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7e648-138">In other words, a link relationship between an Azure AD user and the related user in Skills Base needs to be established.</span></span>

<span data-ttu-id="7e648-139">To configure and test Azure AD single sign-on with Skills Base, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7e648-139">To configure and test Azure AD single sign-on with Skills Base, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7e648-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7e648-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7e648-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e648-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e648-142">**[Create a Skills Base test user](#create-a-skills-base-test-user)** - to have a counterpart of Britta Simon in Skills Base that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7e648-142">**[Create a Skills Base test user](#create-a-skills-base-test-user)** - to have a counterpart of Britta Simon in Skills Base that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e648-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7e648-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e648-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7e648-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7e648-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e648-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7e648-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skills Base application.</span><span class="sxs-lookup"><span data-stu-id="7e648-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skills Base application.</span></span>

<span data-ttu-id="7e648-147">**To configure Azure AD single sign-on with Skills Base, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e648-147">**To configure Azure AD single sign-on with Skills Base, perform the following steps:**</span></span>

1. <span data-ttu-id="7e648-148">In the Azure portal, on the **Skills Base** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7e648-148">In the Azure portal, on the **Skills Base** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="7e648-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7e648-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/skillsbase-tutorial/tutorial_skillsbase_samlbase.png)

3. <span data-ttu-id="7e648-152">On the **Skills Base Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e648-152">On the **Skills Base Domain and URLs** section, perform the following steps:</span></span>

    ![Skills Base Domain and URLs single sign-on information](./media/skillsbase-tutorial/tutorial_skillsbase_url.png)

    <span data-ttu-id="7e648-154">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.skills-base.com/o/<customer-unique-key>`</span><span class="sxs-lookup"><span data-stu-id="7e648-154">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.skills-base.com/o/<customer-unique-key>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7e648-155">You can get the Sign-On URL from Skills Base application.</span><span class="sxs-lookup"><span data-stu-id="7e648-155">You can get the Sign-On URL from Skills Base application.</span></span> <span data-ttu-id="7e648-156">Please login as an Administrator and to go to Admin-> Settings-> Instance details -> Shortcut link.</span><span class="sxs-lookup"><span data-stu-id="7e648-156">Please login as an Administrator and to go to Admin-> Settings-> Instance details -> Shortcut link.</span></span> <span data-ttu-id="7e648-157">Copy the Sign-On URL and paste it in above textbox.</span><span class="sxs-lookup"><span data-stu-id="7e648-157">Copy the Sign-On URL and paste it in above textbox.</span></span>

4. <span data-ttu-id="7e648-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7e648-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/skillsbase-tutorial/tutorial_skillsbase_certificate.png) 

5. <span data-ttu-id="7e648-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7e648-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/skillsbase-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7e648-162">In a different web browser window, login to Skills Base as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="7e648-162">In a different web browser window, login to Skills Base as a Security Administrator.</span></span>

7. <span data-ttu-id="7e648-163">From the left side of menu, under **ADMIN** click **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="7e648-163">From the left side of menu, under **ADMIN** click **Authentication**.</span></span>

    ![The admin](./media/skillsbase-tutorial/tutorial_skillsbase_auth.png)

8. <span data-ttu-id="7e648-165">On the **Authentication** Page, select Single Sign-On as **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="7e648-165">On the **Authentication** Page, select Single Sign-On as **SAML 2**.</span></span>

    ![The single](./media/skillsbase-tutorial/tutorial_skillsbase_single.png)

9. <span data-ttu-id="7e648-167">On the **Authentication** Page, Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e648-167">On the **Authentication** Page, Perform the following steps:</span></span>

    ![The single](./media/skillsbase-tutorial/tutorial_skillsbase_save.png)

    <span data-ttu-id="7e648-169">a.</span><span class="sxs-lookup"><span data-stu-id="7e648-169">a.</span></span> <span data-ttu-id="7e648-170">Click on **Update IdP metadata** button next to **Status** option and paste the contents of Metadata XML that you downloaded from the Azure portal in the specified textbox.</span><span class="sxs-lookup"><span data-stu-id="7e648-170">Click on **Update IdP metadata** button next to **Status** option and paste the contents of Metadata XML that you downloaded from the Azure portal in the specified textbox.</span></span>

    > [!Note]
    > <span data-ttu-id="7e648-171">You can also validate idp metadata through the **Metadata validator** tool as highlighted in screenshot above.</span><span class="sxs-lookup"><span data-stu-id="7e648-171">You can also validate idp metadata through the **Metadata validator** tool as highlighted in screenshot above.</span></span>

    <span data-ttu-id="7e648-172">b.</span><span class="sxs-lookup"><span data-stu-id="7e648-172">b.</span></span> <span data-ttu-id="7e648-173">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7e648-173">Click **Save**.</span></span>
    
### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7e648-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7e648-174">Create an Azure AD test user</span></span>

<span data-ttu-id="7e648-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e648-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7e648-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e648-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7e648-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7e648-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/skillsbase-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7e648-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7e648-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/skillsbase-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7e648-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7e648-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/skillsbase-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7e648-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e648-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/skillsbase-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7e648-186">a.</span><span class="sxs-lookup"><span data-stu-id="7e648-186">a.</span></span> <span data-ttu-id="7e648-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e648-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e648-188">b.</span><span class="sxs-lookup"><span data-stu-id="7e648-188">b.</span></span> <span data-ttu-id="7e648-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e648-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7e648-190">c.</span><span class="sxs-lookup"><span data-stu-id="7e648-190">c.</span></span> <span data-ttu-id="7e648-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7e648-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7e648-192">d.</span><span class="sxs-lookup"><span data-stu-id="7e648-192">d.</span></span> <span data-ttu-id="7e648-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7e648-193">Click **Create**.</span></span>
 
### <a name="create-a-skills-base-test-user"></a><span data-ttu-id="7e648-194">Create a Skills Base test user</span><span class="sxs-lookup"><span data-stu-id="7e648-194">Create a Skills Base test user</span></span>

<span data-ttu-id="7e648-195">The objective of this section is to create a user called Britta Simon in Skills Base.</span><span class="sxs-lookup"><span data-stu-id="7e648-195">The objective of this section is to create a user called Britta Simon in Skills Base.</span></span> <span data-ttu-id="7e648-196">Skills Base supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="7e648-196">Skills Base supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7e648-197">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="7e648-197">There is no action item for you in this section.</span></span> <span data-ttu-id="7e648-198">A new user is created during an attempt to access Skills Base if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="7e648-198">A new user is created during an attempt to access Skills Base if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="7e648-199">If you need to create a user manually, follow the instructions [here](http://wiki.skills-base.net/index.php?title=Adding_people_and_enabling_them_to_log_in).</span><span class="sxs-lookup"><span data-stu-id="7e648-199">If you need to create a user manually, follow the instructions [here](http://wiki.skills-base.net/index.php?title=Adding_people_and_enabling_them_to_log_in).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7e648-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7e648-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="7e648-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skills Base.</span><span class="sxs-lookup"><span data-stu-id="7e648-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skills Base.</span></span>

![Assign the user role][200] 

<span data-ttu-id="7e648-203">**To assign Britta Simon to Skills Base, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e648-203">**To assign Britta Simon to Skills Base, perform the following steps:**</span></span>

1. <span data-ttu-id="7e648-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7e648-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="7e648-206">In the applications list, select **Skills Base**.</span><span class="sxs-lookup"><span data-stu-id="7e648-206">In the applications list, select **Skills Base**.</span></span>

    ![The Skills Base link in the Applications list](./media/skillsbase-tutorial/tutorial_skillsbase_app.png)  

3. <span data-ttu-id="7e648-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7e648-208">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="7e648-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7e648-210">Click **Add** button.</span></span> <span data-ttu-id="7e648-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7e648-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="7e648-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7e648-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7e648-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7e648-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e648-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7e648-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7e648-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e648-216">Test single sign-on</span></span>

<span data-ttu-id="7e648-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7e648-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7e648-218">When you click the Skills Base tile in the Access Panel, you should get automatically signed-on to your Skills Base application.</span><span class="sxs-lookup"><span data-stu-id="7e648-218">When you click the Skills Base tile in the Access Panel, you should get automatically signed-on to your Skills Base application.</span></span>
<span data-ttu-id="7e648-219">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e648-219">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e648-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7e648-220">Additional resources</span></span>

* [<span data-ttu-id="7e648-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e648-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7e648-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e648-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skillsbase-tutorial/tutorial_general_01.png
[2]: ./media/skillsbase-tutorial/tutorial_general_02.png
[3]: ./media/skillsbase-tutorial/tutorial_general_03.png
[4]: ./media/skillsbase-tutorial/tutorial_general_04.png

[100]: ./media/skillsbase-tutorial/tutorial_general_100.png

[200]: ./media/skillsbase-tutorial/tutorial_general_200.png
[201]: ./media/skillsbase-tutorial/tutorial_general_201.png
[202]: ./media/skillsbase-tutorial/tutorial_general_202.png
[203]: ./media/skillsbase-tutorial/tutorial_general_203.png

