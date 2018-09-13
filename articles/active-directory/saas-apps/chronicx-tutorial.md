---
title: 'Tutorial: Azure Active Directory integration with ChronicX® | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ChronicX®.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f3f19be6-6ee8-413c-919c-4884ffe685ca
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2018
ms.author: jeedes
ms.openlocfilehash: 51eab8099aee6378893f24e0cea6aa37a4995495
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869601"
---
# <a name="tutorial-azure-active-directory-integration-with-chronicx"></a><span data-ttu-id="a9fa8-103">Tutorial: Azure Active Directory integration with ChronicX®</span><span class="sxs-lookup"><span data-stu-id="a9fa8-103">Tutorial: Azure Active Directory integration with ChronicX®</span></span>

<span data-ttu-id="a9fa8-104">In this tutorial, you learn how to integrate ChronicX® with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9fa8-104">In this tutorial, you learn how to integrate ChronicX® with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9fa8-105">Integrating ChronicX® with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a9fa8-105">Integrating ChronicX® with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9fa8-106">You can control in Azure AD who has access to ChronicX®.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-106">You can control in Azure AD who has access to ChronicX®.</span></span>
- <span data-ttu-id="a9fa8-107">You can enable your users to automatically get signed-on to ChronicX® (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-107">You can enable your users to automatically get signed-on to ChronicX® (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a9fa8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a9fa8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a9fa8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9fa8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9fa8-110">Prerequisites</span></span>

<span data-ttu-id="a9fa8-111">To configure Azure AD integration with ChronicX®, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a9fa8-111">To configure Azure AD integration with ChronicX®, you need the following items:</span></span>

- <span data-ttu-id="a9fa8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a9fa8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9fa8-113">A ChronicX® single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a9fa8-113">A ChronicX® single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9fa8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9fa8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a9fa8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9fa8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9fa8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9fa8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9fa8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a9fa8-118">Scenario description</span></span>
<span data-ttu-id="a9fa8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9fa8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9fa8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9fa8-121">Adding ChronicX® from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9fa8-121">Adding ChronicX® from the gallery</span></span>
1. <span data-ttu-id="a9fa8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9fa8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chronicx-from-the-gallery"></a><span data-ttu-id="a9fa8-123">Adding ChronicX® from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9fa8-123">Adding ChronicX® from the gallery</span></span>
<span data-ttu-id="a9fa8-124">To configure the integration of ChronicX® into Azure AD, you need to add ChronicX® from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-124">To configure the integration of ChronicX® into Azure AD, you need to add ChronicX® from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9fa8-125">**To add ChronicX® from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9fa8-125">**To add ChronicX® from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9fa8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a9fa8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9fa8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a9fa8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a9fa8-133">In the search box, type **ChronicX®**, select **ChronicX®** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-133">In the search box, type **ChronicX®**, select **ChronicX®** from result panel then click **Add** button to add the application.</span></span>

    ![ChronicX® in the results list](./media/chronicx-tutorial/tutorial_chronicx_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a9fa8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9fa8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a9fa8-136">In this section, you configure and test Azure AD single sign-on with ChronicX® based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a9fa8-136">In this section, you configure and test Azure AD single sign-on with ChronicX® based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9fa8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ChronicX® is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ChronicX® is to a user in Azure AD.</span></span> <span data-ttu-id="a9fa8-138">In other words, a link relationship between an Azure AD user and the related user in ChronicX® needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-138">In other words, a link relationship between an Azure AD user and the related user in ChronicX® needs to be established.</span></span>

<span data-ttu-id="a9fa8-139">To configure and test Azure AD single sign-on with ChronicX®, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9fa8-139">To configure and test Azure AD single sign-on with ChronicX®, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9fa8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a9fa8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a9fa8-142">**[Create a ChronicX® test user](#create-a-chronicx®-test-user)** - to have a counterpart of Britta Simon in ChronicX® that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-142">**[Create a ChronicX® test user](#create-a-chronicx®-test-user)** - to have a counterpart of Britta Simon in ChronicX® that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a9fa8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a9fa8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a9fa8-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9fa8-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a9fa8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ChronicX® application.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ChronicX® application.</span></span>

<span data-ttu-id="a9fa8-147">**To configure Azure AD single sign-on with ChronicX®, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9fa8-147">**To configure Azure AD single sign-on with ChronicX®, perform the following steps:**</span></span>

1. <span data-ttu-id="a9fa8-148">In the Azure portal, on the **ChronicX®** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-148">In the Azure portal, on the **ChronicX®** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a9fa8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/chronicx-tutorial/tutorial_chronicx_samlbase.png)

1. <span data-ttu-id="a9fa8-152">On the **ChronicX® Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9fa8-152">On the **ChronicX® Domain and URLs** section, perform the following steps:</span></span>

    ![ChronicX® Domain and URLs single sign-on information](./media/chronicx-tutorial/tutorial_chronicx_url.png)

    <span data-ttu-id="a9fa8-154">a.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-154">a.</span></span> <span data-ttu-id="a9fa8-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.chronicx.com/ups/processlogonSSO.jsp`</span><span class="sxs-lookup"><span data-stu-id="a9fa8-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.chronicx.com/ups/processlogonSSO.jsp`</span></span>

    <span data-ttu-id="a9fa8-156">b.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-156">b.</span></span> <span data-ttu-id="a9fa8-157">In the **Identifier** textbox, type a URL: `ups.chronicx.com`</span><span class="sxs-lookup"><span data-stu-id="a9fa8-157">In the **Identifier** textbox, type a URL: `ups.chronicx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a9fa8-158">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-158">The Sign-on URL value is not real.</span></span> <span data-ttu-id="a9fa8-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="a9fa8-160">Contact [ChronicX® Client support team](https://www.casebank.com/contact-us/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-160">Contact [ChronicX® Client support team](https://www.casebank.com/contact-us/) to get the value.</span></span> 
 
1. <span data-ttu-id="a9fa8-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/chronicx-tutorial/tutorial_chronicx_certificate.png) 

1. <span data-ttu-id="a9fa8-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/chronicx-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a9fa8-165">To configure single sign-on on **ChronicX®** side, you need to send the downloaded **Metadata XML** to [ChronicX® support team](https://www.casebank.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="a9fa8-165">To configure single sign-on on **ChronicX®** side, you need to send the downloaded **Metadata XML** to [ChronicX® support team](https://www.casebank.com/contact-us/).</span></span> <span data-ttu-id="a9fa8-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a9fa8-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9fa8-167">Create an Azure AD test user</span></span>

<span data-ttu-id="a9fa8-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a9fa8-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9fa8-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9fa8-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/chronicx-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a9fa8-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/chronicx-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a9fa8-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/chronicx-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a9fa8-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9fa8-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/chronicx-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a9fa8-179">a.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-179">a.</span></span> <span data-ttu-id="a9fa8-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9fa8-181">b.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-181">b.</span></span> <span data-ttu-id="a9fa8-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a9fa8-183">c.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-183">c.</span></span> <span data-ttu-id="a9fa8-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a9fa8-185">d.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-185">d.</span></span> <span data-ttu-id="a9fa8-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-186">Click **Create**.</span></span>
 
### <a name="create-a-chronicx-test-user"></a><span data-ttu-id="a9fa8-187">Create a ChronicX® test user</span><span class="sxs-lookup"><span data-stu-id="a9fa8-187">Create a ChronicX® test user</span></span>

<span data-ttu-id="a9fa8-188">The objective of this section is to create a user called Britta Simon in ChronicX®.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-188">The objective of this section is to create a user called Britta Simon in ChronicX®.</span></span> <span data-ttu-id="a9fa8-189">ChronicX® supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-189">ChronicX® supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="a9fa8-190">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-190">There is no action item for you in this section.</span></span> <span data-ttu-id="a9fa8-191">A new user is created during an attempt to access ChronicX® if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-191">A new user is created during an attempt to access ChronicX® if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="a9fa8-192">If you need to create a user manually, contact [ChronicX® support team](https://www.casebank.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="a9fa8-192">If you need to create a user manually, contact [ChronicX® support team](https://www.casebank.com/contact-us/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a9fa8-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9fa8-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="a9fa8-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ChronicX®.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ChronicX®.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a9fa8-196">**To assign Britta Simon to ChronicX®, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9fa8-196">**To assign Britta Simon to ChronicX®, perform the following steps:**</span></span>

1. <span data-ttu-id="a9fa8-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a9fa8-199">In the applications list, select **ChronicX®**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-199">In the applications list, select **ChronicX®**.</span></span>

    ![The ChronicX® link in the Applications list](./media/chronicx-tutorial/tutorial_chronicx_app.png)  

1. <span data-ttu-id="a9fa8-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a9fa8-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-203">Click **Add** button.</span></span> <span data-ttu-id="a9fa8-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a9fa8-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a9fa8-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a9fa8-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a9fa8-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9fa8-209">Test single sign-on</span></span>

<span data-ttu-id="a9fa8-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a9fa8-211">When you click the ChronicX® tile in the Access Panel, you should get automatically signed-on to your ChronicX® application.</span><span class="sxs-lookup"><span data-stu-id="a9fa8-211">When you click the ChronicX® tile in the Access Panel, you should get automatically signed-on to your ChronicX® application.</span></span>
<span data-ttu-id="a9fa8-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a9fa8-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a9fa8-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a9fa8-213">Additional resources</span></span>

* [<span data-ttu-id="a9fa8-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9fa8-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a9fa8-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9fa8-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/chronicx-tutorial/tutorial_general_01.png
[2]: ./media/chronicx-tutorial/tutorial_general_02.png
[3]: ./media/chronicx-tutorial/tutorial_general_03.png
[4]: ./media/chronicx-tutorial/tutorial_general_04.png

[100]: ./media/chronicx-tutorial/tutorial_general_100.png

[200]: ./media/chronicx-tutorial/tutorial_general_200.png
[201]: ./media/chronicx-tutorial/tutorial_general_201.png
[202]: ./media/chronicx-tutorial/tutorial_general_202.png
[203]: ./media/chronicx-tutorial/tutorial_general_203.png

