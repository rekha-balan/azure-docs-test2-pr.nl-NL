---
title: 'Tutorial: Azure Active Directory integration with Box | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Box.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3b565c8d-35e2-482a-b2f4-bf8fd7d8731f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2018
ms.author: jeedes
ms.openlocfilehash: f5aa724e9848c9794eef093aef15b0aaed9cae97
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857887"
---
# <a name="integrate-azure-active-directory-with-box"></a><span data-ttu-id="99da7-103">Integrate Azure Active Directory with Box</span><span class="sxs-lookup"><span data-stu-id="99da7-103">Integrate Azure Active Directory with Box</span></span>

<span data-ttu-id="99da7-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Box.</span><span class="sxs-lookup"><span data-stu-id="99da7-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Box.</span></span>

<span data-ttu-id="99da7-105">By integrating Azure AD with Box, you get the following benefits:</span><span class="sxs-lookup"><span data-stu-id="99da7-105">By integrating Azure AD with Box, you get the following benefits:</span></span>

- <span data-ttu-id="99da7-106">You can control in Azure AD who has access to Box.</span><span class="sxs-lookup"><span data-stu-id="99da7-106">You can control in Azure AD who has access to Box.</span></span>
- <span data-ttu-id="99da7-107">You can enable your users to get signed in automatically to Box (single sign-on, or SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="99da7-107">You can enable your users to get signed in automatically to Box (single sign-on, or SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="99da7-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="99da7-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="99da7-109">To learn about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="99da7-109">To learn about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99da7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99da7-110">Prerequisites</span></span>

<span data-ttu-id="99da7-111">To configure Azure AD integration with Box, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="99da7-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="99da7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="99da7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99da7-113">A Box SSO-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="99da7-113">A Box SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="99da7-114">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span><span class="sxs-lookup"><span data-stu-id="99da7-114">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span></span>

<span data-ttu-id="99da7-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="99da7-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="99da7-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="99da7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="99da7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99da7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99da7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="99da7-118">Scenario description</span></span>
<span data-ttu-id="99da7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="99da7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="99da7-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="99da7-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99da7-121">Adding Box from the gallery</span><span class="sxs-lookup"><span data-stu-id="99da7-121">Adding Box from the gallery</span></span>
1. <span data-ttu-id="99da7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99da7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-box-from-the-gallery"></a><span data-ttu-id="99da7-123">Add Box from the gallery</span><span class="sxs-lookup"><span data-stu-id="99da7-123">Add Box from the gallery</span></span>
<span data-ttu-id="99da7-124">To configure the integration of Azure AD with Box, add Box from the gallery to your list of managed SaaS apps by doing the following:</span><span class="sxs-lookup"><span data-stu-id="99da7-124">To configure the integration of Azure AD with Box, add Box from the gallery to your list of managed SaaS apps by doing the following:</span></span>

1. <span data-ttu-id="99da7-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99da7-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="99da7-127">Select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="99da7-127">Select **Enterprise applications** > **All applications**.</span></span>

    ![The "Enterprise applications" window][2]
    
1. <span data-ttu-id="99da7-129">To add a new application, select the **New application** button at the top of window.</span><span class="sxs-lookup"><span data-stu-id="99da7-129">To add a new application, select the **New application** button at the top of window.</span></span>

    ![The "New application" button][3]

1. <span data-ttu-id="99da7-131">In the search box, type **Box**, select **Box** in the results list, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="99da7-131">In the search box, type **Box**, select **Box** in the results list, and then select **Add**.</span></span>

    ![Box in the results list](./media/box-tutorial/tutorial_box_search.png)
### <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="99da7-133">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99da7-133">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="99da7-134">In this section, you configure and test Azure AD single sign-on with Box, based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="99da7-134">In this section, you configure and test Azure AD single sign-on with Box, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="99da7-135">For single sign-on to work, Azure AD needs to identify the Box user and its counterpart in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99da7-135">For single sign-on to work, Azure AD needs to identify the Box user and its counterpart in Azure AD.</span></span> <span data-ttu-id="99da7-136">In other words, a link relationship between an Azure AD user and the same user in Box must be established.</span><span class="sxs-lookup"><span data-stu-id="99da7-136">In other words, a link relationship between an Azure AD user and the same user in Box must be established.</span></span>

<span data-ttu-id="99da7-137">To establish the link relationship, assign as the Box *Username* the value of the *user name* in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99da7-137">To establish the link relationship, assign as the Box *Username* the value of the *user name* in Azure AD.</span></span>

<span data-ttu-id="99da7-138">To configure and test Azure AD single sign-on with Box, complete the building blocks in the next five sections.</span><span class="sxs-lookup"><span data-stu-id="99da7-138">To configure and test Azure AD single sign-on with Box, complete the building blocks in the next five sections.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="99da7-139">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99da7-139">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="99da7-140">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="99da7-140">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application by doing the following:</span></span>

1. <span data-ttu-id="99da7-141">In the Azure portal, in the **Box** application integration window, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="99da7-141">In the Azure portal, in the **Box** application integration window, select **Single sign-on**.</span></span>

    ![The "Single sign-on" link][4]

1. <span data-ttu-id="99da7-143">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="99da7-143">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span></span>
 
    ![The "Single sign-on" window](./media/box-tutorial/tutorial_box_samlbase.png)

1. <span data-ttu-id="99da7-145">Under **Box Domain and URLs**, do the following:</span><span class="sxs-lookup"><span data-stu-id="99da7-145">Under **Box Domain and URLs**, do the following:</span></span>

    !["Box Domain and URLs" single sign-on information](./media/box-tutorial/url3.png)

    <span data-ttu-id="99da7-147">a.</span><span class="sxs-lookup"><span data-stu-id="99da7-147">a.</span></span> <span data-ttu-id="99da7-148">In the **Sign-on URL** box, type a URL in the following format: *https://\<subdomain>.box.com*.</span><span class="sxs-lookup"><span data-stu-id="99da7-148">In the **Sign-on URL** box, type a URL in the following format: *https://\<subdomain>.box.com*.</span></span>

    <span data-ttu-id="99da7-149">b.</span><span class="sxs-lookup"><span data-stu-id="99da7-149">b.</span></span> <span data-ttu-id="99da7-150">In the **Identifier** textbox, type **box.net**.</span><span class="sxs-lookup"><span data-stu-id="99da7-150">In the **Identifier** textbox, type **box.net**.</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="99da7-151">The preceding values are not real.</span><span class="sxs-lookup"><span data-stu-id="99da7-151">The preceding values are not real.</span></span> <span data-ttu-id="99da7-152">Update them with the actual sign-on URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="99da7-152">Update them with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="99da7-153">To obtain the values, contact the [Box client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire).</span><span class="sxs-lookup"><span data-stu-id="99da7-153">To obtain the values, contact the [Box client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire).</span></span> 

1. <span data-ttu-id="99da7-154">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="99da7-154">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/box-tutorial/tutorial_box_certificate.png) 

1. <span data-ttu-id="99da7-156">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="99da7-156">Select **Save**.</span></span>

    ![Configure Single Sign-On Save button](./media/box-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="99da7-158">To configure SSO for your application, follow the procedure in [Set up SSO on your own](https://community.box.com/t5/How-to-Guides-for-Admins/Setting-Up-Single-Sign-On-SSO-for-your-Enterprise/ta-p/1263#ssoonyourown).</span><span class="sxs-lookup"><span data-stu-id="99da7-158">To configure SSO for your application, follow the procedure in [Set up SSO on your own](https://community.box.com/t5/How-to-Guides-for-Admins/Setting-Up-Single-Sign-On-SSO-for-your-Enterprise/ta-p/1263#ssoonyourown).</span></span>

> [!NOTE] 
> <span data-ttu-id="99da7-159">If you cannot enable the SSO settings for your Box account, you might need to contact the [Box client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide the downloaded XML file.</span><span class="sxs-lookup"><span data-stu-id="99da7-159">If you cannot enable the SSO settings for your Box account, you might need to contact the [Box client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="99da7-160">As you're setting up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="99da7-160">As you're setting up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="99da7-161">After you've added the app in the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation in the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="99da7-161">After you've added the app in the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation in the **Configuration** section at the bottom.</span></span> <span data-ttu-id="99da7-162">For more information about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="99da7-162">For more information about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="99da7-163">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99da7-163">Create an Azure AD test user</span></span>

<span data-ttu-id="99da7-164">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span><span class="sxs-lookup"><span data-stu-id="99da7-164">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Create an Azure AD test user][100]

1. <span data-ttu-id="99da7-166">In the Azure portal, in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99da7-166">In the Azure portal, in the left pane, select **Azure Active Directory**.</span></span>

    ![The Azure Active Directory link](./media/box-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="99da7-168">To display a list of current users, select **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="99da7-168">To display a list of current users, select **Users and groups** > **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/box-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="99da7-170">At the top of the **All Users** window, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="99da7-170">At the top of the **All Users** window, select **Add**.</span></span>

    ![The Add button](./media/box-tutorial/create_aaduser_03.png)

    <span data-ttu-id="99da7-172">The **User** window opens.</span><span class="sxs-lookup"><span data-stu-id="99da7-172">The **User** window opens.</span></span>

1. <span data-ttu-id="99da7-173">In the **User** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="99da7-173">In the **User** window, do the following:</span></span>

    ![The User window](./media/box-tutorial/create_aaduser_04.png)

    <span data-ttu-id="99da7-175">a.</span><span class="sxs-lookup"><span data-stu-id="99da7-175">a.</span></span> <span data-ttu-id="99da7-176">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99da7-176">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99da7-177">b.</span><span class="sxs-lookup"><span data-stu-id="99da7-177">b.</span></span> <span data-ttu-id="99da7-178">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99da7-178">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="99da7-179">c.</span><span class="sxs-lookup"><span data-stu-id="99da7-179">c.</span></span> <span data-ttu-id="99da7-180">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="99da7-180">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="99da7-181">d.</span><span class="sxs-lookup"><span data-stu-id="99da7-181">d.</span></span> <span data-ttu-id="99da7-182">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="99da7-182">Select **Create**.</span></span>
 
### <a name="create-a-box-test-user"></a><span data-ttu-id="99da7-183">Create a Box test user</span><span class="sxs-lookup"><span data-stu-id="99da7-183">Create a Box test user</span></span>

<span data-ttu-id="99da7-184">In this section, you create test user Britta Simon in Box.</span><span class="sxs-lookup"><span data-stu-id="99da7-184">In this section, you create test user Britta Simon in Box.</span></span> <span data-ttu-id="99da7-185">Box supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="99da7-185">Box supports just-in-time provisioning, which is enabled by default.</span></span> <span data-ttu-id="99da7-186">If a user doesn't already exist, a new one is created when you attempt to access Box.</span><span class="sxs-lookup"><span data-stu-id="99da7-186">If a user doesn't already exist, a new one is created when you attempt to access Box.</span></span> <span data-ttu-id="99da7-187">No action is required from you to create the user.</span><span class="sxs-lookup"><span data-stu-id="99da7-187">No action is required from you to create the user.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="99da7-188">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99da7-188">Assign the Azure AD test user</span></span>

<span data-ttu-id="99da7-189">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Box.</span><span class="sxs-lookup"><span data-stu-id="99da7-189">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Box.</span></span> <span data-ttu-id="99da7-190">To do so, do the following:</span><span class="sxs-lookup"><span data-stu-id="99da7-190">To do so, do the following:</span></span>

![Assign the user role][200]

1. <span data-ttu-id="99da7-192">In the Azure portal, open the **Applications** view, go to the **Directory** view, and then select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="99da7-192">In the Azure portal, open the **Applications** view, go to the **Directory** view, and then select **Enterprise applications** > **All applications**.</span></span>

    ![The "Enterprise applications" and "All applications" links][201] 

1. <span data-ttu-id="99da7-194">In the **Applications** list, select **Box**.</span><span class="sxs-lookup"><span data-stu-id="99da7-194">In the **Applications** list, select **Box**.</span></span>

    ![The Box link](./media/box-tutorial/tutorial_box_app.png)  

1. <span data-ttu-id="99da7-196">In the left pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="99da7-196">In the left pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="99da7-198">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="99da7-198">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="99da7-200">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99da7-200">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span></span>

1. <span data-ttu-id="99da7-201">Select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="99da7-201">Select the **Select** button.</span></span>

1. <span data-ttu-id="99da7-202">In the **Add Assignment** window, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="99da7-202">In the **Add Assignment** window, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="99da7-203">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="99da7-203">Test single sign-on</span></span>

<span data-ttu-id="99da7-204">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="99da7-204">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="99da7-205">When you select the **Box** tile in the Access Panel, you open the sign-in page for signing in to your Box application.</span><span class="sxs-lookup"><span data-stu-id="99da7-205">When you select the **Box** tile in the Access Panel, you open the sign-in page for signing in to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99da7-206">Additional resources</span><span class="sxs-lookup"><span data-stu-id="99da7-206">Additional resources</span></span>

* [<span data-ttu-id="99da7-207">List of tutorials about integrating SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99da7-207">List of tutorials about integrating SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="99da7-208">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99da7-208">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="99da7-209">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="99da7-209">Configure user provisioning</span></span>](box-userprovisioning-tutorial.md)



<!--Image references-->

[1]: ./media/box-tutorial/tutorial_general_01.png
[2]: ./media/box-tutorial/tutorial_general_02.png
[3]: ./media/box-tutorial/tutorial_general_03.png
[4]: ./media/box-tutorial/tutorial_general_04.png

[100]: ./media/box-tutorial/tutorial_general_100.png

[200]: ./media/box-tutorial/tutorial_general_200.png
[201]: ./media/box-tutorial/tutorial_general_201.png
[202]: ./media/box-tutorial/tutorial_general_202.png
[203]: ./media/box-tutorial/tutorial_general_203.png

