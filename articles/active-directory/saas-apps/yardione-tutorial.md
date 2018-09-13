---
title: 'Tutorial: Azure Active Directory integration with YardiOne | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and YardiOne.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 508957f6-caa5-4234-a7f3-90015937e4eb
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: d14cca505f85bdf0d8abd32a954487639fe54631
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869348"
---
# <a name="tutorial-azure-active-directory-integration-with-yardione"></a><span data-ttu-id="9d720-103">Tutorial: Azure Active Directory integration with YardiOne</span><span class="sxs-lookup"><span data-stu-id="9d720-103">Tutorial: Azure Active Directory integration with YardiOne</span></span>

<span data-ttu-id="9d720-104">In this tutorial, you learn how to integrate YardiOne with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d720-104">In this tutorial, you learn how to integrate YardiOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d720-105">Integrating YardiOne with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9d720-105">Integrating YardiOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d720-106">You can control in Azure AD who has access to YardiOne.</span><span class="sxs-lookup"><span data-stu-id="9d720-106">You can control in Azure AD who has access to YardiOne.</span></span>
- <span data-ttu-id="9d720-107">You can enable your users to automatically get signed-on to YardiOne (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="9d720-107">You can enable your users to automatically get signed-on to YardiOne (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9d720-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9d720-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9d720-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9d720-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d720-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9d720-110">Prerequisites</span></span>

<span data-ttu-id="9d720-111">To configure Azure AD integration with YardiOne, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9d720-111">To configure Azure AD integration with YardiOne, you need the following items:</span></span>

- <span data-ttu-id="9d720-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9d720-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d720-113">A YardiOne single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9d720-113">A YardiOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d720-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9d720-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d720-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9d720-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d720-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9d720-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d720-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d720-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d720-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9d720-118">Scenario description</span></span>
<span data-ttu-id="9d720-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9d720-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d720-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9d720-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d720-121">Adding YardiOne from the gallery</span><span class="sxs-lookup"><span data-stu-id="9d720-121">Adding YardiOne from the gallery</span></span>
1. <span data-ttu-id="9d720-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d720-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardione-from-the-gallery"></a><span data-ttu-id="9d720-123">Adding YardiOne from the gallery</span><span class="sxs-lookup"><span data-stu-id="9d720-123">Adding YardiOne from the gallery</span></span>
<span data-ttu-id="9d720-124">To configure the integration of YardiOne into Azure AD, you need to add YardiOne from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9d720-124">To configure the integration of YardiOne into Azure AD, you need to add YardiOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d720-125">**To add YardiOne from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d720-125">**To add YardiOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d720-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9d720-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="9d720-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9d720-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d720-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9d720-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="9d720-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9d720-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="9d720-133">In the search box, type **YardiOne**, select **YardiOne** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9d720-133">In the search box, type **YardiOne**, select **YardiOne** from result panel then click **Add** button to add the application.</span></span>

    ![YardiOne in the results list](./media/yardione-tutorial/tutorial_yardione_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9d720-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d720-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9d720-136">In this section, you configure and test Azure AD single sign-on with YardiOne based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9d720-136">In this section, you configure and test Azure AD single sign-on with YardiOne based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d720-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YardiOne is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d720-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YardiOne is to a user in Azure AD.</span></span> <span data-ttu-id="9d720-138">In other words, a link relationship between an Azure AD user and the related user in YardiOne needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9d720-138">In other words, a link relationship between an Azure AD user and the related user in YardiOne needs to be established.</span></span>

<span data-ttu-id="9d720-139">To configure and test Azure AD single sign-on with YardiOne, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9d720-139">To configure and test Azure AD single sign-on with YardiOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d720-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9d720-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9d720-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d720-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9d720-142">**[Create a YardiOne test user](#create-a-yardione-test-user)** - to have a counterpart of Britta Simon in YardiOne that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9d720-142">**[Create a YardiOne test user](#create-a-yardione-test-user)** - to have a counterpart of Britta Simon in YardiOne that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9d720-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9d720-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9d720-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9d720-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9d720-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d720-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9d720-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YardiOne application.</span><span class="sxs-lookup"><span data-stu-id="9d720-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YardiOne application.</span></span>

<span data-ttu-id="9d720-147">**To configure Azure AD single sign-on with YardiOne, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d720-147">**To configure Azure AD single sign-on with YardiOne, perform the following steps:**</span></span>

1. <span data-ttu-id="9d720-148">In the Azure portal, on the **YardiOne** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9d720-148">In the Azure portal, on the **YardiOne** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="9d720-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9d720-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/yardione-tutorial/tutorial_yardione_samlbase.png)

1. <span data-ttu-id="9d720-152">On the **YardiOne Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9d720-152">On the **YardiOne Domain and URLs** section, perform the following steps:</span></span>

    ![YardiOne Domain and URLs single sign-on information](./media/yardione-tutorial/tutorial_yardione_url.png)

    <span data-ttu-id="9d720-154">a.</span><span class="sxs-lookup"><span data-stu-id="9d720-154">a.</span></span> <span data-ttu-id="9d720-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<y1-subdomain>.yardione.com`</span><span class="sxs-lookup"><span data-stu-id="9d720-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<y1-subdomain>.yardione.com`</span></span>

    <span data-ttu-id="9d720-156">b.</span><span class="sxs-lookup"><span data-stu-id="9d720-156">b.</span></span> <span data-ttu-id="9d720-157">In the **Identifier** textbox, type a URL using the following pattern: `http://<y1-subdomain>.yardione.com/yAuth2/trust`</span><span class="sxs-lookup"><span data-stu-id="9d720-157">In the **Identifier** textbox, type a URL using the following pattern: `http://<y1-subdomain>.yardione.com/yAuth2/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d720-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9d720-158">These values are not real.</span></span> <span data-ttu-id="9d720-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="9d720-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9d720-160">Contact [YardiOne Client support team](https://clientcentral.yardi.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9d720-160">Contact [YardiOne Client support team](https://clientcentral.yardi.com) to get these values.</span></span>
     
1. <span data-ttu-id="9d720-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="9d720-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span> 

    ![The Certificate download link](./media/yardione-tutorial/tutorial_yardione_certificate.png) 
 
1. <span data-ttu-id="9d720-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9d720-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/yardione-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="9d720-165">To configure single sign-on on **YardiOne** side, you need to send the **App Federation Metadata Url** to [YardiOne support team](https://clientcentral.yardi.com).</span><span class="sxs-lookup"><span data-stu-id="9d720-165">To configure single sign-on on **YardiOne** side, you need to send the **App Federation Metadata Url** to [YardiOne support team](https://clientcentral.yardi.com).</span></span> <span data-ttu-id="9d720-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="9d720-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9d720-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9d720-167">Create an Azure AD test user</span></span>

<span data-ttu-id="9d720-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d720-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="9d720-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d720-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d720-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="9d720-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/yardione-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="9d720-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9d720-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/yardione-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="9d720-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9d720-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/yardione-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="9d720-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9d720-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/yardione-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9d720-179">a.</span><span class="sxs-lookup"><span data-stu-id="9d720-179">a.</span></span> <span data-ttu-id="9d720-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d720-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d720-181">b.</span><span class="sxs-lookup"><span data-stu-id="9d720-181">b.</span></span> <span data-ttu-id="9d720-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d720-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9d720-183">c.</span><span class="sxs-lookup"><span data-stu-id="9d720-183">c.</span></span> <span data-ttu-id="9d720-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="9d720-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9d720-185">d.</span><span class="sxs-lookup"><span data-stu-id="9d720-185">d.</span></span> <span data-ttu-id="9d720-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d720-186">Click **Create**.</span></span>
 
### <a name="create-a-yardione-test-user"></a><span data-ttu-id="9d720-187">Create a YardiOne test user</span><span class="sxs-lookup"><span data-stu-id="9d720-187">Create a YardiOne test user</span></span>

<span data-ttu-id="9d720-188">The objective of this section is to create a user called Britta Simon in YardiOne.</span><span class="sxs-lookup"><span data-stu-id="9d720-188">The objective of this section is to create a user called Britta Simon in YardiOne.</span></span> <span data-ttu-id="9d720-189">YardiOne supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="9d720-189">YardiOne supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="9d720-190">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="9d720-190">There is no action item for you in this section.</span></span> <span data-ttu-id="9d720-191">A new user is created during an attempt to access YardiOne if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="9d720-191">A new user is created during an attempt to access YardiOne if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="9d720-192">If you need to create a user manually, contact [YardiOne support team](https://clientcentral.yardi.com).</span><span class="sxs-lookup"><span data-stu-id="9d720-192">If you need to create a user manually, contact [YardiOne support team](https://clientcentral.yardi.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9d720-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9d720-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="9d720-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YardiOne.</span><span class="sxs-lookup"><span data-stu-id="9d720-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YardiOne.</span></span>

![Assign the user role][200] 

<span data-ttu-id="9d720-196">**To assign Britta Simon to YardiOne, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d720-196">**To assign Britta Simon to YardiOne, perform the following steps:**</span></span>

1. <span data-ttu-id="9d720-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9d720-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9d720-199">In the applications list, select **YardiOne**.</span><span class="sxs-lookup"><span data-stu-id="9d720-199">In the applications list, select **YardiOne**.</span></span>

    ![The YardiOne link in the Applications list](./media/yardione-tutorial/tutorial_yardione_app.png)  

1. <span data-ttu-id="9d720-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9d720-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="9d720-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9d720-203">Click **Add** button.</span></span> <span data-ttu-id="9d720-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9d720-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="9d720-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9d720-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9d720-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9d720-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9d720-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9d720-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9d720-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d720-209">Test single sign-on</span></span>

<span data-ttu-id="9d720-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9d720-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d720-211">When you click the YardiOne tile in the Access Panel, you should get automatically signed-on to your YardiOne application.</span><span class="sxs-lookup"><span data-stu-id="9d720-211">When you click the YardiOne tile in the Access Panel, you should get automatically signed-on to your YardiOne application.</span></span>
<span data-ttu-id="9d720-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d720-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9d720-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9d720-213">Additional resources</span></span>

* [<span data-ttu-id="9d720-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d720-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9d720-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d720-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/yardione-tutorial/tutorial_general_01.png
[2]: ./media/yardione-tutorial/tutorial_general_02.png
[3]: ./media/yardione-tutorial/tutorial_general_03.png
[4]: ./media/yardione-tutorial/tutorial_general_04.png

[100]: ./media/yardione-tutorial/tutorial_general_100.png

[200]: ./media/yardione-tutorial/tutorial_general_200.png
[201]: ./media/yardione-tutorial/tutorial_general_201.png
[202]: ./media/yardione-tutorial/tutorial_general_202.png
[203]: ./media/yardione-tutorial/tutorial_general_203.png

